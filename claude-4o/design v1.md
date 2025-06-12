<think>
This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. The user has provided detailed architectural considerations and requirements. I need to create a thorough PRD that includes:

1. Executive Summary
2. Product Overview
3. Technology Stack
4. Database Schema Design
5. Codebase File Hierarchy
6. Application Modules and User Interaction Diagram
7. Key Application Modules and Files Description
8. Development and Production Environment Setup
9. Architecture Details
10. Security Considerations
11. Performance Requirements
12. Testing Strategy
13. Deployment Strategy

The document needs to be at least 6000 words and should be comprehensive enough to guide the actual development without ambiguity. I'll need to incorporate the architectural considerations mentioned, including the layered architecture, dependency injection pattern, and asynchronous model.

Let me structure this PRD systematically:
</think>

# Product Requirements Document: SG Point-of-Sale (POS) System

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Product Overview](#product-overview)
3. [Technology Stack](#technology-stack)
4. [System Architecture](#system-architecture)
5. [Database Schema Design](#database-schema-design)
6. [Codebase File Hierarchy](#codebase-file-hierarchy)
7. [Application Modules and User Interaction](#application-modules-and-user-interaction)
8. [Key Application Modules Description](#key-application-modules-description)
9. [Development Environment Setup](#development-environment-setup)
10. [Production Environment Setup](#production-environment-setup)
11. [Security Architecture](#security-architecture)
12. [Performance Requirements](#performance-requirements)
13. [Testing Strategy](#testing-strategy)
14. [Deployment Strategy](#deployment-strategy)
15. [Compliance and Regulatory Requirements](#compliance-and-regulatory-requirements)

## 1. Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed to meet the retail needs of small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for a modern user interface and PostgreSQL for robust data management, this system offers a professional-grade retail tool tailored to Singapore's unique regulatory environment.

The application architecture emphasizes scalability, maintainability, and performance through a clean layered architecture, robust asynchronous processing model, strong data integrity mechanisms, and consistent adherence to software engineering best practices including Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern.

Key features include multi-currency support, GST compliance, comprehensive inventory management, customer relationship management, and detailed financial reporting capabilities. The system is designed to handle real-world business complexity while maintaining a user-friendly interface suitable for retail staff with varying technical expertise.

## 2. Product Overview

### 2.1 Vision Statement
To provide Singapore's SMB retail sector with a modern, efficient, and compliant point-of-sale solution that streamlines operations, enhances customer service, and provides actionable business insights while maintaining full compliance with local regulations.

### 2.2 Target Market
- Small to medium-sized retail businesses in Singapore
- Multi-outlet retail chains
- Specialty stores and boutiques
- Food and beverage establishments
- Service-based businesses requiring point-of-sale capabilities

### 2.3 Core Features

#### 2.3.1 Sales Management
- Quick and intuitive product search and selection
- Barcode scanning support
- Multiple payment methods (cash, credit/debit cards, e-wallets, NETS)
- Split payment functionality
- Quotation and invoice generation
- Returns and exchanges processing
- Layaway and deposit management

#### 2.3.2 Inventory Management
- Real-time stock tracking
- Multi-location inventory support
- Automatic reorder point alerts
- Stock transfer between locations
- Batch and serial number tracking
- Product variants management (size, color, etc.)
- Supplier management and purchase orders

#### 2.3.3 Customer Management
- Customer profile creation and management
- Purchase history tracking
- Loyalty program integration
- Customer credit management
- Targeted marketing capabilities
- Customer feedback collection

#### 2.3.4 Financial Management
- GST calculation and reporting
- Multi-currency support with real-time exchange rates
- Daily cash reconciliation
- Comprehensive financial reporting
- Integration with accounting systems
- Profit margin analysis
- Commission calculation for sales staff

#### 2.3.5 Reporting and Analytics
- Real-time sales dashboards
- Inventory reports
- Customer analytics
- Staff performance reports
- Financial statements
- GST reports for IRAS submission
- Custom report builder

#### 2.3.6 Staff Management
- User role and permission management
- Time clock functionality
- Commission tracking
- Performance metrics
- Shift management

### 2.4 Compliance Features
- IRAS GST compliance
- PDPA (Personal Data Protection Act) compliance
- PCI DSS compliance for payment processing
- Audit trail for all transactions
- Data retention policies

## 3. Technology Stack

### 3.1 Core Technologies

#### 3.1.1 Programming Language
- **Python 3.11+**: Primary development language chosen for its robust ecosystem, excellent library support, and rapid development capabilities.

#### 3.1.2 User Interface Framework
- **PySide6 (Qt 6.5+)**: Modern, cross-platform GUI framework providing native look and feel across Windows, macOS, and Linux.
- **Qt Designer**: For rapid UI prototyping and design.

#### 3.1.3 Database
- **PostgreSQL 15+**: Enterprise-grade relational database with excellent support for complex queries, transactions, and data integrity.
- **SQLAlchemy 2.0+**: Modern ORM providing database abstraction and query building capabilities.
- **Alembic**: Database migration tool for version control of schema changes.

#### 3.1.4 Asynchronous Processing
- **asyncio**: Python's built-in asynchronous I/O framework for non-blocking operations.
- **aiohttp**: Asynchronous HTTP client/server framework for API integrations.
- **asyncpg**: High-performance asynchronous PostgreSQL driver.

### 3.2 Supporting Technologies

#### 3.2.1 API and Integration
- **FastAPI**: Modern web framework for building REST APIs for potential mobile app integration.
- **Pydantic**: Data validation and settings management using Python type annotations.
- **httpx**: Modern HTTP client with async support for external API calls.

#### 3.2.2 Security
- **cryptography**: For encryption of sensitive data.
- **python-jose**: JSON Web Token implementation for secure authentication.
- **passlib**: Password hashing library with bcrypt support.

#### 3.2.3 Reporting and Documents
- **ReportLab**: PDF generation for invoices and reports.
- **openpyxl**: Excel file generation for data exports.
- **Jinja2**: Template engine for document generation.

#### 3.2.4 Development Tools
- **pytest**: Testing framework with async support.
- **pytest-qt**: Qt/PySide6 testing plugin.
- **black**: Code formatter for consistent style.
- **mypy**: Static type checker for Python.
- **ruff**: Fast Python linter.
- **pre-commit**: Git hook framework for code quality.

#### 3.2.5 Deployment and Operations
- **Docker**: Containerization for consistent deployment.
- **docker-compose**: Multi-container orchestration for development.
- **GitHub Actions**: CI/CD pipeline automation.
- **Sentry**: Error tracking and performance monitoring.
- **structlog**: Structured logging for better observability.

## 4. System Architecture

### 4.1 Architectural Principles

The SG POS system follows a clean, layered architecture with strict separation of concerns:

1. **Presentation Layer**: Handles all user interface logic and user interactions.
2. **Business Logic Layer**: Contains all business rules and workflow orchestration.
3. **Data Access Layer**: Manages all database interactions through the repository pattern.
4. **Infrastructure Layer**: Provides cross-cutting concerns like logging, caching, and external integrations.

### 4.2 Architectural Patterns

#### 4.2.1 Dependency Injection
The system uses a centralized `ApplicationCore` class that manages all dependencies through lazy initialization. This approach provides:
- Loose coupling between components
- Easy testing through dependency substitution
- Clear dependency graph
- Simplified initialization process

#### 4.2.2 Repository Pattern
All data access is abstracted through service classes that implement the repository pattern:
- Encapsulation of query logic
- Consistent data access interface
- Easy mocking for testing
- Database vendor independence

#### 4.2.3 Result Pattern
Operations that can fail return Result objects containing either success values or error information:
- Explicit error handling
- No exceptions for expected failures
- Clear success/failure paths
- Rich error information

#### 4.2.4 Data Transfer Objects (DTOs)
DTOs are used for data transfer between layers:
- Clear contracts between layers
- Validation at boundaries
- Decoupling of internal models from external representations

### 4.3 Asynchronous Architecture

The application implements a sophisticated asynchronous model:
- Main GUI thread remains responsive
- Background tasks run in separate asyncio event loop
- Thread-safe communication between GUI and async tasks
- Non-blocking database operations
- Concurrent API calls for external integrations

## 5. Database Schema Design

### 5.1 Core Tables

```sql
-- Company and Configuration
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    registration_number VARCHAR(50) UNIQUE NOT NULL,
    gst_registration_number VARCHAR(50),
    address TEXT,
    phone VARCHAR(50),
    email VARCHAR(255),
    logo_url TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Users and Authentication
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    username VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL CHECK (role IN ('admin', 'manager', 'cashier', 'viewer')),
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, username),
    UNIQUE(company_id, email)
);

-- Outlets/Stores
CREATE TABLE outlets (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(50),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

-- Product Categories
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    parent_id UUID REFERENCES categories(id),
    code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, code)
);

-- Products
CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    category_id UUID REFERENCES categories(id),
    sku VARCHAR(100) NOT NULL,
    barcode VARCHAR(100),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    unit_of_measure VARCHAR(50) NOT NULL,
    cost_price DECIMAL(15, 4) NOT NULL DEFAULT 0,
    selling_price DECIMAL(15, 4) NOT NULL,
    tax_rate DECIMAL(5, 2) NOT NULL DEFAULT 0,
    is_taxable BOOLEAN DEFAULT true,
    is_active BOOLEAN DEFAULT true,
    track_inventory BOOLEAN DEFAULT true,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, sku),
    UNIQUE(company_id, barcode)
);

-- Product Variants
CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID NOT NULL REFERENCES products(id),
    sku VARCHAR(100) NOT NULL,
    barcode VARCHAR(100),
    variant_name VARCHAR(255) NOT NULL,
    attributes JSONB NOT NULL, -- {size: "L", color: "Red"}
    cost_price DECIMAL(15, 4) NOT NULL,
    selling_price DECIMAL(15, 4) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(product_id, sku)
);

-- Inventory
CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    outlet_id UUID NOT NULL REFERENCES outlets(id),
    product_id UUID NOT NULL REFERENCES products(id),
    product_variant_id UUID REFERENCES product_variants(id),
    quantity_on_hand DECIMAL(15, 4) NOT NULL DEFAULT 0,
    quantity_reserved DECIMAL(15, 4) NOT NULL DEFAULT 0,
    quantity_available DECIMAL(15, 4) GENERATED ALWAYS AS (quantity_on_hand - quantity_reserved) STORED,
    last_stock_take_date DATE,
    last_stock_take_quantity DECIMAL(15, 4),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(outlet_id, product_id, product_variant_id)
);

-- Customers
CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    customer_code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    phone VARCHAR(50),
    address TEXT,
    date_of_birth DATE,
    gender VARCHAR(20),
    id_type VARCHAR(50), -- NRIC, FIN, Passport
    id_number VARCHAR(50),
    credit_limit DECIMAL(15, 2) DEFAULT 0,
    current_balance DECIMAL(15, 2) DEFAULT 0,
    loyalty_points INTEGER DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, customer_code)
);

-- Suppliers
CREATE TABLE suppliers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    supplier_code VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL,
    contact_person VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(50),
    address TEXT,
    payment_terms INTEGER DEFAULT 30, -- days
    is_active BOOLEAN DEFAULT true,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(company_id, supplier_code)
);

-- Sales Transactions
CREATE TABLE sales_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    outlet_id UUID NOT NULL REFERENCES outlets(id),
    transaction_number VARCHAR(50) NOT NULL,
    transaction_date TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT CURRENT_TIMESTAMP,
    customer_id UUID REFERENCES customers(id),
    cashier_id UUID NOT NULL REFERENCES users(id),
    subtotal DECIMAL(15, 2) NOT NULL,
    tax_amount DECIMAL(15, 2) NOT NULL,
    discount_amount DECIMAL(15, 2) NOT NULL DEFAULT 0,
    total_amount DECIMAL(15, 2) NOT NULL,
    payment_status VARCHAR(20) NOT NULL CHECK (payment_status IN ('pending', 'partial', 'paid', 'refunded')),
    notes
