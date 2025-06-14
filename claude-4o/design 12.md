This is a comprehensive request for a Product Requirements Document for a sophisticated Point-of-Sale system. I need to create a detailed PRD that covers:
The business context and requirements for Singapore SMBs
Technical architecture based on the provided architectural considerations
Database schema design with proper normalization
Complete codebase structure and file hierarchy
Application modules and user interaction flows
Technology stack details
Development and production environment setup
All regulatory and compliance considerations for Singapore
The user has provided excellent architectural guidance showing this should be an enterprise-grade application with:

Layered architecture with proper separation of concerns
Dependency injection via ApplicationCore
Asynchronous processing model
Repository pattern for data access
Multi-currency and GST compliance
I'll need to create a very detailed document that provides clear specifications for building this system from the ground up, ensuring no ambiguity in implementation. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Executive Summary
The SG Point-of-Sale (POS) system is a comprehensive, cross-platform desktop application specifically designed to meet the retail operational needs of small to medium-sized businesses (SMBs) in Singapore. This professional-grade solution combines modern Python development with PySide6's sophisticated user interface capabilities and PostgreSQL's enterprise-level data management to deliver a robust, scalable retail management platform.

The application addresses the unique regulatory requirements of Singapore's business environment, including GST compliance, multi-currency support for the region's diverse customer base, and integration with local financial reporting standards. Built on a foundation of clean, layered architecture with asynchronous processing capabilities, the system provides real-time performance while maintaining data integrity and regulatory compliance.

Key differentiators include advanced inventory management, comprehensive financial reporting, multi-location support, and seamless integration with Singapore's business ecosystem. The system is architected to scale from single-location retailers to multi-store operations, providing a growth path that accommodates evolving business needs.

Product Overview
Vision Statement
To provide Singapore SMBs with a world-class point-of-sale solution that simplifies retail operations while ensuring regulatory compliance and enabling business growth through data-driven insights.

Product Goals
Operational Efficiency: Streamline daily retail operations through intuitive workflows and automated processes
Regulatory Compliance: Ensure full compliance with Singapore's GST regulations and financial reporting requirements
Scalability: Support business growth from single-location to multi-store operations
Data-Driven Decision Making: Provide comprehensive analytics and reporting capabilities
Integration Ready: Facilitate integration with third-party systems and future technological advances
Core Value Propositions
Singapore-Specific Compliance: Built-in GST handling, local tax requirements, and regulatory reporting
Multi-Currency Support: Native support for SGD, USD, and other regional currencies
Professional Architecture: Enterprise-grade codebase with clean separation of concerns
Real-Time Processing: Asynchronous architecture ensuring responsive user experience
Comprehensive Reporting: Advanced analytics and financial reporting capabilities
Future-Proof Design: Modular architecture supporting feature extensions and integrations
Market Requirements & Target Users
Primary Target Market
Small to Medium-Sized Businesses (SMBs) in Singapore with the following characteristics:

Annual revenue: S
100
K
−
S
100K−S10M
Employee count: 2-50 staff members
Physical retail presence with potential for multiple locations
Need for professional-grade POS system with growth capabilities
Target User Personas
Store Manager/Owner
Primary Responsibilities: Overall store operations, financial oversight, staff management
Key Needs: Comprehensive reporting, inventory oversight, financial control, staff performance tracking
Technical Proficiency: Moderate; requires intuitive interface with powerful features
Cashier/Sales Associate
Primary Responsibilities: Transaction processing, customer service, basic inventory updates
Key Needs: Fast, reliable transaction processing, simple interface, minimal training requirements
Technical Proficiency: Basic; requires streamlined, error-resistant workflows
Inventory Manager
Primary Responsibilities: Stock management, purchasing, supplier relations
Key Needs: Real-time inventory tracking, automated reorder alerts, comprehensive stock reports
Technical Proficiency: Moderate; requires detailed inventory control features
Accountant/Financial Controller
Primary Responsibilities: Financial reporting, GST compliance, audit preparation
Key Needs: Automated GST calculations, comprehensive financial reports, audit trails
Technical Proficiency: High; requires detailed financial data access and export capabilities
Market Requirements
Functional Requirements
Transaction Processing: Fast, reliable POS transaction handling with multiple payment methods
Inventory Management: Real-time stock tracking with automated reorder capabilities
Customer Management: Comprehensive customer database with loyalty program support
Financial Reporting: GST-compliant reporting with comprehensive financial analytics
Multi-Location Support: Centralized management across multiple store locations
Staff Management: User role management with performance tracking capabilities
Regulatory Requirements
GST Compliance: Automated GST calculation and reporting per IRAS requirements
Financial Record Keeping: Compliance with Singapore Companies Act record-keeping requirements
Data Privacy: Adherence to Personal Data Protection Act (PDPA) requirements
Audit Trail: Comprehensive transaction logging for regulatory compliance
Performance Requirements
Response Time: Sub-second response for common operations
Reliability: 99.9% uptime during business hours
Scalability: Support for 100+ concurrent transactions per hour
Data Integrity: Zero data corruption with comprehensive backup strategies
Functional Requirements
Core POS Functions
Transaction Management
Sale Processing: Complete sale transactions with multiple item support
Payment Processing: Cash, card, digital wallet, and split payment support
Receipt Generation: Professional receipt printing with customizable formats
Transaction Modification: Void, refund, and exchange processing with proper authorization
Tax Calculation: Automatic GST calculation with support for different tax rates
Discount Management: Item-level and transaction-level discount application
Inventory Management
Product Catalog: Comprehensive product database with categories, variants, and pricing
Stock Tracking: Real-time inventory levels with automatic deduction on sales
Purchase Orders: Supplier management and purchase order generation
Stock Adjustments: Manual stock level adjustments with audit trails
Low Stock Alerts: Automated notifications for reorder requirements
Barcode Support: Barcode scanning and generation capabilities
Customer Management
Customer Database: Comprehensive customer information management
Loyalty Programs: Points-based loyalty system with reward redemption
Customer History: Complete purchase history and preferences tracking
Marketing Integration: Customer segmentation for targeted marketing campaigns
Reporting & Analytics
Sales Reports: Daily, weekly, monthly, and custom period sales analysis
Inventory Reports: Stock levels, movement analysis, and valuation reports
Financial Reports: Profit/loss statements, GST reports, and cash flow analysis
Staff Performance: Individual staff performance tracking and commission calculations
Customer Analytics: Customer behavior analysis and retention metrics
Advanced Features
Multi-Location Support
Centralized Management: Single dashboard for multiple store locations
Inventory Synchronization: Real-time inventory sharing between locations
Consolidated Reporting: Cross-location reporting and analytics
Location-Specific Configuration: Customizable settings per location
Financial Management
Chart of Accounts: Comprehensive accounting structure with Singapore standards
Journal Entries: Automated journal entry generation for transactions
Bank Reconciliation: Tools for reconciling bank statements
Tax Management: GST filing preparation and submission support
Integration Capabilities
E-commerce Integration: Synchronization with online store platforms
Accounting Software: Integration with popular accounting systems
Payment Gateway: Integration with local and international payment processors
Third-Party Services: API support for additional service integrations
Technical Architecture
Architectural Principles
Layered Architecture
The system implements a strict four-layer architecture ensuring clean separation of concerns:

Presentation Layer (app/ui/): PySide6-based user interface components
Business Logic Layer (app/business_logic/, app/accounting/): Core business operations and workflows
Data Access Layer (app/services/): Repository pattern implementation for data operations
Persistence Layer (app/models/): SQLAlchemy ORM models and database schema
Dependency Injection Pattern
The ApplicationCore class serves as the central dependency injection container, implementing lazy initialization for all system components. This approach ensures:

Loose coupling between system components
Improved testability through dependency inversion
Clean initialization and lifecycle management
Simplified configuration management
Asynchronous Processing Model
The application utilizes a dual-thread architecture:

Main Thread: Handles UI operations and user interactions
Background Thread: Manages I/O operations, database queries, and long-running tasks
Thread Safety: Proper synchronization mechanisms ensure thread-safe operations
Repository Pattern
Data access is standardized through the Repository pattern, providing:

Abstraction of data persistence concerns
Consistent query interfaces across all data entities
Simplified testing through repository mocking
Database-agnostic business logic implementation
Core Architectural Components
ApplicationCore
The central dependency injection container managing all system services and managers. Key responsibilities:

Service lifecycle management through lazy initialization
Configuration management and environment settings
Cross-cutting concern coordination (logging, error handling)
System startup and shutdown orchestration
Manager Classes
Business logic orchestrators implementing complex workflows:

TransactionManager: Handles complete sale transactions
InventoryManager: Manages stock operations and tracking
CustomerManager: Coordinates customer-related operations
PaymentManager: Processes payments and financial transactions
ReportManager: Generates reports and analytics
GST Manager: Handles Singapore-specific tax calculations
Service Classes
Data access layer implementing repository patterns:

ProductService: Product and inventory data operations
CustomerService: Customer data management
TransactionService: Sale transaction persistence
FinancialService: Financial data and reporting queries
AuditService: Audit trail and compliance logging
Database Schema Design
Schema Overview
The database schema is designed with normalization best practices while maintaining performance for retail operations. Key design principles include:

Third Normal Form (3NF) compliance for data integrity
Referential integrity through foreign key constraints
Audit trails for all critical business data
Performance optimization through strategic indexing
Singapore regulatory compliance through specialized fields
Core Entity Relationships
-- Core Business Entities
CREATE TABLE companies (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE,
    gst_registration_number VARCHAR(20),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Product Management
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    parent_id INTEGER REFERENCES categories(id),
    is_active BOOLEAN DEFAULT TRUE
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(100) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    base_price DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2),
    gst_rate DECIMAL(5,4) DEFAULT 0.07,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE product_variants (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    variant_name VARCHAR(255),
    sku VARCHAR(100) UNIQUE,
    price_adjustment DECIMAL(10,2) DEFAULT 0.00,
    cost_adjustment DECIMAL(10,2) DEFAULT 0.00
);

-- Inventory Management
CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    location_id INTEGER REFERENCES locations(id),
    quantity_on_hand INTEGER NOT NULL DEFAULT 0,
    reserved_quantity INTEGER NOT NULL DEFAULT 0,
    reorder_level INTEGER DEFAULT 0,
    max_stock_level INTEGER,
    last_counted_at TIMESTAMP,
    UNIQUE(product_id, location_id)
);

-- Customer Management
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(50) UNIQUE,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    company_name VARCHAR(255),
    email VARCHAR(100),
    phone VARCHAR(20),
    address TEXT,
    loyalty_points INTEGER DEFAULT 0,
    total_spent DECIMAL(12,2) DEFAULT 0.00,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Transaction Management
CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    location_id INTEGER REFERENCES locations(id),
    customer_id INTEGER REFERENCES customers(id),
    cashier_id INTEGER REFERENCES users(id),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    subtotal DECIMAL(12,2) NOT NULL,
    gst_amount DECIMAL(12,2) NOT NULL,
    discount_amount DECIMAL(12,2) DEFAULT 0.00,
    total_amount DECIMAL(12,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'completed',
    notes TEXT
);

CREATE TABLE transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id),
    product_id INTEGER REFERENCES products(id),
    product_variant_id INTEGER REFERENCES product_variants(id),
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(12,2) NOT NULL,
    gst_rate DECIMAL(5,4) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL
);

-- Payment Management
CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id),
    payment_method VARCHAR(50) NOT NULL,
    amount DECIMAL(12,2) NOT NULL,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1.000000,
    reference_number VARCHAR(100),
    processed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Financial Management
CREATE TABLE chart_of_accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL,
    parent_account_id INTEGER REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT TRUE
);

CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    transaction_id INTEGER REFERENCES transactions(id),
    entry_date DATE NOT NULL,
    description TEXT NOT NULL,
    total_debit DECIMAL(12,2) NOT NULL,
    total_credit DECIMAL(12,2) NOT NULL,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entry_lines (
    id SERIAL PRIMARY KEY,
    journal_entry_id INTEGER REFERENCES journal_entries(id),
    account_id INTEGER REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(12,2) DEFAULT 0.00,
    credit_amount DECIMAL(12,2) DEFAULT 0.00,
    description TEXT
);

-- User and Security Management
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    role VARCHAR(50) NOT NULL,
    location_id INTEGER REFERENCES locations(id),
    is_active BOOLEAN DEFAULT TRUE,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Audit and Compliance
CREATE TABLE audit_logs (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    table_name VARCHAR(100) NOT NULL,
    record_id INTEGER NOT NULL,
    action VARCHAR(20) NOT NULL,
    old_values JSONB,
    new_values JSONB,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ip_address INET
);

Database Indexes and Constraints
-- Performance Indexes
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_category ON products(category_id);
CREATE INDEX idx_inventory_product_location ON inventory(product_id, location_id);
CREATE INDEX idx_transactions_date ON transactions(transaction_date);
CREATE INDEX idx_transactions_location ON transactions(location_id);
CREATE INDEX idx_customers_email ON customers(email);
CREATE INDEX idx_customers_phone ON customers(phone);
CREATE INDEX idx_audit_logs_table_record ON audit_logs(table_name, record_id);

-- GST and Financial Indexes
CREATE INDEX idx_transactions_gst_date ON transactions(transaction_date) WHERE gst_amount > 0;
CREATE INDEX idx_journal_entries_date ON journal_entries(entry_date);

-- Data Integrity Constraints
ALTER TABLE products ADD CONSTRAINT chk_positive_prices 
    CHECK (base_price >= 0 AND cost_price >= 0);
ALTER TABLE inventory ADD CONSTRAINT chk_positive_quantities 
    CHECK (quantity_on_hand >= 0 AND reserved_quantity >= 0);
ALTER TABLE transactions ADD CONSTRAINT chk_positive_amounts 
    CHECK (subtotal >= 0 AND total_amount >= 0 AND gst_amount >= 0);

Database Triggers for Audit Trail
-- Automatic audit logging trigger
CREATE OR REPLACE FUNCTION audit_trigger_function()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        INSERT INTO audit_logs (table_name, record_id, action, new_values)
        VALUES (TG_TABLE_NAME, NEW.id, 'INSERT', row_to_json(NEW));
        RETURN NEW;
    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO audit_logs (table_name, record_id, action, old_values, new_values)
        VALUES (TG_TABLE_NAME, NEW.id, 'UPDATE', row_to_json(OLD), row_to_json(NEW));
        RETURN NEW;
    ELSIF TG_OP = 'DELETE' THEN
        INSERT INTO audit_logs (table_name, record_id, action, old_values)
        VALUES (TG_TABLE_NAME, OLD.id, 'DELETE', row_to_json(OLD));
        RETURN OLD;
    END IF;
    RETURN NULL;
END;
$$ LANGUAGE plpgsql;

-- Apply audit triggers to critical tables
CREATE TRIGGER audit_products AFTER INSERT OR UPDATE OR DELETE ON products
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();
CREATE TRIGGER audit_transactions AFTER INSERT OR UPDATE OR DELETE ON transactions
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();
CREATE TRIGGER audit_customers AFTER INSERT OR UPDATE OR DELETE ON customers
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();

Codebase Structure & File Hierarchy
Project Root Structure
sg_pos_system/
├── README.md
├── requirements.txt
├── requirements-dev.txt
├── setup.py
├── .env.example
├── .gitignore
├── pytest.ini
├── pyproject.toml
├── docker-compose.yml
├── Dockerfile
│
├── app/
│   ├── __init__.py
│   ├── main.py                    # Application entry point
│   ├── config.py                  # Configuration management
│   ├── application_core.py        # Dependency injection container
│   │
│   ├── models/                    # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py               # Base model with common fields
│   │   ├── company.py            # Company and location models
│   │   ├── product.py            # Product and inventory models
│   │   ├── customer.py           # Customer management models
│   │   ├── transaction.py        # Transaction and payment models
│   │   ├── accounting.py         # Financial and accounting models
│   │   ├── user.py              # User and authentication models
│   │   └── audit.py             # Audit trail models
│   │
│   ├── services/                  # Data access layer (Repository pattern)
│   │   ├── __init__.py
│   │   ├── base_service.py       # Base repository implementation
│   │   ├── product_service.py    # Product data operations
│   │   ├── customer_service.py   # Customer data operations
│   │   ├── transaction_service.py # Transaction data operations
│   │   ├── inventory_service.py  # Inventory management operations
│   │   ├── financial_service.py  # Financial data operations
│   │   ├── user_service.py       # User management operations
│   │   └── audit_service.py      # Audit logging operations
│   │
│   ├── business_logic/           # Business logic managers
│   │   ├── __init__.py
│   │   ├── transaction_manager.py # Sale transaction workflows
│   │   ├── inventory_manager.py   # Inventory management workflows
│   │   ├── customer_manager.py    # Customer relationship workflows
│   │   ├── payment_manager.py     # Payment processing workflows
│   │   ├── report_manager.py      # Reporting and analytics workflows
│   │   ├── user_manager.py        # User and role management
│   │   └── location_manager.py    # Multi-location management
│   │
│   ├── accounting/               # Singapore-specific accounting logic
│   │   ├── __init__.py
│   │   ├── gst_manager.py        # GST calculation and reporting
│   │   ├── chart_of_accounts.py  # Chart of accounts management
│   │   ├── journal_manager.py    # Journal entry automation
│   │   ├── financial_reports.py  # Financial reporting generation
│   │   └── compliance.py         # Regulatory compliance utilities
│   │
│   ├── ui/                       # PySide6 user interface layer
│   │   ├── __init__.py
│   │   ├── main_window.py        # Main application window
│   │   ├── styles/               # UI styling and themes
│   │   │   ├── __init__.py
│   │   │   ├── main_style.qss    # Main stylesheet
│   │   │   └── themes.py         # Theme management
│   │   │
│   │   ├── widgets/              # Reusable UI components
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py    # Base widget class
│   │   │   ├── product_selector.py
│   │   │   ├── payment_widget.py
│   │   │   ├── customer_selector.py
│   │   │   ├── inventory_widget.py
│   │   │   └── report_widget.py
│   │   │
│   │   ├── dialogs/              # Modal dialogs
│   │   │   ├── __init__.py
│   │   │   ├── product_dialog.py
│   │   │   ├── customer_dialog.py
│   │   │   ├── payment_dialog.py
│   │   │   ├── settings_dialog.py
│   │   │   └── about_dialog.py
│   │   │
│   │   ├── views/                # Main application views
│   │   │   ├── __init__.py
│   │   │   ├── pos_view.py       # Point of sale interface
│   │   │   ├── inventory_view.py # Inventory management
│   │   │   ├── customer_view.py  # Customer management
│   │   │   ├── reports_view.py   # Reports and analytics
│   │   │   ├── settings_view.py  # Application settings
│   │   │   └── admin_view.py     # Administrative functions
│   │   │
│   │   └── models/               # Qt model classes for views
│   │       ├── __init__.py
│   │       ├── product_model.py
│   │       ├── customer_model.py
│   │       ├── transaction_model.py
│   │       └── inventory_model.py
│   │
│   ├── utils/                    # Utility functions and helpers
│   │   ├── __init__.py
│   │   ├── validators.py         # Data validation utilities
│   │   ├── formatters.py         # Data formatting utilities
│   │   ├── exceptions.py         # Custom exception classes
│   │   ├── constants.py          # Application constants
│   │   ├── logging_config.py     # Logging configuration
│   │   ├── currency.py           # Multi-currency utilities
│   │   ├── barcode.py           # Barcode generation/scanning
│   │   └── pdf_generator.py      # PDF report generation
│   │
│   └── migrations/               # Database migration scripts
│       ├── __init__.py
│       ├── migration_manager.py  # Migration execution logic
│       └── versions/             # Individual migration files
│           ├── 001_initial_schema.py
│           ├── 002_add_gst_fields.py
│           ├── 003_add_audit_triggers.py
│           └── 004_add_multi_currency.py
│
├── scripts/                      # Database and deployment scripts
│   ├── setup_database.py        # Database initialization
│   ├── seed_data.py             # Sample data insertion
│   ├── backup_database.py       # Backup utilities
│   ├── restore_database.py      # Restore utilities
│   └── deploy.py               # Deployment automation
│
├── tests/                       # Comprehensive test suite
│   ├── __init__.py
│   ├── conftest.py             # Pytest configuration
│   ├── test_config.py          # Test configuration
│   │
│   ├── unit/                   # Unit tests
│   │   ├── __init__.py
│   │   ├── test_models.py
│   │   ├── test_services.py
│   │   ├── test_managers.py
│   │   └── test_utils.py
│   │
│   ├── integration/            # Integration tests
│   │   ├── __init__.py
│   │   ├── test_database.py
│   │   ├── test_transactions.py
│   │   ├── test_accounting.py
│   │   └── test_reporting.py
│   │
│   └── ui/                     # UI tests
│       ├── __init__.py
│       ├── test_pos_interface.py
│       ├── test_inventory_ui.py
│       └── test_reports_ui.py
│
├── docs/                       # Documentation
│   ├── README.md
│   ├── architecture.md
│   ├── api_reference.md
│   ├── user_guide.md
│   ├── admin_guide.md
│   └── deployment_guide.md
│
├── config/                     # Configuration files
│   ├── development.env
│   ├── production.env
│   ├── logging.yaml
│   └── database.yaml
│
└── assets/                     # Static assets
    ├── icons/                  # Application icons
    ├── images/                 # UI images
    ├── templates/              # Report templates
    └── fonts/                  # Custom fonts
Key File Descriptions
Core Application Files
app/main.py - Application Entry Point

"""
Main application entry point. Initializes the Qt application,
sets up the async event loop in a separate thread, and launches
the main window. Handles graceful shutdown and error recovery.
"""

app/application_core.py - Dependency Injection Container

"""
Central dependency injection container implementing lazy initialization
for all system managers and services. Provides unified access to
all application components while maintaining loose coupling.
"""

app/config.py - Configuration Management

"""
Centralized configuration management supporting multiple environments
(development, testing, production). Handles database connections,
logging levels, feature flags, and Singapore-specific settings.
"""

Data Layer Files
app/models/base.py - Base Model

"""
Base SQLAlchemy model providing common fields (id, created_at, updated_at)
and utility methods. All other models inherit from this base class
ensuring consistency across the data model.
"""

app/services/base_service.py - Base Repository

"""
Base repository implementation providing common CRUD operations,
query builders, and transaction management. All service classes
inherit from this base to ensure consistent data access patterns.
"""

Business Logic Files
app/business_logic/transaction_manager.py - Transaction Workflows

"""
Orchestrates complete sale transactions including inventory updates,
payment processing, GST calculations, and journal entry generation.
Implements complex business rules for refunds, exchanges, and voids.
"""

app/accounting/gst_manager.py - GST Compliance

"""
Singapore-specific GST calculation and reporting functionality.
Handles different GST rates, exemptions, and generates IRAS-compliant
reports. Integrates with the journal entry system for proper accounting.
"""

User Interface Files
app/ui/main_window.py - Main Application Window

"""
Primary application window implementing the MDI (Multiple Document Interface)
pattern. Manages view switching, menu system, toolbar, and status bar.
Coordinates between different functional areas of the application.
"""

app/ui/views/pos_view.py - Point of Sale Interface

"""
Core POS interface for processing sales transactions. Implements
product selection, quantity adjustment, discount application,
payment processing, and receipt generation. Optimized for speed
and ease of use during high-volume periods.
"""

Application Modules & User Interaction Flow
Module Architecture Diagram
┌─────────────────────────────────────────────────────────────────┐
│                     Presentation Layer (PySide6)                │
├─────────────────────────────────────────────────────────────────┤
│  Main Window  │  POS View  │  Inventory  │  Reports  │  Settings │
│               │            │   View      │   View    │   View    │
└─────────────────┬───────────────────────────────────────────────┘
                  │
┌─────────────────┴───────────────────────────────────────────────┐
│                    Business Logic Layer                         │
├─────────────────────────────────────────────────────────────────┤
│ Transaction │ Inventory │ Customer │ Payment │ Report │   GST   │
│  Manager    │  Manager  │ Manager  │ Manager │Manager │ Manager │
└─────────────────┬───────────────────────────────────────────────┘
                  │
┌─────────────────┴───────────────────────────────────────────────┐
│                    Data Access Layer                            │
├─────────────────────────────────────────────────────────────────┤
│ Product │Customer│Transaction│Inventory│Financial│User │ Audit  │
│Service  │Service │ Service   │ Service │ Service │Serv.│Service │
└─────────────────┬───────────────────────────────────────────────┘
                  │
┌─────────────────┴───────────────────────────────────────────────┐
│                    Persistence Layer                            │
├─────────────────────────────────────────────────────────────────┤
│           PostgreSQL Database with SQLAlchemy ORM              │
│     Products │ Customers │ Transactions │ Inventory │ Audit     │
└─────────────────────────────────────────────────────────────────┘
User Interaction Flow Diagrams
Primary Sales Transaction Flow
Customer Enters Store
         │
         ▼
[Cashier Logs In] ──→ Authentication Check ──→ [Main POS Interface]
         │                                              │
         ▼                                              ▼
[Scan/Select Products] ──→ Inventory Check ──→ [Add to Transaction]
         │                                              │
         ▼                                              ▼
[Apply Discounts] ──→ [Calculate GST] ──→ [Display Total]
         │                                              │
         ▼                                              ▼
[Process Payment] ──→ Payment Validation ──→ [Generate Receipt]
         │                                              │
         ▼                                              ▼
[Update Inventory] ──→ [Create Journal Entry] ──→ [Complete Transaction]
Inventory Management Flow
[Inventory Manager Login] ──→ [Inventory Dashboard]
         │                           │
         ▼                           ▼
[Stock Level Review] ──→ [Low Stock Alerts] ──→ [Generate Purchase Orders]
         │                           │                      │
         ▼                           ▼                      ▼
[Receive Goods] ──→ [Update Inventory] ──→ [Cost Price Updates]
         │                           │                      │
         ▼                           ▼                      ▼
[Stock Adjustments] ──→ [Audit Trail] ──→ [Inventory Reports]
Financial Reporting Flow
[Manager/Owner Login] ──→ [Reports Dashboard]
         │                       │
         ▼                       ▼
[Select Report Type] ──→ [Set Date Range] ──→ [Generate Report]
         │                       │                    │
         ▼                       ▼                    ▼
[Sales Analysis] ──→ [Export Options] ──→ [PDF/Excel Generation]
         │                       │                    │
         ▼                       ▼                    ▼
[GST Reports] ──→ [IRAS Filing] ──→ [Compliance Verification]
Key Application Modules
1. Point of Sale Module (app/ui/views/pos_view.py)
Purpose: Core transaction processing interface Key Features:

Product barcode scanning and manual selection
Real-time inventory availability checking
Multi-item transaction building
Discount and promotion application
GST calculation with Singapore compliance
Multiple payment method support
Receipt generation and printing
Transaction void and refund capabilities
User Interactions:

Scan product barcodes or search product catalog
Adjust quantities and apply item-level discounts
Select customer for loyalty point application
Process cash, card, or digital payments
Print or email receipts to customers
2. Inventory Management Module (app/ui/views/inventory_view.py)
Purpose: Comprehensive stock and product management Key Features:

Real-time inventory tracking across locations
Product catalog management with variants
Purchase order generation and receiving
Stock adjustment with audit trails
Automated reorder point alerts
Supplier management and cost tracking
Inventory valuation and reporting
User Interactions:

Add new products with pricing and categories
Monitor stock levels and movement history
Create purchase orders for suppliers
Process goods received and update stock
Adjust inventory for damage or theft
Generate inventory valuation reports
3. Customer Management Module (app/ui/views/customer_view.py)
Purpose: Customer relationship and loyalty management Key Features:

Comprehensive customer database
Purchase history and analytics
Loyalty points program management
Customer segmentation for marketing
Communication preferences tracking
Credit limit and payment terms management
User Interactions:

Register new customers with contact details
View complete purchase history
Manage loyalty points and rewards
Create customer groups for targeted promotions
Generate customer analytics reports
4. Financial Reporting Module (app/ui/views/reports_view.py)
Purpose: Business intelligence and regulatory reporting Key Features:

Real-time sales performance dashboards
GST reporting for IRAS compliance
Profit and loss statement generation
Cash flow analysis and forecasting
Staff performance tracking
Inventory turnover analysis
Multi-location consolidated reporting
User Interactions:

Select report types and date ranges
Customize report parameters and filters
Export reports in multiple formats (PDF, Excel, CSV)
Schedule automated report generation
View interactive charts and graphs
Drill down into transaction details
5. Administration Module (app/ui/views/admin_view.py)
Purpose: System configuration and user management Key Features:

User account and role management
System configuration and preferences
Database backup and restore utilities
Audit trail review and analysis
Integration settings management
License and subscription management
User Interactions:

Create and manage user accounts
Assign roles and permissions
Configure system settings and preferences
Review system logs and audit trails
Manage integrations and API settings
Perform system maintenance tasks
Technology Stack
Core Technologies
Programming Language: Python 3.11+
Rationale: Python provides excellent ecosystem support for business applications, strong database connectivity, and mature GUI frameworks. Version 3.11+ ensures access to latest performance improvements and security features.

Key Benefits:

Rapid development and prototyping capabilities
Extensive library ecosystem for business applications
Strong community support and documentation
Cross-platform compatibility (Windows, macOS, Linux)
Excellent testing framework support
GUI Framework: PySide6 (Qt 6)
Rationale: PySide6 offers enterprise-grade GUI capabilities with native look-and-feel across platforms, comprehensive widget library, and excellent performance for data-intensive applications.

Key Benefits:

Professional, native user interface components
Advanced data visualization capabilities
Comprehensive styling and theming support
Excellent keyboard and accessibility support
Robust event handling and signal/slot architecture
Built-in internationalization support
Database: PostgreSQL 15+
Rationale: PostgreSQL provides enterprise-level reliability, advanced data integrity features, excellent performance for business applications, and strong compliance capabilities required for financial data.

Key Benefits:

ACID compliance for financial data integrity
Advanced indexing and query optimization
Robust backup and recovery capabilities
Excellent concurrent user support
Strong security features and role-based access
JSON support for flexible data structures
Comprehensive audit logging capabilities
ORM: SQLAlchemy 2.0+
Rationale: SQLAlchemy provides sophisticated object-relational mapping with excellent performance, advanced query capabilities, and strong support for complex business data models.

Key Benefits:

Declarative model definition
Advanced relationship mapping
Query optimization and lazy loading
Database migration support
Connection pooling and performance optimization
Cross-database compatibility
Supporting Technologies
Asynchronous Processing: asyncio + threading
Purpose: Ensures responsive UI during database operations and long-running tasks Implementation: Dual-thread architecture with proper synchronization

Configuration Management: Pydantic Settings
Purpose: Type-safe configuration management with validation Benefits: Environment-specific settings, automatic validation, IDE support

Logging: Python logging + structlog
Purpose: Comprehensive application logging with structured output Benefits: Configurable log levels, structured JSON output, audit trail support

Testing Framework: pytest + pytest-qt
Purpose: Comprehensive testing including UI components Benefits: Fixture support, parametrized testing, GUI testing capabilities

Documentation: Sphinx + MkDocs
Purpose: Professional documentation generation Benefits: Auto-generated API docs, user guide generation, version control integration

Package Management: Poetry
Purpose: Dependency management and virtual environment handling Benefits: Lock file for reproducible builds, development vs production dependencies

Development Tools
Code Quality: Black + isort + flake8 + mypy
Purpose: Consistent code formatting and type checking Benefits: Automated formatting, import sorting, linting, type safety

Pre-commit Hooks: pre-commit framework
Purpose: Automated code quality checks before commits Benefits: Consistent code quality, early error detection

IDE Integration: VS Code / PyCharm configurations
Purpose: Optimized development environment Benefits: Debugging support, code completion, integrated testing

Deployment Technologies
Containerization: Docker + Docker Compose
Purpose: Consistent deployment across environments Benefits: Environment isolation, easy scaling, simplified deployment

Process Management: systemd (Linux) / Windows Services
Purpose: Production service management Benefits: Automatic startup, process monitoring, log management

Backup Solutions: pg_dump + automated scheduling
Purpose: Reliable data backup and recovery Benefits: Point-in-time recovery, automated scheduling, off-site storage

Environment Setup
Development Environment Setup
Prerequisites Installation
# Install Python 3.11+ (using pyenv for version management)
curl https://pyenv.run | bash
pyenv install 3.11.7
pyenv global 3.11.7

# Install PostgreSQL 15+
# Ubuntu/Debian:
sudo apt update
sudo apt install postgresql-15 postgresql-contrib-15

# macOS:
brew install postgresql@15
brew services start postgresql@15

# Windows:
# Download and install from https://www.postgresql.org/download/windows/

# Install Poetry for dependency management
curl -sSL https://install.python-poetry.org | python3 -

Project Setup
# Clone repository
git clone <repository-url> sg_pos_system
cd sg_pos_system

# Install dependencies
poetry install

# Install development dependencies
poetry install --with dev

# Activate virtual environment
poetry shell

# Set up pre-commit hooks
pre-commit install

Database Setup
# Create development database
sudo -u postgres createdb sg_pos_dev
sudo -u postgres createuser sg_pos_user --pwprompt

# Grant permissions
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE sg_pos_dev TO sg_pos_user;"

# Create .env file from template
cp .env.example .env

# Edit .env with your database credentials
# DATABASE_URL=postgresql://sg_pos_user:password@localhost:5432/sg_pos_dev

Environment Configuration
# .env.development
DEBUG=True
DATABASE_URL=postgresql://sg_pos_user:password@localhost:5432/sg_pos_dev
LOG_LEVEL=DEBUG
SECRET_KEY=development-secret-key-change-in-production
ENVIRONMENT=development

# Optional: Singapore-specific settings
DEFAULT_CURRENCY=SGD
GST_RATE=0.07
TIMEZONE=Asia/Singapore

Database Initialization
# Run database migrations
python scripts/setup_database.py

# Seed with sample data (optional)
python scripts/seed_data.py --sample-data

# Verify database setup
python -c "from app.config import get_database_url; print('Database connection:', get_database_url())"

Running the Application
# Start the application
python app/main.py

# Or using Poetry
poetry run python app/main.py

# Run with debug logging
LOG_LEVEL=DEBUG python app/main.py

Development Tools Setup
# Format code
black app/ tests/
isort app/ tests/

# Run linting
flake8 app/ tests/
mypy app/

# Run tests
pytest

# Run tests with coverage
pytest --cov=app --cov-report=html

# Generate documentation
cd docs/
make html

Production Environment Setup
System Requirements
Hardware Specifications:

CPU: 4+ cores, 2.4GHz or higher
RAM: 8GB minimum, 16GB recommended
Storage: 100GB SSD minimum, 500GB recommended
Network: 100Mbps connection for multi-location deployments
Operating System:

Ubuntu 22.04 LTS (recommended)
Windows Server 2019/2022
macOS 12+ (for single-location deployments)
Production Server Setup
# System update and basic packages
sudo apt update && sudo apt upgrade -y
sudo apt install -y software-properties-common curl wget git

# Install Python 3.11
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install -y python3.11 python3.11-venv python3.11-dev

# Install PostgreSQL 15
sudo apt install -y postgresql-15 postgresql-contrib-15
sudo systemctl enable postgresql
sudo systemctl start postgresql

# Install additional dependencies
sudo apt install -y build-essential libpq-dev nginx supervisor

Database Production Setup
# Create production database and user
sudo -u postgres createdb sg_pos_prod
sudo -u postgres createuser sg_pos_prod_user --pwprompt

# Configure PostgreSQL for production
sudo nano /etc/postgresql/15/main/postgresql.conf

# Key production settings:
# max_connections = 100
# shared_buffers = 256MB
# effective_cache_size = 1GB
# maintenance_work_mem = 64MB
# checkpoint_completion_target = 0.9
# wal_buffers = 16MB
# default_statistics_target = 100

# Configure authentication
sudo nano /etc/postgresql/15/main/pg_hba.conf

# Add application user access:
# local   sg_pos_prod    sg_pos_prod_user    md5
# host    sg_pos_prod    sg_pos_prod_user    127.0.0.1/32    md5

# Restart PostgreSQL
sudo systemctl restart postgresql

Application Deployment
# Create application user
sudo useradd -m -s /bin/bash sg_pos
sudo mkdir -p /opt/sg_pos
sudo chown sg_pos:sg_pos /opt/sg_pos

# Deploy application code
sudo -u sg_pos git clone <repository-url> /opt/sg_pos/app
cd /opt/sg_pos/app

# Create virtual environment
sudo -u sg_pos python3.11 -m venv venv
sudo -u sg_pos ./venv/bin/pip install --upgrade pip setuptools wheel

# Install production dependencies
sudo -u sg_pos ./venv/bin/pip install -r requirements.txt

Production Configuration
# Create production environment file
sudo -u sg_pos nano /opt/sg_pos/app/.env.production

# Production environment variables:
DEBUG=False
DATABASE_URL=postgresql://sg_pos_prod_user:secure_password@localhost:5432/sg_pos_prod
LOG_LEVEL=INFO
SECRET_KEY=production-secret-key-generate-secure-key
ENVIRONMENT=production
ALLOWED_HOSTS=localhost,your-domain.com

# Singapore production settings
DEFAULT_CURRENCY=SGD
GST_RATE=0.07
TIMEZONE=Asia/Singapore

# Backup configuration
BACKUP_SCHEDULE=0 2 * * *  # Daily at 2 AM
BACKUP_RETENTION_DAYS=30
BACKUP_LOCATION=/opt/sg_pos/backups/

Service Configuration
# Create systemd service file
sudo nano /etc/systemd/system/sg-pos.service

[Unit]
Description=SG Point of Sale System
After=network.target postgresql.service
Requires=postgresql.service

[Service]
Type=simple
User=sg_pos
Group=sg_pos
WorkingDirectory=/opt/sg_pos/app
Environment=PATH=/opt/sg_pos/app/venv/bin
ExecStart=/opt/sg_pos/app/venv/bin/python app/main.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target

# Enable and start service
sudo systemctl daemon-reload
sudo systemctl enable sg-pos
sudo systemctl start sg-pos

Backup Configuration
# Create backup script
sudo nano /opt/sg_pos/scripts/backup.sh
