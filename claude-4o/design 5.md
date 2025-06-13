<think>
This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. The user has provided detailed architectural considerations and requirements. I need to create a thorough PRD that includes:

1. Executive Summary
2. Product Overview
3. Technology Stack
4. Database Schema Design
5. Codebase File Hierarchy
6. Application Modules and User Interaction Diagram
7. Key Application Modules and Files Description
8. Development Environment Setup
9. Production Environment Setup
10. Architecture Details
11. Security Considerations
12. Testing Strategy
13. Deployment Strategy

The document needs to be at least 6000 words and should be comprehensive enough to guide the actual development without ambiguity. I'll need to incorporate the architectural considerations mentioned:
- Layered architecture with clear separation of concerns
- Dependency injection through ApplicationCore
- Asynchronous processing model
- Multi-currency support
- Singapore regulatory compliance

Let me structure this PRD systematically.
</think>

# Product Requirements Document: SG Point-of-Sale (POS) System

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Product Overview](#product-overview)
3. [Technology Stack](#technology-stack)
4. [System Architecture](#system-architecture)
5. [Database Schema Design](#database-schema-design)
6. [Codebase File Hierarchy](#codebase-file-hierarchy)
7. [Application Modules and User Interaction](#application-modules-and-user-interaction)
8. [Key Application Modules Description](#key-application-modules-description)
9. [Development Environment Setup](#development-environment-setup)
10. [Production Environment Setup](#production-environment-setup)
11. [Security Considerations](#security-considerations)
12. [Testing Strategy](#testing-strategy)
13. [Deployment Strategy](#deployment-strategy)
14. [Compliance and Regulatory Requirements](#compliance-and-regulatory-requirements)
15. [Performance Requirements](#performance-requirements)
16. [Future Enhancements](#future-enhancements)

## Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed for small to medium-sized businesses (SMBs) in Singapore. Built with modern technologies including Python, PySide6, and PostgreSQL, this system provides a professional-grade retail management solution that adheres to Singapore's regulatory requirements while offering exceptional performance and user experience.

The application architecture follows industry best practices with a clean layered architecture, robust asynchronous processing capabilities, and strong data integrity mechanisms. The system implements advanced patterns including Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern to ensure maintainability, scalability, and reliability.

Key features include multi-currency support, GST compliance, comprehensive inventory management, customer relationship management, and detailed financial reporting capabilities. The system is designed to handle real-world business complexity while maintaining a user-friendly interface that requires minimal training.

## Product Overview

### Vision Statement
To provide Singapore's SMBs with a world-class point-of-sale system that combines powerful functionality with ease of use, enabling businesses to streamline operations, improve customer service, and maintain regulatory compliance effortlessly.

### Target Market
- Small to medium-sized retail businesses in Singapore
- Multi-location retail chains
- F&B establishments
- Service-based businesses requiring point-of-sale capabilities
- Businesses requiring GST compliance and reporting

### Core Value Propositions
1. **Singapore-Specific Compliance**: Built-in GST calculation, reporting, and submission features
2. **Multi-Currency Support**: Handle transactions in multiple currencies with real-time exchange rates
3. **Scalability**: Architecture designed to grow with the business
4. **Offline Capability**: Continue operations even without internet connectivity
5. **Real-Time Analytics**: Instant insights into business performance
6. **User-Friendly Interface**: Minimal training required for staff

### Key Features

#### Point of Sale Operations
- Fast and intuitive checkout process
- Barcode scanning support
- Multiple payment methods (cash, credit/debit cards, e-wallets, NETS)
- Split payment functionality
- Customer display integration
- Receipt printing and email capabilities
- Return and exchange processing
- Discount and promotion management

#### Inventory Management
- Real-time stock tracking
- Low stock alerts
- Automatic reorder points
- Batch and serial number tracking
- Product variants (size, color, etc.)
- Stock transfer between locations
- Stock take and adjustment features
- Supplier management

#### Customer Management
- Customer database with purchase history
- Loyalty program support
- Customer credit management
- Birthday and anniversary tracking
- Targeted marketing capabilities
- Customer feedback collection

#### Financial Management
- GST calculation and reporting
- Multi-currency transactions
- Daily cash reconciliation
- Profit and loss reporting
- Cash flow management
- Integration with accounting systems
- Expense tracking

#### Employee Management
- User roles and permissions
- Time clock functionality
- Commission tracking
- Performance reporting
- Shift management

#### Reporting and Analytics
- Sales reports (daily, weekly, monthly, yearly)
- Product performance analysis
- Customer behavior insights
- Employee performance metrics
- Inventory turnover reports
- GST reports for IRAS submission

## Technology Stack

### Core Technologies

#### Programming Language
- **Python 3.11+**: Chosen for its robust ecosystem, excellent library support, and rapid development capabilities
- Type hints throughout the codebase for better IDE support and code maintainability

#### GUI Framework
- **PySide6 (Qt for Python)**: Provides native look and feel across platforms
- Modern, responsive UI with hardware acceleration
- Extensive widget library for complex UI requirements
- Strong support for custom styling and theming

#### Database
- **PostgreSQL 15+**: Enterprise-grade relational database
- ACID compliance for data integrity
- Advanced indexing for performance
- JSON support for flexible data structures
- Full-text search capabilities

#### ORM
- **SQLAlchemy 2.0+**: Modern, powerful ORM with async support
- Database-agnostic design
- Migration support through Alembic
- Connection pooling for performance

### Supporting Technologies

#### Asynchronous Processing
- **asyncio**: Native Python async/await support
- **aiohttp**: Async HTTP client for external API calls
- **asyncpg**: High-performance async PostgreSQL driver

#### Data Validation
- **Pydantic**: Data validation using Python type annotations
- Automatic API documentation generation
- Serialization/deserialization support

#### Testing
- **pytest**: Comprehensive testing framework
- **pytest-asyncio**: Async test support
- **pytest-qt**: Qt/PySide6 testing utilities
- **pytest-cov**: Code coverage reporting

#### Development Tools
- **Black**: Code formatting
- **Ruff**: Fast Python linter
- **mypy**: Static type checking
- **pre-commit**: Git hooks for code quality

#### Deployment
- **PyInstaller**: Create standalone executables
- **Docker**: Containerization for consistent deployment
- **GitHub Actions**: CI/CD pipeline

#### External Integrations
- **Stripe API**: Credit card processing
- **NETS API**: Local payment gateway
- **Exchange Rate API**: Real-time currency conversion
- **IRAS API**: GST submission (when available)

## System Architecture

### Architectural Principles

#### 1. Layered Architecture
The system follows a strict layered architecture pattern with clear separation of concerns:

```
┌─────────────────────────────────────────┐
│         Presentation Layer              │
│    (PySide6 UI Components)              │
├─────────────────────────────────────────┤
│      Business Logic Layer               │
│    (Managers & Domain Logic)            │
├─────────────────────────────────────────┤
│      Data Access Layer                  │
│    (Services & Repositories)            │
├─────────────────────────────────────────┤
│      Persistence Layer                  │
│    (SQLAlchemy Models & PostgreSQL)     │
└─────────────────────────────────────────┘
```

#### 2. Dependency Injection
Central `ApplicationCore` class manages all dependencies using lazy initialization:

```python
class ApplicationCore:
    def __init__(self, config: Config):
        self._config = config
        self._db_engine = None
        self._session_factory = None
        # Managers initialized on demand
        
    @property
    def customer_manager(self) -> CustomerManager:
        if not hasattr(self, '_customer_manager'):
            self._customer_manager = CustomerManager(self)
        return self._customer_manager
```

#### 3. Asynchronous Processing Model
- Main thread handles UI interactions
- Separate thread runs asyncio event loop
- Background tasks for I/O operations
- Thread-safe communication via Qt signals

#### 4. Result Pattern
All operations return Result objects for explicit error handling:

```python
@dataclass
class Result[T]:
    success: bool
    data: Optional[T] = None
    error: Optional[str] = None
```

#### 5. Data Transfer Objects (DTOs)
Clean separation between database models and business objects:

```python
@dataclass
class CustomerDTO:
    id: Optional[int]
    name: str
    email: str
    phone: str
    address: str
    loyalty_points: int = 0
```

### Component Architecture

#### ApplicationCore
Central dependency container and application lifecycle manager:
- Lazy initialization of all managers
- Configuration management
- Database connection pooling
- Event bus for inter-component communication

#### Managers
Business logic orchestrators that coordinate between services:
- CustomerManager: Customer lifecycle and loyalty programs
- InventoryManager: Stock management and tracking
- SalesManager: Transaction processing and reporting
- PaymentManager: Payment processing and reconciliation
- GSTManager: Tax calculation and compliance
- ReportManager: Report generation and analytics

#### Services
Data access layer implementing repository pattern:
- CustomerService: CRUD operations for customers
- ProductService: Product catalog management
- TransactionService: Sales transaction persistence
- InventoryService: Stock level management
- ConfigurationService: System settings

#### UI Components
PySide6-based presentation layer:
- MainWindow: Application shell and navigation
- POSWidget: Point of sale interface
- InventoryWidget: Stock management UI
- CustomerWidget: Customer management interface
- ReportsWidget: Reporting and analytics dashboard
- SettingsWidget: Configuration interface

## Database Schema Design

### Core Tables

#### 1. System Tables

```sql
-- System configuration and settings
CREATE TABLE system_config (
    id SERIAL PRIMARY KEY,
    key VARCHAR(100) UNIQUE NOT NULL,
    value JSONB NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Audit log for all system changes
CREATE TABLE audit_log (
    id SERIAL PRIMARY KEY,
    table_name VARCHAR(100) NOT NULL,
    record_id INTEGER NOT NULL,
    action VARCHAR(20) NOT NULL, -- INSERT, UPDATE, DELETE
    user_id INTEGER NOT NULL,
    changes JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 2. User Management Tables

```sql
-- System users and authentication
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role_id INTEGER NOT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (role_id) REFERENCES roles(id)
);

-- User roles and permissions
CREATE TABLE roles (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    permissions JSONB NOT NULL, -- Array of permission strings
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- User sessions for security
CREATE TABLE user_sessions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL,
    token VARCHAR(255) UNIQUE NOT NULL,
    ip_address INET,
    user_agent TEXT,
    expires_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

#### 3. Customer Management Tables

```sql
-- Customer information
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(20) UNIQUE NOT NULL,
    company_name VARCHAR(255),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(255),
    phone VARCHAR(20),
    mobile VARCHAR(20),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    postal_code VARCHAR(10),
    country VARCHAR(2) DEFAULT 'SG',
    customer_type VARCHAR(20) DEFAULT 'RETAIL', -- RETAIL, WHOLESALE, VIP
    credit_limit DECIMAL(15,2) DEFAULT 0,
    current_balance DECIMAL(15,2) DEFAULT 0,
    loyalty_points INTEGER DEFAULT 0,
    tax_id VARCHAR(50), -- For B2B customers
    notes TEXT,
    is_active BOOLEAN DEFAULT TRUE,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Customer loyalty transactions
CREATE TABLE loyalty_transactions (
    id SERIAL PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    transaction_type VARCHAR(20) NOT NULL, -- EARNED, REDEEMED, EXPIRED, ADJUSTED
    points INTEGER NOT NULL,
    reference_type VARCHAR(50), -- SALE, RETURN, MANUAL, PROMOTION
    reference_id INTEGER,
    description TEXT,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES customers(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);
```

#### 4. Product and Inventory Tables

```sql
-- Product categories
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    parent_id INTEGER,
    description TEXT,
    display_order INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (parent_id) REFERENCES categories(id)
);

-- Product information
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER,
    brand VARCHAR(100),
    unit_of_measure VARCHAR(20) DEFAULT 'PIECE',
    cost_price DECIMAL(15,2) NOT NULL,
    selling_price DECIMAL(15,2) NOT NULL,
    tax_rate DECIMAL(5,2) DEFAULT 8.0, -- GST rate
    is_taxable BOOLEAN DEFAULT TRUE,
    is_active BOOLEAN DEFAULT TRUE,
    track_inventory BOOLEAN DEFAULT TRUE,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 0,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Product variants (size, color, etc.)
CREATE TABLE product_variants (
    id SERIAL PRIMARY KEY,
    product_id INTEGER NOT NULL,
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    variant_name VARCHAR(100) NOT NULL,
    attributes JSONB, -- {"size": "L", "color": "Blue"}
    cost_price DECIMAL(15,2),
    selling_price DECIMAL(15,2),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(id)
);

-- Inventory tracking
CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER NOT NULL,
    variant_id INTEGER,
    location_id INTEGER NOT NULL,
    quantity INTEGER NOT NULL DEFAULT 0,
    reserved_quantity INTEGER DEFAULT 0,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(id),
    FOREIGN KEY (variant_id) REFERENCES product_variants(id),
    FOREIGN KEY (location_id) REFERENCES locations(id),
    UNIQUE(product_id, variant_id, location_id)
);

-- Inventory movements
CREATE TABLE inventory_movements (
    id SERIAL PRIMARY KEY,
    product_id INTEGER NOT NULL,
    variant_id INTEGER
```sql
-- Inventory movements (continued)
CREATE TABLE inventory_movements (
    id SERIAL PRIMARY KEY,
    product_id INTEGER NOT NULL,
    variant_id INTEGER,
    location_id INTEGER NOT NULL,
    movement_type VARCHAR(20) NOT NULL, -- PURCHASE, SALE, RETURN, ADJUSTMENT, TRANSFER
    quantity INTEGER NOT NULL,
    reference_type VARCHAR(50),
    reference_id INTEGER,
    cost_price DECIMAL(15,2),
    notes TEXT,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(id),
    FOREIGN KEY (variant_id) REFERENCES product_variants(id),
    FOREIGN KEY (location_id) REFERENCES locations(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Store locations
CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    type VARCHAR(20) DEFAULT 'STORE', -- STORE, WAREHOUSE
    address TEXT,
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 5. Sales and Transaction Tables

```sql
-- Sales transactions
CREATE TABLE sales_transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    location_id INTEGER NOT NULL,
    customer_id INTEGER,
    transaction_date TIMESTAMP NOT NULL,
    subtotal DECIMAL(15,2) NOT NULL,
    tax_amount DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    total_amount DECIMAL(15,2) NOT NULL,
    paid_amount DECIMAL(15,2) DEFAULT 0,
    change_amount DECIMAL(15,2) DEFAULT 0,
    status VARCHAR(20) DEFAULT 'COMPLETED', -- DRAFT, COMPLETED, VOID, REFUNDED
    notes TEXT,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (location_id) REFERENCES locations(id),
    FOREIGN KEY (customer_id) REFERENCES customers(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Sales transaction items
CREATE TABLE sales_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    variant_id INTEGER,
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    tax_amount DECIMAL(15,2) NOT NULL,
    total_amount DECIMAL(15,2) NOT NULL,
    cost_price DECIMAL(15,2) NOT NULL, -- For profit calculation
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (transaction_id) REFERENCES sales_transactions(id),
    FOREIGN KEY (product_id) REFERENCES products(id),
    FOREIGN KEY (variant_id) REFERENCES product_variants(id)
);

-- Payment records
CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER NOT NULL,
    payment_method VARCHAR(50) NOT NULL, -- CASH, CREDIT_CARD, DEBIT_CARD, NETS, PAYNOW, etc.
    amount DECIMAL(15,2) NOT NULL,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1.0,
    reference_number VARCHAR(100), -- For card/online payments
    status VARCHAR(20) DEFAULT 'COMPLETED', -- PENDING, COMPLETED, FAILED, REFUNDED
    processed_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (transaction_id) REFERENCES sales_transactions(id)
);

-- Cash drawer sessions
CREATE TABLE cash_sessions (
    id SERIAL PRIMARY KEY,
    location_id INTEGER NOT NULL,
    user_id INTEGER NOT NULL,
    opening_amount DECIMAL(15,2) NOT NULL,
    closing_amount DECIMAL(15,2),
    expected_amount DECIMAL(15,2),
    difference_amount DECIMAL(15,2),
    status VARCHAR(20) DEFAULT 'OPEN', -- OPEN, CLOSED
    opened_at TIMESTAMP NOT NULL,
    closed_at TIMESTAMP,
    notes TEXT,
    FOREIGN KEY (location_id) REFERENCES locations(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

#### 6. Supplier and Purchase Tables

```sql
-- Supplier information
CREATE TABLE suppliers (
    id SERIAL PRIMARY KEY,
    supplier_code VARCHAR(20) UNIQUE NOT NULL,
    company_name VARCHAR(255) NOT NULL,
    contact_person VARCHAR(100),
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    payment_terms INTEGER DEFAULT 30, -- Days
    tax_id VARCHAR(50),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Purchase orders
CREATE TABLE purchase_orders (
    id SERIAL PRIMARY KEY,
    po_number VARCHAR(50) UNIQUE NOT NULL,
    supplier_id INTEGER NOT NULL,
    order_date DATE NOT NULL,
    expected_date DATE,
    subtotal DECIMAL(15,2) NOT NULL,
    tax_amount DECIMAL(15,2) NOT NULL,
    total_amount DECIMAL(15,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'DRAFT', -- DRAFT, SENT, PARTIAL, RECEIVED, CANCELLED
    notes TEXT,
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (supplier_id) REFERENCES suppliers(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Purchase order items
CREATE TABLE purchase_order_items (
    id SERIAL PRIMARY KEY,
    po_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    variant_id INTEGER,
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(15,2) NOT NULL,
    tax_amount DECIMAL(15,2) NOT NULL,
    total_amount DECIMAL(15,2) NOT NULL,
    received_quantity INTEGER DEFAULT 0,
    FOREIGN KEY (po_id) REFERENCES purchase_orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id),
    FOREIGN KEY (variant_id) REFERENCES product_variants(id)
);
```

#### 7. Accounting Tables

```sql
-- Chart of accounts
CREATE TABLE accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(100) NOT NULL,
    account_type VARCHAR(20) NOT NULL, -- ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE
    parent_id INTEGER,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (parent_id) REFERENCES accounts(id)
);

-- Journal entries
CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT,
    reference_type VARCHAR(50),
    reference_id INTEGER,
    status VARCHAR(20) DEFAULT 'POSTED', -- DRAFT, POSTED, VOID
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);

-- Journal entry lines
CREATE TABLE journal_lines (
    id SERIAL PRIMARY KEY,
    entry_id INTEGER NOT NULL,
    account_id INTEGER NOT NULL,
    debit_amount DECIMAL(15,2) DEFAULT 0,
    credit_amount DECIMAL(15,2) DEFAULT 0,
    description TEXT,
    FOREIGN KEY (entry_id) REFERENCES journal_entries(id),
    FOREIGN KEY (account_id) REFERENCES accounts(id),
    CHECK (debit_amount >= 0 AND credit_amount >= 0),
    CHECK (NOT (debit_amount > 0 AND credit_amount > 0))
);
```

#### 8. GST and Tax Tables

```sql
-- GST configuration
CREATE TABLE gst_config (
    id SERIAL PRIMARY KEY,
    effective_date DATE NOT NULL,
    standard_rate DECIMAL(5,2) NOT NULL,
    zero_rated_categories JSONB, -- Array of category IDs
    exempt_categories JSONB, -- Array of category IDs
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- GST returns
CREATE TABLE gst_returns (
    id SERIAL PRIMARY KEY,
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    box1_total_sales DECIMAL(15,2) NOT NULL, -- Total value of standard-rated supplies
    box2_total_purchases DECIMAL(15,2) NOT NULL, -- Total value of purchases
    box3_output_tax DECIMAL(15,2) NOT NULL, -- Output tax due
    box4_input_tax DECIMAL(15,2) NOT NULL, -- Input tax claimable
    box5_net_tax DECIMAL(15,2) NOT NULL, -- Net GST to be paid/claimed
    box6_total_exports DECIMAL(15,2) DEFAULT 0, -- Value of exports
    box7_total_exempt DECIMAL(15,2) DEFAULT 0, -- Value of exempt supplies
    status VARCHAR(20) DEFAULT 'DRAFT', -- DRAFT, SUBMITTED, ACCEPTED
    submission_date DATE,
    reference_number VARCHAR(50),
    created_by INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);
```

### Database Indexes and Constraints

```sql
-- Performance indexes
CREATE INDEX idx_customers_email ON customers(email);
CREATE INDEX idx_customers_phone ON customers(phone);
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_barcode ON products(barcode);
CREATE INDEX idx_sales_date ON sales_transactions(transaction_date);
CREATE INDEX idx_sales_customer ON sales_transactions(customer_id);
CREATE INDEX idx_inventory_product ON inventory(product_id);
CREATE INDEX idx_audit_table_record ON audit_log(table_name, record_id);

-- Triggers for automatic timestamp updates
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_customers_updated_at BEFORE UPDATE ON customers
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
    
CREATE TRIGGER update_products_updated_at BEFORE UPDATE ON products
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

-- Trigger for audit logging
CREATE OR REPLACE FUNCTION audit_trigger_function()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        INSERT INTO audit_log(table_name, record_id, action, user_id, changes)
        VALUES (TG_TABLE_NAME, NEW.id, TG_OP, current_setting('app.current_user_id')::INTEGER, row_to_json(NEW));
    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO audit_log(table_name, record_id, action, user_id, changes)
        VALUES (TG_TABLE_NAME, NEW.id, TG_OP, current_setting('app.current_user_id')::INTEGER, 
                jsonb_build_object('old', row_to_json(OLD), 'new', row_to_json(NEW)));
    ELSIF TG_OP = 'DELETE' THEN
        INSERT INTO audit_log(table_name, record_id, action, user_id, changes)
        VALUES (TG_TABLE_NAME, OLD.id, TG_OP, current_setting('app.current_user_id')::INTEGER, row_to_json(OLD));
    END IF;
    RETURN NULL;
END;
$$ language 'plpgsql';

-- Apply audit triggers to critical tables
CREATE TRIGGER audit_customers AFTER INSERT OR UPDATE OR DELETE ON customers
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();
    
CREATE TRIGGER audit_sales AFTER INSERT OR UPDATE OR DELETE ON sales_transactions
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();
```

## Codebase File Hierarchy

```
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── config.py                        # Configuration management
│   ├── constants.py                     # Application constants
│   ├── exceptions.py                    # Custom exceptions
│   ├── application_core.py              # Dependency injection container
│   │
│   ├── models/                          # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                      # Base model class
│   │   ├── user.py                      # User and authentication models
│   │   ├── customer.py                  # Customer models
│   │   ├── product.py                   # Product and inventory models
│   │   ├── sales.py                     # Sales transaction models
│   │   ├── supplier.py                  # Supplier and purchase models
│   │   ├── accounting.py                # Accounting models
│   │   └── gst.py                       # GST and tax models
│   │
│   ├── dto/                             # Data Transfer Objects
│   │   ├── __init__.py
│   │   ├── base.py                      # Base DTO and Result classes
│   │   ├── customer_dto.py              # Customer DTOs
│   │   ├── product_dto.py               # Product DTOs
│   │   ├── sales_dto.py                 # Sales DTOs
│   │   ├── payment_dto.py               # Payment DTOs
│   │   └── report_dto.py                # Reporting DTOs
│   │
│   ├── services/                        # Data access layer
│   │   ├── __init__.py
│   │   ├── base_service.py              # Base service class
│   │   ├── customer_service.py          # Customer data operations
│   │   ├── product_service.py           # Product data operations
│   │   ├── inventory_service.py         # Inventory operations
│   │   ├── sales_service.py             # Sales data operations
│   │   ├── payment_service.py           # Payment processing
│   │   ├── supplier_service.py          # Supplier operations
│   │   ├── user_service.py              # User management
│   │   └── configuration_service.py     # System configuration
│   │
│   ├── business_logic/                  # Business logic layer
│   │   ├── __init__.py
│   │   ├── customer_manager.py          # Customer business logic
│   │   ├── inventory_manager.py         # Inventory management
│   │   ├── sales_manager.py             # Sales processing
│   │   ├── payment_manager.py           # Payment handling
│   │   ├── promotion_manager.py         # Promotions and discounts
│   │   ├── loyalty_manager.py           # Loyalty program
│   │   └── report_manager.py            # Report generation
│   │
│   ├── accounting/                      # Accounting module
│   │   ├── __init__.py
│   │   ├── gst_manager.py               # GST calculations
│   │   ├── journal_manager.py           # Journal entries
│   │   ├── ledger_manager.py            # General ledger
│   │   └── financial_reports.py         # Financial reporting
│   │
│   ├── ui/                              # Presentation layer
│   │   ├── __init__.py
│   │   ├── main_window.py               # Main application window
│   │
<think>
The user is right, I didn't complete the PRD. I need to continue from where I left off in the codebase file hierarchy and complete all the remaining sections according to the table of contents I provided. Let me continue from the UI section of the file hierarchy.
</think>

```
│   │   ├── ui/                              # Presentation layer (continued)
│   │   ├── __init__.py
│   │   ├── main_window.py               # Main application window
│   │   ├── styles.py                    # Application styling
│   │   ├── base_widget.py               # Base widget class
│   │   │
│   │   ├── pos/                         # Point of Sale UI
│   │   │   ├── __init__.py
│   │   │   ├── pos_widget.py            # Main POS interface
│   │   │   ├── product_grid.py          # Product selection grid
│   │   │   ├── cart_widget.py           # Shopping cart display
│   │   │   ├── payment_dialog.py        # Payment processing dialog
│   │   │   ├── customer_display.py      # Customer-facing display
│   │   │   └── receipt_preview.py       # Receipt preview/print
│   │   │
│   │   ├── inventory/                   # Inventory management UI
│   │   │   ├── __init__.py
│   │   │   ├── inventory_widget.py      # Main inventory interface
│   │   │   ├── product_editor.py        # Product add/edit dialog
│   │   │   ├── stock_adjustment.py      # Stock adjustment dialog
│   │   │   ├── stock_transfer.py        # Inter-location transfer
│   │   │   └── barcode_scanner.py       # Barcode scanning interface
│   │   │
│   │   ├── customers/                   # Customer management UI
│   │   │   ├── __init__.py
│   │   │   ├── customer_widget.py       # Customer list/search
│   │   │   ├── customer_editor.py       # Customer add/edit dialog
│   │   │   ├── loyalty_widget.py        # Loyalty program interface
│   │   │   └── customer_history.py      # Purchase history view
│   │   │
│   │   ├── reports/                     # Reporting UI
│   │   │   ├── __init__.py
│   │   │   ├── reports_widget.py        # Main reports interface
│   │   │   ├── sales_reports.py         # Sales report views
│   │   │   ├── inventory_reports.py     # Inventory reports
│   │   │   ├── financial_reports.py     # Financial statements
│   │   │   ├── gst_reports.py           # GST reporting
│   │   │   └── chart_widgets.py         # Data visualization
│   │   │
│   │   ├── settings/                    # Settings UI
│   │   │   ├── __init__.py
│   │   │   ├── settings_widget.py       # Main settings interface
│   │   │   ├── user_management.py       # User/role configuration
│   │   │   ├── tax_settings.py          # GST/tax configuration
│   │   │   ├── payment_settings.py      # Payment method setup
│   │   │   └── system_settings.py       # General system settings
│   │   │
│   │   └── components/                  # Reusable UI components
│   │       ├── __init__.py
│   │       ├── search_widget.py         # Universal search component
│   │       ├── data_table.py            # Enhanced table widget
│   │       ├── date_picker.py           # Date selection widget
│   │       ├── number_pad.py            # Numeric input pad
│   │       └── loading_overlay.py       # Loading indicator
│   │
│   ├── integration/                     # External integrations
│   │   ├── __init__.py
│   │   ├── payment_gateways/
│   │   │   ├── __init__.py
│   │   │   ├── base_gateway.py          # Abstract payment gateway
│   │   │   ├── stripe_gateway.py        # Stripe integration
│   │   │   ├── nets_gateway.py          # NETS integration
│   │   │   └── paynow_gateway.py        # PayNow integration
│   │   │
│   │   ├── accounting_sync/
│   │   │   ├── __init__.py
│   │   │   ├── quickbooks_sync.py       # QuickBooks integration
│   │   │   └── xero_sync.py             # Xero integration
│   │   │
│   │   └── hardware/
│   │       ├── __init__.py
│   │       ├── printer_manager.py       # Receipt printer interface
│   │       ├── cash_drawer.py           # Cash drawer control
│   │       ├── barcode_scanner.py       # Scanner integration
│   │       └── customer_display.py      # Customer display driver
│   │
│   └── utils/                           # Utility modules
│       ├── __init__.py
│       ├── async_utils.py               # Async helper functions
│       ├── validators.py                # Data validation utilities
│       ├── formatters.py                # Number/date formatting
│       ├── security.py                  # Security utilities
│       ├── backup.py                    # Database backup utilities
│       └── logger.py                    # Logging configuration
│
├── tests/                               # Test suite
│   ├── __init__.py
│   ├── conftest.py                      # Pytest configuration
│   ├── fixtures/                        # Test fixtures
│   │   ├── __init__.py
│   │   ├── database.py                  # Database fixtures
│   │   ├── models.py                    # Model fixtures
│   │   └── ui.py                        # UI test fixtures
│   │
│   ├── unit/                            # Unit tests
│   │   ├── __init__.py
│   │   ├── test_models/
│   │   ├── test_services/
│   │   ├── test_managers/
│   │   └── test_utils/
│   │
│   ├── integration/                     # Integration tests
│   │   ├── __init__.py
│   │   ├── test_payment_flow.py
│   │   ├── test_inventory_sync.py
│   │   └── test_reporting.py
│   │
│   └── e2e/                            # End-to-end tests
│       ├── __init__.py
│       ├── test_pos_workflow.py
│       └── test_full_transaction.py
│
├── scripts/                             # Utility scripts
│   ├── __init__.py
│   ├── init_db.py                       # Database initialization
│   ├── migrate_db.py                    # Database migrations
│   ├── seed_data.py                     # Development data seeding
│   ├── backup_db.py                     # Database backup script
│   └── generate_reports.py              # Batch report generation
│
├── resources/                           # Application resources
│   ├── images/                          # UI images and icons
│   ├── fonts/                           # Custom fonts
│   ├── templates/                       # Report templates
│   │   ├── receipt.html
│   │   ├── invoice.html
│   │   └── reports/
│   └── translations/                    # i18n files
│       ├── en_US.json
│       ├── zh_CN.json
│       └── ms_MY.json
│
├── docs/                                # Documentation
│   ├── api/                             # API documentation
│   ├── user_guide/                      # User manual
│   ├── admin_guide/                     # Administrator guide
│   └── developer_guide/                 # Developer documentation
│
├── deployment/                          # Deployment configurations
│   ├── docker/
│   │   ├── Dockerfile
│   │   └── docker-compose.yml
│   ├── kubernetes/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   └── installer/
│       ├── windows/
│       ├── macos/
│       └── linux/
│
├── .github/                             # GitHub configurations
│   ├── workflows/
│   │   ├── ci.yml                       # Continuous integration
│   │   ├── release.yml                  # Release automation
│   │   └── codeql.yml                   # Security scanning
│   └── ISSUE_TEMPLATE/
│
├── requirements/                        # Dependency specifications
│   ├── base.txt                         # Core dependencies
│   ├── dev.txt                          # Development dependencies
│   └── prod.txt                         # Production dependencies
│
├── .env.example                         # Environment variables template
├── .gitignore                           # Git ignore rules
├── .pre-commit-config.yaml              # Pre-commit hooks
├── pyproject.toml                       # Project configuration
├── README.md                            # Project documentation
├── LICENSE                              # License file
└── setup.py                             # Package setup
```

## Application Modules and User Interaction

### System Architecture Diagram

```mermaid
graph TB
    subgraph "Presentation Layer"
        UI[PySide6 UI Components]
        MW[Main Window]
        POS[POS Widget]
        INV[Inventory Widget]
        CUST[Customer Widget]
        REP[Reports Widget]
        SET[Settings Widget]
    end
    
    subgraph "Business Logic Layer"
        AC[Application Core]
        CM[Customer Manager]
        IM[Inventory Manager]
        SM[Sales Manager]
        PM[Payment Manager]
        GM[GST Manager]
        RM[Report Manager]
    end
    
    subgraph "Data Access Layer"
        CS[Customer Service]
        PS[Product Service]
        IS[Inventory Service]
        SS[Sales Service]
        PAS[Payment Service]
        US[User Service]
    end
    
    subgraph "Persistence Layer"
        DB[(PostgreSQL Database)]
        CACHE[(Redis Cache)]
    end
    
    subgraph "External Systems"
        PG[Payment Gateways]
        ACC[Accounting Systems]
        HW[Hardware Devices]
    end
    
    UI --> AC
    MW --> POS
    MW --> INV
    MW --> CUST
    MW --> REP
    MW --> SET
    
    AC --> CM
    AC --> IM
    AC --> SM
    AC --> PM
    AC --> GM
    AC --> RM
    
    CM --> CS
    IM --> PS
    IM --> IS
    SM --> SS
    PM --> PAS
    
    CS --> DB
    PS --> DB
    IS --> DB
    SS --> DB
    PAS --> DB
    US --> DB
    
    PM --> PG
    RM --> ACC
    POS --> HW
```

### User Interaction Flow

#### 1. Point of Sale Transaction Flow

```mermaid
sequenceDiagram
    participant C as Cashier
    participant UI as POS UI
    participant SM as Sales Manager
    participant IM as Inventory Manager
    participant PM as Payment Manager
    participant DB as Database
    
    C->>UI: Scan/Select Product
    UI->>SM: Add to Cart
    SM->>IM: Check Availability
    IM->>DB: Query Stock
    DB-->>IM: Stock Level
    IM-->>SM: Availability Status
    SM-->>UI: Update Cart Display
    
    C->>UI: Process Payment
    UI->>PM: Initialize Payment
    PM->>PM: Calculate Total
    PM->>PM: Apply Discounts
    PM->>PM: Calculate GST
    PM-->>UI: Payment Summary
    
    C->>UI: Select Payment Method
    UI->>PM: Process Payment
    PM->>PG: Process Transaction
    PG-->>PM: Payment Result
    PM->>DB: Save Transaction
    PM->>IM: Update Inventory
    PM-->>UI: Transaction Complete
    UI-->>C: Print Receipt
```

#### 2. Inventory Management Flow

```mermaid
stateDiagram-v2
    [*] --> ProductList
    ProductList --> AddProduct: Click Add
    ProductList --> EditProduct: Select Product
    ProductList --> StockAdjustment: Adjust Stock
    
    AddProduct --> ProductForm
    EditProduct --> ProductForm
    ProductForm --> Validation
    Validation --> SaveProduct: Valid
    Validation --> ProductForm: Invalid
    SaveProduct --> ProductList
    
    StockAdjustment --> AdjustmentForm
    AdjustmentForm --> ConfirmAdjustment
    ConfirmAdjustment --> UpdateInventory
    UpdateInventory --> ProductList
    
    ProductList --> StockTransfer: Transfer Stock
    StockTransfer --> TransferForm
    TransferForm --> ConfirmTransfer
    ConfirmTransfer --> UpdateLocations
    UpdateLocations --> ProductList
```

## Key Application Modules Description

### 1. Application Core (`app/application_core.py`)

The ApplicationCore serves as the central dependency injection container and application lifecycle manager. It implements lazy initialization for all managers and services, ensuring efficient resource usage.

```python
class ApplicationCore:
    """Central application container managing all dependencies and services."""
    
    def __init__(self, config: Config):
        self._config = config
        self._db_engine = None
        self._session_factory = None
        self._event_bus = EventBus()
        self._cache = None
        self._logger = self._setup_logging()
        
    @property
    def customer_manager(self) -> CustomerManager:
        """Lazy initialization of CustomerManager."""
        if not hasattr(self, '_customer_manager'):
            self._customer_manager = CustomerManager(self)
        return self._customer_manager
    
    @property
    def inventory_manager(self) -> InventoryManager:
        """Lazy initialization of InventoryManager."""
        if not hasattr(self, '_inventory_manager'):
            self._inventory_manager = InventoryManager(self)
        return self._inventory_manager
    
    @property
    def sales_manager(self) -> SalesManager:
        """Lazy initialization of SalesManager."""
        if not hasattr(self, '_sales_manager'):
            self._sales_manager = SalesManager(self)
        return self._sales_manager
    
    async def initialize(self):
        """Initialize core application components."""
        await self._init_database()
        await self._init_cache()
        await self._load_configuration()
        
    async def shutdown(self):
        """Graceful shutdown of application components."""
        await self._close_database()
        await self._close_cache()
```

### 2. Sales Manager (`app/business_logic/sales_manager.py`)

The SalesManager orchestrates the entire sales process, coordinating between inventory, payment, and customer management systems.

```python
class SalesManager:
    """Manages sales transactions and related business logic."""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        self._active_transactions: Dict[str, SalesTransaction] = {}
        
    async def create_transaction(self, user_id: int, location_id: int) -> Result[SalesTransactionDTO]:
        """Create a new sales transaction."""
        try:
            # Generate unique transaction number
            transaction_number = self._generate_transaction_number()
            
            # Create transaction object
            transaction = SalesTransaction(
                transaction_number=transaction_number,
                user_id=user_id,
                location_id=location_id,
                items=[],
                status=TransactionStatus.DRAFT
            )
            
            # Store in active transactions
            self._active_transactions[transaction_number] = transaction
            
            # Convert to DTO
            dto = self._to_dto(transaction)
            
            return Result(success=True, data=dto)
            
        except Exception as e:
            self._app_core.logger.error(f"Failed to create transaction: {e}")
            return Result(success
<think>
I need to continue from where I left off in the Sales Manager code example and complete the rest of the PRD including all remaining sections.
</think>

```python
            return Result(success=False, error=str(e))
    
    async def add_item(self, transaction_id: str, product_id: int, 
                      quantity: int) -> Result[SalesItemDTO]:
        """Add item to transaction."""
        try:
            # Validate transaction exists
            if transaction_id not in self._active_transactions:
                return Result(success=False, error="Transaction not found")
            
            transaction = self._active_transactions[transaction_id]
            
            # Check inventory availability
            availability = await self._app_core.inventory_manager.check_availability(
                product_id, quantity, transaction.location_id
            )
            
            if not availability.success:
                return Result(success=False, error=availability.error)
            
            # Get product details
            product = await self._app_core.product_service.get_by_id(product_id)
            
            # Calculate pricing
            unit_price = product.selling_price
            discount = await self._calculate_discount(product_id, quantity)
            tax = await self._app_core.gst_manager.calculate_tax(
                unit_price * quantity - discount
            )
            
            # Create sales item
            item = SalesItem(
                product_id=product_id,
                quantity=quantity,
                unit_price=unit_price,
                discount_amount=discount,
                tax_amount=tax,
                total_amount=(unit_price * quantity) - discount + tax
            )
            
            # Add to transaction
            transaction.items.append(item)
            
            # Update transaction totals
            self._update_transaction_totals(transaction)
            
            return Result(success=True, data=self._item_to_dto(item))
            
        except Exception as e:
            self._app_core.logger.error(f"Failed to add item: {e}")
            return Result(success=False, error=str(e))
    
    async def process_payment(self, transaction_id: str, 
                            payments: List[PaymentDTO]) -> Result[TransactionDTO]:
        """Process payment for transaction."""
        try:
            transaction = self._active_transactions.get(transaction_id)
            if not transaction:
                return Result(success=False, error="Transaction not found")
            
            # Validate payment amount
            total_payment = sum(p.amount for p in payments)
            if total_payment < transaction.total_amount:
                return Result(success=False, error="Insufficient payment")
            
            # Process each payment
            payment_results = []
            for payment in payments:
                result = await self._app_core.payment_manager.process_payment(
                    transaction_id, payment
                )
                if not result.success:
                    # Rollback previous payments
                    await self._rollback_payments(payment_results)
                    return Result(success=False, error=result.error)
                payment_results.append(result.data)
            
            # Update inventory
            for item in transaction.items:
                await self._app_core.inventory_manager.deduct_stock(
                    item.product_id, item.quantity, transaction.location_id
                )
            
            # Update customer loyalty points
            if transaction.customer_id:
                points = int(transaction.total_amount)
                await self._app_core.loyalty_manager.add_points(
                    transaction.customer_id, points, transaction_id
                )
            
            # Save transaction to database
            saved = await self._app_core.sales_service.create_transaction(transaction)
            
            # Generate journal entries
            await self._app_core.journal_manager.create_sales_entry(saved.data)
            
            # Remove from active transactions
            del self._active_transactions[transaction_id]
            
            return Result(success=True, data=saved.data)
            
        except Exception as e:
            self._app_core.logger.error(f"Payment processing failed: {e}")
            return Result(success=False, error=str(e))
```

### 3. Inventory Manager (`app/business_logic/inventory_manager.py`)

The InventoryManager handles all inventory-related operations including stock tracking, transfers, and adjustments.

```python
class InventoryManager:
    """Manages inventory operations and stock levels."""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        self._stock_cache = TTLCache(maxsize=1000, ttl=300)  # 5-minute cache
        
    async def check_availability(self, product_id: int, quantity: int, 
                               location_id: int) -> Result[bool]:
        """Check if sufficient stock is available."""
        try:
            # Check cache first
            cache_key = f"{product_id}:{location_id}"
            if cache_key in self._stock_cache:
                current_stock = self._stock_cache[cache_key]
            else:
                # Query database
                inventory = await self._app_core.inventory_service.get_stock_level(
                    product_id, location_id
                )
                current_stock = inventory.quantity - inventory.reserved_quantity
                self._stock_cache[cache_key] = current_stock
            
            available = current_stock >= quantity
            return Result(success=True, data=available)
            
        except Exception as e:
            self._app_core.logger.error(f"Availability check failed: {e}")
            return Result(success=False, error=str(e))
    
    async def transfer_stock(self, product_id: int, from_location: int,
                           to_location: int, quantity: int, 
                           user_id: int) -> Result[StockTransferDTO]:
        """Transfer stock between locations."""
        try:
            # Validate source stock
            availability = await self.check_availability(
                product_id, quantity, from_location
            )
            if not availability.data:
                return Result(success=False, error="Insufficient stock at source")
            
            # Create transfer record
            transfer = StockTransfer(
                product_id=product_id,
                from_location_id=from_location,
                to_location_id=to_location,
                quantity=quantity,
                user_id=user_id,
                status=TransferStatus.PENDING
            )
            
            # Begin transaction
            async with self._app_core.db_session() as session:
                # Deduct from source
                await self._app_core.inventory_service.adjust_stock(
                    product_id, from_location, -quantity, 
                    "TRANSFER_OUT", transfer.id, session
                )
                
                # Add to destination
                await self._app_core.inventory_service.adjust_stock(
                    product_id, to_location, quantity,
                    "TRANSFER_IN", transfer.id, session
                )
                
                # Save transfer record
                transfer.status = TransferStatus.COMPLETED
                session.add(transfer)
                await session.commit()
            
            # Clear cache
            self._clear_stock_cache(product_id, [from_location, to_location])
            
            return Result(success=True, data=self._to_transfer_dto(transfer))
            
        except Exception as e:
            self._app_core.logger.error(f"Stock transfer failed: {e}")
            return Result(success=False, error=str(e))
    
    async def perform_stock_take(self, location_id: int, 
                               counts: List[StockCountDTO],
                               user_id: int) -> Result[StockTakeDTO]:
        """Perform stock take and create adjustments."""
        try:
            adjustments = []
            
            async with self._app_core.db_session() as session:
                for count in counts:
                    # Get current stock
                    current = await self._app_core.inventory_service.get_stock_level(
                        count.product_id, location_id, session
                    )
                    
                    difference = count.counted_quantity - current.quantity
                    
                    if difference != 0:
                        # Create adjustment
                        adjustment = await self._app_core.inventory_service.adjust_stock(
                            count.product_id, location_id, difference,
                            "STOCK_TAKE", None, session
                        )
                        adjustments.append(adjustment)
                
                # Create stock take record
                stock_take = StockTake(
                    location_id=location_id,
                    user_id=user_id,
                    adjustments=adjustments,
                    status=StockTakeStatus.COMPLETED
                )
                
                session.add(stock_take)
                await session.commit()
            
            # Clear cache for location
            self._clear_location_cache(location_id)
            
            return Result(success=True, data=self._to_stock_take_dto(stock_take))
            
        except Exception as e:
            self._app_core.logger.error(f"Stock take failed: {e}")
            return Result(success=False, error=str(e))
```

### 4. Payment Manager (`app/business_logic/payment_manager.py`)

The PaymentManager handles all payment processing including integration with various payment gateways.

```python
class PaymentManager:
    """Manages payment processing and gateway integrations."""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        self._gateways = self._initialize_gateways()
        
    def _initialize_gateways(self) -> Dict[str, PaymentGateway]:
        """Initialize payment gateway integrations."""
        return {
            PaymentMethod.CREDIT_CARD: StripeGateway(self._app_core.config),
            PaymentMethod.DEBIT_CARD: StripeGateway(self._app_core.config),
            PaymentMethod.NETS: NETSGateway(self._app_core.config),
            PaymentMethod.PAYNOW: PayNowGateway(self._app_core.config),
        }
    
    async def process_payment(self, transaction_id: str,
                            payment: PaymentDTO) -> Result[PaymentResultDTO]:
        """Process a payment through appropriate gateway."""
        try:
            # Handle cash payments directly
            if payment.method == PaymentMethod.CASH:
                return await self._process_cash_payment(transaction_id, payment)
            
            # Get appropriate gateway
            gateway = self._gateways.get(payment.method)
            if not gateway:
                return Result(success=False, error="Unsupported payment method")
            
            # Process through gateway
            gateway_result = await gateway.process_payment(
                amount=payment.amount,
                currency=payment.currency,
                reference=transaction_id,
                metadata=payment.metadata
            )
            
            if not gateway_result.success:
                return Result(success=False, error=gateway_result.error)
            
            # Save payment record
            payment_record = Payment(
                transaction_id=transaction_id,
                method=payment.method,
                amount=payment.amount,
                currency=payment.currency,
                reference_number=gateway_result.data.reference_number,
                status=PaymentStatus.COMPLETED,
                gateway_response=gateway_result.data.raw_response
            )
            
            saved = await self._app_core.payment_service.create_payment(payment_record)
            
            # Create journal entry
            await self._create_payment_journal_entry(payment_record)
            
            return Result(success=True, data=self._to_payment_result_dto(saved.data))
            
        except Exception as e:
            self._app_core.logger.error(f"Payment processing failed: {e}")
            return Result(success=False, error=str(e))
    
    async def process_refund(self, payment_id: int, amount: Decimal,
                           reason: str) -> Result[RefundDTO]:
        """Process a refund for a previous payment."""
        try:
            # Get original payment
            payment = await self._app_core.payment_service.get_by_id(payment_id)
            if not payment:
                return Result(success=False, error="Payment not found")
            
            # Validate refund amount
            if amount > payment.amount:
                return Result(success=False, error="Refund exceeds original payment")
            
            # Process refund through gateway
            if payment.method != PaymentMethod.CASH:
                gateway = self._gateways.get(payment.method)
                refund_result = await gateway.process_refund(
                    payment.reference_number, amount
                )
                
                if not refund_result.success:
                    return Result(success=False, error=refund_result.error)
            
            # Create refund record
            refund = Refund(
                payment_id=payment_id,
                amount=amount,
                reason=reason,
                status=RefundStatus.COMPLETED,
                reference_number=refund_result.data.reference_number
                    if payment.method != PaymentMethod.CASH else None
            )
            
            saved = await self._app_core.payment_service.create_refund(refund)
            
            # Create journal entry
            await self._create_refund_journal_entry(refund)
            
            return Result(success=True, data=self._to_refund_dto(saved.data))
            
        except Exception as e:
            self._app_core.logger.error(f"Refund processing failed: {e}")
            return Result(success=False, error=str(e))
```

### 5. GST Manager (`app/accounting/gst_manager.py`)

The GSTManager handles all GST-related calculations and reporting for Singapore compliance.

```python
class GSTManager:
    """Manages GST calculations and compliance reporting."""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        self._gst_config = None
        self._load_gst_config()
        
    async def _load_gst_config(self):
        """Load current GST configuration."""
        config = await self._app_core.configuration_service.get_gst_config()
        self._gst_config = config.data
    
    def calculate_tax(self, amount: Decimal, tax_type: str = "STANDARD") -> Decimal:
        """Calculate GST for given amount."""
        if tax_type == "ZERO_RATED" or tax_type == "EXEMPT":
            return Decimal("0.00")
        
        rate = self._gst_config.standard_rate / 100
        return round(amount * rate / (1 + rate), 2)  # Tax-inclusive calculation
    
    async def generate_gst_return(self, start_date: date, 
                                end_date: date) -> Result[GSTReturnDTO]:
        """Generate GST return for specified period."""
        try:
            # Get all transactions for period
            sales = await self._app_core.sales_service.get_by_date_range(
                start_date, end_date
            )
            
            purchases = await self._app_core.purchase_service.get_by_date_range(
                start_date, end_date
            )
            
            # Calculate boxes
            box1 = Decimal("0.00")  # Total value of standard-rated supplies
            box2 = Decimal("0.00")  # Total value of purchases
            box3 = Decimal("0.00")  # Output tax due
            box4 = Decimal("0.00")  # Input tax claimable
            box6 = Decimal("0.00")  # Total value of exports
            box7 = Decimal("0.00")  # Total value of exempt supplies
            
            # Process sales
            for sale in sales.data:
                if sale.tax_type == "STANDARD":
                    box1 += sale.subtotal
                    box3 += sale.tax_amount
                elif sale.tax_type == "ZERO_RATED":
                    box6 += sale.subtotal
                elif sale.tax_type == "EXEMPT":
                    box7 += sale.subtotal
            
            # Process purchases
            for purchase
<think>
I need to continue from where I left off in the GST Manager code and complete the rest of the PRD, including the remaining sections like Development Environment Setup, Production Environment Setup, Security Considerations, Testing Strategy, Deployment Strategy, Compliance and Regulatory Requirements, Performance Requirements, and Future Enhancements.
</think>

```python
            # Process purchases
            for purchase in purchases.data:
                if purchase.tax_type == "STANDARD":
                    box2 += purchase.subtotal
                    box4 += purchase.tax_amount
            
            # Calculate net GST
            box5 = box3 - box4  # Net GST to be paid/claimed
            
            # Create GST return record
            gst_return = GSTReturn(
                period_start=start_date,
                period_end=end_date,
                box1_total_sales=box1,
                box2_total_purchases=box2,
                box3_output_tax=box3,
                box4_input_tax=box4,
                box5_net_tax=box5,
                box6_total_exports=box6,
                box7_total_exempt=box7,
                status=GSTReturnStatus.DRAFT
            )
            
            saved = await self._app_core.gst_service.create_return(gst_return)
            
            return Result(success=True, data=self._to_gst_return_dto(saved.data))
            
        except Exception as e:
            self._app_core.logger.error(f"GST return generation failed: {e}")
            return Result(success=False, error=str(e))
    
    async def submit_gst_return(self, return_id: int) -> Result[GSTSubmissionDTO]:
        """Submit GST return to IRAS."""
        try:
            # Get return data
            gst_return = await self._app_core.gst_service.get_by_id(return_id)
            if not gst_return:
                return Result(success=False, error="GST return not found")
            
            # Validate return
            validation = self._validate_gst_return(gst_return)
            if not validation.success:
                return Result(success=False, error=validation.error)
            
            # Submit to IRAS API (when available)
            # For now, generate submission file
            submission_data = self._prepare_submission_data(gst_return)
            
            # Update return status
            gst_return.status = GSTReturnStatus.SUBMITTED
            gst_return.submission_date = datetime.now()
            
            await self._app_core.gst_service.update(gst_return)
            
            return Result(success=True, data=submission_data)
            
        except Exception as e:
            self._app_core.logger.error(f"GST submission failed: {e}")
            return Result(success=False, error=str(e))
```

### 6. Report Manager (`app/business_logic/report_manager.py`)

The ReportManager generates various business reports and analytics.

```python
class ReportManager:
    """Manages report generation and business analytics."""
    
    def __init__(self, app_core: ApplicationCore):
        self._app_core = app_core
        self._report_cache = TTLCache(maxsize=100, ttl=3600)  # 1-hour cache
        
    async def generate_sales_report(self, start_date: date, end_date: date,
                                  group_by: str = "day") -> Result[SalesReportDTO]:
        """Generate sales report for specified period."""
        try:
            cache_key = f"sales:{start_date}:{end_date}:{group_by}"
            
            # Check cache
            if cache_key in self._report_cache:
                return Result(success=True, data=self._report_cache[cache_key])
            
            # Get sales data
            sales_data = await self._app_core.sales_service.get_sales_summary(
                start_date, end_date, group_by
            )
            
            # Calculate metrics
            total_sales = sum(s.total_amount for s in sales_data)
            total_transactions = len(sales_data)
            average_transaction = total_sales / total_transactions if total_transactions > 0 else 0
            
            # Get top products
            top_products = await self._app_core.sales_service.get_top_products(
                start_date, end_date, limit=10
            )
            
            # Get sales by category
            category_sales = await self._app_core.sales_service.get_sales_by_category(
                start_date, end_date
            )
            
            # Build report
            report = SalesReportDTO(
                period_start=start_date,
                period_end=end_date,
                total_sales=total_sales,
                total_transactions=total_transactions,
                average_transaction=average_transaction,
                sales_data=sales_data,
                top_products=top_products,
                category_breakdown=category_sales,
                generated_at=datetime.now()
            )
            
            # Cache report
            self._report_cache[cache_key] = report
            
            return Result(success=True, data=report)
            
        except Exception as e:
            self._app_core.logger.error(f"Sales report generation failed: {e}")
            return Result(success=False, error=str(e))
    
    async def generate_inventory_report(self, location_id: Optional[int] = None) -> Result[InventoryReportDTO]:
        """Generate inventory valuation and status report."""
        try:
            # Get inventory data
            inventory_data = await self._app_core.inventory_service.get_inventory_summary(
                location_id
            )
            
            # Calculate metrics
            total_value = Decimal("0.00")
            low_stock_items = []
            out_of_stock_items = []
            
            for item in inventory_data:
                item_value = item.quantity * item.cost_price
                total_value += item_value
                
                if item.quantity == 0:
                    out_of_stock_items.append(item)
                elif item.quantity <= item.reorder_point:
                    low_stock_items.append(item)
            
            # Get inventory turnover
            turnover_data = await self._calculate_inventory_turnover()
            
            # Build report
            report = InventoryReportDTO(
                total_items=len(inventory_data),
                total_value=total_value,
                low_stock_count=len(low_stock_items),
                out_of_stock_count=len(out_of_stock_items),
                low_stock_items=low_stock_items,
                out_of_stock_items=out_of_stock_items,
                turnover_data=turnover_data,
                generated_at=datetime.now()
            )
            
            return Result(success=True, data=report)
            
        except Exception as e:
            self._app_core.logger.error(f"Inventory report generation failed: {e}")
            return Result(success=False, error=str(e))
```

## Development Environment Setup

### Prerequisites

1. **Python 3.11 or higher**
   ```bash
   # Check Python version
   python --version
   ```

2. **PostgreSQL 15 or higher**
   ```bash
   # Install PostgreSQL
   # Ubuntu/Debian
   sudo apt-get install postgresql-15 postgresql-client-15
   
   # macOS with Homebrew
   brew install postgresql@15
   
   # Windows
   # Download installer from https://www.postgresql.org/download/windows/
   ```

3. **Redis (for caching)**
   ```bash
   # Ubuntu/Debian
   sudo apt-get install redis-server
   
   # macOS with Homebrew
   brew install redis
   
   # Windows
   # Download from https://github.com/microsoftarchive/redis/releases
   ```

4. **Git**
   ```bash
   # Clone repository
   git clone https://github.com/your-org/sg-pos-system.git
   cd sg-pos-system
   ```

### Environment Setup

1. **Create Python Virtual Environment**
   ```bash
   # Create virtual environment
   python -m venv venv
   
   # Activate virtual environment
   # Linux/macOS
   source venv/bin/activate
   
   # Windows
   venv\Scripts\activate
   ```

2. **Install Dependencies**
   ```bash
   # Install development dependencies
   pip install -r requirements/dev.txt
   
   # Install pre-commit hooks
   pre-commit install
   ```

3. **Database Setup**
   ```bash
   # Create database
   createdb sg_pos_dev
   
   # Run migrations
   python scripts/init_db.py --env development
   
   # Seed development data
   python scripts/seed_data.py
   ```

4. **Environment Configuration**
   ```bash
   # Copy environment template
   cp .env.example .env.development
   
   # Edit .env.development with your settings
   ```

   Example `.env.development`:
   ```env
   # Database
   DATABASE_URL=postgresql://postgres:password@localhost:5432/sg_pos_dev
   DATABASE_POOL_SIZE=5
   DATABASE_MAX_OVERFLOW=10
   
   # Redis
   REDIS_URL=redis://localhost:6379/0
   
   # Application
   APP_ENV=development
   APP_DEBUG=true
   APP_SECRET_KEY=dev-secret-key-change-in-production
   
   # Payment Gateways
   STRIPE_API_KEY=sk_test_...
   STRIPE_WEBHOOK_SECRET=whsec_test_...
   
   # External APIs
   EXCHANGE_RATE_API_KEY=your-api-key
   
   # Logging
   LOG_LEVEL=DEBUG
   LOG_FILE=logs/development.log
   ```

5. **IDE Configuration**

   **VS Code**
   ```json
   // .vscode/settings.json
   {
     "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python",
     "python.linting.enabled": true,
     "python.linting.pylintEnabled": false,
     "python.linting.flake8Enabled": true,
     "python.formatting.provider": "black",
     "python.testing.pytestEnabled": true,
     "python.testing.pytestArgs": ["tests"],
     "editor.formatOnSave": true,
     "editor.codeActionsOnSave": {
       "source.organizeImports": true
     }
   }
   ```

   **PyCharm**
   - Set Project Interpreter to virtual environment
   - Enable Django support (for templates)
   - Configure code style to use Black
   - Set up database connection for SQL support

### Running the Application

1. **Start Required Services**
   ```bash
   # Start PostgreSQL
   sudo systemctl start postgresql  # Linux
   brew services start postgresql@15  # macOS
   
   # Start Redis
   sudo systemctl start redis  # Linux
   brew services start redis  # macOS
   ```

2. **Run Application**
   ```bash
   # Run in development mode
   python app/main.py --env development
   ```

3. **Run Tests**
   ```bash
   # Run all tests
   pytest
   
   # Run with coverage
   pytest --cov=app --cov-report=html
   
   # Run specific test file
   pytest tests/unit/test_sales_manager.py
   
   # Run tests in parallel
   pytest -n auto
   ```

4. **Code Quality Checks**
   ```bash
   # Format code
   black app tests
   
   # Run linter
   ruff app tests
   
   # Type checking
   mypy app
   
   # All checks (via pre-commit)
   pre-commit run --all-files
   ```

## Production Environment Setup

### Server Requirements

1. **Hardware Requirements**
   - CPU: 4+ cores (8+ recommended)
   - RAM: 8GB minimum (16GB recommended)
   - Storage: 100GB SSD minimum
   - Network: Stable internet connection

2. **Operating System**
   - Ubuntu 22.04 LTS (recommended)
   - CentOS 8/RHEL 8
   - Windows Server 2019+

### Production Setup

1. **System Preparation**
   ```bash
   # Update system
   sudo apt update && sudo apt upgrade -y
   
   # Install required packages
   sudo apt install -y python3.11 python3.11-venv python3.11-dev \
     postgresql-15 postgresql-client-15 redis-server nginx \
     supervisor git build-essential
   
   # Create application user
   sudo useradd -m -s /bin/bash sgpos
   sudo usermod -aG sudo sgpos
   ```

2. **PostgreSQL Configuration**
   ```bash
   # Configure PostgreSQL
   sudo -u postgres psql
   
   CREATE USER sgpos_prod WITH PASSWORD 'strong-password';
   CREATE DATABASE sg_pos_prod OWNER sgpos_prod;
   GRANT ALL PRIVILEGES ON DATABASE sg_pos_prod TO sgpos_prod;
   \q
   
   # Edit PostgreSQL configuration
   sudo nano /etc/postgresql/15/main/postgresql.conf
   ```
   
   Key settings:
   ```conf
   max_connections = 200
   shared_buffers = 256MB
   effective_cache_size = 1GB
   maintenance_work_mem = 64MB
   checkpoint_completion_target = 0.9
   wal_buffers = 16MB
   default_statistics_target = 100
   random_page_cost = 1.1
   effective_io_concurrency = 200
   work_mem = 4MB
   min_wal_size = 1GB
   max_wal_size = 4GB
   ```

3. **Application Deployment**
   ```bash
   # Switch to application user
   sudo su - sgpos
   
   # Clone repository
   git clone https://github.com/your-org/sg-pos-system.git /opt/sgpos
   cd /opt/sgpos
   
   # Create virtual environment
   python3.11 -m venv venv
   source venv/bin/activate
   
   # Install production dependencies
   pip install -r requirements/prod.txt
   
   # Set up environment
   cp .env.example .env.production
   # Edit .env.production with production settings
   
   # Initialize database
   python scripts/init_db.py --env production
   ```

4. **Supervisor Configuration**
   ```ini
   # /etc/supervisor/conf.d/sgpos.conf
   [program:sgpos]
   command=/opt/sgpos/venv/bin/python /opt/sgpos/app/main.py --env production
   directory=/opt/sgpos
   user=sgpos
   autostart=true
   autorestart=true
   redirect_stderr=true
   stdout_logfile=/var/log/sgpos/app.log
   environment=PATH="/opt/sgpos/venv/bin",PYTHONPATH="/opt/sgpos"
   ```

5. **Nginx Configuration** (for API endpoints)
   ```nginx
   # /etc/nginx/sites-available/sgpos
   server {
       listen 80;
       server_name pos.yourdomain.com;
       
       location /api {
           proxy_pass http://localhost:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
       
       location /static {
           alias /opt/sgpos/static;
           expires 30d;
       }
   }
   ```

6. **SSL Configuration**
   ```bash
   # Install Certbot
   sudo apt install certbot python3-certbot-nginx
   
   # Obtain SSL certificate
   sudo certbot --nginx -d pos.yourdomain.com
   ```

7. **Backup Configuration**
   ```bash
   # Create backup script
   cat > /opt/sgpos/scripts/backup_prod.sh << 'EOF'
   #!/bin/bash
   BACKUP_DIR="/backup/sgpos"
   DATE=$(
   
