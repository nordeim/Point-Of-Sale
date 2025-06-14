The user is asking for a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. This needs to be a detailed document (at least 6000 words) that includes:
Database schema design
Codebase file hierarchy diagram
Application modules and user interaction diagram
Key module descriptions
Technology stack description
Environment setup instructions
The architectural considerations provided give clear guidance on the design principles to follow:

Layered architecture with separation of concerns
Dependency injection using ApplicationCore pattern
Asynchronous processing model
I'll structure this PRD to be comprehensive, well-organized, and leave no ambiguity for implementation. The document will follow professional standards and include all necessary technical details. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Project Overview
Business Requirements
Functional Requirements
Non-Functional Requirements
System Architecture
Database Schema Design
Codebase Structure
Module Descriptions
Technology Stack
Development Environment Setup
Production Environment Setup
Security Considerations
Testing Strategy
Deployment Strategy
Future Enhancements
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for a modern user interface and PostgreSQL for robust data management, this professional-grade retail tool is tailored to Singapore's unique regulatory environment, including GST compliance, multi-currency support, and local payment methods.

The system architecture follows industry best practices with a clean layered architecture, asynchronous processing capabilities, and strong data integrity mechanisms. The implementation emphasizes scalability, maintainability, and extensibility through patterns such as Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern.

Key features include real-time inventory management, multi-location support, comprehensive reporting, integrated accounting, customer relationship management, and full compliance with Singapore's regulatory requirements. The system is designed to handle the complexity of real-world retail operations while maintaining a user-friendly interface suitable for non-technical users.

2. Project Overview
2.1 Vision Statement
To create a world-class Point-of-Sale system that empowers Singapore's SMBs with professional-grade retail management capabilities, enabling them to compete effectively in the digital economy while maintaining full regulatory compliance.

2.2 Project Goals
Comprehensive Retail Management: Provide a complete solution covering sales, inventory, accounting, and customer management
Singapore-Specific Compliance: Ensure full compliance with GST regulations, IRAS requirements, and local business practices
User-Friendly Interface: Create an intuitive interface that requires minimal training
Scalability: Support business growth from single outlets to multi-location operations
Data Integrity: Maintain absolute data accuracy and consistency across all operations
Performance: Ensure responsive performance even with large transaction volumes
Security: Implement robust security measures to protect sensitive business data
2.3 Target Users
Primary Users: Cashiers, sales staff, and retail operators
Secondary Users: Business owners, managers, and accountants
Administrative Users: System administrators and IT support staff
2.4 Success Metrics
Transaction processing time under 2 seconds
System uptime of 99.9%
User satisfaction rating above 4.5/5
Zero data loss incidents
Full GST compliance certification
Support for 10,000+ SKUs without performance degradation
3. Business Requirements
3.1 Core Business Processes
3.1.1 Sales Transaction Processing
The system must support complete end-to-end sales transactions including:

Product barcode scanning and manual entry
Multiple payment methods (cash, credit/debit cards, NETS, PayNow, GrabPay)
Split payments across multiple methods
Discounts (percentage and fixed amount)
Returns and exchanges with reason tracking
Void transactions with authorization
Suspended transactions for later retrieval
Multi-currency transactions with real-time exchange rates
3.1.2 Inventory Management
Comprehensive inventory control including:

Real-time stock level tracking
Automatic reorder point notifications
Stock transfers between locations
Stock adjustments with reason codes
Batch and serial number tracking
Expiry date management
Stock take functionality with variance reporting
Supplier management and purchase orders
3.1.3 Customer Management
Complete customer relationship management:

Customer profile creation and maintenance
Purchase history tracking
Loyalty program management
Customer credit accounts
Birthday and anniversary tracking
Customer group segmentation
Marketing campaign targeting
Customer feedback collection
3.1.4 Financial Management
Integrated accounting functionality:

Real-time journal entry creation
Chart of accounts management
GST calculation and reporting
Daily cash reconciliation
Profit and loss statements
Balance sheet generation
Cash flow analysis
Multi-currency accounting
3.2 Regulatory Compliance
3.2.1 GST Compliance
Automatic GST calculation based on product categories
GST-inclusive and GST-exclusive pricing support
GST reports for IRAS submission
GST bad debt relief tracking
Tourist refund scheme support
Proper GST invoice generation
3.2.2 Data Protection
Compliance with Singapore's Personal Data Protection Act (PDPA)
Customer data encryption
Access control and audit trails
Data retention policies
Right to data portability
3.3 Business Rules
3.3.1 Pricing Rules
Tiered pricing based on customer groups
Time-based promotions
Bundle pricing
Quantity discounts
Member vs non-member pricing
Cost-plus pricing calculations
3.3.2 Inventory Rules
Minimum stock level enforcement
FIFO/LIFO/Weighted Average costing
Negative stock prevention
Stock reservation for pending orders
Automatic stock deduction on sale
Stock return on refund
3.3.3 Security Rules
Role-based access control
Transaction authorization limits
Void and refund approvals
Price override restrictions
Discount limit enforcement
Cash drawer access control
4. Functional Requirements
4.1 User Authentication and Authorization
4.1.1 User Management
Create, read, update, delete (CRUD) operations for users
Role assignment (Cashier, Supervisor, Manager, Admin)
Password complexity enforcement
Password expiry and rotation
Two-factor authentication support
Session timeout configuration
Login attempt monitoring and lockout
4.1.2 Permission System
Granular permission control
Role-based permission templates
Custom permission assignments
Permission inheritance
Audit trail for permission changes
4.2 Point of Sale Operations
4.2.1 Transaction Processing
Barcode scanning with fallback to manual entry
Product search by name, SKU, or category
Real-time price and stock checking
Multiple items per transaction
Item quantity modification
Line item discounts
Transaction-level discounts
Tax calculation and display
Payment processing
Change calculation
Receipt printing and email
4.2.2 Payment Processing
Cash payment with denomination breakdown
Credit/debit card integration
NETS integration
PayNow QR code generation
GrabPay integration
Split payment across methods
Payment validation
Change due calculation
Cash drawer management
4.2.3 Receipt Management
Customizable receipt templates
Company branding on receipts
Transaction details display
GST breakdown
Payment method indication
Return policy printing
Promotional messages
Receipt reprint functionality
4.3 Inventory Management
4.3.1 Product Management
Product creation with multiple attributes
Category and subcategory assignment
Multiple barcodes per product
Product variants (size, color)
Product images
Minimum and maximum stock levels
Reorder quantities
Supplier assignment
Cost and selling price management
4.3.2 Stock Operations
Stock receiving from suppliers
Stock transfers between locations
Stock adjustments with reasons
Stock counting procedures
Variance analysis
Damaged goods tracking
Stock write-offs
Consignment stock tracking
4.3.3 Purchase Orders
Purchase order creation
Supplier catalog integration
Order approval workflow
Partial delivery handling
Purchase order tracking
Automatic stock updates
Purchase return processing
Supplier performance tracking
4.4 Customer Relationship Management
4.4.1 Customer Profiles
Customer registration
Contact information management
Purchase history tracking
Preference recording
Communication opt-in/opt-out
Customer notes
Credit limit management
Payment terms assignment
4.4.2 Loyalty Program
Point accumulation rules
Point redemption options
Tier-based benefits
Special member pricing
Birthday rewards
Referral bonuses
Point expiry management
Loyalty card generation
4.4.3 Marketing Tools
Customer segmentation
Targeted promotions
Email campaign integration
SMS campaign support
Purchase behavior analysis
Customer lifetime value calculation
Churn prediction
Win-back campaigns
4.5 Reporting and Analytics
4.5.1 Sales Reports
Daily sales summary
Hourly sales analysis
Product performance reports
Category sales breakdown
Staff performance metrics
Payment method analysis
Discount analysis
Tax collected reports
4.5.2 Inventory Reports
Stock level reports
Stock movement analysis
Aging inventory reports
Stock valuation reports
Reorder reports
Supplier performance
Stock turnover analysis
Dead stock identification
4.5.3 Financial Reports
Profit and loss statements
Cash flow reports
GST reports
Accounts receivable aging
Accounts payable aging
General ledger reports
Trial balance
Financial ratios
4.5.4 Customer Reports
Customer purchase analysis
Loyalty program performance
Customer segmentation reports
Customer lifetime value
Retention rate analysis
New vs returning customers
Geographic distribution
Customer satisfaction metrics
4.6 System Administration
4.6.1 Configuration Management
Company profile setup
Multi-location configuration
Tax rate management
Payment method setup
Receipt template design
Email template configuration
System preferences
Integration settings
4.6.2 Data Management
Database backup scheduling
Data export functionality
Data import tools
Data archiving
Data purging policies
Audit trail maintenance
System logs management
Error log monitoring
4.6.3 Integration Management
Payment gateway configuration
Accounting software integration
E-commerce platform sync
Supplier system integration
Banking integration
Government portal connectivity
Third-party API management
Webhook configuration
5. Non-Functional Requirements
5.1 Performance Requirements
5.1.1 Response Time
Login operation: < 2 seconds
Product search: < 0.5 seconds
Transaction processing: < 2 seconds
Report generation: < 5 seconds for standard reports
Page load time: < 1 second
Database query response: < 100ms for simple queries
5.1.2 Throughput
Support 100 concurrent users
Process 1000 transactions per hour
Handle 10,000 products without degradation
Support 50,000 customers records
Process batch operations for 1000 items in < 1 minute
5.1.3 Resource Utilization
Maximum 2GB RAM usage
CPU usage < 50% during normal operations
Database size growth < 1GB per 100,000 transactions
Network bandwidth < 1Mbps per terminal
5.2 Reliability Requirements
5.2.1 Availability
System uptime: 99.9% (8.76 hours downtime per year)
Planned maintenance windows: Maximum 4 hours per month
Mean Time Between Failures (MTBF): > 720 hours
Mean Time To Recovery (MTTR): < 1 hour
5.2.2 Fault Tolerance
Graceful degradation on component failure
Automatic failover for critical services
Transaction rollback on failure
Data integrity preservation
Automatic error recovery
Circuit breaker pattern implementation
5.3 Security Requirements
5.3.1 Authentication
Multi-factor authentication support
Biometric authentication option
Single Sign-On (SSO) capability
Password complexity requirements
Account lockout policies
Session management
API key authentication
5.3.2 Authorization
Role-Based Access Control (RBAC)
Attribute-Based Access Control (ABAC)
Principle of least privilege
Dynamic permission evaluation
Resource-level permissions
API endpoint protection
5.3.3 Data Protection
AES-256 encryption for data at rest
TLS 1.3 for data in transit
Database column-level encryption
Key rotation policies
Secure key storage
Data masking for sensitive fields
Audit trail encryption
5.4 Usability Requirements
5.4.1 User Interface
Intuitive navigation structure
Consistent design language
Responsive layout
Keyboard shortcuts support
Touch screen optimization
Multi-language support
Accessibility compliance (WCAG 2.1)
5.4.2 User Experience
Maximum 3 clicks to any function
Context-sensitive help
Inline validation
Progress indicators
Undo/redo functionality
Batch operations support
Customizable dashboards
5.5 Scalability Requirements
5.5.1 Vertical Scalability
Support for increased CPU cores
Memory scaling up to 16GB
Storage expansion capability
Database connection pooling
Cache size adjustment
5.5.2 Horizontal Scalability
Multi-location support
Database replication
Load balancing capability
Distributed caching
Microservices architecture readiness
6. System Architecture
6.1 Architecture Overview
The SG POS system follows a clean, layered architecture pattern that ensures separation of concerns, maintainability, and scalability. The architecture consists of four primary layers:

Presentation Layer: Handles all user interface components and user interactions
Business Logic Layer: Contains all business rules and orchestrates operations
Data Access Layer: Manages all database operations through the repository pattern
Infrastructure Layer: Provides cross-cutting concerns like logging, caching, and security
6.2 Architecture Diagram
┌─────────────────────────────────────────────────────────────────────┐
│                         Presentation Layer                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐ │
│  │   Main UI   │  │   Dialogs   │  │   Widgets   │  │  Models   │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘ │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        Business Logic Layer                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐ │
│  │  Managers   │  │  Validators │  │  Calculators│  │Processors │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘ │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         Data Access Layer                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐ │
│  │  Services   │  │Repositories │  │    DTOs     │  │  Mappers  │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘ │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        Infrastructure Layer                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐ │
│  │  Database   │  │   Caching   │  │   Logging   │  │ Security  │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘ │
└─────────────────────────────────────────────────────────────────────┘
6.3 Component Interaction
The system uses a dependency injection pattern centered around the ApplicationCore class, which acts as a service locator and dependency container. This design ensures loose coupling between components and facilitates testing.

6.3.1 ApplicationCore Pattern
# Simplified ApplicationCore Structure
class ApplicationCore:
    def __init__(self):
        self._db_session = None
        self._config = None
        # Lazy-loaded managers
        self._customer_manager = None
        self._product_manager = None
        self._transaction_manager = None
        
    @property
    def customer_manager(self) -> CustomerManager:
        if self._customer_manager is None:
            self._customer_manager = CustomerManager(self)
        return self._customer_manager

6.4 Asynchronous Architecture
The system implements a robust asynchronous architecture to ensure UI responsiveness:

Main Thread: Runs the Qt event loop and handles all UI updates
Async Thread: Runs the asyncio event loop for all I/O operations
Thread Bridge: Safe communication between Qt and asyncio threads
# Thread Bridge Implementation
def schedule_task_from_qt(coro, callback=None):
    """Bridge between Qt thread and asyncio thread"""
    future = asyncio.run_coroutine_threadsafe(coro, async_loop)
    if callback:
        future.add_done_callback(
            lambda f: QMetaObject.invokeMethod(
                callback[0], callback[1], 
                Qt.ConnectionType.QueuedConnection,
                Q_ARG(object, f.result())
            )
        )
    return future

7. Database Schema Design
7.1 Schema Overview
The database schema is designed to support all business requirements while maintaining data integrity through proper normalization, constraints, and relationships. The schema follows these principles:

Third Normal Form (3NF) for data normalization
Consistent naming conventions (snake_case)
Proper indexing for performance
Referential integrity through foreign keys
Audit trails for critical tables
Soft deletes where appropriate
7.2 Core Tables
7.2.1 User and Authentication Tables
-- Users table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role_id INTEGER REFERENCES roles(id),
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_by INTEGER REFERENCES users(id),
    updated_by INTEGER REFERENCES users(id)
);

-- Roles table
CREATE TABLE roles (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    is_system BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Permissions table
CREATE TABLE permissions (
    id SERIAL PRIMARY KEY,
    resource VARCHAR(100) NOT NULL,
    action VARCHAR(50) NOT NULL,
    description TEXT,
    UNIQUE(resource, action)
);

-- Role permissions junction table
CREATE TABLE role_permissions (
    role_id INTEGER REFERENCES roles(id) ON DELETE CASCADE,
    permission_id INTEGER REFERENCES permissions(id) ON DELETE CASCADE,
    PRIMARY KEY (role_id, permission_id)
);

7.2.2 Product and Inventory Tables
-- Categories table
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    parent_id INTEGER REFERENCES categories(id),
    description TEXT,
    is_active BOOLEAN DEFAULT true,
    sort_order INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Products table
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    unit_of_measure VARCHAR(20) NOT NULL,
    cost_price DECIMAL(10,2) NOT NULL DEFAULT 0,
    selling_price DECIMAL(10,2) NOT NULL,
    tax_rate DECIMAL(5,2) DEFAULT 0,
    is_taxable BOOLEAN DEFAULT true,
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    min_stock_level INTEGER DEFAULT 0,
    max_stock_level INTEGER,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 1,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Product barcodes table
CREATE TABLE product_barcodes (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id) ON DELETE CASCADE,
    barcode VARCHAR(50) UNIQUE NOT NULL,
    is_primary BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Inventory locations table
CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    is_active BOOLEAN DEFAULT true,
    is_default BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Inventory table
CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    location_id INTEGER REFERENCES locations(id),
    quantity_on_hand INTEGER NOT NULL DEFAULT 0,
    quantity_reserved INTEGER NOT NULL DEFAULT 0,
    quantity_available INTEGER GENERATED ALWAYS AS 
        (quantity_on_hand - quantity_reserved) STORED,
    last_count_date TIMESTAMP,
    last_count_quantity INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location_id)
);

-- Stock movements table
CREATE TABLE stock_movements (
    id SERIAL PRIMARY KEY,
    movement_type VARCHAR(20) NOT NULL, -- PURCHASE, SALE, TRANSFER, ADJUSTMENT
    reference_type VARCHAR(20), -- PO, INVOICE, TRANSFER, ADJUSTMENT
    reference_id INTEGER,
    product_id INTEGER REFERENCES products(id),
    from_location_id INTEGER REFERENCES locations(id),
    to_location_id INTEGER REFERENCES locations(id),
    quantity INTEGER NOT NULL,
    unit_cost DECIMAL(10,2),
    reason_code VARCHAR(20),
    notes TEXT,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

7.2.3 Customer Tables
-- Customers table
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
    city VARCHAR(100),
    state VARCHAR(100),
    postal_code VARCHAR(20),
    country VARCHAR(2) DEFAULT 'SG',
    customer_type VARCHAR(20) DEFAULT 'RETAIL', -- RETAIL, WHOLESALE, VIP
    tax_id VARCHAR(50),
    credit_limit DECIMAL(10,2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0, -- Days
    is_active BOOLEAN DEFAULT true,
    birth_date DATE,
    anniversary_date DATE,
    loyalty_points INTEGER DEFAULT 0,
    loyalty_tier VARCHAR(20) DEFAULT 'BRONZE',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Customer groups table
CREATE TABLE customer_groups (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    discount_percentage DECIMAL(5,2) DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Customer group members junction table
CREATE TABLE customer_group_members (
    customer_id INTEGER REFERENCES customers(id) ON DELETE CASCADE,
    group_id INTEGER REFERENCES customer_groups(id) ON DELETE CASCADE,
    PRIMARY KEY (customer_id, group_id)
);

7.2.4 Transaction Tables
-- Transactions table
CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    transaction_type VARCHAR(20) NOT NULL, -- SALE, RETURN, EXCHANGE
    transaction_date TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    location_id INTEGER REFERENCES locations(id),
    register_id INTEGER REFERENCES registers(id),
    cashier_id INTEGER REFERENCES users(id),
    customer_id INTEGER REFERENCES customers(id),
    subtotal DECIMAL(10,2) NOT NULL DEFAULT 0,
    tax_amount DECIMAL(10,2) NOT NULL DEFAULT 0,
    discount_amount DECIMAL(10,2) NOT NULL DEFAULT 0,
    total_amount DECIMAL(10,2) NOT NULL DEFAULT 0,
    paid_amount DECIMAL(10,2) NOT NULL DEFAULT 0,
    change_amount DECIMAL(10,2) NOT NULL DEFAULT 0,
    status VARCHAR(20) NOT NULL DEFAULT 'COMPLETED', -- PENDING, COMPLETED, VOIDED
    void_reason TEXT,
    void_by INTEGER REFERENCES users(id),
    void_at TIMESTAMP,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Transaction items table
CREATE TABLE transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    product_id INTEGER REFERENCES products(id),
    quantity INTEGER NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    tax_amount DECIMAL(10,2) DEFAULT 0,
    total_amount DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2) NOT NULL,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Payments table
CREATE TABLE payments (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    payment_method_id INTEGER REFERENCES payment_methods(id),
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1.0,
    reference_number VARCHAR(100),
    card_last_four VARCHAR(4),
    authorization_code VARCHAR(50),
    is_approved BOOLEAN DEFAULT true,
    approval_message TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Payment methods table
CREATE TABLE payment_methods (
    id SERIAL PRIMARY KEY,
    code VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    type VARCHAR(20) NOT NULL, -- CASH, CARD, DIGITAL, VOUCHER
    is_active BOOLEAN DEFAULT true,
    requires_approval BOOLEAN DEFAULT false,
    opens_cash_drawer BOOLEAN DEFAULT true,
    sort_order INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

7.2.5 Accounting Tables
-- Chart of accounts table
CREATE TABLE chart_of_accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(20) NOT NULL, -- ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE
    parent_id INTEGER REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    is_system BOOLEAN DEFAULT false,
    normal_balance VARCHAR(10) NOT NULL, -- DEBIT, CREDIT
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Journal entries table
CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT NOT NULL,
    reference_type VARCHAR(20),
    reference_id INTEGER,
    is_posted BOOLEAN DEFAULT false,
    posted_by INTEGER REFERENCES users(id),
    posted_at TIMESTAMP,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Journal entry lines table
CREATE TABLE journal_entry_lines (
    id SERIAL PRIMARY KEY,
    journal_entry_id INTEGER REFERENCES journal_entries(id) ON DELETE CASCADE,
    account_id INTEGER REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(10,2) DEFAULT 0,
    credit_amount DECIMAL(10,2) DEFAULT 0,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT check_debit_credit CHECK (
        (debit_amount > 0 AND credit_amount = 0) OR 
        (debit_amount = 0 AND credit_amount > 0)
    )
);

7.3 Database Indexes
-- Performance indexes
CREATE INDEX idx_transactions_date ON transactions(transaction_date);
CREATE INDEX idx_transactions_customer ON transactions(customer_id);
CREATE INDEX idx_transaction_items_product ON transaction_items(product_id);
CREATE 
