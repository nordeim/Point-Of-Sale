<think>
This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore Point-of-Sale system. I need to create a detailed, technical document that covers all aspects of the system design and implementation. Let me analyze the key requirements:

1. Target: Small to medium-sized businesses (SMBs) in Singapore
2. Technology: Python + PySide6 + PostgreSQL
3. Architecture: Layered architecture with clean separation of concerns
4. Features: Comprehensive POS functionality with Singapore regulatory compliance
5. Quality: Production-ready code with best practices

I need to structure this PRD to include:
- Business context and requirements
- Technical architecture and design
- Database schema design
- Codebase structure and hierarchy
- Application modules and interactions
- Environment setup for development and production
- Implementation details

Let me create a comprehensive PRD that addresses all these aspects while maintaining professional quality and technical depth.
</think>

# SG Point-of-Sale (POS) System - Product Requirements Document

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Business Context & Objectives](#business-context--objectives)
3. [Functional Requirements](#functional-requirements)
4. [Technical Architecture](#technical-architecture)
5. [Technology Stack](#technology-stack)
6. [Database Schema Design](#database-schema-design)
7. [Codebase Structure & File Hierarchy](#codebase-structure--file-hierarchy)
8. [Application Modules & Components](#application-modules--components)
9. [User Interface Design](#user-interface-design)
10. [Security & Compliance](#security--compliance)
11. [Performance Requirements](#performance-requirements)
12. [Development Environment Setup](#development-environment-setup)
13. [Production Environment Setup](#production-environment-setup)
14. [Testing Strategy](#testing-strategy)
15. [Deployment & Maintenance](#deployment--maintenance)

## Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail needs of small to medium-sized businesses (SMBs) operating in Singapore. This system addresses the unique requirements of the Singapore market, including GST compliance, multi-currency support, and local regulatory requirements.

Built on a modern technology stack featuring Python 3.11+, PySide6 for the user interface, and PostgreSQL for data persistence, the application implements enterprise-grade architectural patterns including layered architecture, dependency injection, asynchronous processing, and robust data integrity mechanisms.

The system is designed to handle real-world business complexity while maintaining scalability, reliability, and user-friendliness. It provides comprehensive retail management capabilities including inventory management, sales processing, customer relationship management, financial reporting, and regulatory compliance features.

## Business Context & Objectives

### Target Market

**Primary Users:**
- Small to medium-sized retail businesses in Singapore
- Independent retailers, boutiques, cafes, restaurants
- Franchise operations with multiple locations
- Service-based businesses requiring point-of-sale functionality

**Business Objectives:**
- Streamline retail operations and reduce manual errors
- Ensure compliance with Singapore's GST regulations and reporting requirements
- Provide real-time business insights through comprehensive reporting
- Support multi-currency transactions for international customers
- Enable efficient inventory management and stock control
- Facilitate customer relationship management and loyalty programs

### Key Success Metrics

- **Operational Efficiency:** Reduce transaction processing time by 40%
- **Compliance:** 100% accuracy in GST calculations and reporting
- **User Adoption:** Achieve 95% user satisfaction rate within 6 months
- **System Reliability:** Maintain 99.9% uptime during business hours
- **Data Integrity:** Zero data loss incidents through robust backup systems

## Functional Requirements

### Core POS Functionality

**Sales Transaction Processing:**
- Process cash, card, and digital payment transactions
- Handle partial payments and split payments
- Support for discounts, promotions, and coupon codes
- Tax calculation with GST compliance
- Receipt generation and printing
- Transaction void and refund capabilities
- Multi-currency transaction support

**Inventory Management:**
- Product catalog management with categories and variants
- Real-time stock level tracking
- Low stock alerts and reorder notifications
- Barcode scanning and product lookup
- Batch and serial number tracking
- Supplier management and purchase orders
- Stock adjustment and cycle counting

**Customer Management:**
- Customer database with contact information
- Purchase history and transaction tracking
- Loyalty program integration
- Customer credit management
- Marketing campaign management
- Customer analytics and segmentation

**Financial Management:**
- Daily sales reporting and end-of-day procedures
- GST reporting and compliance
- Profit and loss statements
- Cash flow management
- Payment method reconciliation
- Multi-location financial consolidation

### Singapore-Specific Requirements

**GST Compliance:**
- Accurate GST calculation for all applicable transactions
- GST registration number validation
- GST reporting in IRAS-compliant format
- Support for zero-rated and exempt transactions
- GST audit trail maintenance

**Multi-Currency Support:**
- SGD as base currency with support for major international currencies
- Real-time exchange rate updates
- Currency conversion tracking
- Multi-currency reporting capabilities

**Regulatory Compliance:**
- PDPA compliance for customer data protection
- Audit trail maintenance for financial transactions
- Data retention policies aligned with Singapore regulations
- Secure data encryption and access controls

## Technical Architecture

### Architectural Principles

The SG POS System follows enterprise-grade architectural principles designed for scalability, maintainability, and reliability:

**Layered Architecture:**
The application implements a strict four-layer architecture pattern:

1. **Presentation Layer** (`app/ui/`): Handles all user interface components and user interactions
2. **Business Logic Layer** (`app/business_logic/`, `app/accounting/`): Contains core business rules and workflows
3. **Data Access Layer** (`app/services/`): Implements repository pattern for data operations
4. **Persistence Layer** (`app/models/`, database): Manages data storage and retrieval

**Dependency Injection:**
The system implements a sophisticated dependency injection mechanism through the `ApplicationCore` class, enabling:
- Loose coupling between components
- Easy testing and mocking
- Simplified maintenance and updates
- Modular component architecture

**Asynchronous Processing:**
Critical for maintaining responsive UI while handling complex operations:
- Background task processing for reports and data synchronization
- Non-blocking I/O operations
- Thread-safe UI updates
- Scalable concurrent operations

### Design Patterns Implementation

**Repository Pattern:**
Data access is abstracted through service classes that implement the repository pattern, providing:
- Clean separation between business logic and data access
- Consistent data access interface
- Easy database vendor switching capability
- Improved testability through mock repositories

**Result Pattern:**
Error handling and operation results are managed through the Result pattern:
- Explicit success/failure handling
- Rich error information propagation
- Improved debugging and logging capabilities
- Consistent error handling across layers

**Data Transfer Objects (DTOs):**
Data exchange between layers uses DTOs to ensure:
- Data integrity and validation
- Clear contract definitions between layers
- Reduced coupling between internal models and external interfaces
- Enhanced security through controlled data exposure

## Technology Stack

### Core Technologies

**Python 3.11+**
- **Rationale:** Modern Python features, improved performance, enhanced type hints
- **Key Features:** Pattern matching, performance improvements, better error messages
- **Dependencies:** asyncio for asynchronous operations, dataclasses for DTOs

**PySide6 (Qt6)**
- **Rationale:** Professional desktop UI framework with native look and feel
- **Key Features:** Cross-platform compatibility, rich widget set, modern UI components
- **Components:** QtWidgets for UI, QtCore for application logic, QtCharts for reporting

**PostgreSQL 14+**
- **Rationale:** Enterprise-grade database with ACID compliance and advanced features
- **Key Features:** JSON support, advanced indexing, concurrent transactions, data integrity
- **Extensions:** UUID support, full-text search, advanced analytics functions

### Supporting Libraries

**SQLAlchemy 2.0+**
- **Purpose:** Object-Relational Mapping (ORM) and database abstraction
- **Features:** Modern async support, type safety, query optimization
- **Benefits:** Database vendor independence, complex query support, migration management

**Alembic**
- **Purpose:** Database migration management
- **Features:** Version control for database schema, automated migrations
- **Benefits:** Environment synchronization, rollback capabilities, change tracking

**Pydantic 2.0+**
- **Purpose:** Data validation and serialization
- **Features:** Type validation, JSON schema generation, performance optimization
- **Benefits:** Runtime type checking, API documentation, data integrity

**AsyncIO & Asyncio-based Libraries**
- **Purpose:** Asynchronous programming support
- **Libraries:** aiofiles for file operations, aiohttp for web requests
- **Benefits:** Non-blocking operations, improved responsiveness, scalable I/O

**Testing Framework**
- **pytest:** Primary testing framework with extensive plugin ecosystem
- **pytest-asyncio:** Async test support
- **pytest-qt:** Qt application testing capabilities
- **coverage.py:** Code coverage analysis

### Development & Deployment Tools

**Development Environment:**
- **Poetry:** Dependency management and virtual environment handling
- **Black:** Code formatting and style consistency
- **mypy:** Static type checking and validation
- **pre-commit:** Code quality hooks and automated checks

**Monitoring & Logging:**
- **structlog:** Structured logging with JSON output
- **psutil:** System resource monitoring
- **Sentry:** Error tracking and performance monitoring (optional)

## Database Schema Design

### Core Entities

The database schema is designed to support comprehensive retail operations while maintaining data integrity and performance:

```sql
-- Companies and Multi-tenancy Support
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE,
    gst_registration_number VARCHAR(20),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    base_currency VARCHAR(3) DEFAULT 'SGD',
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
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    role VARCHAR(50) DEFAULT 'staff',
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Product Categories
CREATE TABLE product_categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    parent_category_id UUID REFERENCES product_categories(id),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Products
CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    category_id UUID REFERENCES product_categories(id),
    sku VARCHAR(100) NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    barcode VARCHAR(100),
    unit_price DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2),
    gst_rate DECIMAL(5,2) DEFAULT 7.00,
    is_gst_inclusive BOOLEAN DEFAULT false,
    track_inventory BOOLEAN DEFAULT true,
    current_stock INTEGER DEFAULT 0,
    minimum_stock INTEGER DEFAULT 0,
    maximum_stock INTEGER,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, sku)
);

-- Customers
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    customer_number VARCHAR(50),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    company_name VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    gst_registration_number VARCHAR(20),
    credit_limit DECIMAL(10,2) DEFAULT 0,
    current_balance DECIMAL(10,2) DEFAULT 0,
    loyalty_points INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, customer_number)
);

-- Sales Transactions
CREATE TABLE sales_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    transaction_number VARCHAR(50) NOT NULL,
    customer_id UUID REFERENCES customers(id),
    user_id UUID NOT NULL REFERENCES users(id),
    transaction_date TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    subtotal DECIMAL(10,2) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    total_amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,4) DEFAULT 1.0000,
    payment_status VARCHAR(20) DEFAULT 'pending',
    transaction_status VARCHAR(20) DEFAULT 'active',
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, transaction_number)
);

-- Sales Transaction Items
CREATE TABLE sales_transaction_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID NOT NULL REFERENCES sales_transactions(id) ON DELETE CASCADE,
    product_id UUID NOT NULL REFERENCES products(id),
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    gst_rate DECIMAL(5,2) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(10,2) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Payment Methods
CREATE TABLE payment_methods (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(100) NOT NULL,
    type VARCHAR(50) NOT NULL, -- 'cash', 'card', 'digital', 'bank_transfer'
    is_active BOOLEAN DEFAULT true,
    processing_fee_rate DECIMAL(5,4) DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, name)
);

-- Payments
CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID NOT NULL REFERENCES sales_transactions(id),
    payment_method_id UUID NOT NULL REFERENCES payment_methods(id),
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,4) DEFAULT 1.0000,
    reference_number VARCHAR(100),
    processing_fee DECIMAL(10,2) DEFAULT 0,
    payment_date TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'completed',
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Inventory Movements
CREATE TABLE inventory_movements (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    product_id UUID NOT NULL REFERENCES products(id),
    movement_type VARCHAR(50) NOT NULL, -- 'sale', 'purchase', 'adjustment', 'return'
    reference_type VARCHAR(50), -- 'sales_transaction', 'purchase_order', 'adjustment'
    reference_id UUID,
    quantity_change INTEGER NOT NULL,
    unit_cost DECIMAL(10,2),
    total_cost DECIMAL(10,2),
    stock_before INTEGER NOT NULL,
    stock_after INTEGER NOT NULL,
    movement_date TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Chart of Accounts for Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    account_code VARCHAR(20) NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL, -- 'asset', 'liability', 'equity', 'revenue', 'expense'
    parent_account_id UUID REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, account_code)
);

-- Journal Entries for Double-Entry Bookkeeping
CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    entry_number VARCHAR(50) NOT NULL,
    reference_type VARCHAR(50), -- 'sales_transaction', 'payment', 'adjustment'
    reference_id UUID,
    entry_date DATE NOT NULL,
    description TEXT,
    total_debit DECIMAL(10,2) NOT NULL,
    total_credit DECIMAL(10,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'posted',
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, entry_number)
);

-- Journal Entry Lines
CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    journal_entry_id UUID NOT NULL REFERENCES journal_entries(id) ON DELETE CASCADE,
    account_id UUID NOT NULL REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(10,2) DEFAULT 0,
    credit_amount DECIMAL(10,2) DEFAULT 0,
    description TEXT,
    line_number INTEGER NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- GST Transactions for Compliance Reporting
CREATE TABLE gst_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    transaction_id UUID NOT NULL REFERENCES sales_transactions(id),
    gst_rate DECIMAL(5,2) NOT NULL,
    taxable_amount DECIMAL(10,2) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL,
    transaction_type VARCHAR(20) NOT NULL, -- 'standard', 'zero_rated', 'exempt'
    gst_period VARCHAR(10) NOT NULL, -- Format: YYYY-MM
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Exchange Rates for Multi-Currency Support
CREATE TABLE exchange_rates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    from_currency VARCHAR(3) NOT NULL,
    to_currency VARCHAR(3) NOT NULL,
    rate DECIMAL(10,6) NOT NULL,
    effective_date DATE NOT NULL,
    source VARCHAR(50) DEFAULT 'manual',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(from_currency, to_currency, effective_date)
);
```

### Database Indexes and Constraints

```sql
-- Performance Indexes
CREATE INDEX idx_products_company_sku ON products(company_id, sku);
CREATE INDEX idx_products_barcode ON products(barcode) WHERE barcode IS NOT NULL;
CREATE INDEX idx_sales_transactions_date ON sales_transactions(company_id, transaction_date);
CREATE INDEX idx_sales_transactions_customer ON sales_transactions(customer_id) WHERE customer_id IS NOT NULL;
CREATE INDEX idx_inventory_movements_product_date ON inventory_movements(product_id, movement_date);
CREATE INDEX idx_gst_transactions_period ON gst_transactions(company_id, gst_period);

-- Data Integrity Constraints
ALTER TABLE journal_entries ADD CONSTRAINT check_balanced_entry 
    CHECK (total_debit = total_credit);

ALTER TABLE journal_entry_lines ADD CONSTRAINT check_debit_or_credit 
    CHECK ((debit_amount > 0 AND credit_amount = 0) OR (credit_amount > 0 AND debit_amount = 0));

ALTER TABLE exchange_rates ADD CONSTRAINT check_positive_rate 
    CHECK (rate > 0);

-- Triggers for Automatic Updates
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_companies_updated_at BEFORE UPDATE ON companies 
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

CREATE TRIGGER update_products_updated_at BEFORE UPDATE ON products 
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

CREATE TRIGGER update_customers_updated_at BEFORE UPDATE ON customers 
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
```

## Codebase Structure & File Hierarchy

The application follows a well-organized, modular structure that supports scalability and maintainability:

```
sg_pos_system/
├── app/                                    # Main application directory
│   ├── __init__.py
│   ├── main.py                            # Application entry point
│   ├── application_core.py                # Dependency injection container
│   ├── config/                            # Configuration management
│   │   ├── __init__.py
│   │   ├── settings.py                    # Application settings
│   │   ├── database.py                    # Database configuration
│   │   └── logging_config.py              # Logging configuration
│   ├── models/                            # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                        # Base model class
│   │   ├── company.py                     # Company model
│   │   ├── user.py                        # User model
│   │   ├── product.py                     # Product and category models
│   │   ├── customer.py                    # Customer model
│   │   ├── transaction.py                 # Sales transaction models
│   │   ├── payment.py                     # Payment models
│   │   ├── inventory.py                   # Inventory movement models
│   │   ├── accounting.py                  # Chart of accounts and journal entries
│   │   └── gst.py                         # GST-related models
│   ├── services/                          # Data access layer (Repository pattern)
│   │   ├── __init__.py
│   │   ├── base_service.py               # Base service class
│   │   ├── company_service.py            # Company data operations
│   │   ├── user_service.py               # User authentication and management
│   │   ├── product_service.py            # Product catalog operations
│   │   ├── customer_service.py           # Customer management operations
│   │   ├── transaction_service.py        # Sales transaction operations
│   │   ├── payment_service.py            # Payment processing operations
│   │   ├── inventory_service.py          # Inventory management operations
│   │   ├── accounting_service.py         # Accounting and journal entry operations
│   │   ├── gst_service.py                # GST calculations and reporting
│   │   └── exchange_rate_service.py      # Currency exchange operations
│   ├── business_logic/                    # Business layer managers
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── base_manager.py           # Base manager class
│   │   │   ├── customer_manager.py       # Customer business logic
│   │   │   ├── product_manager.py        # Product management logic
│   │   │   ├── sales_manager.py          # Sales processing logic
│   │   │   ├── payment_manager.py        # Payment processing logic
│   │   │   ├── inventory_manager.py      # Inventory management logic
│   │   │   ├── reporting_manager.py      # Report generation logic
│   │   │   └── user_manager.py           # User management logic
│   │   ├── workflows/                    # Complex business workflows
│   │   │   ├── __init__.py
│   │   │   ├── checkout_workflow.py      # Complete checkout process
│   │   │   ├── refund_workflow.py        # Refund processing workflow
│   │   │   ├── inventory_adjustment_workflow.py  # Stock adjustment workflow
│   │   │   └── end_of_day_workflow.py    # End-of-day procedures
│   │   └── validators/                   # Business rule validators
│   │       ├── __init__.py
│   │       ├── transaction_validator.py  # Transaction validation rules
│   │       ├── customer_validator.py     # Customer data validation
│   │       └── product_validator.py      # Product validation rules
│   ├── accounting/                        # Singapore-specific accounting
│   │   ├── __init__.py
│   │   ├── gst_manager.py                # GST calculations and compliance
│   │   ├── journal_manager.py            # Double-entry bookkeeping
│   │   ├── chart_of_accounts_manager.py  # Chart of accounts management
│   │   └── financial_reports_manager.py  # Financial reporting
│   ├── ui/                               # Presentation layer (PySide6)
│   │   ├── __init__.py
│   │   ├── main_window.py                # Main application window
│   │   ├── dialogs/                      # Modal dialogs
│   │   │   ├── __init__.py
│   │   │   ├── login_dialog.py           # User authentication dialog
│   │   │   ├── customer_dialog.py        # Customer add/edit dialog
│   │   │   ├── product_dialog.py         # Product add/edit dialog
│   │   │   ├── payment_dialog.py         # Payment processing dialog
│   │   │   ├── refund_dialog.py          # Refund processing dialog
│   │   │   └── settings_dialog.py        # Application settings dialog
│   │   ├── widgets/                      # Reusable UI components
│   │   │   ├── __init__.py
│   │   │   ├── pos_widget.py             # Main POS interface
│   │   │   ├── product_catalog_widget.py # Product browsing interface
│   │   │   ├── customer_widget.py        # Customer management interface
│   │   │   ├── inventory_widget.py       # Inventory management interface
│   │   │   ├── reports_widget.py         # Reporting interface
│   │   │   ├── chart_of_accounts_widget.py # Accounting interface
│   │   │   └── dashboard_widget.py       # Business dashboard
│   │   ├── models/                       # Qt models for data binding
│   │   │   ├── __init__.py
│   │   │   ├── product_model.py          # Product table model
│   │   │   ├── customer_model.py         # Customer table model
│   │   │   ├── transaction_model.py      # Transaction table model
│   │   │   └── cart_model.py             # Shopping cart model
│   │   ├── components/                   # UI components
│   │   │   ├── __init__.py
│   │   │   ├── barcode_scanner.py        # Barcode scanning component
│   │   │   ├── receipt_printer.py        # Receipt printing component
│   │   │   ├── cash_drawer.py            # Cash drawer control
│   │   │   └── display_screen.py         # Customer display screen
│   │   └── styles/                       # UI styling and themes
│   │       ├── __init__.py
│   │       ├── default_theme.py          # Default application theme
│   │       └── singapore_theme.py        # Singapore-specific theme
│   ├── dto/                              # Data Transfer Objects
│   │   ├── __init__.py
│   │   ├── base_dto.py                   # Base DTO class
│   │   ├── customer_dto.py               # Customer data transfer objects
│   │   ├── product_dto.py                # Product data transfer objects
│   │   ├── transaction_dto.py            # Transaction data transfer objects
│   │   ├── payment_dto.py                # Payment data transfer objects
│   │   └── report_dto.py                 # Report data transfer objects
│   ├── utils/                            # Utility functions and helpers
│   │   ├── __init__.py
│   │   ├── async_utils.py                # Asynchronous operation utilities
│   │   ├── currency_utils.py             # Currency conversion utilities
│   │   ├── gst_utils.py                  # GST calculation utilities
│   │   ├── validation_utils.py           # Data validation utilities
│   │   ├── encryption_utils.py           # Data encryption utilities
│   │   ├── pdf_utils.py                  # PDF generation utilities
│   │   └── barcode_utils.py              # Barcode generation utilities
│   ├── exceptions/                       # Custom exception classes
│   │   ├── __init__.py
│   │   ├── base_exceptions.py            # Base exception classes
│   │   ├── business_exceptions.py        # Business logic exceptions
│   │   ├── data_exceptions.py            # Data access exceptions
│   │   └── ui_exceptions.py              # UI-related exceptions
│   └── interfaces/                       # Abstract interfaces and protocols
│       ├── __init__.py
│       ├── repository_interface.py       # Repository pattern interface
│       ├── manager_interface.py          # Manager pattern interface
│       └── service_interface.py          # Service pattern interface
├── tests/                                # Test suites
│   ├── __init__.py
│   ├── conftest.py                       # Pytest configuration
│   ├── unit/                             # Unit tests
│   │   ├── __init__.py
│   │   ├── test_services/                # Service layer tests
│   │   ├── test_managers/                # Manager layer tests
│   │   ├── test_models/                  # Model layer tests
│   │   └── test_utils/                   # Utility function tests
│   ├── integration/                      # Integration tests
│   │   ├── __init__.py
│   │   ├── test_workflows/               # Workflow integration tests
│   │   └── test_database/                # Database integration tests
│   └── ui/                               # UI tests
│       ├── __init__.py
│       └── test_widgets/                 # Widget functionality tests
├── scripts/                              # Database and deployment scripts
│   ├── create_database.py               # Database creation script
│   ├── migrate_database.py              # Database migration script
│   ├── seed_data.py                     # Test data seeding script
│   ├── backup_database.py               # Database backup script
│   └── deployment/                       # Deployment automation
│       ├── build_installer.py           # Application installer builder
│       └── update_checker.py            # Application update checker
├── migrations/                           # Alembic database migrations
│   ├── versions/                         # Migration version files
│   ├── alembic.ini                      # Alembic configuration
│   └── env.py                           # Migration environment setup
├── resources/                            # Static resources
│   ├── icons/                           # Application icons
│   ├── images/                          # UI images and graphics
│   ├── fonts/                           # Custom fonts
│   ├── templates/                       # Report and receipt templates
│   │   ├── receipt_template.html        # Receipt template
│   │   ├── invoice_template.html        # Invoice template
│   │   └── report_templates/            # Various report templates
│   └── sql/                             # SQL scripts and schema
│       ├── schema.sql                   # Database schema definition
│       ├── initial_data.sql             # Initial setup data
│       └── functions.sql                # Database functions and triggers
├── config/                               # Configuration files
│   ├── settings.yaml                    # Application settings
│   ├── database.yaml                    # Database configuration
│   ├── logging.yaml                     # Logging configuration
│   └── environments/                    # Environment-specific configs
│       ├── development.yaml             # Development settings
│       ├── production.yaml              # Production settings
│       └── testing.yaml                 # Testing settings
├── docs/                                # Documentation
│   ├── user_manual.md                   # User manual
│   ├── api_documentation.md             # API documentation
│   ├── deployment_guide.md              # Deployment guide
│   └── architecture_overview.md         # Architecture documentation
├── requirements/                         # Python dependencies
│   ├── base.txt                         # Base requirements
│   ├── development.txt                  # Development dependencies
│   ├── production.txt                   # Production dependencies
│   └── testing.txt                      # Testing dependencies
├── pyproject.toml                       # Poetry configuration and metadata
├── README.md                            # Project overview and setup
├── LICENSE                              # Software license
└── .gitignore                           # Git ignore rules
```

## Application Modules & Components

### Core Application Modules

**ApplicationCore (`app/application_core.py`)**
The central dependency injection container that manages all application services and managers. It implements lazy initialization for optimal performance and provides a unified access point for all application components.

Key features:
- Lazy initialization of services and managers using `@property` decorators
- Centralized configuration management
- Database session management
- Async task coordination
- Logging and monitoring integration

**Configuration Management (`app/config/`)**
Handles application configuration across different environments with support for YAML-based configuration files, environment variable overrides, and runtime configuration updates.

Components:
- `settings.py`: Core application settings management
- `database.py`: Database connection configuration
- `logging_config.py`: Structured logging setup

### Data Layer

**Models (`app/models/`)**
SQLAlchemy ORM models that define the database schema and relationships. Each model includes:
- Proper field validation and constraints
- Relationship definitions with lazy loading optimization
- Audit trail fields (created_at, updated_at)
- String representations for debugging

Key models:
- `Company`: Multi-tenant support with company isolation
- `User`: Authentication and authorization
- `Product`: Comprehensive product catalog with categories
- `Customer`: Customer relationship management
- `Transaction`: Sales transaction processing
- `Payment`: Multi-method payment support
- `Inventory`: Real-time stock tracking
- `Accounting`: Double-entry bookkeeping support

**Services (`app/services/`)**
Repository pattern implementation providing clean data access abstraction. Each service implements:
- CRUD operations with proper error handling
- Complex query operations
- Transaction management
- Data validation and sanitization

### Business Logic Layer

**Managers (`app/business_logic/managers/`)**
Orchestrate complex business workflows and enforce business rules. Each manager focuses on a specific domain:

- `SalesManager`: Complete sales transaction processing
- `PaymentManager`: Multi-method payment processing with journal entry generation
- `InventoryManager`: Real-time stock tracking and movement recording
- `CustomerManager`: Customer lifecycle management
- `ProductManager`: Product catalog management with pricing rules
- `ReportingManager`: Comprehensive business reporting

**Workflows (`app/business_logic/workflows/`)**
Complex multi-step business processes that coordinate multiple managers:

- `CheckoutWorkflow`: Complete checkout process from cart to receipt
- `RefundWorkflow`: Comprehensive refund processing with inventory updates
- `EndOfDayWorkflow`: Daily reconciliation and reporting procedures

**Singapore-Specific Accounting (`app/accounting/`)**
Specialized modules for Singapore regulatory compliance:

- `GSTManager`: GST calculation, validation, and reporting
- `JournalManager`: Double-entry bookkeeping with audit trails
- `ChartOfAccountsManager`: Singapore-standard chart of accounts
- `FinancialReportsManager`: IRAS-compliant financial reporting

### Presentation Layer

**Main Window (`app/ui/main_window.py`)**
Central application interface featuring:
- Tabbed interface for different functional areas
- Real-time dashboard with key metrics
- Quick access toolbar for common operations
- Status bar with system information
- Menu system with keyboard shortcuts

**Widgets (`app/ui/widgets/`)**
Specialized UI components for different business functions:

- `POSWidget`: Main point-of-sale interface with product selection, cart management, and payment processing
- `ProductCatalogWidget`: Product management with category browsing and search
- `CustomerWidget`: Customer management with purchase history
- `InventoryWidget`: Real-time inventory monitoring and management
- `ReportsWidget`: Interactive reporting with charts and export capabilities
- `DashboardWidget`: Executive dashboard with key performance indicators

**Dialogs (`app/ui/dialogs/`)**
Modal dialogs for specific operations:
- User authentication and session management
- Customer and product data entry
- Payment processing with multiple methods
- Settings and configuration management

### Support Components

**Data Transfer Objects (`app/dto/`)**
Structured data containers for inter-layer communication:
- Input validation and sanitization
- Type safety and serialization
- API contract enforcement
- Version compatibility management

**Utilities (`app/utils/`)**
Shared utility functions:
- Asynchronous operation helpers
- Currency conversion and formatting
- GST calculation utilities
- Encryption and security functions
- PDF generation for receipts and reports

**Exception Handling (`app/exceptions/`)**
Comprehensive error handling system:
- Hierarchical exception classes
- Error context preservation
- User-friendly error messages
- Logging and monitoring integration

## User Interface Design

### Design Principles

**Professional Appearance**
The application follows modern desktop application design principles with a clean, professional interface that reduces cognitive load and improves user efficiency.

**Responsive Layout**
All interface components are designed to work effectively across different screen sizes and resolutions, with proper scaling and layout adjustment.

**Accessibility**
The interface implements accessibility best practices including:
- Keyboard navigation support
- High contrast mode compatibility
- Screen reader compatibility
- Configurable font sizes

### Main Interface Components

**Navigation Structure**
- **Tabbed Interface**: Primary navigation using tabs for different functional areas
- **Quick Access Toolbar**: Frequently used functions accessible via toolbar buttons
- **Context Menus**: Right-click menus for context-sensitive operations
- **Keyboard Shortcuts**: Comprehensive keyboard shortcuts for power users

**POS Interface**
- **Product Selection**: Visual product grid with search and category filtering
- **Shopping Cart**: Real-time cart with quantity adjustment and item removal
- **Payment Processing**: Multi-method payment interface with change calculation
- **Receipt Generation**: Instant receipt preview and printing options

**Dashboard**
- **Sales Metrics**: Real-time sales performance indicators
- **Inventory Alerts**: Low stock notifications and reorder suggestions
- **Financial Summary**: Daily, weekly, and monthly financial summaries
- **Customer Insights**: Top customers and purchasing patterns

## Security & Compliance

### Data Protection

**Encryption Standards**
- **Data at Rest**: AES-256 encryption for sensitive data storage
- **Data in Transit**: TLS 1.3 for all network communications
- **Password Security**: bcrypt hashing with salt for password storage
- **PII Protection**: Tokenization of personally identifiable information

**Access Control**
- **Role-Based Access Control (RBAC)**: Granular permissions based on user roles
- **Multi-Factor Authentication**: Optional 2FA for enhanced security
- **Session Management**: Secure session handling with automatic timeout
- **Audit Logging**: Comprehensive audit trail for all user actions

### Regulatory Compliance

**Singapore PDPA Compliance**
- **Data Minimization**: Collect only necessary customer information
- **Consent Management**: Clear consent mechanisms for data collection
- **Data Retention**: Automated data retention policy enforcement
- **Right to Access**: Customer data access and portability features

**GST Compliance**
- **Accurate Calculations**: Precise GST calculation for all transaction types
- **Audit Trail**: Complete audit trail for GST transactions
- **Reporting Integration**: Direct integration with IRAS reporting requirements
- **Record Keeping**: Automated record keeping for regulatory compliance

**Financial Regulations**
- **Double-Entry Bookkeeping**: Complete financial transaction recording
- **Audit Support**: Comprehensive audit trail and reporting capabilities
- **Data Integrity**: Cryptographic verification of financial data
- **Backup Requirements**: Automated backup systems for data preservation

## Performance Requirements

### System Performance

**Response Time Targets**
- **Transaction Processing**: < 2 seconds for complete sales transaction
- **Product Lookup**: < 500ms for product search and selection
- **Report Generation**: < 10 seconds for standard reports
- **Database Operations**: < 1 second for standard CRUD operations

**Scalability Requirements**
- **Concurrent Users**: Support for up to 10 concurrent users per instance
- **Transaction Volume**: Handle up to 1000 transactions per day
- **Product Catalog**: Support for up to 10,000 products
- **Customer Database**: Support for up to 50,000 customers

**Resource Utilization**
- **Memory Usage**: Maximum 1GB RAM usage under normal operation
- **Disk Space**: Maximum 10GB for application and data storage
- **CPU Usage**: Maximum 50% CPU utilization during peak operations
- **Network Bandwidth**: Minimal network usage for local operations

### Database Performance

**Query Optimization**
- Strategic indexing for frequently accessed data
- Query optimization for complex reporting operations
- Connection pooling for efficient database access
- Caching strategies for frequently accessed data

**Data Integrity**
- Foreign key constraints to ensure referential integrity
- Check constraints for business rule enforcement
- Triggers for automatic data validation and updates
- Regular integrity checks and maintenance procedures

## Development Environment Setup

### Prerequisites

**System Requirements**
- Python 3.11 or higher
- PostgreSQL 14 or higher
- Git version control system
- Visual Studio Code or PyCharm IDE (recommended)

**Installation Steps**

1. **Clone Repository**
```bash
git clone https://github.com/company/sg-pos-system.git
cd sg-pos-system
```

2. **Install Poetry (Dependency Management)**
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

3. **Setup Python Environment**
```bash
poetry install --with dev,test
poetry shell
```

4. **Database Setup**
```bash
# Install PostgreSQL (Ubuntu/Debian)
sudo apt update
sudo apt install postgresql postgresql-contrib

# Create database user and database
sudo -u postgres psql
CREATE USER sgpos_user WITH PASSWORD 'development_password';
CREATE DATABASE sgpos_dev OWNER sgpos_user;
GRANT ALL PRIVILEGES ON DATABASE sgpos_dev TO sgpos_user;
\q
```

5. **Environment Configuration**
```bash
# Copy environment template
cp config/environments/development.yaml.template config/environments/development.yaml

# Edit configuration file with your settings
nano config/environments/development.yaml
```

6. **Database Migration**
```bash
# Run database migrations
alembic upgrade head

# Seed initial data
python scripts/seed_data.py
```

7. **Development Tools Setup**
```bash
# Install pre-commit hooks
pre-commit install

# Setup IDE configuration
cp .vscode/settings.json.template .vscode/settings.json
```

### Development Workflow

**Code Quality Tools**
```bash
# Code formatting
black app/ tests/

# Type checking
mypy app/

# Linting
flake8 app/ tests/

# Testing
pytest tests/ --cov=app

# Pre-commit validation
pre-commit run --all-files
```

**Running the Application**
```bash
# Development mode with hot reload
python -m app.main --dev

# Debug mode with verbose logging
python -m app.main --debug
```

**Database Operations**
```bash
# Create new migration
alembic revision --autogenerate -m "Description of changes"

# Apply migration
alembic upgrade head

# Rollback migration
alembic downgrade -1

# Reset database (development only)
python scripts/reset_database.py
```

## Production Environment Setup

### Infrastructure Requirements

**Server Specifications**
- **CPU**: Minimum 4 cores, recommended 8 cores
- **RAM**: Minimum 8GB, recommended 16GB
- **Storage**: Minimum 100GB SSD storage
- **Network**: Stable internet connection for updates and support
- **Operating System**: Ubuntu 20.04 LTS or Windows Server 2019

**Database Configuration**
```yaml
# Production PostgreSQL configuration
postgresql:
  host: localhost
  port: 5432
  database: sgpos_production
  username: sgpos_prod
  password: ${POSTGRES_PASSWORD}
  pool_size: 20
  max_overflow: 0
  pool_timeout: 30
  pool_recycle: 3600
```

### Deployment Process

**Application Packaging**
```bash
# Build production package
poetry build

# Create installer package
python scripts/deployment/build_installer.py --production

# Generate deployment artifacts
python scripts/deployment/create_deployment_package.py
```

**Production Database Setup**
```bash
# Create production database
sudo -u postgres createdb sgpos_production

# Create production user with limited privileges
sudo -u postgres psql
CREATE USER sgpos_prod WITH PASSWORD 'secure_production_password';
GRANT CONNECT ON DATABASE sgpos_production TO sgpos_prod;
GRANT USAGE ON SCHEMA public TO sgpos_prod;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO sgpos_prod;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO sgpos_prod;
```

**Security Configuration**
```yaml
# Production security settings
security:
  encryption_key: ${ENCRYPTION_KEY}
  jwt_secret: ${JWT_SECRET}
  session_timeout: 3600
  max_login_attempts: 5
  password_policy:
    min_length: 8
    require_uppercase: true
    require_lowercase: true
    require_numbers: true
    require_symbols: true
```

**Monitoring and Logging**
```yaml
# Production logging configuration
logging:
  level: INFO
  format: json
  file_rotation: daily
  retention_days: 30
  syslog_enabled: true
  error_tracking: sentry
```

**Backup Configuration**
```bash
# Automated database backup
0 2 * * * /usr/local/bin/backup_sgpos_db.sh

# Application data backup
0 3 * * * /usr/local/bin/backup_sgpos_data.sh

# Weekly full system backup
0 4 * * 0 /usr/local/bin/backup_sgpos_full.sh
```

### Performance Optimization

**Database Optimization**
- Regular VACUUM and ANALYZE operations
- Index optimization based on query patterns
- Connection pooling configuration
- Query performance monitoring

**Application Optimization**
- Asset minification and compression
- Caching strategies for frequently accessed data
- Lazy loading for heavy operations
- Memory usage monitoring and optimization

**System Monitoring**
- Real-time performance monitoring
- Error tracking and alerting
- Resource usage monitoring
- Automated health checks

## Testing Strategy

### Test Coverage Requirements

**Unit Tests (Target: 90% Coverage)**
- Model validation and business logic
- Service layer functionality
- Utility function testing
- Exception handling verification

**Integration Tests**
- Database integration testing
- API endpoint testing
- Workflow integration testing
- Third-party service integration

**UI Tests**
- Widget functionality testing
- User interaction testing
- Accessibility testing
- Cross-platform compatibility

### Test Automation

**Continuous Integration Pipeline**
```yaml
# GitHub Actions workflow
name: CI/CD Pipeline
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: |
          pip install poetry
          poetry install --with dev,test
      - name: Run tests
        run: |
          poetry run pytest --cov=app --cov-report=xml
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

**Test Data Management**
- Automated test data generation
- Database state management for tests
- Mock data for external dependencies
- Test environment isolation

## Deployment & Maintenance

### Release Management

**Version Control Strategy**
- Semantic versioning (MAJOR.MINOR.PATCH)
- Feature branch workflow
- Release branch stabilization
- Tag-based release deployment

**Deployment Pipeline**
1. **Development**: Continuous integration testing
2. **Staging**: Pre-production validation
3. **Production**: Automated deployment with rollback capability
4. **Post-deployment**: Monitoring and validation

**Update Management**
- Automatic update checking
- Incremental update packages
- Database migration handling
- Configuration migration support

### Maintenance Procedures

**Regular Maintenance Tasks**
- Database optimization and cleanup
- Log file rotation and cleanup
- Security patch application
- Performance monitoring and optimization

**Backup and Recovery**
- Daily automated backups
- Weekly full system backups
- Monthly backup verification
- Disaster recovery procedures

**Support and Monitoring**
- 24/7 system monitoring
- Error tracking and alerting
- Performance monitoring
- User support and documentation

This comprehensive Product Requirements Document provides a complete blueprint for building the SG Point-of-Sale system. The document covers all aspects of the system from business requirements to technical implementation details, ensuring that development teams have clear guidance for building a robust, scalable, and compliant retail management solution tailored specifically for the Singapore market.

The architecture and design outlined in this PRD emphasizes clean code principles, proper separation of concerns, and enterprise-grade patterns that will ensure the system can handle real-world business complexity while remaining maintainable and extensible for future enhancements.
