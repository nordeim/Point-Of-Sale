Product Requirements Document: SG Point-of-Sale (POS) System
Version: 1.0
Date: June 12, 2025
Status: Draft

Table of Contents
Executive Summary
Background and Context
Product Vision
User Profiles and Personas
Functional Requirements
Non-Functional Requirements
Technology Stack
Architecture and System Design
Database Schema Design
Codebase Structure
Application Modules
Development Environment Setup
Production Environment Setup
Deployment and Maintenance
Implementation Plan
Risk Assessment and Mitigation
Appendices
Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail management needs of small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for the user interface and PostgreSQL for data management, the system provides a complete solution that addresses the unique regulatory and business requirements of the Singapore market.

The SG POS System aims to provide SMB retailers with enterprise-grade functionality in an affordable, user-friendly package. Key features include sales processing, inventory management, customer relationship management, employee management, multi-currency support, and comprehensive reporting that complies with Singapore's regulatory requirements, particularly regarding GST (Goods and Services Tax).

This PRD outlines the detailed requirements for the development of the SG POS System, including functional and technical specifications, architecture design, implementation strategy, and deployment considerations. It serves as the definitive reference for all stakeholders involved in the development process.

Background and Context
Market Analysis
The retail landscape in Singapore is characterized by a vibrant mix of traditional and modern businesses, with SMBs representing a significant portion of the market. These businesses face several challenges:

Regulatory Compliance: Singapore maintains strict regulatory requirements for financial record-keeping, GST reporting, and customer data protection under the Personal Data Protection Act (PDPA).

Technological Adoption: Many SMBs struggle with the transition from manual or basic digital systems to more comprehensive business management solutions.

Cost Constraints: Enterprise-grade POS systems often come with high licensing costs and hardware requirements that are prohibitive for smaller businesses.

Multi-Currency Needs: Singapore's position as a global hub necessitates handling transactions in multiple currencies, particularly for businesses catering to tourists and international customers.

Integration Requirements: Modern retailers need systems that can integrate with e-commerce platforms, accounting software, and other business tools.

Competitor Analysis
The POS market in Singapore includes several categories of competitors:

Global Enterprise Solutions: Systems like Oracle Retail, SAP Retail, and Microsoft Dynamics offer comprehensive features but at price points beyond most SMBs' reach.

Mid-tier International Solutions: Products like Lightspeed, Shopify POS, and Square provide good functionality but often lack Singapore-specific features (e.g., GST compliance, local payment methods).

Local Singaporean Solutions: Systems specifically developed for the Singapore market, such as Qashier and Epos, address local needs but may lack the technical sophistication or scalability of international offerings.

Legacy Systems: Many businesses still operate on outdated systems with limited functionality or rely on basic cash registers and manual record-keeping.

Regulatory Environment
The SG POS System must comply with several key regulatory considerations:

GST Compliance: Singapore's 8% (subject to change) Goods and Services Tax must be correctly calculated, collected, and reported according to Inland Revenue Authority of Singapore (IRAS) requirements.

PDPA Compliance: The system must handle customer data in accordance with Singapore's Personal Data Protection Act, including consent management, data security, and retention policies.

MAS Electronic Payments Guidelines: For electronic payment processing, compliance with Monetary Authority of Singapore guidelines is essential.

Accounting Standards: The system should facilitate compliance with Singapore Financial Reporting Standards (SFRS).

Product Vision
Vision Statement
To be the definitive point-of-sale solution for Singapore's SMB retailers, combining enterprise-grade functionality with local market knowledge, regulatory compliance, and exceptional usability at an accessible price point.

Core Principles
Compliance by Design: Regulatory requirements are addressed as fundamental design elements, not afterthoughts.

Usability First: The interface prioritizes ease of use without compromising on functionality, minimizing training requirements.

Scalable Architecture: The system grows with the business, from single-register operations to multi-location enterprises.

Data-Driven Insights: Beyond transaction processing, the system provides actionable business intelligence.

Technological Independence: Cross-platform design ensures businesses aren't locked into specific hardware ecosystems.

Comprehensive Integration: The system works seamlessly with other business tools through standardized APIs.

Success Metrics
Market Adoption: Target acquisition of 500 SMB customers within the first year of release.

User Satisfaction: Achieve and maintain a user satisfaction rating of 4.5/5 or higher.

Feature Utilization: 80% of customers utilizing advanced features beyond basic transaction processing.

Support Efficiency: 90% of support inquiries resolved within 24 hours.

System Reliability: Maintain 99.9% uptime for critical functions.

User Profiles and Personas
Primary User Types
Cashier/Sales Associate

Profile: Front-line staff with varying levels of technical proficiency
Key Needs: Simple, intuitive interface; quick transaction processing; minimal training
Pain Points: System complexity; slow checkout process; difficulty handling special cases
Usage Pattern: Continuous use throughout shift; high volume of repetitive actions
Store Manager

Profile: Responsible for day-to-day operations with moderate technical skills
Key Needs: Staff management; inventory oversight; daily reporting; issue resolution
Pain Points: Limited visibility into operations; manual reconciliation processes; staff training
Usage Pattern: Intermittent use throughout day; deeper engagement with management functions
Business Owner

Profile: Ultimate decision-maker with variable technical background
Key Needs: Business performance insights; cost control; compliance assurance
Pain Points: Lack of actionable data; regulatory compliance concerns; system cost
Usage Pattern: Periodic use focusing on reports and strategic functions
Inventory Manager

Profile: Specialized role in larger businesses with moderate technical expertise
Key Needs: Stock level management; supplier coordination; product catalog maintenance
Pain Points: Inaccurate inventory counts; inefficient ordering processes; data entry burden
Usage Pattern: Regular use focusing on inventory-specific functions
Accountant/Bookkeeper

Profile: Financial professional with strong domain knowledge
Key Needs: Financial data extraction; GST reporting; audit support
Pain Points: Data inconsistencies; manual reconciliation; compliance documentation
Usage Pattern: Periodic intensive use, particularly at month/quarter end
Detailed Personas
Persona 1: Sarah Chen - Cashier
Demographics: 22 years old, part-time university student
Technical Proficiency: Moderate, comfortable with smartphones and basic computer applications
Goals:
Process transactions quickly and accurately
Minimize customer wait times
Avoid making errors that require manager intervention
Frustrations:
Complex interfaces that require extensive training
Systems that crash or freeze during busy periods
Difficulty handling special cases like returns or split payments
Scenario: During the weekend rush, Sarah needs to quickly process a transaction with multiple payment methods, apply a loyalty discount, and handle a partial return from a previous purchase.
Persona 2: Michael Tan - Store Owner
Demographics: 45 years old, owner of a growing specialty retail store with two locations
Technical Proficiency: Basic, relies on staff for technical tasks
Goals:
Maintain accurate financial records for tax compliance
Understand business performance across multiple locations
Minimize operational costs while maximizing customer satisfaction
Frustrations:
Lack of clear insights into which products are performing well
Difficulty ensuring consistent processes across locations
Time spent on administrative tasks rather than business growth
Scenario: At the end of the quarter, Michael needs to review the performance of both store locations, identify top-selling products, evaluate staff productivity, and prepare data for GST reporting.
Functional Requirements
Core POS Features
Sales Processing
Transaction Management

Create, modify, and complete sales transactions
Support for transaction holds and recalls
Void and return processing with appropriate authorization
Split tendering across multiple payment methods
Discounting at item and transaction level (percentage and fixed amount)
Tax calculation with appropriate GST rules
Receipt generation with all required legal information
Email/SMS receipt options
Product Handling

Barcode scanning with support for multiple barcode formats
Manual product lookup by code, name, or category
Product image display for visual confirmation
Variant selection (size, color, etc.)
Bundle and kit processing
Serial number tracking for applicable items
Age verification prompts for restricted products
Customer Interaction

Customer identification via loyalty card, phone number, or name
Display of customer purchase history and preferences
Application of customer-specific pricing or discounts
Loyalty point accumulation and redemption
Store credit management
User Interface Requirements

Touchscreen-optimized layout with large, clear buttons
Keyboard shortcut support for high-speed operation
Customizable quick-access product buttons
Clear visual indicators for transaction status
Dark/light mode support for different environments
Accessibility features for users with disabilities
Inventory Management
Product Catalog

Comprehensive product database with hierarchical categories
Support for product variants (size, color, etc.)
Multiple pricing levels (regular, sale, wholesale, etc.)
Product images and detailed descriptions
Custom attribute fields for specialty information
Barcode generation and printing
Bulk import/export functionality
Stock Control

Real-time inventory tracking
Multi-location inventory management
Minimum stock level alerts
Automated purchase order suggestions
Stock transfer between locations
Stock taking and inventory adjustment tools
Inventory valuation (FIFO, LIFO, average cost methods)
Serialized inventory tracking
Supplier Management

Supplier database with contact information
Preferred supplier designation per product
Purchase order creation and tracking
Goods receipt processing
Supplier performance metrics
Order history and reordering patterns
Customer Management
Customer Database

Comprehensive customer profiles
Contact information with validation
Purchase history and preferences
Notes and custom fields
Customer categorization/tagging
PDPA consent tracking
Loyalty Program

Points accumulation based on purchase value
Configurable points-to-value conversion
Redemption mechanisms at checkout
Member tier management with different benefits
Special promotions for loyalty members
Expiration date management for points
Birthday rewards and other automated benefits
Marketing Support

Customer segmentation for targeted marketing
Export capabilities for email/SMS campaigns
Purchase pattern analysis
Abandoned basket tracking (if integrated with e-commerce)
Promotion effectiveness reporting
Employee Management
User Access Control

Role-based access control system
Granular permission settings
Biometric or smart card authentication options
Audit trails for all system actions
Automatic session timeouts for security
Staff Performance

Sales performance tracking by employee
Commission calculation based on configurable rules
Productivity metrics and targets
Time and attendance tracking
Training mode for new employees
Shift Management

Shift scheduling and timesheet functionality
Cash drawer assignment and accountability
Shift handover procedures
Break tracking
Labor cost reporting against sales
Reporting and Analytics
Sales Reports

Real-time sales dashboard
Hourly, daily, weekly, monthly, and custom period reports
Sales by product, category, supplier, and department
Sales by payment method
Discount and promotion analysis
Tax (GST) collection reports
Comparative analysis (year-over-year, period-over-period)
Inventory Reports

Current stock levels
Inventory valuation
Slow-moving item identification
Shrinkage and loss reporting
Stock turnover analysis
Out-of-stock frequency
ABC analysis (inventory categorization)
Customer Reports

Customer purchase frequency
Average transaction value
Loyalty program participation
Customer acquisition and retention metrics
Customer lifetime value calculations
Top customer identification
Financial Reports

Profit and loss statements
Cost of goods sold
Margin analysis
Cash flow reports
GST reporting for IRAS compliance
End-of-day reconciliation
Custom Reporting

Report builder with drag-and-drop interface
Saved report templates
Scheduled report generation
Export to multiple formats (PDF, Excel, CSV)
Email distribution options
Payment Processing
Cash Management

Cash drawer control and reconciliation
Float and petty cash management
Denomination tracking for cash counts
Over/short reporting
Safe drop procedures
Electronic Payments

Credit/debit card processing
Integration with Singapore payment gateways
Support for NETS, PayNow, and PayLah!
QR code payment support (SGQR)
Contactless payment methods
Mobile wallet compatibility
Alternative Payments

Gift card issuance and redemption
Store credit management
Voucher and coupon processing
Invoice creation for corporate clients
Installment payment plans
Multi-Currency Support

Support for all major currencies
Real-time or manual exchange rate management
Currency conversion at checkout
Multi-currency reporting
Base currency configuration (SGD default)
GST Compliance
Tax Calculation

Automatic GST calculation based on current rates
Support for GST-exempt items
Handling of zero-rated supplies
Tourist refund scheme support
GST inclusive/exclusive pricing options
GST Reporting

GST summary reports for filing periods
Detailed GST transaction logs
IRAS-compliant report formats
Digital export for e-filing
GST audit trail for compliance verification
Invoice Requirements

IRAS-compliant tax invoice generation
GST registration number display
Proper tax breakdown on receipts
Electronic invoice delivery options
Integration Capabilities
Accounting Integration

Bidirectional sync with popular accounting packages
Automated journal entry creation
Chart of accounts mapping
Period close procedures
Audit trail for financial transactions
E-commerce Integration

Product catalog synchronization
Inventory level sharing across channels
Order import from online platforms
Customer data unification
Pricing consistency management
External Systems

Open API for custom integrations
Webhook support for real-time event handling
Bulk data import/export tools
Integration with shipping and logistics providers
Support for external hardware (scales, RFID readers, etc.)
Non-Functional Requirements
Performance Requirements
Response Time

Transaction processing: < 1 second
Product lookup: < 0.5 seconds
Report generation: < 5 seconds for standard reports
Database queries: 95% complete in < 1 second
UI rendering: < 100ms for interface updates
Throughput

Support for 10,000+ SKUs
Handling of 1,000+ daily transactions
Concurrent user support: up to 20 simultaneous users
Database capacity: 5+ years of transaction history without performance degradation
Resource Utilization

Memory usage: < 500MB in normal operation
CPU utilization: < 25% during regular operation, < 75% during peak processing
Storage requirements: < 100MB for application, scalable database storage
Network bandwidth: < 1Mbps per active user session
Security Requirements
Authentication and Authorization

Multi-factor authentication support
Role-based access control
Password policy enforcement
Automatic session timeout
Failed login attempt limiting
Data Protection

Encryption of sensitive data at rest
Secure transmission using TLS 1.3
Payment card data handling compliant with PCI-DSS
Personal data protection in accordance with PDPA
Secure backup encryption
Audit and Compliance

Comprehensive audit logging
User action tracking
System change history
Immutable transaction records
Compliance reporting tools
Reliability Requirements
Availability

99.9% uptime during business hours
Scheduled maintenance windows with minimal disruption
Graceful degradation during component failures
Fault Tolerance

Automatic recovery from common error conditions
Transaction integrity preservation during failures
Local operation capability during network outages
Data synchronization upon reconnection
Backup and Recovery

Automated daily backups
Point-in-time recovery capabilities
15-minute recovery time objective (RTO)
1-hour recovery point objective (RPO)
Backup verification and testing procedures
Usability Requirements
User Interface

Consistent visual design across all modules
Adherence to platform UI guidelines
Support for internationalization (English, Chinese, Malay, Tamil)
Responsive design for different screen sizes
Touch-friendly interfaces for tablet use
Accessibility

Compliance with WCAG 2.1 AA standards
Screen reader compatibility
Keyboard navigation support
Color contrast considerations
Font size adjustability
Learnability

Intuitive navigation structure
Context-sensitive help system
Interactive tutorials and tooltips
Consistent terminology and iconography
Progressive disclosure of advanced features
Maintainability Requirements
Code Quality

Adherence to PEP 8 style guide for Python
Comprehensive automated test coverage (>80%)
Code documentation standards
Modular architecture with clear separation of concerns
Static code analysis integration
Extensibility

Plugin architecture for custom extensions
Clear API documentation
Feature flag system for gradual rollout
Configuration-driven behavior
Customization capabilities without core code changes
Supportability

Detailed logging with configurable levels
Remote diagnostics capabilities
Automated error reporting
System health monitoring
Performance profiling tools
Technology Stack
Frontend Technology
PySide6 (Qt for Python)

PySide6 has been selected as the primary UI framework for the following reasons:

Cross-Platform Compatibility: PySide6 provides native-looking interfaces on Windows, macOS, and Linux, allowing the application to run consistently across different operating systems common in Singapore's business environment.

Rich Widget Set: PySide6 offers a comprehensive collection of UI components, including tables, trees, charts, and forms that are essential for a complex business application.

Performance: As a C++ based framework with Python bindings, PySide6 delivers superior performance compared to pure Python UI frameworks, which is critical for a responsive POS system.

Customization Capabilities: The framework allows for extensive styling and theming to create a modern, distinctive interface while maintaining platform-appropriate behavior.

Integration with Qt Designer: The visual design tool simplifies UI development and iteration, speeding up the development process.

Mature Technology: Backed by The Qt Company, PySide6 is a mature, well-documented technology with long-term support guarantees.

Additional Frontend Technologies:

Qt Charts: For visual data representation in reports and dashboards
Qt WebEngine: For displaying web content and potential embedded browser capabilities
Qt Quick/QML: For advanced animated interfaces where appropriate
OpenGL Integration: For hardware-accelerated graphics where needed
Backend Technology
Python

Python has been chosen as the core programming language for the following reasons:

Developer Productivity: Python's clear syntax and extensive standard library enable rapid development and maintenance.

Ecosystem: Rich ecosystem of libraries for data processing, business logic, and integration with external systems.

Cross-Platform Support: Python runs consistently across Windows, macOS, and Linux environments.

Scalability: Modern Python implementations provide good performance for business applications, with the ability to optimize critical sections as needed.

Community and Support: Large community and commercial support options ensure long-term viability.

Key Python Libraries:

SQLAlchemy: Object-relational mapper for database interactions
Pydantic: Data validation and settings management
asyncio: For asynchronous programming model
pytest: For comprehensive testing
NumPy/Pandas: For data analysis and reporting functions
Requests/aiohttp: For API integrations
python-barcode/pyzbar: For barcode generation and scanning
ReportLab/WeasyPrint: For PDF generation
PyInstaller: For application packaging and distribution
Database Technology
PostgreSQL

PostgreSQL has been selected as the database system for the following reasons:

Data Integrity: Strong transactional support and ACID compliance to ensure business data reliability.

Advanced Features: Rich feature set including JSON support, full-text search, and complex querying capabilities.

Scalability: Handles large datasets efficiently with good performance optimization options.

Extensibility: Custom data types, functions, and procedural languages allow for database-level business logic when appropriate.

Security: Robust security features including row-level security, SSL support, and strong authentication options.

Cost-Effectiveness: Open-source licensing reduces total cost of ownership.

Database Design Considerations:

Connection Pooling: Using pgBouncer for efficient connection management
Partitioning: Table partitioning strategy for historical transaction data
Indexing Strategy: Carefully designed indexes for performance optimization
Backup System: Point-in-time recovery with WAL archiving
Replication: Optional standby replication for larger deployments
Supporting Technologies
Redis: For caching, session management, and pub/sub messaging
Docker: For development environment consistency and production deployment
Git: For version control with branch strategy for feature development
GitHub Actions/Jenkins: For CI/CD pipeline
Sentry: For error tracking and performance monitoring
Prometheus/Grafana: For system metrics and monitoring
OpenAPI: For API documentation
Alembic: For database migrations
Black/Flake8/mypy: For code quality enforcement
Sphinx: For documentation generation
Architecture and System Design
System Architecture Overview
The SG POS System follows a layered architecture pattern with clear separation of concerns. The architecture consists of the following layers:

Presentation Layer

Responsible for all user interface components
Implements the Model-View-Presenter (MVP) pattern
Handles user input and display rendering
Communicates with the business logic layer via well-defined interfaces
Business Logic Layer

Implements all business rules and workflows
Coordinates operations across different modules
Validates data and ensures business rule compliance
Processes commands from the presentation layer
Returns results and notifications to the presentation layer
Data Access Layer

Abstracts database operations from business logic
Implements the repository pattern for data operations
Handles query construction and execution
Manages transaction boundaries
Performs data mapping between domain models and persistence models
Infrastructure Layer

Provides cross-cutting concerns such as logging, caching, and configuration
Implements technical services like printing, device communication, and integrations
Manages communication with external systems
Handles security, authentication, and authorization
Architectural Patterns
Dependency Injection

All components receive their dependencies through constructor injection
Central application core manages object creation and lifetime
Improves testability and decoupling
Repository Pattern

Data access abstractions provide a collection-like interface for domain entities
Centralizes data access logic and query operations
Facilitates unit testing through repository mocking
Unit of Work

Coordinates transactions and ensures consistency across multiple repositories
Provides atomic operations for complex business processes
CQRS (Command Query Responsibility Segregation)

Separates read and write operations for improved performance and scalability
Read models optimized for specific UI needs
Write operations validated and processed through command handlers
Event-Driven Architecture

Business events published for loose coupling between components
Enables extension points for custom behaviors
Facilitates audit logging and cross-cutting concerns
Concurrency Model
Asynchronous Processing

Non-blocking I/O for database and network operations
Task-based concurrency model using Python's asyncio
Background processing for time-consuming operations
Progress reporting to UI for long-running tasks
Thread Management

UI thread dedicated to interface responsiveness
Worker thread pool for background processing
Thread synchronization using appropriate mechanisms
Deadlock prevention strategies
Error Handling Strategy
Exception Hierarchy

Custom exception types for different error categories
Business exceptions vs. technical exceptions
User-friendly error messages mapped to exception types
Result Pattern

Operations return result objects rather than throwing exceptions for expected error conditions
Results contain success/failure status and relevant data
Consistent error handling across the application
Graceful Degradation

Fallback mechanisms for non-critical component failures
Offline operation capabilities when network connectivity is lost
Clear user notification for degraded operation modes
Data Flow Architecture
Command Flow

UI actions create command objects
Commands validated by validators
Command handlers execute business logic
Results returned to UI for presentation
Events published for side effects
Query Flow

UI requests data via query objects
Query handlers retrieve and shape data
Read models returned to UI for presentation
Caching applied at appropriate levels
Integration Flow

Adapters translate between external systems and internal models
Message queues for asynchronous communication
Retry policies for transient failures
Circuit breakers for external system protection
Database Schema Design
Entity Relationship Diagram
The database schema is organized into several logical groups:

Core Retail Operations

Products, categories, pricing
Inventory, stock movements
Sales transactions, line items
Payments, refunds
Customer Management

Customer profiles
Loyalty program
Marketing preferences
Employee and Security

Users, roles, permissions
Audit logs, session tracking
Accounting and Finance

Chart of accounts
Journal entries
Tax configurations
System Configuration

Store information
Application settings
Integration configurations
Detailed Table Specifications
Core Tables
products

id                  UUID PRIMARY KEY
sku                 VARCHAR(50) UNIQUE NOT NULL
barcode             VARCHAR(100) UNIQUE
name                VARCHAR(255) NOT NULL
description         TEXT
category_id         UUID REFERENCES categories(id)
supplier_id         UUID REFERENCES suppliers(id)
cost_price          DECIMAL(19,4) NOT NULL
selling_price       DECIMAL(19,4) NOT NULL
tax_rate_id         UUID REFERENCES tax_rates(id)
is_active           BOOLEAN DEFAULT TRUE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
deleted_at          TIMESTAMP WITH TIME ZONE
product_attributes

id                  UUID PRIMARY KEY
product_id          UUID REFERENCES products(id)
attribute_name      VARCHAR(100) NOT NULL
attribute_value     VARCHAR(255)
display_order       INTEGER
is_variant          BOOLEAN DEFAULT FALSE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
product_variants

id                  UUID PRIMARY KEY
product_id          UUID REFERENCES products(id)
sku                 VARCHAR(50) UNIQUE NOT NULL
barcode             VARCHAR(100) UNIQUE
attributes_json     JSONB NOT NULL
additional_cost     DECIMAL(19,4) DEFAULT 0
additional_price    DECIMAL(19,4) DEFAULT 0
stock_quantity      INTEGER DEFAULT 0
is_active           BOOLEAN DEFAULT TRUE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
categories

id                  UUID PRIMARY KEY
name                VARCHAR(100) NOT NULL
parent_id           UUID REFERENCES categories(id)
description         TEXT
image_path          VARCHAR(255)
display_order       INTEGER
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
inventory

id                  UUID PRIMARY KEY
product_id          UUID REFERENCES products(id)
variant_id          UUID REFERENCES product_variants(id)
location_id         UUID REFERENCES locations(id)
quantity            INTEGER NOT NULL
min_stock_level     INTEGER DEFAULT 0
max_stock_level     INTEGER
reorder_quantity    INTEGER
last_counted_at     TIMESTAMP WITH TIME ZONE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
inventory_transactions

id                  UUID PRIMARY KEY
inventory_id        UUID REFERENCES inventory(id)
transaction_type    VARCHAR(50) NOT NULL
quantity            INTEGER NOT NULL
reference_id        UUID
reference_type      VARCHAR(50)
notes               TEXT
performed_by        UUID REFERENCES users(id)
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
sales_transactions

id                  UUID PRIMARY KEY
transaction_number  VARCHAR(50) UNIQUE NOT NULL
store_id            UUID REFERENCES stores(id)
register_id         UUID REFERENCES registers(id)
user_id             UUID REFERENCES users(id)
customer_id         UUID REFERENCES customers(id)
transaction_date    TIMESTAMP WITH TIME ZONE NOT NULL
subtotal            DECIMAL(19,4) NOT NULL
tax_total           DECIMAL(19,4) NOT NULL
discount_total      DECIMAL(19,4) DEFAULT 0
grand_total         DECIMAL(19,4) NOT NULL
rounding_adjustment DECIMAL(19,4) DEFAULT 0
status              VARCHAR(20) NOT NULL
notes               TEXT
invoice_number      VARCHAR(50)
currency_code       CHAR(3) DEFAULT 'SGD'
exchange_rate       DECIMAL(19,6) DEFAULT 1
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
sales_line_items

id                  UUID PRIMARY KEY
transaction_id      UUID REFERENCES sales_transactions(id)
product_id          UUID REFERENCES products(id)
variant_id          UUID REFERENCES product_variants(id)
quantity            DECIMAL(19,4) NOT NULL
unit_price          DECIMAL(19,4) NOT NULL
line_discount       DECIMAL(19,4) DEFAULT 0
tax_rate            DECIMAL(9,4) NOT NULL
tax_amount          DECIMAL(19,4) NOT NULL
subtotal            DECIMAL(19,4) NOT NULL
total               DECIMAL(19,4) NOT NULL
cost_price          DECIMAL(19,4) NOT NULL
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
payments

id                  UUID PRIMARY KEY
transaction_id      UUID REFERENCES sales_transactions(id)
payment_method      VARCHAR(50) NOT NULL
amount              DECIMAL(19,4) NOT NULL
reference_number    VARCHAR(100)
status              VARCHAR(20) NOT NULL
payment_date        TIMESTAMP WITH TIME ZONE NOT NULL
currency_code       CHAR(3) DEFAULT 'SGD'
exchange_rate       DECIMAL(19,6) DEFAULT 1
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
Customer Management Tables
customers

id                  UUID PRIMARY KEY
customer_number     VARCHAR(50) UNIQUE
first_name          VARCHAR(100) NOT NULL
last_name           VARCHAR(100)
email               VARCHAR(255)
phone               VARCHAR(20)
address_line1       VARCHAR(255)
address_line2       VARCHAR(255)
city                VARCHAR(100)
postal_code         VARCHAR(20)
country             VARCHAR(100) DEFAULT 'Singapore'
tax_id              VARCHAR(50)
notes               TEXT
loyalty_points      INTEGER DEFAULT 0
customer_group_id   UUID REFERENCES customer_groups(id)
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
customer_groups

id                  UUID PRIMARY KEY
name                VARCHAR(100) NOT NULL
discount_percent    DECIMAL(5,2) DEFAULT 0
description         TEXT
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
loyalty_transactions

id                  UUID PRIMARY KEY
customer_id         UUID REFERENCES customers(id)
transaction_id      UUID REFERENCES sales_transactions(id)
points              INTEGER NOT NULL
transaction_type    VARCHAR(20) NOT NULL
expiry_date         DATE
notes               TEXT
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
Employee and Security Tables
users

id                  UUID PRIMARY KEY
username            VARCHAR(50) UNIQUE NOT NULL
password_hash       VARCHAR(255) NOT NULL
first_name          VARCHAR(100) NOT NULL
last_name           VARCHAR(100) NOT NULL
email               VARCHAR(255) UNIQUE NOT NULL
phone               VARCHAR(20)
role_id             UUID REFERENCES roles(id)
is_active           BOOLEAN DEFAULT TRUE
last_login          TIMESTAMP WITH TIME ZONE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
roles

id                  UUID PRIMARY KEY
name                VARCHAR(50) UNIQUE NOT NULL
description         TEXT
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
permissions

id                  UUID PRIMARY KEY
name                VARCHAR(100) UNIQUE NOT NULL
description         TEXT
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
role_permissions

role_id             UUID REFERENCES roles(id)
permission_id       UUID REFERENCES permissions(id)
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
PRIMARY KEY (role_id, permission_id)
audit_logs

id                  UUID PRIMARY KEY
user_id             UUID REFERENCES users(id)
action              VARCHAR(100) NOT NULL
entity_type         VARCHAR(50)
entity_id           UUID
details             JSONB
ip_address          VARCHAR(45)
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
Accounting and Finance Tables
tax_rates

id                  UUID PRIMARY KEY
name                VARCHAR(100) NOT NULL
rate                DECIMAL(5,2) NOT NULL
is_default          BOOLEAN DEFAULT FALSE
tax_code            VARCHAR(20)
is_compound         BOOLEAN DEFAULT FALSE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
chart_of_accounts

id                  UUID PRIMARY KEY
account_code        VARCHAR(20) UNIQUE NOT NULL
account_name        VARCHAR(100) NOT NULL
account_type        VARCHAR(50) NOT NULL
parent_id           UUID REFERENCES chart_of_accounts(id)
description         TEXT
is_active           BOOLEAN DEFAULT TRUE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
journal_entries

id                  UUID PRIMARY KEY
entry_number        VARCHAR(50) UNIQUE NOT NULL
entry_date          DATE NOT NULL
reference_id        UUID
reference_type      VARCHAR(50)
description         TEXT
is_posted           BOOLEAN DEFAULT FALSE
posted_by           UUID REFERENCES users(id)
posted_at           TIMESTAMP WITH TIME ZONE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
journal_lines

id                  UUID PRIMARY KEY
journal_entry_id    UUID REFERENCES journal_entries(id)
account_id          UUID REFERENCES chart_of_accounts(id)
debit_amount        DECIMAL(19,4) DEFAULT 0
credit_amount       DECIMAL(19,4) DEFAULT 0
description         TEXT
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
System Configuration Tables
stores

id                  UUID PRIMARY KEY
name                VARCHAR(100) NOT NULL
code                VARCHAR(20) UNIQUE NOT NULL
address_line1       VARCHAR(255) NOT NULL
address_line2       VARCHAR(255)
city                VARCHAR(100) DEFAULT 'Singapore'
postal_code         VARCHAR(20) NOT NULL
country             VARCHAR(100) DEFAULT 'Singapore'
phone               VARCHAR(20)
email               VARCHAR(255)
tax_registration    VARCHAR(50)
is_active           BOOLEAN DEFAULT TRUE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
registers

id                  UUID PRIMARY KEY
store_id            UUID REFERENCES stores(id)
name                VARCHAR(100) NOT NULL
code                VARCHAR(20) NOT NULL
description         TEXT
is_active           BOOLEAN DEFAULT TRUE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
UNIQUE (store_id, code)
app_settings

id                  UUID PRIMARY KEY
setting_key         VARCHAR(100) UNIQUE NOT NULL
setting_value       TEXT
setting_group       VARCHAR(50)
description         TEXT
is_system           BOOLEAN DEFAULT FALSE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
currencies

code                CHAR(3) PRIMARY KEY
name                VARCHAR(100) NOT NULL
symbol              VARCHAR(10) NOT NULL
decimal_places      INTEGER DEFAULT 2
exchange_rate       DECIMAL(19,6) DEFAULT 1
is_active           BOOLEAN DEFAULT TRUE
last_updated        TIMESTAMP WITH TIME ZONE
created_at          TIMESTAMP WITH TIME ZONE NOT NULL
updated_at          TIMESTAMP WITH TIME ZONE NOT NULL
Database Indexes
-- Product lookup optimization
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_barcode ON products(barcode);
CREATE INDEX idx_products_category_id ON products(category_id);

-- Inventory lookup optimization
CREATE INDEX idx_inventory_product_id ON inventory(product_id);
CREATE INDEX idx_inventory_location_id ON inventory(location_id);

-- Transaction lookup optimization
CREATE INDEX idx_sales_transactions_transaction_number ON sales_transactions(transaction_number);
CREATE INDEX idx_sales_transactions_transaction_date ON sales_transactions(transaction_date);
CREATE INDEX idx_sales_transactions_customer_id ON sales_transactions(customer_id);
CREATE INDEX idx_sales_transactions_user_id ON sales_transactions(user_id);

-- Line item optimization
CREATE INDEX idx_sales_line_items_transaction_id ON sales_line_items(transaction_id);
CREATE INDEX idx_sales_line_items_product_id ON sales_line_items(product_id);

-- Payment lookup optimization
CREATE INDEX idx_payments_transaction_id ON payments(transaction_id);
CREATE INDEX idx_payments_payment_method ON payments(payment_method);

-- Customer lookup optimization
CREATE INDEX idx_customers_email ON customers(email);
CREATE INDEX idx_customers_phone ON customers(phone);
CREATE INDEX idx_customers_customer_number ON customers(customer_number);

-- User lookup optimization
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role_id ON users(role_id);

-- Audit log optimization
CREATE INDEX idx_audit_logs_user_id ON audit_logs(user_id);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);
CREATE INDEX idx_audit_logs_entity_id ON audit_logs(entity_id);

Database Triggers
-- Trigger to maintain updated_at timestamp
CREATE OR REPLACE FUNCTION update_modified_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = NOW();
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Apply to all tables with updated_at column
CREATE TRIGGER update_products_modtime
    BEFORE UPDATE ON products
    FOR EACH ROW
    EXECUTE PROCEDURE update_modified_column();

-- Additional triggers for inventory management
CREATE OR REPLACE FUNCTION update_inventory_on_sale()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE inventory
    SET quantity = quantity - NEW.quantity
    WHERE product_id = NEW.product_id
    AND (NEW.variant_id IS NULL OR variant_id = NEW.variant_id)
    AND location_id = (SELECT register_id FROM sales_transactions WHERE id = NEW.transaction_id);
    
    INSERT INTO inventory_transactions (
        id, inventory_id, transaction_type, quantity, reference_id, reference_type, created_at
    )
    VALUES (
        gen_random_uuid(),
        (SELECT id FROM inventory WHERE product_id = NEW.product_id AND location_id = (SELECT register_id FROM sales_transactions WHERE id = NEW.transaction_id)),
        'SALE',
        -NEW.quantity,
        NEW.transaction_id,
        'SALES_LINE_ITEM',
        NOW()
    );
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_inventory_after_sale
    AFTER INSERT ON sales_line_items
    FOR EACH ROW
    EXECUTE PROCEDURE update_inventory_on_sale();

Codebase Structure
The SG POS System follows a modular, layered architecture with clear separation of concerns. The codebase is organized as follows:

sg_pos/
├── app/                       # Application source code
│   ├── __init__.py           # Package initialization
│   ├── main.py               # Application entry point
│   ├── config.py             # Configuration management
│   ├── application_core.py   # Core application services and DI container
│   ├── business_logic/       # Business logic layer
│   │   ├── __init__.py
│   │   ├── managers/         # Business logic managers
│   │   │   ├── __init__.py
│   │   │   ├── sales_manager.py
│   │   │   ├── inventory_manager.py
│   │   │   ├── customer_manager.py
│   │   │   ├── payment_manager.py
│   │   │   ├── user_manager.py
│   │   │   └── ...
│   │   ├── validators/       # Business rule validators
│   │   │   ├── __init__.py
│   │   │   ├── sale_validators.py
│   │   │   ├── inventory_validators.py
│   │   │   └── ...
│   │   └── dto/              # Data Transfer Objects
│   │       ├── __init__.py
│   │       ├── sale_dto.py
│   │       ├── product_dto.py
│   │       └── ...
│   ├── services/             # Data access and infrastructure services
│   │   ├── __init__.py
│   │   ├── database.py       # Database connection management
│   │   ├── repositories/     # Data access repositories
│   │   │   ├── __init__.py
│   │   │   ├── product_repository.py
│   │   │   ├── sale_repository.py
│   │   │   ├── customer_repository.py
│   │   │   └── ...
│   │   ├── external/         # External service integrations
│   │   │   ├── __init__.py
│   │   │   ├── payment_gateway.py
│   │   │   ├── tax_service.py
│   │   │   └── ...
│   │   └── utils/            # Utility services
│   │       ├── __init__.py
│   │       ├── printing_service.py
│   │       ├── barcode_service.py
│   │       └── ...
│   ├── accounting/           # Accounting-specific modules
│   │   ├── __init__.py
│   │   ├── chart_of_accounts.py
│   │   ├── journal_entry.py
│   │   ├── tax_manager.py
│   │   └── ...
│   ├── models/               # Database models
│   │   ├── __init__.py
│   │   ├── base.py           # Base model class
│   │   ├── product.py
│   │   ├── inventory.py
│   │   ├── sale.py
│   │   ├── customer.py
│   │   ├── user.py
│   │   └── ...
│   ├── ui/                   # User interface layer
│   │   ├── __init__.py
│   │   ├── main_window.py    # Main application window
│   │   ├── resources/        # UI resources (icons, images)
│   │   ├── style/            # CSS stylesheets
│   │   ├── widgets/          # Reusable UI widgets
│   │   │   ├── __init__.py
│   │   │   ├── product_browser.py
│   │   │   ├── sale_editor.py
│   │   │   └── ...
│   │   ├── dialogs/          # Modal dialogs
│   │   │   ├── __init__.py
│   │   │   ├── login_dialog.py
│   │   │   ├── payment_dialog.py
│   │   │   └── ...
│   │   ├── views/            # Main application views
│   │   │   ├── __init__.py
│   │   │   ├── pos_view.py
│   │   │   ├── inventory_view.py
│   │   │   ├── reporting_view.py
│   │   │   └── ...
│   │   └── models/           # UI-specific data models
│   │       ├── __init__.py
│   │       ├── product_table_model.py
│   │       ├── sales_table_model.py
│   │       └── ...
│   └── common/               # Shared utilities and helpers
│       ├── __init__.py
│       ├── constants.py      # Application constants
│       ├── exceptions.py     # Custom exception types
│       ├── result.py         # Result pattern implementation
│       ├── logging_config.py # Logging configuration
│       └── ...
├── migrations/               # Database migration scripts
│   ├── __init__.py
│   ├── env.py
│   ├── script.py.mako
│   └── versions/             # Migration version files
├── scripts/                  # Utility scripts
│   ├── schema.sql           # Database schema creation script
│   ├── seed_data.py         # Initial data seeding script
│   ├── backup.py            # Database backup utility
│   └── ...
├── tests/                    # Test suite
│   ├── __init__.py
│   ├── conftest.py          # Test configuration and fixtures
│   ├── unit/                # Unit tests
│   │   ├── __init__.py
│   │   ├── test_sales_manager.py
│   │   ├── test_inventory_manager.py
│   │   └── ...
│   ├── integration/         # Integration tests
│   │   ├── __init__.py
│   │   ├── test_repositories.py
│   │   ├── test_services.py
│   │   └── ...
│   └── ui/                  # UI tests
│       ├── __init__.py
│       ├── test_pos_view.py
│       └── ...
├── docs/                     # Documentation
│   ├── index.md
│   ├── architecture.md
│   ├── user_guide.md
│   ├── developer_guide.md
│   └── ...
├── resources/                # Application resources
│   ├── images/
│   ├── reports/             # Report templates
│   ├── localization/        # Translation files
│   └── ...
├── .gitignore
├── pyproject.toml           # Project metadata and dependencies
├── setup.py                 # Installation script
├── requirements.txt         # Development dependencies
├── requirements-prod.txt    # Production dependencies
├── README.md                # Project overview
└── LICENSE                  # License information
Application Modules
Core Application Modules
ApplicationCore (app/application_core.py)
The central component responsible for dependency management and application lifecycle.

Key Responsibilities:

Manages service and manager instances
Provides dependency injection
Coordinates application startup and shutdown
Maintains application state
Implementation Pattern:

class ApplicationCore:
    """Central application core that manages all dependencies."""
    
    def __init__(self, config_path=None):
        """Initialize the application core with optional configuration path."""
        self.config = self._load_config(config_path)
        self._db_session = None
        self._managers = {}
        self._services = {}
        
    def startup(self):
        """Initialize all required services and prepare the application."""
        self._initialize_database()
        self._initialize_services()
        self._initialize_managers()
        
    def shutdown(self):
        """Perform cleanup and shutdown procedures."""
        # Close database connections, etc.
        
    @property
    def sales_manager(self):
        """Lazy-loaded sales manager instance."""
        if 'sales_manager' not in self._managers:
            from app.business_logic.managers.sales_manager import SalesManager
            self._managers['sales_manager'] = SalesManager(self)
        return self._managers['sales_manager']
    
    @property
    def inventory_manager(self):
        """Lazy-loaded inventory manager instance."""
        if 'inventory_manager' not in self._managers:
            from app.business_logic.managers.inventory_manager import InventoryManager
            self._managers['inventory_manager'] = InventoryManager(self)
        return self._managers['inventory_manager']
    
    # Additional manager properties follow the same pattern
    
    @property
    def product_repository(self):
        """Lazy-loaded product repository instance."""
        if 'product_repository' not in self._services:
            from app.services.repositories.product_repository import ProductRepository
            self._services['product_repository'] = ProductRepository(self.db_session)
        return self._services['product_repository']
    
    # Additional repository and service properties follow the same pattern
    
    @property
    def db_session(self):
        """Get the current database session."""
        if not self._db_session:
            self._initialize_database()
        return self._db_session
    
    def _initialize_database(self):
        """Set up the database connection."""
        from app.services.database import get_session
        self._db_session = get_session(self.config)
    
    def _load_config(self, config_path):
        """Load application configuration."""
        from app.config import load_config
        return load_config(config_path)

Business Logic Managers
Business logic managers implement the core business functionality of the application. Each manager focuses on a specific domain area.

SalesManager Example (app/business_logic/managers/sales_manager.py):

from app.common.result import Result
from app.business_logic.dto.sale_dto import SaleCreateDTO, SaleDTO, SaleLineItemDTO
from app.business_logic.validators.sale_validators import validate_new_sale

class SalesManager:
    """Manages all sales-related business operations."""
    
    def __init__(self, app_core):
        """Initialize with application core for dependency access."""
        self.app_core = app_core
    
    async def create_sale(self, sale_dto: SaleCreateDTO) -> Result[SaleDTO]:
        """Create a new sale transaction."""
        # Validate input
        validation_result = validate_new_sale(sale_dto)
        if not validation_result.success:
            return validation_result
        
        # Process business logic
        try:
            # Begin transaction
            async with self.app_core.db_session.begin():
                # Create sale record
                sale = await self.app_core.sale_repository.create_sale(sale_dto)
                
                # Process inventory changes
                for item in sale_dto.line_items:
                    await self.app_core.inventory_manager.adjust_inventory(
                        item.product_id, item.variant_id, -item.quantity, 
                        reference_id=sale.id, reference_type="SALE"
                    )
                
                # Process payment if provided
                if sale_dto.payment:
                    payment_result = await self.app_core.payment_manager.process_payment(
                        sale.id, sale_dto.payment
                    )
                    if not payment_result.success:
                        return payment_result
                
                # Generate accounting entries
                await self.app_core.accounting_manager.create_sale_journal_entry(sale.id)
                
                # Return completed sale
                sale_dto = await self.app_core.sale_repository.get_sale_by_id(sale.id)
                return Result.success(sale_dto)
        except Exception as e:
            # Log error
            self.app_core.logger.error(f"Error creating sale: {str(e)}")
            return Result.failure(f"Failed to create sale: {str(e)}")
    
    # Additional methods for sales operations
    async def get_sale(self, sale_id):
        """Retrieve a sale by ID."""
        pass
    
    async def void_sale(self, sale_id, reason):
        """Void an existing sale."""
        pass
    
    async def process_return(self, original_sale_id, return_items, reason):
        """Process a return against an original sale."""
        pass
