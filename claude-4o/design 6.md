<think> This is a substantial request for a comprehensive Product Requirements Document for a Singapore Point-of-Sale system. I need to create a detailed, technical PRD that covers all the specified requirements while incorporating the architectural considerations provided. Let me break this down systematically:
Key Requirements:

At least 6000 words
Database schema design
Codebase file hierarchy diagram
Application modules and user interaction diagram
Key modules and files descriptions
Technology stack details
Development and production environment setup
Clear, unambiguous design for implementation
Technical Architecture Focus:

Layered architecture (Presentation, Business Logic, Data Access, Persistence)
Dependency Injection with ApplicationCore
Asynchronous processing model
Clean code practices (DTOs, Result pattern)
Singapore regulatory compliance (GST, multi-currency)
PySide6 + PostgreSQL + Python stack
I'll structure this as a comprehensive PRD that provides complete technical specifications for building this system. The document should be detailed enough that a development team could implement the entire system based on these requirements. </think>

SG Point-of-Sale System - Product Requirements Document
Table of Contents
Executive Summary
Product Overview
Technical Architecture
Database Schema Design
Application File Hierarchy
Core Modules and Components
User Interface and Interaction Flow
Technology Stack
Development Environment Setup
Production Environment Setup
Implementation Guidelines
Quality Assurance Framework
1. Executive Summary
The SG Point-of-Sale (POS) system is a comprehensive, cross-platform desktop application specifically designed for small to medium-sized businesses (SMBs) operating in Singapore's retail environment. This system addresses the unique regulatory, operational, and business requirements of the Singapore market, including GST compliance, multi-currency support, and local business practices.

Built on a modern technology stack comprising Python 3.11+, PySide6 for the graphical user interface, and PostgreSQL for robust data management, the application provides a professional-grade retail solution that can scale with business growth. The system architecture emphasizes clean separation of concerns, asynchronous processing capabilities, and maintainable code patterns that ensure long-term sustainability and extensibility.

Key Business Objectives
Provide comprehensive retail management capabilities for Singapore SMBs
Ensure compliance with Singapore's GST regulations and IRAS requirements
Support multi-currency transactions for international business operations
Deliver real-time inventory management and reporting capabilities
Maintain high data integrity and audit trail requirements
Enable seamless integration with Singapore's business ecosystem
Success Metrics
Processing capability of 1000+ transactions per day
Sub-second response times for all user interactions
99.9% uptime reliability for business-critical operations
Complete GST compliance with automated reporting capabilities
Support for 10+ concurrent users in multi-workstation environments
2. Product Overview
2.1 Target Market and User Personas
Primary Target Market: Small to medium-sized retail businesses in Singapore with annual revenue between SGD 500,000 to SGD 10 million.

User Personas:

Store Manager: Responsible for overall operations, reporting, and business analytics
Cashier/Sales Associate: Primary system users for transaction processing
Inventory Manager: Handles stock management, purchasing, and supplier relationships
Accountant/Bookkeeper: Manages financial reporting and GST compliance
2.2 Core Functional Requirements
Transaction Management
Process sales transactions with multiple payment methods (cash, credit/debit cards, digital payments)
Handle returns, exchanges, and refunds with proper audit trails
Support discount applications, promotions, and loyalty programs
Generate detailed receipts and invoices with GST breakdown
Inventory Management
Real-time stock tracking with low-stock alerts
Multi-location inventory support for businesses with multiple outlets
Supplier management and purchase order processing
Automated reorder point calculations and purchase suggestions
Customer Management
Comprehensive customer database with transaction history
Loyalty program management and rewards tracking
Customer communication tools for promotions and notifications
Credit limit management for B2B customers
Financial Management
GST calculation and reporting in compliance with IRAS requirements
Multi-currency support with real-time exchange rate updates
Comprehensive financial reporting and analytics
Integration-ready for external accounting systems
Administrative Functions
User management with role-based access control
Audit trail maintenance for all system activities
Backup and data recovery capabilities
System configuration and customization options
2.3 Non-Functional Requirements
Performance Requirements
Response time: <1 second for all user interactions
Throughput: Support 100+ concurrent transactions
Database query optimization for reports generation
Memory usage: <2GB RAM under normal operating conditions
Security Requirements
Role-based access control with granular permissions
Data encryption at rest and in transit
Audit logging for all sensitive operations
Regular security updates and vulnerability patching
Reliability Requirements
99.9% system uptime during business hours
Automated backup systems with point-in-time recovery
Graceful error handling and recovery mechanisms
Offline capability for critical functions during network outages
Usability Requirements
Intuitive user interface requiring minimal training
Keyboard shortcuts for power users
Multi-language support (English, Mandarin, Malay, Tamil)
Accessibility compliance for users with disabilities
3. Technical Architecture
3.1 Architectural Principles
The SG POS system follows a strict layered architecture pattern with clear separation of concerns, ensuring maintainability, testability, and scalability. The architecture adheres to SOLID principles and implements proven design patterns throughout the codebase.

Layer Structure
┌─────────────────────────────────────┐
│         Presentation Layer          │
│        (PySide6 UI Components)      │
├─────────────────────────────────────┤
│       Business Logic Layer          │
│     (Managers & Core Logic)         │
├─────────────────────────────────────┤
│       Data Access Layer             │
│      (Services & Repositories)      │
├─────────────────────────────────────┤
│        Persistence Layer            │
│    (PostgreSQL Database)            │
└─────────────────────────────────────┘
3.2 Core Architectural Components
ApplicationCore - Dependency Injection Container
The ApplicationCore serves as the central dependency injection container, implementing lazy initialization patterns for optimal resource utilization. It manages the lifecycle of all manager classes and provides a unified access point for business logic components.

Key Features:

Lazy initialization using @property decorators
Unified constructor signatures across all managers
Centralized configuration management
Service locator pattern implementation
Manager Classes - Business Logic Orchestration
Manager classes encapsulate complex business workflows and coordinate multiple services without containing direct database or UI code. Each manager focuses on a specific business domain while maintaining loose coupling with other components.

Core Managers:

TransactionManager: Handles sales processing and payment workflows
InventoryManager: Manages stock operations and supplier relationships
CustomerManager: Customer data and relationship management
GSTManager: Singapore GST compliance and reporting
PaymentManager: Payment processing and financial transactions
ReportManager: Business intelligence and reporting generation
Service Classes - Data Access Abstraction
Service classes implement the Repository pattern, serving as the exclusive interface between the business logic layer and the SQLAlchemy ORM. They abstract complex query logic and provide consistent data access patterns.

Service Categories:

Entity Services: CRUD operations for core business entities
Query Services: Complex reporting and analytics queries
Integration Services: External system communication
Audit Services: Change tracking and compliance logging
3.3 Asynchronous Processing Model
The application implements a sophisticated asynchronous processing architecture to ensure responsive user interactions while handling intensive background operations.

Event Loop Management
Dedicated thread for asyncio event loop management
GUI thread isolation to prevent blocking operations
Thread-safe communication between async and UI components
Proper resource cleanup and exception handling
Background Task Processing
Queue-based task scheduling for intensive operations
Progress reporting for long-running tasks
Cancellation support for user-initiated interruptions
Retry mechanisms with exponential backoff
UI Thread Safety
QMetaObject.invokeMethod for cross-thread UI updates
Signal-slot pattern for loose coupling between components
Thread-safe data structures for shared state management
Proper synchronization primitives where necessary
4. Database Schema Design
4.1 Core Entity Relationships
The database schema is designed with normalization principles while maintaining performance considerations for high-frequency operations. The schema supports multi-tenancy, audit trails, and extensibility for future enhancements.

Primary Entities
Companies Table

CREATE TABLE companies (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE,
    gst_number VARCHAR(20),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Customers Table

CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id) ON DELETE CASCADE,
    customer_code VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(100),
    phone VARCHAR(20),
    address TEXT,
    customer_type VARCHAR(20) DEFAULT 'retail',
    credit_limit DECIMAL(15,2) DEFAULT 0.00,
    outstanding_balance DECIMAL(15,2) DEFAULT 0.00,
    loyalty_points INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_customer_code (customer_code),
    INDEX idx_customer_type (customer_type)
);

Products Table

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id) ON DELETE CASCADE,
    sku VARCHAR(100) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES product_categories(id),
    unit_price DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2),
    stock_quantity INTEGER DEFAULT 0,
    min_stock_level INTEGER DEFAULT 0,
    max_stock_level INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    gst_rate DECIMAL(5,2) DEFAULT 7.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_sku (sku),
    INDEX idx_category (category_id),
    INDEX idx_active (is_active)
);

Transactions Table

CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id) ON DELETE CASCADE,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    customer_id INTEGER REFERENCES customers(id),
    user_id INTEGER REFERENCES users(id),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    transaction_type VARCHAR(20) NOT NULL, -- 'sale', 'return', 'exchange'
    subtotal DECIMAL(15,2) NOT NULL,
    gst_amount DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0.00,
    total_amount DECIMAL(15,2) NOT NULL,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,4) DEFAULT 1.0000,
    status VARCHAR(20) DEFAULT 'completed',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_transaction_number (transaction_number),
    INDEX idx_transaction_date (transaction_date),
    INDEX idx_customer (customer_id),
    INDEX idx_status (status)
);

Transaction Items Table

CREATE TABLE transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    product_id INTEGER REFERENCES products(id),
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_percentage DECIMAL(5,2) DEFAULT 0.00,
    discount_amount DECIMAL(10,2) DEFAULT 0.00,
    subtotal DECIMAL(15,2) NOT NULL,
    gst_rate DECIMAL(5,2) NOT NULL,
    gst_amount DECIMAL(10,2) NOT NULL,
    total_amount DECIMAL(15,2) NOT NULL,
    INDEX idx_transaction (transaction_id),
    INDEX idx_product (product_id)
);

4.2 Advanced Schema Components
GST Management Tables
CREATE TABLE gst_rates (
    id SERIAL PRIMARY KEY,
    rate_name VARCHAR(50) NOT NULL,
    rate_percentage DECIMAL(5,2) NOT NULL,
    effective_from DATE NOT NULL,
    effective_to DATE,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE gst_transactions (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    gst_type VARCHAR(20) NOT NULL, -- 'standard', 'zero_rated', 'exempt'
    taxable_amount DECIMAL(15,2) NOT NULL,
    gst_rate DECIMAL(5,2) NOT NULL,
    gst_amount DECIMAL(15,2) NOT NULL,
    reporting_period VARCHAR(10) NOT NULL, -- 'YYYY-MM' format
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_reporting_period (reporting_period),
    INDEX idx_gst_type (gst_type)
);

Inventory Management Tables
CREATE TABLE stock_movements (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id) ON DELETE CASCADE,
    movement_type VARCHAR(20) NOT NULL, -- 'in', 'out', 'adjustment'
    quantity_change INTEGER NOT NULL,
    previous_quantity INTEGER NOT NULL,
    new_quantity INTEGER NOT NULL,
    unit_cost DECIMAL(10,2),
    reference_type VARCHAR(50), -- 'transaction', 'purchase_order', 'adjustment'
    reference_id INTEGER,
    notes TEXT,
    user_id INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_product (product_id),
    INDEX idx_movement_type (movement_type),
    INDEX idx_created_at (created_at)
);

CREATE TABLE purchase_orders (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id) ON DELETE CASCADE,
    po_number VARCHAR(50) UNIQUE NOT NULL,
    supplier_id INTEGER REFERENCES suppliers(id),
    order_date DATE NOT NULL,
    expected_delivery_date DATE,
    status VARCHAR(20) DEFAULT 'pending',
    subtotal DECIMAL(15,2) NOT NULL,
    gst_amount DECIMAL(15,2) NOT NULL,
    total_amount DECIMAL(15,2) NOT NULL,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

4.3 Data Integrity and Constraints
Database Triggers for Audit Trail
-- Automatic timestamp updates
CREATE OR REPLACE FUNCTION update_modified_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_customers_modtime 
    BEFORE UPDATE ON customers 
    FOR EACH ROW EXECUTE FUNCTION update_modified_column();

-- Stock quantity validation
CREATE OR REPLACE FUNCTION validate_stock_quantity()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.stock_quantity < 0 THEN
        RAISE EXCEPTION 'Stock quantity cannot be negative for product ID %', NEW.id;
    END IF;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER check_stock_quantity 
    BEFORE UPDATE ON products 
    FOR EACH ROW EXECUTE FUNCTION validate_stock_quantity();

Check Constraints
ALTER TABLE transactions ADD CONSTRAINT check_positive_amounts 
    CHECK (subtotal >= 0 AND gst_amount >= 0 AND total_amount >= 0);

ALTER TABLE transaction_items ADD CONSTRAINT check_positive_quantity 
    CHECK (quantity > 0);

ALTER TABLE customers ADD CONSTRAINT check_customer_type 
    CHECK (customer_type IN ('retail', 'wholesale', 'corporate'));

5. Application File Hierarchy
5.1 Project Root Structure
sg_pos_system/
├── app/
│   ├── __init__.py
│   ├── main.py                     # Application entry point
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py             # Configuration management
│   │   ├── database.py             # Database configuration
│   │   └── logging_config.py       # Logging setup
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py     # Dependency injection container
│   │   ├── base_classes.py         # Abstract base classes
│   │   ├── exceptions.py           # Custom exception classes
│   │   └── result.py               # Result pattern implementation
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                 # SQLAlchemy base model
│   │   ├── company.py              # Company entity model
│   │   ├── customer.py             # Customer entity model
│   │   ├── product.py              # Product entity model
│   │   ├── transaction.py          # Transaction entity models
│   │   ├── inventory.py            # Inventory-related models
│   │   ├── gst.py                  # GST-specific models
│   │   └── user.py                 # User and authentication models
│   ├── services/
│   │   ├── __init__.py
│   │   ├── base_service.py         # Base service class
│   │   ├── customer_service.py     # Customer data operations
│   │   ├── product_service.py      # Product data operations
│   │   ├── transaction_service.py  # Transaction data operations
│   │   ├── inventory_service.py    # Inventory data operations
│   │   ├── gst_service.py          # GST calculations and data
│   │   ├── reporting_service.py    # Report generation queries
│   │   └── audit_service.py        # Audit trail operations
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── base_manager.py     # Base manager class
│   │   │   ├── transaction_manager.py   # Transaction processing logic
│   │   │   ├── inventory_manager.py     # Inventory management logic
│   │   │   ├── customer_manager.py      # Customer management logic
│   │   │   ├── product_manager.py       # Product management logic
│   │   │   ├── gst_manager.py           # GST compliance logic
│   │   │   ├── payment_manager.py       # Payment processing logic
│   │   │   └── report_manager.py        # Reporting and analytics logic
│   │   ├── validators/
│   │   │   ├── __init__.py
│   │   │   ├── transaction_validator.py # Transaction validation rules
│   │   │   ├── customer_validator.py    # Customer data validation
│   │   │   └── product_validator.py     # Product data validation
│   │   └── workflows/
│   │       ├── __init__.py
│   │       ├── sales_workflow.py       # Sales process orchestration
│   │       ├── return_workflow.py      # Return process handling
│   │       └── inventory_workflow.py   # Inventory update workflows
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py          # Main application window
│   │   ├── base/
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py      # Base UI widget class
│   │   │   ├── base_dialog.py      # Base dialog class
│   │   │   └── ui_helpers.py       # UI utility functions
│   │   ├── components/
│   │   │   ├── __init__.py
│   │   │   ├── product_search.py   # Product search widget
│   │   │   ├── customer_selector.py # Customer selection widget
│   │   │   ├── payment_panel.py    # Payment processing panel
│   │   │   ├── receipt_generator.py # Receipt generation widget
│   │   │   └── reporting_charts.py # Chart components for reports
│   │   ├── windows/
│   │   │   ├── __init__.py
│   │   │   ├── pos_window.py       # Point of sale interface
│   │   │   ├── inventory_window.py # Inventory management interface
│   │   │   ├── customer_window.py  # Customer management interface
│   │   │   ├── reports_window.py   # Reports and analytics interface
│   │   │   └── settings_window.py  # System configuration interface
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── transaction_dialog.py    # Transaction details dialog
│   │   │   ├── customer_dialog.py       # Customer add/edit dialog
│   │   │   ├── product_dialog.py        # Product add/edit dialog
│   │   │   ├── payment_dialog.py        # Payment processing dialog
│   │   │   └── settings_dialog.py       # Configuration dialog
│   │   └── models/
│   │       ├── __init__.py
│   │       ├── table_models.py     # QAbstractTableModel implementations
│   │       ├── tree_models.py      # QAbstractItemModel for trees
│   │       └── list_models.py      # QAbstractListModel implementations
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── currency.py             # Currency conversion utilities
│   │   ├── gst_calculator.py       # GST calculation utilities
│   │   ├── date_helpers.py         # Date manipulation utilities
│   │   ├── validation.py           # General validation functions
│   │   ├── formatting.py           # Text and number formatting
│   │   └── async_helpers.py        # Async/await utility functions
│   └── tests/
│       ├── __init__.py
│       ├── conftest.py             # Pytest configuration
│       ├── unit/
│       │   ├── test_managers/      # Unit tests for business logic
│       │   ├── test_services/      # Unit tests for data services
│       │   └── test_utils/         # Unit tests for utilities
│       ├── integration/
│       │   ├── test_workflows/     # Integration tests for workflows
│       │   └── test_database/      # Database integration tests
│       └── ui/
│           ├── test_components/    # UI component tests
│           └── test_windows/       # Window integration tests
├── scripts/
│   ├── database/
│   │   ├── schema.sql              # Complete database schema
│   │   ├── initial_data.sql        # Seed data for development
│   │   ├── migrations/             # Database migration scripts
│   │   └── backup_restore.py       # Database backup utilities
│   ├── deployment/
│   │   ├── build.py               # Application build script
│   │   ├── package.py             # Packaging and distribution
│   │   └── installer.py           # Installation script generator
│   └── development/
│       ├── dev_server.py          # Development server setup
│       ├── test_data_generator.py # Generate test data
│       └── performance_test.py    # Performance testing utilities
├── resources/
│   ├── icons/                     # Application icons and images
│   ├── styles/                    # QSS stylesheet files
│   ├── templates/                 # Report and receipt templates
│   └── localization/              # Multi-language support files
├── docs/
│   ├── api/                       # API documentation
│   ├── user_guide/                # End-user documentation
│   ├── developer_guide/           # Developer documentation
│   └── deployment_guide/          # Deployment instructions
├── requirements/
│   ├── base.txt                   # Core dependencies
│   ├── development.txt            # Development dependencies
│   ├── testing.txt                # Testing dependencies
│   └── production.txt             # Production dependencies
├── .env.example                   # Environment variables template
├── pyproject.toml                 # Project configuration
├── README.md                      # Project overview and setup
└── LICENSE                        # Software license
5.2 Module Dependencies Diagram
┌─────────────────────────────────────────────────────────────────┐
│                          UI Layer                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Windows   │  │  Dialogs    │  │ Components  │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                  ApplicationCore                                │
│                (Dependency Injection)                          │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                Business Logic Layer                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Managers   │  │ Validators  │  │ Workflows   │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                 Data Access Layer                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Services   │  │    Utils    │  │   Models    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                PostgreSQL Database                              │
└─────────────────────────────────────────────────────────────────┘
6. Core Modules and Components
6.1 ApplicationCore Module
File: app/core/application_core.py

The ApplicationCore serves as the central dependency injection container and configuration hub for the entire application. It implements lazy initialization patterns to optimize resource usage and provides a unified access point for all business logic components.

Key Responsibilities:

Dependency injection container management
Configuration loading and validation
Database connection management
Service lifecycle management
Cross-cutting concern coordination (logging, caching, security)
Implementation Pattern:

class ApplicationCore:
    def __init__(self):
        self._config = None
        self._database_session = None
        self._managers = {}
        self._services = {}
    
    @property
    def transaction_manager(self) -> TransactionManager:
        if 'transaction_manager' not in self._managers:
            self._managers['transaction_manager'] = TransactionManager(self)
        return self._managers['transaction_manager']
    
    @property
    def customer_service(self) -> CustomerService:
        if 'customer_service' not in self._services:
            self._services['customer_service'] = CustomerService(self.database_session)
        return self._services['customer_service']

6.2 Business Logic Managers
TransactionManager
File: app/business_logic/managers/transaction_manager.py

Orchestrates the complete transaction processing workflow, from cart validation to payment processing and receipt generation. Coordinates with multiple services while maintaining transaction integrity.

Core Methods:

process_sale(cart_items, customer_info, payment_info) -> Result[Transaction]
process_return(original_transaction_id, return_items) -> Result[Transaction]
calculate_totals(cart_items, discounts) -> TransactionTotals
validate_transaction(transaction_data) -> ValidationResult
Business Rules Enforced:

GST calculation accuracy according to IRAS guidelines
Multi-currency transaction handling with proper exchange rate application
Inventory availability validation before transaction completion
Customer credit limit enforcement for B2B transactions
InventoryManager
File: app/business_logic/managers/inventory_manager.py

Manages all aspects of inventory operations including stock movements, reorder point calculations, and supplier relationship management.

Core Methods:

update_stock(product_id, quantity_change, movement_type) -> Result[StockMovement]
check_availability(product_id, required_quantity) -> bool
calculate_reorder_suggestions() -> List[ReorderSuggestion]
process_purchase_order(po_data) -> Result[PurchaseOrder]
Advanced Features:

Automated reorder point calculations based on sales velocity
Supplier performance tracking and rating system
Batch and serial number tracking for regulated products
Integrated cost calculation using FIFO/LIFO/Weighted Average methods
GSTManager
File: app/business_logic/managers/gst_manager.py

Handles all GST-related calculations and compliance requirements specific to Singapore's tax regulations.

Core Methods:

calculate_gst(amount, gst_rate, transaction_type) -> GSTCalculation
generate_gst_report(period_start, period_end) -> GSTReport
validate_gst_registration(gst_number) -> ValidationResult
get_applicable_gst_rate(product_category, transaction_date) -> Decimal
Compliance Features:

Automatic GST rate application based on product categories
Support for zero-rated and exempt transactions
IRAS-compliant reporting format generation
Multi-period GST reporting with comparative analysis
6.3 Data Access Services
BaseService
File: app/services/base_service.py

Provides common data access patterns and query optimization techniques used across all service classes.

Common Patterns:

Repository pattern implementation
Query result caching strategies
Batch operation support
Connection pooling management
TransactionService
File: app/services/transaction_service.py

Handles all database operations related to transaction processing, including complex queries for reporting and analytics.

Key Methods:

create_transaction(transaction_data) -> Result[Transaction]
get_transaction_history(customer_id, date_range) -> List[Transaction]
get_sales_analytics(period, grouping) -> SalesAnalytics
search_transactions(criteria) -> PaginatedResult[Transaction]
Query Optimization:

Indexed search capabilities for transaction lookups
Eager loading for related entities to minimize N+1 queries
Materialized views for complex reporting queries
Partitioning strategies for large transaction tables
6.4 User Interface Components
MainWindow
File: app/ui/main_window.py

The primary application window that serves as the container for all functional modules and provides the main navigation interface.

Architecture Features:

Modular widget system with lazy loading
Responsive layout management
Theme and styling support
Multi-monitor awareness
POSWindow
File: app/ui/windows/pos_window.py

The core point-of-sale interface optimized for high-frequency transaction processing.

Key Features:

Barcode scanning integration
Touch-screen optimization
Keyboard shortcut support
Real-time pricing and availability updates
Multi-tender payment processing
Receipt preview and printing
Performance Optimizations:

Cached product lookup for faster searches
Asynchronous price calculations
Background inventory availability checks
Optimized rendering for large product catalogs
ReportsWindow
File: app/ui/windows/reports_window.py

Comprehensive reporting interface with interactive charts and export capabilities.

Report Categories:

Sales performance reports
Inventory analysis reports
Customer behavior reports
Financial summary reports
GST compliance reports
Interactive Features:

Date range selection controls
Dynamic filtering and grouping
Export to multiple formats (PDF, Excel, CSV)
Printable report layouts
Scheduled report generation
6.5 Utility Modules
CurrencyUtilities
File: app/utils/currency.py

Provides comprehensive multi-currency support with real-time exchange rate management.

Features:

Exchange rate API integration
Historical rate tracking
Currency conversion calculations
Rounding rules compliance
Multi-currency reporting support
GSTCalculator
File: app/utils/gst_calculator.py

Specialized utility for Singapore GST calculations with support for various transaction types and compliance requirements.

Calculation Types:

Standard rate GST (7%)
Zero-rated supplies
Exempt supplies
Import GST calculations
Reverse charge mechanisms
7. User Interface and Interaction Flow
7.1 User Experience Design Principles
The SG POS system prioritizes usability and efficiency, recognizing that the primary users will be interacting with the system throughout their workday. The interface design follows established UX principles specifically adapted for retail environments.

Core Design Principles:

Speed and Efficiency: Minimize clicks and keystrokes for common operations
Error Prevention: Validate inputs in real-time with clear feedback
Accessibility: Support for keyboard navigation and screen readers
Consistency: Uniform interface patterns across all modules
Context Awareness: Display relevant information based on current task
7.2 Main Application Flow
Application Startup Sequence
1. Application Launch
   ├── Configuration Loading
   ├── Database Connection Validation
   ├── User Authentication
   └── Main Window Initialization

2. Main Dashboard Display
   ├── Sales Summary Widgets
   ├── Inventory Alerts
   ├── Quick Action Buttons
   └── Navigation Menu
Primary User Workflows
Sales Transaction Workflow:

Start Transaction
├── Customer Selection (Optional)
├── Product Addition Loop
│   ├── Product Search/Scan
│   ├── Quantity Selection
│   ├── Price Verification
│   └── Add to Cart
├── Discount Application (Optional)
├── Tax Calculation Display
├── Payment Processing
│   ├── Payment Method Selection
│   ├── Amount Validation
│   └── Change Calculation
├── Receipt Generation
└── Transaction Completion
Inventory Management Workflow:

Inventory Operations
├── Stock Level Monitoring
├── Product Management
│   ├── Add New Products
│   ├── Update Product Information
│   ├── Price Management
│   └── Category Assignment
├── Purchase Order Processing
│   ├── Supplier Selection
│   ├── Order Creation
│   ├── Receiving Goods
│   └── Invoice Matching
└── Stock Adjustment
    ├── Physical Count Entry
    ├── Variance Analysis
    └── Adjustment Approval
7.3 Interface Layout Specifications
Main Window Layout
┌─────────────────────────────────────────────────────────────────┐
│ Menu Bar: File | Edit | View | Tools | Reports | Help           │
├─────────────────────────────────────────────────────────────────┤
│ Toolbar: [New Sale] [Inventory] [Customers] [Reports] [Settings]│
├─────────────────┬───────────────────────────────────────────────┤
│ Navigation      │                                               │
│ Panel           │           Main Content Area                   │
│ - Dashboard     │                                               │
│ - Point of Sale │                                               │
│ - Inventory     │                                               │
│ - Customers     │                                               │
│ - Reports       │                                               │
│ - Settings      │                                               │
│                 │                                               │
├─────────────────┴───────────────────────────────────────────────┤
│ Status Bar: User | Date/Time | Database Status | Messages       │
└─────────────────────────────────────────────────────────────────┘
Point of Sale Interface Layout
┌─────────────────────────────────────────────────────────────────┐
│                    Transaction Header                           │
│ Customer: [Search/Select Customer]    Transaction #: TXN-001    │
├─────────────────────────────────────┬───────────────────────────┤
│          Product Search             │                           │
│ [Search Box] [Scan Barcode]         │     Shopping Cart         │
│                                     │                           │
│          Product List               │  Item | Qty | Price |Total│
│ ┌─────────────────────────────────┐ │  ──────────────────────── │
│ │ Product Name        | Price     │ │  Product A | 2 | $10 | $20│
│ │ Product B           | $15.50    │ │  Product B | 1 | $15 | $15│
│ │ Product C           | $8.99     │ │                           │
│ │ ...                 | ...       │ │  Subtotal:          $35.00│
│ └─────────────────────────────────┘ │  GST (7%):           $2.45│
│                                     │  Total:             $37.45│
├─────────────────────────────────────┼───────────────────────────┤
│            Quick Actions            │        Payment Panel     │
│ [Discount] [Return] [Hold] [Void]   │ [Cash] [Card] [Digital]   │
│                                     │ Amount Due:         $37.45│
│                                     │ Amount Paid:    [Entry]   │
│                                     │ Change:             $0.00 │
│                                     │ [Complete Sale]           │
└─────────────────────────────────────┴───────────────────────────┘
7.4 Responsive Design Considerations
The application supports multiple screen resolutions and can adapt to different display configurations commonly found in retail environments.

Supported Resolutions:

Minimum: 1024x768 (older POS terminals)
Standard: 1920x1080 (modern desktop displays)
Touch-optimized: 1280x800 (tablet POS systems)
Adaptive Features:

Scalable UI elements based on screen size
Touch-friendly controls with appropriate sizing
Keyboard navigation support for all functions
High contrast mode for improved visibility
8. Technology Stack
8.1 Core Technologies
Python 3.11+
Role: Primary programming language and runtime environment Justification: Python provides excellent ecosystem support for business applications, with robust libraries for database interaction, GUI development, and business logic implementation. The 3.11+ requirement ensures access to the latest performance improvements and security features.

Key Features Utilized:

Type hints for improved code maintainability
Async/await support for non-blocking operations
Dataclasses for efficient data structure definitions
Context managers for resource management
Extensive standard library for common operations
PySide6 (Qt 6)
Role: Cross-platform GUI framework Justification: PySide6 provides professional-grade desktop application development capabilities with native look and feel across different operating systems. Qt's mature ecosystem offers comprehensive widgets and tools for building sophisticated user interfaces.

Components Used:

QtWidgets: Core UI components and layouts
QtCore: Event handling, threading, and core functionality
QtGui: Graphics, fonts, and visual elements
QtCharts: Data visualization and reporting charts
QtPrintSupport: Receipt and report printing capabilities
QtSql: Database connectivity (supplementary to SQLAlchemy)
PostgreSQL 14+
Role: Primary data storage and management system Justification: PostgreSQL offers enterprise-grade reliability, ACID compliance, and advanced features required for business-critical applications. Its robust concurrency control and extensibility make it ideal for POS systems.

Features Leveraged:

Full ACID compliance for transaction integrity
Advanced indexing for query performance optimization
Triggers and stored procedures for business rule enforcement
Partitioning for large table management
JSON support for flexible data structures
Robust backup and recovery mechanisms
SQLAlchemy 2.0+
Role: Object-Relational Mapping (ORM) and database abstraction Justification: SQLAlchemy provides a Pythonic interface to database operations while maintaining the flexibility to optimize performance-critical queries. The 2.0 version offers improved async support and modern API design.

Usage Patterns:

Declarative models for database schema definition
Session management for transaction control
Query optimization through relationship loading strategies
Migration support through Alembic integration
Connection pooling for performance optimization
8.2 Supporting Libraries and Frameworks
Async Framework
asyncio: Native Python async/await support for non-blocking operations
QAsync: Qt integration for async operations in GUI applications
Data Processing
pandas: Data analysis and reporting computations
numpy: Numerical calculations for financial and statistical operations
Decimal: Precise decimal arithmetic for monetary calculations
Configuration and Environment
pydantic: Data validation and settings management
python-dotenv: Environment variable management
configparser: Configuration file parsing and management
Testing Framework
pytest: Primary testing framework with comprehensive plugin ecosystem
pytest-asyncio: Async test support
pytest-qt: Qt application testing utilities
factory-boy: Test data generation and management
coverage: Code coverage analysis and reporting
Development Tools
black: Code formatting and style consistency
isort: Import statement organization
mypy: Static type checking and validation
pre-commit: Git hook management for code quality
sphinx: Documentation generation and management
8.3 Architecture Integration
Database Layer Integration
# SQLAlchemy session management with async support
from sqlalchemy.ext.asyncio import AsyncSession, create_async_engine
from sqlalchemy.orm import sessionmaker

class DatabaseManager:
    def __init__(self, connection_string: str):
        self.engine = create_async_engine(connection_string)
        self.session_factory = sessionmaker(
            self.engine, class_=AsyncSession, expire_on_commit=False
        )
    
    async def get_session(self) -> AsyncSession:
        async with self.session_factory() as session:
            yield session

Qt-Python Integration Patterns
# Async operation integration with Qt signals
class AsyncWorker(QObject):
    finished = Signal(object)
    error = Signal(str)
    
    def __init__(self, coro):
        super().__init__()
        self.coro = coro
    
    async def run(self):
        try:
            result = await self.coro
            self.finished.emit(result)
        except Exception as e:
            self.error.emit(str(e))

8.4 Performance Considerations
Memory Management
Connection pooling to minimize database connection overhead
Lazy loading of UI components to reduce startup time
Efficient data structures for high-frequency operations
Garbage collection optimization for long-running sessions
Query Optimization
Database indexing strategy for common query patterns
Eager loading configuration for related entities
Query result caching for frequently accessed data
Batch operations for bulk data processing
UI Responsiveness
Async operations for database interactions
Background threading for intensive computations
Progressive loading for large datasets
Optimized rendering for data grids and charts
9. Development Environment Setup
9.1 System Requirements
Hardware Requirements
CPU: Multi-core processor (4+ cores recommended)
RAM: 8GB minimum, 16GB recommended
Storage: 20GB free space for development environment
Display: 1920x1080 or higher resolution
Operating System Support
Windows: Windows 10/11 (64-bit)
macOS: macOS 11+ (Intel or Apple Silicon)
Linux: Ubuntu 20.04+, Fedora 35+, or equivalent
9.2 Development Environment Configuration
Python Environment Setup
# Install Python 3.11+ using pyenv (recommended)
curl https://pyenv.run | bash
pyenv install 3.11.8
pyenv global 3.11.8

# Verify installation
python --version  # Should output Python 3.11.8

# Create virtual environment
python -m venv sg_pos_venv
source sg_pos_venv/bin/activate  # Linux/macOS
# sg_pos_venv\Scripts\activate.bat  # Windows

# Upgrade pip and install build tools
pip install --upgrade pip setuptools wheel

Project Dependencies Installation
# Clone the repository
git clone https://github.com/company/sg-pos-system.git
cd sg-pos-system

# Install development dependencies
pip install -r requirements/development.txt

# Install pre-commit hooks
pre-commit install

# Verify installation
python -m pytest --version
black --version
mypy --version

Database Setup for Development
# Install PostgreSQL using package manager
# Ubuntu/Debian
sudo apt update
sudo apt install postgresql postgresql-contrib

# macOS (using Homebrew)
brew install postgresql
brew services start postgresql

# Windows: Download installer from postgresql.org

# Create development database
sudo -u postgres createuser --createdb --login sg_pos_dev
sudo -u postgres createdb sg_pos_development -O sg_pos_dev

# Set password for development user
sudo -u postgres psql
postgres=# ALTER USER sg_pos_dev PASSWORD 'dev_password_2024';
postgres=# \q

Environment Configuration
# Copy environment template
cp .env.example .env

# Edit .env file with development settings
DATABASE_URL=postgresql://sg_pos_dev:dev_password_2024@localhost/sg_pos_development
DEBUG=True
LOG_LEVEL=DEBUG
SECRET_KEY=your-development-secret-key
ENVIRONMENT=development

Database Schema Initialization
# Initialize database schema
python scripts/database/init_dev_db.py

# Load sample data for development
python scripts/development/load_test_data.py

# Verify database setup
python -c "from app.core.application_core import ApplicationCore; print('Database connection successful')"

9.3 IDE Configuration
Recommended IDE: PyCharm Professional
Configuration Steps:

Create new project from existing sources
Configure Python interpreter to use virtual environment
Set up database connection in Database tool window
Configure code style to use Black
