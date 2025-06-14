This is a comprehensive request for a detailed Product Requirements Document (PRD) for a Singapore Point-of-Sale system. I need to create a well-structured, thorough document that covers all aspects of the system design, architecture, and implementation details.
Let me break down what I need to include:

Executive Summary and Product Overview
Technology Stack detailed explanation
System Architecture (layered architecture as described)
Database Schema Design (comprehensive POS database)
Codebase File Hierarchy (showing the layered structure)
Application Modules and User Interaction Diagrams
Key Features and Functionality
Singapore-specific regulatory requirements
Development and Production environment setup
Security, performance, and testing considerations
The user has provided detailed architectural considerations that show they want:

Layered architecture with clear separation of concerns
Dependency injection with ApplicationCore
Asynchronous processing model
High-quality code patterns (DTOs, Result pattern)
Multi-currency support
Singapore regulatory compliance
I need to ensure this PRD is comprehensive, detailed, and leaves no ambiguity for implementation. The target is at least 6000 words, so I need to be thorough in each section.

Let me structure this systematically, starting with the executive summary and working through each major section. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Product Overview
Technology Stack
System Architecture
Database Schema Design
Codebase Structure & File Hierarchy
Core Application Modules
User Interface Design
Key Features & Functionality
Singapore Regulatory Compliance
Development Environment Setup
Production Environment Setup
Security Considerations
Performance Requirements
Testing Strategy
Deployment Strategy
Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail operational needs of small to medium-sized businesses (SMBs) in Singapore. This professional-grade retail management solution combines modern Python development practices with robust data management to deliver a scalable, maintainable, and regulation-compliant business tool.

Built on a foundation of Python 3.11+, PySide6 for the user interface, and PostgreSQL for data persistence, the system implements a clean layered architecture that ensures separation of concerns, maintainability, and extensibility. The application addresses the unique requirements of Singapore's business environment, including GST compliance, multi-currency support, and local regulatory adherence.

The system is architected to handle real-world business complexity through sophisticated design patterns including Dependency Injection, Data Transfer Objects (DTOs), the Result pattern, and asynchronous processing models. This ensures that the application can scale with business growth while maintaining performance and reliability.

Key differentiators include comprehensive inventory management, advanced reporting capabilities, multi-user support with role-based access control, and seamless integration capabilities for future expansion. The application's design prioritizes user experience while maintaining the robustness required for mission-critical business operations.

Product Overview
Target Market
The SG POS System targets small to medium-sized businesses in Singapore's retail sector, including:

Specialty retail stores
Convenience stores
Electronics retailers
Fashion and apparel shops
Bookstores and stationery shops
Hardware and home improvement stores
Gift shops and souvenir stores
Core Value Proposition
The system delivers comprehensive retail management capabilities through a single, integrated platform that addresses the complete sales cycle from inventory management to financial reporting. Key value propositions include:

Operational Efficiency: Streamlined workflows that reduce manual processes and minimize errors in day-to-day operations.

Regulatory Compliance: Built-in Singapore GST handling, proper tax reporting, and audit trail maintenance that ensures compliance with local regulations.

Business Intelligence: Advanced reporting and analytics capabilities that provide actionable insights for inventory optimization, sales performance, and customer behavior analysis.

Scalability: Architected to grow with the business, supporting multiple users, locations, and increasing transaction volumes without performance degradation.

Cost Effectiveness: Eliminates the need for multiple disparate systems by providing comprehensive functionality in a single application, reducing total cost of ownership.

Key Business Objectives
Streamline Sales Operations: Reduce transaction processing time and improve customer checkout experience
Enhance Inventory Control: Provide real-time inventory visibility and automated reorder management
Ensure Regulatory Compliance: Maintain accurate GST records and generate required regulatory reports
Improve Decision Making: Deliver comprehensive analytics and reporting for data-driven business decisions
Reduce Operational Costs: Minimize manual processes and reduce the need for multiple software solutions
Technology Stack
Core Technologies
Python 3.11+ The foundation programming language chosen for its excellent ecosystem, maintainability, and rapid development capabilities. Python's extensive library ecosystem and strong typing support (through type hints) enable robust, maintainable code development.

PySide6 (Qt6) The primary GUI framework providing cross-platform desktop application capabilities. PySide6 offers:

Native look and feel across Windows, macOS, and Linux
Comprehensive widget library for professional applications
Advanced styling capabilities through Qt StyleSheets
Robust event handling and signal-slot architecture
High-performance graphics and rendering capabilities
PostgreSQL 15+ The primary database management system chosen for its:

ACID compliance ensuring data integrity
Advanced indexing and query optimization
JSON support for flexible data structures
Robust concurrent transaction handling
Excellent performance characteristics for business applications
Comprehensive backup and recovery capabilities
Data Access and ORM
SQLAlchemy 2.0+ The Object-Relational Mapping (ORM) framework providing:

Declarative model definitions
Advanced query capabilities
Connection pooling and optimization
Transaction management
Database schema migration support
Alembic Database migration management tool for:

Version-controlled schema changes
Automated migration generation
Production deployment safety
Rollback capabilities
Asynchronous Processing
asyncio Python's built-in asynchronous I/O framework for:

Non-blocking database operations
Background task processing
Improved application responsiveness
Efficient resource utilization
asyncpg High-performance PostgreSQL driver for Python providing:

Native asyncio support
Optimized binary protocol communication
Connection pooling
Prepared statement support
Development and Testing
pytest Comprehensive testing framework for:

Unit testing
Integration testing
Test fixtures and parameterization
Coverage reporting
pytest-asyncio AsyncIO testing support for testing asynchronous components.

Factory Boy Test data generation library for creating realistic test scenarios.

Black Code formatting tool ensuring consistent code style across the codebase.

mypy Static type checking to catch type-related errors during development.

Additional Libraries
pydantic Data validation and serialization for:

DTO (Data Transfer Object) implementations
API request/response validation
Configuration management
Type-safe data structures
structlog Structured logging framework providing:

JSON-formatted log output
Contextual logging information
Performance monitoring capabilities
Debugging support
cryptography Security library for:

Password hashing and verification
Data encryption/decryption
Secure token generation
Digital signature support
System Architecture
Layered Architecture Overview
The SG POS System implements a strict four-layer architecture that ensures clean separation of concerns, maintainability, and testability:

┌─────────────────────────────────────┐
│        Presentation Layer           │
│     (app/ui/, PySide6 Widgets)     │
├─────────────────────────────────────┤
│       Business Logic Layer         │
│  (app/business_logic/, Managers)    │
├─────────────────────────────────────┤
│       Data Access Layer            │
│    (app/services/, Repositories)   │
├─────────────────────────────────────┤
│       Persistence Layer            │
│   (app/models/, Database Schema)    │
└─────────────────────────────────────┘
Presentation Layer (app/ui/)
This layer contains all user interface components and is responsible for:

Rendering UI elements using PySide6 widgets
Handling user input and events
Displaying data to users
Delegating all business operations to the Business Logic Layer
Key Components:

Main application window and dialog boxes
Custom widgets for specific business functions
Qt Models for data display (QAbstractTableModel implementations)
UI controllers that coordinate between widgets and business logic
Design Principles:

No direct database access
No business logic implementation
Minimal data transformation (primarily for display purposes)
Asynchronous operation invocation through ApplicationCore
Business Logic Layer (app/business_logic/)
The core of the application's business intelligence, implementing:

Complex business workflows and rules
Transaction coordination across multiple data entities
Business validation and constraint enforcement
Integration of multiple services to complete business operations
Key Components:

Manager Classes: Orchestrate complex business operations
Domain Services: Implement specific business rules
Validators: Ensure business constraint compliance
DTOs: Transfer data between layers safely
Design Principles:

No direct database access (delegates to Data Access Layer)
No UI concerns (communicates through DTOs)
Comprehensive error handling with Result pattern
Transactional integrity through proper service coordination
Data Access Layer (app/services/)
Implements the Repository pattern to abstract database operations:

CRUD operations for all business entities
Complex query implementations
Database transaction management
Data validation and constraint enforcement
Key Components:

Service Classes: Implement repository pattern for each entity
Query Builders: Construct complex database queries
Transaction Managers: Handle database transaction boundaries
Data Mappers: Convert between ORM models and DTOs
Design Principles:

Sole point of database interaction
No business logic implementation
Efficient query optimization
Proper error handling and logging
Persistence Layer (app/models/)
Defines the data model and database schema:

SQLAlchemy ORM model definitions
Database constraints and relationships
Indexes for performance optimization
Database triggers for data integrity
Dependency Injection Architecture
The ApplicationCore class serves as the dependency injection container, implementing:

Lazy Initialization Pattern:

@property
def customer_manager(self) -> CustomerManager:
    if self._customer_manager is None:
        self._customer_manager = CustomerManager(self)
    return self._customer_manager

Unified Constructor Pattern: All manager classes implement consistent constructor signatures:

def __init__(self, app_core: "ApplicationCore"):
    self.app_core = app_core

This architecture ensures:

Loose coupling between components
Easy testing through dependency substitution
Clear dependency relationships
Simplified component initialization
Asynchronous Processing Model
The application implements a sophisticated asynchronous model:

Thread Separation:

Main thread: UI operations and user interactions
Background thread: Async event loop for I/O operations
Communication Bridge:

def schedule_task_from_qt(coro, callback=None):
    """Bridge function to execute async tasks from Qt thread"""
    future = asyncio.run_coroutine_threadsafe(coro, loop)
    if callback:
        future.add_done_callback(callback)

Benefits:

Non-blocking UI operations
Improved application responsiveness
Efficient resource utilization
Scalable concurrent processing
Database Schema Design
Core Tables
users

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL DEFAULT 'cashier',
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_login TIMESTAMP
);

customers

CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    country VARCHAR(2) DEFAULT 'SG',
    customer_type VARCHAR(20) DEFAULT 'individual',
    tax_registration_number VARCHAR(50),
    credit_limit DECIMAL(15,2) DEFAULT 0.00,
    payment_terms INTEGER DEFAULT 30,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

suppliers

CREATE TABLE suppliers (
    id SERIAL PRIMARY KEY,
    supplier_code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    contact_person VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    country VARCHAR(2) DEFAULT 'SG',
    tax_registration_number VARCHAR(50),
    payment_terms INTEGER DEFAULT 30,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

product_categories

CREATE TABLE product_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    parent_id INTEGER REFERENCES product_categories(id),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

products

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES product_categories(id),
    unit_of_measure VARCHAR(20) DEFAULT 'each',
    cost_price DECIMAL(15,4) NOT NULL DEFAULT 0.0000,
    selling_price DECIMAL(15,4) NOT NULL DEFAULT 0.0000,
    gst_rate DECIMAL(5,2) DEFAULT 0.00,
    is_taxable BOOLEAN DEFAULT true,
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    minimum_stock_level INTEGER DEFAULT 0,
    maximum_stock_level INTEGER,
    reorder_point INTEGER DEFAULT 0,
    barcode VARCHAR(100),
    weight DECIMAL(10,3),
    dimensions JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

inventory

CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER NOT NULL REFERENCES products(id),
    location VARCHAR(100) DEFAULT 'main',
    current_stock INTEGER NOT NULL DEFAULT 0,
    reserved_stock INTEGER NOT NULL DEFAULT 0,
    available_stock INTEGER GENERATED ALWAYS AS (current_stock - reserved_stock) STORED,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location)
);

sales_transactions

CREATE TABLE sales_transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    customer_id INTEGER REFERENCES customers(id),
    user_id INTEGER NOT NULL REFERENCES users(id),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    subtotal_amount DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    discount_amount DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    tax_amount DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    total_amount DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    amount_paid DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    change_amount DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    status VARCHAR(20) DEFAULT 'completed',
    payment_method VARCHAR(50),
    reference_number VARCHAR(100),
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

sales_transaction_items

CREATE TABLE sales_transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER NOT NULL REFERENCES sales_transactions(id) ON DELETE CASCADE,
    product_id INTEGER NOT NULL REFERENCES products(id),
    quantity DECIMAL(10,3) NOT NULL,
    unit_price DECIMAL(15,4) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0.00,
    tax_rate DECIMAL(5,2) DEFAULT 0.00,
    tax_amount DECIMAL(15,2) DEFAULT 0.00,
    line_total DECIMAL(15,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

payments

CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    payment_number VARCHAR(50) UNIQUE NOT NULL,
    transaction_id INTEGER REFERENCES sales_transactions(id),
    customer_id INTEGER REFERENCES customers(id),
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    amount DECIMAL(15,2) NOT NULL,
    payment_method VARCHAR(50) NOT NULL,
    reference_number VARCHAR(100),
    currency VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1.000000,
    base_amount DECIMAL(15,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'completed',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Financial Tables
chart_of_accounts

CREATE TABLE chart_of_accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL,
    parent_id INTEGER REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

journal_entries

CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT NOT NULL,
    reference_type VARCHAR(50),
    reference_id INTEGER,
    total_debit DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    total_credit DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    status VARCHAR(20) DEFAULT 'posted',
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

journal_entry_lines

CREATE TABLE journal_entry_lines (
    id SERIAL PRIMARY KEY,
    journal_entry_id INTEGER NOT NULL REFERENCES journal_entries(id) ON DELETE CASCADE,
    account_id INTEGER NOT NULL REFERENCES chart_of_accounts(id),
    description TEXT,
    debit_amount DECIMAL(15,2) DEFAULT 0.00,
    credit_amount DECIMAL(15,2) DEFAULT 0.00,
    line_order INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

GST and Tax Tables
gst_rates

CREATE TABLE gst_rates (
    id SERIAL PRIMARY KEY,
    rate_name VARCHAR(50) NOT NULL,
    rate_percentage DECIMAL(5,2) NOT NULL,
    effective_from DATE NOT NULL,
    effective_to DATE,
    is_default BOOLEAN DEFAULT false,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

gst_transactions

CREATE TABLE gst_transactions (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER NOT NULL REFERENCES sales_transactions(id),
    gst_rate_id INTEGER NOT NULL REFERENCES gst_rates(id),
    taxable_amount DECIMAL(15,2) NOT NULL,
    gst_amount DECIMAL(15,2) NOT NULL,
    transaction_type VARCHAR(20) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Configuration and System Tables
system_settings

CREATE TABLE system_settings (
    id SERIAL PRIMARY KEY,
    setting_key VARCHAR(100) UNIQUE NOT NULL,
    setting_value TEXT,
    data_type VARCHAR(20) DEFAULT 'string',
    description TEXT,
    is_user_configurable BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

currencies

CREATE TABLE currencies (
    id SERIAL PRIMARY KEY,
    currency_code VARCHAR(3) UNIQUE NOT NULL,
    currency_name VARCHAR(100) NOT NULL,
    symbol VARCHAR(10),
    is_base_currency BOOLEAN DEFAULT false,
    exchange_rate DECIMAL(10,6) DEFAULT 1.000000,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    is_active BOOLEAN DEFAULT true
);

Indexes and Constraints
-- Performance indexes
CREATE INDEX idx_sales_transactions_date ON sales_transactions(transaction_date);
CREATE INDEX idx_sales_transactions_customer ON sales_transactions(customer_id);
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_category ON products(category_id);
CREATE INDEX idx_inventory_product ON inventory(product_id);
CREATE INDEX idx_payments_date ON payments(payment_date);
CREATE INDEX idx_journal_entries_date ON journal_entries(entry_date);

-- Data integrity constraints
ALTER TABLE sales_transactions ADD CONSTRAINT chk_total_amount_positive 
    CHECK (total_amount >= 0);
ALTER TABLE payments ADD CONSTRAINT chk_payment_amount_positive 
    CHECK (amount > 0);
ALTER TABLE inventory ADD CONSTRAINT chk_stock_non_negative 
    CHECK (current_stock >= 0 AND reserved_stock >= 0);

Codebase Structure & File Hierarchy
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py          # Dependency injection container
│   │   ├── config.py                    # Configuration management
│   │   ├── exceptions.py                # Custom exception classes
│   │   ├── logging_config.py            # Logging configuration
│   │   └── result.py                    # Result pattern implementation
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                      # Base model class
│   │   ├── user.py                      # User model
│   │   ├── customer.py                  # Customer model
│   │   ├── supplier.py                  # Supplier model
│   │   ├── product.py                   # Product and category models
│   │   ├── inventory.py                 # Inventory model
│   │   ├── sales.py                     # Sales transaction models
│   │   ├── payment.py                   # Payment model
│   │   ├── accounting.py                # Chart of accounts, journal entries
│   │   ├── gst.py                       # GST-related models
│   │   └── system.py                    # System settings, currencies
│   ├── services/
│   │   ├── __init__.py
│   │   ├── base_service.py              # Base service class
│   │   ├── user_service.py              # User repository
│   │   ├── customer_service.py          # Customer repository
│   │   ├── supplier_service.py          # Supplier repository
│   │   ├── product_service.py           # Product repository
│   │   ├── inventory_service.py         # Inventory repository
│   │   ├── sales_service.py             # Sales repository
│   │   ├── payment_service.py           # Payment repository
│   │   ├── accounting_service.py        # Accounting repository
│   │   ├── gst_service.py               # GST repository
│   │   └── system_service.py            # System settings repository
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── customer_manager.py      # Customer business logic
│   │   │   ├── supplier_manager.py      # Supplier business logic
│   │   │   ├── product_manager.py       # Product business logic
│   │   │   ├── inventory_manager.py     # Inventory business logic
│   │   │   ├── sales_manager.py         # Sales business logic
│   │   │   ├── payment_manager.py       # Payment business logic
│   │   │   ├── accounting_manager.py    # Accounting business logic
│   │   │   ├── gst_manager.py           # GST business logic
│   │   │   ├── reporting_manager.py     # Reporting business logic
│   │   │   └── user_manager.py          # User management logic
│   │   ├── validators/
│   │   │   ├── __init__.py
│   │   │   ├── customer_validator.py    # Customer validation rules
│   │   │   ├── product_validator.py     # Product validation rules
│   │   │   ├── sales_validator.py       # Sales validation rules
│   │   │   └── gst_validator.py         # GST validation rules
│   │   └── dtos/
│   │       ├── __init__.py
│   │       ├── customer_dto.py          # Customer DTOs
│   │       ├── product_dto.py           # Product DTOs
│   │       ├── sales_dto.py             # Sales DTOs
│   │       ├── payment_dto.py           # Payment DTOs
│   │       └── reporting_dto.py         # Reporting DTOs
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py               # Main application window
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── customer_dialog.py       # Customer CRUD dialog
│   │   │   ├── product_dialog.py        # Product CRUD dialog
│   │   │   ├── supplier_dialog.py       # Supplier CRUD dialog
│   │   │   ├── sales_dialog.py          # Sales transaction dialog
│   │   │   ├── payment_dialog.py        # Payment processing dialog
│   │   │   ├── settings_dialog.py       # System settings dialog
│   │   │   └── about_dialog.py          # About application dialog
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── pos_widget.py            # Point of sale interface
│   │   │   ├── inventory_widget.py      # Inventory management
│   │   │   ├── customers_widget.py      # Customer management
│   │   │   ├── products_widget.py       # Product management
│   │   │   ├── suppliers_widget.py      # Supplier management
│   │   │   ├── reports_widget.py        # Reporting interface
│   │   │   ├── accounting_widget.py     # Accounting interface
│   │   │   └── dashboard_widget.py      # Dashboard overview
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── customer_table_model.py  # Customer table model
│   │   │   ├── product_table_model.py   # Product table model
│   │   │   ├── sales_table_model.py     # Sales table model
│   │   │   └── inventory_table_model.py # Inventory table model
│   │   ├── utils/
│   │   │   ├── __init__.py
│   │   │   ├── ui_helpers.py            # UI utility functions
│   │   │   ├── validators.py            # UI input validators
│   │   │   └── formatters.py            # Data formatting utilities
│   │   └── resources/
│   │       ├── icons/                   # Application icons
│   │       ├── images/                  # Images and logos
│   │       └── styles/                  # CSS stylesheets
│   └── accounting/
│       ├── __init__.py
│       ├── managers/
│       │   ├── __init__.py
│       │   ├── chart_of_accounts_manager.py  # COA management
│       │   ├── journal_entry_manager.py      # Journal entry management
│       │   └── financial_reporting_manager.py # Financial reports
│       └── engines/
│           ├── __init__.py
│           ├── journal_engine.py        # Journal posting engine
│           └── balance_engine.py        # Balance calculation engine
├── scripts/
│   ├── __init__.py
│   ├── schema.sql                       # Database schema definition
│   ├── initial_data.sql                 # Initial system data
│   ├── migrations/                      # Database migration scripts
│   ├── backup_db.py                     # Database backup utility
│   ├── restore_db.py                    # Database restore utility
│   └── setup_dev_env.py                 # Development environment setup
├── tests/
│   ├── __init__.py
│   ├── conftest.py                      # Test configuration
│   ├── fixtures/                        # Test data fixtures
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_models/                 # Model unit tests
│   │   ├── test_services/               # Service unit tests
│   │   └── test_managers/               # Manager unit tests
│   ├── integration/
│   │   ├── __init__.py
│   │   ├── test_database/               # Database integration tests
│   │   └── test_workflows/              # Business workflow tests
│   └── ui/
│       ├── __init__.py
│       └── test_widgets/                # UI widget tests
├── docs/
│   ├── api/                             # API documentation
│   ├── user_guide/                      # User documentation
│   ├── developer_guide/                 # Developer documentation
│   └── deployment/                      # Deployment documentation
├── config/
│   ├── development.env                  # Development configuration
│   ├── production.env                   # Production configuration
│   └── test.env                         # Test configuration
├── requirements/
│   ├── base.txt                         # Base requirements
│   ├── development.txt                  # Development requirements
│   ├── production.txt                   # Production requirements
│   └── test.txt                         # Test requirements
├── .env.example                         # Environment template
├── .gitignore                           # Git ignore rules
├── README.md                            # Project documentation
├── setup.py                             # Package setup
└── pyproject.toml                       # Project configuration
Core Application Modules
ApplicationCore (app/core/application_core.py)
The central dependency injection container that manages all application dependencies and provides lazy initialization of managers and services.

Key Responsibilities:

Dependency injection container
Service lifecycle management
Configuration management
Database connection management
Asynchronous task coordination
Implementation Pattern:

class ApplicationCore:
    def __init__(self):
        self._config = None
        self._database_session = None
        self._customer_manager = None
        self._product_manager = None
        # ... other managers
    
    @property
    def customer_manager(self) -> CustomerManager:
        if self._customer_manager is None:
            self._customer_manager = CustomerManager(self)
        return self._customer_manager

Manager Classes (app/business_logic/managers/)
CustomerManager
Purpose: Orchestrates all customer-related business operations Key Methods:

create_customer(customer_dto: CustomerCreateDTO) -> Result[CustomerDTO]
update_customer(id: int, customer_dto: CustomerUpdateDTO) -> Result[CustomerDTO]
get_customer_by_id(id: int) -> Result[CustomerDTO]
search_customers(criteria: CustomerSearchDTO) -> Result[List[CustomerDTO]]
validate_customer_credit_limit(customer_id: int, amount: Decimal) -> Result[bool]
ProductManager
Purpose: Manages product catalog and pricing operations Key Methods:

create_product(product_dto: ProductCreateDTO) -> Result[ProductDTO]
update_pricing(product_id: int, pricing_dto: PricingUpdateDTO) -> Result[ProductDTO]
get_product_by_sku(sku: str) -> Result[ProductDTO]
check_product_availability(product_id: int, quantity: Decimal) -> Result[bool]
calculate_product_margins() -> Result[List[MarginAnalysisDTO]]
SalesManager
Purpose: Orchestrates sales transaction processing Key Methods:

create_transaction(transaction_dto: SalesTransactionCreateDTO) -> Result[SalesTransactionDTO]
process_payment(transaction_id: int, payment_dto: PaymentDTO) -> Result[PaymentDTO]
void_transaction(transaction_id: int, reason: str) -> Result[bool]
apply_discount(transaction_id: int, discount_dto: DiscountDTO) -> Result[SalesTransactionDTO]
generate_receipt(transaction_id: int) -> Result[ReceiptDTO]
InventoryManager
Purpose: Manages inventory levels and stock movements Key Methods:

adjust_stock(product_id: int, adjustment_dto: StockAdjustmentDTO) -> Result[InventoryDTO]
reserve_stock(product_id: int, quantity: Decimal) -> Result[bool]
release_reserved_stock(product_id: int, quantity: Decimal) -> Result[bool]
check_reorder_points() -> Result[List[ReorderAlertDTO]]
generate_stock_report(criteria: StockReportCriteria) -> Result[StockReportDTO]
PaymentManager
Purpose: Handles payment processing and validation Key Methods:

process_payment(payment_dto: PaymentCreateDTO) -> Result[PaymentDTO]
validate_payment_method(method: str, amount: Decimal) -> Result[bool]
calculate_change(amount_paid: Decimal, total_amount: Decimal) -> Result[Decimal]
handle_multi_currency_payment(payment_dto: MultiCurrencyPaymentDTO) -> Result[PaymentDTO]
generate_payment_journal_entry(payment_id: int) -> Result[JournalEntryDTO]
GSTManager
Purpose: Manages GST calculations and compliance Key Methods:

calculate_gst(amount: Decimal, gst_rate: Decimal) -> Result[GSTCalculationDTO]
get_applicable_gst_rate(product_id: int, transaction_date: date) -> Result[Decimal]
generate_gst_report(period: DateRange) -> Result[GSTReportDTO]
validate_gst_registration(registration_number: str) -> Result[bool]
create_gst_journal_entries(transaction_id: int) -> Result[List[JournalEntryDTO]]
Service Classes (app/services/)
BaseService
Purpose: Provides common repository functionality Key Features:

Generic CRUD operations
Query building utilities
Transaction management
Error handling and logging
CustomerService
Purpose: Data access layer for customer operations Key Methods:

create(customer: Customer) -> Customer
get_by_id(id: int) -> Optional[Customer]
get_by_email(email: str) -> Optional[Customer]
search(criteria: Dict[str, Any]) -> List[Customer]
update(customer: Customer) -> Customer
delete(id: int) -> bool
ProductService
Purpose: Data access layer for product operations Key Methods:

create(product: Product) -> Product
get_by_sku(sku: str) -> Optional[Product]
get_by_category(category_id: int) -> List[Product]
search_by_name(name: str) -> List[Product]
get_low_stock_products() -> List[Product]
update_pricing(product_id: int, new_price: Decimal) -> Product
UI Components (app/ui/)
MainWindow
Purpose: Primary application window and navigation controller Key Features:

Menu bar with all application functions
Status bar with system information
Tab-based navigation between modules
User session management
Application-wide shortcuts
POSWidget
Purpose: Point-of-sale transaction interface Key Features:

Product search and selection
Shopping cart management
Price calculation and tax computation
Payment processing interface
Receipt generation and printing
InventoryWidget
Purpose: Inventory management interface Key Features:

Stock level monitoring
Stock adjustment forms
Reorder point management
Inventory reports and analytics
Barcode scanning integration
CustomersWidget
Purpose: Customer management interface Key Features:

Customer CRUD operations
Customer search and filtering
Credit limit management
Customer transaction history
Customer analytics and reports
Data Transfer Objects (app/business_logic/dtos/)
CustomerDTO Classes
@dataclass
class CustomerCreateDTO:
    name: str
    email: Optional[str]
    phone: Optional[str]
    address: Optional[str]
    customer_type: str = "individual"
    credit_limit: Decimal = Decimal("0.00")

@dataclass
class CustomerDTO:
    id: int
    customer_code: str
    name: str
    email: Optional[str]
    phone: Optional[str]
    address: Optional[str]
    customer_type: str
    credit_limit: Decimal
    is_active: bool
    created_at: datetime

SalesTransactionDTO Classes
@dataclass
class SalesTransactionCreateDTO:
    customer_id: Optional[int]
    items: List[SalesItemDTO]
    discount_amount: Decimal = Decimal("0.00")
    payment_method: str = "cash"
    notes: Optional[str] = None

@dataclass
class SalesTransactionDTO:
    id: int
    transaction_number: str
    customer_id: Optional[int]
    transaction_date: datetime
    subtotal_amount: Decimal
    discount_amount: Decimal
    tax_amount: Decimal
    total_amount: Decimal
    status: str
    items: List[SalesItemDTO]

User Interface Design
Design Principles
Consistency: All UI elements follow a consistent design language with standardized colors, fonts, spacing, and interaction patterns.

Efficiency: The interface is optimized for rapid data entry and transaction processing, minimizing the number of clicks and keystrokes required for common operations.

Accessibility: The application supports keyboard navigation, appropriate contrast ratios, and clear visual hierarchies to ensure usability for all users.

Responsiveness: The interface adapts to different screen sizes and resolutions while maintaining functionality and usability.

Main Application Layout
The main window uses a tab-based interface with the following primary sections:

Point of Sale - Primary transaction processing interface
Inventory - Stock management and control
Customers - Customer relationship management
Products - Product catalog management
Reports - Business intelligence and analytics
Accounting - Financial management and reporting
Settings - System configuration and preferences
Point of Sale Interface
The POS interface is the primary working area for cashiers and includes:

Product Search Panel:

Barcode scanner input
Product name search with autocomplete
Category-based product browsing
Frequently used items quick access
Transaction Panel:

Shopping cart with item details
Real-time price calculation
Tax computation display
Discount application interface
Customer selection dropdown
Payment Panel:

Multiple payment method support
Cash payment with change calculation
Credit card processing interface
Multi-currency payment handling
Receipt generation and printing
Inventory Management Interface
Stock Overview:

Real-time inventory levels
Low stock alerts and notifications
Product availability status
Reorder point indicators
Stock Adjustment Forms:

Stock in/out transactions
Adjustment reason codes
Batch and serial number tracking
Automatic journal entry generation
Reporting Dashboard:

Inventory valuation reports
Stock movement history
Turnover analysis
Aging inventory reports
Customer Management Interface
Customer List View:

Searchable and sortable customer database
Quick filters for customer types
Credit limit status indicators
Account status visualization
Customer Detail Forms:

Comprehensive customer information
Transaction history display
Payment terms management
Credit limit monitoring
Customer Analytics:

Purchase history analysis
Customer profitability reports
Loyalty program integration
Marketing campaign tracking
Key Features & Functionality
Core POS Features
Transaction Processing:

Fast product lookup by barcode, SKU, or name
Multiple quantity and unit of measure support
Real-time price calculation with tax computation
Flexible discount application (percentage, fixed amount, item-specific)
Multi-tender payment processing (cash, credit, combination)
Automatic change calculation
Receipt generation and printing
Transaction void and refund capabilities
Inventory Management:

Real-time stock tracking
Automated reorder point notifications
Stock adjustment with reason codes
Barcode generation and printing
Multi-location inventory support
Product bundling and kit management
Expiry date tracking for perishables
Supplier management and purchase orders
Customer Relationship Management:

Comprehensive customer database
Customer transaction history
Credit limit management and monitoring
Customer-specific pricing and discounts
Loyalty program integration
Customer communication tools
Purchase behavior analytics
Advanced Features
Multi-Currency Support:

Multiple currency acceptance
Real-time exchange rate updates
Currency conversion calculations
Multi-currency financial reporting
Base currency standardization
User Management:

Role-based access control
User activity logging
Permission management
Shift management for cashiers
User performance analytics
Reporting and Analytics:

Sales performance reports
Inventory turnover analysis
Customer behavior insights
Financial performance dashboards
Custom report builder
Export capabilities (PDF, Excel, CSV)
Integration Capabilities:

Barcode scanner integration
Receipt printer support
Cash drawer control
Credit card terminal integration
Accounting software export
E-commerce platform synchronization
Business Intelligence Features
Dashboard Overview:

Key performance indicators (KPIs)
Real-time sales metrics
Inventory alerts and notifications
Top-selling products analysis
Customer activity summaries
Financial performance indicators
Advanced Analytics:

Sales trend analysis
Seasonal demand forecasting
Product profitability analysis
Customer segmentation
Inventory optimization recommendations
Price elasticity analysis
Reporting Suite:

Daily sales summaries
Inventory valuation reports
Customer transaction reports
Tax and GST compliance reports
Profit and loss statements
Balance sheet generation
Cash flow analysis
Singapore Regulatory Compliance
GST (Goods and Services Tax) Compliance
GST Registration Management:

GST registration number validation
Multiple GST rates support (standard, zero-rated, exempt)
Automatic GST calculation based on product classification
GST-inclusive and GST-exclusive pricing modes
Customer GST status tracking
GST Reporting:

GST return preparation (Form GST F5)
Input and output tax calculations
GST liability computation
Detailed transaction logs for audit purposes
GST payment tracking and reconciliation
Tax Invoice Requirements:

Compliant tax invoice generation
Sequential invoice numbering
Required field validation (GST number, date, amounts)
Customer details verification
Electronic invoice archival
Accounting Standards Compliance
Singapore Financial Reporting Standards (SFRS):

Chart of accounts structured per SFRS requirements
Proper revenue recognition principles
Expense categorization and allocation
Asset depreciation calculations
Financial statement preparation
Audit Trail Maintenance:

Complete transaction logging
User activity tracking
Data modification history
System access logs
Backup and recovery procedures
Data Protection Compliance
Personal Data Protection Act (PDPA):

Customer consent management
Data collection purpose limitation
Access controls and user permissions
Data retention policy enforcement
Secure data disposal procedures
Breach notification mechanisms
Security Measures:

Data encryption at rest and in transit
Secure user authentication
Role-based access controls
Regular security assessments
Compliance monitoring and reporting
Business Registration Integration
ACRA (Accounting and Corporate Regulatory Authority) Compliance:

Business registration number validation
Director and shareholder information management
Annual return preparation support
Company secretary appointment tracking
Compliance deadline notifications
UEN (Unique Entity Number) Management:

UEN validation and verification
Entity type classification
Registration status monitoring
Government correspondence tracking
Development Environment Setup
Prerequisites
System Requirements:

Python 3.11 or higher
PostgreSQL 15 or higher
Git version control system
8GB RAM minimum (16GB recommended)
50GB available disk space
Internet connection for package downloads
Development Tools:

PyCharm Professional or VS Code with Python extensions
pgAdmin 4 or similar PostgreSQL management tool
Postman or similar API testing tool
Database migration tools (Alembic)
Installation Steps
1. Clone Repository:

git clone https://github.com/company/sg-pos-system.git
cd sg-pos-system

2. Create Virtual Environment:

python -m venv venv
source venv/bin/activate  # Linux/macOS
# or
venv\Scripts\activate  # Windows

3. Install Dependencies:

pip install -r requirements/development.txt

4. Database Setup:

# Create PostgreSQL database
createdb sg_pos_dev

# Set environment variables
cp .env.example .env.dev
# Edit .env.dev with your database credentials

# Run database migrations
alembic upgrade head

# Load initial data
python scripts/load_initial_data.py

5. Configuration:

# Copy development configuration
cp config/development.env.example config/development.env
# Edit configuration file with appropriate values

# Generate encryption keys
python scripts/generate_keys.py

6. Run Application:

python -m app.main --env development

Development Workflow
Code Quality Checks:

# Run linting
black app/ tests/
flake8 app/ tests/
mypy app/

# Run tests
pytest tests/ -v --cov=app

Database Management:

# Create new migration
alembic revision --autogenerate -m "Description"

# Apply migrations
alembic upgrade head

# Rollback migration
alembic downgrade -1

Testing:

# Run unit tests
pytest tests/unit/ -v

# Run integration tests
pytest tests/integration/ -v

# Run all tests with coverage
pytest tests/ --cov=app --cov-report=html

Development Tools Configuration
IDE Setup (PyCharm):

Configure Python interpreter to use project virtual environment
Set up code style to use Black formatting
Configure database data source for PostgreSQL
Set up run configurations for main application and tests
Enable type checking with mypy plugin
Git Hooks:

# Install pre-commit hooks
pre-commit install

# Configure hooks for code quality
# .pre-commit-config.yaml includes:
# - black (code formatting)
# - flake8 (linting)
# - mypy (type checking)
# - pytest (testing)

Environment Variables:

# Development environment (.env.dev)
DATABASE_URL=postgresql://user:password@localhost/sg_pos_dev
SECRET_KEY=development-secret-key
DEBUG=True
LOG_LEVEL=DEBUG
ENVIRONMENT=development

Production Environment Setup
Infrastructure Requirements
Server Specifications:

CPU: 4 cores minimum (8 cores recommended)
RAM: 16GB minimum (32GB recommended)
Storage: 500GB SSD minimum
Network: Gigabit Ethernet
Operating System: Ubuntu 22.04 LTS or Windows Server 2022
Database Server:

PostgreSQL 15 or higher
Dedicated server or managed database service
Automated backup and recovery
High availability configuration
SSL/TLS encryption enabled
Production Deployment
1. Server Preparation:

# Update system packages
sudo apt update && sudo apt upgrade -y

# Install Python and dependencies
sudo apt install python3.11 python3.11-venv python3-pip postgresql-client

# Create application user
sudo useradd -m -s /bin/bash sgpos
sudo usermod -aG sudo sgpos

2. Application Deployment:

# Switch to application user
sudo su - sgpos

# Create application directory
mkdir -p /opt/sgpos
cd /opt/sgpos

# Clone production code
git clone -b production https://github.com/company/sg-pos-system.git .

# Create virtual environment
python3.11 -m venv venv
source venv/bin/activate

# Install production dependencies
pip install -r requirements/production.txt

3. Database Configuration:

# Create production database
createdb sg_pos_prod

# Run migrations
export DATABASE_URL="postgresql://user:password@dbserver/sg_pos_prod"
alembic upgrade head

# Load initial production data
python scripts/load_production_data.py

4. System Service Configuration:

# Create systemd service file
sudo nano /etc/systemd/system/sgpos.service

[Unit]
Description=SG POS System
After=network.target postgresql.service

[Service]
Type=simple
User=sgpos
WorkingDirectory=/opt/sgpos
Environment=PATH=/opt/sgpos/venv/bin
ExecStart=/opt/sgpos/venv/bin/python -m app.main --env production
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target

# Enable and start service
sudo systemctl enable sgpos
sudo systemctl start sgpos

5. Security Configuration:

# Configure firewall
sudo ufw enable
sudo ufw allow ssh
sudo 
