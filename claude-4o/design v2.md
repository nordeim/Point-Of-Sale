Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Project Overview
Business Requirements
Functional Requirements
Technical Architecture
Database Schema Design
Codebase Structure
Application Modules
User Interaction Flow
Technology Stack
Development Environment Setup
Production Environment Setup
Security Requirements
Performance Requirements
Testing Strategy
Deployment Strategy
Maintenance and Support
Future Considerations
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail needs of small to medium-sized businesses (SMBs) in Singapore. This system represents a significant advancement in retail management technology, combining modern software architecture with Singapore-specific regulatory compliance features.

Built on a robust technology stack featuring Python, PySide6, and PostgreSQL, the application delivers professional-grade retail management capabilities while maintaining the flexibility and cost-effectiveness that SMBs require. The system's architecture follows industry best practices, implementing a clean layered design with strict separation of concerns, dependency injection, and asynchronous processing capabilities.

Key differentiators of this POS system include its deep integration with Singapore's regulatory requirements (particularly GST compliance), multi-currency support essential for Singapore's international business environment, and a sophisticated accounting integration that provides real-time financial visibility. The system is designed from the ground up to handle real-world business complexity while maintaining an intuitive user interface that minimizes training requirements.

2. Project Overview
2.1 Vision Statement
To provide Singapore's SMBs with a world-class point-of-sale system that seamlessly integrates retail operations with accounting and regulatory compliance, enabling businesses to operate more efficiently while maintaining full compliance with local regulations.

2.2 Project Scope
The SG POS System encompasses the following core functional areas:

Sales Processing: Complete point-of-sale functionality including product management, pricing, promotions, and transaction processing
Inventory Management: Real-time inventory tracking, stock alerts, and automated reordering capabilities
Customer Relationship Management: Customer profiles, purchase history, loyalty programs, and targeted marketing capabilities
Financial Integration: Full double-entry accounting system with automated journal entry generation from sales transactions
Regulatory Compliance: Built-in GST calculation, reporting, and submission capabilities compliant with IRAS requirements
Reporting and Analytics: Comprehensive business intelligence features including sales analytics, inventory reports, and financial statements
Multi-Store Support: Centralized management of multiple retail locations with consolidated reporting
Employee Management: User access control, shift management, and performance tracking
2.3 Target Users
The system is designed for three primary user categories:

Cashiers/Sales Staff: Front-line employees who process sales transactions and interact with customers
Store Managers: Supervisory staff responsible for daily operations, inventory management, and staff oversight
Business Owners/Administrators: Decision-makers who require comprehensive business insights and financial reporting
2.4 Success Criteria
The project will be considered successful when it achieves:

Transaction processing time under 3 seconds for typical sales
99.9% system uptime during business hours
Full IRAS GST compliance certification
Positive user satisfaction ratings (>4.5/5) from pilot businesses
Successful deployment to at least 10 SMB pilot customers
Zero critical bugs in production after stabilization period
3. Business Requirements
3.1 Market Context
Singapore's retail sector presents unique challenges and opportunities:

Regulatory Environment: Strict GST compliance requirements with regular IRAS audits
Multi-Currency Operations: High percentage of tourist customers requiring multi-currency support
Space Constraints: Limited physical space requiring efficient, integrated systems
Tech-Savvy Market: High digital adoption rates among both businesses and consumers
Competitive Landscape: Intense competition requiring sophisticated analytics and customer insights
3.2 Business Objectives
Operational Efficiency

Reduce transaction processing time by 50%
Eliminate manual inventory counting through real-time tracking
Automate GST calculation and reporting
Minimize training time for new staff
Financial Visibility

Provide real-time profit and loss visibility
Enable cash flow forecasting
Automate financial reconciliation
Support multi-currency transactions
Customer Experience

Reduce checkout waiting time
Enable personalized promotions
Support multiple payment methods
Provide digital receipts
Compliance Assurance

Ensure 100% GST compliance
Maintain complete audit trails
Generate regulatory reports automatically
Support data retention requirements
3.3 Key Business Rules
GST Handling

All prices must clearly indicate GST-inclusive amounts
GST must be calculated based on current IRAS rates
Zero-rated and exempt items must be properly categorized
GST reports must be generated in IRAS-specified formats
Inventory Management

Stock levels must update in real-time
Low stock alerts must trigger at configurable thresholds
Stock movements must maintain complete audit trails
Inter-store transfers must be properly documented
Financial Processing

All transactions must generate appropriate journal entries
Daily cash reconciliation is mandatory
Foreign currency transactions must use daily exchange rates
Void/refund transactions require authorization
Customer Data

Personal data collection must comply with PDPA
Customer consent must be obtained for marketing
Data retention must follow regulatory requirements
Cross-border data transfer restrictions must be enforced
4. Functional Requirements
4.1 Sales Management
4.1.1 Product Catalog Management
Product Creation: Support for multiple product types (simple, variant, bundled, service)
Categorization: Hierarchical category structure with unlimited depth
Pricing: Multiple price tiers, promotional pricing, time-based pricing
Barcode Support: Generate and print barcodes, support multiple barcode formats
Image Management: Product images with thumbnail generation
Attributes: Customizable product attributes (size, color, material, etc.)
4.1.2 Point of Sale Operations
Quick Sale: Barcode scanning, manual SKU entry, product search
Cart Management: Add/remove items, quantity adjustment, price override (with authorization)
Discounts: Percentage/fixed discounts, item-level/transaction-level discounts
Payment Processing: Cash, credit/debit cards, e-wallets, vouchers
Split Payments: Support multiple payment methods in single transaction
Hold/Resume: Save incomplete transactions for later completion
4.1.3 Customer Management
Customer Profiles: Contact information, purchase history, preferences
Loyalty Programs: Points accumulation, tier management, rewards redemption
Credit Management: Store credit, payment terms for B2B customers
Marketing Preferences: Opt-in/opt-out management, communication channels
Customer Groups: Segmentation for targeted promotions
4.2 Inventory Management
4.2.1 Stock Control
Real-time Tracking: Live inventory levels across all locations
Stock Movements: Purchase orders, goods receipt, stock transfers, adjustments
Serialization: Serial number tracking for high-value items
Batch Tracking: Expiry date management, FIFO/LIFO costing
Stock Takes: Partial and full stock count support with variance reporting
4.2.2 Purchasing
Supplier Management: Supplier profiles, payment terms, performance tracking
Purchase Orders: Create, approve, receive POs with three-way matching
Reorder Management: Automatic reorder point calculation, suggested orders
Cost Tracking: Landing costs, currency conversion, price history
4.2.3 Warehouse Operations
Multi-location Support: Manage inventory across stores and warehouses
Transfer Orders: Inter-location stock movements with approval workflow
Receiving: Barcode scanning, quantity verification, quality checks
Put-away: Suggested locations, bin management
4.3 Financial Management
4.3.1 Accounting Integration
Chart of Accounts: Comprehensive COA tailored for Singapore businesses
Journal Entries: Automatic generation from transactions, manual entries
General Ledger: Real-time GL updates, account reconciliation
Financial Statements: P&L, Balance Sheet, Cash Flow statements
4.3.2 GST Compliance
Tax Calculation: Automatic GST calculation based on product tax codes
GST Reports: GST F5, GST F7, GST listing statements
IRAS Integration: Electronic submission capability
Audit Trail: Complete documentation for GST audits
4.3.3 Payment Processing
Cash Management: Till management, cash counting, float tracking
Card Processing: Integrated payment terminal support
Digital Payments: PayNow, GrabPay, other e-wallets
Reconciliation: Automatic matching of payments with bank statements
4.4 Reporting and Analytics
4.4.1 Sales Analytics
Dashboard: Real-time sales metrics, KPI monitoring
Sales Reports: By period, product, category, staff, customer
Trend Analysis: Year-over-year comparisons, seasonality detection
Forecasting: Sales predictions based on historical data
4.4.2 Inventory Reports
Stock Status: Current stock levels, valuation, aging
Movement Reports: Stock in/out, transfer history
Performance Metrics: Turnover rates, dead stock identification
Reorder Reports: Items below reorder point, suggested orders
4.4.3 Financial Reports
Daily Reports: X-report, Z-report, cash reconciliation
Period Reports: Monthly/quarterly/annual financial statements
Tax Reports: GST returns, withholding tax statements
Custom Reports: User-definable report templates
4.5 System Administration
4.5.1 User Management
Role-based Access: Predefined roles with customizable permissions
User Profiles: Employee information, access credentials
Audit Logging: Comprehensive activity tracking
Session Management: Concurrent session limits, timeout policies
4.5.2 System Configuration
Business Settings: Company information, tax registration, operating hours
POS Settings: Receipt formats, payment types, rounding rules
Integration Settings: Payment gateway configuration, accounting mappings
Backup/Restore: Automated backups, point-in-time recovery
5. Technical Architecture
5.1 Architecture Overview
The SG POS System implements a modern, layered architecture designed for maintainability, scalability, and testability. The architecture strictly separates concerns across four primary layers:

Presentation Layer: PySide6-based UI components handling user interactions
Business Logic Layer: Core business rules and workflow orchestration
Data Access Layer: Repository pattern implementation for data persistence
Infrastructure Layer: Cross-cutting concerns like logging, caching, and security
5.2 Architecture Principles
5.2.1 Separation of Concerns
Each layer has clearly defined responsibilities:

UI components never contain business logic
Business logic layer is framework-agnostic
Data access is abstracted through service interfaces
Cross-cutting concerns are handled through dependency injection
5.2.2 Dependency Inversion
High-level modules depend on abstractions, not concrete implementations
Dependencies flow inward toward the business core
External frameworks are isolated at the boundaries
5.2.3 Single Responsibility
Each class has one reason to change
Managers orchestrate workflows without implementing details
Services handle specific data operations
UI components focus solely on presentation
5.3 Component Architecture
┌─────────────────────────────────────────────────────────────────┐
│                        Presentation Layer                        │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │   Main     │  │   Sales    │  │ Inventory  │  │  Reports   ││
│  │  Window    │  │  Widget    │  │  Widget    │  │  Widget    ││
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘│
└─────────────────────────────────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Business Logic Layer                          │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │   Sales    │  │ Inventory  │  │ Accounting │  │    GST     ││
│  │  Manager   │  │  Manager   │  │  Manager   │  │  Manager   ││
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘│
└─────────────────────────────────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Data Access Layer                           │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │  Product   │  │   Order    │  │  Customer  │  │  Account   ││
│  │  Service   │  │  Service   │  │  Service   │  │  Service   ││
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘│
└─────────────────────────────────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Infrastructure Layer                        │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │ PostgreSQL │  │   Redis    │  │  Logging   │  │  Security  ││
│  │  Database  │  │   Cache    │  │  System    │  │  Module    ││
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘│
└─────────────────────────────────────────────────────────────────┘
5.4 Asynchronous Processing Model
The application implements a sophisticated asynchronous model to ensure responsive UI:

# Asynchronous Architecture Pattern
Main Thread (Qt Event Loop)
    │
    ├── UI Event Handling
    ├── Widget Updates
    └── User Interactions
    
Worker Thread (asyncio Event Loop)
    │
    ├── Database Operations
    ├── Network Requests
    ├── File I/O
    └── Background Tasks
    
Thread Communication
    │
    ├── Qt Signals/Slots
    ├── Thread-safe Queues
    └── QMetaObject.invokeMethod

5.5 Dependency Injection Architecture
The ApplicationCore class serves as the central dependency injection container:

class ApplicationCore:
    """Central dependency injection container"""
    
    def __init__(self):
        self._db_session = None
        self._cache = None
        self._config = None
        
    @property
    def sales_manager(self) -> SalesManager:
        """Lazy initialization of sales manager"""
        if not hasattr(self, '_sales_manager'):
            self._sales_manager = SalesManager(self)
        return self._sales_manager

6. Database Schema Design
6.1 Schema Overview
The database schema is designed to support all functional requirements while maintaining data integrity and query performance. Key design decisions include:

Use of UUID primary keys for distributed system compatibility
Comprehensive audit trails on all transactional tables
Proper normalization while maintaining query efficiency
Strategic denormalization for reporting performance
6.2 Core Schema Entities
-- Company and Configuration
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    uen VARCHAR(20) UNIQUE NOT NULL, -- Singapore UEN
    gst_reg_no VARCHAR(20),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    postal_code VARCHAR(10),
    phone VARCHAR(20),
    email VARCHAR(255),
    fiscal_year_start DATE NOT NULL,
    base_currency VARCHAR(3) NOT NULL DEFAULT 'SGD',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- User Management
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Product Management
CREATE TABLE product_categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    parent_id UUID REFERENCES product_categories(id),
    name VARCHAR(100) NOT NULL,
    description TEXT,
    sort_order INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, parent_id, name)
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    category_id UUID REFERENCES product_categories(id),
    sku VARCHAR(50) NOT NULL,
    barcode VARCHAR(50),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    unit_of_measure VARCHAR(20) NOT NULL DEFAULT 'UNIT',
    cost_price DECIMAL(15,2),
    selling_price DECIMAL(15,2) NOT NULL,
    tax_code VARCHAR(20) NOT NULL DEFAULT 'SR', -- Standard-Rated
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    reorder_point INTEGER,
    reorder_quantity INTEGER,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, sku)
);

-- Inventory Management
CREATE TABLE stock_locations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(20) NOT NULL,
    name VARCHAR(100) NOT NULL,
    type VARCHAR(20) NOT NULL, -- STORE, WAREHOUSE
    address VARCHAR(500),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID NOT NULL REFERENCES products(id),
    location_id UUID NOT NULL REFERENCES stock_locations(id),
    quantity_on_hand DECIMAL(15,3) NOT NULL DEFAULT 0,
    quantity_reserved DECIMAL(15,3) NOT NULL DEFAULT 0,
    quantity_available DECIMAL(15,3) GENERATED ALWAYS AS 
        (quantity_on_hand - quantity_reserved) STORED,
    average_cost DECIMAL(15,4),
    last_counted_date DATE,
    last_counted_quantity DECIMAL(15,3),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location_id)
);

-- Customer Management
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    customer_code VARCHAR(20) NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(20),
    address VARCHAR(500),
    customer_type VARCHAR(20) NOT NULL DEFAULT 'RETAIL', -- RETAIL, WHOLESALE
    credit_limit DECIMAL(15,2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0, -- Days
    tax_registration_no VARCHAR(50),
    loyalty_points INTEGER DEFAULT 0,
    loyalty_tier VARCHAR(20) DEFAULT 'BASIC',
    is_active BOOLEAN DEFAULT true,
    pdpa_consent BOOLEAN DEFAULT false,
    pdpa_consent_date TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, customer_code)
);

-- Sales Transactions
CREATE TABLE sales_orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    order_number VARCHAR(20) NOT NULL,
    order_date TIMESTAMP WITH TIME ZONE NOT NULL,
    customer_id UUID REFERENCES customers(id),
    location_id UUID NOT NULL REFERENCES stock_locations(id),
    user_id UUID NOT NULL REFERENCES users(id),
    status VARCHAR(20) NOT NULL DEFAULT 'DRAFT', -- DRAFT, CONFIRMED, COMPLETED, CANCELLED
    currency VARCHAR(3) NOT NULL DEFAULT 'SGD',
    exchange_rate DECIMAL(15,6) NOT NULL DEFAULT 1,
    subtotal DECIMAL(15,2) NOT NULL,
    tax_amount DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    total_amount DECIMAL(15,2) NOT NULL,
    payment_status VARCHAR(20) NOT NULL DEFAULT 'PENDING', -- PENDING, PARTIAL, PAID
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, order_number)
);

CREATE TABLE sales_order_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sales_order_id UUID NOT NULL REFERENCES sales_orders(id),
    line_number INTEGER NOT NULL,
    product_id UUID NOT NULL REFERENCES products(id),
    description VARCHAR(500),
    quantity DECIMAL(15,3) NOT NULL,
    unit_price DECIMAL(15,4) NOT NULL,
    discount_percent DECIMAL(5,2) DEFAULT 0,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    tax_code VARCHAR(20) NOT NULL,
    tax_amount DECIMAL(15,2) NOT NULL,
    line_total DECIMAL(15,2) NOT NULL,
    cost_price DECIMAL(15,4),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(sales_order_id, line_number)
);

-- Payment Processing
CREATE TABLE payment_methods (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(20) NOT NULL,
    name VARCHAR(50) NOT NULL,
    type VARCHAR(20) NOT NULL, -- CASH, CARD, EWALLET, VOUCHER
    is_active BOOLEAN DEFAULT true,
    requires_reference BOOLEAN DEFAULT false,
    gl_account_id UUID,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    payment_number VARCHAR(20) NOT NULL,
    payment_date TIMESTAMP WITH TIME ZONE NOT NULL,
    sales_order_id UUID REFERENCES sales_orders(id),
    customer_id UUID REFERENCES customers(id),
    payment_method_id UUID NOT NULL REFERENCES payment_methods(id),
    amount DECIMAL(15,2) NOT NULL,
    reference_number VARCHAR(100),
    status VARCHAR(20) NOT NULL DEFAULT 'PENDING', -- PENDING, COMPLETED, FAILED, REFUNDED
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, payment_number)
);

-- Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    account_code VARCHAR(20) NOT NULL,
    account_name VARCHAR(100) NOT NULL,
    account_type VARCHAR(20) NOT NULL, -- ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE
    parent_id UUID REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    is_system_account BOOLEAN DEFAULT false,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, account_code)
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    journal_number VARCHAR(20) NOT NULL,
    journal_date DATE NOT NULL,
    description VARCHAR(500),
    reference_type VARCHAR(50), -- SALES, PAYMENT, INVENTORY
    reference_id UUID,
    status VARCHAR(20) NOT NULL DEFAULT 'DRAFT', -- DRAFT, POSTED, REVERSED
    posted_by UUID REFERENCES users(id),
    posted_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, journal_number)
);

CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    journal_entry_id UUID NOT NULL REFERENCES journal_entries(id),
    line_number INTEGER NOT NULL,
    account_id UUID NOT NULL REFERENCES chart_of_accounts(id),
    description VARCHAR(500),
    debit_amount DECIMAL(15,2) DEFAULT 0,
    credit_amount DECIMAL(15,2) DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(journal_entry_id, line_number),
    CHECK (debit_amount >= 0 AND credit_amount >= 0),
    CHECK (NOT (debit_amount > 0 AND credit_amount > 0))
);

-- GST Management
CREATE TABLE gst_codes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(20) PRIMARY KEY,
    description VARCHAR(100) NOT NULL,
    rate DECIMAL(5,2) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Initial GST codes for Singapore
INSERT INTO gst_codes (code, description, rate) VALUES
    ('SR', 'Standard-Rated Supply', 9.0),
    ('ZR', 'Zero-Rated Supply', 0.0),
    ('ES', 'Exempt Supply', 0.0),
    ('OS', 'Out-of-Scope Supply', 0.0),
    ('TX', 'Purchase with GST', 9.0),
    ('ZP', 'Zero-Rated Purchase', 0.0),
    ('EP', 'Exempt Purchase', 0.0),
    ('OP', 'Out-of-Scope Purchase', 0.0);

-- Audit Trail
CREATE TABLE audit_log (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    user_id UUID REFERENCES users(id),
    action VARCHAR(50) NOT NULL,
    table_name VARCHAR(50) NOT NULL,
    record_id UUID NOT NULL,
    old_values JSONB,
    new_values JSONB,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Indexes for Performance
CREATE INDEX idx_products_sku ON products(company_id, sku);
CREATE INDEX idx_products_barcode ON products(company_id, barcode);
CREATE INDEX idx_inventory_product ON inventory(product_id);
CREATE INDEX idx_sales_orders_date ON sales_orders(company_id, order_date);
CREATE INDEX idx_sales_orders_customer ON sales_orders(customer_id);
CREATE INDEX idx_journal_entries_date ON journal_entries(company_id, journal_date);
CREATE INDEX idx_audit_log_table ON audit_log(company_id, table_name, created_at);

6.3 Database Triggers and Functions
-- Automatic timestamp updates
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

-- Apply to all tables with updated_at
CREATE TRIGGER update_companies_updated_at BEFORE UPDATE ON companies
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
-- (Repeat for all tables with updated_at column)

-- Inventory update trigger
CREATE OR REPLACE FUNCTION update_inventory_on_sale()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.status = 'COMPLETED' AND OLD.status != 'COMPLETED' THEN
        UPDATE inventory i
        SET quantity_on_hand = quantity_on_hand - sol.quantity
        FROM sales_order_lines sol
        WHERE sol.sales_order_id = NEW.id
        AND i.product_id = sol.product_id
        AND i.location_id = NEW.location_id;
    END IF;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER trigger_update_inventory_on_sale
    AFTER UPDATE ON sales_orders
    FOR EACH ROW EXECUTE FUNCTION update_inventory_on_sale();

-- Audit log trigger
CREATE OR REPLACE FUNCTION audit_trigger_function()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO audit_log (
        company_id, user_id, action, table_name, record_id,
        old_values, new_values
    )
    VALUES (
        COALESCE(NEW.company_id, OLD.company_id),
        current_setting('app.current_user_id')::UUID,
        TG_OP,
        TG_TABLE_NAME,
        COALESCE(NEW.id, OLD.id),
        CASE WHEN TG_OP = 'DELETE' OR TG_OP = 'UPDATE' THEN row_to_json(OLD) END,
        CASE WHEN TG_OP = 'INSERT' OR TG_OP = 'UPDATE' THEN row_to_json(NEW) END
    );
    RETURN NEW;
END;
$$ language 'plpgsql';

-- Apply audit triggers to key tables
CREATE TRIGGER audit_trigger_sales_orders
    AFTER INSERT OR UPDATE OR DELETE ON sales_orders
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();

7. Codebase Structure
7.1 Project Directory Structure
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                      # Application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py      # Dependency injection container
│   │   ├── config.py               # Configuration management
│   │   ├── constants.py            # Application constants
│   │   └── exceptions.py           # Custom exceptions
│   │
│   ├── models/                      # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                 # Base model class
│   │   ├── company.py
│   │   ├── user.py
│   │   ├── product.py
│   │   ├── inventory.py
│   │   ├── customer.py
│   │   ├── sales.py
│   │   ├── payment.py
│   │   ├── accounting.py
│   │   └── audit.py
│   │
│   ├── services/                    # Data access layer
│   │   ├── __init__.py
│   │   ├── base_service.py         # Base service class
│   │   ├── product_service.py
│   │   ├── inventory_service.py
│   │   ├── customer_service.py
│   │   ├── sales_service.py
│   │   ├── payment_service.py
│   │   ├── accounting_service.py
│   │   └── report_service.py
│   │
│   ├── business_logic/              # Business logic layer
│   │   ├── __init__.py
│   │   ├── sales_manager.py
│   │   ├── inventory_manager.py
│   │   ├── customer_manager.py
│   │   ├── payment_manager.py
│   │   ├── gst_manager.py
│   │   └── promotion_manager.py
│   │
│   ├── accounting/                  # Accounting module
│   │   ├── __init__.py
│   │   ├── journal_manager.py
│   │   ├── ledger_manager.py
│   │   ├── financial_reports.py
│   │   └── gst_reports.py
│   │
│   ├── ui/                         # Presentation layer
│   │   ├── __init__.py
│   │   ├── main_window.py
│   │   ├── theme.py               # UI theme and styling
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py
│   │   │   ├── sales_widget.py
│   │   │   ├── inventory_widget.py
│   │   │   ├── customer_widget.py
│   │   │   ├── reports_widget.py
│   │   │   └── settings_widget.py
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── product_dialog.py
│   │   │   ├── payment_dialog.py
│   │   │   ├── customer_dialog.py
│   │   │   └── refund_dialog.py
│   │   ├── models/                # Qt models for views
│   │   │   ├── __init__.py
│   │   │   ├── product_model.py
│   │   │   ├── sales_model.py
│   │   │   └── customer_model.py
│   │   └── components/            # Reusable UI components
│   │       ├── __init__.py
│   │       ├── search_bar.py
│   │       ├── number_pad.py
│   │       ├── receipt_viewer.py
│   │       └── chart_widgets.py
│   │
│   ├── utils/                      # Utility modules
│   │   ├── __init__.py
│   │   ├── validators.py
│   │   ├── formatters.py
│   │   ├── security.py
│   │   ├── async_utils.py
│   │   └── barcode_utils.py
│   │
│   ├── integrations/               # External integrations
│   │   ├── __init__.py
│   │   ├── payment_gateway.py
│   │   ├── accounting_sync.py
│   │   ├── email_service.py
│   │   └── sms_service.py
│   │
│   └── resources/                  # Application resources
│       ├── images/
│       ├── icons/
│       ├── fonts/
│       └── translations/
│
├── tests/                          # Test suite
│   ├── __init__.py
│   ├── conftest.py               # Pytest configuration
│   ├── unit/
│   │   ├── test_sales_manager.py
│   │   ├── test_inventory_service.py
│   │   └── test_gst_calculations.py
│   ├── integration/
│   │   ├── test_sales_workflow.py
│   │   └── test_payment_processing.py
│   └── e2e/
│       └── test_complete_sale.py
│
├── scripts/                        # Utility scripts
│   ├── init_db.py                # Database initialization
│   ├── migrate_db.py             # Database migrations
│   ├── seed_data.py              # Test data seeding
│   └── generate_reports.py       # Report generation
│
├── docs/                          # Documentation
│   ├── api/
│   ├── user_guide/
│   ├── admin_guide/
│   └── developer_guide/
│
├── deployment/                    # Deployment configurations
│   ├── docker/
│   │   ├── Dockerfile
│   │   └── docker-compose.yml
│   ├── kubernetes/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   └── scripts/
│       ├── deploy.sh
│       └── rollback.sh
│
├── requirements/                  # Dependency management
│   ├── base.txt
│   ├── development.txt
│   ├── testing.txt
│   └── production.txt
│
├── .env.example                  # Environment variables template
├── .gitignore
├── README.md
├── LICENSE
├── pyproject.toml               # Project configuration
└── setup.py                     # Package setup
7.2 Key Module Descriptions
7.2.1 Core Module (app/core/)
application_core.py

class ApplicationCore:
    """Central dependency injection container and application orchestrator"""
    
    def __init__(self):
        self._config = None
        self._db_session = None
        self._cache = None
        self._event_bus = None
        
    @property
    def sales_manager(self) -> 'SalesManager':
        """Lazy initialization of sales manager"""
        if not hasattr(self, '_sales_manager'):
            from app.business_logic.sales_manager import SalesManager
            self._sales_manager = SalesManager(self)
        return self._sales_manager

config.py

class Config:
    """Application configuration management"""
    
    # Database settings
    DATABASE_URL: str
    DATABASE_POOL_SIZE: int = 10
    DATABASE_MAX_OVERFLOW: int = 20
    
    # Redis cache settings
    REDIS_URL: str
    CACHE_TTL: int = 300
    
    # Application settings
    LOG_LEVEL: str = "INFO"
    TIMEZONE: str = "Asia/Singapore"
    CURRENCY: str = "SGD"
    GST_RATE: Decimal = Decimal("0.09")

7.2.2 Business Logic Layer (app/business_logic/)
sales_manager.py

class SalesManager:
    """Orchestrates sales-related business operations"""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        
    async def create_sale(self, sale_data: SaleDTO) -> Result[Sale]:
        """Creates a new sale with all business rules applied"""
        # Validate customer
        # Check inventory availability
        # Calculate pricing and discounts
        # Apply GST
        # Create journal entries
        # Update inventory
        # Process payment

inventory_manager.py

class InventoryManager:
    """Manages inventory operations and stock control"""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        
    async def check_availability(self, product_id: UUID, quantity: Decimal) -> Result[bool]:
        """Checks product availability across all locations"""
        
    async def reserve_stock(self, items: List[StockReservation]) -> Result[ReservationId]:
        """Reserves stock for pending transactions"""
        
    async def transfer_stock(self, transfer: StockTransferDTO) -> Result[StockTransfer]:
        """Handles inter-location stock transfers"""

7.2.3 UI Layer (app/ui/)
main_window.py

class MainWindow(QMainWindow):
    """Main application window"""
    
    def __init__(self, app_core: ApplicationCore):
        super().__init__()
        self._app_core = app_core
        self._setup_ui()
        self._setup_navigation()
        
    def _setup_ui(self):
        """Initialize UI components"""
        self.setWindowTitle("SG POS System")
        self.setMinimumSize(1366, 768)
        
        # Create central widget with navigation
        self._central_widget = QWidget()
        self._layout = QHBoxLayout()
        
        # Navigation sidebar
        self._nav_widget = NavigationWidget()
        self._layout.addWidget(self._nav_widget)
        
        # Content area
        self._content_stack = QStackedWidget()
        self._layout.addWidget(self._content_stack)

widgets/sales_widget.py

class SalesWidget(BaseWidget):
    """Point of sale interface"""
    
    def __init__(self, app_core: ApplicationCore):
        super().__init__(app_core)
        self._setup_pos_interface()
        
    def _setup_pos_interface(self):
        """Creates the POS interface layout"""
        # Product search and selection
        # Shopping cart
        # Customer selection
        # Payment processing
        # Receipt generation

8. Application Modules
8.1 Module Architecture Overview
The application is organized into distinct modules, each responsible for specific business functionality. The modular architecture ensures:

Clear separation of concerns
Independent development and testing
Scalability and maintainability
Reusability of components
8.2 Core Application Modules
8.2.1 Sales Module
Purpose: Handles all point-of-sale operations from product selection to payment processing.

Key Components:

Product catalog browser with search and filtering
Shopping cart management with real-time updates
Multiple payment method support
Receipt generation and printing
Return/refund processing
Integration Points:

Inventory Module: Real-time stock checking and updates
Customer Module: Customer selection and loyalty points
Accounting Module: Automatic journal entry generation
Payment Module: Payment processing and reconciliation
8.2.2 Inventory Module
Purpose: Manages stock levels, movements, and procurement across all locations.

Key Components:

Real-time stock tracking
Purchase order management
Stock transfer between locations
Physical stock count support
Automated reorder suggestions
Integration Points:

Sales Module: Stock reservation and deduction
Accounting Module: Inventory valuation and COGS
Reporting Module: Stock reports and analytics
8.2.3 Customer Module
Purpose: Maintains customer information and manages relationships.

Key Components:

Customer profile management
Purchase history tracking
Loyalty program administration
Credit limit management
PDPA compliance tools
Integration Points:

Sales Module: Customer selection during sale
Marketing Module: Targeted campaigns
Reporting Module: Customer analytics
8.2.4 Accounting Module
Purpose: Provides full double-entry accounting functionality.

Key Components:

Chart of accounts management
Automatic journal entry generation
General ledger maintenance
Financial statement generation
Bank reconciliation
Integration Points:

All transactional modules for journal entries
GST Module: Tax calculations and reporting
Reporting Module: Financial reports
8.2.5 GST Module
Purpose: Ensures compliance with Singapore GST regulations.

Key Components:

GST calculation engine
Tax code management
GST report generation (F5, F7)
IRAS submission preparation
Audit trail maintenance
Integration Points:

Sales Module: Tax calculation on sales
Purchase Module: Input tax tracking
Accounting Module: GST liability accounts
8.2.6 Reporting Module
Purpose: Provides comprehensive business intelligence and reporting.

Key Components:

Real-time dashboard
Standard report library
Custom report builder
Data export functionality
Scheduled report generation
Integration Points:

All modules for data aggregation
Email Module: Report distribution
8.3 Module Interaction Diagram
┌─────────────────────────────────────────────────────────────────────┐
│                          User Interface Layer                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌────────────┐│
│  │    Sales    │  │  Inventory  │  │  Customer   │  │  Reports   ││
│  │   Widget    │  │   Widget    │  │   Widget    │  │  Widget    ││
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └─────┬──────┘│
│         │                 │                 │                │       │
├─────────┼─────────────────┼─────────────────┼────────────────┼──────┤
│         ▼                 ▼                 ▼                ▼       │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    Application Core                          │   │
│  │                 (Dependency Injection)                       │   │
│  └─────────────────────────────────────────────────────────────┘   │
│         │                                                            │
├─────────┼────────────────────────────────────────────────────────────┤
│         ▼                                                            │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌─────────────┐     │
│  │   Sales   │←→│ Inventory │←→│ Customer  │←→│ Accounting  │     │
│  │  Manager  │  │  Manager  │  │  Manager  │  │   Manager   │     │
│  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘  └──────┬──────┘     │
│        │              │              │                 │            │
│        ▼              ▼              ▼                 ▼            │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌─────────────┐     │
│  │   Order   │  │   Stock   │  │ Customer  │  │   Journal   │     │
│  │  Service  │  │  Service  │  │  Service  │  │   Service   │     │
│  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘  └──────┬──────┘     │
│        │              │              │                 │            │
├────────┼──────────────┼──────────────┼─────────────────┼────────────┤
│        ▼              ▼              ▼                 ▼            │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    PostgreSQL Database                       │   │
│  └─────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
9. User Interaction Flow
9.1 Primary User Workflows
9.1.1 Sales Transaction Flow
Start Sale
    │
    ├─→ Customer Selection (Optional)
    │      ├─→ Search existing customer
    │      └─→ Create new customer
    │
    ├─→ Product Selection
    │      ├─→ Barcode scanning
    │      ├─→ SKU entry
    │      └─→ Product search
    │
    ├─→ Cart Management
    │      ├─→ Quantity adjustment
    │      ├─→ Price override (authorized)
    │      └─→ Apply discounts
    │
    ├─→ Payment Processing
    │      ├─→ Select payment method(s)
    │      ├─→ Process payment
    │      └─→ Handle change/receipt
    │
    └─→ Transaction Completion
           ├─→ Update inventory
           ├─→ Generate journal entries
           ├─→ Update customer points
           └─→ Print/email receipt
9.1.2 Inventory Management Flow
Inventory Operations
    │
    ├─→ Stock Receipt
    │      ├─→ Select purchase order
    │      ├─→ Scan/enter received items
    │      ├─→ Quality check
    │      └─→ Update stock levels
    │
    ├─→ Stock Transfer
    │      ├─→ Select source/destination
    │      ├─→ Select items/quantities
    │      ├─→ Generate transfer order
    │      └─→ Confirm receipt
    │
    └─→ Stock Count
           ├─→ Generate count sheet
           ├─→ Physical count entry
           ├─→ Variance analysis
           └─→ Adjustment posting
9.2 User Interface Navigation
Main Navigation Structure:

Dashboard
    ├─→ Sales Summary
    ├─→ Key Metrics
    └─→ Alerts

Sales
    ├─→ Point of Sale
    ├─→ Sales History
    ├─→ Returns/Refunds
    └─→ Quotations

Inventory
    ├─→ Stock Levels
    ├─→ Purchase Orders
    ├─→ Stock Transfers
    └─→ Stock Count

Customers
    
