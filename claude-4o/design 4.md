<think>
This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore Point-of-Sale (POS) system. The user has provided detailed architectural considerations and requirements. I need to create a thorough PRD that includes:

1. Executive Summary
2. Product Overview
3. Technology Stack
4. Database Schema Design
5. Codebase File Hierarchy
6. Application Modules and User Interaction Diagram
7. Key Application Modules and Files Description
8. Development Environment Setup
9. Production Environment Setup
10. Architecture Details
11. Security Considerations
12. Testing Strategy
13. Deployment Strategy

The document needs to be at least 6000 words and should be comprehensive enough to guide the actual development without ambiguity. I'll need to incorporate the architectural considerations mentioned:
- Layered architecture with clear separation of concerns
- Dependency injection through ApplicationCore
- Asynchronous processing model
- Multi-currency support
- Singapore regulatory compliance

Let me structure this PRD systematically.
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
12. [Testing Strategy](#testing-strategy)
13. [Deployment and Maintenance](#deployment-and-maintenance)

## Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application specifically designed for small to medium-sized businesses (SMBs) in Singapore. Built with modern technologies including Python, PySide6, and PostgreSQL, this system provides a professional-grade retail management solution that fully complies with Singapore's regulatory requirements, including GST reporting, multi-currency transactions, and local payment methods.

The application architecture emphasizes scalability, maintainability, and performance through a clean layered architecture, robust asynchronous processing capabilities, and strong data integrity mechanisms. The system implements industry best practices including Dependency Injection, Data Transfer Objects (DTOs), and the Result pattern to ensure code quality and maintainability.

### Key Features
- Complete point-of-sale functionality with barcode scanning support
- Inventory management with real-time stock tracking
- Customer relationship management (CRM)
- Multi-currency support with real-time exchange rates
- GST compliance and automated reporting
- Employee management with role-based access control
- Comprehensive reporting and analytics
- Integration with Singapore payment gateways (NETS, PayNow)
- Offline capability with automatic synchronization
- Multi-store support

## Product Overview

### Business Context

Singapore's retail landscape presents unique challenges for SMBs, including strict GST compliance requirements, diverse payment methods, and multi-currency transactions due to tourism and cross-border trade. The SG POS System addresses these challenges by providing a localized solution that understands and adapts to Singapore's business environment.

### Target Users

1. **Primary Users**: Retail store owners and managers in Singapore
2. **Secondary Users**: 
   - Cashiers and sales staff
   - Inventory managers
   - Accountants and bookkeepers
   - Business analysts

### Core Value Propositions

1. **Regulatory Compliance**: Automated GST calculation, reporting, and submission to IRAS
2. **Localization**: Support for Singapore-specific payment methods and business practices
3. **Efficiency**: Streamlined operations through automation and intelligent workflows
4. **Scalability**: Architecture supporting growth from single store to multi-location operations
5. **Reliability**: Offline capability ensuring business continuity
6. **Integration**: Seamless connection with local banks, payment gateways, and government systems

### Functional Requirements

#### Point of Sale Operations
- Product catalog management with variants and bundles
- Barcode scanning and printing
- Quick product search and filtering
- Shopping cart management with discounts and promotions
- Multiple payment methods (cash, card, NETS, PayNow, vouchers)
- Receipt printing and email
- Return and exchange processing
- Layaway and deposit management
- Split payment functionality

#### Inventory Management
- Real-time stock tracking across locations
- Purchase order management
- Supplier management
- Stock transfer between locations
- Automatic reorder points
- Stock take and adjustment
- Product categorization and tagging
- Batch and expiry tracking
- Serial number tracking for high-value items

#### Customer Management
- Customer profile creation and management
- Purchase history tracking
- Loyalty program management
- Customer segmentation
- Targeted promotions
- Credit account management
- Customer feedback collection

#### Financial Management
- Daily cash reconciliation
- Multi-currency transactions
- Exchange rate management
- GST calculation and reporting
- Payment gateway reconciliation
- Accounts receivable tracking
- Financial reporting
- Integration with accounting software

#### Employee Management
- User account creation with role-based permissions
- Time clock functionality
- Commission tracking
- Performance metrics
- Shift management
- Access control and audit trails

#### Reporting and Analytics
- Sales reports (daily, weekly, monthly, yearly)
- Inventory reports
- Customer analytics
- Employee performance reports
- GST reports for IRAS submission
- Custom report builder
- Dashboard with key metrics
- Export functionality (PDF, Excel, CSV)

### Non-Functional Requirements

#### Performance
- Transaction processing: < 2 seconds
- Report generation: < 5 seconds for standard reports
- System startup: < 10 seconds
- Database query response: < 500ms for common operations
- Support for 10,000+ products
- Handle 1,000+ transactions per day

#### Reliability
- 99.9% uptime during business hours
- Automatic backup every 4 hours
- Transaction rollback capability
- Data recovery within 15 minutes
- Offline mode for up to 7 days

#### Security
- End-to-end encryption for sensitive data
- PCI DSS compliance for payment processing
- Role-based access control
- Audit trail for all transactions
- Secure API authentication
- Data anonymization for reports

#### Usability
- Intuitive interface requiring minimal training
- Keyboard shortcuts for common operations
- Touch screen support
- Multi-language support (English, Mandarin, Malay, Tamil)
- Accessibility compliance (WCAG 2.1 AA)

#### Scalability
- Support for up to 50 concurrent users
- Database capable of storing 5 years of transaction data
- Modular architecture for feature additions
- Cloud-ready architecture

## Technology Stack

### Core Technologies

#### Programming Language: Python 3.11+
- **Rationale**: Python offers excellent library ecosystem, rapid development capabilities, and strong community support
- **Key Libraries**:
  - `asyncio`: Asynchronous programming support
  - `typing`: Type hints for better code quality
  - `dataclasses`: Simplified data structure definitions
  - `decimal`: Precise financial calculations

#### GUI Framework: PySide6 (Qt for Python)
- **Rationale**: Cross-platform compatibility, modern UI capabilities, excellent performance
- **Key Components**:
  - Qt Widgets for traditional desktop UI
  - Qt Quick/QML for modern, fluid interfaces
  - Qt Charts for data visualization
  - Qt Network for API communications
  - Qt Print Support for receipt printing

#### Database: PostgreSQL 15+
- **Rationale**: ACID compliance, advanced features, excellent performance, JSON support
- **Key Features Used**:
  - Triggers for audit trails
  - Stored procedures for complex calculations
  - Materialized views for reporting
  - Full-text search for product lookup
  - JSONB for flexible data storage

#### ORM: SQLAlchemy 2.0+
- **Rationale**: Mature, feature-rich ORM with excellent PostgreSQL support
- **Configuration**:
  - Declarative mapping
  - Connection pooling
  - Query optimization
  - Migration support via Alembic

### Supporting Technologies

#### API Framework: FastAPI
- For future REST API development
- OpenAPI documentation generation
- Async support

#### Task Queue: Celery with Redis
- Background job processing
- Scheduled tasks (reports, backups)
- Distributed task execution

#### Caching: Redis
- Session management
- Temporary data storage
- Performance optimization

#### Message Queue: RabbitMQ
- Event-driven architecture
- Microservices communication
- Real-time notifications

#### Monitoring and Logging
- **Sentry**: Error tracking and monitoring
- **Prometheus + Grafana**: Performance monitoring
- **ELK Stack**: Centralized logging
- **structlog**: Structured logging in application

#### Testing Frameworks
- **pytest**: Unit and integration testing
- **pytest-asyncio**: Async code testing
- **pytest-qt**: GUI testing
- **factory_boy**: Test data generation
- **hypothesis**: Property-based testing

#### Development Tools
- **Black**: Code formatting
- **isort**: Import sorting
- **mypy**: Static type checking
- **pylint**: Code quality analysis
- **pre-commit**: Git hooks for code quality
- **Poetry**: Dependency management

#### Deployment and Infrastructure
- **Docker**: Containerization
- **Docker Compose**: Local development environment
- **Kubernetes**: Production orchestration
- **GitHub Actions**: CI/CD pipeline
- **Terraform**: Infrastructure as Code

## System Architecture

### Architectural Principles

1. **Separation of Concerns**: Clear boundaries between layers
2. **Dependency Inversion**: High-level modules independent of low-level modules
3. **Single Responsibility**: Each class/module has one reason to change
4. **Open/Closed Principle**: Open for extension, closed for modification
5. **Interface Segregation**: Specific interfaces rather than general-purpose ones
6. **Don't Repeat Yourself (DRY)**: Minimize code duplication

### Layered Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Presentation Layer                     │
│  (PySide6 UI Components, Views, Controllers)            │
├─────────────────────────────────────────────────────────┤
│                  Business Logic Layer                    │
│  (Managers, Use Cases, Business Rules, Validators)      │
├─────────────────────────────────────────────────────────┤
│                   Service Layer                          │
│  (Application Services, DTOs, Mappers)                  │
├─────────────────────────────────────────────────────────┤
│                 Data Access Layer                        │
│  (Repositories, Query Objects, Unit of Work)            │
├─────────────────────────────────────────────────────────┤
│                  Infrastructure Layer                    │
│  (Database, External APIs, File System, Cache)          │
└─────────────────────────────────────────────────────────┘
```

### Component Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   UI Components │     │  Business Logic │     │   Data Access   │
│                 │────▶│                 │────▶│                 │
│  - MainWindow   │     │  - Managers     │     │  - Services     │
│  - Dialogs      │     │  - Validators   │     │  - Repositories │
│  - Widgets      │     │  - Calculators  │     │  - Queries      │
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │                       │                       │
         │                       ▼                       │
         │              ┌─────────────────┐             │
         └─────────────▶│ ApplicationCore │◀────────────┘
                        │                 │
                        │ - DI Container  │
                        │ - Config        │
                        │ - Event Bus     │
                        └─────────────────┘
```

### Asynchronous Architecture

The application implements a sophisticated asynchronous model to ensure responsive UI and efficient resource utilization:

```python
# Async Event Loop Architecture
Main Thread (Qt Event Loop)
    │
    ├── UI Components
    │   └── User Interactions
    │
    └── Async Bridge (schedule_task_from_qt)
        │
        └── Worker Thread (asyncio Event Loop)
            ├── Database Operations
            ├── API Calls
            ├── File I/O
            └── Background Tasks
```

## Database Schema Design

### Core Tables

#### 1. Users and Authentication

```sql
-- Users table for system access
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role_id UUID NOT NULL,
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_by UUID REFERENCES users(id),
    updated_by UUID REFERENCES users(id),
    FOREIGN KEY (role_id) REFERENCES roles(id)
);

-- Roles for access control
CREATE TABLE roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    permissions JSONB NOT NULL DEFAULT '{}',
    is_system BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Audit trail for all changes
CREATE TABLE audit_log (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    table_name VARCHAR(100) NOT NULL,
    record_id UUID NOT NULL,
    action VARCHAR(20) NOT NULL, -- INSERT, UPDATE, DELETE
    old_values JSONB,
    new_values JSONB,
    user_id UUID NOT NULL,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

#### 2. Products and Inventory

```sql
-- Product categories with hierarchical structure
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) NOT NULL,
    parent_id UUID,
    path TEXT NOT NULL, -- Materialized path for efficient queries
    level INTEGER NOT NULL DEFAULT 0,
    is_active BOOLEAN DEFAULT true,
    sort_order INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (parent_id) REFERENCES categories(id)
);

-- Main products table
CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category_id UUID NOT NULL,
    brand_id UUID,
    unit_of_measure VARCHAR(20) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    is_service BOOLEAN DEFAULT false,
    track_inventory BOOLEAN DEFAULT true,
    allow_negative_stock BOOLEAN DEFAULT false,
    min_stock_level DECIMAL(10,2) DEFAULT 0,
    reorder_point DECIMAL(10,2) DEFAULT 0,
    reorder_quantity DECIMAL(10,2) DEFAULT 0,
    attributes JSONB DEFAULT '{}', -- Flexible attributes
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id),
    FOREIGN KEY (brand_id) REFERENCES brands(id)
);

-- Product variants (size, color, etc.)
CREATE TABLE product_variants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id UUID NOT NULL,
    sku VARCHAR(50) UNIQUE NOT NULL,
    barcode VARCHAR(50) UNIQUE,
    name VARCHAR(255) NOT NULL,
    attributes JSONB NOT NULL DEFAULT '{}',
    cost DECIMAL(10,2) NOT NULL DEFAULT 0,
    price DECIMAL(10,2) NOT NULL,
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE
);

-- Inventory tracking by location
CREATE TABLE inventory (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    
