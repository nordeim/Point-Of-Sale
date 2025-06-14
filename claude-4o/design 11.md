The user is asking for a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. This needs to be extremely detailed (at least 6000 words) and include:
Database schema design
Codebase file hierarchy diagram
Application modules and user interaction diagram
Listing and description of key application modules and files
Technology stack description
Development and production environment setup
Singapore-specific regulatory requirements
The system should use:

Python with PySide6 for UI
PostgreSQL for database
Clean layered architecture
Asynchronous processing
Dependency injection
DTOs and Result pattern
Multi-currency support
I need to create a comprehensive document that leaves no ambiguity for implementation. Let me structure this properly with all the required sections. </think>

Product Requirements Document
SG Point-of-Sale (POS) System
Version 1.0
Date: June 2025
Table of Contents
Executive Summary
Product Overview
Technology Stack
System Architecture
Database Schema Design
Codebase Structure and File Hierarchy
Core Application Modules
User Interaction Flow
Key Features and Functionality
Singapore Regulatory Compliance
Development Environment Setup
Production Environment Setup
Security Considerations
Performance and Scalability
Testing Strategy
Deployment Strategy
Maintenance and Support
Future Enhancements
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) in Singapore. Built on a robust technology stack featuring Python, PySide6, and PostgreSQL, this system provides a professional-grade retail management solution that adheres to Singapore's unique regulatory requirements while offering exceptional performance and scalability.

Key Objectives
Regulatory Compliance: Full compliance with Singapore's GST requirements, IRAS regulations, and financial reporting standards
User Experience: Intuitive, modern interface that minimizes training requirements
Performance: Sub-second response times for all common operations
Scalability: Architecture supporting growth from single-terminal to multi-location deployments
Data Integrity: Robust transaction management with complete audit trails
Multi-Currency Support: Native handling of Singapore Dollar (SGD) and major foreign currencies
Target Market
Primary target users include:

Retail shops (clothing, electronics, general merchandise)
F&B establishments (restaurants, cafes, food courts)
Service businesses (salons, clinics, repair shops)
Small supermarkets and convenience stores
Success Metrics
Transaction processing time < 3 seconds
System uptime > 99.9%
Zero data loss guarantee
GST report generation < 30 seconds
User satisfaction score > 4.5/5
2. Product Overview
2.1 Product Vision
To create the most reliable, efficient, and user-friendly point-of-sale system tailored specifically for Singapore's SMB market, enabling businesses to streamline operations, ensure regulatory compliance, and make data-driven decisions.

2.2 Core Value Propositions
Singapore-Centric Design: Built from the ground up with Singapore's business environment in mind
Regulatory Peace of Mind: Automated GST calculations, IRAS-compliant reporting
Operational Efficiency: Streamlined workflows reducing transaction time by up to 40%
Business Intelligence: Real-time analytics and insights for informed decision-making
Future-Proof Architecture: Scalable design supporting business growth
2.3 Key Differentiators
Offline-First Architecture: Full functionality without internet connectivity
Multi-Language Support: English, Chinese, Malay, and Tamil interfaces
Integrated Accounting: Built-in double-entry bookkeeping system
Smart Inventory Management: Predictive stock alerts and automated reordering
Customer Relationship Management: Integrated loyalty programs and customer analytics
2.4 Product Scope
In Scope:

Point-of-sale transactions
Inventory management
Customer management
Employee management
GST compliance and reporting
Financial reporting
Multi-currency transactions
Loyalty programs
Basic accounting features
Out of Scope (v1.0):

E-commerce integration
Mobile POS terminals
Advanced manufacturing features
Third-party accounting software integration
Multi-company consolidation
3. Technology Stack
3.1 Core Technologies
Programming Language
Python 3.11+: Chosen for its extensive ecosystem, excellent library support, and rapid development capabilities
Type Hints: Comprehensive type annotations throughout the codebase for improved maintainability
User Interface Framework
PySide6 (Qt6): Modern, cross-platform UI framework providing native look and feel
Qt Designer: For rapid UI prototyping and development
QML: For advanced, animated UI components where needed
Database
PostgreSQL 15+: Enterprise-grade relational database with excellent performance and reliability
SQLAlchemy 2.0+: Modern ORM with async support
Alembic: Database migration management
Asynchronous Programming
asyncio: Python's native async/await implementation
aiohttp: For async HTTP operations
asyncpg: High-performance async PostgreSQL driver
3.2 Supporting Technologies
Development Tools
Poetry: Dependency management and packaging
Black: Code formatting
Ruff: Fast Python linter
mypy: Static type checking
pre-commit: Git hooks for code quality
Testing
pytest: Test framework
pytest-asyncio: Async test support
pytest-qt: Qt/PySide6 testing
coverage.py: Code coverage analysis
factory_boy: Test data generation
Documentation
Sphinx: Documentation generation
autodoc: API documentation from docstrings
PlantUML: Architecture and sequence diagrams
Monitoring & Logging
structlog: Structured logging
Sentry: Error tracking and monitoring
Prometheus: Metrics collection
Grafana: Metrics visualization
3.3 Third-Party Integrations
Payment Processing
NETS: Singapore's national payment gateway
PayNow: QR code-based payments
Stripe: Credit card processing
Hardware Support
python-escpos: Receipt printer support
pyserial: Barcode scanner and cash drawer integration
pyzbar: QR code scanning
Reporting
ReportLab: PDF generation
openpyxl: Excel report generation
matplotlib: Chart generation
4. System Architecture
4.1 Architecture Overview
The SG POS system follows a clean, layered architecture pattern with clear separation of concerns:

┌─────────────────────────────────────────────────────────────────┐
│                     Presentation Layer                          │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────┐   │
│  │   Qt/PySide6 │  │   Widgets    │  │   View Models     │   │
│  │   Windows    │  │   Dialogs    │  │   Controllers     │   │
│  └──────────────┘  └──────────────┘  └───────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Business Logic Layer                         │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────┐   │
│  │   Managers   │  │   Services   │  │   Validators      │   │
│  │   (Core)     │  │   (Domain)   │  │   (Rules)         │   │
│  └──────────────┘  └──────────────┘  └───────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Data Access Layer                            │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────┐   │
│  │ Repositories │  │    DTOs      │  │   Query Objects   │   │
│  │              │  │              │  │                   │   │
│  └──────────────┘  └──────────────┘  └───────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                     Persistence Layer                           │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────┐   │
│  │  SQLAlchemy  │  │  PostgreSQL  │  │   Migrations      │   │
│  │   Models     │  │   Database   │  │   (Alembic)       │   │
│  └──────────────┘  └──────────────┘  └───────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
4.2 Core Design Patterns
Dependency Injection
The ApplicationCore class serves as the central dependency injection container:

class ApplicationCore:
    """Central dependency injection container using lazy initialization"""
    
    def __init__(self, config: Config):
        self._config = config
        self._db_engine = None
        self._session_factory = None
        # Manager instances cached after first access
        self._customer_manager = None
        self._inventory_manager = None
        # ... other managers
    
    @property
    def customer_manager(self) -> CustomerManager:
        if self._customer_manager is None:
            self._customer_manager = CustomerManager(self)
        return self._customer_manager

Repository Pattern
All data access is abstracted through repository interfaces:

class CustomerRepository(BaseRepository[Customer]):
    """Repository for customer data access"""
    
    async def find_by_phone(self, phone: str) -> Optional[Customer]:
        """Find customer by phone number"""
        ...
    
    async def search(self, query: str, limit: int = 50) -> List[Customer]:
        """Search customers by name or phone"""
        ...

Result Pattern
All business operations return Result objects for explicit error handling:

@dataclass
class Result(Generic[T]):
    """Result container for operation outcomes"""
    success: bool
    value: Optional[T] = None
    error: Optional[str] = None
    error_code: Optional[str] = None
    
    @classmethod
    def ok(cls, value: T) -> "Result[T]":
        return cls(success=True, value=value)
    
    @classmethod
    def fail(cls, error: str, error_code: Optional[str] = None) -> "Result[T]":
        return cls(success=False, error=error, error_code=error_code)

4.3 Asynchronous Architecture
The application uses a dual-thread model:

Main Thread: Qt event loop for UI responsiveness
Worker Thread: asyncio event loop for all I/O operations
# Bridge function for Qt → asyncio communication
def schedule_task_from_qt(coro, callback=None):
    """Schedule async task from Qt thread"""
    future = asyncio.run_coroutine_threadsafe(coro, worker_loop)
    if callback:
        future.add_done_callback(
            lambda f: QMetaObject.invokeMethod(
                callback[0], callback[1], Qt.QueuedConnection, 
                Q_ARG(object, f.result())
            )
        )
    return future

5. Database Schema Design
5.1 Schema Overview
The database schema is designed with the following principles:

Normalization: 3NF to minimize redundancy
Integrity: Comprehensive constraints and triggers
Performance: Strategic indexing and partitioning
Audit Trail: Complete history tracking for compliance
5.2 Core Tables
Company and Configuration
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    uen VARCHAR(20) UNIQUE NOT NULL, -- Singapore UEN
    gst_reg_no VARCHAR(20),
    address TEXT NOT NULL,
    phone VARCHAR(20),
    email VARCHAR(255),
    fiscal_year_start DATE NOT NULL,
    base_currency CHAR(3) NOT NULL DEFAULT 'SGD',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE branches (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(20) NOT NULL,
    name VARCHAR(255) NOT NULL,
    address TEXT NOT NULL,
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

User Management
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
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

CREATE TABLE user_permissions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    permission VARCHAR(100) NOT NULL,
    granted_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    granted_by UUID REFERENCES users(id),
    UNIQUE(user_id, permission)
);

Product Catalog
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    parent_id UUID REFERENCES categories(id),
    display_order INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id UUID REFERENCES categories(id),
    unit_of_measure VARCHAR(20) NOT NULL DEFAULT 'EACH',
    cost_price DECIMAL(19, 4) NOT NULL DEFAULT 0,
    selling_price DECIMAL(19, 4) NOT NULL,
    tax_code VARCHAR(20) NOT NULL DEFAULT 'SR', -- GST tax code
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID NOT NULL REFERENCES products(id),
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    attributes JSONB NOT NULL DEFAULT '{}',
    cost_price DECIMAL(19, 4) NOT NULL,
    selling_price DECIMAL(19, 4) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Inventory Management
CREATE TABLE inventory_locations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    branch_id UUID NOT NULL REFERENCES branches(id),
    code VARCHAR(20) NOT NULL,
    name VARCHAR(255) NOT NULL,
    type VARCHAR(50) NOT NULL, -- WAREHOUSE, STORE_FRONT, etc.
    is_active BOOLEAN DEFAULT true,
    UNIQUE(branch_id, code)
);

CREATE TABLE inventory_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    location_id UUID NOT NULL REFERENCES inventory_locations(id),
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity DECIMAL(19, 4) NOT NULL DEFAULT 0,
    reserved_quantity DECIMAL(19, 4) NOT NULL DEFAULT 0,
    last_counted_at TIMESTAMP WITH TIME ZONE,
    last_count_quantity DECIMAL(19, 4),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(location_id, COALESCE(product_id, variant_id)),
    CHECK (
        (product_id IS NOT NULL AND variant_id IS NULL) OR
        (product_id IS NULL AND variant_id IS NOT NULL)
    )
);

CREATE TABLE inventory_movements (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    movement_type VARCHAR(50) NOT NULL, -- PURCHASE, SALE, TRANSFER, ADJUSTMENT
    reference_type VARCHAR(50),
    reference_id UUID,
    from_location_id UUID REFERENCES inventory_locations(id),
    to_location_id UUID REFERENCES inventory_locations(id),
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity DECIMAL(19, 4) NOT NULL,
    unit_cost DECIMAL(19, 4),
    total_cost DECIMAL(19, 4),
    notes TEXT,
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Customer Management
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    customer_type VARCHAR(50) DEFAULT 'RETAIL',
    tax_registration_no VARCHAR(50),
    credit_limit DECIMAL(19, 4) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0, -- days
    loyalty_points INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE customer_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id UUID NOT NULL REFERENCES customers(id),
    transaction_type VARCHAR(50) NOT NULL, -- PURCHASE, PAYMENT, REFUND
    reference_type VARCHAR(50),
    reference_id UUID,
    amount DECIMAL(19, 4) NOT NULL,
    points_earned INTEGER DEFAULT 0,
    points_redeemed INTEGER DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Sales Transactions
CREATE TABLE sales_orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    order_no VARCHAR(50) UNIQUE NOT NULL,
    branch_id UUID NOT NULL REFERENCES branches(id),
    customer_id UUID REFERENCES customers(id),
    order_date DATE NOT NULL,
    order_time TIME NOT NULL,
    subtotal DECIMAL(19, 4) NOT NULL,
    tax_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    discount_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    total_amount DECIMAL(19, 4) NOT NULL,
    currency CHAR(3) NOT NULL DEFAULT 'SGD',
    exchange_rate DECIMAL(19, 6) NOT NULL DEFAULT 1,
    status VARCHAR(50) NOT NULL DEFAULT 'COMPLETED',
    cashier_id UUID NOT NULL REFERENCES users(id),
    terminal_id VARCHAR(50),
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE sales_order_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    order_id UUID NOT NULL REFERENCES sales_orders(id),
    line_no INTEGER NOT NULL,
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    description VARCHAR(255) NOT NULL,
    quantity DECIMAL(19, 4) NOT NULL,
    unit_price DECIMAL(19, 4) NOT NULL,
    discount_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    tax_code VARCHAR(20) NOT NULL,
    tax_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    line_total DECIMAL(19, 4) NOT NULL,
    cost_price DECIMAL(19, 4),
    UNIQUE(order_id, line_no)
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    payment_no VARCHAR(50) UNIQUE NOT NULL,
    order_id UUID REFERENCES sales_orders(id),
    payment_date DATE NOT NULL,
    payment_method VARCHAR(50) NOT NULL, -- CASH, CARD, NETS, PAYNOW
    amount DECIMAL(19, 4) NOT NULL,
    currency CHAR(3) NOT NULL DEFAULT 'SGD',
    exchange_rate DECIMAL(19, 6) NOT NULL DEFAULT 1,
    reference_no VARCHAR(100),
    card_last_four VARCHAR(4),
    status VARCHAR(50) NOT NULL DEFAULT 'COMPLETED',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL, -- ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE
    parent_id UUID REFERENCES chart_of_accounts(id),
    is_system_account BOOLEAN DEFAULT false,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entry_no VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT NOT NULL,
    reference_type VARCHAR(50),
    reference_id UUID,
    status VARCHAR(50) NOT NULL DEFAULT 'POSTED',
    created_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    posted_at TIMESTAMP WITH TIME ZONE
);

CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entry_id UUID NOT NULL REFERENCES journal_entries(id),
    line_no INTEGER NOT NULL,
    account_id UUID NOT NULL REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    credit_amount DECIMAL(19, 4) NOT NULL DEFAULT 0,
    description TEXT,
    UNIQUE(entry_id, line_no),
    CHECK (
        (debit_amount > 0 AND credit_amount = 0) OR
        (debit_amount = 0 AND credit_amount > 0)
    )
);

5.3 Database Indexes
-- Performance indexes
CREATE INDEX idx_products_category ON products(category_id) WHERE is_active = true;
CREATE INDEX idx_products_barcode ON products(barcode) WHERE barcode IS NOT NULL;
CREATE INDEX idx_inventory_product ON inventory_items(product_id) WHERE product_id IS NOT NULL;
CREATE INDEX idx_inventory_variant ON inventory_items(variant_id) WHERE variant_id IS NOT NULL;
CREATE INDEX idx_sales_orders_date ON sales_orders(order_date DESC);
CREATE INDEX idx_sales_orders_customer ON sales_orders(customer_id) WHERE customer_id IS NOT NULL;
CREATE INDEX idx_payments_date ON payments(payment_date DESC);
CREATE INDEX idx_journal_entries_date ON journal_entries(entry_date DESC);

-- Text search indexes
CREATE INDEX idx_products_name_search ON products USING gin(to_tsvector('english', name));
CREATE INDEX idx_customers_name_search ON customers USING gin(to_tsvector('english', name));

5.4 Database Triggers
-- Auto-update timestamps
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_products_updated_at BEFORE UPDATE ON products
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

-- Inventory movement tracking
CREATE OR REPLACE FUNCTION track_inventory_movement()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'UPDATE' THEN
        IF NEW.quantity != OLD.quantity THEN
            INSERT INTO inventory_movements (
                movement_type, from_location_id, product_id, variant_id,
                quantity, created_by
            ) VALUES (
                'ADJUSTMENT', NEW.location_id, NEW.product_id, NEW.variant_id,
                NEW.quantity - OLD.quantity, current_setting('app.current_user_id')::uuid
            );
        END IF;
    END IF;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER track_inventory_changes AFTER UPDATE ON inventory_items
    FOR EACH ROW EXECUTE FUNCTION track_inventory_movement();

6. Codebase Structure and File Hierarchy
6.1 Project Root Structure
sg-pos-system/
├── app/                          # Main application code
│   ├── __init__.py
│   ├── main.py                   # Application entry point
│   ├── config.py                 # Configuration management
│   ├── core/                     # Core application components
│   ├── business_logic/           # Business logic layer
│   ├── services/                 # Data access layer
│   ├── models/                   # Database models
│   ├── ui/                       # User interface layer
│   ├── utils/                    # Utility functions
│   └── resources/                # Static resources
├── tests/                        # Test suite
│   ├── unit/
│   ├── integration/
│   ├── e2e/
│   └── fixtures/
├── scripts/                      # Utility scripts
│   ├── setup_db.py
│   ├── seed_data.py
│   └── migrations/
├── docs/                         # Documentation
│   ├── api/
│   ├── user_guide/
│   └── deployment/
├── deployment/                   # Deployment configurations
│   ├── docker/
│   ├── kubernetes/
│   └── ansible/
├── .env.example                  # Environment variables template
├── pyproject.toml                # Poetry configuration
├── alembic.ini                   # Database migration config
└── README.md
6.2 Application Core Structure
app/core/
├── __init__.py
├── application.py                # ApplicationCore class
├── dependency_injection.py       # DI container implementation
├── events.py                     # Event bus system
├── result.py                     # Result pattern implementation
├── exceptions.py                 # Custom exceptions
├── decorators.py                 # Common decorators
└── constants.py                  # Application constants
6.3 Business Logic Layer
app/business_logic/
├── __init__.py
├── managers/
│   ├── __init__.py
│   ├── base_manager.py           # Base manager class
│   ├── auth_manager.py           # Authentication logic
│   ├── customer_manager.py       # Customer operations
│   ├── inventory_manager.py      # Inventory management
│   ├── sales_manager.py          # Sales transactions
│   ├── payment_manager.py        # Payment processing
│   ├── reporting_manager.py      # Report generation
│   └── accounting_manager.py     # Accounting operations
├── validators/
│   ├── __init__.py
│   ├── base_validator.py
│   ├── customer_validator.py
│   ├── product_validator.py
│   └── transaction_validator.py
├── calculators/
│   ├── __init__.py
│   ├── gst_calculator.py         # GST calculations
│   ├── discount_calculator.py
│   └── loyalty_calculator.py
└── workflows/
    ├── __init__.py
    ├── checkout_workflow.py
    ├── refund_workflow.py
    └── stocktake_workflow.py
6.4 Services Layer
app/services/
├── __init__.py
├── repositories/
│   ├── __init__.py
│   ├── base_repository.py        # Generic repository base
│   ├── customer_repository.py
│   ├── product_repository.py
│   ├── order_repository.py
│   ├── inventory_repository.py
│   └── accounting_repository.py
├── external/
│   ├── __init__.py
│   ├── payment_gateway.py        # Payment integrations
│   ├── email_service.py
│   ├── sms_service.py
│   └── tax_service.py            # IRAS integration
└── cache/
    ├── __init__.py
    ├── cache_manager.py
    └── cache_keys.py
6.5 Models Layer
app/models/
├── __init__.py
├── base.py                       # SQLAlchemy base configuration
├── company.py                    # Company and branch models
├── user.py                       # User and permission models
├── customer.py                   # Customer models
├── product.py                    # Product and category models
├── inventory.py                  # Inventory models
├── sales.py                      # Sales order models
├── payment.py                    # Payment models
├── accounting.py                 # Accounting models
└── audit.py                      # Audit trail models
6.6 User Interface Layer
app/ui/
├── __init__.py
├── main_window.py                # Main application window
├── styles/
│   ├── __init__.py
│   ├── theme.py                  # Application theme
│   └── styles.qss                # Qt stylesheets
├── widgets/
│   ├── __init__.py
│   ├── base_widget.py            # Base widget class
│   ├── pos/
│   │   ├── __init__.py
│   │   ├── pos_widget.py         # Main POS interface
│   │   ├── product_grid.py       # Product selection
│   │   ├── cart_widget.py        # Shopping cart
│   │   └── payment_dialog.py     # Payment processing
│   ├── inventory/
│   │   ├── __init__.py
│   │   ├── inventory_widget.py
│   │   ├── stock_adjustment.py
│   │   └── purchase_order.py
│   ├── customers/
│   │   ├── __init__.py
│   │   ├── customer_list.py
│   │   ├── customer_details.py
│   │   └── loyalty_program.py
│   ├── reports/
│   │   ├── __init__.py
│   │   ├── reports_widget.py
│   │   ├── sales_report.py
│   │   ├── inventory_report.py
│   │   └── gst_report.py
│   └── admin/
│       ├── __init__.py
│       ├── settings_widget.py
│       ├── user_management.py
│       └── system_config.py
├── dialogs/
│   ├── __init__.py
│   ├── base_dialog.py
│   ├── confirm_dialog.py
│   ├── error_dialog.py
│   └── search_dialog.py
└── view_models/
    ├── __init__.py
    ├── base_view_model.py
    ├── pos_view_model.py
    ├── inventory_view_model.py
    └── customer_view_model.py
6.7 Utilities
app/utils/
├── __init__.py
├── async_utils.py                # Async helper functions
├── date_utils.py                 # Date/time utilities
├── money_utils.py                # Currency formatting
├── validation_utils.py           # Input validation
├── encryption_utils.py           # Data encryption
├── barcode_utils.py              # Barcode generation/scanning
├── pdf_utils.py                  # PDF generation
└── excel_utils.py                # Excel operations
7. Core Application Modules
7.1 ApplicationCore Module
The ApplicationCore serves as the central nervous system of the application, implementing dependency injection and managing the lifecycle of all major components.

# app/core/application.py
from typing import Optional, Dict, Any
import asyncio
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
from sqlalchemy.orm import sessionmaker

class ApplicationCore:
    """
    Central application core implementing lazy-loaded dependency injection.
    All managers and services are instantiated on first access.
    """
    
    def __init__(self, config: Config):
        self.config = config
        self._engine = None
        self._session_factory = None
        self._event_bus = EventBus()
        
        # Manager cache
        self._managers: Dict[str, Any] = {}
        
        # Service cache
        self._services: Dict[str, Any] = {}
        
    async def initialize(self):
        """Initialize core components"""
        # Setup database
        self._engine = create_async_engine(
            self.config.database_url,
            echo=self.config.debug,
            pool_size=20,
            max_overflow=40
        )
        
        self._session_factory = sessionmaker(
            self._engine,
            class_=AsyncSession,
            expire_on_commit=False
        )
        
        # Initialize event handlers
        self._setup_event_handlers()
        
    @property
    def customer_manager(self) -> CustomerManager:
        """Lazy-loaded customer manager"""
        if 'customer' not in self._managers:
            self._managers['customer'] = CustomerManager(self)
        return self._managers['customer']
    
    @property
    def inventory_manager(self) -> InventoryManager:
        """Lazy-loaded inventory manager"""
        if 'inventory' not in self._managers:
            self._managers['inventory'] = InventoryManager(self)
        return self._managers['inventory']
    
    @property
    def sales_manager(self) -> SalesManager:
        """Lazy-loaded sales manager"""
        if 'sales' not in self._managers:
            self._managers['sales'] = SalesManager(self)
        return self._managers['sales']
    
    async def get_session(self) -> AsyncSession:
        """Get database session"""
        return self._session_factory()
    
    def publish_event(self, event: Event):
        """Publish event to event bus"""
        self._event_bus.publish(event)

7.2 Business Logic Managers
Sales Manager
Handles all sales-related operations including order creation, payment processing, and refunds.

# app/business_logic/managers/sales_manager.py
from typing import List, Optional
from decimal import Decimal
from app.core.result import Result
from app.models.sales import SalesOrder, SalesOrderItem

class SalesManager:
    """Manages sales transactions and order processing"""
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
        self._order_repo = None
        self._payment_processor = None
        
    @property
    def order_repository(self) -> OrderRepository:
        if self._order_repo is None:
            self._order_repo = OrderRepository(self.app_core)
        return self._order_repo
    
    async def create_order(
        self,
        items: List[Dict],
        customer_id: Optional[UUID] = None,
        payment_method: str = "CASH"
    ) -> Result[SalesOrder]:
        """
        Create a new sales order with full transaction handling
        """
        async with self.app_core.get_session() as session:
            try:
                # Begin transaction
                async with session.begin():
                    # Validate inventory availability
                    availability_check = await self._check_inventory_availability(
                        session, items
                    )
                    if not availability_check.success:
                        return availability_check
                    
                    # Calculate order totals
                    calculation_result = await self._calculate_order_totals(
                        session, items, customer_id
                    )
                    if not calculation_result.success:
                        return calculation_result
                    
                    totals = calculation_result.value
                    
                    # Create order
                    order = SalesOrder(
                        order_no=await self._generate_order_number(),
                        branch_id=self.app_core.current_branch_id,
                        customer_id=customer_id,
                        subtotal=totals['subtotal'],
                        tax_amount=totals['tax_amount'],
                        discount_amount=totals['discount_amount'],
                        total_amount=totals['total_amount'],
                        cashier_id=self.app_core.current_user_id,
                        terminal_id=self.app_core.terminal_id
                    )
                    
                    # Add order items
                    for idx, item in enumerate(items):
                        order_item = SalesOrderItem(
                            line_no=idx + 1,
                            product_id=item['product_id'],
                            quantity=item['quantity'],
                            unit_price=item['unit_price'],
                            discount_amount=item.get('discount', 0),
                            tax_code=item['tax_code'],
                            tax_amount=item['tax_amount'],
                            line_total=item['line_total']
                        )
                        order.items.append(order_item)
                    
                    # Save order
                    session.add(order)
                    await session.flush()
                    
                    # Process payment
                    payment_result = await self._process_payment(
                        session, order, payment_method
                    )
                    if not payment_result.success:
                        await session.rollback()
                        return payment_result
                    
                    # Update inventory
                    inventory_result = await self._update_inventory(
                        session, order
                    )
                    if not inventory_result.success:
                        await session.rollback()
                        return inventory_result
                    
                    # Update customer loyalty points
                    if customer_id:
                        await self._update_loyalty_points(
                            session, customer_id, order.total_amount
                        )
                    
                    # Create accounting entries
                    await self._create_accounting_entries(session, order)
                    
                    # Commit transaction
                    await session.commit()
                    
                    # Publish event
                    self.app_core.publish_event(
                        OrderCreatedEvent(order_id=order.id)
                    )
                    
                    return Result.ok(order)
                    
            except Exception as e:
                logger.error(f"Error creating order: {str(e)}")
                return Result.fail(
                    "Failed to create order",
                    error_code="ORDER_CREATION_FAILED"
                )

Inventory Manager
Manages stock levels, transfers, and inventory tracking.

# app/business_logic/managers/inventory_manager.py
class InventoryManager:
    """Manages inventory operations and stock control"""
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
        
    async def check_availability(
        self,
        product_id: UUID,
        quantity: Decimal,
        location_id: Optional[UUID] = None
    ) -> Result[bool]:
        """Check if product quantity is available"""
        async with self.app_core.get_session() as session:
            repo = InventoryRepository(session)
            
            if location_id is None:
                location_id = self.app_core.current_location_id
            
            available = await repo.get_available_quantity(
                product_id, location_id
            )
            
            if available >= quantity:
                return Result.ok(True)
            else:
                return Result.fail(
                    f"Insufficient stock. Available: {available}",
                    error_code="INSUFFICIENT_STOCK"
                )
    
    async def perform_stock_adjustment(
        self,
        adjustments: List[StockAdjustmentDTO],
        reason: str,
        notes: Optional[str] = None
    ) -> Result[StockAdjustment]:
        """Perform stock adjustment with full audit trail"""
        async with self.app_core.get_session() as session:
            try:
                async with session.begin():
                    adjustment = StockAdjustment(
                        adjustment_no=await self._generate_adjustment_number(),
                        reason=reason,
                        notes=notes,
                        created_by=self.app_core.current_user_id
                    )
                    
                    for item in adjustments:
                        # Get current stock level
                        current = await self._get_current_stock(
                            session, item.product_id, item.location_id
                        )
                        
                        # Create adjustment line
                        line = StockAdjustmentLine(
                            product_id=item.product_id,
                            location_id=item.location_id,
                            old_quantity=current,
                            new_quantity=item.new_quantity,
                            difference=item.new_quantity - current,
                            cost=item.cost
                        )
                        adjustment.lines.append(line)
                        
                        # Update inventory
                        await self._update_stock_level(
                            session,
                            item.product_id,
                            item.location_id,
                            item.new_quantity
                        )
                        
                        # Create inventory movement
                        await self._create_movement(
                            session,
                            movement_type="ADJUSTMENT",
                            product_id=item.product_id,
                            location_id=item.location_id,
                            quantity=item.new_quantity - current,
                            reference=adjustment
                        )
                    
                    session.add(adjustment)
                    await session.commit()
                    
                    # Publish event
                    self.app_core.publish_event(
                        StockAdjustedEvent(adjustment_id=adjustment.id)
                    )
                    
                    return Result.ok(adjustment)
                    
            except Exception as e:
                logger.error(f"Stock adjustment failed: {str(e)}")
                return Result.fail("Stock adjustment failed")

7.3 Data Transfer Objects (DTOs)
DTOs provide a clean interface between layers and ensure data integrity.

# app/services/dtos/sales_dto.py
from dataclasses import dataclass
from typing import List, Optional
from decimal import Decimal
from datetime import datetime
from uuid import UUID

@dataclass(frozen=True)
class OrderItemDTO:
    """Immutable order item data transfer object"""
    product_id: UUID
    quantity: Decimal
    unit_price: Decimal
    discount_amount: Decimal = Decimal('0')
    tax_code: str = 'SR'
    
    @property
    def subtotal(self) -> Decimal:
        return self.quantity * self.unit_price
    
    @property
    def discounted_amount(self) -> Decimal:
        return self.subtotal - self.discount_amount
    
    def validate(self) -> Result[bool]:
        """Validate order item data"""
        if self.quantity <= 0:
            return Result.fail("Quantity must be positive")
        if self.unit_price < 0:
            return Result.fail("Unit price cannot be negative")
        if self.discount_amount > self.subtotal:
            return Result.fail("Discount cannot exceed subtotal")
        return Result.ok(True)

@dataclass(frozen=True)
class CreateOrderDTO:
    """DTO for order creation"""
    items: List[OrderItemDTO]
    customer_id: Optional[UUID] = None
    payment_method: str = "CASH"
    payment_amount: Optional[Decimal] = None
    notes: Optional[str] = None
    
    def validate(self) -> Result[bool]:
        """Validate order data"""
        if not self.items:
            return Result.fail("Order must contain at least one item")
        
        for item in self.items:
            validation = item.validate()
            if not validation.success:
                return validation
        
        if self.payment_amount and self.payment_amount < 0:
            return Result.fail("Payment amount cannot be negative")
            
        return Result.ok(True)

7.4 Repository Pattern Implementation
# app/services/repositories/base_repository.py
from typing import TypeVar, Generic, List, Optional
from sqlalchemy.ext.asyncio import AsyncSession
from sqlalchemy import select, update, delete
from uuid import UUID

T = TypeVar('T')

class BaseRepository(Generic[T]):
    """Generic repository base class"""
    
    def __init__(self, session: AsyncSession, model_class: Type[T]):
        self.session = session
        self.model_class = model_class
    
    async def get_by_id(self, id: UUID) -> Optional[T]:
        """Get entity by ID"""
        result = await self.session.execute(
            select(self.model_class).where(self.model_class.id == id)
        )
        return result.scalar_one_or_none()
    
    async def get_all(
        self,
        skip: int = 0,
        limit: int = 100,
        **filters
    ) -> List[T]:
        """Get all entities with pagination"""
        query = select(self.model_class)
        
        # Apply filters
        for key, value in filters.items():
            if hasattr(self.model_class, key):
                query = query.where(
                    getattr(self.model_class, key) == value
                )
        
        query = query.offset(skip).limit(limit)
        result = await self.session.execute(query)
        return result.scalars().all()
    
    async def create(self, **kwargs) -> T:
        """Create new entity"""
        entity = self.model_class(**kwargs)
        self.session.add(entity)
        await self.session.flush()
        return entity
    
    async def update(self, id: UUID, **kwargs) -> Optional[T]:
        """Update entity"""
        entity = await self.get_by_id(id)
        if entity:
            for key, value in kwargs.items():
                setattr(entity, key, value)
            await self.session.flush()
        return entity
    
    async def delete(self, id: UUID) -> bool:
        """Delete entity"""
        result = await self.session.execute(
            delete(self.model_class).where(self.model_class.id == id)
        )
        return result.rowcount > 0

7.5 UI Components
Main POS Widget
The primary point-of-sale interface for cashiers.

# app/ui/widgets/pos/pos_widget.py
from PySide6.QtWidgets import *
from PySide6.QtCore import *
from typing import Optional
from decimal import Decimal

class POSWidget(QWidget):
    """Main point-of-sale interface"""
    
    def __init__(self, app_core: ApplicationCore, parent=None):
        super().__init__(parent)
        self.app_core = app_core
        self.current_order_items = []
        self.selected_customer = None
        
        self._setup_ui()
        self._connect_signals()
    
    def _setup_ui(self):
        """Initialize UI components"""
        layout = QHBoxLayout(self)
        
        # Left panel - Product selection
        left_panel = QWidget()
        left_layout = QVBoxLayout(left_panel)
        
        # Search bar
        self.search_input = QLineEdit()
        self.search_input.setPlaceholderText("Search products...")
        left_layout.addWidget(self.search_input)
        
        # Category tabs
        self.category_tabs = QTabWidget()
        left_layout.addWidget(self.category_tabs)
        
        # Product grid
        self.product_grid = ProductGrid(self.app_core)
        left_layout.addWidget(self.product_grid)
        
        # Right panel - Cart and payment
        right_panel = QWidget()
        right_layout = QVBoxLayout(right_panel)
        
        # Customer selection
        customer_widget = QWidget()
        customer_layout = QHBoxLayout(customer_widget)
        self.customer_label = QLabel("Walk-in Customer")
        self.select_customer_btn = QPushButton("Select Customer")
        customer_layout.addWidget(self.customer_label)
        customer_layout.addWidget(self.select_customer_btn)
        right_layout.addWidget(customer_widget)
        
        # Cart widget
        self.cart_widget = CartWidget(self.app_core)
        right_layout.addWidget(self.cart_widget)
        
        # Payment buttons
        payment_widget = QWidget()
        payment_layout = QGridLayout(payment_widget)
        
        self.cash_btn = QPushButton("Cash")
        self.card_btn = QPushButton("Card")
        self.nets_btn = QPushButton("NETS")
        self.paynow_btn = QPushButton("PayNow")
        
        payment_layout.addWidget(self.cash_btn, 0, 0)
        payment_layout.addWidget(self.card_btn, 0, 1)
        payment_layout.addWidget(self.nets_btn, 1, 0)
        payment_layout.addWidget(self.paynow_btn, 1, 1)
        
        right_layout.addWidget(payment_widget)
        
        # Add panels to main layout
        splitter = QSplitter(Qt.Horizontal)
        splitter.addWidget(left_panel)
        splitter.addWidget(right_panel)
        splitter.setStretchFactor(0, 2)
        splitter.setStretchFactor(1, 1)
        
        layout.addWidget(splitter)
    
    def _connect_signals(self):
        """Connect UI signals"""
        self.search_input.textChanged.connect(self._on_search_changed)
        self.select_customer_btn.clicked.connect(self._select_customer)
        self.product_grid.product_selected.connect(self._add_to_cart)
        self.cash_btn.clicked.connect(lambda: self._process_payment("CASH"))
        self.card_btn.clicked.connect(lambda: self._process_payment("CARD"))
        self.nets_btn.clicked.connect(lambda: 
