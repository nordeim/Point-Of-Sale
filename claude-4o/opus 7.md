This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore-focused Point-of-Sale system. The user has provided excellent architectural context and wants a detailed, professional-grade document that covers all aspects of the system design and implementation.

Key requirements to address:
1. Comprehensive PRD in markdown format (6000+ words)
2. Database schema design
3. Codebase file hierarchy diagram
4. Application modules and user interaction diagrams
5. Detailed descriptions of key modules and files
6. Technology stack specification
7. Development and production environment setup
8. Architecture that demonstrates layered design, async processing, data integrity
9. Best practices like Dependency Injection, DTOs, Result patterns

I need to structure this as a professional PRD that would guide actual development, leaving no ambiguity about implementation details.

Let me organize this into logical sections:
- Executive Summary
- Product Overview & Goals
- Functional Requirements
- Technical Architecture
- Database Schema Design
- Codebase Structure
- Application Modules
- User Interface Design
- Technology Stack
- Environment Setup
- Security & Compliance
- Performance Requirements
- Quality Assurance
- Implementation Timeline
- Future Considerations

I'll make this comprehensive and detailed, ensuring it meets the word count while providing actionable technical specifications.
</think>

# Product Requirements Document: SG Point-of-Sale (POS) System

## Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) operating in Singapore's retail environment. This enterprise-grade solution combines modern UI/UX principles with robust backend architecture to deliver a professional retail management platform that addresses the unique regulatory, tax, and operational requirements of the Singapore market.

Built on a foundation of Python 3.11+, PySide6, and PostgreSQL, the system implements a clean layered architecture with asynchronous processing capabilities, ensuring scalability, maintainability, and exceptional performance. The application serves as a complete business management solution, encompassing point-of-sale transactions, inventory management, customer relationship management, financial reporting, and regulatory compliance.

The primary objective is to deliver a production-ready system that can handle real-world business complexity while maintaining code quality, architectural integrity, and user experience excellence. The system is designed to grow with businesses, supporting multiple locations, various payment methods, comprehensive reporting, and integration capabilities with Singapore's regulatory systems.

## Product Overview and Goals

### Primary Objectives

The SG POS System aims to revolutionize retail operations for Singapore-based businesses by providing:

**Operational Excellence**: Streamline daily retail operations through intuitive interfaces, automated processes, and real-time data synchronization across all business functions.

**Regulatory Compliance**: Ensure full compliance with Singapore's tax regulations, including GST requirements, IRAS reporting standards, and consumer protection laws.

**Business Intelligence**: Provide comprehensive analytics and reporting capabilities that enable data-driven decision making and business growth optimization.

**Scalability**: Support business growth from single-location operations to multi-branch enterprises with centralized management capabilities.

### Target Market

The system targets Singapore-based SMBs in retail sectors including:
- General merchandise stores
- Food and beverage establishments
- Fashion and apparel retailers
- Electronics and technology stores
- Specialty retail businesses
- Service-based businesses with retail components

### Key Value Propositions

**Localized for Singapore**: Built specifically for Singapore's business environment, incorporating local tax structures, payment methods, and regulatory requirements.

**Enterprise-Grade Architecture**: Professional software architecture ensuring reliability, performance, and maintainability at scale.

**Modern User Experience**: Contemporary UI design following current usability standards, ensuring minimal training requirements and high user adoption.

**Comprehensive Integration**: Seamless integration with local payment processors, accounting systems, and government reporting requirements.

## Functional Requirements

### Core POS Operations

**Transaction Processing**: The system must support complete sales transaction workflows including item scanning/selection, pricing calculations, discount applications, tax computations, and payment processing. Multi-tender transactions, partial payments, and complex promotional pricing must be handled seamlessly.

**Inventory Management**: Real-time inventory tracking with automatic stock level updates, reorder point notifications, supplier management, and purchase order generation. The system must support various inventory valuation methods including FIFO, LIFO, and weighted average costing.

**Customer Management**: Comprehensive customer database with contact information, purchase history, loyalty program integration, and customer analytics. Support for corporate accounts, credit limits, and customer-specific pricing.

**Payment Processing**: Integration with multiple payment methods including cash, credit cards, debit cards, digital wallets, and Singapore-specific payment systems like PayNow and NETS. Support for split payments, refunds, and payment plan arrangements.

### Financial Management

**GST Compliance**: Automated GST calculation, reporting, and submission capabilities aligned with IRAS requirements. Support for different GST rates, exemptions, and zero-rated supplies.

**Financial Reporting**: Comprehensive financial reporting including profit and loss statements, balance sheets, cash flow reports, and tax reports. Real-time financial dashboards with key performance indicators.

**Accounting Integration**: Chart of accounts management, general ledger functionality, and integration capabilities with external accounting systems.

### Advanced Features

**Multi-Location Support**: Centralized management of multiple retail locations with location-specific reporting, inventory allocation, and performance tracking.

**Employee Management**: User account management with role-based access control, time tracking, commission calculations, and performance monitoring.

**Reporting and Analytics**: Advanced business intelligence capabilities including sales analytics, customer behavior analysis, inventory optimization reports, and predictive analytics.

**Backup and Recovery**: Automated data backup, disaster recovery procedures, and data integrity verification systems.

## Technical Architecture

### Architectural Principles

The SG POS System implements a sophisticated layered architecture designed for enterprise-level reliability, maintainability, and scalability. The architecture follows established software engineering principles including separation of concerns, dependency inversion, and single responsibility principle.

**Presentation Layer**: Handles all user interface interactions using PySide6 widgets and custom UI components. This layer is responsible for data presentation, user input validation, and UI state management while delegating all business logic to lower layers.

**Business Logic Layer**: Contains the core business rules, workflow orchestration, and domain-specific logic. This layer is framework-agnostic and focuses purely on business requirements implementation.

**Data Access Layer**: Implements the Repository pattern for data persistence operations, providing a clean abstraction over the database layer and supporting multiple data sources.

**Infrastructure Layer**: Handles cross-cutting concerns including logging, configuration management, security, and external service integration.

### Asynchronous Processing Model

The application implements a robust asynchronous processing architecture to ensure responsive user experience and efficient resource utilization:

**Event Loop Integration**: A dedicated thread manages the asyncio event loop, preventing I/O operations from blocking the GUI thread.

**Task Scheduling**: Background tasks are scheduled through a thread-safe bridge that coordinates between Qt's signal-slot mechanism and Python's async/await paradigm.

**UI Thread Safety**: All UI updates from background operations are marshaled back to the main thread using Qt's meta-object system, ensuring thread safety and preventing race conditions.

### Data Integrity and Consistency

**Transaction Management**: Database operations are wrapped in transactions with proper rollback mechanisms to ensure data consistency.

**Referential Integrity**: Foreign key constraints and database triggers enforce data integrity at the persistence layer.

**Validation Framework**: Multi-layer validation including client-side validation, business rule validation, and database constraint validation.

## Database Schema Design

### Core Entity Structure

The database schema is designed to support complex retail operations while maintaining data integrity and query performance. The schema follows third normal form principles with strategic denormalization for performance optimization.

```sql
-- Core Business Entities

CREATE TABLE companies (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE,
    gst_registration_number VARCHAR(50),
    address TEXT,
    postal_code VARCHAR(10),
    phone VARCHAR(20),
    email VARCHAR(255),
    website VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    company_id INTEGER REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    address TEXT,
    postal_code VARCHAR(10),
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- User Management
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(100) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    role VARCHAR(50) NOT NULL,
    location_id INTEGER REFERENCES locations(id),
    is_active BOOLEAN DEFAULT TRUE,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Customer Management
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(50) UNIQUE,
    company_name VARCHAR(255),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    customer_type VARCHAR(50) DEFAULT 'individual',
    credit_limit DECIMAL(15,2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0,
    gst_registration_number VARCHAR(50),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Product and Inventory Management
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    parent_id INTEGER REFERENCES categories(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(100) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    unit_of_measure VARCHAR(20) DEFAULT 'each',
    cost_price DECIMAL(15,4),
    selling_price DECIMAL(15,2) NOT NULL,
    gst_rate DECIMAL(5,2) DEFAULT 7.00,
    is_gst_inclusive BOOLEAN DEFAULT FALSE,
    barcode VARCHAR(100),
    minimum_stock_level INTEGER DEFAULT 0,
    maximum_stock_level INTEGER,
    reorder_point INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    location_id INTEGER REFERENCES locations(id),
    quantity_on_hand INTEGER DEFAULT 0,
    quantity_allocated INTEGER DEFAULT 0,
    quantity_available INTEGER GENERATED ALWAYS AS (quantity_on_hand - quantity_allocated) STORED,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location_id)
);

-- Sales Transaction Management
CREATE TABLE sales_transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    location_id INTEGER REFERENCES locations(id),
    customer_id INTEGER REFERENCES customers(id),
    user_id INTEGER REFERENCES users(id),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    subtotal DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    gst_amount DECIMAL(15,2) DEFAULT 0,
    total_amount DECIMAL(15,2) NOT NULL,
    payment_status VARCHAR(20) DEFAULT 'pending',
    transaction_status VARCHAR(20) DEFAULT 'active',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE sales_transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES sales_transactions(id),
    product_id INTEGER REFERENCES products(id),
    quantity DECIMAL(10,3) NOT NULL,
    unit_price DECIMAL(15,2) NOT NULL,
    discount_amount DECIMAL(15,2) DEFAULT 0,
    gst_rate DECIMAL(5,2) NOT NULL,
    gst_amount DECIMAL(15,2) DEFAULT 0,
    line_total DECIMAL(15,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES sales_transactions(id),
    payment_method VARCHAR(50) NOT NULL,
    payment_reference VARCHAR(255),
    amount DECIMAL(15,2) NOT NULL,
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'completed',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Financial and Accounting
CREATE TABLE chart_of_accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL,
    parent_account_id INTEGER REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT,
    reference VARCHAR(255),
    total_debit DECIMAL(15,2) DEFAULT 0,
    total_credit DECIMAL(15,2) DEFAULT 0,
    status VARCHAR(20) DEFAULT 'draft',
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    posted_at TIMESTAMP
);

CREATE TABLE journal_entry_lines (
    id SERIAL PRIMARY KEY,
    journal_entry_id INTEGER REFERENCES journal_entries(id),
    account_id INTEGER REFERENCES chart_of_accounts(id),
    description TEXT,
    debit_amount DECIMAL(15,2) DEFAULT 0,
    credit_amount DECIMAL(15,2) DEFAULT 0,
    line_number INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Configuration and System Management
CREATE TABLE system_settings (
    id SERIAL PRIMARY KEY,
    key VARCHAR(100) UNIQUE NOT NULL,
    value TEXT,
    data_type VARCHAR(20) DEFAULT 'string',
    description TEXT,
    is_encrypted BOOLEAN DEFAULT FALSE,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE audit_logs (
    id SERIAL PRIMARY KEY,
    table_name VARCHAR(100) NOT NULL,
    record_id INTEGER NOT NULL,
    action VARCHAR(20) NOT NULL,
    old_values JSONB,
    new_values JSONB,
    user_id INTEGER REFERENCES users(id),
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Database Triggers and Constraints

```sql
-- Audit Trail Triggers
CREATE OR REPLACE FUNCTION audit_trigger_function()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        INSERT INTO audit_logs (table_name, record_id, action, new_values, user_id)
        VALUES (TG_TABLE_NAME, NEW.id, 'INSERT', to_jsonb(NEW), CURRENT_USER_ID());
        RETURN NEW;
    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO audit_logs (table_name, record_id, action, old_values, new_values, user_id)
        VALUES (TG_TABLE_NAME, NEW.id, 'UPDATE', to_jsonb(OLD), to_jsonb(NEW), CURRENT_USER_ID());
        RETURN NEW;
    ELSIF TG_OP = 'DELETE' THEN
        INSERT INTO audit_logs (table_name, record_id, action, old_values, user_id)
        VALUES (TG_TABLE_NAME, OLD.id, 'DELETE', to_jsonb(OLD), CURRENT_USER_ID());
        RETURN OLD;
    END IF;
    RETURN NULL;
END;
$$ LANGUAGE plpgsql;

-- Inventory Update Triggers
CREATE OR REPLACE FUNCTION update_inventory_on_sale()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE inventory 
    SET quantity_on_hand = quantity_on_hand - NEW.quantity,
        last_updated = CURRENT_TIMESTAMP
    WHERE product_id = NEW.product_id 
    AND location_id = (SELECT location_id FROM sales_transactions WHERE id = NEW.transaction_id);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER sales_inventory_update_trigger
    AFTER INSERT ON sales_transaction_items
    FOR EACH ROW EXECUTE FUNCTION update_inventory_on_sale();
```

## Codebase Structure and File Hierarchy

### Project Structure Overview

The codebase follows a clean, layered architecture with clear separation of concerns and logical organization of components:

```
sg_pos_system/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py                  # Configuration management
│   │   ├── database.py                  # Database configuration
│   │   └── logging_config.py            # Logging configuration
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py          # Dependency injection container
│   │   ├── base_manager.py              # Base class for business managers
│   │   ├── exceptions.py                # Custom exception classes
│   │   ├── result.py                    # Result pattern implementation
│   │   └── async_bridge.py              # Qt-AsyncIO bridge
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                      # SQLAlchemy base model
│   │   ├── company.py                   # Company and location models
│   │   ├── user.py                      # User management models
│   │   ├── customer.py                  # Customer models
│   │   ├── product.py                   # Product and inventory models
│   │   ├── sales.py                     # Sales transaction models
│   │   ├── payment.py                   # Payment models
│   │   ├── accounting.py                # Accounting and financial models
│   │   └── system.py                    # System configuration models
│   ├── services/
│   │   ├── __init__.py
│   │   ├── base_service.py              # Base repository class
│   │   ├── company_service.py           # Company data access
│   │   ├── user_service.py              # User data access
│   │   ├── customer_service.py          # Customer data access
│   │   ├── product_service.py           # Product data access
│   │   ├── inventory_service.py         # Inventory data access
│   │   ├── sales_service.py             # Sales transaction data access
│   │   ├── payment_service.py           # Payment data access
│   │   ├── accounting_service.py        # Accounting data access
│   │   └── system_service.py            # System configuration data access
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── customer_manager.py          # Customer business logic
│   │   ├── product_manager.py           # Product business logic
│   │   ├── inventory_manager.py         # Inventory business logic
│   │   ├── sales_manager.py             # Sales transaction business logic
│   │   ├── payment_manager.py           # Payment processing business logic
│   │   ├── reporting_manager.py         # Reporting business logic
│   │   └── user_manager.py              # User management business logic
│   ├── accounting/
│   │   ├── __init__.py
│   │   ├── gst_manager.py               # GST calculation and reporting
│   │   ├── chart_of_accounts_manager.py # Chart of accounts management
│   │   ├── journal_entry_manager.py     # Journal entry management
│   │   └── financial_reports_manager.py # Financial reporting
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py               # Main application window
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── pos_widget.py            # Point of sale interface
│   │   │   ├── inventory_widget.py      # Inventory management interface
│   │   │   ├── customer_widget.py       # Customer management interface
│   │   │   ├── reports_widget.py        # Reporting interface
│   │   │   ├── settings_widget.py       # System settings interface
│   │   │   └── dashboard_widget.py      # Dashboard interface
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── product_dialog.py        # Product add/edit dialog
│   │   │   ├── customer_dialog.py       # Customer add/edit dialog
│   │   │   ├── payment_dialog.py        # Payment processing dialog
│   │   │   ├── settings_dialog.py       # Settings configuration dialog
│   │   │   └── about_dialog.py          # About application dialog
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── table_models.py          # Qt table models
│   │   │   ├── tree_models.py           # Qt tree models
│   │   │   └── list_models.py           # Qt list models
│   │   └── utils/
│   │       ├── __init__.py
│   │       ├── validators.py            # UI input validators
│   │       ├── formatters.py            # Data formatters
│   │       └── themes.py                # UI theming utilities
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── datetime_utils.py            # Date/time utilities
│   │   ├── number_utils.py              # Number formatting utilities
│   │   ├── security_utils.py            # Security and encryption utilities
│   │   ├── export_utils.py              # Data export utilities
│   │   └── validation_utils.py          # Data validation utilities
│   └── integrations/
│       ├── __init__.py
│       ├── payment_gateways/
│       │   ├── __init__.py
│       │   ├── base_gateway.py          # Base payment gateway interface
│       │   ├── nets_gateway.py          # NETS payment integration
│       │   └── paynow_gateway.py        # PayNow integration
│       ├── accounting_systems/
│       │   ├── __init__.py
│       │   └── quickbooks_integration.py # QuickBooks integration
│       └── government_systems/
│           ├── __init__.py
│           └── iras_integration.py      # IRAS reporting integration
├── scripts/
│   ├── database/
│   │   ├── schema.sql                   # Database schema creation
│   │   ├── initial_data.sql             # Initial data seeding
│   │   ├── migrations/                  # Database migration scripts
│   │   └── backup_restore.py            # Database backup/restore utilities
│   ├── deployment/
│   │   ├── build_installer.py           # Application installer builder
│   │   ├── docker_setup.py              # Docker containerization
│   │   └── environment_setup.py         # Environment configuration
│   └── development/
│       ├── generate_test_data.py        # Test data generation
│       ├── database_tools.py            # Database management tools
│       └── code_generators.py           # Code generation utilities
├── tests/
│   ├── __init__.py
│   ├── conftest.py                      # Pytest configuration
│   ├── unit/
│   │   ├── test_business_logic/         # Business logic unit tests
│   │   ├── test_services/               # Service layer unit tests
│   │   └── test_utils/                  # Utility function tests
│   ├── integration/
│   │   ├── test_database/               # Database integration tests
│   │   ├── test_api/                    # API integration tests
│   │   └── test_ui/                     # UI integration tests
│   └── e2e/
│       └── test_workflows/              # End-to-end workflow tests
├── docs/
│   ├── api/                             # API documentation
│   ├── user_manual/                     # User documentation
│   ├── developer_guide/                 # Developer documentation
│   └── deployment_guide/                # Deployment documentation
├── resources/
│   ├── icons/                           # Application icons
│   ├── images/                          # UI images and graphics
│   ├── styles/                          # Qt stylesheets
│   └── translations/                    # Internationalization files
├── requirements/
│   ├── base.txt                         # Base requirements
│   ├── development.txt                  # Development requirements
│   └── production.txt                   # Production requirements
├── .env.example                         # Environment variables template
├── .gitignore                          # Git ignore rules
├── setup.py                            # Package setup configuration
├── pyproject.toml                      # Python project configuration
└── README.md                           # Project documentation
```

### Key Architecture Files

**application_core.py**: The central dependency injection container implementing lazy initialization of all business managers and services. This class serves as the single point of access for all application components and manages their lifecycles.

**base_manager.py**: Abstract base class defining the common interface for all business logic managers. Implements common patterns like logging, error handling, and result wrapping.

**base_service.py**: Abstract base class for all data access services implementing the Repository pattern. Provides common database operations and query building functionality.

**result.py**: Implementation of the Result pattern for consistent error handling across the application. Eliminates the need for exception-based control flow in business logic.

**async_bridge.py**: Thread-safe bridge between Qt's signal-slot mechanism and Python's async/await paradigm, enabling seamless integration of asynchronous operations with the GUI.

## Application Modules and Components

### Core Application Modules

#### Application Core Module

The Application Core serves as the central nervous system of the application, implementing a sophisticated dependency injection container with lazy initialization capabilities.

**Key Responsibilities**:
- Manages the lifecycle of all business managers and services
- Provides centralized access to application components
- Implements lazy loading to optimize startup performance
- Manages database connections and transaction contexts
- Coordinates cross-cutting concerns like logging and configuration

**Implementation Details**:
```python
class ApplicationCore:
    def __init__(self, database_url: str, config: Dict[str, Any]):
        self._database_url = database_url
        self._config = config
        self._engine = None
        self._session_factory = None
        self._managers = {}
        self._services = {}
    
    @property
    def customer_manager(self) -> CustomerManager:
        if 'customer_manager' not in self._managers:
            self._managers['customer_manager'] = CustomerManager(self)
        return self._managers['customer_manager']
    
    # Similar properties for all other managers...
```

#### Business Logic Layer

The business logic layer contains manager classes that orchestrate complex business workflows and enforce business rules.

**Customer Manager**: Handles all customer-related operations including registration, profile management, loyalty program integration, and customer analytics. Implements sophisticated customer segmentation and targeted marketing capabilities.

**Sales Manager**: Manages the complete sales transaction lifecycle from cart creation to payment completion. Handles complex pricing rules, promotional discounts, tax calculations, and multi-tender transactions.

**Inventory Manager**: Provides comprehensive inventory management including stock tracking, reorder point management, supplier relationships, and inventory valuation. Implements various costing methods and supports multi-location inventory.

**Payment Manager**: Orchestrates payment processing workflows integrating with multiple payment gateways. Handles payment validation, fraud detection, refund processing, and payment plan management.

**Reporting Manager**: Generates comprehensive business reports including sales analytics, inventory reports, financial statements, and compliance reports. Implements real-time dashboard updates and scheduled report generation.

#### Data Access Layer

The data access layer implements the Repository pattern, providing clean abstractions over database operations.

**Service Architecture**: Each service class corresponds to a specific domain entity and provides CRUD operations, complex queries, and data aggregation functionality. Services are stateless and thread-safe, supporting concurrent access patterns.

**Transaction Management**: Services implement proper transaction management with automatic rollback on errors. Support for nested transactions and transaction scoping across multiple operations.

**Query Optimization**: Services implement intelligent query optimization including eager loading, query batching, and result caching to minimize database round trips.

### User Interface Architecture

#### Main Window Framework

The main application window implements a modern ribbon-style interface with contextual tabs and integrated search functionality.

**Navigation System**: Hierarchical navigation with breadcrumb trails, recently accessed items, and bookmark functionality. Support for keyboard shortcuts and customizable toolbars.

**Widget Management**: Dynamic widget loading and unloading to optimize memory usage. Support for floating windows, dockable panels, and custom workspace layouts.

**State Management**: Automatic saving and restoration of user preferences, window layouts, and application state. Support for user profiles and role-based interface customization.

#### Specialized UI Components

**POS Widget**: Touch-optimized point of sale interface with large buttons, visual product selection, and integrated payment processing. Support for barcode scanning, receipt printing, and customer display integration.

**Inventory Widget**: Comprehensive inventory management interface with advanced filtering, bulk operations, and visual stock level indicators. Integration with supplier catalogs and automated reordering.

**Reports Widget**: Interactive reporting interface with drill-down capabilities, export options, and real-time data updates. Support for custom report creation and scheduled report delivery.

**Dashboard Widget**: Executive dashboard with key performance indicators, trend analysis, and actionable insights. Customizable widgets and real-time data visualization.

### Integration Modules

#### Payment Gateway Integration

**NETS Integration**: Full integration with Singapore's NETS payment system supporting various card types, contactless payments, and mobile payments. Handles payment authorization, settlement, and reconciliation.

**PayNow Integration**: Integration with Singapore's PayNow instant payment system enabling QR code payments and mobile wallet integration. Support for merchant-presented and customer-presented QR codes.

**Credit Card Processing**: Integration with major credit card processors supporting EMV chip cards, contactless payments, and online authorization. PCI compliance implementation for secure card data handling.

#### Government System Integration

**IRAS Integration**: Automated GST reporting and submission to Singapore's Inland Revenue Authority. Support for GST F5 returns, tax computation, and electronic filing.

**ACRA Integration**: Integration with Singapore's Accounting and Corporate Regulatory Authority for business registration verification and compliance reporting.

#### Third-Party System Integration

**Accounting System Integration**: Seamless integration with popular accounting systems including QuickBooks, Xero, and MYOB. Automated journal entry creation and financial data synchronization.

**E-commerce Platform Integration**: Integration with major e-commerce platforms for unified inventory management and order processing across online and offline channels.

## User Interface Design

### Design Philosophy

The user interface design follows modern UX principles emphasizing clarity, efficiency, and accessibility. The design system implements a clean, professional aesthetic suitable for business environments while maintaining usability across different user skill levels.

**Visual Hierarchy**: Clear information hierarchy using typography, color, and spacing to guide user attention and facilitate quick information scanning.

**Consistency**: Standardized UI patterns, terminology, and interactions across all application modules to minimize learning curve and reduce user errors.

**Accessibility**: Full compliance with WCAG 2.1 guidelines including keyboard navigation, screen reader support, and high contrast modes.

### Interface Layout

#### Main Application Window

The main window implements a modern ribbon interface with contextual functionality and intelligent space utilization:

**Header Area**: Company branding, user account information, global search, and system notifications. Quick access to frequently used functions and help resources.

**Navigation Ribbon**: Context-sensitive ribbon tabs that display relevant functionality based on the current active module. Collapsible ribbon for maximizing workspace area.

**Content Area**: Main workspace with tab-based navigation supporting multiple concurrent workflows. Support for split-screen viewing and floating windows.

**Status Bar**: Real-time system status, connection indicators, background task progress, and contextual help information.

**Side Panels**: Collapsible side panels for quick access tools, recently accessed items, and contextual information related to current tasks.

#### Module-Specific Interfaces

**Point of Sale Interface**: Optimized for touch interaction with large buttons, visual product selection grid, and integrated customer display. Support for multiple payment methods and receipt options.

**Inventory Management Interface**: Comprehensive product catalog with advanced filtering, sorting, and bulk operation capabilities. Visual stock level indicators and reorder point alerts.

**Customer Management Interface**: Customer database with advanced search, customer history, and communication tools. Integration with loyalty programs and marketing campaigns.

**Reporting Interface**: Interactive dashboard with customizable widgets, drill-down capabilities, and export options. Real-time data updates and automated report scheduling.

### Responsive Design

The interface implements responsive design principles to support various screen sizes and orientations:

**Adaptive Layouts**: Interface elements automatically adjust to available screen space while maintaining functionality and usability.

**Scalable Typography**: Font sizes and UI elements scale appropriately for different screen densities and user preferences.

**Touch Optimization**: Touch-friendly interface elements with appropriate sizing and spacing for tablet and touch screen usage.

## Technology Stack

### Core Technologies

**Python 3.11+**: Selected for its mature ecosystem, extensive library support, and strong community. Python provides excellent development productivity while maintaining performance for business applications.

**PySide6 (Qt 6.x)**: Chosen for its comprehensive widget set, native look-and-feel across platforms, and professional UI capabilities. Qt provides excellent performance, extensive theming support, and robust internationalization.

**PostgreSQL 15+**: Enterprise-grade relational database providing ACID compliance, advanced querying capabilities, and excellent performance. PostgreSQL offers strong data integrity features and extensive extension ecosystem.

**SQLAlchemy 2.0**: Modern Python ORM providing sophisticated object-relational mapping, query optimization, and database abstraction. Supports both Core and ORM interfaces for optimal performance.

### Supporting Libraries and Frameworks

**Asyncio**: Python's built-in asynchronous programming framework enabling responsive UI and efficient I/O operations. Provides coroutine support and event loop management.

**Pydantic**: Data validation and serialization library ensuring type safety and data integrity. Provides automatic validation and clear error messages.

**Alembic**: Database migration tool for SQLAlchemy providing version control for database schema changes. Supports both automatic and manual migration generation.

**pytest**: Comprehensive testing framework supporting unit tests, integration tests, and end-to-end testing. Extensive plugin ecosystem and fixture support.

**Black**: Code formatting tool ensuring consistent code style across the entire codebase. Automatic formatting reduces code review overhead and maintains readability.

**mypy**: Static type checker providing compile-time type validation and catching potential runtime errors. Improves code reliability and development efficiency.

### Development Tools

**Poetry**: Modern Python dependency management and packaging tool providing deterministic builds and virtual environment management.

**pre-commit**: Git hook framework ensuring code quality standards are maintained through automated checks before commits.

**pylint**: Comprehensive code analysis tool identifying potential errors, code smells, and style violations.

**pytest-cov**: Code coverage analysis tool ensuring comprehensive test coverage and identifying untested code paths.

### Production Infrastructure

**Docker**: Containerization platform providing consistent deployment environments and simplified application distribution.

**PostgreSQL Connection Pooling**: pgBouncer for efficient database connection management and resource optimization.

**Logging Framework**: Structured logging using Python's logging module with configurable handlers for file, console, and remote logging.

**Configuration Management**: Environment-based configuration using environment variables and configuration files for different deployment scenarios.

## Environment Setup

### Development Environment Setup

#### Prerequisites Installation

**Python Environment Setup**:
```bash
# Install Python 3.11+ using pyenv for version management
curl https://pyenv.run | bash
pyenv install 3.11.7
pyenv global 3.11.7

# Install Poetry for dependency management
curl -sSL https://install.python-poetry.org | python3 -
export PATH="$HOME/.local/bin:$PATH"
```

**Database Setup**:
```bash
# Install PostgreSQL 15
# On Ubuntu/Debian:
sudo apt update
sudo apt install postgresql-15 postgresql-contrib-15

# On macOS:
brew install postgresql@15

# Start PostgreSQL service
sudo systemctl start postgresql
# or on macOS:
brew services start postgresql@15

# Create development database
sudo -u postgres createdb sg_pos_dev
sudo -u postgres psql -c "CREATE USER sg_pos_user WITH PASSWORD 'dev_password';"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE sg_pos_dev TO sg_pos_user;"
```

#### Project Setup

**Repository Clone and Environment Setup**:
```bash
# Clone the repository
git clone https://github.com/your-org/sg-pos-system.git
cd sg-pos-system

# Install project dependencies
poetry install --with dev

# Activate virtual environment
poetry shell

# Copy environment configuration
cp .env.example .env

# Edit .env file with development settings
DATABASE_URL=postgresql://sg_pos_user:dev_password@localhost:5432/sg_pos_dev
DEBUG=True
LOG_LEVEL=DEBUG
SECRET_KEY=your-development-secret-key
```

**Database Schema Creation**:
```bash
# Initialize database schema
python scripts/database/create_schema.py

# Apply initial migrations
alembic upgrade head

# Seed initial data
python scripts/database/seed_data.py
```

**Development Tools Setup**:
```bash
# Install pre-commit hooks
pre-commit install

# Run initial code quality checks
pre-commit run --all-files

# Run test suite
pytest

# Start development server
python app/main.py
```

#### IDE Configuration

**VS Code Configuration** (.vscode/settings.json):
```json
{
    "python.defaultInterpreterPath": ".venv/bin/python",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.mypyEnabled": true,
    "python.formatting.provider": "black",
    "python.testing.pytestEnabled": true,
    "python.testing.pytestArgs": ["tests/"],
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    }
}
```

### Production Environment Setup

#### Infrastructure Requirements

**Server Specifications**:
- **CPU**: Minimum 4 cores, recommended 8+ cores for multi-location deployments
- **Memory**: Minimum 8GB RAM, recommended 16GB+ for large databases
- **Storage**: SSD storage with minimum 100GB, recommended 500GB+ for data growth
- **Network**: Stable internet connection with minimum 100Mbps for cloud integrations

**Operating System**: Ubuntu 22.04 LTS Server or RHEL 8+ for production deployments

#### Production Database Setup

**PostgreSQL Production Configuration**:
```bash
# Install PostgreSQL 15 with performance optimizations
sudo apt update
sudo apt install postgresql-15 postgresql-contrib-15

# Configure PostgreSQL for production
sudo nano /etc/postgresql/15/main/postgresql.conf
```

**PostgreSQL Configuration Optimizations**:
```ini
# Memory settings
shared_buffers = 2GB
effective_cache_size = 6GB
work_mem = 64MB
maintenance_work_mem = 512MB

# Connection settings
max_connections = 200
max_prepared_transactions = 200

# Performance settings
checkpoint_timeout = 15min
checkpoint_completion_target = 0.9
wal_buffers = 64MB
default_statistics_target = 100

# Logging settings
log_min_duration_statement = 1000
log_checkpoints = on
log_connections = on
log_disconnections = on
log_lock_waits = on
```

**Database Security Configuration**:
```bash
# Create production database and user
sudo -u postgres createdb sg_pos_prod
sudo -u postgres psql -c "CREATE USER sg_pos_prod WITH PASSWORD 'secure_production_password';"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE sg_pos_prod TO sg_pos_prod;"

# Configure SSL connections
sudo -u postgres psql -c "ALTER SYSTEM SET ssl = on;"
sudo systemctl restart postgresql
```

#### Application Deployment

**Docker Production Setup**:
```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements/production.txt .
RUN pip install --no-cache-dir -r production.txt

# Copy application code
COPY app/ ./app/
COPY scripts/ ./scripts/
COPY resources/ ./resources/

# Create non-root user
RUN useradd -m -u 1000 appuser && chown -R appuser:appuser /app
USER appuser

# Expose port
EXPOSE 8000

# Start application
CMD ["python", "app/main.py"]
```

**Docker Compose Configuration**:
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://sg_pos_prod:${DB_PASSWORD}@db:5432/sg_pos_prod
      - DEBUG=False
      - LOG_LEVEL=INFO
    depends_on:
      - db
    restart: unless-stopped
    volumes:
      - ./logs:/app/logs
      - ./backups:/app/backups

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=sg_pos_prod
      - POSTGRES_USER=sg_pos_prod
      - POSTGRES_PASSWORD=${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./backups:/backups
    restart: unless-stopped
    ports:
      - "5432:5432"

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - app
    restart: unless-stopped

volumes:
  postgres_data:
```

#### Security Configuration

**SSL/TLS Setup**:
```bash
# Generate SSL certificates (using Let's Encrypt)
sudo apt install certbot
sudo certbot certonly --standalone -d your-domain.com

# Configure nginx with SSL
sudo nano /etc/nginx/sites-available/sg-pos
```

**Firewall Configuration**:
```bash
# Configure UFW firewall
sudo ufw allow 22/tcp   # SSH
sudo ufw allow 80/tcp   # HTTP
sudo ufw allow 443/tcp  # HTTPS
sudo ufw enable
```

**Application Security**:
```bash
# Set secure environment variables
export SECRET_KEY=$(openssl rand -hex 32)
export DATABASE_URL="postgresql://sg_pos_prod:${DB_PASSWORD}@localhost:5432/sg_pos_prod"
export JWT_SECRET_KEY=$(openssl rand -hex 32)
```

#### Monitoring and Logging

**Log Management**:
```bash
# Configure logrotate
sudo nano /etc/logrotate.d/sg-pos
```

**Logrotate Configuration**:
```
/app/logs/*.log {
    daily
    missingok
    rotate 30
    compress
    delaycompress
    notifempty
    create 644 appuser appuser
    postrotate
        systemctl reload sg-pos
    endscript
}
```

**System Monitoring**:
```bash
# Install monitoring tools
sudo apt install htop iotop postgresql-client

# Create monitoring scripts
cat > /usr/local/bin/sg-pos-health-check.sh << 'EOF'
#!/bin/bash
# Application health check script
curl -f http://localhost:8000/health || exit 1
psql $DATABASE_URL -c "SELECT 1;" || exit 1
EOF

chmod +x /usr/local/bin/sg-pos-health-check.sh
```

#### Backup and Recovery

**Automated Backup Setup**:
```bash
# Create backup script
cat > /usr/local/bin/sg-pos-backup.sh << 'EOF'
#!/bin/bash
BACKUP_DIR="/app/backups"
DATE=$(date +%Y%m%d_%H%M%S)

# Database backup
pg_dump $DATABASE_URL > "$BACKUP_DIR/database_backup_$DATE.sql"

# Application data backup
tar -czf "$BACKUP_DIR/app_data_backup_$DATE.tar.gz" /app/data

# Cleanup old backups (keep 30 days)
find "$BACKUP_DIR" -name "*.sql" -mtime +30 -delete
find "$BACKUP_DIR" -name "*.tar.gz" -mtime +30 -delete
EOF

chmod +x /usr/local/bin/sg-pos-backup.sh

# Schedule daily backups
echo "0 2 * * * /usr/local/bin/sg-pos-backup.sh" | sudo crontab -
```

#### Performance Optimization

**Application Performance Tuning**:
```python
# Production configuration settings
PRODUCTION_CONFIG = {
    "database": {
        "pool_size": 20,
        "max_overflow": 30,
        "pool_timeout": 30,
        "pool_recycle": 3600
    },
    "cache": {
        "enabled": True,
        "ttl": 300,
        "max_size": 10000
    },
    "logging": {
        "level": "INFO",
        "file_rotation": "daily",
        "max_files": 30
    }
}
```

**Database Performance Monitoring**:
```sql
-- Create performance monitoring views
CREATE VIEW performance_summary AS
SELECT 
    schemaname,
    tablename,
    seq_scan,
    seq_tup_read,
    idx_scan,
    idx_tup_fetch,
    n_tup_ins,
    n_tup_upd,
    n_tup_del
FROM pg_stat_user_tables;

-- Index usage monitoring
CREATE VIEW index_usage AS
SELECT 
    schemaname,
    tablename,
    indexname,
    idx_scan,
    idx_tup_read,
    idx_tup_fetch
FROM pg_stat_user_indexes;
```

This comprehensive Product Requirements Document provides a complete blueprint for building the SG Point-of-Sale system. The document covers all aspects from high-level architecture to detailed implementation specifications, ensuring that developers have clear guidance for building a production-ready, enterprise-grade retail management system specifically tailored for the Singapore market.

The architecture emphasizes clean code principles, scalability, maintainability, and regulatory compliance while providing a modern user experience. The detailed environment setup instructions ensure consistent deployments across development and production environments, supporting the system's reliability and operational requirements.
