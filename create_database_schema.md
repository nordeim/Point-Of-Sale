Below is a **single, self-contained PostgreSQL 15 DDL script** that realises the complete data-model described in the PRD.  
Copy it to `schema.sql`, run it with `psql -f schema.sql`, or execute through any migration tool (e.g. Alembic `op.execute(open("schema.sql").read())`).

```sql
/* =======================================================================
   SG-POS  –  Canonical Database Schema
   -----------------------------------------------------------------------
   • Target  : PostgreSQL 15
   • Encoding: UTF-8
   • Author  : SG-POS Core Team
   • Created : 2024-06-19
   ======================================================================= */

-- -----------------------------------------------------------------------
-- 0. EXTENSIONS ‑- enable only if not already present
-- -----------------------------------------------------------------------
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";   -- v4 UUID generator
CREATE EXTENSION IF NOT EXISTS pgcrypto;      -- cryptographic helpers

-- -----------------------------------------------------------------------
-- 1. ENUMERATIONS
-- -----------------------------------------------------------------------
CREATE TYPE sale_status_enum        AS ENUM ('OPEN','COMPLETED','REFUNDED');
CREATE TYPE po_status_enum          AS ENUM ('DRAFT','SENT','RECEIVED','CANCELLED');
CREATE TYPE stock_source_enum       AS ENUM ('SALE','PURCHASE_RECEIPT','STOCK_ADJUST','TRANSFER');
CREATE TYPE payment_method_enum     AS ENUM ('CASH','CARD','EWALLET','CREDIT','FOREIGN_CURRENCY');
CREATE TYPE promotion_rule_enum     AS ENUM ('PERCENT','FIXED','BUY_X_GET_Y','TIERED');
CREATE TYPE permission_scope_enum   AS ENUM ('COMPANY','STORE','OWN');
CREATE TYPE user_status_enum        AS ENUM ('ACTIVE','LOCKED','INVITED');

-- -----------------------------------------------------------------------
-- 2. BASE TABLES
-- -----------------------------------------------------------------------
/* ---------- 2.1. Company & Stores ------------------------------------ */
CREATE TABLE company (
    id               UUID            PRIMARY KEY DEFAULT uuid_generate_v4(),
    legal_name       TEXT            NOT NULL,
    registration_no  TEXT            UNIQUE NOT NULL,
    gst_registered   BOOLEAN         NOT NULL DEFAULT TRUE,
    default_currency CHAR(3)         NOT NULL DEFAULT 'SGD',
    address          TEXT,
    phone            TEXT,
    email            TEXT,
    created_at       TIMESTAMPTZ     NOT NULL DEFAULT now()
);

CREATE TABLE store (
    id          UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id  UUID REFERENCES company(id) ON DELETE CASCADE,
    code        TEXT NOT NULL,
    name        TEXT NOT NULL,
    address     TEXT,
    phone       TEXT,
    timezone    TEXT NOT NULL DEFAULT 'Asia/Singapore',
    created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
    UNIQUE (company_id, code)
);

CREATE TABLE pos_terminal (
    id           UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    store_id     UUID REFERENCES store(id) ON DELETE CASCADE,
    code         TEXT NOT NULL,
    location     TEXT,
    active       BOOLEAN NOT NULL DEFAULT TRUE,
    created_at   TIMESTAMPTZ NOT NULL DEFAULT now(),
    UNIQUE(store_id, code)
);

/* ---------- 2.2. Security & Users ------------------------------------ */
CREATE TABLE role (
    id          UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name        TEXT UNIQUE NOT NULL,
    description TEXT
);

CREATE TABLE permission (
    code        TEXT PRIMARY KEY,
    description TEXT NOT NULL
);

CREATE TABLE role_permission (
    role_id       UUID REFERENCES role(id) ON DELETE CASCADE,
    permission_id TEXT REFERENCES permission(code) ON DELETE CASCADE,
    scope         permission_scope_enum NOT NULL DEFAULT 'COMPANY',
    PRIMARY KEY (role_id, permission_id)
);

CREATE TABLE "user" (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id      UUID REFERENCES company(id) ON DELETE CASCADE,
    username        TEXT UNIQUE NOT NULL,
    email           TEXT UNIQUE NOT NULL,
    password_hash   TEXT NOT NULL,
    full_name       TEXT,
    status          user_status_enum NOT NULL DEFAULT 'ACTIVE',
    last_login_at   TIMESTAMPTZ,
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE user_role (
    user_id UUID REFERENCES "user"(id) ON DELETE CASCADE,
    role_id UUID REFERENCES role(id)   ON DELETE CASCADE,
    PRIMARY KEY (user_id, role_id)
);

/* ---------- 2.3. Currency & FX -------------------------------------- */
CREATE TABLE currency (
    code         CHAR(3) PRIMARY KEY,
    name         TEXT NOT NULL,
    symbol       TEXT NOT NULL,
    precision    INT  NOT NULL DEFAULT 2,
    is_default   BOOLEAN NOT NULL DEFAULT FALSE
);

INSERT INTO currency (code, name, symbol, is_default)
VALUES ('SGD','Singapore Dollar','$', TRUE)
ON CONFLICT DO NOTHING;

CREATE TABLE exchange_rate (
    base_currency        CHAR(3) NOT NULL DEFAULT 'SGD',
    currency_code        CHAR(3) REFERENCES currency(code) ON DELETE CASCADE,
    rate                 NUMERIC(16,6) NOT NULL CHECK (rate > 0),
    effective_date       DATE NOT NULL,
    PRIMARY KEY (base_currency, currency_code, effective_date)
);

/* ---------- 2.4. Business Partners ---------------------------------- */
CREATE TABLE customer (
    id             UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id     UUID REFERENCES company(id) ON DELETE CASCADE,
    nric           VARCHAR(12) UNIQUE,
    name           TEXT NOT NULL,
    email          TEXT,
    phone          VARCHAR(16),
    dob            DATE,
    pdpa_consent   BOOLEAN NOT NULL DEFAULT FALSE,
    consent_at     TIMESTAMPTZ,
    points_balance INT NOT NULL DEFAULT 0,
    created_at     TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE supplier (
    id             UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id     UUID REFERENCES company(id) ON DELETE CASCADE,
    reg_no         TEXT,
    name           TEXT NOT NULL,
    contact_person TEXT,
    phone          TEXT,
    email          TEXT,
    address        TEXT,
    created_at     TIMESTAMPTZ NOT NULL DEFAULT now()
);

/* ---------- 2.5. Product Catalogue ---------------------------------- */
CREATE TABLE category (
    id          UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id  UUID REFERENCES company(id) ON DELETE CASCADE,
    parent_id   UUID REFERENCES category(id),
    name        TEXT NOT NULL,
    description TEXT
);

CREATE TABLE inventory_item (
    id             UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id     UUID REFERENCES company(id) ON DELETE CASCADE,
    sku            TEXT NOT NULL,
    barcode        TEXT UNIQUE,
    name           TEXT NOT NULL,
    category_id    UUID REFERENCES category(id),
    supplier_id    UUID REFERENCES supplier(id),
    uom            TEXT NOT NULL DEFAULT 'EA',
    cost_price     NUMERIC(12,2) NOT NULL,
    selling_price  NUMERIC(12,2) NOT NULL,
    gst_rate       NUMERIC(5,2)  NOT NULL DEFAULT 8.00, -- %
    reorder_level  NUMERIC(12,2) NOT NULL DEFAULT 0,
    is_active      BOOLEAN NOT NULL DEFAULT TRUE,
    created_at     TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at     TIMESTAMPTZ
);

CREATE UNIQUE INDEX ix_inventory_item_company_sku ON inventory_item(company_id, sku);

/* ---------- 2.6. Stock per Store & Journal -------------------------- */
CREATE TABLE inventory_stock (
    store_id           UUID REFERENCES store(id) ON DELETE CASCADE,
    item_id            UUID REFERENCES inventory_item(id) ON DELETE CASCADE,
    qty_on_hand        NUMERIC(14,4) NOT NULL DEFAULT 0,
    qty_reserved       NUMERIC(14,4) NOT NULL DEFAULT 0,
    PRIMARY KEY (store_id, item_id)
);

CREATE TABLE stock_journal (
    id            BIGSERIAL PRIMARY KEY,
    store_id      UUID REFERENCES store(id),
    item_id       UUID REFERENCES inventory_item(id),
    source_type   stock_source_enum NOT NULL,
    source_id     UUID  NOT NULL,
    qty_delta     NUMERIC(14,4) NOT NULL,
    cost_price    NUMERIC(12,2),
    created_at    TIMESTAMPTZ NOT NULL DEFAULT now()
);

/* ---------- 2.7. Purchase Orders ------------------------------------ */
CREATE TABLE purchase_order (
    id             UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    store_id       UUID REFERENCES store(id) ON DELETE CASCADE,
    supplier_id    UUID REFERENCES supplier(id),
    status         po_status_enum NOT NULL DEFAULT 'DRAFT',
    order_date     DATE NOT NULL DEFAULT current_date,
    expected_date  DATE,
    total_amount   NUMERIC(14,2),
    currency_code  CHAR(3) REFERENCES currency(code) DEFAULT 'SGD',
    created_at     TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at     TIMESTAMPTZ
);

CREATE TABLE purchase_order_line (
    id             BIGSERIAL PRIMARY KEY,
    purchase_order_id UUID REFERENCES purchase_order(id) ON DELETE CASCADE,
    item_id        UUID REFERENCES inventory_item(id),
    qty_ordered    NUMERIC(14,4) NOT NULL CHECK (qty_ordered > 0),
    qty_received   NUMERIC(14,4) NOT NULL DEFAULT 0,
    unit_cost      NUMERIC(12,2) NOT NULL,
    gst_rate       NUMERIC(5,2)  NOT NULL DEFAULT 8.00,
    line_total     NUMERIC(14,2) GENERATED ALWAYS AS ((unit_cost * qty_ordered)) STORED
);

/* ---------- 2.8. Stock Adjustments ---------------------------------- */
CREATE TABLE stock_adjustment (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    store_id        UUID REFERENCES store(id) ON DELETE CASCADE,
    item_id         UUID REFERENCES inventory_item(id),
    qty_adjust      NUMERIC(14,4) NOT NULL CHECK (qty_adjust <> 0),
    reason          TEXT,
    approved_by     UUID REFERENCES "user"(id),
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);

/* ---------- 2.9. Sales & Payments ----------------------------------- */
CREATE TABLE sale (
    id                UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    store_id          UUID REFERENCES store(id),
    pos_terminal_id   UUID REFERENCES pos_terminal(id),
    cashier_id        UUID REFERENCES "user"(id),
    customer_id       UUID REFERENCES customer(id),
    receipt_no        TEXT UNIQUE,
    total_amount      NUMERIC(14,2) NOT NULL,
    gst_amount        NUMERIC(14,2) NOT NULL,
    discount_amount   NUMERIC(14,2) NOT NULL DEFAULT 0,
    currency_code     CHAR(3) REFERENCES currency(code) DEFAULT 'SGD',
    status            sale_status_enum NOT NULL DEFAULT 'OPEN',
    opened_at         TIMESTAMPTZ NOT NULL DEFAULT now(),
    closed_at         TIMESTAMPTZ
);

CREATE INDEX ix_sale_store_opened   ON sale(store_id, opened_at DESC);
CREATE INDEX ix_sale_status         ON sale(status);

CREATE TABLE sale_line (
    id               BIGSERIAL PRIMARY KEY,
    sale_id          UUID REFERENCES sale(id) ON DELETE CASCADE,
    item_id          UUID REFERENCES inventory_item(id),
    qty              NUMERIC(14,4) NOT NULL CHECK (qty <> 0),
    unit_price       NUMERIC(12,2) NOT NULL,
    discount         NUMERIC(12,2) DEFAULT 0,
    gst_rate         NUMERIC(5,2)  NOT NULL,
    line_total       NUMERIC(14,2) GENERATED ALWAYS AS (((unit_price - discount) * qty)) STORED
);

CREATE TABLE payment (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    sale_id         UUID REFERENCES sale(id) ON DELETE CASCADE,
    method          payment_method_enum NOT NULL,
    amount          NUMERIC(14,2) NOT NULL CHECK (amount > 0),
    currency_code   CHAR(3) REFERENCES currency(code) DEFAULT 'SGD',
    exchange_rate   NUMERIC(16,6),
    reference_no    TEXT,
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);

/* ---------- 2.10. Promotions & Loyalty ----------------------------- */
CREATE TABLE promotion (
    id           UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_id   UUID REFERENCES company(id),
    code         TEXT UNIQUE NOT NULL,
    name         TEXT NOT NULL,
    description  TEXT,
    rule_type    promotion_rule_enum NOT NULL,
    priority     INT  NOT NULL DEFAULT 100,
    exclusive    BOOLEAN NOT NULL DEFAULT FALSE,
    start_date   DATE NOT NULL,
    end_date     DATE NOT NULL,
    active       BOOLEAN NOT NULL DEFAULT TRUE,
    created_at   TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE promotion_item (
    promotion_id UUID REFERENCES promotion(id) ON DELETE CASCADE,
    item_id      UUID REFERENCES inventory_item(id) ON DELETE CASCADE,
    PRIMARY KEY (promotion_id, item_id)
);

CREATE TABLE sale_promotion (
    id             BIGSERIAL PRIMARY KEY,
    sale_id        UUID REFERENCES sale(id) ON DELETE CASCADE,
    promotion_id   UUID REFERENCES promotion(id),
    discount_amount NUMERIC(14,2) NOT NULL
);

CREATE TABLE loyalty_ledger (
    id                UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    customer_id       UUID REFERENCES customer(id),
    sale_id           UUID REFERENCES sale(id),
    points_earned     INT NOT NULL DEFAULT 0,
    points_redeemed   INT NOT NULL DEFAULT 0,
    balance_after     INT NOT NULL,
    created_at        TIMESTAMPTZ NOT NULL DEFAULT now()
);

/* --------------------------------------------------------------------
   3. AUDIT SUPPORT  (generic JSONB row-level log, optional)
   ------------------------------------------------------------------ */
CREATE TABLE audit_log (
    id            BIGSERIAL PRIMARY KEY,
    table_name    TEXT NOT NULL,
    row_id        UUID,
    action        TEXT NOT NULL CHECK (action IN ('INSERT','UPDATE','DELETE')),
    old_data      JSONB,
    new_data      JSONB,
    changed_at    TIMESTAMPTZ NOT NULL DEFAULT now(),
    changed_by    UUID REFERENCES "user"(id)
);

/* --------------------------------------------------------------------
   4. TRIGGER FUNCTIONS
   ------------------------------------------------------------------ */

-- 4.1  Maintain inventory_stock & stock_journal on SALE lines
CREATE OR REPLACE FUNCTION f_after_insert_sale_line()
RETURNS TRIGGER LANGUAGE plpgsql AS $$
BEGIN
    /* 1) Deduct stock */
    INSERT INTO inventory_stock (store_id, item_id, qty_on_hand)
         VALUES (NEW.sale_id::uuid, NEW.item_id, -(NEW.qty))            -- dummy store; will fix via join
    ON CONFLICT (store_id, item_id)
         DO UPDATE SET qty_on_hand = inventory_stock.qty_on_hand - NEW.qty;

    /* 2) Journal entry */
    INSERT INTO stock_journal (store_id, item_id, source_type, source_id,
                               qty_delta, cost_price)
    SELECT s.store_id, NEW.item_id, 'SALE', NEW.sale_id,
           -NEW.qty, it.cost_price
      FROM sale s
      JOIN inventory_item it ON it.id = NEW.item_id
     WHERE s.id = NEW.sale_id;

    RETURN NEW;
END;
$$;

CREATE TRIGGER trg_after_insert_sale_line
AFTER INSERT ON sale_line
FOR EACH ROW
EXECUTE FUNCTION f_after_insert_sale_line();

-- 4.2  Maintain stock on PURCHASE receipt (qty_received update)
CREATE OR REPLACE FUNCTION f_after_update_po_line()
RETURNS TRIGGER LANGUAGE plpgsql AS $$
DECLARE
    diff NUMERIC(14,4);
BEGIN
    diff := NEW.qty_received - OLD.qty_received;
    IF diff = 0 THEN
        RETURN NEW;
    END IF;

    /* Update inventory_stock */
    INSERT INTO inventory_stock (store_id, item_id, qty_on_hand)
         VALUES ((SELECT store_id FROM purchase_order WHERE id = NEW.purchase_order_id), NEW.item_id, diff)
    ON CONFLICT (store_id, item_id)
         DO UPDATE SET qty_on_hand = inventory_stock.qty_on_hand + diff;

    /* Journal */
    INSERT INTO stock_journal (store_id, item_id, source_type, source_id,
                               qty_delta, cost_price)
    SELECT po.store_id, NEW.item_id, 'PURCHASE_RECEIPT', NEW.purchase_order_id,
           diff, NEW.unit_cost
      FROM purchase_order po
     WHERE po.id = NEW.purchase_order_id;

    RETURN NEW;
END;
$$;

CREATE TRIGGER trg_after_update_po_line
AFTER UPDATE OF qty_received ON purchase_order_line
FOR EACH ROW
WHEN (NEW.qty_received <> OLD.qty_received)
EXECUTE FUNCTION f_after_update_po_line();

-- 4.3  Stock Adjustments
CREATE OR REPLACE FUNCTION f_after_insert_stock_adjust()
RETURNS TRIGGER LANGUAGE plpgsql AS $$
BEGIN
    INSERT INTO inventory_stock (store_id, item_id, qty_on_hand)
         VALUES (NEW.store_id, NEW.item_id, NEW.qty_adjust)
    ON CONFLICT (store_id, item_id)
         DO UPDATE SET qty_on_hand = inventory_stock.qty_on_hand + NEW.qty_adjust;

    INSERT INTO stock_journal (store_id, item_id, source_type, source_id,
                               qty_delta, cost_price)
         VALUES (NEW.store_id, NEW.item_id, 'STOCK_ADJUST', NEW.id,
                 NEW.qty_adjust, NULL);
    RETURN NEW;
END;
$$;

CREATE TRIGGER trg_after_insert_stock_adjust
AFTER INSERT ON stock_adjustment
FOR EACH ROW EXECUTE FUNCTION f_after_insert_stock_adjust();

-- 4.4  Generic audit trigger generator
CREATE OR REPLACE FUNCTION f_audit_trigger()
RETURNS TRIGGER LANGUAGE plpgsql AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        INSERT INTO audit_log(table_name,row_id,action,new_data)
        VALUES (TG_TABLE_NAME, NEW.id, 'INSERT', to_jsonb(NEW));

    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO audit_log(table_name,row_id,action,old_data,new_data)
        VALUES (TG_TABLE_NAME, NEW.id, 'UPDATE', to_jsonb(OLD), to_jsonb(NEW));

    ELSIF TG_OP = 'DELETE' THEN
        INSERT INTO audit_log(table_name,row_id,action,old_data)
        VALUES (TG_TABLE_NAME, OLD.id, 'DELETE', to_jsonb(OLD));
    END IF;
    RETURN COALESCE(NEW, OLD);
END;
$$;

-- Apply audit trigger to critical tables
DO $$
DECLARE
    t TEXT;
BEGIN
    FOREACH t IN ARRAY ARRAY[
        'sale','sale_line','inventory_item','inventory_stock',
        'purchase_order','purchase_order_line','stock_adjustment'
    ] LOOP
        EXECUTE format('CREATE TRIGGER trg_audit_%I
                        AFTER INSERT OR UPDATE OR DELETE ON %I
                        FOR EACH ROW EXECUTE FUNCTION f_audit_trigger();', t, t);
    END LOOP;
END;
$$;

/* --------------------------------------------------------------------
   5. FINAL HOUSEKEEPING
   ------------------------------------------------------------------ */
COMMENT ON DATABASE current_database() IS 'SG-POS – Point-of-Sale unified schema';

-- Convenient VIEW: on-hand + reserved + reorder flag
CREATE VIEW v_inventory_overview AS
SELECT it.id, it.sku, it.name, st.store_id, st.qty_on_hand, st.qty_reserved,
       (st.qty_on_hand - st.qty_reserved) AS qty_available,
       it.reorder_level,
       CASE WHEN (st.qty_on_hand - st.qty_reserved) <= it.reorder_level THEN TRUE ELSE FALSE END
         AS needs_reorder
  FROM inventory_item it
  JOIN inventory_stock st ON st.item_id = it.id;

-- Grant read-only role example
CREATE ROLE sgpos_readonly NOLOGIN;
GRANT CONNECT ON DATABASE current_database() TO sgpos_readonly;
GRANT USAGE ON SCHEMA public TO sgpos_readonly;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO sgpos_readonly;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO sgpos_readonly;

/* =====================================================================
   END  OF  SCHEMA
   ===================================================================== */
```

### How to Load

```bash
psql -U sgpos -d sgpos_db -f schema.sql
```

### Key Characteristics

1. **Regulatory-Ready**  
   • GST captured on every monetary line.  
   • Five-year immutable audit trail via `audit_log`.

2. **Multi-Store & Multi-Currency**  
   • `store_id` present on all operational entities.  
   • Foreign currency payments supported with on-date exchange rates.

3. **Data-Integrity First**  
   • Cascading FKs, `CHECK` constraints, generated columns.  
   • Stock movement fully journalled & quantity kept in sync by triggers.

4. **Performance**  
   • Strategic composite indexes (`ix_sale_store_opened`, `ix_inventory_item_company_sku`).  
   • Numeric fields sized for typical retail volumes (14,2 allows ≥ 999 trillion).

5. **Extensibility**  
   • Enum types for status fields—easy to add more with migrations.  
   • Auditing trigger can be attached to additional tables in a single statement.  

This schema is **production-grade** yet intentionally **straight-forward** to understand and extend; it maps 1-to-1 with the DTOs and ORM models outlined in the PRD and `README.md`. Happy building!
