This is a comprehensive request for a detailed Product Requirements Document (PRD) for a Singapore-specific Point-of-Sale system. The user wants a professional-grade document that covers:
Complete system architecture with layered design
Database schema with proper normalization
Technology stack details
File hierarchy and module organization
Development and production environment setup
At least 6000 words with no ambiguity
Key considerations for Singapore market:

GST compliance (7% GST rate)
Multi-currency support (SGD primary)
Local business regulations
SMB focus with scalability
Professional retail requirements
The architecture needs to be:

Layered (Presentation → Business Logic → Data Access → Persistence)
Asynchronous for performance
Dependency injection for modularity
Clean separation of concerns
Result pattern and DTOs for robust error handling
I'll structure this as a comprehensive PRD covering all technical and business aspects needed to build this system. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Project Overview
Functional Requirements
Non-Functional Requirements
Technology Stack
System Architecture
Database Schema Design
Application Modules & File Hierarchy
User Interface Design
Development Environment Setup
Production Environment Setup
Implementation Roadmap
Risk Assessment & Mitigation
Success Metrics
Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed for small to medium-sized businesses (SMBs) operating in Singapore's retail environment. This professional-grade solution addresses the unique regulatory requirements of Singapore's business landscape while providing robust functionality for modern retail operations.

Built on a foundation of Python and PySide6, with PostgreSQL as the backend database, the system employs a sophisticated layered architecture that ensures scalability, maintainability, and performance. The application incorporates Singapore-specific features including GST compliance, multi-currency support with SGD as the primary currency, and integration capabilities with local financial institutions and regulatory systems.

The system's architecture follows industry best practices including dependency injection, asynchronous processing, the Result pattern, and Data Transfer Objects (DTOs) to ensure robust error handling and clean separation of concerns. This foundation provides exceptional reliability while maintaining the flexibility needed for future enhancements and integrations.

Project Overview
Business Context
Singapore's retail sector requires sophisticated point-of-sale solutions that can navigate complex regulatory requirements while providing the operational efficiency modern businesses demand. Small to medium-sized businesses face particular challenges in finding affordable yet comprehensive POS solutions that can handle Singapore's GST requirements, multi-currency transactions, and integration with local banking systems.

Target Audience
Primary Users:

Small to medium retail businesses (5-50 employees)
Restaurant and hospitality establishments
Service-based businesses requiring transaction processing
Multi-location retail chains with centralized management needs
Secondary Users:

Business owners requiring comprehensive reporting
Accountants needing GST-compliant transaction records
Store managers requiring inventory oversight
Customer service representatives processing returns and exchanges
Key Value Propositions
Singapore Compliance: Built-in GST calculation, reporting, and submission capabilities aligned with IRAS requirements
Multi-Currency Support: Native handling of SGD and major international currencies with real-time exchange rates
Scalable Architecture: Layered design supporting growth from single-location to multi-store operations
Professional Reliability: Enterprise-grade error handling and data integrity mechanisms
Modern User Experience: Intuitive PySide6-based interface optimized for efficiency and ease of use
Functional Requirements
Core Transaction Processing
Sales Transaction Management

Process single and multi-item sales with barcode scanning support
Apply discounts at item and transaction levels with business rule validation
Handle complex pricing scenarios including bulk discounts and promotional offers
Support split payments across multiple payment methods
Generate and print professional receipts with customizable templates
Process returns and exchanges with proper audit trails
Payment Processing

Accept cash, credit/debit cards, and digital payments (PayNow, GrabPay, etc.)
Integration with local payment gateways and card processors
Real-time payment validation and fraud detection
Automatic change calculation and cash drawer management
Support for gift cards and store credit systems
Inventory Management
Product Catalog Management

Comprehensive product database with categories, variants, and attributes
Barcode generation and management system
Multi-location inventory tracking with transfer capabilities
Automated reorder points and purchase order generation
Supplier management with contact information and terms
Cost tracking and margin analysis tools
Stock Control

Real-time inventory updates across all sales channels
Stock adjustment capabilities with approval workflows
Perpetual inventory system with periodic reconciliation
Lot and serial number tracking for applicable products
Expiration date monitoring and automated alerts
Customer Relationship Management
Customer Database

Comprehensive customer profiles with purchase history
Loyalty program integration with points and rewards tracking
Customer segmentation and targeted marketing capabilities
Birthday and anniversary tracking for promotional opportunities
Customer communication preferences and contact management
Financial Management & GST Compliance
GST Handling

Automatic GST calculation based on product categories and customer types
GST-exempt transaction processing for eligible customers
Comprehensive GST reporting aligned with IRAS requirements
Support for various GST rates and exemptions
Integration with accounting systems for seamless financial management
Financial Reporting

Daily, weekly, monthly, and custom period reports
Sales analysis by product, category, and customer segments
Profit and loss statements with cost of goods sold calculations
Cash flow tracking and bank reconciliation tools
Tax reporting and audit trail maintenance
User Management & Security
Role-Based Access Control

Hierarchical user roles with granular permissions
Employee time tracking and performance monitoring
Secure login with password policies and session management
Activity logging and audit trail maintenance
Multi-factor authentication for administrative functions
Multi-Location Support
Centralized Management

Head office oversight of multiple store locations
Centralized inventory management with location-specific stock levels
Consolidated reporting across all locations
Inter-store transfers and stock balancing
Centralized pricing and promotion management
Non-Functional Requirements
Performance Requirements
Response Time Standards

Transaction processing: < 2 seconds for standard sales
Report generation: < 10 seconds for daily reports, < 30 seconds for complex analytics
Database queries: < 1 second for customer lookups, < 3 seconds for inventory searches
System startup: < 15 seconds for full application initialization
Throughput Requirements

Support minimum 100 concurrent transactions across all locations
Process 1000+ transactions per hour per terminal during peak periods
Handle 50,000+ products in inventory database
Support 10,000+ active customers per location
Reliability & Availability
System Uptime

Target 99.5% uptime during business hours
Graceful degradation when network connectivity is limited
Offline mode capability for essential functions
Automatic recovery from system failures with minimal data loss
Data Integrity

ACID compliance for all financial transactions
Automatic backup systems with point-in-time recovery
Transaction logging with immutable audit trails
Data validation at all system entry points
Security Requirements
Data Protection

Encryption of sensitive data both at rest and in transit
PCI DSS compliance for payment card information
Singapore Personal Data Protection Act (PDPA) compliance
Role-based access controls with principle of least privilege
System Security

Secure authentication and session management
Protection against SQL injection and other common attacks
Regular security updates and vulnerability assessments
Comprehensive logging of security-related events
Scalability & Maintainability
Horizontal Scaling

Architecture supporting addition of new locations and terminals
Database design optimized for growth and performance
Modular codebase allowing feature additions without core system changes
API-first design enabling third-party integrations
Code Quality

Comprehensive unit and integration testing coverage (>90%)
Adherence to Python PEP 8 style guidelines
Extensive documentation for all modules and APIs
Continuous integration and deployment pipelines
Technology Stack
Core Technologies
Programming Language: Python 3.11+ Python provides the ideal foundation for this application due to its excellent ecosystem of business-focused libraries, strong database connectivity options, and mature GUI frameworks. The language's emphasis on readability and maintainability aligns perfectly with the project's long-term sustainability goals.

GUI Framework: PySide6 PySide6 offers the most comprehensive and modern GUI framework for Python desktop applications. Its Qt foundation provides:

Native look and feel across different operating systems
Comprehensive widget set for complex business applications
Excellent printing and report generation capabilities
Strong internationalization support for multi-language requirements
Professional-grade layout management and styling options
Database System: PostgreSQL 15+ PostgreSQL serves as the primary database engine, chosen for:

ACID compliance ensuring data integrity for financial transactions
Advanced indexing capabilities for optimal query performance
JSON support for flexible data structures and configurations
Robust backup and recovery mechanisms
Excellent concurrency handling for multi-user environments
Strong ecosystem of monitoring and maintenance tools
Supporting Libraries & Frameworks
Database & ORM Layer

# SQLAlchemy 2.0+ - Advanced ORM with async support
# Alembic - Database migration management
# asyncpg - High-performance PostgreSQL adapter
# psycopg2-binary - Synchronous PostgreSQL adapter (fallback)

Asynchronous Processing

# asyncio - Native Python async runtime
# aiofiles - Asynchronous file operations
# asyncqt - Bridge between Qt event loop and asyncio

Data Validation & Serialization

# Pydantic 2.0+ - Data validation and serialization
# marshmallow - Alternative serialization library
# python-dateutil - Advanced date/time handling

Business Logic Support

# decimal - Precise financial calculations
# babel - Internationalization and localization
# reportlab - PDF generation for receipts and reports
# xlsxwriter - Excel report generation
# qrcode - QR code generation for receipts

Testing & Quality Assurance

# pytest - Comprehensive testing framework
# pytest-asyncio - Async testing support
# pytest-qt - Qt application testing
# coverage - Code coverage analysis
# black - Code formatting
# flake8 - Code linting
# mypy - Static type checking

Development Tools
Dependency Management

Poetry for dependency management and virtual environment handling
Pre-commit hooks for code quality enforcement
GitHub Actions for continuous integration
Database Management

DBeaver for database administration and query development
pgAdmin for PostgreSQL-specific administration
Database migration scripts using Alembic
Documentation

Sphinx for comprehensive API documentation
MkDocs for user guides and business documentation
Draw.io for system architecture diagrams
System Architecture
Architectural Overview
The SG POS System implements a sophisticated four-layer architecture that ensures clean separation of concerns, maintaiability, and scalability. Each layer has distinct responsibilities and communicates through well-defined interfaces.

┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                       │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────────────────┐│
│  │   Dialogs   │ │   Widgets   │ │      Main Windows       ││
│  └─────────────┘ └─────────────┘ └─────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                 BUSINESS LOGIC LAYER                        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────────────────┐│
│  │  Managers   │ │ Controllers │ │    Domain Services      ││
│  └─────────────┘ └─────────────┘ └─────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  DATA ACCESS LAYER                          │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────────────────┐│
│  │ Repositories│ │  Services   │ │       DTOs              ││
│  └─────────────┘ └─────────────┘ └─────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                   PERSISTENCE LAYER                         │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────────────────┐│
│  │    Models   │ │  Database   │ │    Migrations           ││
│  └─────────────┘ └─────────────┘ └─────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
Layer Responsibilities
Presentation Layer (app/ui/)

User interface components built with PySide6
Event handling and user input validation
Data presentation and formatting
Navigation and workflow management
No direct database access or business logic
Business Logic Layer (app/business_logic/, app/managers/)

Core business rules and workflows
Transaction processing logic
GST calculations and compliance
Validation of business rules
Coordination between data services
Data Access Layer (app/services/, app/repositories/)

Database abstraction and query optimization
Data transformation and mapping
Caching strategies and performance optimization
External API integration
Repository pattern implementation
Persistence Layer (app/models/, database/)

SQLAlchemy ORM models
Database schema definition
Migration management
Database constraints and triggers
Data integrity enforcement
Dependency Injection Architecture
The system implements a sophisticated dependency injection mechanism through the ApplicationCore class, which serves as the central service locator and dependency container.

class ApplicationCore:
    """Central dependency injection container and service locator."""
    
    def __init__(self):
        self._db_session = None
        self._services = {}
        self._managers = {}
    
    @property
    def customer_service(self) -> CustomerService:
        if 'customer_service' not in self._services:
            self._services['customer_service'] = CustomerService(self.db_session)
        return self._services['customer_service']
    
    @property
    def sales_manager(self) -> SalesManager:
        if 'sales_manager' not in self._managers:
            self._managers['sales_manager'] = SalesManager(self)
        return self._managers['sales_manager']

Asynchronous Architecture
The application employs a dual-threaded asynchronous architecture to ensure responsive user interfaces while handling intensive background operations.

Main Thread (Qt Event Loop)

GUI rendering and user interaction
Event handling and immediate responses
UI updates and state management
Background Thread (AsyncIO Event Loop)

Database operations and queries
File I/O and report generation
External API calls and integrations
Background processing tasks
Thread Communication Bridge

def schedule_task_from_qt(coro):
    """Bridge function to schedule asyncio tasks from Qt thread."""
    future = asyncio.run_coroutine_threadsafe(coro, async_loop)
    return future

def update_ui_from_async(widget, method, *args):
    """Safely update UI from async context."""
    QMetaObject.invokeMethod(
        widget, method, Qt.QueuedConnection, *args
    )

Database Schema Design
Schema Overview
The database schema is designed following third normal form (3NF) principles while maintaining practical performance considerations. The schema supports multi-currency transactions, comprehensive audit trails, and Singapore-specific business requirements.

Core Entity Relationships
-- Core business entities and their relationships
Users (1) ←→ (N) Transactions
Customers (1) ←→ (N) Transactions
Products (1) ←→ (N) TransactionItems
Categories (1) ←→ (N) Products
Suppliers (1) ←→ (N) Products
Locations (1) ←→ (N) Inventory
Taxes (1) ←→ (N) TransactionItems
PaymentMethods (1) ←→ (N) Payments

Detailed Schema Definition
Users and Authentication

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role VARCHAR(20) NOT NULL CHECK (role IN ('admin', 'manager', 'cashier', 'viewer')),
    is_active BOOLEAN DEFAULT TRUE,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE user_sessions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    session_token VARCHAR(255) UNIQUE NOT NULL,
    expires_at TIMESTAMP WITH TIME ZONE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Customer Management

CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(20) UNIQUE NOT NULL,
    company_name VARCHAR(255),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(255),
    phone VARCHAR(20),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(10),
    country VARCHAR(3) DEFAULT 'SGP',
    gst_registration_number VARCHAR(20),
    is_gst_registered BOOLEAN DEFAULT FALSE,
    customer_type VARCHAR(20) DEFAULT 'individual' CHECK (customer_type IN ('individual', 'business')),
    credit_limit DECIMAL(12,2) DEFAULT 0.00,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE customer_loyalty_points (
    id SERIAL PRIMARY KEY,
    customer_id INTEGER REFERENCES customers(id) ON DELETE CASCADE,
    points_balance INTEGER DEFAULT 0,
    lifetime_points INTEGER DEFAULT 0,
    tier_level VARCHAR(20) DEFAULT 'bronze',
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Product and Inventory Management

CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    parent_id INTEGER REFERENCES categories(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE suppliers (
    id SERIAL PRIMARY KEY,
    supplier_code VARCHAR(20) UNIQUE NOT NULL,
    company_name VARCHAR(255) NOT NULL,
    contact_person VARCHAR(100),
    email VARCHAR(255),
    phone VARCHAR(20),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(10),
    country VARCHAR(3) DEFAULT 'SGP',
    payment_terms INTEGER DEFAULT 30,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    supplier_id INTEGER REFERENCES suppliers(id),
    unit_of_measure VARCHAR(20) DEFAULT 'piece',
    cost_price DECIMAL(10,2) NOT NULL DEFAULT 0.00,
    selling_price DECIMAL(10,2) NOT NULL DEFAULT 0.00,
    gst_rate DECIMAL(5,2) DEFAULT 7.00,
    is_gst_inclusive BOOLEAN DEFAULT TRUE,
    is_active BOOLEAN DEFAULT TRUE,
    is_service BOOLEAN DEFAULT FALSE,
    minimum_stock_level INTEGER DEFAULT 0,
    maximum_stock_level INTEGER,
    reorder_point INTEGER DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    location_code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(10),
    is_main_location BOOLEAN DEFAULT FALSE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id) ON DELETE CASCADE,
    location_id INTEGER REFERENCES locations(id) ON DELETE CASCADE,
    quantity_on_hand INTEGER NOT NULL DEFAULT 0,
    quantity_allocated INTEGER NOT NULL DEFAULT 0,
    quantity_available INTEGER GENERATED ALWAYS AS (quantity_on_hand - quantity_allocated) STORED,
    last_counted_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location_id)
);

Transaction Processing

CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(20) UNIQUE NOT NULL,
    transaction_type VARCHAR(20) NOT NULL CHECK (transaction_type IN ('sale', 'return', 'exchange', 'void')),
    customer_id INTEGER REFERENCES customers(id),
    user_id INTEGER REFERENCES users(id) NOT NULL,
    location_id INTEGER REFERENCES locations(id) NOT NULL,
    transaction_date TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    subtotal DECIMAL(12,2) NOT NULL DEFAULT 0.00,
    total_discount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
    gst_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
    total_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
    currency VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,4) DEFAULT 1.0000,
    status VARCHAR(20) DEFAULT 'completed' CHECK (status IN ('pending', 'completed', 'voided', 'refunded')),
    notes TEXT,
    receipt_printed BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    product_id INTEGER REFERENCES products(id),
    quantity DECIMAL(10,3) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0.00,
    gst_rate DECIMAL(5,2) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(12,2) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    payment_method VARCHAR(20) NOT NULL CHECK (payment_method IN ('cash', 'card', 'paynow', 'grabpay', 'store_credit')),
    amount DECIMAL(12,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'SGD',
    reference_number VARCHAR(100),
    card_last_four VARCHAR(4),
    approval_code VARCHAR(20),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

GST and Financial Reporting

CREATE TABLE gst_rates (
    id SERIAL PRIMARY KEY,
    rate_name VARCHAR(50) NOT NULL,
    rate_percentage DECIMAL(5,2) NOT NULL,
    effective_from DATE NOT NULL,
    effective_to DATE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE gst_transactions (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    gst_rate_id INTEGER REFERENCES gst_rates(id),
    taxable_amount DECIMAL(12,2) NOT NULL,
    gst_amount DECIMAL(12,2) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

Database Indexes and Performance Optimization
-- Performance indexes for frequent queries
CREATE INDEX idx_transactions_date ON transactions(transaction_date);
CREATE INDEX idx_transactions_customer ON transactions(customer_id);
CREATE INDEX idx_transactions_user ON transactions(user_id);
CREATE INDEX idx_transaction_items_product ON transaction_items(product_id);
CREATE INDEX idx_inventory_product_location ON inventory(product_id, location_id);
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_barcode ON products(barcode);
CREATE INDEX idx_customers_code ON customers(customer_code);

-- Composite indexes for complex queries
CREATE INDEX idx_transactions_date_location ON transactions(transaction_date, location_id);
CREATE INDEX idx_inventory_location_quantity ON inventory(location_id, quantity_available);

Database Triggers and Constraints
-- Automatic timestamp updates
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_users_updated_at BEFORE UPDATE ON users
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

-- Inventory update triggers
CREATE OR REPLACE FUNCTION update_inventory_on_transaction()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        UPDATE inventory 
        SET quantity_on_hand = quantity_on_hand - NEW.quantity
        WHERE product_id = NEW.product_id;
    END IF;
    RETURN NULL;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_inventory_after_sale 
    AFTER INSERT ON transaction_items
    FOR EACH ROW EXECUTE FUNCTION update_inventory_on_transaction();

Application Modules & File Hierarchy
Project Structure Overview
The application follows a sophisticated modular architecture with clear separation of concerns and dependency management. The file hierarchy is organized to support scalability, maintainability, and testing.

sg_pos_system/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py          # Central DI container
│   │   ├── config.py                    # Configuration management
│   │   ├── exceptions.py                # Custom exception definitions
│   │   ├── logging_config.py            # Logging configuration
│   │   └── result.py                    # Result pattern implementation
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                      # SQLAlchemy base model
│   │   ├── user.py                      # User and authentication models
│   │   ├── customer.py                  # Customer-related models
│   │   ├── product.py                   # Product and category models
│   │   ├── inventory.py                 # Inventory management models
│   │   ├── transaction.py               # Transaction and payment models
│   │   ├── gst.py                       # GST and tax models
│   │   └── location.py                  # Store location models
│   ├── services/
│   │   ├── __init__.py
│   │   ├── base_service.py              # Base service class
│   │   ├── user_service.py              # User management service
│   │   ├── customer_service.py          # Customer operations service
│   │   ├── product_service.py           # Product management service
│   │   ├── inventory_service.py         # Inventory operations service
│   │   ├── transaction_service.py       # Transaction processing service
│   │   ├── payment_service.py           # Payment processing service
│   │   ├── gst_service.py               # GST calculation service
│   │   └── report_service.py            # Reporting and analytics service
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── sales_manager.py         # Sales transaction orchestration
│   │   │   ├── inventory_manager.py     # Inventory business logic
│   │   │   ├── customer_manager.py      # Customer relationship management
│   │   │   ├── payment_manager.py       # Payment processing coordination
│   │   │   ├── gst_manager.py           # GST compliance management
│   │   │   └── report_manager.py        # Report generation coordination
│   │   ├── validators/
│   │   │   ├── __init__.py
│   │   │   ├── transaction_validator.py # Transaction validation rules
│   │   │   ├── customer_validator.py    # Customer data validation
│   │   │   ├── product_validator.py     # Product data validation
│   │   │   └── gst_validator.py         # GST compliance validation
│   │   └── workflows/
│   │       ├── __init__.py
│   │       ├── sales_workflow.py        # Sales process workflow
│   │       ├── return_workflow.py       # Return/exchange workflow
│   │       └── inventory_workflow.py    # Inventory management workflow
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py               # Primary application window
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── pos_widget.py            # Point-of-sale interface
│   │   │   ├── customer_widget.py       # Customer management interface
│   │   │   ├── product_widget.py        # Product management interface
│   │   │   ├── inventory_widget.py      # Inventory management interface
│   │   │   ├── reports_widget.py        # Reports and analytics interface
│   │   │   └── settings_widget.py       # Application settings interface
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── login_dialog.py          # User authentication dialog
│   │   │   ├── customer_dialog.py       # Customer add/edit dialog
│   │   │   ├── product_dialog.py        # Product add/edit dialog
│   │   │   ├── payment_dialog.py        # Payment processing dialog
│   │   │   └── settings_dialog.py       # Application configuration dialog
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── table_models.py          # Qt table model implementations
│   │   │   └── list_models.py           # Qt list model implementations
│   │   └── resources/
│   │       ├── icons/                   # Application icons
│   │       ├── styles/                  # Qt stylesheet files
│   │       └── templates/               # Receipt and report templates
│   ├── dto/
│   │   ├── __init__.py
│   │   ├── customer_dto.py              # Customer data transfer objects
│   │   ├── product_dto.py               # Product data transfer objects
│   │   ├── transaction_dto.py           # Transaction data transfer objects
│   │   └── report_dto.py                # Report data transfer objects
│   └── utils/
│       ├── __init__.py
│       ├── formatting.py               # Data formatting utilities
│       ├── validation.py               # Common validation functions
│       ├── currency.py                 # Currency handling utilities
│       ├── barcode.py                  # Barcode generation utilities
│       └── printing.py                 # Receipt printing utilities
├── database/
│   ├── migrations/                     # Alembic migration files
│   ├── schema.sql                      # Database schema definition
│   ├── seed_data.sql                   # Initial data setup
│   └── alembic.ini                     # Alembic configuration
├── tests/
│   ├── __init__.py
│   ├── conftest.py                     # Pytest configuration
│   ├── unit/
│   │   ├── test_services/              # Service layer unit tests
│   │   ├── test_managers/              # Business logic unit tests
│   │   └── test_models/                # Model unit tests
│   ├── integration/
│   │   ├── test_workflows/             # Integration workflow tests
│   │   └── test_database/              # Database integration tests
│   └── ui/
│       ├── test_widgets/               # UI widget tests
│       └── test_dialogs/               # Dialog functionality tests
├── scripts/
│   ├── setup_dev_environment.py       # Development environment setup
│   ├── backup_database.py             # Database backup utility
│   ├── generate_test_data.py          # Test data generation
│   └── deployment/
│       ├── deploy_production.py       # Production deployment script
│       └── health_check.py            # System health monitoring
├── docs/
│   ├── api/                           # API documentation
│   ├── user_guide/                    # End-user documentation
│   ├── developer_guide/               # Developer documentation
│   └── architecture/                  # System architecture documentation
├── config/
│   ├── development.json               # Development configuration
│   ├── production.json                # Production configuration
│   └── testing.json                   # Testing configuration
├── requirements/
│   ├── base.txt                       # Core dependencies
│   ├── development.txt                # Development dependencies
│   └── production.txt                 # Production dependencies
├── pyproject.toml                     # Poetry configuration
├── README.md                          # Project documentation
├── LICENSE                            # Software license
└── .gitignore                         # Git ignore rules
Key Application Modules
Core Infrastructure Modules
ApplicationCore (app/core/application_core.py) The central dependency injection container that manages service lifecycle and provides lazy initialization of all system components.

class ApplicationCore:
    """
    Central dependency injection container implementing the Service Locator pattern.
    Provides lazy initialization and singleton management for all application services.
    """
    
    def __init__(self):
        self._config = None
        self._db_session = None
        self._services = {}
        self._managers = {}
        self._async_loop = None
    
    @property
    def config(self) -> Config:
        """Application configuration singleton."""
        if self._config is None:
            self._config = Config()
        return self._config
    
    @property
    def db_session(self) -> Session:
        """Database session singleton with connection pooling."""
        if self._db_session is None:
            self._db_session = create_session(self.config.database_url)
        return self._db_session
    
    # Service property implementations with lazy loading
    @property
    def customer_service(self) -> CustomerService:
        if 'customer_service' not in self._services:
            self._services['customer_service'] = CustomerService(self.db_session)
        return self._services['customer_service']
    
    @property
    def sales_manager(self) -> SalesManager:
        if 'sales_manager' not in self._managers:
            self._managers['sales_manager'] = SalesManager(self)
        return self._managers['sales_manager']

Result Pattern Implementation (app/core/result.py) Provides robust error handling and operation result management throughout the application.

from typing import Generic, TypeVar, Union, Optional
from dataclasses import dataclass

T = TypeVar('T')
E = TypeVar('E')

@dataclass
class Result(Generic[T, E]):
    """
    Result pattern implementation for explicit error handling.
    Eliminates the need for exception-based error flow in business logic.
    """
    
    _value: Optional[T] = None
    _error: Optional[E] = None
    _is_success: bool = False
    
    @classmethod
    def success(cls, value: T) -> 'Result[T, E]':
        return cls(_value=value, _is_success=True)
    
    @classmethod
    def failure(cls, error: E) -> 'Result[T, E]':
        return cls(_error=error, _is_success=False)
    
    @property
    def is_success(self) -> bool:
        return self._is_success
    
    @property
    def is_failure(self) -> bool:
        return not self._is_success
    
    @property
    def value(self) -> T:
        if not self.is_success:
            raise ValueError("Cannot access value of failed result")
        return self._value
    
    @property
    def error(self) -> E:
        if self.is_success:
            raise ValueError("Cannot access error of successful result")
        return self._error

Business Logic Managers
Sales Manager (app/business_logic/managers/sales_manager.py) Orchestrates the complete sales transaction workflow including validation, processing, and completion.

class SalesManager:
    """
    Coordinates sales transactions including item processing, payment handling,
    GST calculations, and inventory updates.
    """
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
    
    async def process_sale(self, sale_dto: SaleTransactionDTO) -> Result[TransactionDTO, str]:
        """
        Process a complete sales transaction with full validation and business rule enforcement.
        
        Args:
            sale_dto: Complete sale transaction data
            
        Returns:
            Result containing transaction details or error information
        """
        try:
            # Validate transaction data
            validation_result = await self._validate_sale_transaction(sale_dto)
            if validation_result.is_failure:
                return Result.failure(validation_result.error)
            
            # Calculate GST and totals
            gst_result = await self.app_core.gst_manager.calculate_transaction_gst(sale_dto)
            if gst_result.is_failure:
                return Result.failure(gst_result.error)
            
            # Process inventory updates
            inventory_result = await self._process_inventory_updates(sale_dto)
            if inventory_result.is_failure:
                return Result.failure(inventory_result.error)
            
            # Create transaction record
            transaction_result = await self.app_core.transaction_service.create_transaction(sale_dto)
            if transaction_result.is_failure:
                return Result.failure(transaction_result.error)
            
            # Process payments
            payment_result = await self.app_core.payment_manager.process_payments(
                sale_dto.payments, transaction_result.value.id
            )
            if payment_result.is_failure:
                # Rollback transaction
                await self._rollback_transaction(transaction_result.value.id)
                return Result.failure(payment_result.error)
            
            return Result.success(transaction_result.value)
            
        except Exception as e:
            return Result.failure(f"Unexpected error processing sale: {str(e)}")

GST Manager (app/business_logic/managers/gst_manager.py) Handles Singapore GST compliance including rate calculations, exemption handling, and reporting.

class GSTManager:
    """
    Manages GST calculations, compliance, and reporting for Singapore tax requirements.
    """
    
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
    
    async def calculate_transaction_gst(self, transaction_dto: TransactionDTO) -> Result[GSTCalculationDTO, str]:
        """
        Calculate GST amounts for a transaction based on Singapore tax rules.
        
        Args:
            transaction_dto: Transaction data requiring GST calculation
            
        Returns:
            Result containing GST calculation details or error information
        """
        try:
            gst_calculation = GSTCalculationDTO()
            
            for item in transaction_dto.items:
                # Get product GST rate
                product_result = await self.app_core.product_service.get_by_id(item.product_id)
                if product_result.is_failure:
                    return Result.failure(f"Product not found: {item.product_id}")
                
                product = product_result.value
                
                # Calculate item GST based on customer type and product settings
                item_gst = await self._calculate_item_gst(
                    item, product, 
