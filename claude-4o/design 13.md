I need to create a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale system. This should be at least 6000 words and cover all the specified requirements. Let me structure this carefully:
Executive Summary
Product Overview
Technology Stack
System Architecture
Database Schema Design
Codebase File Hierarchy
Application Modules and User Interaction
Key Modules and Files Description
Development Environment Setup
Production Environment Setup
Implementation Guidelines
Security and Compliance
Performance Requirements
Testing Strategy
I'll ensure the document is detailed, professional, and leaves no ambiguity for implementation while adhering to the architectural principles mentioned. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Product Overview
Technology Stack
System Architecture
Database Schema Design
Codebase File Hierarchy
Application Modules and User Interaction
Key Modules and Files Description
Development Environment Setup
Production Environment Setup
Implementation Guidelines
Security and Compliance
Performance Requirements
Testing Strategy
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail needs of small to medium-sized businesses (SMBs) in Singapore. Built with modern technologies including Python, PySide6, and PostgreSQL, the system provides a professional-grade retail management solution that fully complies with Singapore's regulatory requirements, including GST regulations, IRAS compliance, and local business practices.

The application architecture emphasizes clean separation of concerns, robust asynchronous processing, strong data integrity, and scalability. By implementing industry best practices such as Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern, the system provides a solid foundation for both current operations and future enhancements.

Key features include comprehensive inventory management, multi-currency support, GST-compliant invoicing, customer relationship management, employee management with role-based access control, and detailed reporting capabilities. The system is designed to handle the complexity of real-world retail operations while maintaining high performance and reliability.

2. Product Overview
2.1 Product Vision
The SG POS System aims to be the premier retail management solution for Singapore SMBs, offering enterprise-level features at an accessible price point. The system empowers business owners to streamline their operations, maintain regulatory compliance, and make data-driven decisions through comprehensive analytics and reporting.

2.2 Target Market
Primary Users: Small to medium-sized retail businesses in Singapore
Business Types: General retail stores, specialty shops, mini-marts, fashion boutiques, electronics stores, and service-based businesses with retail components
User Profiles: Store owners, managers, cashiers, inventory staff, and accountants
2.3 Core Value Propositions
Singapore-Specific Compliance: Built-in GST calculation, IRAS-compliant reporting, and local business practice support
Comprehensive Feature Set: All-in-one solution covering sales, inventory, customers, employees, and accounting
Modern User Experience: Intuitive interface designed for efficiency and ease of use
Scalability: Architecture supports business growth from single-store to multi-location operations
Data Security: Enterprise-grade security measures protecting sensitive business data
Offline Capability: Core functions remain operational during internet outages
2.4 Key Features
Sales Management
Quick product search and barcode scanning
Multiple payment methods (cash, credit/debit cards, NETS, PayNow)
Split payment support
Hold and recall transactions
Returns and exchanges processing
Quotation generation
Layaway management
Inventory Management
Real-time stock tracking
Multi-location inventory support
Stock transfer between locations
Low stock alerts
Automatic reorder point management
Batch and serial number tracking
Product categorization and variants
Supplier management
Customer Management
Customer profile management
Purchase history tracking
Loyalty programs
Customer-specific pricing
Credit account management
Marketing campaign integration
Birthday and anniversary tracking
Employee Management
Role-based access control
Time clock functionality
Commission tracking
Performance metrics
Shift management
Cash drawer assignment
Financial Management
GST-compliant invoicing
Multi-currency support
Petty cash management
Daily cash reconciliation
Expense tracking
Profit margin analysis
Payment tracking
Reporting and Analytics
Sales reports (daily, weekly, monthly, yearly)
Inventory reports
Customer analytics
Employee performance reports
GST reports for IRAS submission
Financial statements
Custom report builder
3. Technology Stack
3.1 Core Technologies
Programming Language
Python 3.11+: Primary development language chosen for its robust ecosystem, cross-platform compatibility, and extensive library support
Type Hints: Full typing support using Python's typing module for improved code quality and IDE support
User Interface Framework
PySide6 (Qt 6.5+): Modern, cross-platform GUI framework providing native look and feel
Qt Designer: For rapid UI prototyping and complex form design
Custom Widget Library: Extended PySide6 widgets for specialized retail UI components
Database
PostgreSQL 15+: Enterprise-grade relational database for data persistence
SQLAlchemy 2.0+: Modern ORM for database abstraction and query building
Alembic: Database migration management
Redis: In-memory data store for caching and session management
Asynchronous Processing
asyncio: Python's native asynchronous framework
aiohttp: Asynchronous HTTP client/server
asyncpg: High-performance PostgreSQL driver for asyncio
3.2 Supporting Technologies
Development Tools
Poetry: Dependency management and packaging
Black: Code formatting
Ruff: Fast Python linter
mypy: Static type checking
pytest: Testing framework
pytest-asyncio: Asynchronous test support
pytest-qt: Qt/PySide6 testing support
DevOps and Deployment
Docker: Containerization for consistent deployment
GitHub Actions: CI/CD pipeline
Sentry: Error tracking and monitoring
Prometheus + Grafana: Application metrics and monitoring
Security
bcrypt: Password hashing
PyJWT: JSON Web Token implementation
cryptography: Encryption for sensitive data
SSL/TLS: Secure communication
External Integrations
Stripe API: Credit card processing
NETS API: Local payment gateway integration
Twilio: SMS notifications
SendGrid: Email notifications
Google Cloud Vision: Receipt OCR processing
3.3 Architecture Patterns
Layered Architecture: Clear separation between presentation, business logic, service, and data layers
Repository Pattern: Abstraction of data access logic
Dependency Injection: Loose coupling and testability
DTO Pattern: Clean data transfer between layers
Result Pattern: Explicit error handling without exceptions
Event-Driven Architecture: Decoupled component communication
CQRS: Separation of read and write operations for performance optimization
4. System Architecture
4.1 High-Level Architecture
The SG POS System follows a clean, layered architecture with clear separation of concerns:

┌─────────────────────────────────────────────────────────────┐
│                    Presentation Layer                        │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │   PySide6   │  │   Widgets    │  │   View Models   │   │
│  │     GUI     │  │  & Dialogs   │  │   & Adapters    │   │
│  └─────────────┘  └──────────────┘  └─────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                  Business Logic Layer                        │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │  Managers   │  │   Domain     │  │   Validators    │   │
│  │             │  │   Models     │  │   & Rules       │   │
│  └─────────────┘  └──────────────┘  └─────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Service Layer                             │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │  Services   │  │ Repositories │  │   External      │   │
│  │             │  │              │  │   Integrations  │   │
│  └─────────────┘  └──────────────┘  └─────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Data Layer                                │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │ PostgreSQL  │  │    Redis     │  │   File System   │   │
│  │  Database   │  │    Cache     │  │    Storage      │   │
│  └─────────────┘  └──────────────┘  └─────────────────┘   │
└─────────────────────────────────────────────────────────────┘
4.2 Component Architecture
ApplicationCore
The central dependency injection container that manages all application components:

class ApplicationCore:
    """Central application container managing all dependencies"""
    
    @property
    def database_service(self) -> DatabaseService
    @property
    def auth_manager(self) -> AuthManager
    @property
    def sales_manager(self) -> SalesManager
    @property
    def inventory_manager(self) -> InventoryManager
    @property
    def customer_manager(self) -> CustomerManager
    @property
    def employee_manager(self) -> EmployeeManager
    @property
    def accounting_manager(self) -> AccountingManager
    @property
    def gst_manager(self) -> GSTManager
    @property
    def report_manager(self) -> ReportManager

4.3 Asynchronous Architecture
The application implements a robust asynchronous processing model:

┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Main Thread   │────▶│ Event Scheduler  │────▶│  Worker Thread  │
│   (Qt GUI)      │     │                  │     │   (asyncio)     │
└─────────────────┘     └──────────────────┘     └─────────────────┘
         ▲                                                 │
         │                                                 │
         └─────────────────────────────────────────────────┘
                    Qt Signal/Slot Mechanism
4.4 Data Flow Architecture
User Action → UI Widget → View Model → Manager → Service → Repository → Database
     ↑                                                                        │
     └────────────────────── Result/DTO ─────────────────────────────────────┘
5. Database Schema Design
5.1 Schema Overview
The database schema is designed to support all POS operations while maintaining data integrity and performance:

-- Core Business Entities
CREATE SCHEMA IF NOT EXISTS pos;
SET search_path TO pos;

-- Companies (Multi-tenant support)
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_no VARCHAR(50) UNIQUE NOT NULL,
    gst_registration_no VARCHAR(50),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    currency_code CHAR(3) DEFAULT 'SGD',
    fiscal_year_start DATE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Stores/Locations
CREATE TABLE stores (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Users and Authentication
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    is_active BOOLEAN DEFAULT true,
    is_superuser BOOLEAN DEFAULT false,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Roles and Permissions
CREATE TABLE roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(50) NOT NULL,
    description TEXT,
    is_system BOOLEAN DEFAULT false,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, name)
);

CREATE TABLE permissions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    module VARCHAR(50) NOT NULL,
    action VARCHAR(50) NOT NULL,
    description TEXT,
    UNIQUE(module, action)
);

CREATE TABLE role_permissions (
    role_id UUID NOT NULL REFERENCES roles(id) ON DELETE CASCADE,
    permission_id UUID NOT NULL REFERENCES permissions(id) ON DELETE CASCADE,
    PRIMARY KEY (role_id, permission_id)
);

CREATE TABLE user_roles (
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    role_id UUID NOT NULL REFERENCES roles(id) ON DELETE CASCADE,
    store_id UUID REFERENCES stores(id),
    PRIMARY KEY (user_id, role_id, store_id)
);

-- Product Management
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    parent_id UUID REFERENCES categories(id),
    name VARCHAR(100) NOT NULL,
    description TEXT,
    display_order INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE brands (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(100) NOT NULL,
    description TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, name)
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    sku VARCHAR(50) NOT NULL,
    barcode VARCHAR(50),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id UUID REFERENCES categories(id),
    brand_id UUID REFERENCES brands(id),
    unit_of_measure VARCHAR(20),
    cost_price DECIMAL(15, 4),
    selling_price DECIMAL(15, 4),
    min_price DECIMAL(15, 4),
    tax_rate DECIMAL(5, 2) DEFAULT 0,
    is_taxable BOOLEAN DEFAULT true,
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    reorder_point INTEGER,
    reorder_quantity INTEGER,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, sku)
);

-- Product Variants
CREATE TABLE product_attributes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(50) NOT NULL,
    display_order INTEGER DEFAULT 0,
    UNIQUE(company_id, name)
);

CREATE TABLE product_attribute_values (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    attribute_id UUID NOT NULL REFERENCES product_attributes(id),
    value VARCHAR(100) NOT NULL,
    display_order INTEGER DEFAULT 0,
    UNIQUE(attribute_id, value)
);

CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID NOT NULL REFERENCES products(id),
    sku VARCHAR(50) NOT NULL,
    barcode VARCHAR(50),
    cost_price DECIMAL(15, 4),
    selling_price DECIMAL(15, 4),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, sku)
);

CREATE TABLE product_variant_attributes (
    variant_id UUID NOT NULL REFERENCES product_variants(id),
    attribute_value_id UUID NOT NULL REFERENCES product_attribute_values(id),
    PRIMARY KEY (variant_id, attribute_value_id)
);

-- Inventory Management
CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    store_id UUID NOT NULL REFERENCES stores(id),
    product_id UUID NOT NULL REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity DECIMAL(15, 4) NOT NULL DEFAULT 0,
    reserved_quantity DECIMAL(15, 4) NOT NULL DEFAULT 0,
    last_updated TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(store_id, product_id, variant_id)
);

CREATE TABLE inventory_movements (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    store_id UUID NOT NULL REFERENCES stores(id),
    product_id UUID NOT NULL REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    movement_type VARCHAR(50) NOT NULL, -- SALE, RETURN, ADJUSTMENT, TRANSFER_IN, TRANSFER_OUT, etc.
    quantity DECIMAL(15, 4) NOT NULL,
    reference_type VARCHAR(50),
    reference_id UUID,
    notes TEXT,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Customer Management
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(20),
    mobile VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(20),
    date_of_birth DATE,
    gender VARCHAR(10),
    nationality VARCHAR(50),
    id_type VARCHAR(20), -- NRIC, FIN, PASSPORT
    id_number VARCHAR(50),
    credit_limit DECIMAL(15, 2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0, -- days
    is_active BOOLEAN DEFAULT true,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

CREATE TABLE customer_groups (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(100) NOT NULL,
    discount_percentage DECIMAL(5, 2) DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    UNIQUE(company_id, name)
);

CREATE TABLE customer_group_members (
    customer_id UUID NOT NULL REFERENCES customers(id),
    group_id UUID NOT NULL REFERENCES customer_groups(id),
    PRIMARY KEY (customer_id, group_id)
);

-- Supplier Management
CREATE TABLE suppliers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    contact_person VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    payment_terms INTEGER DEFAULT 0,
    tax_registration_no VARCHAR(50),
    bank_account_no VARCHAR(50),
    bank_name VARCHAR(100),
    is_active BOOLEAN DEFAULT true,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

-- Sales Transactions
CREATE TABLE sales_orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    store_id UUID NOT NULL REFERENCES stores(id),
    order_no VARCHAR(50) NOT NULL,
    order_date TIMESTAMP WITH TIME ZONE NOT NULL,
    customer_id UUID REFERENCES customers(id),
    status VARCHAR(20) NOT NULL, -- DRAFT, CONFIRMED, PARTIAL, COMPLETED, CANCELLED
    subtotal DECIMAL(15, 2) NOT NULL,
    discount_amount DECIMAL(15, 2) DEFAULT 0,
    tax_amount DECIMAL(15, 2) DEFAULT 0,
    total_amount DECIMAL(15, 2) NOT NULL,
    paid_amount DECIMAL(15, 2) DEFAULT 0,
    notes TEXT,
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, order_no)
);

CREATE TABLE sales_order_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    order_id UUID NOT NULL REFERENCES sales_orders(id),
    product_id UUID NOT NULL REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity DECIMAL(15, 4) NOT NULL,
    unit_price DECIMAL(15, 4) NOT NULL,
    discount_percentage DECIMAL(5, 2) DEFAULT 0,
    discount_amount DECIMAL(15, 2) DEFAULT 0,
    tax_rate DECIMAL(5, 2) DEFAULT 0,
    tax_amount DECIMAL(15, 2) DEFAULT 0,
    total_amount DECIMAL(15, 2) NOT NULL,
    notes TEXT
);

-- Payments
CREATE TABLE payment_methods (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(50) NOT NULL,
    type VARCHAR(20) NOT NULL, -- CASH, CARD, NETS, PAYNOW, CHEQUE, etc.
    is_active BOOLEAN DEFAULT true,
    requires_reference BOOLEAN DEFAULT false,
    gl_account_id UUID,
    UNIQUE(company_id, name)
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    store_id UUID NOT NULL REFERENCES stores(id),
    payment_no VARCHAR(50) NOT NULL,
    payment_date TIMESTAMP WITH TIME ZONE NOT NULL,
    customer_id UUID REFERENCES customers(id),
    payment_method_id UUID NOT NULL REFERENCES payment_methods(id),
    amount DECIMAL(15, 2) NOT NULL,
    reference_no VARCHAR(100),
    notes TEXT,
    status VARCHAR(20) DEFAULT 'COMPLETED',
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, payment_no)
);

CREATE TABLE payment_allocations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    payment_id UUID NOT NULL REFERENCES payments(id),
    order_id UUID NOT NULL REFERENCES sales_orders(id),
    amount DECIMAL(15, 2) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- GST Configuration
CREATE TABLE gst_rates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(50) NOT NULL,
    rate DECIMAL(5, 2) NOT NULL,
    is_default BOOLEAN DEFAULT false,
    is_active BOOLEAN DEFAULT true,
    effective_from DATE NOT NULL,
    effective_to DATE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    account_code VARCHAR(20) NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(20) NOT NULL, -- ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE
    parent_id UUID REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, account_code)
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    entry_no VARCHAR(50) NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT,
    reference_type VARCHAR(50),
    reference_id UUID,
    status VARCHAR(20) DEFAULT 'POSTED',
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, entry_no)
);

CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entry_id UUID NOT NULL REFERENCES journal_entries(id),
    account_id UUID NOT NULL REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(15, 2) DEFAULT 0,
    credit_amount DECIMAL(15, 2) DEFAULT 0,
    description TEXT
);

-- Indexes for Performance
CREATE INDEX idx_inventory_store_product ON inventory(store_id, product_id);
CREATE INDEX idx_sales_orders_customer ON sales_orders(customer_id);
CREATE INDEX idx_sales_orders_date ON sales_orders(order_date);
CREATE INDEX idx_payments_date ON payments(payment_date);
CREATE INDEX idx_inventory_movements_date ON inventory_movements(created_at);

-- Triggers
CREATE OR REPLACE FUNCTION update_timestamp()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_companies_timestamp BEFORE UPDATE ON companies
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

CREATE TRIGGER update_stores_timestamp BEFORE UPDATE ON stores
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

CREATE TRIGGER update_users_timestamp BEFORE UPDATE ON users
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

CREATE TRIGGER update_products_timestamp BEFORE UPDATE ON products
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

CREATE TRIGGER update_customers_timestamp BEFORE UPDATE ON customers
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

CREATE TRIGGER update_sales_orders_timestamp BEFORE UPDATE ON sales_orders
    FOR EACH ROW EXECUTE FUNCTION update_timestamp();

6. Codebase File Hierarchy
6.1 Project Structure
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                      # Application entry point
│   ├── config.py                    # Configuration management
│   ├── constants.py                 # Application constants
│   ├── exceptions.py                # Custom exceptions
│   ├── types.py                     # Type definitions and aliases
│   │
│   ├── core/                        # Core application infrastructure
│   │   ├── __init__.py
│   │   ├── application.py           # ApplicationCore container
│   │   ├── database.py              # Database connection management
│   │   ├── result.py                # Result pattern implementation
│   │   ├── dto.py                   # Base DTO classes
│   │   ├── events.py                # Event system
│   │   └── logging.py               # Logging configuration
│   │
│   ├── models/                      # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                  # Base model class
│   │   ├── company.py               # Company and store models
│   │   ├── user.py                  # User and authentication models
│   │   ├── product.py               # Product and category models
│   │   ├── inventory.py             # Inventory models
│   │   ├── customer.py              # Customer models
│   │   ├── sales.py                 # Sales order models
│   │   ├── payment.py               # Payment models
│   │   └── accounting.py            # Accounting models
│   │
│   ├── dto/                         # Data Transfer Objects
│   │   ├── __init__.py
│   │   ├── auth.py                  # Authentication DTOs
│   │   ├── product.py               # Product DTOs
│   │   ├── sales.py                 # Sales DTOs
│   │   ├── customer.py              # Customer DTOs
│   │   ├── inventory.py             # Inventory DTOs
│   │   └── reports.py               # Reporting DTOs
│   │
│   ├── services/                    # Service layer (repositories)
│   │   ├── __init__.py
│   │   ├── base.py                  # Base service class
│   │   ├── auth_service.py          # Authentication service
│   │   ├── product_service.py       # Product service
│   │   ├── inventory_service.py     # Inventory service
│   │   ├── customer_service.py      # Customer service
│   │   ├── sales_service.py         # Sales service
│   │   ├── payment_service.py       # Payment service
│   │   └── report_service.py        # Reporting service
│   │
│   ├── business_logic/              # Business logic layer
│   │   ├── __init__.py
│   │   ├── managers/                # Manager classes
│   │   │   ├── __init__.py
│   │   │   ├── auth_manager.py      # Authentication manager
│   │   │   ├── sales_manager.py     # Sales manager
│   │   │   ├── inventory_manager.py # Inventory manager
│   │   │   ├── customer_manager.py  # Customer manager
│   │   │   ├── employee_manager.py  # Employee manager
│   │   │   ├── gst_manager.py       # GST manager
│   │   │   └── report_manager.py    # Report manager
│   │   │
│   │   ├── validators/              # Business validators
│   │   │   ├── __init__.py
│   │   │   ├── sales_validator.py
│   │   │   ├── product_validator.py
│   │   │   └── payment_validator.py
│   │   │
│   │   └── rules/                   # Business rules
│   │       ├── __init__.py
│   │       ├── pricing_rules.py
│   │       ├── discount_rules.py
│   │       └── gst_rules.py
│   │
│   ├── ui/                          # User interface layer
│   │   ├── __init__.py
│   │   ├── main_window.py           # Main application window
│   │   ├── styles.py                # Application styling
│   │   ├── themes.py                # Theme management
│   │   │
│   │   ├── widgets/                 # Reusable widgets
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py       # Base widget class
│   │   │   ├── search_widget.py     # Search widget
│   │   │   ├── table_widget.py      # Enhanced table widget
│   │   │   └── chart_widget.py      # Chart widget
│   │   │
│   │   ├── dialogs/                 # Dialog windows
│   │   │   ├── __init__.py
│   │   │   ├── base_dialog.py       # Base dialog class
│   │   │   ├── product_dialog.py    # Product dialog
│   │   │   ├── customer_dialog.py   # Customer dialog
│   │   │   └── payment_dialog.py    # Payment dialog
│   │   │
│   │   ├── views/                   # Main views
│   │   │   ├── __init__.py
│   │   │   ├── dashboard_view.py    # Dashboard
│   │   │   ├── sales_view.py        # Sales/POS view
│   │   │   ├── inventory_view.py    # Inventory management
│   │   │   ├── customers_view.py    # Customer management
│   │   │   ├── reports_view.py      # Reports
│   │   │   └── settings_view.py     # Settings
│   │   │
│   │   └── models/                  # Qt models
│   │       ├── __init__.py
│   │       ├── product_model.py     # Product table model
│   │       ├── customer_model.py    # Customer table model
│   │       └── sales_model.py       # Sales table model
│   │
│   ├── integrations/                # External integrations
│   │   ├── __init__.py
│   │   ├── payment_gateways/
│   │   │   ├── __init__.py
│   │   │   ├── stripe_gateway.py
│   │   │   └── nets_gateway.py
│   │   │
│   │   └── communications/
│   │       ├── __init__.py
│   │       ├── email_service.py
│   │       └── sms_service.py
│   │
│   └── utils/                       # Utility modules
│       ├── __init__.py
│       ├── async_utils.py           # Async utilities
│       ├── date_utils.py            # Date/time utilities
│       ├── currency_utils.py        # Currency utilities
│       ├── validation_utils.py      # Validation utilities
│       └── export_utils.py          # Export utilities
│
├── tests/                           # Test suite
│   ├── __init__.py
│   ├── conftest.py                  # Pytest configuration
│   ├── unit/                        # Unit tests
│   ├── integration/                 # Integration tests
│   └── e2e/                        # End-to-end tests
│
├── scripts/                         # Utility scripts
│   ├── init_db.py                   # Database initialization
│   ├── seed_data.py                 # Seed data
│   └── migrate_db.py                # Database migrations
│
├── resources/                       # Application resources
│   ├── images/                      # Icons and images
│   ├── translations/                # i18n files
│   └── templates/                   # Report templates
│
├── docs/                           # Documentation
│   ├── api/                        # API documentation
│   ├── user_manual/                # User manual
│   └── developer_guide/            # Developer guide
│
├── deploy/                         # Deployment configurations
│   ├── docker/                     # Docker files
│   ├── kubernetes/                 # Kubernetes manifests
│   └── scripts/                    # Deployment scripts
│
├── .github/                        # GitHub configuration
│   └── workflows/                  # CI/CD workflows
│
├── pyproject.toml                  # Poetry configuration
├── poetry.lock                     # Dependency lock file
├── .env.example                    # Environment variables example
├── .gitignore                      # Git ignore file
├── README.md                       # Project README
└── LICENSE                         # License file
7. Application Modules and User Interaction
7.1 Module Architecture Diagram
┌─────────────────────────────────────────────────────────────────────┐
│                           Main Application                           │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │                      Main Window Frame                        │  │
│  │  ┌─────────┐  ┌──────────────────────────────────────────┐  │  │
│  │  │  Menu   │  │              Content Area                 │  │  │
│  │  │  Bar    │  │  ┌────────────────────────────────────┐  │  │  │
│  │  └─────────┘  │  │        Active View/Module          │  │  │  │
│  │  ┌─────────┐  │  │                                    │  │  │  │
│  │  │  Tool   │  │  │  • Dashboard                       │  │  │  │
│  │  │  Bar    │  │  │  • Sales/POS                       │  │  │  │
│  │  └─────────┘  │  │  • Inventory                       │  │  │  │
│  │  ┌─────────┐  │  │  • Customers                       │  │  │  │
│  │  │  Side   │  │  │  • Reports                         │  │  │  │
│  │  │  Bar    │  │  │  • Settings                        │  │  │  │
│  │  │         │  │  │                                    │  │  │  │
│  │  │ • Sales │  │  └────────────────────────────────────┘  │  │  │
│  │  │ • Inv.  │  │                                          │  │  │
│  │  │ • Cust. │  └──────────────────────────────────────────┘  │  │
│  │  │ • Rpts. │  ┌──────────────────────────────────────────┐  │  │
│  │  │ • More  │  │            Status Bar                    │  │  │
│  │  └─────────┘  └──────────────────────────────────────────┘  │  │
│  └─────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
7.2 User Interaction Flow
7.2.1 Sales Module Flow
Customer Arrives → Cashier Login → Sales Screen
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              Scan Items          Manual Entry         Quick Keys
                    │                   │                   │
                    └───────────────────┴───────────────────┘
                                        │
                                        ▼
                                  Shopping Cart
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              Apply Discount      Customer Link       Item Modify
                                        │
                                        ▼
                                    Checkout
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              Cash Payment       Card Payment        Mixed Payment
                                        │
                                        ▼
                                 Print Receipt
                                        │
                                        ▼
                              Transaction Complete
7.2.2 Inventory Module Flow
Inventory Management
        │
        ├── Stock Inquiry
        │   ├── Search Products
        │   ├── View Stock Levels
        │   └── Check Movement History
        │
        ├── Stock Adjustment
        │   ├── Physical Count
        │   ├── Adjustment Entry
        │   └── Approval Process
        │
        ├── Stock Transfer
        │   ├── Create Transfer Order
        │   ├── Ship Items
        │   └── Receive Items
        │
        └── Purchase Management
            ├── Create Purchase Order
            ├── Receive Goods
            └── Update Stock Levels
7.3 Key Module Interactions
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Sales     │────▶│  Inventory  │────▶│ Accounting  │
│   Module    │     │   Module    │     │   Module    │
└─────────────┘     └─────────────┘     └─────────────┘
       │                    │                    │
       ▼                    ▼                    ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Customer   │     │   Product   │     │   Reports   │
│   Module    │     │   Module    │     │   Module    │
└─────────────┘     └─────────────┘     └─────────────┘
8. Key Modules and Files Description
8.1 Core Infrastructure
ApplicationCore (app/core/application.py)
Central dependency injection container managing all application components:

class ApplicationCore:
    """
    Central application container that manages dependencies and provides
    lazy initialization of all managers and services.
    
    Implements the Dependency Injection pattern to ensure loose coupling
    between components while maintaining a single source of truth for
    application state.
    """
    
    def __init__(self, config: Config):
        self._config = config
        self._database_service: Optional[DatabaseService] = None
        self._event_bus: Optional[EventBus] = None
        self._cache: Optional[CacheService] = None
        # ... other service declarations
    
    @property
    def database_service(self) -> DatabaseService:
        """Lazy initialization of database service"""
        if self._database_service is None:
            self._database_service = DatabaseService(self._config.database_url)
        return self._database_service
    
    @property
    def auth_manager(self) -> AuthManager:
        """Lazy initialization of authentication manager"""
        if self._auth_manager is None:
            self._auth_manager = AuthManager(self)
        return self._auth_manager
    
    # ... other manager properties

Result Pattern (app/core/result.py)
Implementation of the Result pattern for explicit error handling:

from typing import TypeVar, Generic, Union, Optional
from dataclasses import dataclass

T = TypeVar('T')
E = TypeVar('E')

@dataclass(frozen=True)
class Success(Generic[T]):
    """Represents a successful operation result"""
    value: T

@dataclass(frozen=True)
class Failure(Generic[E]):
    """Represents a failed operation result"""
    error: E

Result = Union[Success[T], Failure[E]]

class ResultMixin:
    """Mixin providing Result pattern utilities"""
    
    @staticmethod
    def success(value: T) -> Result[T, E]:
        return Success(value)
    
    @staticmethod
    def failure(error: E) -> Result[T, E]:
        return Failure(error)
    
    @staticmethod
    def is_success(result: Result[T, E]) -> bool:
        return isinstance(result, Success)
    
    @staticmethod
    def is_failure(result: Result[T, E]) -> bool:
        return isinstance(result, Failure)

8.2 Business Logic Layer
Sales Manager (app/business_logic/managers/sales_manager.py)
Orchestrates sales-related business operations:

class SalesManager:
    """
    Manages all sales-related business operations including order creation,
    payment processing, and transaction management.
    """
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
        
    @property
    def sales_service(self) -> SalesService:
        return self.app_core.sales_service
    
    @property
    def inventory_manager(self) -> InventoryManager:
        return self.app_core.inventory_manager
    
    @property
    def payment_manager(self) -> PaymentManager:
        return self.app_core.payment_manager
    
    async def create_sales_order(
        self,
        order_data: CreateSalesOrderDTO
    ) -> Result[SalesOrderDTO, SalesError]:
        """
        Creates a new sales order with inventory validation and
        reservation.
        """
        # Validate customer
        if order_data.customer_id:
            customer_result = await self._validate_customer(order_data.customer_id)
            if self.is_failure(customer_result):
                return customer_result
        
        # Validate and reserve inventory
        inventory_result = await self._validate_and_reserve_inventory(
            order_data.items
        )
        if self.is_failure(inventory_result):
            return inventory_result
        
        # Calculate pricing and taxes
        pricing_result = await self._calculate_order_totals(order_data)
        if self.is_failure(pricing_result):
            # Rollback inventory reservation
            await self._release_inventory_reservation(order_data.items)
            return pricing_result
        
        # Create order
        try:
            order = await self.sales_service.create_order(
                order_data,
                pricing_result.value
            )
            
            # Emit event
            await self.app_core.event_bus.emit(
                SalesOrderCreatedEvent(order_id=order.id)
            )
            
            return self.success(order)
            
        except Exception as e:
            # Rollback inventory reservation
            await self._release_inventory_reservation(order_data.items)
            return self.failure(SalesError.ORDER_CREATION_FAILED)

Inventory Manager (app/business_logic/managers/inventory_manager.py)
Manages inventory operations with real-time tracking:

class InventoryManager:
    """
    Manages inventory operations including stock tracking, movements,
    and multi-location inventory management.
    """
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
    
    async def check_availability(
        self,
        store_id: UUID,
        items: List[OrderItemDTO]
    ) -> Result[Dict[UUID, InventoryStatus], InventoryError]:
        """
        Checks product availability for given items at a specific store.
        """
        availability = {}
        
        for item in items:
            stock_result = await self.app_core.inventory_service.get_stock_level(
                store_id=store_id,
                product_id=item.product_id,
                variant_id=item.variant_id
            )
            
            if self.is_failure(stock_result):
                return self.failure(InventoryError.STOCK_CHECK_FAILED)
            
            stock = stock_result.value
            available_qty = stock.quantity - stock.reserved_quantity
            
            availability[item.product_id] = InventoryStatus(
                product_id=item.product_id,
                available_quantity=available_qty,
                is_available=available_qty >= item.quantity
            )
        
        return self.success(availability)
    
    async def reserve_stock(
        self,
        store_id: UUID,
        items: List[OrderItemDTO],
        reference_id: UUID
    ) -> Result[None, InventoryError]:
        """
        Reserves stock for an order, ensuring atomicity.
        """
        async with self.app_core.database_service.transaction():
            for item in items:
                result = await self.app_core.inventory_service.reserve_stock(
                    store_id=store_id,
                    product_id=item.product_id,
                    quantity=item.quantity,
                    reference_id=reference_id
                )
                
                if self.is_failure(result):
                    raise RollbackTransaction()
            
            return self.success(None)

8.3 Service Layer
Product Service (app/services/product_service.py)
Repository pattern implementation for product data access:

class ProductService:
    """
    Service layer for product-related data operations.
    Implements the Repository pattern for clean data access.
    """
    
    def __init__(self, db_session: AsyncSession):
        self.db_session = db_session
    
    async def get_product_by_sku(
        self,
        company_id: UUID,
        sku: str
    ) -> Result[ProductDTO, ProductError]:
        """Retrieves a product by SKU"""
        try:
            query = select(Product).where(
                and_(
                    Product.company_id == company_id,
                    Product.sku == sku,
                    Product.is_active == True
                )
            )
            
            result = await self.db_session.execute(query)
            product = result.scalar_one_or_none()
            
            if not product:
                return Failure(ProductError.NOT_FOUND)
            
            return Success(ProductDTO.from_orm(product))
            
        except Exception as e:
            logger.error(f"Error retrieving product: {e}")
            return Failure(ProductError.DATABASE_ERROR)
    
    async def search_products(
        self,
        company_id: UUID,
        search_term: str,
        limit: int = 50
    ) -> Result[List[ProductDTO], ProductError]:
        """Searches products by name, SKU, or barcode"""
        try:
            query = select(Product).where(
                and_(
                    Product.company_id == company_id,
                    Product.is_active == True,
                    or_(
                        Product.name.ilike(f"%{search_term}%"),
                        Product.sku.ilike(f"%{search_term}%"),
                        Product.barcode == search_term
                    )
                )
            ).limit(limit)
            
            result = await self.db_session.execute(query)
            products = result.scalars().all()
            
            return Success([ProductDTO.from_orm(p) for p in products])
            
        except Exception as e:
            logger.error(f"Error searching products: {e}")
            return Failure(ProductError.SEARCH_FAILED)

8.4 UI Layer
Main Window (app/ui/main_window.py)
Primary application window managing navigation and view switching:

class MainWindow(QMainWindow):
    """
    Main application window providing navigation and view management.
    """
    
    def __init__(self, app_core: ApplicationCore):
        super().__init__()
        self.app_core = app_core
        self.current_user = None
        self.init_ui()
        
    def init_ui(self):
        """Initializes the user interface"""
        self.setWindowTitle("SG POS System")
        self.setMinimumSize(1200, 800)
        
        # Create central widget and layout
        central_widget = QWidget()
        self.setCentralWidget(central_widget)
        
        main_layout = QHBoxLayout(central_widget)
        main_layout.setContentsMargins(0, 0, 0, 0)
        main_layout.setSpacing(0)
        
        # Create sidebar
        self.sidebar = NavigationSidebar(self.app_core)
        self.sidebar.navigation_requested.connect(self.switch_view)
        main_layout.addWidget(self.sidebar)
        
        # Create content area
        self.content_stack = QStackedWidget()
        main_layout.addWidget(self.content_stack, 1)
        
        # Initialize views
        self._init_views()
        
        # Create menu bar
        self._create_menu_bar()
        
