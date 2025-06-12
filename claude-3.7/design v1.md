Product Requirements Document (PRD): SG Point-of-Sale (POS) System
Version: 1.0
Date: June 12, 2025
Author: Technical Design Team

Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) in Singapore. Built with Python and leveraging PySide6 for the user interface and PostgreSQL for data management, this solution provides a robust, feature-rich retail management platform that addresses the unique regulatory and business requirements of the Singaporean market.

The system will support all essential retail operations including sales processing, inventory management, customer relationship management, employee management, reporting, and accounting, with special attention to Singapore-specific requirements such as GST compliance, multi-currency support, and integration with local payment methods. The architecture emphasizes reliability, security, and extensibility, allowing businesses to scale their operations without needing to migrate to a different platform.

This PRD outlines the complete requirements, technical specifications, and implementation details for the development team to deliver a production-ready application that meets the highest standards of software quality and user experience.

1. Introduction
1.1 Purpose
This document outlines the comprehensive requirements for the SG Point-of-Sale (POS) System, a specialized retail management solution for Singapore's SMB market. It serves as the authoritative reference for all development activities, establishing clear expectations for functionality, architecture, and quality.

1.2 Scope
The SG POS System encompasses all core retail operations needed by SMBs in Singapore, from basic sales transactions to advanced inventory management, customer tracking, employee management, and financial reporting. The system is designed as a desktop application that operates independently of internet connectivity for core functions while supporting cloud-based features when online.

1.3 Target Users
Retail Store Owners/Managers: Decision-makers who need comprehensive visibility into business operations
Sales Associates: Front-line staff handling customer transactions and inquiries
Inventory Managers: Staff responsible for stock management and procurement
Accountants/Bookkeepers: Financial professionals managing business accounts and tax compliance
IT Administrators: Technical staff responsible for system maintenance and configuration
1.4 Business Context
Singapore's retail sector is characterized by:

Strict regulatory compliance requirements, particularly around GST
High degree of digitalization and adoption of electronic payments
Multicultural customer base requiring multilingual support
Significant tourism driving the need for multi-currency capabilities
Competitive market requiring robust loyalty and promotion features
2. Product Overview
2.1 Product Vision
To provide Singapore's SMBs with a comprehensive, compliant, and user-friendly point-of-sale solution that streamlines operations, enhances customer experiences, and provides actionable business insights while meeting all local regulatory requirements.

2.2 Key Features
Sales Processing

Intuitive transaction interface optimized for speed and accuracy
Support for multiple payment methods including cash, cards, QR payments, and mobile wallets
Return and exchange processing with configurable policies
Inventory Management

Real-time stock tracking across multiple locations
Automated reorder notifications
Batch tracking and expiration date management
Stock transfers between locations
Customer Management

Comprehensive customer profiles with purchase history
Tiered loyalty programs with points and rewards
Customer communications via SMS and email
Employee Management

Role-based access control with detailed permissions
Time tracking and shift management
Sales performance tracking and commissions
Reporting and Analytics

Customizable dashboard with key performance indicators
Detailed sales, inventory, and financial reports
Export capabilities to common formats (Excel, PDF, CSV)
Financial Management

GST tracking and reporting compliant with IRAS requirements
Multi-currency support with real-time exchange rates
Integration with popular accounting software
Singapore-Specific Features

GST implementation following Singapore tax regulations
Support for Singapore-specific payment methods (NETS, PayNow, etc.)
Compliance with local data protection requirements (PDPA)
3. Functional Requirements
3.1 User Management
3.1.1 User Authentication and Authorization
Secure login system with multi-factor authentication option
Role-based access control with granular permissions
Password policies compliant with Singapore's cybersecurity guidelines
Session management with automatic timeout for security
Audit logging of all authentication events
3.1.2 User Roles and Permissions
Role	Description	Default Permissions
Administrator	System-wide access	All permissions
Manager	Store management	Sales, inventory, reporting, limited settings
Cashier	Front-line sales	Sales processing, basic customer management
Inventory Clerk	Stock management	Inventory viewing and adjustment
Accountant	Financial operations	Financial reports, end-of-day reconciliation
3.1.3 User Profile Management
Personal information management (name, contact, etc.)
Individual settings and preferences
Activity history and statistics
Password reset and account recovery mechanisms
3.2 Product Management
3.2.1 Product Catalog
Hierarchical category management
Comprehensive product attributes (name, description, images, etc.)
Multiple SKU support for variants (size, color, etc.)
Custom fields for additional product information
Product import/export via CSV and Excel
3.2.2 Pricing Management
Base price and cost tracking
Multiple price levels (retail, wholesale, special)
Time-based promotional pricing
Quantity-based pricing (bulk discounts)
Margin and markup calculations
3.2.3 Barcode Management
Support for multiple barcode formats (UPC, EAN, QR, etc.)
Barcode generation for internal products
Batch barcode printing
3.3 Inventory Management
3.3.1 Stock Tracking
Real-time inventory levels across locations
Minimum stock level alerts
Stock movement history
Variance tracking and reconciliation
3.3.2 Procurement
Purchase order creation and management
Supplier management with contact information and terms
Receiving and partial receiving workflows
Cost tracking and updates
3.3.3 Inventory Adjustments
Reason-based adjustment tracking
Bulk adjustment capabilities
Scheduled physical inventory counts
Shrinkage analysis and reporting
3.4 Sales Processing
3.4.1 Point of Sale Interface
Touch-optimized interface for efficient transactions
Product lookup by name, SKU, barcode, or category
Customer association with transactions
Discount application (percentage, fixed amount, etc.)
Tax calculation and display
Line item editing and removal
3.4.2 Payment Processing
Support for multiple payment methods in a single transaction
Change calculation for cash payments
Integration with payment terminals (credit/debit cards)
QR code payments (PayNow, NETS QR, etc.)
Payment splitting between methods
Foreign currency handling with exchange rate management
3.4.3 Receipt Management
Customizable receipt templates
Digital receipt option (email, SMS)
Receipt reprinting and retrieval
Inclusion of promotional messages and return policies
3.4.4 Returns and Exchanges
Original transaction lookup
Partial and full return processing
Reason tracking for returns
Exchange processing with balance calculation
Return policy enforcement (time limits, condition, etc.)
3.5 Customer Management
3.5.1 Customer Profiles
Basic information (name, contact details, preferences)
Purchase history and statistics
Account balance for store credit or prepayments
Notes and custom fields
PDPA compliance for data collection and usage
3.5.2 Loyalty Program
Points accumulation based on purchase amount
Tiered membership levels with benefits
Points redemption for discounts or products
Expiration management for points
Birthday rewards and special promotions
3.5.3 Customer Communications
Targeted promotions based on purchase history
Birthday and anniversary messages
Receipt and transaction notifications
Marketing campaign management
Opt-in/opt-out management for PDPA compliance
3.6 Reporting and Analytics
3.6.1 Sales Reports
Daily, weekly, monthly, and annual sales summaries
Sales by product, category, employee, time period
Comparative analysis (current vs. previous periods)
Tax collection reports
Payment method distribution
3.6.2 Inventory Reports
Current stock levels and valuation
Slow-moving and fast-moving items
Stockout frequency and duration
Shrinkage and loss reports
Product performance analysis
3.6.3 Financial Reports
Profit and loss statements
Cost of goods sold
Margin analysis
GST reports for IRAS filing
Cash flow reports
3.6.4 Customer Reports
Customer purchase frequency and value
Loyalty program participation and redemption
Customer acquisition and retention metrics
Demographic analysis (where applicable)
3.7 Financial Management
3.7.1 Cash Management
Cash drawer tracking and reconciliation
Bank deposit preparation and recording
Petty cash management
Over/short tracking and analysis
3.7.2 Tax Management
Automatic GST calculation based on product categories
GST-inclusive and GST-exclusive price management
GST reporting in compliance with IRAS requirements
Support for GST-registered and non-registered businesses
3.7.3 Accounting Integration
Export of financial data to common accounting systems
Chart of accounts mapping
Journal entry creation for accounting records
Period closing procedures
4. Technical Requirements
4.1 Technology Stack
4.1.1 Core Technologies
Programming Language: Python 3.10+
UI Framework: PySide6 (Qt for Python)
Database: PostgreSQL 14+
ORM: SQLAlchemy 2.0+
Build and Packaging: PyInstaller
4.1.2 Key Libraries and Dependencies
Database Access: psycopg2, alembic (migrations)
UI Components: Qt Material or custom theme
Data Visualization: matplotlib, seaborn
Report Generation: reportlab, weasyprint
Networking: requests, aiohttp
Internationalization: gettext
Testing: pytest, pytest-qt
Logging: Python standard logging module
Async Processing: asyncio, QThreadPool
Data Validation: pydantic
Error Handling: Result pattern implementation
4.2 System Architecture
The SG POS System follows a layered architecture pattern with clear separation of concerns:

4.2.1 Architectural Layers
Presentation Layer (UI)

Responsible for user interface rendering and interaction
Delegates all business logic to lower layers
Implements reactive UI pattern using Qt signals and slots
Business Logic Layer

Implements core application logic and workflows
Coordinates between services
Enforces business rules and validation
Implements manager classes for each functional domain
Data Access Layer

Provides services for database operations
Abstracts database interaction details
Implements repository pattern for data access
Handles data mapping between persistence and domain models
Persistence Layer

ORM models representing database schema
Database migration scripts
SQL scripts for complex queries or functions
4.2.2 Cross-Cutting Concerns
Security: Authentication, authorization, encryption
Logging: Application events, errors, audit trails
Configuration: Environment-specific settings management
Error Handling: Consistent exception handling and reporting
Internationalization: Multi-language support
4.3 Database Schema Design
4.3.1 Core Entities and Relationships


4.3.2 Tables and Relationships
Users

user_id (PK)
username
password_hash
full_name
email
phone
role_id (FK to Roles)
is_active
last_login
created_at
updated_at
Roles

role_id (PK)
name
description
created_at
updated_at
Permissions

permission_id (PK)
name
description
resource
action
created_at
updated_at
RolePermissions (Junction table)

role_id (PK, FK to Roles)
permission_id (PK, FK to Permissions)
created_at
Products

product_id (PK)
sku
barcode
name
description
category_id (FK to Categories)
cost_price
selling_price
tax_rate_id (FK to TaxRates)
is_active
created_by (FK to Users)
created_at
updated_at
ProductAttributes

attribute_id (PK)
product_id (FK to Products)
name
value
created_at
updated_at
Categories

category_id (PK)
name
description
parent_id (FK to Categories, self-reference)
is_active
created_at
updated_at
Inventory

inventory_id (PK)
product_id (FK to Products)
location_id (FK to Locations)
quantity
reorder_level
reorder_quantity
last_counted_at
created_at
updated_at
InventoryTransactions

transaction_id (PK)
product_id (FK to Products)
location_id (FK to Locations)
quantity
transaction_type (enum: purchase, sale, adjustment, transfer)
reference_id (sale_id, purchase_id, etc.)
note
user_id (FK to Users)
created_at
Locations

location_id (PK)
name
address
is_active
created_at
updated_at
Suppliers

supplier_id (PK)
name
contact_person
email
phone
address
tax_registration_no
is_active
created_at
updated_at
PurchaseOrders

po_id (PK)
supplier_id (FK to Suppliers)
order_date
expected_date
status (enum: draft, ordered, partial, received, cancelled)
subtotal
tax_amount
total_amount
notes
created_by (FK to Users)
created_at
updated_at
PurchaseOrderItems

po_item_id (PK)
po_id (FK to PurchaseOrders)
product_id (FK to Products)
quantity_ordered
quantity_received
unit_cost
line_total
created_at
updated_at
Customers

customer_id (PK)
name
email
phone
address
loyalty_points
membership_level
tax_exemption_no
created_at
updated_at
Sales

sale_id (PK)
customer_id (FK to Customers, nullable)
user_id (FK to Users)
sale_date
status (enum: completed, voided, returned)
subtotal
tax_amount
discount_amount
total_amount
notes
created_at
updated_at
SaleItems

sale_item_id (PK)
sale_id (FK to Sales)
product_id (FK to Products)
quantity
unit_price
discount_amount
tax_amount
line_total
created_at
updated_at
Payments

payment_id (PK)
sale_id (FK to Sales)
payment_method_id (FK to PaymentMethods)
amount
reference_no
status (enum: completed, pending, failed)
created_at
updated_at
PaymentMethods

method_id (PK)
name
is_cash
is_active
created_at
updated_at
TaxRates

tax_rate_id (PK)
name
rate
is_default
created_at
updated_at
Currencies

currency_id (PK)
code
name
symbol
exchange_rate (to base currency)
is_base
is_active
last_updated
created_at
updated_at
Shifts

shift_id (PK)
user_id (FK to Users)
location_id (FK to Locations)
start_time
end_time
opening_amount
closing_amount
status (enum: active, closed)
notes
created_at
updated_at
AuditLog

log_id (PK)
user_id (FK to Users)
action
table_name
record_id
old_values
new_values
ip_address
created_at
Settings

setting_id (PK)
category
key
value
data_type
description
created_at
updated_at
4.3.3 Constraints and Indexes
Primary Keys: Defined for all tables
Foreign Keys: Enforcing referential integrity
Unique Constraints:
Username in Users table
SKU and barcode in Products table
Email in Customers table (if not null)
Category + key in Settings table
Check Constraints:
Positive quantities in Inventory
Valid email formats
Valid phone number formats
Indexes:
Foreign key columns
Search columns (product name, customer name, etc.)
Date columns used in reporting
Status columns for filtering
4.4 Codebase File Hierarchy
sg_pos/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── config.py
│   ├── constants.py
│   ├── core/
│   │   ├── __init__.py
│   │   ├── application.py          # ApplicationCore class, central dependency provider
│   │   ├── exceptions.py           # Custom exception classes
│   │   └── result.py               # Result pattern implementation
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                 # Base model classes and mixins
│   │   ├── user.py                 # User and permission models
│   │   ├── product.py              # Product, category, and attribute models
│   │   ├── inventory.py            # Inventory and stock movement models
│   │   ├── customer.py             # Customer and loyalty models
│   │   ├── sale.py                 # Sale and sale item models
│   │   ├── payment.py              # Payment and payment method models
│   │   ├── purchase.py             # Purchase order models
│   │   ├── supplier.py             # Supplier models
│   │   ├── tax.py                  # Tax rate models
│   │   ├── currency.py             # Currency and exchange rate models
│   │   ├── shift.py                # Shift and cash management models
│   │   ├── audit.py                # Audit log models
│   │   └── settings.py             # System settings models
│   ├── services/
│   │   ├── __init__.py
│   │   ├── database.py             # Database connection and session management
│   │   ├── user_service.py         # User and authentication services
│   │   ├── product_service.py      # Product and category data services
│   │   ├── inventory_service.py    # Inventory data services
│   │   ├── customer_service.py     # Customer data services
│   │   ├── sales_service.py        # Sales data services
│   │   ├── payment_service.py      # Payment processing services
│   │   ├── purchase_service.py     # Purchase order services
│   │   ├── supplier_service.py     # Supplier data services
│   │   ├── tax_service.py          # Tax calculation and reporting services
│   │   ├── currency_service.py     # Currency and exchange rate services
│   │   ├── shift_service.py        # Shift management services
│   │   ├── audit_service.py        # Audit logging services
│   │   ├── settings_service.py     # System settings services
│   │   ├── report_service.py       # Reporting and data export services
│   │   └── backup_service.py       # Backup and restore services
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── user_manager.py         # User and permission management
│   │   ├── product_manager.py      # Product and category management
│   │   ├── inventory_manager.py    # Inventory management
│   │   ├── customer_manager.py     # Customer and loyalty management
│   │   ├── sales_manager.py        # Sales processing and management
│   │   ├── payment_manager.py      # Payment processing
│   │   ├── purchase_manager.py     # Purchase order management
│   │   ├── supplier_manager.py     # Supplier management
│   │   ├── shift_manager.py        # Shift and cash management
│   │   └── report_manager.py       # Report generation and management
│   ├── accounting/
│   │   ├── __init__.py
│   │   ├── ledger.py               # General ledger implementation
│   │   ├── journal_entry.py        # Journal entry creation and management
│   │   ├── account.py              # Chart of accounts
│   │   ├── gst_manager.py          # GST tax management
│   │   └── reconciliation.py       # Account reconciliation
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py          # Main application window
│   │   ├── application.qss         # Stylesheet for the application
│   │   ├── styles/
│   │   │   ├── __init__.py
│   │   │   ├── colors.py           # Color definitions
│   │   │   ├── fonts.py            # Font definitions
│   │   │   └── theme.py            # Theme management
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── login_widget.py     # Login screen
│   │   │   ├── dashboard_widget.py # Main dashboard
│   │   │   ├── pos_widget.py       # Point of sale interface
│   │   │   ├── inventory_widget.py # Inventory management
│   │   │   ├── customers_widget.py # Customer management
│   │   │   ├── reports_widget.py   # Reporting interface
│   │   │   ├── settings_widget.py  # Settings configuration
│   │   │   └── ...
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── message_dialog.py   # Custom message dialogs
│   │   │   ├── product_dialog.py   # Product editing
│   │   │   ├── customer_dialog.py  # Customer editing
│   │   │   ├── payment_dialog.py   # Payment processing
│   │   │   ├── user_dialog.py      # User management
│   │   │   └── ...
│   │   └── models/
│   │       ├── __init__.py
│   │       ├── table_models.py     # Qt table models
│   │       ├── list_models.py      # Qt list models
│   │       └── ...
│   └── utils/
│       ├── __init__.py
│       ├── validators.py           # Input validation helpers
│       ├── formatters.py           # Data formatting utilities
│       ├── exporters.py            # Data export utilities
│       ├── importers.py            # Data import utilities
│       ├── pdf_generator.py        # PDF generation utilities
│       ├── barcode_generator.py    # Barcode generation
│       ├── async_utils.py          # Async processing utilities
│       └── date_utils.py           # Date and time utilities
├── tests/
│   ├── __init__.py
│   ├── conftest.py                 # Test configuration and fixtures
│   ├── test_models/
│   ├── test_services/
│   ├── test_business_logic/
│   ├── test_accounting/
│   └── test_ui/
├── scripts/
│   ├── __init__.py
│   ├── setup_db.py                 # Database initialization
│   ├── generate_sample_data.py     # Test data generation
│   ├── backup_db.py                # Database backup utility
│   └── restore_db.py               # Database restore utility
├── resources/
│   ├── icons/                      # Application icons
│   ├── images/                     # UI images
│   ├── templates/                  # Report templates
│   ├── sql/                        # SQL scripts
│   │   ├── schema.sql              # Full database schema
│   │   ├── functions.sql           # PostgreSQL functions
│   │   ├── triggers.sql            # Database triggers
│   │   └── views.sql               # Database views
│   └── i18n/                       # Internationalization files
├── docs/
│   ├── api/                        # API documentation
│   ├── user_manual/                # End-user documentation
│   └── developer_guide/            # Developer documentation
├── migrations/
│   ├── __init__.py
│   ├── env.py                      # Alembic environment
│   └── versions/                   # Database migration scripts
├── logs/                           # Application logs directory
├── data/                           # Application data directory
├── .gitignore
├── README.md
├── requirements.txt                # Production dependencies
├── requirements-dev.txt            # Development dependencies
├── setup.py                        # Package installation script
└── pyproject.toml                  # Python project configuration
4.5 Key Application Modules and Files
4.5.1 Core Module
app/core/application.py

class ApplicationCore:
    """
    Central dependency provider and application entry point.
    Implements lazy initialization of all managers and services.
    """
    
    def __init__(self, config_path=None):
        self._config = None
        self._db_service = None
        self._user_manager = None
        self._product_manager = None
        # ... other managers
        
        self.initialize(config_path)
    
    def initialize(self, config_path=None):
        """Initialize core application components"""
        self._config = self._load_config(config_path)
        self._setup_logging()
        
    @property
    def db_service(self):
        """Lazy initialization of database service"""
        if self._db_service is None:
            from app.services.database import DatabaseService
            self._db_service = DatabaseService(self.config)
        return self._db_service
    
    @property
    def user_manager(self):
        """Lazy initialization of user manager"""
        if self._user_manager is None:
            from app.business_logic.user_manager import UserManager
            self._user_manager = UserManager(self)
        return self._user_manager
    
    # Additional properties for other managers...

app/core/result.py

class Result:
    """
    Represents the result of an operation that might fail.
    Used instead of exceptions for expected error conditions.
    """
    
    def __init__(self, success=True, value=None, error=None):
        self.success = success
        self.value = value
        self.error = error
    
    @classmethod
    def ok(cls, value=None):
        """Create a successful result with an optional value"""
        return cls(success=True, value=value)
    
    @classmethod
    def fail(cls, error):
        """Create a failed result with an error message"""
        return cls(success=False, error=error)
    
    def __bool__(self):
        """Allow using the result in boolean contexts"""
        return self.success

4.5.2 Database Models
app/models/base.py

from sqlalchemy import Column, Integer, DateTime, func
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class BaseModel(Base):
    """Base model with common fields and methods"""
    __abstract__ = True
    
    created_at = Column(DateTime, default=func.now(), nullable=False)
    updated_at = Column(DateTime, default=func.now(), onupdate=func.now(), nullable=False)

app/models/user.py

from sqlalchemy import Column, Integer, String, Boolean, ForeignKey, DateTime
from sqlalchemy.orm import relationship

from app.models.base import BaseModel

class User(BaseModel):
    """User model representing system users"""
    __tablename__ = 'users'
    
    user_id = Column(Integer, primary_key=True)
    username = Column(String(50), unique=True, nullable=False)
    password_hash = Column(String(256), nullable=False)
    full_name = Column(String(100), nullable=False)
    email = Column(String(100), nullable=True)
    phone = Column(String(20), nullable=True)
    role_id = Column(Integer, ForeignKey('roles.role_id'), nullable=False)
    is_active = Column(Boolean, default=True, nullable=False)
    last_login = Column(DateTime, nullable=True)
    
    # Relationships
    role = relationship("Role", back_populates="users")
    
    def __repr__(self):
        return f"<User(username='{self.username}', full_name='{self.full_name}')>"

4.5.3 Services
app/services/database.py

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, scoped_session
from contextlib import contextmanager

class DatabaseService:
    """
    Manages database connections and session handling.
    """
    
    def __init__(self, config):
        self.config = config
        self.engine = create_engine(self._get_connection_string())
        self.session_factory = sessionmaker(bind=self.engine)
        self.Session = scoped_session(self.session_factory)
    
    def _get_connection_string(self):
        """Build connection string from configuration"""
        db_config = self.config.database
        return f"postgresql://{db_config.user}:{db_config.password}@{db_config.host}:{db_config.port}/{db_config.name}"
    
    @contextmanager
    def session(self):
        """Provide a transactional scope around a series of operations."""
        session = self.Session()
        try:
            yield session
            session.commit()
        except Exception as e:
            session.rollback()
            raise
        finally:
            session.close()

app/services/user_service.py

import bcrypt
from sqlalchemy import select

from app.models.user import User
from app.models.role import Role
from app.core.result import Result

class UserService:
    """
    Service for user-related database operations.
    """
    
    def __init__(self, db_service):
        self.db_service = db_service
    
    def authenticate(self, username, password):
        """Authenticate a user by username and password"""
        with self.db_service.session() as session:
            stmt = select(User).where(User.username == username, User.is_active == True)
            user = session.execute(stmt).scalar_one_or_none()
            
            if not user:
                return Result.fail("Invalid username or password")
            
            if not self._verify_password(password, user.password_hash):
                return Result.fail("Invalid username or password")
            
            return Result.ok(user)
    
    def _verify_password(self, plain_password, password_hash):
        """Verify a password against a hash"""
        return bcrypt.checkpw(
            plain_password.encode('utf-8'),
            password_hash.encode('utf-8')
        )
    
    # Additional methods for user management...

4.5.4 Business Logic
app/business_logic/user_manager.py

from app.core.result import Result

class UserManager:
    """
    Manages user-related business logic and workflows.
    """
    
    def __init__(self, app_core):
        self.app_core = app_core
        self.user_service = None
        self.audit_service = None
    
    @property
    def _user_service(self):
        if self.user_service is None:
            from app.services.user_service import UserService
            self.user_service = UserService(self.app_core.db_service)
        return self.user_service
    
    @property
    def _audit_service(self):
        if self.audit_service is None:
            from app.services.audit_service import AuditService
            self.audit_service = AuditService(self.app_core.db_service)
        return self.audit_service
    
    async def login(self, username, password):
        """Process user login with audit logging"""
        result = self._user_service.authenticate(username, password)
        
        if result:
            user = result.value
            # Update last login timestamp
            login_result = self._user_service.update_last_login(user.user_id)
            if not login_result:
                return Result.fail("Failed to update login timestamp")
            
            # Log successful login
            self._audit_service.log_action(
                user_id=user.user_id,
                action="LOGIN",
                table_name="users",
                record_id=user.user_id
            )
            
            return Result.ok(user)
        else:
            # Log failed login attempt
            self._audit_service.log_action(
                user_id=None,
                action="LOGIN_FAILED",
                table_name="users",
                record_id=None,
                new_values={"username": username}
            )
            
            return result
    
    # Additional user management methods...

4.5.5 UI Components
app/ui/main_window.py

from PySide6.QtWidgets import QMainWindow, QStackedWidget, QMessageBox
from PySide6.QtCore import Slot, Signal

from app.ui.widgets.login_widget import LoginWidget
from app.ui.widgets.dashboard_widget import DashboardWidget
from app.ui.widgets.pos_widget import POSWidget
# ... other widget imports

class MainWindow(QMainWindow):
    """
    Main application window that manages the UI workflow.
    """
    
    def __init__(self, app_core):
        super().__init__()
        self.app_core = app_core
        self.current_user = None
        
        self.setWindowTitle("SG POS System")
        self.resize(1280, 800)
        
        self.stacked_widget = QStackedWidget()
        self.setCentralWidget(self.stacked_widget)
        
        self.login_widget = LoginWidget()
        self.dashboard_widget = DashboardWidget(self.app_core)
        self.pos_widget = POSWidget(self.app_core)
        # ... other widgets
        
        self.stacked_widget.addWidget(self.login_widget)
        self.stacked_widget.addWidget(self.dashboard_widget)
        self.stacked_widget.addWidget(self.pos_widget)
        # ... add other widgets
        
        # Connect signals
        self.login_widget.login_successful.connect(self.on_login_successful)
        self.dashboard_widget.pos_button_clicked.connect(self.show_pos)
        # ... other connections
        
        # Start with login screen
        self.stacked_widget.setCurrentWidget(self.login_widget)
    
    @Slot(object)
    def on_login_successful(self, user):
        """Handle successful login"""
        self.current_user = user
        self.dashboard_widget.set_user(user)
        self.pos_widget.set_user(user)
        # ... set user for other widgets
        
        self.stacked_widget.setCurrentWidget(self.dashboard_widget)
    
    @Slot()
    def show_pos(self):
        """Switch to POS widget"""
        self.stacked_widget.setCurrentWidget(self.pos_widget)
    
    # Additional UI management methods...

app/ui/widgets/pos_widget.py

from PySide6.QtWidgets import QWidget, QVBoxLayout, QHBoxLayout, QPushButton, QTableView
from PySide6.QtCore import Signal, Slot

from app.ui.models.table_models import SaleItemsTableModel
from app.ui.dialogs.payment_dialog import PaymentDialog

class POSWidget(QWidget):
    """
    Point of Sale interface widget.
    """
    
    def __init__(self, app_core):
        super().__init__()
        self.app_core = app_core
        self.current_user = None
        self.current_sale = None
        self.sale_items_model = SaleItemsTableModel()
        
        self.setup_ui()
    
    def setup_ui(self):
        """Initialize the UI components"""
        main_layout = QVBoxLayout(self)
        
        # Sale items table
        self.items_table = QTableView()
        self.items_table.setModel(self.sale_items_model)
        main_layout.addWidget(self.items_table)
        
        # Buttons layout
        buttons_layout = QHBoxLayout()
        
        self.new_sale_button = QPushButton("New Sale")
        self.payment_button = QPushButton("Payment")
        self.cancel_button = QPushButton("Cancel")
        
        buttons_layout.addWidget(self.new_sale_button)
        buttons_layout.addWidget(self.payment_button)
        buttons_layout.addWidget(self.cancel_button)
        
        main_layout.addLayout(buttons_layout)
        
        # Connect signals
        self.new_sale_button.clicked.connect(self.on_new_sale)
        self.payment_button.clicked.connect(self.on_payment)
        self.cancel_button.clicked.connect(self.on_cancel)
    
    def set_user(self, user):
        """Set the current user"""
        self.current_user = user
    
    @Slot()
    def on_new_sale(self):
        """Start a new sale"""
        self.current_sale = None  # Reset current sale
        self.sale_items_model.clear()
        # Initialize a new sale through business logic
        result = self.app_core.sales_manager.create_sale(self.current_user.user_id)
        if result:
            self.current_sale = result.value
        else:
            # Show error message
            pass
    
    @Slot()
    def on_payment(self):
        """Process payment for the current sale"""
        if not self.current_sale:
            return
        
        payment_dialog = PaymentDialog(self.app_core, self.current_sale)
        if payment_dialog.exec():
            # Payment successful, reset the sale
            self.current_sale = None
            self.sale_items_model.clear()
    
    @Slot()
    def on_cancel(self):
        """Cancel the current sale"""
        if not self.current_sale:
            return
        
        # Cancel the sale through business logic
        result = self.app_core.sales_manager.cancel_sale(self.current_sale.sale_id)
        if result:
            self.current_sale = None
            self.sale_items_model.clear()
        else:
            # Show error message
            pass
    
    # Additional POS functionality...

4.6 Application Modules and User Interaction Diagram
┌───────────────────────────────────────────────────────────────────┐
│                                                                   │
│                        UI Layer (PySide6)                         │
│                                                                   │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌──────┐  │
│  │LoginWidget  │   │DashboardW.  │   │POSWidget    │   │Other │  │
│  └─────┬───────┘   └──────┬──────┘   └──────┬──────┘   │UIs   │  │
│        │                  │                  │          └──────┘  │
└────────┼──────────────────┼──────────────────┼─────────────────────┘
         │                  │                  │
         ▼                  ▼                  ▼
┌────────────────────────────────────────────────────────────────────┐
│                                                                    │
│                    Application Core (Dependency Provider)          │
│                                                                    │
└───────────┬────────────────┬─────────────────┬─────────────────────┘
            │                │                 │
            ▼                ▼                 ▼
┌───────────────────┐ ┌──────────────────┐ ┌──────────────────────┐
│                   │ │                  │ │                      │
│ Business Logic    │ │ Business Logic   │ │ Business Logic       │
│ (UserManager)     │ │ (SalesManager)   │ │ (Other Managers)     │
│                   │ │                  │ │                      │
└─────────┬─────────┘ └────────┬─────────┘ └───────────┬──────────┘
          │                    │                       │
          ▼                    ▼                       ▼
┌───────────────────┐ ┌──────────────────┐ ┌──────────────────────┐
│                   │ │                  │ │                      │
│ Data Services     │ │ Data Services    │ │ Data Services        │
│ (UserService)     │ │ (SalesService)   │ │ (Other Services)     │
│                   │ │                  │ │                      │
└─────────┬─────────┘ └────────┬─────────┘ └───────────┬──────────┘
          │                    │                       │
          │                    │                       │
          ▼                    ▼                       ▼
┌────────────────────────────────────────────────────────────────────┐
│                                                                    │
│                 Database Layer (PostgreSQL via SQLAlchemy)         │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
5. Development Environment Setup
5.1 Prerequisites
Python 3.10+: Required for core application development
PostgreSQL 14+: Required for database server
Git: Required for version control
pipenv or virtualenv: Recommended for Python environment management
VSCode or PyCharm: Recommended IDEs with Python support
5.2 Installation Steps
Clone the repository:

git clone https://github.com/your-org/sg-pos.git
cd sg-pos

Set up a virtual environment:

python -m venv venv
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate

Install dependencies:

pip install -r requirements-dev.txt

Set up PostgreSQL:

Install PostgreSQL 14+ from postgresql.org
Create a new database:
CREATE DATABASE sg_pos_dev;
CREATE USER sg_pos_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE sg_pos_dev TO sg_pos_user;

Initialize the database:

# Run the database setup script
python -m scripts.setup_db --config config/development.json

Configure environment variables: Create a .env file in the project root:

DB_HOST=localhost
DB_PORT=5432
DB_NAME=sg_pos_dev
DB_USER=sg_pos_user
DB_PASSWORD=your_password
APP_SECRET_KEY=your_random_secret_key
DEBUG=True
Run the application:

python -m app.main

5.3 Development Tools
Code Linting:

Flake8 for Python style checking
Black for code formatting
isort for import sorting
Pre-commit hooks for automated checking
Testing:

pytest for unit and integration testing
pytest-qt for UI testing
Coverage.py for measuring test coverage
Database Migration:

Alembic for schema migrations
SQL scripts for initial schema creation
Documentation:

Sphinx for API documentation
Markdown for user and developer guides
Automated documentation builds
Code Quality:

SonarQube or similar for code quality monitoring
GitHub Actions for CI/CD pipeline
6. Production Environment Setup
6.1 Server Requirements
Operating System: Ubuntu 22.04 LTS or similar
CPU: 4+ cores (recommended)
RAM: 8GB+ (recommended)
Storage: 100GB+ SSD (depends on expected database size)
Network: Reliable internet connection for updates and external services
6.2 Software Requirements
Python 3.10+: Runtime environment
PostgreSQL 14+: Production database
Nginx: Web server for serving static files and SSL termination
Supervisor: Process control system for managing the application
UFW or similar: Firewall for securing the server
Fail2ban: Protection against brute force attacks
Certbot: SSL certificate management
6.3 Installation Steps
Server Preparation:

# Update system packages
sudo apt update && sudo apt upgrade -y

# Install required packages
sudo apt install -y python3 python3-pip python3-venv postgresql nginx supervisor ufw fail2ban certbot

Database Setup:

# Create production database and user
sudo -u postgres psql -c "CREATE DATABASE sg_pos_prod;"
sudo -u postgres psql -c "CREATE USER sg_pos_user WITH PASSWORD 'secure_password';"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE sg_pos_prod TO sg_pos_user;"

# Secure PostgreSQL
sudo nano /etc/postgresql/14/main/pg_hba.conf
# Set appropriate client authentication method

# Restart PostgreSQL
sudo systemctl restart postgresql

Application Deployment:

# Create application user
sudo useradd -m -s /bin/bash sg_pos_app

# Clone repository
sudo -u sg_pos_app git clone https://github.com/your-org/sg-pos.git /home/sg_pos_app/sg-pos

# Set up virtual environment
sudo -u sg_pos_app python3 -m venv /home/sg_pos_app/venv
sudo -u sg_pos_app /home/sg_pos_app/venv/bin/pip install -r /home/sg_pos_app/sg-pos/requirements.txt

# Create production configuration
sudo -u sg_pos_app cp /home/sg_pos_app/sg-pos/config/production.example.json /home/sg_pos_app/sg-pos/config/production.json
sudo -u sg_pos_app nano /home/sg_pos_app/sg-pos/config/production.json
# Edit configuration with appropriate settings

Supervisor Configuration:

# Create supervisor configuration
sudo nano /etc/supervisor/conf.d/sg-pos.conf
Add the following content:

[program:sg-pos]
command=/home/sg_pos_app/venv/bin/python -m app.main --config /home/sg_pos_app/sg-pos/config/production.json
directory=/home/sg_pos_app/sg-pos
user=sg_pos_app
autostart=true
autorestart=true
stderr_logfile=/var/log/sg-pos/err.log
stdout_logfile=/var/log/sg-pos/out.log
environment=PYTHONPATH="/home/sg_pos_app/sg-pos",PYTHONUNBUFFERED="1"
Create log directory and start the application:

sudo mkdir -p /var/log/sg-pos
sudo chown sg_pos_app:sg_pos_app /var/log/sg-pos

sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start sg-pos

Backup Configuration:

# Create backup script
sudo nano /home/sg_pos_app/backup.sh

Add the following content:

#!/bin/bash
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR=/home/sg_pos_app/backups

# Create backup directory if it doesn't exist
mkdir -p $BACKUP_DIR

# Backup database
pg_dump -U sg_pos_user -h localhost sg_pos_prod > $BACKUP_DIR/sg_pos_$TIMESTAMP.sql

# Compress backup
gzip $BACKUP_DIR/sg_pos_$TIMESTAMP.sql

# Remove backups older than 30 days
find $BACKUP_DIR -name "sg_pos_*.sql.gz" -mtime +30 -delete

Make the script executable and set up a cron job:

sudo chmod +x /home/sg_pos_app/backup.sh
sudo -u sg_pos_app crontab -e

Add the following line to run the backup daily at 2 AM:

0 2 * * * /home/sg_pos_app/backup.sh
Security Configuration:

# Configure firewall
sudo ufw allow 22/tcp  # SSH
sudo ufw allow 80/tcp  # HTTP
sudo ufw allow 443/tcp # HTTPS
sudo ufw enable

# Configure fail2ban
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
# Edit configuration as needed
sudo systemctl restart fail2ban

6.4 Monitoring and Maintenance
System Monitoring:

Setup Prometheus and Grafana for system metrics
Configure log rotation for application logs
Set up email alerts for critical errors
Application Updates:

# Pull latest changes
sudo -u sg_pos_app git -C /home/sg_pos_app/sg-pos pull

# Install updated dependencies
sudo -u sg_pos_app /home/sg_pos_app/venv/bin/pip install -r /home/sg_pos_app/sg-pos/requirements.txt

# Run database migrations
sudo -u sg_pos_app /home/sg_pos_app/venv/bin/python -m alembic upgrade head

# Restart application
sudo supervisorctl restart sg-pos

Backup Verification:

Regularly test database restores to ensure backup integrity
Implement off-site backup storage for disaster recovery
7. Non-Functional Requirements
7.1 Performance Requirements
Response Time:

UI operations should respond within 100ms
Database queries should complete within 500ms
Report generation should complete within 5 seconds for standard reports
Throughput:

The system should support at least 1000 transactions per day
Concurrent user support for up to 10 users
Resource Utilization:

CPU usage should not exceed 70% during normal operations
Memory usage should be kept under 2GB
Database size should be managed with archiving for historical data
7.2 Security Requirements
Authentication and Authorization:

Role-based access control for all functions
Strong password policies (minimum length, complexity)
Automatic logout after period of inactivity
Audit logging for security-related events
Data Protection:

Encryption of sensitive data at rest
Secure storage of payment information
Compliance with Singapore's PDPA regulations
Regular security assessments
System Security:

Regular updates and security patches
Network security controls
Protection against common vulnerabilities (SQL injection, XSS, etc.)
7.3 Reliability Requirements
Availability:

System should be available during all business hours
Planned maintenance should be scheduled outside business hours
Fault Tolerance:

Automatic recovery from common errors
Graceful degradation when components fail
No data loss during system crashes
Backup and Recovery:

Daily automated backups
Point-in-time recovery capability
Maximum data loss in case of failure: 24 hours
7.4 Usability Requirements
User Interface:

Consistent design across all screens
Responsive interface with minimal loading times
Accessibility features for users with disabilities
Support for both mouse and keyboard operation
Learnability:

Intuitive workflow requiring minimal training
Context-sensitive help throughout the application
Comprehensive user documentation
Efficiency:

Keyboard shortcuts for common operations
Configurable interface for experienced users
Batch operations for common tasks
7.5 Maintainability Requirements
Code Quality:

Comprehensive unit and integration tests
Documentation for all key components
Consistent coding standards
Modular architecture for easy replacement of components
Extensibility:

Plugin architecture for custom extensions
Clear extension points for future development
Backwards compatibility for custom extensions
8. Conclusion
The SG Point-of-Sale (POS) System is designed to be a comprehensive, robust, and user-friendly solution for small to medium-sized businesses in Singapore. By leveraging modern technologies and adhering to best practices in software development, the system will provide a scalable and maintainable platform that can grow with the business.

The layered architecture ensures clear separation of concerns, making the system easier to maintain and extend. The use of Python with PySide6 for the user interface and PostgreSQL for data management provides a solid foundation for building a reliable and performant application.

The comprehensive requirements outlined in this document provide a clear roadmap for development, ensuring that all stakeholders have a shared understanding of the project goals and expectations. By following these requirements, the development team will be able to deliver a high-quality product that meets the needs of Singapore's SMB retail sector.

This PRD provides a detailed blueprint for the development of the SG Point-of-Sale (POS) System. It covers all aspects of the project, from functional requirements to technical architecture, development environment setup, and production deployment. The document is designed to be comprehensive yet approachable,
