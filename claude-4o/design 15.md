The user wants a comprehensive Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. They've specified it should be at least 6000 words and include:
Database schema design
Codebase file hierarchy diagram
Application modules and user interaction diagram
Listing and description of key application modules and files
Technology stack description
Development and production environment setup
The architectural considerations they've provided show they want:

Clean layered architecture (Presentation, Business Logic, Data Access, Persistence)
Dependency injection via ApplicationCore
Asynchronous processing model
Best practices like DTOs and Result pattern
Multi-currency support
Singapore regulatory compliance
I'll structure this as a comprehensive PRD that covers all these aspects in detail, ensuring it's well-thought-out and leaves no ambiguity for implementation. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Project Overview
Business Requirements
Functional Requirements
Non-Functional Requirements
Technology Stack
System Architecture
Database Schema Design
Application Modules and Components
Codebase File Hierarchy
User Interaction Flow
Key Modules and Files Description
Development Environment Setup
Production Environment Setup
Security Considerations
Testing Strategy
Deployment Strategy
Maintenance and Support
Future Enhancements
Appendices
1. Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) operating in Singapore. Built with modern technologies including Python, PySide6, and PostgreSQL, this system provides a professional-grade retail management solution that fully complies with Singapore's regulatory requirements, including GST reporting and multi-currency support.

The application employs a clean, layered architecture with strict separation of concerns, implementing industry best practices such as dependency injection, data transfer objects (DTOs), and the Result pattern. Its robust asynchronous processing model ensures responsive user interactions while maintaining data integrity through comprehensive transaction management and validation mechanisms.

Key differentiators include:

Full compliance with Singapore's GST requirements and IRAS reporting standards
Multi-currency support with real-time exchange rate management
Integrated accounting system with double-entry bookkeeping
Comprehensive inventory management with real-time stock tracking
Advanced reporting and analytics capabilities
Scalable architecture supporting future growth and feature expansion
2. Project Overview
2.1 Project Goals
The primary goal is to develop a modern, efficient, and user-friendly POS system that addresses the unique needs of Singapore's retail sector while providing a foundation for future growth and expansion. The system aims to:

Streamline retail operations through intuitive workflows and automation
Ensure regulatory compliance with minimal manual intervention
Provide real-time business insights through comprehensive reporting
Support business growth through scalable architecture
Minimize training requirements through intuitive user interface design
2.2 Target Market
The SG POS System targets small to medium-sized retail businesses in Singapore, including:

Independent retail stores
Chain stores with multiple outlets
Specialty shops and boutiques
Service-based businesses requiring point-of-sale capabilities
Businesses requiring multi-currency transaction support
2.3 Success Criteria
Success will be measured by:

System reliability with 99.9% uptime during business hours
Transaction processing time under 2 seconds
Zero data loss or corruption incidents
Full GST compliance with automated reporting
User adoption rate above 90% within first month
Reduction in checkout time by at least 30%
3. Business Requirements
3.1 Core Business Needs
The system must address fundamental retail business operations:

Sales Processing

Quick and accurate transaction processing
Support for multiple payment methods
Real-time inventory updates
Customer information management
Receipt generation and printing
Inventory Management

Real-time stock level tracking
Low stock alerts and reorder management
Product categorization and variants
Barcode scanning support
Stock movement tracking
Financial Management

Integrated accounting with double-entry bookkeeping
Multi-currency support with exchange rate management
GST calculation and reporting
Daily cash reconciliation
Financial reporting and analytics
Customer Relationship Management

Customer profile management
Purchase history tracking
Loyalty program support
Customer analytics and insights
Marketing campaign integration
3.2 Singapore-Specific Requirements
GST Compliance

Automated GST calculation based on current rates
GST-inclusive and GST-exclusive pricing support
GST registration number validation
IRAS-compliant GST reporting formats
GST refund scheme support for tourists
Multi-Currency Operations

Support for SGD as base currency
Common foreign currency acceptance (USD, EUR, MYR, etc.)
Real-time exchange rate updates
Currency conversion tracking for accounting
Multi-currency reporting capabilities
Regulatory Compliance

Data protection compliance (PDPA)
Electronic transaction records retention
Audit trail maintenance
Business registration integration
Payment gateway compliance (PCI DSS where applicable)
4. Functional Requirements
4.1 User Management
User Authentication

Secure login with username/password
Role-based access control (RBAC)
Session management with automatic timeout
Password complexity requirements
Account lockout after failed attempts
User Roles

Administrator: Full system access
Manager: Access to reports and configuration
Cashier: POS operations only
Accountant: Financial modules access
Inventory Staff: Stock management access
4.2 Point of Sale Operations
Transaction Processing

Barcode scanning for quick item entry
Manual product search and selection
Quantity adjustment and price override (with permissions)
Discount application (percentage or fixed amount)
Tax calculation and display
Multiple payment method support per transaction
Change calculation and display
Transaction suspension and retrieval
Refund and exchange processing
Payment Methods

Cash with change calculation
Credit/Debit card integration
Mobile payment support (PayNow, GrabPay, etc.)
Vouchers and gift cards
Store credit management
Split payment across multiple methods
Receipt Management

Customizable receipt templates
Email receipt option
Receipt reprint functionality
Digital receipt storage
QR code generation for digital receipts
4.3 Inventory Management
Product Management

Product creation with multiple attributes
Variant management (size, color, etc.)
Barcode generation and printing
Product categorization and tagging
Supplier information linkage
Cost and pricing management
Product image support
Stock Control

Real-time stock level tracking
Stock adjustment with reason codes
Stock transfer between locations
Stock take functionality
Expiry date tracking for perishables
Serial number tracking for electronics
Low stock alerts and notifications
Purchase Orders

PO creation and management
Supplier catalog integration
Automatic reorder point suggestions
PO approval workflow
Goods receipt processing
Purchase return management
4.4 Customer Management
Customer Profiles

Customer registration and data capture
Contact information management
Purchase history tracking
Customer notes and preferences
Birthday and anniversary tracking
Customer segmentation
Loyalty Programs

Points-based loyalty system
Tier-based membership levels
Loyalty point earning rules
Point redemption options
Member-exclusive promotions
Loyalty program analytics
4.5 Financial Management
Accounting Integration

Chart of accounts management
Journal entry creation
Account reconciliation
Trial balance generation
Financial statement preparation
Multi-currency accounting
Cash Management

Cash drawer management
Daily cash reconciliation
Cash float tracking
Petty cash management
Bank deposit preparation
Cash variance reporting
GST Management

Automated GST calculation
GST report generation (GST F5, GST F7)
Input tax tracking
Output tax management
GST clearing account reconciliation
Tourist refund scheme support
4.6 Reporting and Analytics
Sales Reports

Daily sales summary
Sales by product/category
Sales by time period
Sales by payment method
Sales by staff member
Top selling products
Financial Reports

Profit and loss statement
Cash flow report
GST reports
Accounts receivable aging
Accounts payable aging
Financial dashboard
Inventory Reports

Stock level report
Stock movement report
Stock valuation report
Slow-moving items report
Stock variance report
Reorder report
Customer Reports

Customer purchase analysis
Customer segmentation report
Loyalty program performance
Customer lifetime value
Customer retention analysis
5. Non-Functional Requirements
5.1 Performance Requirements
Response Time

Transaction processing: < 2 seconds
Report generation: < 5 seconds for standard reports
Search operations: < 1 second
Screen navigation: < 0.5 seconds
Database queries: < 1 second for common operations
Throughput

Support 100+ transactions per hour per terminal
Handle 10+ concurrent users
Process 1000+ SKUs without performance degradation
Generate reports for 1 year of data within 10 seconds
Resource Usage

Maximum 4GB RAM usage under normal operations
CPU usage below 50% during peak operations
Database size growth < 1GB per year for typical SMB
Network bandwidth < 10 Mbps for cloud sync
5.2 Reliability Requirements
Availability

99.9% uptime during business hours
Graceful degradation for non-critical features
Automatic recovery from temporary failures
Offline mode for core POS functions
Data Integrity

Zero data loss tolerance
ACID compliance for all transactions
Automatic backup every 4 hours
Point-in-time recovery capability
Data validation at all entry points
5.3 Usability Requirements
User Interface

Intuitive navigation with minimal clicks
Consistent UI patterns across modules
Responsive design for different screen sizes
Keyboard shortcuts for common operations
Touch-screen optimized interface
Accessibility

High contrast mode support
Adjustable font sizes
Screen reader compatibility
Keyboard-only navigation support
Multi-language support (English, Mandarin, Malay, Tamil)
5.4 Security Requirements
Authentication & Authorization

Strong password policy enforcement
Session timeout after 15 minutes of inactivity
Role-based access control
Audit logging for all sensitive operations
Two-factor authentication support (future)
Data Protection

Encryption at rest for sensitive data
Encryption in transit for all communications
PCI DSS compliance for payment data
PDPA compliance for personal data
Regular security updates
5.5 Scalability Requirements
Vertical Scalability

Support growth from 1 to 50 users
Handle inventory growth from 100 to 50,000 SKUs
Process growth from 10 to 1000 daily transactions
Maintain performance with 5 years of historical data
Horizontal Scalability

Multi-store support with centralized management
Database replication for high availability
Load balancing for multiple POS terminals
Cloud deployment readiness
6. Technology Stack
6.1 Core Technologies
Programming Language: Python 3.11+

Modern Python features for clean, maintainable code
Strong ecosystem for business applications
Excellent library support for all required functionalities
Cross-platform compatibility
UI Framework: PySide6 (Qt 6)

Modern, native-looking UI across platforms
Comprehensive widget library
Excellent performance for desktop applications
Strong community and commercial support
Built-in support for threading and async operations
Database: PostgreSQL 15+

Enterprise-grade reliability
ACID compliance
Advanced features (JSON support, full-text search)
Excellent performance at scale
Strong security features
6.2 Key Libraries and Frameworks
ORM: SQLAlchemy 2.0+

Powerful and flexible ORM
Database-agnostic design
Advanced query capabilities
Connection pooling and optimization
Migration support with Alembic
Async Support: asyncio + aiohttp

Native Python async/await support
Efficient I/O operations
Integration with Qt event loop
HTTP client for external APIs
Data Validation: Pydantic 2.0+

Type-safe data validation
Automatic documentation generation
JSON schema support
Integration with modern Python type hints
Testing: pytest + pytest-asyncio

Comprehensive testing framework
Async test support
Fixture system for test data
Coverage reporting integration
Additional Libraries:

python-barcode: Barcode generation
reportlab: PDF generation for receipts/reports
openpyxl: Excel report generation
python-dateutil: Date/time handling
forex-python: Currency exchange rates
cryptography: Data encryption
python-dotenv: Environment configuration
6.3 Development Tools
Version Control: Git

Distributed version control
Branch-based development workflow
Integration with CI/CD pipelines
IDE: PyCharm Professional / VS Code

Advanced Python development features
Integrated debugging
Database tools
Git integration
Code Quality:

black: Code formatting
flake8: Linting
mypy: Type checking
bandit: Security scanning
Documentation:

sphinx: API documentation
mkdocs: User documentation
plantuml: Architecture diagrams
7. System Architecture
7.1 Architectural Overview
The SG POS System follows a clean, layered architecture with strict separation of concerns:

┌─────────────────────────────────────────────────────────────┐
│                    Presentation Layer                        │
│                    (PySide6 UI Components)                   │
├─────────────────────────────────────────────────────────────┤
│                    Application Core                          │
│              (Dependency Injection Container)                │
├─────────────────────────────────────────────────────────────┤
│                  Business Logic Layer                        │
│            (Managers, Business Rules, DTOs)                  │
├─────────────────────────────────────────────────────────────┤
│                   Data Access Layer                          │
│          (Services, Repositories, Query Builders)            │
├─────────────────────────────────────────────────────────────┤
│                   Persistence Layer                          │
│           (SQLAlchemy Models, Database Schema)               │
├─────────────────────────────────────────────────────────────┤
│                      PostgreSQL                              │
└─────────────────────────────────────────────────────────────┘
7.2 Layer Descriptions
Presentation Layer

Contains all UI components built with PySide6
Implements Model-View-Controller pattern
Handles user input and display logic only
Communicates with business layer through ApplicationCore
Application Core

Central dependency injection container
Manages lifecycle of all components
Provides lazy initialization of managers
Maintains application-wide configuration
Business Logic Layer

Implements all business rules and workflows
Contains manager classes for each domain area
Uses DTOs for data transfer between layers
Implements Result pattern for error handling
Data Access Layer

Provides abstraction over database operations
Implements Repository pattern for data access
Contains query builders for complex queries
Handles database transactions
Persistence Layer

Defines SQLAlchemy ORM models
Manages database schema and migrations
Implements database constraints and triggers
Handles connection pooling
7.3 Asynchronous Architecture
The application implements a sophisticated asynchronous model:

# Main Thread (Qt Event Loop)
#     ↓
# UI Events → Schedule Task → Task Queue
#                                 ↓
# Async Thread (asyncio Event Loop)
#     ↓
# Execute Task → Database/API Calls
#     ↓
# Results → Qt Signal → Main Thread
#     ↓
# Update UI

This ensures:

UI remains responsive during long operations
Database operations don't block user interactions
External API calls are handled efficiently
Proper thread safety for UI updates
7.4 Security Architecture
Authentication Flow:

User Login → Password Hash Verification → Session Creation
    ↓                                           ↓
Role Assignment ← Database Query ← User Permissions
    ↓
Access Control Enforcement → Feature Access
Data Security Layers:

Application-level encryption for sensitive data
Database-level encryption at rest
TLS for all network communications
Audit logging for compliance
8. Database Schema Design
8.1 Core Schema Overview
The database schema is designed for flexibility, performance, and data integrity:

-- Company and Configuration
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50),
    gst_registration_number VARCHAR(50),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(20),
    country VARCHAR(2) DEFAULT 'SG',
    phone VARCHAR(50),
    email VARCHAR(255),
    base_currency VARCHAR(3) DEFAULT 'SGD',
    fiscal_year_start DATE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- User Management
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT chk_role CHECK (role IN ('admin', 'manager', 'cashier', 'accountant', 'inventory'))
);

-- Product Management
CREATE TABLE product_categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    parent_id UUID REFERENCES product_categories(id),
    description TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, name, parent_id)
);

CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    category_id UUID REFERENCES product_categories(id),
    sku VARCHAR(100) NOT NULL,
    barcode VARCHAR(100),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    unit_of_measure VARCHAR(50),
    cost_price DECIMAL(15, 4),
    selling_price DECIMAL(15, 4) NOT NULL,
    tax_rate DECIMAL(5, 2) DEFAULT 8.0,
    is_taxable BOOLEAN DEFAULT true,
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    reorder_level INTEGER,
    reorder_quantity INTEGER,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, sku),
    UNIQUE(company_id, barcode) WHERE barcode IS NOT NULL
);

-- Inventory Management
CREATE TABLE inventory_locations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    code VARCHAR(50) NOT NULL,
    address TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

CREATE TABLE inventory_stocks (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID REFERENCES products(id),
    location_id UUID REFERENCES inventory_locations(id),
    quantity_on_hand DECIMAL(15, 4) NOT NULL DEFAULT 0,
    quantity_reserved DECIMAL(15, 4) NOT NULL DEFAULT 0,
    quantity_available DECIMAL(15, 4) GENERATED ALWAYS AS (quantity_on_hand - quantity_reserved) STORED,
    last_stock_take_date DATE,
    last_stock_take_quantity DECIMAL(15, 4),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, location_id),
    CONSTRAINT chk_quantity CHECK (quantity_on_hand >= 0 AND quantity_reserved >= 0)
);

-- Customer Management
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    customer_code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(50),
    mobile VARCHAR(50),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(20),
    country VARCHAR(2) DEFAULT 'SG',
    tax_id VARCHAR(50),
    credit_limit DECIMAL(15, 2),
    payment_terms INTEGER DEFAULT 0,
    loyalty_points DECIMAL(15, 2) DEFAULT 0,
    loyalty_tier VARCHAR(50),
    date_of_birth DATE,
    anniversary_date DATE,
    notes TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, customer_code),
    UNIQUE(company_id, email) WHERE email IS NOT NULL
);

-- Sales Transactions
CREATE TABLE sales_orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    order_number VARCHAR(50) NOT NULL,
    order_date TIMESTAMP WITH TIME ZONE NOT NULL,
    customer_id UUID REFERENCES customers(id),
    user_id UUID REFERENCES users(id),
    location_id UUID REFERENCES inventory_locations(id),
    status VARCHAR(50) NOT NULL,
    subtotal DECIMAL(15, 2) NOT NULL,
    tax_amount DECIMAL(15, 2) NOT NULL,
    discount_amount DECIMAL(15, 2) DEFAULT 0,
    total_amount DECIMAL(15, 2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    exchange_rate DECIMAL(15, 6) DEFAULT 1,
    base_total_amount DECIMAL(15, 2) NOT NULL,
    payment_status VARCHAR(50) NOT NULL,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, order_number),
    CONSTRAINT chk_status CHECK (status IN ('draft', 'confirmed', 'completed', 'cancelled', 'refunded')),
    CONSTRAINT chk_payment_status CHECK (payment_status IN ('unpaid', 'partial', 'paid', 'refunded'))
);

CREATE TABLE sales_order_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sales_order_id UUID REFERENCES sales_orders(id) ON DELETE CASCADE,
    product_id UUID REFERENCES products(id),
    quantity DECIMAL(15, 4) NOT NULL,
    unit_price DECIMAL(15, 4) NOT NULL,
    discount_percentage DECIMAL(5, 2) DEFAULT 0,
    discount_amount DECIMAL(15, 2) DEFAULT 0,
    tax_rate DECIMAL(5, 2) NOT NULL,
    tax_amount DECIMAL(15, 2) NOT NULL,
    line_total DECIMAL(15, 2) NOT NULL,
    cost_price DECIMAL(15, 4),
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT chk_quantity CHECK (quantity > 0),
    CONSTRAINT chk_discount CHECK (discount_percentage >= 0 AND discount_percentage <= 100)
);

-- Payment Management
CREATE TABLE payment_methods (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    name VARCHAR(100) NOT NULL,
    code VARCHAR(50) NOT NULL,
    type VARCHAR(50) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    requires_reference BOOLEAN DEFAULT false,
    gl_account_id UUID,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code),
    CONSTRAINT chk_type CHECK (type IN ('cash', 'card', 'bank_transfer', 'mobile_payment', 'voucher', 'store_credit'))
);

CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    payment_number VARCHAR(50) NOT NULL,
    payment_date TIMESTAMP WITH TIME ZONE NOT NULL,
    sales_order_id UUID REFERENCES sales_orders(id),
    customer_id UUID REFERENCES customers(id),
    payment_method_id UUID REFERENCES payment_methods(id),
    amount DECIMAL(15, 2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    exchange_rate DECIMAL(15, 6) DEFAULT 1,
    base_amount DECIMAL(15, 2) NOT NULL,
    reference_number VARCHAR(100),
    notes TEXT,
    status VARCHAR(50) NOT NULL DEFAULT 'completed',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, payment_number),
    CONSTRAINT chk_status CHECK (status IN ('pending', 'completed', 'failed', 'refunded'))
);

-- Accounting Integration
CREATE TABLE chart_of_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    account_code VARCHAR(50) NOT NULL,
    account_name VARCHAR(255) NOT NULL,
    account_type VARCHAR(50) NOT NULL,
    parent_id UUID REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT true,
    is_system_account BOOLEAN DEFAULT false,
    description TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, account_code),
    CONSTRAINT chk_account_type CHECK (account_type IN ('asset', 'liability', 'equity', 'revenue', 'expense'))
);

CREATE TABLE journal_entries (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    journal_number VARCHAR(50) NOT NULL,
    journal_date DATE NOT NULL,
    description TEXT NOT NULL,
    reference_type VARCHAR(50),
    reference_id UUID,
    status VARCHAR(50) NOT NULL DEFAULT 'draft',
    posted_by UUID REFERENCES users(id),
    posted_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, journal_number),
    CONSTRAINT chk_status CHECK (status IN ('draft', 'posted', 'cancelled'))
);

CREATE TABLE journal_entry_lines (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    journal_entry_id UUID REFERENCES journal_entries(id) ON DELETE CASCADE,
    account_id UUID REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(15, 2) DEFAULT 0,
    credit_amount DECIMAL(15, 2) DEFAULT 0,
    description TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT chk_amounts CHECK (
        (debit_amount > 0 AND credit_amount = 0) OR 
        (debit_amount = 0 AND credit_amount > 0)
    )
);

-- GST Management
CREATE TABLE gst_rates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    rate_code VARCHAR(50) NOT NULL,
    rate_name VARCHAR(100) NOT NULL,
    rate_percentage DECIMAL(5, 2) NOT NULL,
    effective_from DATE NOT NULL,
    effective_to DATE,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, rate_code, effective_from),
    CONSTRAINT chk_dates CHECK (effective_to IS NULL OR effective_to > effective_from)
);

CREATE TABLE gst_submissions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    submission_type VARCHAR(50) NOT NULL,
    total_sales DECIMAL(15, 2) NOT NULL,
    total_purchases DECIMAL(15, 2) NOT NULL,
    output_tax DECIMAL(15, 2) NOT NULL,
    input_tax DECIMAL(15, 2) NOT NULL,
    net_gst DECIMAL(15, 2) NOT NULL,
    status VARCHAR(50) NOT NULL DEFAULT 'draft',
    submitted_date DATE,
    submitted_by UUID REFERENCES users(id),
    reference_number VARCHAR(100),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, period_start, period_end),
    CONSTRAINT chk_submission_type CHECK (submission_type IN ('gst_f5', 'gst_f7')),
    CONSTRAINT chk_status CHECK (status IN ('draft', 'submitted', 'accepted', 'rejected'))
);

-- Audit and Security
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(id),
    user_id UUID REFERENCES users(id),
    action VARCHAR(100) NOT NULL,
    entity_type VARCHAR(100) NOT NULL,
    entity_id UUID,
    old_values JSONB,
    new_values JSONB,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Indexes for Performance
CREATE INDEX idx_products_company_category ON products(company_id, category_id);
CREATE INDEX idx_products_barcode ON products(barcode) WHERE barcode IS NOT NULL;
CREATE INDEX idx_inventory_stocks_product_location ON inventory_stocks(product_id, location_id);
CREATE INDEX idx_sales_orders_company_date ON sales_orders(company_id, order_date);
CREATE INDEX idx_sales_orders_customer ON sales_orders(customer_id);
CREATE INDEX idx_sales_order_items_order ON sales_order_items(sales_order_id);
CREATE INDEX idx_payments_company_date ON payments(company_id, payment_date);
CREATE INDEX idx_journal_entries_company_date ON journal_entries(company_id, journal_date);
CREATE INDEX idx_audit_logs_company_date ON audit_logs(company_id, created_at);
CREATE INDEX idx_audit_logs_entity ON audit_logs(entity_type, entity_id);

-- Triggers for Updated Timestamps
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_companies_updated_at BEFORE UPDATE ON companies
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
CREATE TRIGGER update_users_updated_at BEFORE UPDATE ON users
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
CREATE TRIGGER update_products_updated_at BEFORE UPDATE ON products
    FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
-- (Additional triggers for other tables with updated_at columns)

8.2 Data Integrity Constraints
The schema implements comprehensive data integrity through:

Referential Integrity

Foreign key constraints ensure data consistency
Cascade deletes where appropriate (e.g., order items)
Restrict deletes for critical relationships
Check Constraints

Enum-like constraints for status fields
Business rule validation (e.g., quantity checks)
Date range validations
Unique Constraints

Prevent duplicate entries for business keys
Composite uniqueness for multi-tenant data
Conditional unique constraints where needed
Computed Columns

Automatic calculation of available inventory
Generated total amounts for consistency
9. Application Modules and Components
9.1 Module Architecture Diagram
┌─────────────────────────────────────────────────────────────┐
│                        Main Application                      │
│                          (main.py)                           │
├─────────────┬─────────────┬─────────────┬─────────────────┤
│   POS       │  Inventory  │  Customers  │    Reports      │
│   Module    │   Module    │   Module    │    Module       │
├─────────────┼─────────────┼─────────────┼─────────────────┤
│  Payment    │   Stock     │   CRM       │   Analytics     │
│  Manager    │   Manager   │  Manager    │   Manager       │
├─────────────┴─────────────┴─────────────┴─────────────────┤
│                    Business Logic Layer                      │
│              (Shared Services and Utilities)                 │
├─────────────────────────────────────────────────────────────┤
│                    Data Access Layer                         │
│                 (Repository Services)                        │
├─────────────────────────────────────────────────────────────┤
│                      Database Layer                          │
│                      (PostgreSQL)                            │
└─────────────────────────────────────────────────────────────┘
9.2 Core Modules
POS Module

Transaction processing engine
Payment handling
Receipt generation
Cash drawer management
Quick product lookup
Customer selection
Inventory Module

Stock level management
Purchase order processing
Stock transfers
Stock adjustments
Barcode management
Supplier management
Customer Module

Customer registration
Profile management
Purchase history
Loyalty program
Communication preferences
Credit management
Accounting Module

Chart of accounts
Journal entries
Financial reports
GST management
Multi-currency handling
Bank reconciliation
Reports Module

Sales analytics
Inventory reports
Financial statements
Customer insights
Performance dashboards
Custom report builder
Admin Module

User management
System configuration
Company settings
Security settings
Backup management
Audit logs
9.3 Component Interaction Flow
# Example: Sales Transaction Flow
1. UI Layer (POS Screen)
   └─> Scan/Select Products
   
2. POS Manager
   ├─> Validate Product Availability
   ├─> Calculate Pricing and Discounts
   └─> Apply Tax Calculations
   
3. Payment Manager
   ├─> Process Payment Methods
   ├─> Validate Payment Amounts
   └─> Generate Transaction Record
   
4. Inventory Service
   ├─> Update Stock Levels
   └─> Create Stock Movement Records
   
5. Accounting Manager
   ├─> Create Journal Entries
   └─> Update GL Accounts
   
6. Customer Service
   ├─> Update Purchase History
   └─> Award Loyalty Points
   
7. Receipt Service
   ├─> Generate Receipt Data
   └─> Print/Email Receipt

10. Codebase File Hierarchy
sg-pos/
├── app/
│   ├── __init__.py
│   ├── main.py                    # Application entry point
│   ├── config.py                  # Configuration management
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application.py         # ApplicationCore class
│   │   ├── constants.py           # Application constants
│   │   ├── exceptions.py          # Custom exceptions
│   │   ├── result.py              # Result pattern implementation
│   │   └── decorators.py          # Common decorators
│   │
│   ├── models/                    # SQLAlchemy ORM models
│   │   ├── __init__.py
│   │   ├── base.py                # Base model class
│   │   ├── company.py             # Company model
│   │   ├── user.py                # User model
│   │   ├── product.py             # Product models
│   │   ├── inventory.py           # Inventory models
│   │   ├── customer.py            # Customer model
│   │   ├── sales.py               # Sales models
│   │   ├── payment.py             # Payment models
│   │   ├── accounting.py          # Accounting models
│   │   └── audit.py               # Audit log model
│   │
│   ├── services/                  # Data access layer
│   │   ├── __init__.py
│   │   ├── base.py                # Base service class
│   │   ├── user_service.py        # User data access
│   │   ├── product_service.py     # Product data access
│   │   ├── inventory_service.py   # Inventory data access
│   │   ├── customer_service.py    # Customer data access
│   │   ├── sales_service.py       # Sales data access
│   │   ├── payment_service.py     # Payment data access
│   │   ├── accounting_service.py  # Accounting data access
│   │   └── report_service.py      # Reporting queries
│   │
│   ├── business_logic/            # Business logic layer
│   │   ├── __init__.py
│   │   ├── pos_manager.py         # POS operations
│   │   ├── inventory_manager.py   # Inventory management
│   │   ├── customer_manager.py    # Customer management
│   │   ├── payment_manager.py     # Payment processing
│   │   ├── gst_manager.py         # GST calculations
│   │   ├── accounting_manager.py  # Accounting operations
│   │   ├── report_manager.py      # Report generation
│   │   └── audit_manager.py       # Audit logging
│   │
│   ├── dto/                       # Data transfer objects
│   │   ├── __init__.py
│   │   ├── common.py              # Common DTOs
│   │   ├── product_dto.py         # Product DTOs
│   │   ├── sales_dto.py           # Sales DTOs
│   │   ├── payment_dto.py         # Payment DTOs
│   │   ├── customer_dto.py        # Customer DTOs
│   │   └── report_dto.py          # Report DTOs
│   │
│   ├── ui/                        # PySide6 UI layer
│   │   ├── __init__.py
│   │   ├── main_window.py         # Main application window
│   │   ├── styles/                # UI styles and themes
│   │   │   ├── __init__.py
│   │   │   ├── theme.py           # Theme definitions
│   │   │   └── styles.qss         # Qt stylesheets
│   │   │
│   │   ├── common/                # Common UI components
│   │   │   ├── __init__.py
│   │   │   ├── widgets.py         # Reusable widgets
│   │   │   ├── dialogs.py         # Common dialogs
│   │   │   ├── validators.py      # Input validators
│   │   │   └── formatters.py      # Display formatters
│   │   │
│   │   ├── pos/                   # POS UI module
│   │   │   ├── __init__.py
│   │   │   ├── pos_screen.py      # Main POS screen
│   │   │   ├── product_search.py  # Product search widget
│   │   │   ├── cart_widget.py     # Shopping cart widget
│   │   │   ├── payment_dialog.py  # Payment dialog
│   │   │   └── receipt_viewer.py  # Receipt preview
│   │   │
│   │   ├── inventory/             # Inventory UI module
│   │   │   ├── __init__.py
│   │   │   ├── inventory_main.py  # Inventory dashboard
│   │   │   ├── product_editor.py  # Product editor
│   │   │   ├── stock_adjust.py    # Stock adjustment
│   │   │   ├── purchase_order.py  # PO management
│   │   │   └── barcode_manager.py # Barcode tools
│   │   │
│   │   ├── customers/             # Customer UI module
│   │   │   ├── __init__.py
│   │   │   ├── customer_list.py   # Customer list view
│   │   │   ├── customer_editor.py # Customer editor
│   │   │   ├── loyalty_manager.py # Loyalty program
│   │   │   └── customer_history.py # Purchase history
│   │   │
│   │   ├── reports/               # Reports UI module
│   │   │   ├── __init__.py
│   │   │   ├── reports_main.py    # Reports dashboard
│   │   │   ├── sales_reports.py   # Sales reports
│   │   │   ├── inventory_reports.py # Inventory reports
│   │   │   ├── financial_reports.py # Financial reports
│   │   │   └── report_viewer.py   # Report viewer widget
│   │   │
│   │   ├── accounting/            # Accounting UI module
│   │   │   ├── __init__.py
│   │   │   ├── chart_accounts.py  # COA management
│   │   │   ├── journal_entry.py   # Journal entries
│   │   │   ├── gst_management.py  # GST tools
│   │   │   └── reconciliation.py  # Bank reconciliation
│   │   │
│   │   └── admin/                 # Admin UI module
│   │       ├── __init__.py
│   │       ├── admin_panel.py     # Admin dashboard
│   │       ├── user_management.py # User management
│   │       ├── company_settings.py # Company config
│   │       ├── backup_restore.py  # Backup tools
│   │       └── audit_viewer.py    # Audit log viewer
│   │
│   ├── utils/                     # Utility modules
│   │   ├── __init__.py
│   │   ├── async_utils.py         # Async helpers
│   │   ├── currency.py            # Currency utilities
│   │   ├── datetime_utils.py      # Date/time helpers
│   │   ├── encryption.py          # Encryption utilities
│   │   ├── validators.py          # Data validators
│   │   ├── formatters.py          # Data formatters
│   │   └── barcode_utils.py       # Barcode utilities
│   │
│   └── external/                  # External integrations
│       ├── __init__.py
│       ├── payment_gateway.py     # Payment gateway integration
│       ├── currency_api.py        # Currency rate API
│       ├── email_service.py       # Email service
│       └── sms_service.py         # SMS service
│
├── scripts/                       # Database and utility scripts
│   ├── __init__.py
│   ├── create_schema.sql          # Database schema
│   ├── seed_data.py               # Initial data seeding
│   ├── migrate.py                 # Database migrations
│   └── backup.py                  # Backup script
│
├── tests/                         # Test suite
│   ├── __init__.py
│   ├── conftest.py                # Test configuration
│   ├── unit/                      # Unit tests
│   │   ├── __init__.py
│   │   ├── test_models/
│   │   ├── test_services/
│   │   ├── test_managers/
│   │   
