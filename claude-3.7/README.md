# Product Requirements Document (PRD): SG Point-of-Sale (POS) System

**Version:** 1.0  
**Date:** June 12, 2025  
**Author:** Technical Design Team

---

## Executive Summary

The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for the user interface and PostgreSQL for data management, this solution provides a robust, feature-rich retail management platform that addresses the unique regulatory and business requirements of the Singaporean market.

The system will support all essential retail operations including sales processing, inventory management, customer relationship management, employee management, reporting, and accounting, with special attention to Singapore-specific requirements such as GST compliance, multi-currency support, and integration with local payment methods. The architecture emphasizes reliability, security, and extensibility, allowing businesses to scale their operations without needing to migrate to a different platform.

This PRD outlines the complete requirements, technical specifications, and implementation details for the development team to deliver a production-ready application that meets the highest standards of software quality and user experience.

---

## 1. Introduction

### 1.1 Purpose
This document outlines the comprehensive requirements for the SG Point-of-Sale (POS) System, a specialized retail management solution for Singapore's SMB market. It serves as the authoritative reference for all development activities, establishing clear expectations for functionality, architecture, and quality.

### 1.2 Scope
The SG POS System encompasses all core retail operations needed by SMBs in Singapore, from basic sales transactions to advanced inventory management, customer tracking, employee management, and financial reporting. The system is designed as a desktop application that operates independently of internet connectivity for core functions while supporting cloud-based features when online.

### 1.3 Target Users
- **Retail Store Owners/Managers:** Decision-makers who need comprehensive visibility into business operations
- **Sales Associates:** Front-line staff handling customer transactions and inquiries
- **Inventory Managers:** Staff responsible for stock management and procurement
- **Accountants/Bookkeepers:** Financial professionals managing business accounts and tax compliance
- **IT Administrators:** Technical staff responsible for system maintenance and configuration

### 1.4 Business Context
Singapore's retail sector is characterized by:
- Strict regulatory compliance requirements, particularly around GST
- High degree of digitalization and adoption of electronic payments
- Multicultural customer base requiring multilingual support
- Significant tourism driving the need for multi-currency capabilities
- Competitive market requiring robust loyalty and promotion features

## 2. Product Overview

### 2.1 Product Vision
To provide Singapore's SMBs with a comprehensive, compliant, and user-friendly point-of-sale solution that streamlines operations, enhances customer experiences, and provides actionable business insights while meeting all local regulatory requirements.

### 2.2 Key Features
- **Sales Processing**
  - Intuitive transaction interface optimized for speed and accuracy
  - Support for multiple payment methods including cash, cards, QR payments, and mobile wallets
  - Return and exchange processing with configurable policies
- **Inventory Management**
  - Real-time stock tracking across multiple locations
  - Automated reorder notifications
  - Batch tracking and expiration date management
  - Stock transfers between locations
- **Customer Management**
  - Comprehensive customer profiles with purchase history
  - Tiered loyalty programs with points and rewards
  - Customer communications via SMS and email
- **Employee Management**
  - Role-based access control with detailed permissions
  - Time tracking and shift management
  - Sales performance tracking and commissions
- **Reporting and Analytics**
  - Customizable dashboard with key performance indicators
  - Detailed sales, inventory, and financial reports
  - Export capabilities to common formats (Excel, PDF, CSV)
- **Financial Management**
  - GST tracking and reporting compliant with IRAS requirements
  - Multi-currency support with real-time exchange rates
  - Integration with popular accounting software
- **Singapore-Specific Features**
  - GST implementation following Singapore tax regulations
  - Support for Singapore-specific payment methods (NETS, PayNow, etc.)
  - Compliance with local data protection requirements (PDPA)

## 3. Functional Requirements

### 3.1 User Management
#### 3.1.1 User Authentication and Authorization
- Secure login system with multi-factor authentication option
- Role-based access control with granular permissions
- Password policies compliant with Singapore's cybersecurity guidelines
- Session management with automatic timeout for security
- Audit logging of all authentication events

#### 3.1.2 User Roles and Permissions
| Role          | Description               | Default Permissions     |
|---------------|---------------------------|-------------------------|
| Administrator | System-wide access        | All permissions         |
| Manager       | Store management          | Sales, inventory, reporting, limited settings |
| Cashier       | Front-line sales          | Sales processing, basic customer management |
| Inventory Clerk | Stock management        | Inventory viewing and adjustment |
| Accountant    | Financial operations      | Financial reports, end-of-day reconciliation |

#### 3.1.3 User Profile Management
- Personal information management (name, contact, etc.)
- Individual settings and preferences
- Activity history and statistics
- Password reset and account recovery mechanisms

### 3.2 Product Management
#### 3.2.1 Product Catalog
- Hierarchical category management
- Comprehensive product attributes (name, description, images, etc.)
- Multiple SKU support for variants (size, color, etc.)
- Custom fields for additional product information
- Product import/export via CSV and Excel

#### 3.2.2 Pricing Management
- Base price and cost tracking
- Multiple price levels (retail, wholesale, special)
- Time-based promotional pricing
- Quantity-based pricing (bulk discounts)
- Margin and markup calculations

#### 3.2.3 Barcode Management
- Support for multiple barcode formats (UPC, EAN, QR, etc.)
- Barcode generation for internal products
- Batch barcode printing

### 3.3 Inventory Management
#### 3.3.1 Stock Tracking
- Real-time inventory levels across locations
- Minimum stock level alerts
- Stock movement history
- Variance tracking and reconciliation

#### 3.3.2 Procurement
- Purchase order creation and management
- Supplier management with contact information and terms
- Receiving and partial receiving workflows
- Cost tracking and updates

#### 3.3.3 Inventory Adjustments
- Reason-based adjustment tracking
- Bulk adjustment capabilities
- Scheduled physical inventory counts
- Shrinkage analysis and reporting

### 3.4 Sales Processing
#### 3.4.1 Point of Sale Interface
- Touch-optimized interface for efficient transactions
- Product lookup by name, SKU, barcode, or category
- Customer association with transactions
- Discount application (percentage, fixed amount, etc.)
- Tax calculation and display
- Line item editing and removal

#### 3.4.2 Payment Processing
- Support for multiple payment methods in a single transaction
- Change calculation for cash payments
- Integration with payment terminals (credit/debit cards)
- QR code payments (PayNow, NETS QR, etc.)
- Payment splitting between methods
- Foreign currency handling with exchange rate management

#### 3.4.3 Receipt Management
- Customizable receipt templates
- Digital receipt option (email, SMS)
- Receipt reprinting and retrieval
- Inclusion of promotional messages and return policies

#### 3.4.4 Returns and Exchanges
- Original transaction lookup
- Partial and full return processing
- Reason tracking for returns
- Exchange processing with balance calculation
- Return policy enforcement (time limits, condition, etc.)

### 3.5 Customer Management
#### 3.5.1 Customer Profiles
- Basic information (name, contact details, preferences)
- Purchase history and statistics
- Account balance for store credit or prepayments
- Notes and custom fields
- PDPA compliance for data collection and usage

#### 3.5.2 Loyalty Program
- Points accumulation based on purchase amount
- Tiered membership levels with benefits
- Points redemption for discounts or products
- Expiration management for points
- Birthday rewards and special promotions

#### 3.5.3 Customer Communications
- Targeted promotions based on purchase history
- Birthday and anniversary messages
- Receipt and transaction notifications
- Marketing campaign management
- Opt-in/opt-out management for PDPA compliance

### 3.6 Reporting and Analytics
#### 3.6.1 Sales Reports
- Daily, weekly, monthly, and annual sales summaries
- Sales by product, category, employee, time period
- Comparative analysis (current vs. previous periods)
- Tax collection reports
- Payment method distribution

#### 3.6.2 Inventory Reports
- Current stock levels and valuation
- Slow-moving and fast-moving items
- Stockout frequency and duration
- Shrinkage and loss reports
- Product performance analysis

#### 3.6.3 Financial Reports
- Profit and loss statements
- Cost of goods sold
- Margin analysis
- GST reports for IRAS filing
- Cash flow reports

#### 3.6.4 Customer Reports
- Customer purchase frequency and value
- Loyalty program participation and redemption
- Customer acquisition and retention metrics
- Demographic analysis (where applicable)

### 3.7 Financial Management
#### 3.7.1 Cash Management
- Cash drawer tracking and reconciliation
- Bank deposit preparation and recording
- Petty cash management
- Over/short tracking and analysis

#### 3.7.2 Tax Management
- Automatic GST calculation based on product categories
- GST-inclusive and GST-exclusive price management
- GST reporting in compliance with IRAS requirements
- Support for GST-registered and non-registered businesses

#### 3.7.3 Accounting Integration
- Export of financial data to common accounting systems
- Chart of accounts mapping
- Journal entry creation for accounting records
- Period closing procedures

## 4. Technical Requirements

### 4.1 Technology Stack
#### 4.1.1 Core Technologies
- **Programming Language:** Python 3.10+
- **UI Framework:** PySide6 (Qt for Python)
- **Database:** PostgreSQL 14+
- **ORM:** SQLAlchemy 2.0+
- **Build and Packaging:** PyInstaller

#### 4.1.2 Key Libraries and Dependencies
- **Database Access:** `psycopg2`, `alembic` (migrations)
- **UI Components:** Qt Material or custom theme
- **Data Visualization:** `matplotlib`, `seaborn`
- **Report Generation:** `reportlab`, `weasyprint`
- **Networking:** `requests`, `aiohttp`
- **Internationalization:** `gettext`
- **Testing:** `pytest`, `pytest-qt`
- **Logging:** Python standard `logging` module
- **Async Processing:** `asyncio`, `QThreadPool`
- **Data Validation:** `pydantic`
- **Error Handling:** Result pattern implementation

### 4.2 System Architecture
The SG POS System follows a layered architecture pattern with clear separation of concerns.

#### 4.2.1 Architectural Layers
- **Presentation Layer (UI)**
  - Responsible for user interface rendering and interaction
  - Delegates all business logic to lower layers
  - Implements reactive UI pattern using Qt signals and slots
- **Business Logic Layer**
  - Implements core application logic and workflows
  - Coordinates between services
  - Enforces business rules and validation
  - Implements manager classes for each functional domain
- **Data Access Layer**
  - Provides services for database operations
  - Abstracts database interaction details
  - Implements repository pattern for data access
  - Handles data mapping between persistence and domain models
- **Persistence Layer**
  - ORM models representing database schema
  - Database migration scripts
  - SQL scripts for complex queries or functions

#### 4.2.2 Cross-Cutting Concerns
- **Security:** Authentication, authorization, encryption
- **Logging:** Application events, errors, audit trails
- **Configuration:** Environment-specific settings management
- **Error Handling:** Consistent exception handling and reporting
- **Internationalization:** Multi-language support

### 4.3 Database Schema Design

#### 4.3.1 Core Entities and Relationships
*A visual ERD would be provided here. The tables below describe the schema.*

#### 4.3.2 Tables and Relationships

**Users**
- `user_id` (PK)
- `username`, `password_hash`, `full_name`, `email`, `phone`
- `role_id` (FK to Roles)
- `is_active`, `last_login`, `created_at`, `updated_at`

**Roles**
- `role_id` (PK)
- `name`, `description`, `created_at`, `updated_at`

**Permissions**
- `permission_id` (PK)
- `name`, `description`, `resource`, `action`, `created_at`, `updated_at`

**RolePermissions** (Junction table)
- `role_id` (PK, FK to Roles)
- `permission_id` (PK, FK to Permissions)
- `created_at`

**Products**
- `product_id` (PK)
- `sku`, `barcode`, `name`, `description`
- `category_id` (FK to Categories)
- `cost_price`, `selling_price`
- `tax_rate_id` (FK to TaxRates)
- `is_active`, `created_by` (FK to Users), `created_at`, `updated_at`

**ProductAttributes**
- `attribute_id` (PK)
- `product_id` (FK to Products)
- `name`, `value`, `created_at`, `updated_at`

**Categories**
- `category_id` (PK)
- `name`, `description`
- `parent_id` (FK to Categories, self-reference)
- `is_active`, `created_at`, `updated_at`

**Inventory**
- `inventory_id` (PK)
- `product_id` (FK to Products), `location_id` (FK to Locations)
- `quantity`, `reorder_level`, `reorder_quantity`, `last_counted_at`
- `created_at`, `updated_at`

**InventoryTransactions**
- `transaction_id` (PK)
- `product_id` (FK to Products), `location_id` (FK to Locations)
- `quantity`, `transaction_type` (enum), `reference_id`, `note`
- `user_id` (FK to Users), `created_at`

... *(and so on for all other tables: Locations, Suppliers, PurchaseOrders, PurchaseOrderItems, Customers, Sales, SaleItems, Payments, PaymentMethods, TaxRates, Currencies, Shifts, AuditLog, Settings)*

#### 4.3.3 Constraints and Indexes
- **Primary Keys:** Defined for all tables
- **Foreign Keys:** Enforcing referential integrity
- **Unique Constraints:**
  - `username` in Users table
  - `sku` and `barcode` in Products table
  - `email` in Customers table (if not null)
  - `category` + `key` in Settings table
- **Check Constraints:**
  - Positive quantities in Inventory
  - Valid email formats
  - Valid phone number formats
- **Indexes:**
  - Foreign key columns
  - Search columns (product name, customer name, etc.)
  - Date columns used in reporting
  - Status columns for filtering

### 4.4 Codebase File Hierarchy
```plaintext
sg_pos/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── config.py
│   ├── constants.py
│   ├── core/
│   ├── models/
│   ├── services/
│   ├── business_logic/
│   ├── accounting/
│   ├── ui/
│   │   ├── main_window.py
│   │   ├── styles/
│   │   ├── widgets/
│   │   ├── dialogs/
│   │   └── models/
│   └── utils/
├── tests/
├── scripts/
├── resources/
│   ├── icons/
│   ├── images/
│   ├── templates/
│   ├── sql/
│   └── i18n/
├── docs/
├── migrations/
├── logs/
├── data/
├── .gitignore
├── README.md
├── requirements.txt
├── requirements-dev.txt
├── setup.py
└── pyproject.toml
```

### 4.5 Key Application Modules and Files

#### 4.5.1 Core Module
**app/core/application.py**
```python
class ApplicationCore:
    """
    Central dependency provider and application entry point.
    Implements lazy initialization of all managers and services.
    """
    def __init__(self, config_path=None):
        # ...
    def initialize(self, config_path=None):
        # ...
    @property
    def db_service(self):
        # ...
    @property
    def user_manager(self):
        # ...
```
**app/core/result.py**
```python
class Result:
    """
    Represents the result of an operation that might fail.
    Used instead of exceptions for expected error conditions.
    """
    def __init__(self, success=True, value=None, error=None):
        # ...
    @classmethod
    def ok(cls, value=None):
        # ...
    @classmethod
    def fail(cls, error):
        # ...
```

#### 4.5.2 Database Models
**app/models/base.py**
```python
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class BaseModel(Base):
    """Base model with common fields and methods"""
    __abstract__ = True
    # ...
```
**app/models/user.py**
```python
from sqlalchemy import Column, Integer, String, Boolean, ForeignKey
from sqlalchemy.orm import relationship
from app.models.base import BaseModel

class User(BaseModel):
    """User model representing system users"""
    __tablename__ = 'users'
    
    user_id = Column(Integer, primary_key=True)
    # ...
```

#### 4.5.3 Services
**app/services/database.py**
```python
class DatabaseService:
    """Manages database connections and session handling."""
    def __init__(self, config):
        # ...
    @contextmanager
    def session(self):
        # ...
```
**app/services/user_service.py**
```python
class UserService:
    """Service for user-related database operations."""
    def __init__(self, db_service):
        # ...
    def authenticate(self, username, password):
        # ...
```

#### 4.5.4 Business Logic
**app/business_logic/user_manager.py**
```python
class UserManager:
    """Manages user-related business logic and workflows."""
    def __init__(self, app_core):
        # ...
    async def login(self, username, password):
        # ...
```

#### 4.5.5 UI Components
**app/ui/main_window.py**
```python
from PySide6.QtWidgets import QMainWindow, QStackedWidget

class MainWindow(QMainWindow):
    """Main application window that manages the UI workflow."""
    def __init__(self, app_core):
        # ...
    @Slot(object)
    def on_login_successful(self, user):
        # ...
```
**app/ui/widgets/pos_widget.py**
```python
from PySide6.QtWidgets import QWidget

class POSWidget(QWidget):
    """Point of Sale interface widget."""
    def __init__(self, app_core):
        # ...
    @Slot()
    def on_new_sale(self):
        # ...
    @Slot()
    def on_payment(self):
        # ...
```

### 4.6 Application Modules and User Interaction Diagram
```plaintext
┌───────────────────────────────────────────────────────────────────┐
│                        UI Layer (PySide6)                         │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌──────┐  │
│  │LoginWidget  │   │DashboardW.  │   │POSWidget    │   │Other │  │
│  └─────┬───────┘   └──────┬──────┘   └──────┬──────┘   │UIs   │  │
└────────┼──────────────────┼──────────────────┼─────────────────────┘
         │                  │                  │
         ▼                  ▼                  ▼
┌────────────────────────────────────────────────────────────────────┐
│                    Application Core (Dependency Provider)          │
└───────────┬────────────────┬─────────────────┬─────────────────────┘
            │                │                 │
            ▼                ▼                 ▼
┌───────────────────┐ ┌──────────────────┐ ┌──────────────────────┐
│ Business Logic    │ │ Business Logic   │ │ Business Logic       │
│ (UserManager)     │ │ (SalesManager)   │ │ (Other Managers)     │
└─────────┬─────────┘ └────────┬─────────┘ └───────────┬──────────┘
          │                    │                       │
          ▼                    ▼                       ▼
┌───────────────────┐ ┌──────────────────┐ ┌──────────────────────┐
│ Data Services     │ │ Data Services    │ │ Data Services        │
│ (UserService)     │ │ (SalesService)   │ │ (Other Services)     │
└─────────┬─────────┘ └────────┬─────────┘ └───────────┬──────────┘
          │                    │                       │
          ▼                    ▼                       ▼
┌────────────────────────────────────────────────────────────────────┐
│                 Database Layer (PostgreSQL via SQLAlchemy)         │
└────────────────────────────────────────────────────────────────────┘
```

## 5. Development Environment Setup
### 5.1 Prerequisites
- Python 3.10+
- PostgreSQL 14+
- Git
- `pipenv` or `virtualenv`
- VSCode or PyCharm

### 5.2 Installation Steps
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-org/sg-pos.git
    cd sg-pos
    ```
2.  **Set up a virtual environment:**
    ```bash
    python -m venv venv
    # On Windows: venv\Scripts\activate
    # On macOS/Linux: source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements-dev.txt
    ```
4.  **Set up PostgreSQL:**
    ```sql
    CREATE DATABASE sg_pos_dev;
    CREATE USER sg_pos_user WITH PASSWORD 'your_password';
    GRANT ALL PRIVILEGES ON DATABASE sg_pos_dev TO sg_pos_user;
    ```
5.  **Initialize the database:**
    ```bash
    python -m scripts.setup_db --config config/development.json
    ```
6.  **Run the application:**
    ```bash
    python -m app.main
    ```

### 5.3 Development Tools
- **Code Linting:** Flake8, Black, isort
- **Testing:** pytest, pytest-qt, Coverage.py
- **Database Migration:** Alembic
- **Documentation:** Sphinx, Markdown
- **Code Quality:** SonarQube, GitHub Actions (CI/CD)

## 6. Production Environment Setup
*Details for server setup, including software requirements, deployment steps, Supervisor configuration, backup scripts, and security hardening.*

## 7. Non-Functional Requirements
### 7.1 Performance Requirements
- **Response Time:** UI operations < 100ms, DB queries < 500ms.
- **Throughput:** Support 1000+ transactions/day, 10+ concurrent users.
- **Resource Utilization:** CPU < 70%, Memory < 2GB during normal operations.

### 7.2 Security Requirements
- **Authentication:** RBAC, strong passwords, session timeout, audit logs.
- **Data Protection:** Encryption at rest, PDPA compliance.
- **System Security:** Regular patches, firewall, vulnerability protection.

### 7.3 Reliability Requirements
- **Availability:** Available during business hours.
- **Fault Tolerance:** Graceful degradation, no data loss on crash.
- **Backup and Recovery:** Daily automated backups, RPO of 24 hours.

### 7.4 Usability Requirements
- **User Interface:** Consistent, responsive, accessible design.
- **Learnability:** Intuitive workflow, context-sensitive help.
- **Efficiency:** Keyboard shortcuts, batch operations.

### 7.5 Maintainability Requirements
- **Code Quality:** High test coverage, documented, modular architecture.
- **Extensibility:** Plugin architecture, clear extension points.

---

## 8. Conclusion
The SG Point-of-Sale (POS) System is designed to be a comprehensive, robust, and user-friendly solution for small to medium-sized businesses in Singapore. By leveraging modern technologies and adhering to best practices in software development, the system will provide a scalable and maintainable platform that can grow with the business. This PRD provides a detailed blueprint for development, ensuring all stakeholders have a shared understanding of the project goals and expectations.
