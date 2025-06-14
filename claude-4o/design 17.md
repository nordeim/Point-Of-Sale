I need to create a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. This document needs to be extremely detailed (at least 6000 words) and include:
Database schema design
Codebase file hierarchy diagram
Application modules and user interaction diagram
Key application modules and files description
Technology stack description
Development and production environment setup
Clean architecture with proper separation of concerns
Singapore-specific regulatory compliance
The document should reflect the architectural considerations mentioned:

Layered architecture (Presentation, Business Logic, Data Access, Persistence)
Dependency injection with ApplicationCore
Asynchronous processing model
Best practices like DTOs and Result pattern
Multi-currency support
Let me structure this comprehensively. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
System Overview
Business Requirements
Technical Architecture
Database Schema Design
Codebase Structure
Application Modules
Technology Stack
Environment Setup
Security & Compliance
Performance Requirements
Development Guidelines
Testing Strategy
Deployment Strategy
Future Considerations
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed for small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for modern UI capabilities and PostgreSQL for robust data management, this system provides a professional-grade retail solution that fully complies with Singapore's regulatory requirements, including GST compliance, multi-currency support, and local payment methods integration.

The application architecture follows industry best practices with a clean, layered design that ensures maintainability, scalability, and robustness. The system implements advanced patterns including Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern, while maintaining a strong asynchronous processing model that ensures responsive user interfaces even during complex operations.

Key differentiators include:

Full compliance with Singapore's IRAS GST requirements
Support for multiple currencies with real-time exchange rates
Integration with local payment gateways (NETS, PayNow, GrabPay, etc.)
Comprehensive inventory management with multi-location support
Advanced reporting and analytics capabilities
Offline-first architecture with cloud synchronization
Multi-language support (English, Mandarin, Malay, Tamil)
2. System Overview
2.1 Purpose and Scope
The SG POS System serves as a complete retail management solution encompassing:

Point of Sale transactions
Inventory management
Customer relationship management
Employee management
Financial reporting and accounting integration
GST compliance and reporting
Multi-store operations
Business analytics and insights
2.2 Target Users
Primary users include:

Cashiers: Daily transaction processing, customer service
Store Managers: Inventory management, staff scheduling, daily reports
Business Owners: Financial oversight, strategic planning, compliance
Accountants: Financial reporting, GST filing, reconciliation
System Administrators: User management, system configuration
2.3 Core Functionality
The system provides comprehensive functionality across several domains:

Sales Processing

Quick product search and barcode scanning
Multiple payment methods support
Split payments and partial payments
Quotation and invoice generation
Returns and exchanges processing
Loyalty program integration
Inventory Management

Real-time stock tracking
Multi-location inventory
Automatic reorder points
Stock transfer between locations
Batch and serial number tracking
Expiry date management
Customer Management

Customer profiles and purchase history
Loyalty points tracking
Customer credit management
Marketing campaign integration
Customer analytics
Financial Management

GST calculation and reporting
Multi-currency transactions
Cash flow management
Integration with accounting systems
Comprehensive financial reports
Business Intelligence

Sales analytics and trends
Product performance metrics
Customer behavior analysis
Predictive analytics for inventory
Custom report builder
3. Business Requirements
3.1 Functional Requirements
3.1.1 Sales Management
FR-SM-001: System shall process sales transactions with multiple payment methods
FR-SM-002: System shall support barcode and QR code scanning
FR-SM-003: System shall calculate GST automatically based on product categories
FR-SM-004: System shall generate receipts in compliance with IRAS requirements
FR-SM-005: System shall support offline transactions with automatic synchronization
FR-SM-006: System shall handle returns and exchanges with audit trail
FR-SM-007: System shall support promotional pricing and discounts
FR-SM-008: System shall process multi-currency transactions with real-time rates
3.1.2 Inventory Management
FR-IM-001: System shall track inventory levels in real-time
FR-IM-002: System shall support multi-location inventory management
FR-IM-003: System shall generate automatic purchase orders at reorder points
FR-IM-004: System shall track product variants (size, color, etc.)
FR-IM-005: System shall manage supplier information and purchase history
FR-IM-006: System shall perform stock takes and adjustments
FR-IM-007: System shall track product movement history
FR-IM-008: System shall manage product bundles and kits
3.1.3 Customer Relationship Management
FR-CRM-001: System shall maintain comprehensive customer profiles
FR-CRM-002: System shall track customer purchase history and preferences
FR-CRM-003: System shall manage loyalty programs with points calculation
FR-CRM-004: System shall support customer credit limits and payment terms
FR-CRM-005: System shall generate customer statements and aging reports
FR-CRM-006: System shall support customer segmentation for marketing
FR-CRM-007: System shall handle customer feedback and complaints
3.1.4 Financial Management
FR-FM-001: System shall generate GST F5/F7 reports for IRAS submission
FR-FM-002: System shall track cash movements and reconciliation
FR-FM-003: System shall generate profit and loss statements
FR-FM-004: System shall support multiple payment terminals integration
FR-FM-005: System shall handle petty cash management
FR-FM-006: System shall generate daily sales summaries
FR-FM-007: System shall support export to accounting software
FR-FM-008: System shall maintain audit trails for all financial transactions
3.1.5 Reporting and Analytics
FR-RA-001: System shall generate customizable sales reports
FR-RA-002: System shall provide real-time dashboard with KPIs
FR-RA-003: System shall generate inventory valuation reports
FR-RA-004: System shall provide sales trend analysis
FR-RA-005: System shall generate employee performance reports
FR-RA-006: System shall support report scheduling and automation
FR-RA-007: System shall export reports in multiple formats
3.2 Non-Functional Requirements
3.2.1 Performance
NFR-P-001: System shall process transactions within 2 seconds
NFR-P-002: System shall support concurrent users (minimum 10 per store)
NFR-P-003: System shall handle 1000 transactions per day per terminal
NFR-P-004: Database queries shall return results within 1 second
NFR-P-005: System shall support databases up to 100GB
3.2.2 Security
NFR-S-001: System shall implement role-based access control
NFR-S-002: System shall encrypt sensitive data at rest and in transit
NFR-S-003: System shall maintain comprehensive audit logs
NFR-S-004: System shall support two-factor authentication
NFR-S-005: System shall comply with PCI-DSS for payment processing
3.2.3 Usability
NFR-U-001: System shall provide intuitive touch-screen interface
NFR-U-002: System shall support keyboard shortcuts for power users
NFR-U-003: System shall provide contextual help and tooltips
NFR-U-004: System shall support multiple languages
NFR-U-005: System shall be accessible to users with disabilities
3.2.4 Reliability
NFR-R-001: System shall maintain 99.9% uptime
NFR-R-002: System shall recover from crashes within 30 seconds
NFR-R-003: System shall perform automatic backups every hour
NFR-R-004: System shall support hot-standby failover
NFR-R-005: System shall maintain data integrity during power failures
4. Technical Architecture
4.1 Architecture Overview
The SG POS System follows a clean, layered architecture pattern that ensures separation of concerns, maintainability, and scalability. The architecture is designed to support both offline and online operations, with automatic synchronization capabilities.

4.2 Architecture Layers
4.2.1 Presentation Layer
The presentation layer handles all user interface concerns using PySide6 (Qt for Python). This layer is responsible for:

Rendering UI components and screens
Handling user input and events
Displaying data from the business layer
Managing UI state and navigation
Implementing responsive design for different screen sizes
Key characteristics:

No business logic in UI components
Uses Model-View-ViewModel (MVVM) pattern
Implements reactive UI updates
Supports theme customization
Handles internationalization (i18n)
4.2.2 Business Logic Layer
The business logic layer contains all business rules and workflows. It orchestrates operations across multiple services and ensures business constraints are met. This layer includes:

Transaction processing logic
Inventory management rules
Pricing and discount calculations
GST computation logic
Business validation rules
Workflow orchestration
Key characteristics:

Platform-agnostic business rules
Implements Domain-Driven Design (DDD) principles
Uses Command and Query Responsibility Segregation (CQRS)
Implements the Result pattern for error handling
Stateless service design
4.2.3 Data Access Layer
The data access layer provides abstraction over data persistence using the Repository pattern. It handles:

Database queries and commands
Data mapping and transformation
Query optimization
Caching strategies
Transaction management
Key characteristics:

Repository pattern implementation
Unit of Work pattern for transactions
Query builder abstractions
Database-agnostic interfaces
Connection pooling
4.2.4 Persistence Layer
The persistence layer manages actual data storage using PostgreSQL. It includes:

Database schema definitions
Stored procedures and functions
Triggers for data integrity
Indexes for performance
Backup and recovery procedures
4.3 Cross-Cutting Concerns
4.3.1 Dependency Injection
The application uses a centralized ApplicationCore class that implements dependency injection:

Lazy initialization of services
Singleton pattern for shared services
Circular dependency resolution
Service lifecycle management
Configuration injection
4.3.2 Asynchronous Processing
To maintain UI responsiveness, the application implements:

Separate thread for asyncio event loop
Background task scheduling
Progress reporting for long operations
Cancellable operations
Thread-safe communication
4.3.3 Error Handling
Comprehensive error handling strategy:

Result pattern for operation outcomes
Centralized exception handling
User-friendly error messages
Error logging and monitoring
Graceful degradation
4.3.4 Logging and Monitoring
Structured logging approach:

Multiple log levels (DEBUG, INFO, WARNING, ERROR, CRITICAL)
Contextual logging information
Performance metrics collection
Business event tracking
Log rotation and archival
5. Database Schema Design
5.1 Schema Overview
The database schema is designed to support all business requirements while maintaining data integrity, performance, and scalability. It follows normalization principles while strategically denormalizing for performance where necessary.

5.2 Core Tables
-- Company and Configuration
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE NOT NULL,
    gst_number VARCHAR(50),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    logo_url TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE stores (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- User Management
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    role VARCHAR(50) NOT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE user_stores (
    user_id UUID REFERENCES users(id),
    store_id UUID REFERENCES stores(id),
    is_default BOOLEAN DEFAULT FALSE,
    PRIMARY KEY (user_id, store_id)
);

-- Product Management
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    parent_id UUID REFERENCES categories(id),
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    gst_rate DECIMAL(5,2) DEFAULT 8.00,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id UUID REFERENCES categories(id),
    unit_of_measure VARCHAR(20) NOT NULL,
    cost DECIMAL(12,2) NOT NULL,
    selling_price DECIMAL(12,2) NOT NULL,
    min_stock_level INTEGER DEFAULT 0,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT TRUE,
    track_inventory BOOLEAN DEFAULT TRUE,
    allow_negative_stock BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID REFERENCES products(id),
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    attributes JSONB NOT NULL,
    cost DECIMAL(12,2) NOT NULL,
    selling_price DECIMAL(12,2) NOT NULL,
    is_active BOOLEAN DEFAULT TRUE
);

-- Inventory Management
CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    store_id UUID REFERENCES stores(id),
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity INTEGER NOT NULL DEFAULT 0,
    reserved_quantity INTEGER NOT NULL DEFAULT 0,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(store_id, product_id, variant_id)
);

CREATE TABLE inventory_movements (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    store_id UUID REFERENCES stores(id),
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    movement_type VARCHAR(50) NOT NULL,
    quantity INTEGER NOT NULL,
    reference_type VARCHAR(50),
    reference_id UUID,
    notes TEXT,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Customer Management
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_code VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(20),
    address TEXT,
    tax_id VARCHAR(50),
    credit_limit DECIMAL(12,2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0,
    loyalty_points INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Sales Transactions
CREATE TABLE sales_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    store_id UUID REFERENCES stores(id),
    customer_id UUID REFERENCES customers(id),
    transaction_date TIMESTAMP NOT NULL,
    subtotal DECIMAL(12,2) NOT NULL,
    discount_amount DECIMAL(12,2) DEFAULT 0,
    gst_amount DECIMAL(12,2) NOT NULL,
    total_amount DECIMAL(12,2) NOT NULL,
    payment_status VARCHAR(20) NOT NULL,
    notes TEXT,
    voided BOOLEAN DEFAULT FALSE,
    void_reason TEXT,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE sales_transaction_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID REFERENCES sales_transactions(id),
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(12,2) NOT NULL,
    discount_amount DECIMAL(12,2) DEFAULT 0,
    gst_amount DECIMAL(12,2) NOT NULL,
    total_amount DECIMAL(12,2) NOT NULL
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID REFERENCES sales_transactions(id),
    payment_method VARCHAR(50) NOT NULL,
    amount DECIMAL(12,2) NOT NULL,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1.000000,
    reference_number VARCHAR(100),
    status VARCHAR(20) NOT NULL,
    processed_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL,
    parent_id UUID REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT,
    reference_type VARCHAR(50),
    reference_id UUID,
    is_posted BOOLEAN DEFAULT FALSE,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    journal_entry_id UUID REFERENCES journal_entries(id),
    account_id UUID REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(12,2) DEFAULT 0,
    credit_amount DECIMAL(12,2) DEFAULT 0,
    description TEXT
);

5.3 Indexes and Constraints
-- Performance Indexes
CREATE INDEX idx_products_category ON products(category_id);
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_inventory_store_product ON inventory(store_id, product_id);
CREATE INDEX idx_sales_transactions_date ON sales_transactions(transaction_date);
CREATE INDEX idx_sales_transactions_customer ON sales_transactions(customer_id);
CREATE INDEX idx_payments_transaction ON payments(transaction_id);

-- Check Constraints
ALTER TABLE products ADD CONSTRAINT chk_positive_price CHECK (selling_price >= 0);
ALTER TABLE inventory ADD CONSTRAINT chk_non_negative_quantity CHECK (quantity >= 0);
ALTER TABLE sales_transactions ADD CONSTRAINT chk_valid_total CHECK (total_amount >= 0);

-- Triggers
CREATE OR REPLACE FUNCTION update_timestamp()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_products_timestamp
    BEFORE UPDATE ON products
    FOR EACH ROW
    EXECUTE FUNCTION update_timestamp();

6. Codebase Structure
6.1 File Hierarchy Diagram
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py          # Dependency injection container
│   │   ├── config.py                    # Configuration management
│   │   ├── constants.py                 # Application constants
│   │   └── exceptions.py                # Custom exceptions
│   │
│   ├── models/                          # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                      # Base model class
│   │   ├── company.py
│   │   ├── user.py
│   │   ├── product.py
│   │   ├── inventory.py
│   │   ├── customer.py
│   │   ├── sales.py
│   │   ├── payment.py
│   │   └── accounting.py
│   │
│   ├── dto/                             # Data Transfer Objects
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── product_dto.py
│   │   ├── sales_dto.py
│   │   ├── customer_dto.py
│   │   └── report_dto.py
│   │
│   ├── services/                        # Data Access Layer
│   │   ├── __init__.py
│   │   ├── base_service.py
│   │   ├── product_service.py
│   │   ├── inventory_service.py
│   │   ├── customer_service.py
│   │   ├── sales_service.py
│   │   ├── payment_service.py
│   │   └── report_service.py
│   │
│   ├── business_logic/                  # Business Logic Layer
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── base_manager.py
│   │   │   ├── sales_manager.py
│   │   │   ├── inventory_manager.py
│   │   │   ├── customer_manager.py
│   │   │   ├── payment_manager.py
│   │   │   └── gst_manager.py
│   │   │
│   │   ├── validators/
│   │   │   ├── __init__.py
│   │   │   ├── product_validator.py
│   │   │   ├── sales_validator.py
│   │   │   └── payment_validator.py
│   │   │
│   │   └── calculators/
│   │       ├── __init__.py
│   │       ├── pricing_calculator.py
│   │       ├── gst_calculator.py
│   │       └── discount_calculator.py
│   │
│   ├── ui/                              # Presentation Layer
│   │   ├── __init__.py
│   │   ├── main_window.py
│   │   ├── styles/
│   │   │   ├── __init__.py
│   │   │   ├── theme.py
│   │   │   └── styles.qss
│   │   │
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py
│   │   │   ├── pos_widget.py
│   │   │   ├── inventory_widget.py
│   │   │   ├── customer_widget.py
│   │   │   ├── reports_widget.py
│   │   │   └── settings_widget.py
│   │   │
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── product_dialog.py
│   │   │   ├── payment_dialog.py
│   │   │   ├── customer_dialog.py
│   │   │   └── receipt_dialog.py
│   │   │
│   │   └── models/                      # Qt Models
│   │       ├── __init__.py
│   │       ├── product_model.py
│   │       ├── sales_model.py
│   │       └── customer_model.py
│   │
│   ├── utils/                           # Utility functions
│   │   ├── __init__.py
│   │   ├── async_utils.py
│   │   ├── date_utils.py
│   │   ├── currency_utils.py
│   │   ├── barcode_utils.py
│   │   └── export_utils.py
│   │
│   └── integrations/                    # External integrations
│       ├── __init__.py
│       ├── payment_gateways/
│       │   ├── __init__.py
│       │   ├── base_gateway.py
│       │   ├── nets_gateway.py
│       │   ├── paynow_gateway.py
│       │   └── grabpay_gateway.py
│       │
│       └── accounting/
│           ├── __init__.py
│           ├── quickbooks_integration.py
│           └── xero_integration.py
│
├── tests/                               # Test suite
│   ├── __init__.py
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── scripts/                             # Database and utility scripts
│   ├── create_database.sql
│   ├── seed_data.sql
│   ├── backup_database.py
│   └── migrate_database.py
│
├── config/                              # Configuration files
│   ├── development.ini
│   ├── production.ini
│   └── logging.conf
│
├── docs/                                # Documentation
│   ├── api/
│   ├── user_manual/
│   └── deployment/
│
├── requirements.txt                     # Python dependencies
├── requirements-dev.txt                 # Development dependencies
├── setup.py                            # Package setup
├── README.md                           # Project documentation
└── LICENSE                             # License file
7. Application Modules
7.1 User Interaction Flow Diagram
graph TB
    A[Login Screen] --> B{Authentication}
    B -->|Success| C[Main Dashboard]
    B -->|Failure| A
    
    C --> D[POS Module]
    C --> E[Inventory Module]
    C --> F[Customer Module]
    C --> G[Reports Module]
    C --> H[Settings Module]
    
    D --> D1[Product Search]
    D --> D2[Cart Management]
    D --> D3[Payment Processing]
    D --> D4[Receipt Generation]
    
    E --> E1[Stock Management]
    E --> E2[Purchase Orders]
    E --> E3[Stock Takes]
    E --> E4[Transfers]
    
    F --> F1[Customer Profiles]
    F --> F2[Loyalty Management]
    F --> F3[Credit Management]
    
    G --> G1[Sales Reports]
    G --> G2[Inventory Reports]
    G --> G3[GST Reports]
    G --> G4[Financial Reports]

7.2 Key Application Modules
7.2.1 Core Module (app/core/)
ApplicationCore (application_core.py) The central dependency injection container that manages all service and manager instances. Implements lazy initialization pattern for optimal resource usage.

Key responsibilities:

Service lifecycle management
Configuration injection
Dependency resolution
Application initialization
class ApplicationCore:
    def __init__(self, config: Config):
        self._config = config
        self._db_engine = None
        self._session_factory = None
        # Lazy-loaded services and managers
        
    @property
    def sales_manager(self) -> SalesManager:
        if not hasattr(self, '_sales_manager'):
            self._sales_manager = SalesManager(self)
        return self._sales_manager

Configuration (config.py) Manages application configuration with environment-specific settings.

class Config:
    def __init__(self, env: str = 'development'):
        self.env = env
        self.load_from_file(f'config/{env}.ini')
        
    @property
    def database_url(self) -> str:
        return self._config.get('database', 'url')

7.2.2 Business Logic Module (app/business_logic/)
Sales Manager (managers/sales_manager.py) Orchestrates all sales-related operations, ensuring business rules are enforced.

Key methods:

create_transaction(): Initiates new sales transaction
add_item(): Adds product to transaction
apply_discount(): Applies discounts with validation
process_payment(): Handles payment processing
complete_transaction(): Finalizes sale with inventory updates
class SalesManager:
    def __init__(self, app_core: ApplicationCore):
        self.app_core = app_core
        
    async def create_transaction(self, store_id: UUID, user_id: UUID) -> Result[SalesTransaction]:
        # Validate store and user
        # Create new transaction
        # Return Result object

Inventory Manager (managers/inventory_manager.py) Manages all inventory operations with real-time stock tracking.

Key methods:

check_availability(): Verifies product availability
reserve_stock(): Reserves stock for pending transactions
update_stock(): Updates inventory levels
transfer_stock(): Handles inter-store transfers
perform_stock_take(): Manages stock reconciliation
GST Manager (managers/gst_manager.py) Handles GST calculations and compliance for Singapore.

Key methods:

calculate_gst(): Computes GST based on product categories
generate_gst_report(): Creates IRAS-compliant reports
validate_gst_number(): Validates GST registration numbers
7.2.3 Data Access Module (app/services/)
Base Service (base_service.py) Provides common repository functionality for all services.

class BaseService:
    def __init__(self, app_core: ApplicationCore, model_class):
        self.app_core = app_core
        self.model_class = model_class
        
    async def get_by_id(self, id: UUID) -> Optional[Model]:
        async with self.app_core.get_session() as session:
            return await session.get(self.model_class, id)

Product Service (product_service.py) Handles all product-related data operations.

Key methods:

search_products(): Advanced product search with filters
get_by_barcode(): Quick barcode lookup
update_prices(): Bulk price updates
get_low_stock(): Identifies products below reorder point
7.2.4 User Interface Module (app/ui/)
Main Window (main_window.py) The primary application window that hosts all other widgets.

class MainWindow(QMainWindow):
    def __init__(self, app_core: ApplicationCore):
        super().__init__()
        self.app_core = app_core
        self.setup_ui()
        self.setup_navigation()

POS Widget (widgets/pos_widget.py) The main point-of-sale interface for processing transactions.

Key features:

Product search and selection
Cart management
Payment processing
Receipt preview and printing
Reports Widget (widgets/reports_widget.py) Comprehensive reporting interface with customizable reports.

Features:

Report templates
Custom report builder
Export functionality
Scheduled reports
7.2.5 Integration Module (app/integrations/)
Payment Gateway Base (payment_gateways/base_gateway.py) Abstract base class for payment gateway integrations.

class PaymentGateway(ABC):
    @abstractmethod
    async def process_payment(self, amount: Decimal, reference: str) -> PaymentResult:
        pass
        
    @abstractmethod
    async def refund_payment(self, transaction_id: str, amount: Decimal) -> RefundResult:
        pass

8. Technology Stack
8.1 Core Technologies
8.1.1 Programming Language
Python 3.11+

Modern async/await support
Type hints for better code clarity
Enhanced performance
Strong ecosystem for business applications
8.1.2 User Interface Framework
PySide6 (Qt for Python)

Cross-platform desktop UI
Rich widget library
Hardware acceleration
Touch screen support
Excellent documentation
8.1.3 Database
PostgreSQL 15+

ACID compliance
Advanced indexing
JSON support for flexible data
Full-text search capabilities
Robust replication options
8.1.4 ORM
SQLAlchemy 2.0

Modern async support
Type-safe queries
Migration support with Alembic
Connection pooling
Query optimization
8.2 Supporting Libraries
8.2.1 Async Processing
asyncio: Core async functionality
aiohttp: Async HTTP client
asyncpg: Fast PostgreSQL driver
8.2.2 Data Processing
pandas: Data analysis and reporting
numpy: Numerical computations
openpyxl: Excel file generation
8.2.3 Utilities
pydantic: Data validation and settings
python-barcode: Barcode generation
Pillow: Image processing
cryptography: Encryption utilities
8.2.4 Testing
pytest: Testing framework
pytest-asyncio: Async test support
pytest-qt: Qt testing utilities
factory_boy: Test data generation
8.2.5 Development Tools
black: Code formatting
mypy: Static type checking
pylint: Code quality checks
pre-commit: Git hooks
8.3 External Services
8.3.1 Payment Processing
NETS API integration
PayNow QR generation
GrabPay merchant API
Credit card processing (via payment gateway)
8.3.2 Government Services
IRAS API for GST submission
ACRA for business verification
8.3.3 Cloud Services (Optional)
AWS S3 for backup storage
CloudFlare for API protection
SendGrid for email notifications
9. Environment Setup
9.1 Development Environment
9.1.1 Prerequisites
# System requirements
- Ubuntu 22.04 LTS / Windows 11 / macOS 12+
- Python 3.11+
- PostgreSQL 15+
- Git
- VS Code or PyCharm

9.1.2 Development Setup Script
#!/bin/bash
# setup_dev.sh

# Clone repository
git clone https://github.com/company/sg-pos-system.git
cd sg-pos-system

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Setup PostgreSQL database
sudo -u postgres psql << EOF
CREATE USER pos_dev WITH PASSWORD 'dev_password';
CREATE DATABASE pos_development OWNER pos_dev;
GRANT ALL PRIVILEGES ON DATABASE pos_development TO pos_dev;
EOF

# Run database migrations
alembic upgrade head

# Seed development data
python scripts/seed_dev_data.py

# Setup pre-commit hooks
pre-commit install

# Copy development configuration
cp config/development.ini.example config/development.ini

echo "Development environment setup complete!"

9.1.3 IDE Configuration
VS Code settings.json

{
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.formatting.provider": "black",
    "python.testing.pytestEnabled": true,
    "editor.formatOnSave": true,
    "python.analysis.typeCheckingMode": "strict"
}

9.2 Production Environment
9.2.1 Server Requirements
Ubuntu 22.04 LTS Server
8GB RAM minimum (16GB recommended)
4 CPU cores
100GB SSD storage
Gigabit network connection
9.2.2 Production Setup
System Preparation

# Update system
sudo apt update && sudo apt upgrade -y

# Install required packages
sudo apt install -y python3.11 python3.11-venv python3-pip
sudo apt install -y postgresql-15 postgresql-contrib
sudo apt install -y nginx redis-server
sudo apt install -y build-essential libpq-dev

# Create application user
sudo useradd -m -s /bin/bash posapp
sudo usermod -aG sudo posapp

Application Deployment

# As posapp user
sudo su - posapp

# Clone application
git clone https://github.com/company/sg-pos-system.git /opt/sg-pos
cd /opt/sg-pos

# Create virtual environment
python3.11 -m venv venv
source venv/bin/activate

# Install production dependencies
pip install -r requirements.txt
pip install gunicorn supervisor

# Setup PostgreSQL
sudo -u postgres psql << EOF
CREATE USER pos_prod WITH PASSWORD 'strong_password';
CREATE DATABASE pos_production OWNER pos_prod;
GRANT ALL PRIVILEGES ON DATABASE pos_production TO pos_prod;
EOF

# Configure application
cp config/production.ini.example config/production.ini
# Edit configuration with production values

# Run migrations
alembic upgrade head

# Setup systemd service
sudo cp deployment/sg-pos.service /etc/systemd/system/
sudo systemctl enable sg-pos
sudo systemctl start sg-pos

Database Backup Configuration

# Create backup script
cat > /opt/sg-pos/scripts/backup_db.sh << 'EOF'
#!/bin/bash
BACKUP_DIR="/backup/postgres"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
DB_NAME="pos_production"

# Create backup
pg_dump -U pos_prod -h localhost $DB_NAME | gzip > $BACKUP_DIR/backup_$TIMESTAMP.sql.gz

# Keep only last 30 days of backups
find $BACKUP_DIR -name "backup_*.sql.gz" -mtime +30 -delete
EOF

# Setup cron job
echo "0 2 * * * /opt/sg-pos/scripts/backup_db.sh" | crontab -

9.2.3 Security Hardening
# Firewall configuration
sudo ufw allow 22/tcp
sudo ufw allow 443/tcp
sudo ufw enable

# Fail2ban installation
sudo apt install fail2ban
sudo systemctl enable fail2ban

# SSL Certificate
sudo apt install certbot
sudo certbot certonly --standalone -d pos.company.com

# Application security
# Enable audit logging
# Configure rate limiting
# Setup intrusion detection

10. Security & Compliance
10.1 Security Architecture
10.1.1 Authentication & Authorization
Multi-factor authentication support
Role-based access control (RBAC)
JWT tokens for session management
Password complexity requirements
Account lockout policies
10.1.2 Data Security
AES-256 encryption for sensitive data
TLS 1.3 for data in transit
Database encryption at rest
Secure key management
PCI-DSS compliance for payment data
10.1.3 Audit & Compliance
Comprehensive audit logging
Tamper-proof audit trails
GDPR compliance features
Data retention policies
Regular security assessments
10.2 Singapore Regulatory Compliance
10.2.1 IRAS GST Requirements
GST-registered business validation
Accurate GST calculations
GST-inclusive pricing display
F5/F7 report generation
Electronic submission capability
10.2.2 PDPA Compliance
Personal data protection measures
Consent management
Data portability features
Right to erasure implementation
Data breach notification procedures
11. Performance Requirements
11.1 Response Time Requirements
Operation	Target Response Time	Maximum Response Time
Product search	< 0.5 seconds	1 second
Transaction processing	< 2 seconds	3 seconds
Report generation	< 5 seconds	10 seconds
Inventory update	< 1 second	2 seconds
Receipt printing	< 3 seconds	5 seconds
11.2 Scalability Requirements
Support 50 concurrent users per store
Handle 10,000 transactions per day
Manage 100,000+ product SKUs
Store 5 years of transaction history
Support up to 50 store locations
11.3 Performance Optimization
