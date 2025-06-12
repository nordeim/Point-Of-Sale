Product Requirements Document (PRD)
SG Point-of-Sale (POS) System
Version: 1.0
Date: June 12, 2025
Status: Draft

Table of Contents
Introduction
Product Overview
System Architecture
Database Design
Codebase Organization
Functional Requirements
Non-Functional Requirements
Development Environment
Production Environment
Future Enhancements
1. Introduction
1.1 Purpose and Scope
The SG Point-of-Sale (POS) system is a comprehensive, cross-platform desktop application designed to meet the typical retail needs of small to medium-sized businesses (SMBs) in Singapore. This Product Requirements Document (PRD) outlines the functional and technical specifications for the development of this application.

The system aims to streamline retail operations while ensuring compliance with Singapore's regulatory environment, particularly regarding Goods and Services Tax (GST), electronic receipts, and financial reporting. It offers a complete retail management solution covering sales processing, inventory management, customer tracking, reporting, and accounting integration.

1.2 Definitions and Acronyms
POS: Point of Sale
SMB: Small to Medium-sized Business
GST: Goods and Services Tax (Singapore's value-added tax)
IRAS: Inland Revenue Authority of Singapore
DTO: Data Transfer Object
DI: Dependency Injection
UI: User Interface
BLL: Business Logic Layer
DAL: Data Access Layer
ORM: Object-Relational Mapping
API: Application Programming Interface
PDPA: Personal Data Protection Act
UEN: Unique Entity Number
SGQR: Singapore Quick Response Code
1.3 System Overview
The SG POS system is built with Python and leverages PySide6 for a modern user interface and PostgreSQL for robust data management. It follows a clean, layered architecture to ensure maintainability, scalability, and performance.

Key features include:

Intuitive sales interface with barcode scanning capabilities
Comprehensive inventory management
Customer relationship management with PDPA compliance
Multi-currency support tailored for Singapore's business environment
GST-compliant tax calculation and reporting
Detailed financial and sales reporting
Secure user authentication and role-based access control
Asynchronous processing for responsive UI
Offline operation capability for core functions
2. Product Overview
2.1 Product Perspective
The SG POS system is designed as a standalone desktop application that can operate independently or integrate with other business systems. It aims to replace manual sales processes, spreadsheet-based inventory tracking, and basic cash registers currently used by many SMBs in Singapore.

The system is positioned as a professional-grade yet affordable alternative to enterprise-level POS solutions, offering comparable functionality tailored specifically to the Singaporean market without the complexity and cost of larger systems.

2.2 User Classes and Characteristics
The system will serve several types of users:

Cashiers/Sales Staff

Primary users who process sales transactions
Typically have limited technical knowledge
Require an intuitive, efficient interface
Need quick access to product information and pricing
Will use the system for extended periods daily
Store Managers

Responsible for day-to-day operations
Need access to real-time sales and inventory data
Configure promotions and pricing
Manage staff accounts and permissions
Generate and analyze reports
Business Owners

Require comprehensive financial overview
Access to all system functions
Focus on profitability metrics and business performance
May have varying levels of technical expertise
Inventory Managers

Responsible for stock levels and product management
Need detailed inventory reports and alerts
Manage product categories, attributes, and pricing
Process purchase orders and stock receipts
System Administrators

Technical users responsible for system configuration
Manage database backups and system updates
Configure system parameters and integrations
Troubleshoot technical issues
2.3 Operating Environment
The SG POS system will operate in the following environment:

Hardware: Standard desktop or laptop computers, with support for peripheral devices including:

Barcode scanners
Receipt printers
Cash drawers
Customer-facing displays
Touch screens (optional)
Operating Systems:

Windows 10/11
macOS 10.14 (Mojave) and later
Major Linux distributions (Ubuntu 20.04+, Fedora 34+)
Minimum System Requirements:

Processor: Dual-core 2.0 GHz or higher
RAM: 4GB minimum, 8GB recommended
Storage: 1GB for application, plus database storage (varies with usage)
Display: 1366x768 resolution minimum
Network: Internet connection for updates and cloud features
2.4 Design and Implementation Constraints
Regulatory Compliance: Must adhere to Singapore's GST regulations and electronic receipt requirements
Data Protection: Must comply with Singapore's Personal Data Protection Act (PDPA)
Offline Operation: Core sales functionality must operate without internet connectivity
Database Integrity: Must maintain transactional integrity even during system failures
Cross-Platform Compatibility: Must provide consistent experience across supported operating systems
Performance: Transaction processing must complete within 2 seconds under normal load
Localization: All monetary values, dates, and numbers must follow Singapore formatting standards
2.5 Assumptions and Dependencies
Assumptions:
Users have basic computer literacy
Businesses have reliable power supply
Standard POS peripherals follow industry protocols
Single-store deployment (multi-store functionality planned for future versions)
Dependencies:
Python 3.9 or higher runtime environment
PostgreSQL 12.0 or higher database server
PySide6 library and dependencies
Network connectivity for certain features (cloud backup, electronic receipts)
Appropriate drivers for POS peripherals
3. System Architecture
3.1 Architectural Overview
The SG POS system follows a clean, layered architecture pattern with clear separation of concerns. This architecture ensures maintainability, testability, and scalability while facilitating future enhancements.

Architecture Diagram

The system is structured into four primary layers:

Presentation Layer: Handles all user interface components and user interactions
Business Logic Layer: Implements the core application logic and business rules
Data Access Layer: Manages database interactions and data persistence
Domain Layer: Defines the core business entities and value objects
These layers interact through well-defined interfaces, reducing coupling and enabling modular development and testing.

The system also incorporates cross-cutting concerns such as:

Error handling and logging
Authentication and authorization
Configuration management
Asynchronous processing
3.2 Technology Stack
Core Technologies:
Programming Language: Python 3.9+
UI Framework: PySide6 (Qt for Python)
Database: PostgreSQL 12.0+
ORM: SQLAlchemy 2.0+
Asynchronous Framework: asyncio
Testing: pytest
Additional Libraries and Tools:
Data Validation: Pydantic
Logging: Python standard logging with rotating file handlers
PDF Generation: ReportLab
Barcode Processing: python-barcode
Currency Handling: py-moneyed
Date/Time Handling: Arrow
Configuration: PyYAML
Encryption: cryptography
Database Migrations: Alembic
3.3 Layered Architecture
3.3.1 Presentation Layer (app/ui)
Implements all UI components using PySide6
Maintains separation from business logic through view models
Handles user input validation and formatting
Communicates with business layer through the ApplicationCore
Key components:

Main application window and navigation
Sales terminal interface
Inventory management screens
Customer management interface
Reporting and analytics dashboards
Settings and configuration screens
3.3.2 Business Logic Layer (app/business_logic, app/accounting)
Implements core application functionality
Enforces business rules and validation
Orchestrates complex workflows
Maintains application state
Handles error conditions and exceptional cases
Key components:

ApplicationCore (central coordination point)
Manager classes for major functional areas
Business validators and rule enforcers
Service coordinators
Event handlers
3.3.3 Data Access Layer (app/services)
Abstracts database operations
Implements the Repository pattern
Handles data conversion between domain entities and database models
Manages transactions and ensures data integrity
Implements caching strategies for performance optimization
Key components:

Service classes for each domain entity
Query builders and executors
Data mappers and converters
Transaction managers
Cache managers
3.3.4 Domain Layer (app/models)
Defines business entities and value objects
Implements entity behavior and business rules
Defines domain events and state transitions
Provides a stable core for the application
Key components:

Entity classes (Product, Customer, Sale, etc.)
Value objects (Money, Address, etc.)
Domain events
Enumerations and constants
3.4 Dependency Injection Model
The SG POS system employs a dependency injection (DI) approach to manage component dependencies, improve testability, and maintain loose coupling between components.

Key Features of the DI Implementation:
ApplicationCore as DI Container:

Central registry for all system services and managers
Implements lazy initialization via property methods
Provides controlled access to system components
Unified Constructor Signature:

All manager classes follow consistent initialization pattern
Simplified constructor: __init__(self, app_core: "ApplicationCore")
Components source dependencies from the ApplicationCore
Interface-Based Design:

Components depend on interfaces rather than concrete implementations
Enables mock substitution for testing
Facilitates alternative implementations
Configuration-Driven Initialization:

Component behavior configurable through external settings
Allows customization without code changes
Supports different environments (development, testing, production)
3.5 Asynchronous Processing Model
The system implements a robust asynchronous processing model to ensure responsive UI while handling potentially long-running operations.

Key Components:
Dedicated AsyncIO Thread:

Separate thread for the asyncio event loop
Prevents I/O operations from blocking the main UI thread
Initialized at application startup in app/main.py
Task Scheduling Bridge:

schedule_task_from_qt function safely bridges Qt and asyncio
Allows UI components to initiate background tasks
Handles exceptions and task lifecycle management
Thread-Safe UI Updates:

Background tasks marshal UI updates back to main thread
Uses QMetaObject.invokeMethod for thread safety
Implements callback pattern for completion notification
Cancellation and Timeout Handling:

Tasks can be cancelled from UI actions
Timeouts prevent indefinite waiting
Resources are properly released on cancellation
Progress Reporting:

Long-running tasks report progress back to UI
Enables accurate progress indicators
Allows user feedback during processing
4. Database Design
4.1 Database Schema
The database schema is designed to support all functional requirements while ensuring data integrity, performance, and flexibility. The schema follows normalized design principles with strategic denormalization where performance demands.

Core Entity Groups:
Products and Inventory

Products (master product data)
Inventory (stock levels and location)
Product Categories (hierarchical classification)
Product Attributes (customizable properties)
Units of Measure (conversion rules)
Suppliers (vendor information)
Sales and Customers

Customers (customer master data)
Sales (transaction headers)
Sale Items (transaction lines)
Payments (payment records)
Refunds (return processing)
Loyalty (points and rewards)
Financial and Accounting

Tax Rates (GST configurations)
Payment Methods (cash, card, etc.)
Currencies (exchange rates)
Journal Entries (accounting records)
Chart of Accounts (account structure)
Fiscal Periods (accounting periods)
System and Administration

Users (user accounts)
Roles (permission groups)
Permissions (access rights)
Audit Log (system activity)
Settings (configuration values)
Stores (business locations)
4.2 Entity Relationship Diagram
┌────────────────┐       ┌────────────────┐       ┌────────────────┐
│    products    │       │   categories   │       │   attributes   │
├────────────────┤       ├────────────────┤       ├────────────────┤
│ id             │       │ id             │       │ id             │
│ sku            │◄──────┤ parent_id      │       │ name           │
│ barcode        │       │ name           │       │ type           │
│ name           │       │ description    │       │ required       │
│ description    │       │ image_url      │       └────────┬───────┘
│ category_id    │───────┤ active         │                │
│ unit_id        │       └────────────────┘                │
│ cost_price     │                                         │
│ sell_price     │                                         │
│ tax_rate_id    │       ┌────────────────┐                │
│ min_stock      │       │ product_attrs  │◄───────────────┘
│ active         │       ├────────────────┤
└──────┬─────────┘       │ id             │
       │                 │ product_id     │◄───────┐
       │                 │ attribute_id   │        │
       │                 │ value          │        │
       │                 └────────────────┘        │
       │                                           │
┌──────▼─────────┐       ┌────────────────┐       │
│   inventory    │       │  sale_items    │       │
├────────────────┤       ├────────────────┤       │
│ id             │       │ id             │       │
│ product_id     │       │ sale_id        │◄──────┼──────────┐
│ location_id    │       │ product_id     │◄──────┘          │
│ quantity       │       │ quantity       │                  │
│ updated_at     │       │ unit_price     │                  │
└────────────────┘       │ discount       │                  │
                         │ tax_amount     │                  │
┌────────────────┐       │ subtotal       │        ┌────────▼───────┐
│   customers    │       └────────────────┘        │     sales      │
├────────────────┤                                 ├────────────────┤
│ id             │       ┌────────────────┐        │ id             │
│ code           │       │   
