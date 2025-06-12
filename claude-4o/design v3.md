<think> I need to create a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. Based on the requirements, this needs to be at least 6000 words and include detailed technical specifications, database schema, codebase structure, and environment setup instructions. The system should be built with Python, PySide6, and PostgreSQL, following a layered architecture with dependency injection, async processing, and other best practices.
Let me structure this PRD comprehensively to cover all required aspects:

Executive Summary
Project Overview
Functional Requirements
Technical Architecture
Database Schema Design
Codebase File Hierarchy
Application Modules & User Interaction
Key Modules and Files Description
Technology Stack
Development Environment Setup
Production Environment Setup
Additional Considerations (Security, Testing, Deployment, etc.)
</think>
Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Project Overview
Functional Requirements
Technical Architecture
Database Schema Design
Codebase File Hierarchy
Application Modules & User Interaction
Key Modules and Files Description
Technology Stack
Development Environment Setup
Production Environment Setup
Security Considerations
Testing Strategy
Deployment Strategy
Future Considerations
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) in Singapore. Built on a robust technology stack featuring Python, PySide6, and PostgreSQL, this system provides a professional-grade retail management solution that fully complies with Singapore's regulatory requirements, including GST regulations and multi-currency support.

The application architecture follows industry best practices, implementing a clean layered architecture with strict separation of concerns, dependency injection, asynchronous processing models, and comprehensive data integrity mechanisms. The system is designed to handle real-world business complexity while maintaining scalability, reliability, and ease of maintenance.

Key features include real-time inventory management, multi-payment method support, comprehensive GST compliance, customer relationship management, employee management with role-based access control, and extensive reporting capabilities. The system is built with future extensibility in mind, providing a solid foundation for additional features and integrations.

2. Project Overview
2.1 Business Context
Singapore's retail landscape demands sophisticated point-of-sale solutions that can handle complex regulatory requirements while providing intuitive user experiences. SMBs require systems that can manage inventory, process transactions efficiently, handle GST calculations accurately, and provide comprehensive business insights through reporting.

2.2 Project Goals
Primary Goal: Deliver a comprehensive POS system that meets all typical retail needs of Singapore SMBs
Secondary Goals:
Ensure full compliance with Singapore GST regulations
Provide multi-currency transaction support
Implement robust inventory management
Enable comprehensive business reporting
Maintain high performance and reliability
Ensure data security and integrity
2.3 Target Users
Primary Users: Cashiers, sales staff, and retail floor personnel
Secondary Users: Store managers, business owners, and administrators
Tertiary Users: Accountants and financial controllers
2.4 Success Metrics
Transaction processing time under 3 seconds
99.9% uptime during business hours
Zero GST calculation errors
Complete audit trail for all transactions
User satisfaction rating above 4.5/5
3. Functional Requirements
3.1 Core POS Functions
3.1.1 Transaction Processing
Quick Product Search: Barcode scanning, SKU lookup, and smart search functionality
Cart Management: Add/remove items, quantity adjustment, price overrides with authorization
Discount Application: Percentage and fixed amount discounts at item and transaction levels
Multi-Payment Support: Cash, credit/debit cards, e-wallets, vouchers, and split payments
Transaction Suspension: Hold and recall transactions for later completion
Receipt Generation: Customizable receipts with GST breakdown and business information
3.1.2 Inventory Management
Real-time Stock Tracking: Automatic stock deduction upon sale completion
Stock Alerts: Low stock notifications and reorder point management
Stock Adjustment: Manual adjustments with reason tracking
Product Variants: Support for size, color, and other variant attributes
Batch/Serial Number Tracking: For products requiring detailed tracking
Stock Transfer: Between locations for multi-outlet businesses
3.1.3 Customer Management
Customer Database: Comprehensive customer profiles with purchase history
Loyalty Program: Points accumulation and redemption system
Customer Groups: Tiered pricing and special discounts for customer segments
Contact Management: Email, SMS integration for marketing communications
Credit Management: Customer credit limits and payment terms
3.1.4 Employee Management
User Authentication: Secure login with password policies
Role-Based Access Control: Granular permissions for different user roles
Shift Management: Clock in/out functionality with break tracking
Commission Tracking: Sales commission calculation and reporting
Activity Logging: Comprehensive audit trail of all user actions
3.2 Financial Management
3.2.1 GST Compliance
Automatic GST Calculation: Based on current Singapore GST rates
GST-Inclusive/Exclusive Pricing: Flexible pricing models
GST Reports: GST F5, GST F7, and other regulatory reports
Tax Invoice Generation: Compliant with IRAS requirements
GST Rate Management: Support for different GST rates and exemptions
3.2.2 Multi-Currency Support
Currency Management: Support for major currencies with real-time exchange rates
Automatic Conversion: At point of sale with rounding rules
Multi-Currency Reporting: Financial reports in base and foreign currencies
Exchange Rate History: Historical rate tracking for audit purposes
3.2.3 Payment Processing
Cash Management: Cash drawer reconciliation and float management
Card Terminal Integration: Direct integration with payment terminals
E-Wallet Integration: Support for popular Singapore e-wallets
Payment Reconciliation: Daily settlement reports and discrepancy tracking
3.3 Reporting and Analytics
3.3.1 Sales Reports
Daily Sales Summary: Revenue, units sold, average transaction value
Product Performance: Best sellers, slow movers, profit margins
Hourly Sales Analysis: Peak hour identification and staffing optimization
Comparative Reports: Year-over-year, month-over-month comparisons
3.3.2 Financial Reports
Profit & Loss Statements: Comprehensive P&L with drill-down capabilities
Cash Flow Reports: Daily cash position and movement
Tax Reports: GST liability and input tax credit tracking
Accounts Receivable: Outstanding customer balances and aging
3.3.3 Inventory Reports
Stock Valuation: Current inventory value by various methods (FIFO, weighted average)
Stock Movement: Detailed tracking of all stock transactions
Reorder Reports: Items below reorder points
Dead Stock Analysis: Items with no movement over specified periods
3.4 System Administration
3.4.1 Configuration Management
Business Profile: Company information, logo, and receipt customization
System Parameters: Tax rates, rounding rules, default settings
Integration Settings: Third-party system configurations
Backup Configuration: Automated backup schedules and retention policies
3.4.2 Security Features
Data Encryption: At-rest and in-transit encryption
Access Logging: Comprehensive audit trails
Session Management: Automatic timeout and session controls
Data Privacy: PDPA compliance features
4. Technical Architecture
4.1 Architecture Overview
The SG POS system follows a clean, layered architecture pattern that ensures separation of concerns, maintainability, and scalability. The architecture consists of four primary layers:

4.1.1 Presentation Layer
Technology: PySide6 (Qt for Python)
Responsibility: User interface rendering, user input handling, and presentation logic
Key Components: Widgets, dialogs, view models, and UI controllers
4.1.2 Business Logic Layer
Technology: Pure Python with async/await patterns
Responsibility: Business rules, workflow orchestration, and transaction management
Key Components: Managers, validators, calculators, and business services
4.1.3 Data Access Layer
Technology: SQLAlchemy ORM with repository pattern
Responsibility: Database abstraction, query optimization, and data mapping
Key Components: Repositories, data services, and query builders
4.1.4 Persistence Layer
Technology: PostgreSQL database
Responsibility: Data storage, integrity constraints, and transactional consistency
Key Components: Tables, indexes, triggers, and stored procedures
4.2 Core Design Patterns
4.2.1 Dependency Injection
The system implements a comprehensive dependency injection pattern through the ApplicationCore class, which serves as the central service locator and dependency container. This approach provides:

Lazy initialization of services
Simplified testing through mock injection
Loose coupling between components
Centralized service lifecycle management
4.2.2 Repository Pattern
All data access is abstracted through repository interfaces, providing:

Database technology independence
Testable data access logic
Consistent query patterns
Optimized data fetching strategies
4.2.3 Data Transfer Objects (DTOs)
The system uses DTOs for data transfer between layers:

Type safety across layer boundaries
Decoupling of database models from business logic
Validation at layer boundaries
Optimized data serialization
4.2.4 Result Pattern
All service methods return Result objects that encapsulate:

Success/failure status
Return values for successful operations
Error details for failed operations
Chainable operations with monadic patterns
4.2.5 Observer Pattern
Event-driven communication between components:

Qt signals and slots for UI events
Custom event bus for business events
Decoupled component communication
Asynchronous event propagation
4.3 Asynchronous Architecture
The application implements a sophisticated asynchronous processing model:

4.3.1 Threading Model
Main Thread: Qt event loop for UI responsiveness
Worker Thread: Asyncio event loop for background operations
Database Thread Pool: Connection pooling for concurrent database access
Task Queue: Priority-based task scheduling
4.3.2 Inter-Thread Communication
Qt Signals: Safe communication from worker threads to UI
Asyncio Futures: Promise-based async operations
Thread-Safe Queues: Message passing between threads
Lock-Free Data Structures: Where appropriate for performance
5. Database Schema Design
5.1 Schema Overview
The database schema is designed with normalization, referential integrity, and performance optimization in mind. It consists of several logical groups of tables:

5.2 Core Tables
-- Company and Configuration Tables
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE NOT NULL,
    gst_registration_number VARCHAR(50),
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    logo_url TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE outlets (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    code VARCHAR(50) UNIQUE NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- User Management Tables
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    employee_id VARCHAR(50) UNIQUE,
    is_active BOOLEAN DEFAULT true,
    last_login_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    is_system BOOLEAN DEFAULT false,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE permissions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    module VARCHAR(100) NOT NULL,
    action VARCHAR(100) NOT NULL,
    description TEXT,
    UNIQUE(module, action)
);

CREATE TABLE role_permissions (
    role_id UUID REFERENCES roles(id) ON DELETE CASCADE,
    permission_id UUID REFERENCES permissions(id) ON DELETE CASCADE,
    PRIMARY KEY (role_id, permission_id)
);

CREATE TABLE user_roles (
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    role_id UUID REFERENCES roles(id) ON DELETE CASCADE,
    outlet_id UUID REFERENCES outlets(id) ON DELETE CASCADE,
    assigned_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    assigned_by UUID REFERENCES users(id),
    PRIMARY KEY (user_id, role_id, outlet_id)
);

-- Product Management Tables
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    parent_id UUID REFERENCES categories(id),
    display_order INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE brands (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) UNIQUE NOT NULL,
    logo_url TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sku VARCHAR(100) UNIQUE NOT NULL,
    barcode VARCHAR(100) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id UUID REFERENCES categories(id),
    brand_id UUID REFERENCES brands(id),
    unit_of_measure VARCHAR(50) DEFAULT 'PIECE',
    is_active BOOLEAN DEFAULT true,
    is_service BOOLEAN DEFAULT false,
    track_inventory BOOLEAN DEFAULT true,
    allow_decimal_quantity BOOLEAN DEFAULT false,
    gst_rate DECIMAL(5,2) DEFAULT 9.00,
    is_gst_inclusive BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID REFERENCES products(id) ON DELETE CASCADE,
    sku VARCHAR(100) UNIQUE NOT NULL,
    barcode VARCHAR(100) UNIQUE,
    variant_name VARCHAR(255) NOT NULL,
    attributes JSONB,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE product_prices (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID REFERENCES products(id) ON DELETE CASCADE,
    variant_id UUID REFERENCES product_variants(id) ON DELETE CASCADE,
    price_type VARCHAR(50) NOT NULL, -- 'STANDARD', 'PROMOTIONAL', 'MEMBER'
    currency_code VARCHAR(3) DEFAULT 'SGD',
    price DECIMAL(10,2) NOT NULL,
    min_quantity INTEGER DEFAULT 1,
    valid_from DATE NOT NULL,
    valid_to DATE,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, variant_id, price_type, currency_code, valid_from)
);

-- Inventory Management Tables
CREATE TABLE stock_locations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    outlet_id UUID REFERENCES outlets(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    code VARCHAR(50) NOT NULL,
    is_default BOOLEAN DEFAULT false,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(outlet_id, code)
);

CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID REFERENCES products(id) ON DELETE CASCADE,
    variant_id UUID REFERENCES product_variants(id) ON DELETE CASCADE,
    location_id UUID REFERENCES stock_locations(id) ON DELETE CASCADE,
    quantity DECIMAL(10,3) NOT NULL DEFAULT 0,
    reserved_quantity DECIMAL(10,3) NOT NULL DEFAULT 0,
    reorder_point DECIMAL(10,3),
    reorder_quantity DECIMAL(10,3),
    last_counted_at TIMESTAMP WITH TIME ZONE,
    last_counted_quantity DECIMAL(10,3),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, variant_id, location_id)
);

CREATE TABLE stock_movements (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    movement_type VARCHAR(50) NOT NULL, -- 'PURCHASE', 'SALE', 'ADJUSTMENT', 'TRANSFER'
    reference_type VARCHAR(50),
    reference_id UUID,
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    from_location_id UUID REFERENCES stock_locations(id),
    to_location_id UUID REFERENCES stock_locations(id),
    quantity DECIMAL(10,3) NOT NULL,
    unit_cost DECIMAL(10,2),
    reason TEXT,
    performed_by UUID REFERENCES users(id),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Customer Management Tables
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_code VARCHAR(50) UNIQUE NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    company_name VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(20),
    mobile VARCHAR(20),
    address TEXT,
    postal_code VARCHAR(10),
    date_of_birth DATE,
    gender VARCHAR(20),
    customer_group_id UUID,
    loyalty_card_number VARCHAR(50) UNIQUE,
    loyalty_points DECIMAL(10,2) DEFAULT 0,
    credit_limit DECIMAL(10,2) DEFAULT 0,
    outstanding_balance DECIMAL(10,2) DEFAULT 0,
    tax_id VARCHAR(50),
    notes TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE customer_groups (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) UNIQUE NOT NULL,
    discount_percentage DECIMAL(5,2) DEFAULT 0,
    price_tier VARCHAR(50),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Transaction Tables
CREATE TABLE transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    outlet_id UUID REFERENCES outlets(id),
    register_id UUID,
    cashier_id UUID REFERENCES users(id),
    customer_id UUID REFERENCES customers(id),
    transaction_type VARCHAR(50) NOT NULL, -- 'SALE', 'RETURN', 'EXCHANGE'
    status VARCHAR(50) NOT NULL, -- 'COMPLETED', 'VOIDED', 'SUSPENDED'
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1,
    subtotal DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    tax_amount DECIMAL(10,2) NOT NULL,
    total_amount DECIMAL(10,2) NOT NULL,
    paid_amount DECIMAL(10,2) DEFAULT 0,
    change_amount DECIMAL(10,2) DEFAULT 0,
    notes TEXT,
    voided_by UUID REFERENCES users(id),
    voided_at TIMESTAMP WITH TIME ZONE,
    void_reason TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    completed_at TIMESTAMP WITH TIME ZONE
);

CREATE TABLE transaction_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID REFERENCES transactions(id) ON DELETE CASCADE,
    line_number INTEGER NOT NULL,
    product_id UUID REFERENCES products(id),
    variant_id UUID REFERENCES product_variants(id),
    description VARCHAR(255) NOT NULL,
    quantity DECIMAL(10,3) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    discount_percentage DECIMAL(5,2) DEFAULT 0,
    tax_rate DECIMAL(5,2) NOT NULL,
    tax_amount DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(10,2) NOT NULL,
    cost DECIMAL(10,2),
    sales_person_id UUID REFERENCES users(id),
    commission_rate DECIMAL(5,2) DEFAULT 0,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(transaction_id, line_number)
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id UUID REFERENCES transactions(id) ON DELETE CASCADE,
    payment_method VARCHAR(50) NOT NULL, -- 'CASH', 'CARD', 'EWALLET', 'VOUCHER'
    amount DECIMAL(10,2) NOT NULL,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1,
    reference_number VARCHAR(100),
    card_type VARCHAR(50),
    card_last_four VARCHAR(4),
    approval_code VARCHAR(50),
    processed_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    processor_response JSONB
);

-- Financial Tables
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    account_code VARCHAR(50) UNIQUE NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL, -- 'ASSET', 'LIABILITY', 'EQUITY', 'REVENUE', 'EXPENSE'
    parent_id UUID REFERENCES chart_of_accounts(id),
    currency_code VARCHAR(3) DEFAULT 'SGD',
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    description TEXT,
    reference_type VARCHAR(50),
    reference_id UUID,
    status VARCHAR(50) DEFAULT 'POSTED',
    created_by UUID REFERENCES users(id),
    posted_by UUID REFERENCES users(id),
    posted_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE journal_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    journal_entry_id UUID REFERENCES journal_entries(id) ON DELETE CASCADE,
    line_number INTEGER NOT NULL,
    account_id UUID REFERENCES chart_of_accounts(id),
    description TEXT,
    debit_amount DECIMAL(10,2) DEFAULT 0,
    credit_amount DECIMAL(10,2) DEFAULT 0,
    currency_code VARCHAR(3) DEFAULT 'SGD',
    exchange_rate DECIMAL(10,6) DEFAULT 1,
    UNIQUE(journal_entry_id, line_number),
    CHECK (debit_amount >= 0 AND credit_amount >= 0),
    CHECK (NOT (debit_amount > 0 AND credit_amount > 0))
);

-- System Tables
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    action VARCHAR(100) NOT NULL,
    entity_type VARCHAR(100),
    entity_id UUID,
    old_values JSONB,
    new_values JSONB,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE system_settings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    category VARCHAR(100) NOT NULL,
    key VARCHAR(100) NOT NULL,
    value TEXT,
    data_type VARCHAR(50) NOT NULL,
    is_encrypted BOOLEAN DEFAULT false,
    updated_by UUID REFERENCES users(id),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(category, key)
);

-- Indexes for Performance
CREATE INDEX idx_transactions_outlet_date ON transactions(outlet_id, created_at);
CREATE INDEX idx_transactions_customer ON transactions(customer_id);
CREATE INDEX idx_transaction_items_product ON transaction_items(product_id);
CREATE INDEX idx_inventory_product_location ON inventory(product_id, location_id);
CREATE INDEX idx_stock_movements_product_date ON stock_movements(product_id, created_at);
CREATE INDEX idx_customers_email ON customers(email);
CREATE INDEX idx_customers_phone ON customers(phone);
CREATE INDEX idx_audit_logs_user_date ON audit_logs(user_id, created_at);

5.3 Database Triggers and Functions
-- Auto-update timestamp trigger
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

-- Apply trigger to all tables with updated_at column
CREATE TRIGGER update_companies_updated_at BEFORE UPDATE ON companies
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
-- Repeat for all tables with updated_at column

-- Inventory update trigger
CREATE OR REPLACE FUNCTION update_inventory_on_sale()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.status = 'COMPLETED' AND OLD.status != 'COMPLETED' THEN
        UPDATE inventory i
        SET quantity = quantity - ti.quantity,
            updated_at = CURRENT_TIMESTAMP
        FROM transaction_items ti
        WHERE ti.transaction_id = NEW.id
          AND i.product_id = ti.product_id
          AND (i.variant_id = ti.variant_id OR (i.variant_id IS NULL AND ti.variant_id IS NULL));
    END IF;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER trigger_update_inventory_on_sale
    AFTER UPDATE ON transactions
    FOR EACH ROW
    EXECUTE FUNCTION update_inventory_on_sale();

-- Generate transaction number function
CREATE OR REPLACE FUNCTION generate_transaction_number(outlet_code VARCHAR)
RETURNS VARCHAR AS $$
DECLARE
    new_number VARCHAR;
    counter INTEGER;
BEGIN
    SELECT COUNT(*) + 1 INTO counter
    FROM transactions
    WHERE transaction_number LIKE outlet_code || '-' || TO_CHAR(CURRENT_DATE, 'YYYYMMDD') || '%';
    
    new_number := outlet_code || '-' || TO_CHAR(CURRENT_DATE, 'YYYYMMDD') || '-' || LPAD(counter::TEXT, 4, '0');
    RETURN new_number;
END;
$$ language 'plpgsql';

6. Codebase File Hierarchy
sg-pos/
├── app/
│   ├── __init__.py
│   ├── main.py                          # Application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application_core.py          # Dependency injection container
│   │   ├── config.py                    # Configuration management
│   │   ├── constants.py                 # Application constants
│   │   ├── exceptions.py                # Custom exception classes
│   │   ├── result.py                    # Result pattern implementation
│   │   └── decorators.py                # Common decorators
│   │
│   ├── models/                          # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                      # Base model class
│   │   ├── company.py
│   │   ├── user.py
│   │   ├── product.py
│   │   ├── inventory.py
│   │   ├── customer.py
│   │   ├── transaction.py
│   │   ├── payment.py
│   │   └── financial.py
│   │
│   ├── dto/                             # Data Transfer Objects
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── product_dto.py
│   │   ├── transaction_dto.py
│   │   ├── customer_dto.py
│   │   ├── inventory_dto.py
│   │   └── report_dto.py
│   │
│   ├── services/                        # Data access services
│   │   ├── __init__.py
│   │   ├── base_service.py
│   │   ├── database_service.py
│   │   ├── product_service.py
│   │   ├── inventory_service.py
│   │   ├── customer_service.py
│   │   ├── transaction_service.py
│   │   ├── payment_service.py
│   │   ├── user_service.py
│   │   └── report_service.py
│   │
│   ├── business_logic/                  # Business logic managers
│   │   ├── __init__.py
│   │   ├── base_manager.py
│   │   ├── auth_manager.py
│   │   ├── product_manager.py
│   │   ├── inventory_manager.py
│   │   ├── sales_manager.py
│   │   ├── customer_manager.py
│   │   ├── payment_manager.py
│   │   ├── discount_manager.py
│   │   ├── gst_manager.py
│   │   └── report_manager.py
│   │
│   ├── accounting/                      # Accounting specific logic
│   │   ├── __init__.py
│   │   ├── journal_manager.py
│   │   ├── chart_of_accounts_manager.py
│   │   ├── gst_calculator.py
│   │   └── financial_report_manager.py
│   │
│   ├── ui/                              # PySide6 UI components
│   │   ├── __init__.py
│   │   ├── main_window.py
│   │   ├── styles/
│   │   │   ├── __init__.py
│   │   │   ├── theme.py
│   │   │   └── stylesheets.qss
│   │   │
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── base_widget.py
│   │   │   ├── pos_widget.py
│   │   │   ├── product_search_widget.py
│   │   │   ├── cart_widget.py
│   │   │   ├── payment_widget.py
│   │   │   ├── customer_widget.py
│   │   │   ├── inventory_widget.py
│   │   │   ├── reports_widget.py
│   │   │   └── settings_widget.py
│   │   │
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── base_dialog.py
│   │   │   ├── login_dialog.py
│   │   │   ├── product_dialog.py
│   │   │   ├── customer_dialog.py
│   │   │   ├── payment_dialog.py
│   │   │   ├── discount_dialog.py
│   │   │   └── refund_dialog.py
│   │   │
│   │   └── models/                      # Qt models for views
│   │       ├── __init__.py
│   │       ├── product_model.py
│   │       ├── transaction_model.py
│   │       ├── customer_model.py
│   │       └── inventory_model.py
│   │
│   ├── integrations/                    # Third-party integrations
│   │   ├── __init__.py
│   │   ├── payment_gateway/
│   │   │   ├── __init__.py
│   │   │   ├── base_gateway.py
│   │   │   ├── stripe_gateway.py
│   │   │   └── nets_gateway.py
│   │   │
│   │   ├── accounting/
│   │   │   ├── __init__.py
│   │   │   └── quickbooks_integration.py
│   │   │
│   │   └── email/
│   │       ├── __init__.py
│   │       └── email_service.py
│   │
│   └── utils/                           # Utility functions
│       ├── __init__.py
│       ├── validators.py
│       ├── formatters.py
│       ├── crypto.py
│       ├── barcode.py
│       ├── receipt_printer.py
│       └── async_utils.py
│
├── tests/                               # Test suite
│   ├── __init__.py
│   ├── conftest.py
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_models/
│   │   ├── test_services/
│   │   ├── test_managers/
│   │   └── test_utils/
│   │
│   ├── integration/
│   │   ├── __init__.py
│   │   ├── test_transactions/
│   │   ├── test_inventory/
│   │   └── test_reports/
│   │
│   └── e2e/
│       ├── __init__.py
│       └── test_workflows/
│
├── scripts/                             # Database and utility scripts
│   ├── __init__.py
│   ├── create_database.py
│   ├── migrate_database.py
│   ├── seed_data.py
│   └── backup_database.py
│
├── migrations/                          # Database migrations
│   ├── alembic.ini
│   ├── env.py
│   └── versions/
│
├── config/                              # Configuration files
│   ├── development.yaml
│   ├── production.yaml
│   ├── testing.yaml
│   └── logging.yaml
│
├── resources/                           # Static resources
│   ├── images/
│   ├── icons/
│   ├── fonts/
│   └── translations/
│
├── docs/                                # Documentation
│   ├── api/
│   ├── user_manual/
│   ├── deployment/
│   └── architecture/
│
├── requirements/                        # Dependency specifications
│   ├── base.txt
│   ├── development.txt
│   ├── production.txt
│   └── testing.txt
│
├── .env.example                         # Environment variables template
├── .gitignore
├── README.md
├── LICENSE
├── setup.py
└── pyproject.toml
7. Application Modules & User Interaction
7.1 Module Architecture Diagram
┌─────────────────────────────────────────────────────────────────────┐
│                          Presentation Layer                          │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────┐  ┌─────────┐ │
│  │ Main Window │  │ POS Widget   │  │   Dialogs    │  │ Reports │ │
│  └──────┬──────┘  └──────┬───────┘  └──────┬───────┘  └────┬────┘ │
└─────────┼─────────────────┼─────────────────┼───────────────┼──────┘
          │                 │                 │               │
          ▼                 ▼                 ▼               ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      Application Core (DI Container)                 │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ Lazy-loaded Managers: Auth, Product, Sales, Customer, Payment  │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        Business Logic Layer                          │
│  ┌──────────────┐  ┌─────────────┐  ┌──────────────┐  ┌─────────┐ │
│  │Sales Manager │  │ GST Manager │  │Inventory Mgr │  │ Others  │ │
│  └──────┬───────┘  └──────┬──────┘  └──────┬───────┘  └────┬────┘ │
└─────────┼──────────────────┼────────────────┼───────────────┼──────┘
          │                  │                │               │
          ▼                  ▼                ▼               ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         Data Access Layer                            │
│  ┌─────────────────┐  ┌──────────────────┐  ┌──────────────────┐  │
│  │ Product Service │  │Transaction Service│  │ Customer Service │  │
│  └────────┬────────┘  └────────┬─────────┘  └────────┬─────────┘  │
└───────────┼─────────────────────┼──────────────────────┼───────────┘
            │                     │                      │
            ▼                     ▼                      ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         PostgreSQL Database                          │
└─────────────────────────────────────────────────────────────────────┘
7.2 User Interaction Flow
7.2.1 Point of Sale Transaction Flow
User                    POS Widget           Sales Manager         Database
 │                          │                      │                   │
 │──Scan/Search Product────▶│                      │                   │
 │                          │──Get Product Info───▶│                   │
 │                          │                      │──Query Product───▶│
 │                          │                      │◀─────Result───────│
 │                          │◀───Product Details───│                   │
 │◀────Display Product──────│                      │                   │
 │                          │                      │                   │
 │──Add to Cart────────────▶│                      │                   │
 │                          │──Calculate Totals───▶│                   │
 │                          │◀───Updated Cart──────│                   │
 │◀────Show Cart────────────│                      │                   │
 │                          │                      │                   │
 │──Proceed to Payment─────▶│                      │                   │
 │                          │──Validate Cart──────▶│                   │
 │                          │◀───Validation OK─────│                   │
 │◀────Payment Dialog───────│                      │                   │
 │                          │                      │                   │
 │──Select Payment Method──▶│                      │                   │
 │──Enter Amount───────────▶│                      │                   │
 │                          │──Process Payment────▶│                   │
 │                          │                      │──Begin Trans─────▶│
 │                          │                      │──Save Trans──────▶│
 │                          │                      │──Update Stock────▶│
 │                          │                      │──Create Journal──▶│
 │                          │                      │◀─────Success──────│
 │                          │◀───Payment Complete──│                   │
 │◀────Receipt──────────────│                      │                   │
7.2.2 Inventory Management Flow
User                 Inventory Widget      Inventory Manager      Database
 │                          │                      │                   │
 │──View Stock Levels──────▶│                      │                   │
 │                          │──Request Stock Data─▶│                   │
 │                          │                      │──Query Inventory─▶│
 │                          │                      │◀────Stock Data────│
 │                          │◀───Stock Levels──────│                   │
 │◀────Display Grid─────────│                      │                   │
 │                          │                      │                   │
 │──Adjust Stock───────────▶│                      │                   │
 │                          │──Show Adjustment─────│                   │
 │◀────Adjustment Dialog────│      Dialog          │                   │
 │                          │                      │                   │
 │──Enter Quantity─────────▶│                      │                   │
 │──Enter Reason───────────▶│                      │                   │
 │──Confirm────────────────▶│                      │                   │
 │                          │──Process Adjustment─▶│                   │
 │                          │                      │──Validate─────────│
 │                          │                      │──Update Stock────▶│
 │                          │                      │──Log Movement────▶│
 │                          │                      │◀────Success───────│
 │                          │◀───Update Complete───│                   │
 │◀────Refresh Display──────│                      │                   │
8. Key Modules and Files Description
8.1 Core Modules
8.1.1 ApplicationCore (app/core/application_core.py)
The ApplicationCore class serves as the central dependency injection container and service locator for the entire application. Key features include:

Lazy Initialization: All managers are initialized only when first accessed through property decorators
Singleton Pattern: Ensures only one instance of each manager exists throughout the application lifecycle
Service Registry: Maintains references to all major services and managers
Configuration Management: Loads and manages application configuration
Event Bus: Provides application-wide event publishing and subscription
class ApplicationCore:
    def __init__(self, config_path: str):
        self._config = self._load_config(config_path)
        self._db_service = None
        self._auth_manager = None
        self._sales_manager = None
        # ... other manager references
        
    @property
    def auth_manager(self) -> AuthManager:
        if self._auth_manager is None:
            self._auth_manager = AuthManager(self)
        return self._auth_manager
        
    @property
    def sales_manager(self) -> SalesManager:
        if self._sales_manager is None:
            self._sales_manager = SalesManager(self)
        return self._sales_manager

8.1.2 Result Pattern (app/core/result.py)
The Result pattern provides a consistent way to handle success and failure cases throughout the application:

@dataclass
class Result(Generic[T]):
    success: bool
    value: Optional[T] = None
    error: Optional[str] = None
    error_code: Optional[str] = None
    
    @classmethod
    def ok(cls, value: T) -> 'Result[T]':
        return cls(success=True, value=value)
        
    @classmethod
    def fail(cls, error: str, error_code: Optional[str] = None) -> 'Result[T]':
        return cls(success=False, error=error, error_code=error_code)
        
    def map(self, func: Callable[[T], U]) -> 'Result[U]':
        if self.success:
            return Result.ok(func(self.value))
        return Result.fail(self.error, self.error_code)

8.2 Business Logic Managers
8.2.1 SalesManager (app/business_logic/sales_manager.py)
Orchestrates the entire sales transaction workflow:

Transaction Creation: Manages transaction lifecycle from creation to completion
Cart Management: Handles adding, removing, and modifying items
Discount Application: Applies various discount rules and validations
Payment Coordination: Coordinates with PaymentManager for payment processing
Inventory Updates: Triggers inventory updates upon transaction completion
GST Calculation: Integrates with GSTManager for tax calculations
Key methods:

create_transaction(): Initializes a new transaction
add_item_to_cart(): Adds products with validation
apply_discount(): Handles discount logic and authorization
complete_transaction(): Finalizes sale with all necessary updates
8.2.2 InventoryManager (app/business_logic/inventory_manager.py)
Manages all inventory-related operations:

Stock Level Tracking: Real-time inventory levels across locations
Stock Movements: Records all inventory changes with audit trail
Reorder Management: Monitors reorder points and generates alerts
Stock Adjustments: Handles manual adjustments with reason tracking
Transfer Management: Manages stock transfers between locations
Key methods:

get_stock_levels(): Retrieves current stock for products
adjust_stock(): Processes manual stock adjustments
transfer_stock(): Handles inter-location transfers
check_availability(): Validates stock for sales
8.2.3 PaymentManager (app/business_logic/payment_manager.py)
Handles all payment processing logic:

Multi-Payment Support: Processes multiple payment types in single transaction
Gateway Integration: Interfaces with payment gateways
Change Calculation: Handles cash payments and change
Payment Validation: Ensures payment totals match transaction
Refund Processing: Manages refunds and reversals
8.3 Data Services
8.3.1 BaseService (app/services/base_service.py)
Abstract base class for all data services implementing common patterns:

class BaseService(ABC, Generic[T]):
    def __init__(self, db_service: DatabaseService):
        self.db_service = db_service
        
    async def get_by_id(self, id: UUID) -> Result[T]:
        async with self.db_service.get_session() as session:
            try:
                result = await session.get(self.model_class, id)
                if result:
                    return Result.ok(result)
                return Result.fail("Not found", "NOT_FOUND")
            except Exception as e:
                return Result.fail(str(e), "DATABASE_ERROR")

8.3.2 TransactionService (app/services/transaction_service.py)
Provides data access for transaction-related operations:

CRUD Operations: Create, read, update, delete transactions
Complex Queries: Daily summaries, sales reports, performance metrics
Batch Operations: Bulk status updates, mass void operations
Transaction Search: Advanced search with multiple criteria
8.4 UI Components
8.4.1 MainWindow (app/ui/main_window.py)
The main application window that:

Navigation Management: Handles switching between different modules
User Context: Maintains current user session and permissions
Status Updates: Shows real-time status messages and notifications
Quick Actions: Provides toolbar for common operations
8.4.2 POSWidget (app/ui/widgets/pos_widget.py)
The primary point-of-sale interface featuring:

Product Search: Barcode scanning and text search
Cart Display: Real-time cart updates with totals
Customer Selection: Quick customer lookup and selection
Payment Initiation: Launches payment dialog
Transaction Info: Shows current transaction details
8.4.3 PaymentDialog (app/ui/dialogs/payment_dialog.py)
Sophisticated payment handling dialog:

Payment Method Tabs: Separate tabs for each payment type
Amount Validation: Ensures correct payment amounts
Change Display: Real-time change calculation
Receipt Options: Print, email, or SMS receipt
Payment Confirmation: Final confirmation before processing
8.5 Integration Modules
8.5.1 Payment Gateway Integration (app/integrations/payment_gateway/)
Abstract base class and implementations for payment processing:

class BasePaymentGateway(ABC):
    @abstractmethod
    async def process_payment(self, amount: Decimal, 
                            payment_details: Dict) -> Result[PaymentResponse]:
        pass
        
    @abstractmethod
    async def refund_payment(self, transaction_id: str, 
                           amount: Decimal) -> Result[RefundResponse]:
        pass

8.6 Utility Modules
8.6.1 Validators (app/utils/validators.py)
Comprehensive validation functions:

NRIC/FIN Validation: Singapore ID validation
GST Registration: Validates GST registration numbers
Phone Numbers: Singapore phone number formats
Email Validation: RFC-compliant email validation
Postal Codes: Singapore postal code validation
8.6.2 Receipt Printer (app/utils/receipt_printer.py)
Handles receipt generation and printing:

Template Engine: Customizable receipt templates
Printer Communication: Direct communication with POS printers
Format Support: ESC/POS command generation
Error Handling: Graceful handling of printer errors
9. Technology Stack
9.1 Core Technologies
9.1.1 Programming Language
Python 3.11+: Latest stable Python version for optimal performance and features
Type Hints: Comprehensive type annotations for better IDE support and runtime validation
Async/Await: Native coroutine support for asynchronous operations
9.1.2 GUI Framework
PySide6 (Qt6): Modern, cross-platform GUI framework
Qt Designer: For rapid UI prototyping
QML: For advanced UI components where needed
Custom Widgets: Extended Qt widgets for specialized functionality
9.1.3 Database
PostgreSQL 15+: Enterprise-grade relational database
PostGIS: Spatial data support for location-based features
Full-Text Search: Built-in FTS for product search
JSONB: For flexible schema requirements
9.1.4 ORM and Database Tools
SQLAlchemy 2.0+: Modern ORM with async support
Alembic: Database migration management
asyncpg: High-performance PostgreSQL driver
9.2 Supporting Libraries
9.2.1 Data Processing
Pandas: Data analysis and reporting
NumPy: Numerical computations
Decimal: Precise monetary calculations
9.2.2 Networking and API
aiohttp: Async HTTP client/server
httpx: Modern HTTP client with async support
websockets: Real-time communication
9.2.3 Security
