This is a comprehensive request for a Product Requirements Document (PRD) for a Singapore Point-of-Sale system. The user has provided clear architectural guidance and wants a detailed document covering database design, file hierarchy, technology stack, environment setup, and key modules. They've emphasized the need for layered architecture, dependency injection, asynchronous processing, and high code quality.
I need to structure this PRD to be both comprehensive and actionable, covering:

Business requirements and scope
Technical architecture details
Database schema design
File structure and modules
Technology stack specifications
Environment setup procedures
User interaction flows
Implementation considerations
The document should be detailed enough (6000+ words) to serve as a complete blueprint for development while incorporating the architectural principles they've outlined. </think>

Product Requirements Document: SG Point-of-Sale (POS) System
Table of Contents
Executive Summary
Product Overview
Technical Requirements
System Architecture
Database Design
Technology Stack
Development Environment Setup
Production Environment Setup
Application Modules
User Interface Design
Security Considerations
Performance Requirements
Testing Strategy
Deployment Strategy
Future Considerations
Executive Summary
The SG Point-of-Sale (POS) System is a comprehensive, cross-platform desktop application designed specifically for small to medium-sized businesses (SMBs) operating in Singapore's retail environment. This system addresses the unique regulatory, tax, and operational requirements of the Singapore market while providing a robust, scalable foundation for retail operations.

Built on a modern technology stack featuring Python, PySide6, and PostgreSQL, the application emphasizes clean architecture, maintainability, and professional-grade functionality. The system supports complex business workflows including inventory management, sales processing, customer relationship management, financial reporting, and compliance with Singapore's Goods and Services Tax (GST) regulations.

The application is architected with a layered approach, implementing industry best practices such as dependency injection, asynchronous processing, and comprehensive data integrity mechanisms. This design ensures scalability, maintainability, and the ability to adapt to evolving business requirements.

Product Overview
Vision Statement
To provide Singapore SMBs with a professional-grade POS solution that seamlessly integrates sales, inventory, customer management, and financial reporting while ensuring compliance with local regulations and supporting business growth.

Target Market
Small to medium-sized retail businesses in Singapore
Restaurants and food service establishments
Service-based businesses requiring point-of-sale functionality
Businesses requiring GST compliance and multi-currency support
Key Features
Sales Management: Complete transaction processing with multiple payment methods
Inventory Control: Real-time stock tracking, automatic reorder points, and supplier management
Customer Relationship Management: Customer profiles, purchase history, and loyalty programs
Financial Reporting: Comprehensive reporting suite with GST compliance
Multi-Currency Support: SGD primary with support for major international currencies
User Management: Role-based access control and audit trails
Offline Capability: Continued operation during network outages with synchronization
Integration Ready: APIs for third-party integrations and data export capabilities
Business Objectives
Reduce transaction processing time by 40%
Improve inventory accuracy to 99.5%
Ensure 100% GST compliance
Provide real-time financial insights
Support business scaling without system limitations
Technical Requirements
Functional Requirements
Core Sales Operations
Process point-of-sale transactions with multiple item types
Support various payment methods (cash, card, digital wallets)
Apply discounts, promotions, and tax calculations
Generate receipts and transaction records
Handle returns and exchanges with proper audit trails
Inventory Management
Track stock levels in real-time across multiple locations
Manage product variants (size, color, model)
Support barcode scanning and product lookup
Automate reorder notifications and purchase order generation
Handle stock adjustments and transfers
Customer Management
Maintain customer profiles with contact information
Track purchase history and preferences
Support loyalty programs and customer rewards
Manage customer credit accounts and payment terms
Financial Reporting
Generate daily, weekly, monthly, and annual reports
GST reporting with proper tax code handling
Profit and loss statements with detailed breakdowns
Cash flow analysis and reconciliation tools
Export capabilities for external accounting systems
User Management
Role-based access control with customizable permissions
User authentication and session management
Audit logging for all system activities
Multi-user concurrent access support
Non-Functional Requirements
Performance
Transaction processing: < 2 seconds per transaction
Report generation: < 30 seconds for monthly reports
Database queries: < 1 second for standard operations
System startup: < 10 seconds on standard hardware
Scalability
Support up to 10,000 products per location
Handle up to 1,000 transactions per day per terminal
Accommodate up to 50 concurrent users
Database growth capacity of 100GB+ over 5 years
Reliability
99.9% system uptime during business hours
Automatic backup and recovery mechanisms
Graceful degradation during network outages
Data integrity verification and correction
Security
Encrypted data transmission and storage
PCI DSS compliance for payment processing
Regular security audits and vulnerability assessments
Secure API endpoints with authentication
Usability
Intuitive interface requiring minimal training
Responsive design for various screen sizes
Keyboard shortcuts for power users
Multi-language support (English, Chinese, Malay, Tamil)
System Architecture
Layered Architecture Overview
The SG POS System implements a strict layered architecture that promotes separation of concerns, maintainability, and testability. The architecture consists of four primary layers:

1. Presentation Layer (app/ui/)
The topmost layer handles all user interface interactions and display logic. This layer is responsible for:

User input validation and formatting
Display of business data in appropriate formats
Navigation and workflow management
Integration with the business logic layer through the ApplicationCore
Key Components:

Main window and dialog managers
Widget components for specific business functions
Custom UI controls and layouts
Event handling and user interaction management
2. Business Logic Layer (app/business_logic/, app/accounting/)
The core layer containing all business rules, workflows, and domain logic. This layer orchestrates complex business operations while remaining independent of UI and data access concerns.

Key Components:

Manager classes for different business domains
Workflow orchestration and business rule enforcement
Transaction management and data validation
Integration with external services and APIs
3. Data Access Layer (app/services/)
This layer implements the Repository pattern, providing a clean abstraction over data persistence operations. It handles all database interactions and query logic.

Key Components:

Service classes implementing repository patterns
Database query abstraction and optimization
Data mapping and transformation
Connection management and transaction control
4. Persistence Layer (app/models/, database/)
The foundation layer responsible for data modeling and database schema management.

Key Components:

SQLAlchemy ORM models
Database schema definitions
Data constraints and integrity rules
Migration and versioning scripts
Dependency Injection Architecture
The system implements a sophisticated dependency injection mechanism centered around the ApplicationCore class:

class ApplicationCore:
    def __init__(self):
        self._database_service = None
        self._managers = {}
    
    @property
    def customer_manager(self) -> CustomerManager:
        if 'customer_manager' not in self._managers:
            self._managers['customer_manager'] = CustomerManager(self)
        return self._managers['customer_manager']

This approach provides:

Lazy initialization of expensive resources
Centralized dependency management
Easy testing through dependency mocking
Reduced coupling between components
Asynchronous Processing Model
The application implements a dual-thread architecture:

Main Thread (Qt GUI):

Handles all UI operations and user interactions
Maintains responsive user interface
Marshals async operations to the background thread
Background Thread (AsyncIO):

Processes database operations and external API calls
Handles file I/O and network operations
Manages scheduled tasks and background processes
Thread Communication:

schedule_task_from_qt() bridges Qt to AsyncIO
QMetaObject.invokeMethod() safely updates UI from background
Result patterns ensure proper error handling across threads
Database Design
Core Database Schema
The database schema is designed to support complex retail operations while maintaining data integrity and performance. The schema includes the following major entity groups:

Product Management
-- Products table with comprehensive product information
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    sku VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    supplier_id INTEGER REFERENCES suppliers(id),
    cost_price DECIMAL(10,2),
    selling_price DECIMAL(10,2),
    tax_code VARCHAR(10) DEFAULT 'GST',
    barcode VARCHAR(50),
    track_inventory BOOLEAN DEFAULT TRUE,
    reorder_point INTEGER DEFAULT 0,
    reorder_quantity INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Product variants for size, color, etc.
CREATE TABLE product_variants (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    variant_name VARCHAR(100) NOT NULL,
    variant_value VARCHAR(100) NOT NULL,
    sku_suffix VARCHAR(20),
    price_adjustment DECIMAL(10,2) DEFAULT 0,
    stock_quantity INTEGER DEFAULT 0
);

Customer Management
-- Customers table with comprehensive customer data
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    customer_code VARCHAR(50) UNIQUE NOT NULL,
    company_name VARCHAR(200),
    contact_person VARCHAR(100),
    email VARCHAR(150),
    phone VARCHAR(20),
    mobile VARCHAR(20),
    address_line1 VARCHAR(200),
    address_line2 VARCHAR(200),
    city VARCHAR(100),
    state VARCHAR(100),
    postal_code VARCHAR(20),
    country VARCHAR(100) DEFAULT 'Singapore',
    customer_type VARCHAR(20) DEFAULT 'Individual',
    credit_limit DECIMAL(10,2) DEFAULT 0,
    payment_terms INTEGER DEFAULT 0,
    gst_registration VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Sales and Transactions
-- Sales transactions header
CREATE TABLE sales_transactions (
    id SERIAL PRIMARY KEY,
    transaction_number VARCHAR(50) UNIQUE NOT NULL,
    customer_id INTEGER REFERENCES customers(id),
    user_id INTEGER REFERENCES users(id),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    subtotal DECIMAL(10,2) NOT NULL,
    tax_amount DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    total_amount DECIMAL(10,2) NOT NULL,
    payment_status VARCHAR(20) DEFAULT 'Pending',
    transaction_type VARCHAR(20) DEFAULT 'Sale',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Sales transaction line items
CREATE TABLE sales_transaction_items (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES sales_transactions(id),
    product_id INTEGER REFERENCES products(id),
    variant_id INTEGER REFERENCES product_variants(id),
    quantity DECIMAL(10,3) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    tax_amount DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2)
);

Payment Processing
-- Payment methods configuration
CREATE TABLE payment_methods (
    id SERIAL PRIMARY KEY,
    method_name VARCHAR(50) UNIQUE NOT NULL,
    method_type VARCHAR(20) NOT NULL, -- 'Cash', 'Card', 'Digital', 'Credit'
    is_active BOOLEAN DEFAULT TRUE,
    requires_reference BOOLEAN DEFAULT FALSE,
    processing_fee DECIMAL(5,4) DEFAULT 0
);

-- Payment transactions
CREATE TABLE payment_transactions (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES sales_transactions(id),
    payment_method_id INTEGER REFERENCES payment_methods(id),
    amount DECIMAL(10,2) NOT NULL,
    reference_number VARCHAR(100),
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'Completed',
    processor_response TEXT
);

Inventory Management
-- Inventory tracking with full audit trail
CREATE TABLE inventory_movements (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    variant_id INTEGER REFERENCES product_variants(id),
    movement_type VARCHAR(20) NOT NULL, -- 'In', 'Out', 'Adjustment', 'Transfer'
    quantity DECIMAL(10,3) NOT NULL,
    reference_id INTEGER, -- Links to sales, purchases, adjustments
    reference_type VARCHAR(20),
    cost_price DECIMAL(10,2),
    notes TEXT,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Current stock levels (materialized view)
CREATE MATERIALIZED VIEW current_stock AS
SELECT 
    product_id,
    variant_id,
    SUM(CASE WHEN movement_type IN ('In', 'Adjustment') THEN quantity ELSE -quantity END) as current_quantity,
    AVG(cost_price) as average_cost
FROM inventory_movements
GROUP BY product_id, variant_id;

Financial and Accounting
-- Chart of accounts for proper financial tracking
CREATE TABLE chart_of_accounts (
    id SERIAL PRIMARY KEY,
    account_code VARCHAR(20) UNIQUE NOT NULL,
    account_name VARCHAR(200) NOT NULL,
    account_type VARCHAR(20) NOT NULL, -- 'Asset', 'Liability', 'Equity', 'Income', 'Expense'
    parent_account_id INTEGER REFERENCES chart_of_accounts(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Journal entries for double-entry bookkeeping
CREATE TABLE journal_entries (
    id SERIAL PRIMARY KEY,
    entry_number VARCHAR(50) UNIQUE NOT NULL,
    entry_date DATE NOT NULL,
    reference_id INTEGER,
    reference_type VARCHAR(20), -- 'Sale', 'Purchase', 'Payment', 'Adjustment'
    description TEXT,
    total_debit DECIMAL(10,2) NOT NULL,
    total_credit DECIMAL(10,2) NOT NULL,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT balanced_entry CHECK (total_debit = total_credit)
);

-- Journal entry line items
CREATE TABLE journal_entry_lines (
    id SERIAL PRIMARY KEY,
    entry_id INTEGER REFERENCES journal_entries(id),
    account_id INTEGER REFERENCES chart_of_accounts(id),
    debit_amount DECIMAL(10,2) DEFAULT 0,
    credit_amount DECIMAL(10,2) DEFAULT 0,
    description TEXT,
    CONSTRAINT debit_or_credit CHECK (
        (debit_amount > 0 AND credit_amount = 0) OR 
        (credit_amount > 0 AND debit_amount = 0)
    )
);

Database Constraints and Triggers
Data Integrity Constraints
-- Ensure positive quantities in sales
ALTER TABLE sales_transaction_items 
ADD CONSTRAINT positive_quantity CHECK (quantity > 0);

-- Ensure valid transaction totals
ALTER TABLE sales_transactions 
ADD CONSTRAINT valid_total CHECK (total_amount >= 0);

-- Ensure unique transaction numbers per day
CREATE UNIQUE INDEX unique_daily_transaction 
ON sales_transactions (DATE(transaction_date), transaction_number);

Audit Triggers
-- Automatically update timestamps
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

Inventory Tracking Triggers
-- Automatically update stock levels
CREATE OR REPLACE FUNCTION update_stock_levels()
RETURNS TRIGGER AS $$
BEGIN
    -- Refresh materialized view when inventory changes
    REFRESH MATERIALIZED VIEW current_stock;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER inventory_change_trigger
    AFTER INSERT OR UPDATE OR DELETE ON inventory_movements
    FOR EACH STATEMENT
    EXECUTE FUNCTION update_stock_levels();

Indexing Strategy
-- Performance indexes for common queries
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_barcode ON products(barcode);
CREATE INDEX idx_sales_date ON sales_transactions(transaction_date);
CREATE INDEX idx_sales_customer ON sales_transactions(customer_id);
CREATE INDEX idx_inventory_product ON inventory_movements(product_id, created_at);
CREATE INDEX idx_journal_date ON journal_entries(entry_date);

-- Composite indexes for complex queries
CREATE INDEX idx_sales_items_product_date ON sales_transaction_items(product_id, created_at);
CREATE INDEX idx_customer_search ON customers(customer_code, company_name, contact_person);

Technology Stack
Core Technologies
Programming Language: Python 3.11+
Python serves as the primary development language due to its:

Excellent ecosystem for desktop applications
Strong database integration capabilities
Rich library support for business applications
Cross-platform compatibility
Mature debugging and profiling tools
GUI Framework: PySide6
PySide6 (Qt for Python) provides:

Native look and feel across platforms
Comprehensive widget library
Advanced graphics and animation capabilities
Robust event handling system
Professional UI development tools
Excellent documentation and community support
Database: PostgreSQL 15+
PostgreSQL offers:

ACID compliance for financial data integrity
Advanced JSON support for flexible data structures
Powerful query optimization
Extensive indexing capabilities
Robust backup and recovery mechanisms
JSON and JSONB support for configuration data
ORM: SQLAlchemy 2.0
SQLAlchemy provides:

Database abstraction layer
Advanced query construction
Relationship mapping
Connection pooling
Transaction management
Schema migration support
Supporting Libraries and Frameworks
Asynchronous Processing
AsyncIO: Native Python async/await support
aiofiles: Asynchronous file operations
asyncpg: High-performance PostgreSQL driver
Data Processing and Validation
Pydantic: Data validation and serialization
Pandas: Data analysis and reporting
NumPy: Numerical computations
Decimal: Precise financial calculations
Reporting and Export
ReportLab: PDF generation
openpyxl: Excel file generation
jinja2: Template rendering
matplotlib: Chart generation
Security and Authentication
cryptography: Encryption and hashing
bcrypt: Password hashing
PyJWT: JWT token handling
keyring: Secure credential storage
Testing Framework
pytest: Primary testing framework
pytest-asyncio: Async test support
pytest-qt: GUI testing
coverage: Code coverage analysis
factory-boy: Test data generation
Development Tools
black: Code formatting
flake8: Code linting
mypy: Static type checking
pre-commit: Git hooks
sphinx: Documentation generation
Architecture Patterns and Principles
Design Patterns
Repository Pattern: Data access abstraction
Manager Pattern: Business logic orchestration
Factory Pattern: Object creation
Observer Pattern: Event notification
Command Pattern: Operation encapsulation
Architectural Principles
SOLID Principles: Single responsibility, Open-closed, Liskov substitution, Interface segregation, Dependency inversion
DRY (Don't Repeat Yourself): Code reusability
KISS (Keep It Simple, Stupid): Simplicity in design
YAGNI (You Aren't Gonna Need It): Feature minimalism
Data Transfer Objects (DTOs)
from dataclasses import dataclass
from typing import Optional, List
from decimal import Decimal

@dataclass
class ProductDTO:
    id: Optional[int] = None
    sku: str = ""
    name: str = ""
    description: Optional[str] = None
    cost_price: Decimal = Decimal('0.00')
    selling_price: Decimal = Decimal('0.00')
    stock_quantity: int = 0
    
@dataclass
class SalesTransactionDTO:
    id: Optional[int] = None
    transaction_number: str = ""
    customer_id: Optional[int] = None
    subtotal: Decimal = Decimal('0.00')
    tax_amount: Decimal = Decimal('0.00')
    total_amount: Decimal = Decimal('0.00')
    items: List[SalesTransactionItemDTO] = None

Result Pattern Implementation
from typing import Generic, TypeVar, Union
from dataclasses import dataclass

T = TypeVar('T')

@dataclass
class Success(Generic[T]):
    value: T
    
@dataclass
class Failure:
    error: str
    details: Optional[str] = None

Result = Union[Success[T], Failure]

# Usage in services
async def get_product_by_sku(self, sku: str) -> Result[ProductDTO]:
    try:
        product = await self._repository.find_by_sku(sku)
        if product:
            return Success(ProductDTO.from_model(product))
        return Failure(f"Product not found: {sku}")
    except Exception as e:
        return Failure(f"Database error: {str(e)}")

Development Environment Setup
System Requirements
Hardware Requirements
CPU: Intel i5 or AMD Ryzen 5 equivalent (4+ cores)
RAM: 8GB minimum, 16GB recommended
Storage: 50GB available space (SSD recommended)
Display: 1920x1080 minimum resolution
Operating System Support
Windows: 10/11 (64-bit)
macOS: 10.15 Catalina or later
Linux: Ubuntu 20.04 LTS or equivalent
Development Environment Installation
Step 1: Python Environment Setup
# Install Python 3.11 or later
# Windows: Download from python.org
# macOS: brew install python@3.11
# Linux: sudo apt-get install python3.11

# Verify installation
python --version

# Install pipenv for dependency management
pip install pipenv

# Create virtual environment
pipenv install --dev
pipenv shell

Step 2: PostgreSQL Database Setup
# Windows: Download PostgreSQL installer
# macOS: brew install postgresql
# Linux: sudo apt-get install postgresql postgresql-contrib

# Start PostgreSQL service
# Windows: Services management
# macOS: brew services start postgresql
# Linux: sudo systemctl start postgresql

# Create development database
createdb sg_pos_dev

# Create database user
psql -c "CREATE USER pos_dev WITH PASSWORD 'dev_password';"
psql -c "GRANT ALL PRIVILEGES ON DATABASE sg_pos_dev TO pos_dev;"

Step 3: Project Setup
# Clone repository
git clone https://github.com/your-org/sg-pos-system.git
cd sg-pos-system

# Install dependencies
pipenv install --dev

# Set up environment variables
cp .env.example .env
# Edit .env with development settings

# Run database migrations
python scripts/migrate.py

# Initialize development data
python scripts/init_dev_data.py

# Run tests to verify setup
pytest

Step 4: IDE Configuration
VS Code Setup
// .vscode/settings.json
{
    "python.defaultInterpreterPath": "path/to/pipenv/python",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": false,
    "python.linting.flake8Enabled": true,
    "python.formatting.provider": "black",
    "python.testing.pytestEnabled": true,
    "python.testing.unittestEnabled": false,
    "python.testing.nosetestsEnabled": false
}

PyCharm Setup
Configure Python interpreter to use pipenv environment
Set up database connection to development PostgreSQL
Configure code style to use Black formatter
Set up run configurations for main application and tests
Development Workflow
Git Workflow
# Feature development
git checkout -b feature/new-feature-name
# Make changes
git add .
git commit -m "Add new feature description"
git push origin feature/new-feature-name

# Code review process
# Create pull request
# Address review comments
# Merge to main branch

Code Quality Checks
# Pre-commit hooks setup
pre-commit install

# Manual code quality checks
black app/ tests/
flake8 app/ tests/
mypy app/
pytest --cov=app tests/

Database Development
# Create new migration
python scripts/create_migration.py "description_of_changes"

# Apply migrations
python scripts/migrate.py

# Rollback migration
python scripts/rollback.py

# Reset development database
python scripts/reset_dev_db.py

Development Configuration
Environment Variables (.env)
# Database Configuration
DATABASE_URL=postgresql://pos_dev:dev_password@localhost/sg_pos_dev
DATABASE_POOL_SIZE=5
DATABASE_MAX_OVERFLOW=10

# Application Configuration
DEBUG=True
LOG_LEVEL=DEBUG
SECRET_KEY=development-secret-key-change-in-production

# External Services
PAYMENT_GATEWAY_URL=https://sandbox.payment-gateway.com/api
PAYMENT_GATEWAY_KEY=sandbox_key

# File Paths
UPLOAD_DIRECTORY=./uploads
BACKUP_DIRECTORY=./backups
LOG_DIRECTORY=./logs

# Feature Flags
ENABLE_ADVANCED_REPORTING=True
ENABLE_MULTI_CURRENCY=True
ENABLE_OFFLINE_MODE=True

Logging Configuration
# app/config/logging.py
import logging
import logging.handlers
from pathlib import Path

def setup_logging():
    log_dir = Path("logs")
    log_dir.mkdir(exist_ok=True)
    
    # Create formatters
    detailed_formatter = logging.Formatter(
        '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
    )
    
    # File handler
    file_handler = logging.handlers.RotatingFileHandler(
        log_dir / "sg_pos.log",
        maxBytes=10*1024*1024,  # 10MB
        backupCount=5
    )
    file_handler.setFormatter(detailed_formatter)
    
    # Console handler
    console_handler = logging.StreamHandler()
    console_handler.setFormatter(detailed_formatter)
    
    # Root logger
    root_logger = logging.getLogger()
    root_logger.setLevel(logging.DEBUG)
    root_logger.addHandler(file_handler)
    root_logger.addHandler(console_handler)

Production Environment Setup
Infrastructure Requirements
Server Specifications
CPU: Intel Xeon or AMD EPYC (8+ cores)
RAM: 32GB minimum, 64GB for high-volume stores
Storage: 500GB NVMe SSD with RAID 1 configuration
Network: Gigabit Ethernet with redundant connections
UPS: Uninterruptible power supply with 30+ minute runtime
Operating System
Recommended: Ubuntu Server 22.04 LTS
Alternative: CentOS Stream 9 or RHEL 9
Windows Server: 2019 or later (if required)
Production Database Setup
PostgreSQL Configuration
# Install PostgreSQL 15
sudo apt-get update
sudo apt-get install postgresql-15 postgresql-client-15

# Configure PostgreSQL
sudo -u postgres psql

-- Create production database and user
CREATE DATABASE sg_pos_production;
CREATE USER pos_production WITH PASSWORD 'secure_production_password';
GRANT ALL PRIVILEGES ON DATABASE sg_pos_production TO pos_production;

-- Configure performance settings
ALTER SYSTEM SET shared_buffers = '256MB';
ALTER SYSTEM SET effective_cache_size = '1GB';
ALTER SYSTEM SET maintenance_work_mem = '64MB';
ALTER SYSTEM SET checkpoint_completion_target = 0.9;
ALTER SYSTEM SET wal_buffers = '16MB';
ALTER SYSTEM SET default_statistics_target = 100;

-- Reload configuration
SELECT pg_reload_conf();

Database Security Configuration
# Edit postgresql.conf
sudo nano /etc/postgresql/15/main/postgresql.conf

# Key security settings:
ssl = on
ssl_cert_file = 'server.crt'
ssl_key_file = 'server.key'
ssl_ca_file = 'ca.crt'
password_encryption = scram-sha-256

# Edit pg_hba.conf
sudo nano /etc/postgresql/15/main/pg_hba.conf

# Security settings:
hostssl sg_pos_production pos_production 0.0.0.0/0 scram-sha-256
hostssl sg_pos_production pos_production ::0/0 scram-sha-256

Backup Configuration
# Automated backup script
#!/bin/bash
# /opt/sg-pos/scripts/backup.sh

BACKUP_DIR="/opt/sg-pos/backups"
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
DATABASE="sg_pos_production"
USER="pos_production"

# Create backup directory
mkdir -p $BACKUP_DIR

# Full database backup
pg_dump -h localhost -U $USER -d $DATABASE -f $BACKUP_DIR/backup_$TIMESTAMP.sql

# Compress backup
gzip $BACKUP_DIR/backup_$TIMESTAMP.sql

# Remove backups older than 30 days
find $BACKUP_DIR -name "*.sql.gz" -mtime +30 -delete

# Log backup completion
echo "$(date): Backup completed - backup_$TIMESTAMP.sql.gz" >> /var/log/sg-pos-backup.log

# Add to crontab
sudo crontab -e
# Add line: 0 2 * * * /opt/sg-pos/scripts/backup.sh

Application Deployment
Application Structure
/opt/sg-pos/
├── app/                    # Application code
├── config/                 # Configuration files
├── logs/                   # Application logs
├── backups/               # Database backups
├── uploads/               # File uploads
├── scripts/               # Utility scripts
├── requirements.txt       # Python dependencies
├── .env                   # Environment variables
└── sg-pos.service        # Systemd service file
Systemd Service Configuration
# /etc/systemd/system/sg-pos.service
[Unit]
Description=SG POS System
After=network.target postgresql.service

[Service]
Type=simple
User=pos
Group=pos
WorkingDirectory=/opt/sg-pos
Environment=PATH=/opt/sg-pos/venv/bin
ExecStart=/opt/sg-pos/venv/bin/python app/main.py
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target

Production Environment Variables
# Database Configuration
DATABASE_URL=postgresql://pos_production:secure_production_password@localhost/sg_pos_production
DATABASE_POOL_SIZE=20
DATABASE_MAX_OVERFLOW=30
DATABASE_SSL_MODE=require

# Application Configuration
DEBUG=False
LOG_LEVEL=INFO
SECRET_KEY=ultra-secure-production-secret-key-change-regularly

# External Services
PAYMENT_GATEWAY_URL=https://api.payment-gateway.com
PAYMENT_GATEWAY_KEY=production_key_encrypted

# Security Settings
ALLOWED_HOSTS=pos.yourcompany.com,192.168.1.100
CORS_ORIGINS=https://pos.yourcompany.com

# File Paths
UPLOAD_DIRECTORY=/opt/sg-pos/uploads
BACKUP_DIRECTORY=/opt/sg-pos/backups
LOG_DIRECTORY=/opt/sg-pos/logs

# Performance Settings
ENABLE_CACHING=True
CACHE_TTL=300
MAX_CONCURRENT_USERS=50

# Feature Flags
ENABLE_ADVANCED_REPORTING=True
ENABLE_MULTI_CURRENCY=True
ENABLE_OFFLINE_MODE=True
ENABLE_API_ACCESS=True

SSL Certificate Setup
# Let's Encrypt SSL certificate
sudo apt-get install certbot
sudo certbot certonly --standalone -d pos.yourcompany.com

# Configure nginx reverse proxy
sudo nano /etc/nginx/sites-available/sg-pos

server {
    listen 80;
    server_name pos.yourcompany.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name pos.yourcompany.com;

    ssl_certificate /etc/letsencrypt/live/pos.yourcompany.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/pos.yourcompany.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Monitoring and Logging
System Monitoring
# Install monitoring tools
sudo apt-get install htop iotop nethogs

# Configure log rotation
sudo nano /etc/logrotate.d/sg-pos

/opt/sg-pos/logs/*.log {
    daily
    missingok
    rotate 30
    compress
    delaycompress
    notifempty
    create 644 pos pos
    postrotate
        systemctl reload sg-pos
    endscript
}
Application Monitoring
# app/monitoring/health_check.py
import asyncio
import psutil
from datetime import datetime
from app.services.database_service import DatabaseService

class HealthMonitor:
    async def check_system_health(self):
        return {
            'timestamp': datetime.now().isoformat(),
            'cpu_usage': psutil.cpu_percent(),
            'memory_usage': psutil.virtual_memory().percent,
            'disk_usage': psutil.disk_usage('/').percent,
            'database_status': await self._check_database(),
            'active_connections': await self._check_connections()
        }
    
    async def _check_database(self):
        try:
            db_service = DatabaseService()
            result = await db_service.execute_query("SELECT 1")
            return 'healthy' if result else 'unhealthy'
        except Exception as e:
            return f'error: {str(e)}'

Application Modules
File Hierarchy Structure
sg-pos-system/
├── app/
│   ├── __init__.py
│   ├── main.py                     # Application entry point
│   ├── application_core.py         # Dependency injection container
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py            # Configuration management
│   │   ├── database.py            # Database configuration
│   │   └── logging.py             # Logging configuration
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py                # Base model class
│   │   ├── product.py             # Product models
│   │   ├── customer.py            # Customer models
│   │   ├── sales.py               # Sales transaction models
│   │   ├── inventory.py           # Inventory models
│   │   ├── payment.py             # Payment models
│   │   ├── user.py                # User and authentication models
│   │   └── accounting.py          # Accounting and financial models
│   ├── services/
│   │   ├── __init__.py
│   │   ├── base_service.py        # Base service class
│   │   ├── database_service.py    # Database connection service
│   │   ├── product_service.py     # Product data service
│   │   ├── customer_service.py    # Customer data service
│   │   ├── sales_service.py       # Sales data service
│   │   ├── inventory_service.py   # Inventory data service
│   │   ├── payment_service.py     # Payment processing service
│   │   ├── user_service.py        # User management service
│   │   └── reporting_service.py   # Reporting data service
│   ├── business_logic/
│   │   ├── __init__.py
│   │   ├── managers/
│   │   │   ├── __init__.py
│   │   │   ├── product_manager.py      # Product business logic
│   │   │   ├── customer_manager.py     # Customer business logic
│   │   │   ├── sales_manager.py        # Sales business logic
│   │   │   ├── inventory_manager.py    # Inventory business logic
│   │   │   ├── payment_manager.py      # Payment business logic
│   │   │   ├── user_manager.py         # User management logic
│   │   │   └── reporting_manager.py    # Reporting business logic
│   │   ├── workflows/
│   │   │   ├── __init__.py
│   │   │   ├── sales_workflow.py       # Sales process workflow
│   │   │   ├── return_workflow.py      # Return process workflow
│   │   │   └── inventory_workflow.py   # Inventory workflows
│   │   └── validators/
│   │       ├── __init__.py
│   │       ├── product_validator.py    # Product validation
│   │       ├── customer_validator.py   # Customer validation
│   │       └── sales_validator.py      # Sales validation
│   ├── accounting/
│   │   ├── __init__.py
│   │   ├── gst_manager.py         # GST calculation and reporting
│   │   ├── journal_manager.py     # Journal entry management
│   │   ├── financial_manager.py   # Financial reporting
│   │   └── tax_calculator.py      # Tax calculation utilities
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── main_window.py         # Main application window
│   │   ├── widgets/
│   │   │   ├── __init__.py
│   │   │   ├── sales_widget.py         # Sales interface
│   │   │   ├── product_widget.py       # Product management
│   │   │   ├── customer_widget.py      # Customer management
│   │   │   ├── inventory_widget.py     # Inventory management
│   │   │   ├── reports_widget.py       # Reporting interface
│   │   │   └── settings_widget.py      # Settings management
│   │   ├── dialogs/
│   │   │   ├── __init__.py
│   │   │   ├── product_dialog.py       # Product add/edit dialog
│   │   │   ├── customer_dialog.py      # Customer add/edit dialog
│   │   │   ├── payment_dialog.py       # Payment processing dialog
│   │   │   └── login_dialog.py         # User login dialog
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── product_model.py        # Product table model
│   │   │   ├── customer_model.py       # Customer table model
│   │   │   └── sales_model.py          # Sales table model
│   │   └── utils/
│   │       ├── __init__.py
│   │       ├── ui_helpers.py           # UI utility functions
│   │       └── validators.py           # UI validation helpers
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── constants.py           # Application constants
│   │   ├── exceptions.py          # Custom exceptions
│   │   ├── formatters.py          # Data formatting utilities
│   │   ├── validators.py          # Data validation utilities
│   │   └── async_helpers.py       # Async utility functions
│   └── api/
│       ├── __init__.py
│       ├── routes/
│       │   ├── __init__.py
│       │   ├── products.py             # Product API endpoints
│       │   ├── customers.py            # Customer API endpoints
│       │   ├── sales.py                # Sales API endpoints
│       │   └── reports.py              # Reports API endpoints
│       ├── middleware/
│       │   ├── __init__.py
│       │   ├── authentication.py       # API authentication
│       │   └── rate_limiting.py        # Rate limiting
│       └── schemas/
│           ├── __init__.py
│           ├── product_schema.py       # Product API schemas
│           ├── customer_schema.py      # Customer API schemas
│           └── sales_schema.py         # Sales API schemas
├── tests/
│   ├── __init__.py
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_models/
│   │   ├── test_services/
│   │   ├── test_business_logic/
│   │   └── test_utils/
│   ├── integration/
│   │   ├── __init__.py
│   │   ├── test_database/
│   │   ├── test_workflows/
│   │   └── test_api/
│   └── ui/
│       ├── __init__.py
│       ├── test_widgets/
│       └── test_dialogs/
├── scripts/
│   ├── __init__.py
│   ├── migrate.py                 # Database migration script
│   ├── create_migration.py        # Migration creation script
│   ├── init_dev_data.py          # Development data initialization
│   ├── backup.py                 # Backup script
│   └── deploy.py                 # Deployment script
├── database/
│   ├── schema.sql                # Database schema
│   ├── migrations/               # Database migrations
│   └── seeds/                    # Seed data files
├── docs/
│   ├── api/                      # API documentation
│   ├── user/                     # User documentation
│   └── technical/                # Technical documentation
├── requirements.txt              # Python dependencies
├── requirements-dev.txt          # Development dependencies
├── Pipfile                       # Pipenv configuration
├── .env.example                  # Environment variables template
├── .gitignore                    # Git ignore rules
├── pytest.ini                   # Pytest configuration
├── mypy.ini                      # MyPy configuration
├── setup.py                      # Package setup
└── README.md                     # Project documentation
Core Application Modules
1. Application Entry Point (app/main.py)
"""
Main application entry point that initializes the Qt application,
sets up the async event loop, and manages the application lifecycle.
"""

import sys
import asyncio
import logging
from pathlib import Path
from PySide6.QtWidgets import QApplication
from PySide6.QtCore import QThread, QTimer

from app.config.settings import Settings
from app.config.logging import setup_logging
from app.application_core import ApplicationCore
from app.ui.main_window import MainWindow
from app.utils.async_helpers import AsyncEventLoop

class SGPOSApplication:
    def __init__(self):
        self.app = QApplication(sys.argv)
        self.settings = Settings()
        self.app_core = ApplicationCore()
        self.main_window = None
        self.async_thread = None
        
    async def initialize(self):
        """Initialize application components"""
        setup_logging()
        await self.app_core.initialize()
        
        # Initialize main window
        self.main_window = MainWindow(self.app_core)
        self.main_window.show()
        
    def run(self):
        """Run the application"""
        # Set up async event loop in separate thread
        self.async_thread = AsyncEventLoop()
        self.async_thread.start()
        
        # Schedule initialization
        QTimer.singleShot(0, lambda: self.async_thread.run_coroutine(self.initialize()))
        
        # Run Qt event loop
        sys.exit(self.app.exec())

if __name__ == "__main__":
    app = SGPOSApplication()
    app.run()

2. Application Core (app/application_core.py)
"""
Central dependency injection container that manages all application services
and business logic managers with lazy initialization.
"""

from typing import Optional
import logging
from app.config.settings import Settings
from app.services.database_service import DatabaseService
from app.business_logic.managers.product_manager import ProductManager
from app.business_logic.managers.customer_manager import CustomerManager
from app.business_logic.managers.sales_manager import SalesManager
from app.business_logic.managers.inventory_manager import InventoryManager
from app.business_logic.managers.payment_manager import PaymentManager
from app.business_logic.managers.user_manager import UserManager
from app.business_logic.managers.reporting_manager import ReportingManager

class ApplicationCore:
    """Central application core managing all dependencies"""
    
    def __init__(self):
        self.settings = Settings()
        self.logger = logging.getLogger(__name__)
        self._services = {}
        self._managers = {}
        self._initialized = False
    
    async def initialize(self):
        """Initialize core services"""
        if self._initialized:
            return
            
        self.logger.info("Initializing ApplicationCore...")
        
        # Initialize database service
        await self.database_service.initialize()
        
        self._initialized = True
        self.logger.info("ApplicationCore initialized successfully")
    
    # Service Properties (Lazy Loading)
    @property
    def database_service(self) -> DatabaseService:
        if 'database_service' not in self._services:
            self._services['database_service'] = DatabaseService(self.settings.database_url)
        return self._services['database_service']
    
    # Manager Properties (Lazy Loading)
    @property
    def product_manager(self) -> ProductManager:
        if 'product_manager' not in self._managers:
            self._managers['product_manager'] = ProductManager(self)
        return self._managers['product_manager']
    
    @property
    def customer_manager(self) -> CustomerManager:
        if 'customer_manager' not in self._managers:
            self._managers['customer_manager'] = CustomerManager(self)
        return self._managers['customer_manager']
    
    @property
    def sales_manager(self) -> SalesManager:
        if 'sales_manager' not in self._managers:
            self._managers['sales_manager'] = SalesManager(self)
        return self._managers['sales_manager']
    
    @property
    def inventory_manager(self) -> InventoryManager:
        if 'inventory_manager' not in self._managers:
            self._managers['inventory_manager'] = InventoryManager(self)
        return self._managers['inventory_manager']
    
    @property
    def payment_manager(self) -> PaymentManager:
        if 'payment_manager' not in self._managers:
            self._managers['payment_manager'] = PaymentManager(self)
        return self._managers['payment_manager']
    
    @property
    def user_manager(self) -> UserManager:
        if 'user_manager' not in self._managers:
            self._managers['user_manager'] = UserManager(self)
        return self._managers['user_manager']
    
    @property
    def reporting_manager(self) -> ReportingManager:
        if 'reporting_manager' not in self._managers:
            self._managers['reporting_manager'] = ReportingManager(self)
        return self._managers['reporting_manager']
    
    async def shutdown(self):
        """Cleanup resources"""
        self.logger.info("Shutting down ApplicationCore...")
        
        # Close database connections
        if 'database_service' in self._services:
            await self._services['database_service'].close()
        
        self.logger.info("ApplicationCore shutdown complete")

3. Database Service (app/services/database_service.py)
"""
Database service implementing the Repository pattern with connection pooling,
transaction management, and query abstraction.
"""

import asyncio
import logging
from typing import Optional, List, Dict, Any
from contextlib import asynccontextmanager
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession, async_sessionmaker
from sqlalchemy.orm import selectinload
from sqlalchemy import select, update, delete, text
from app.models.base import BaseModel

class DatabaseService:
    """Database service with connection pooling and transaction management"""
    
    def __init__(self, database_url: str):
        self.database_url = database_url
        self.engine = None
        self.session_factory = None
        self.logger = logging.getLogger(__name__)
    
    async def initialize(self):
        """Initialize database engine and session factory"""
        self.engine = create_async_engine(
            self.database_url,
            pool_size=20,
            max_overflow=30,
            pool_pre_ping=True,
            echo=False
        )
        
        self.session_factory = async_sessionmaker(
            bind=self.engine,
            class_=AsyncSession,
            expire_on_commit=False
        )
        
        self.logger.info("Database service initialized")
    
    @asynccontextmanager
    async def get_session(self):
        """Get database session with automatic cleanup"""
        async with self.session_factory() as session:
            try:
                yield session
            except Exception as e:
                await session.rollback()
                self.logger.error(f"Database session error: {e}")
                raise
            finally:
                await session.close()
    
    @asynccontextmanager
    async def get_transaction(self):
        """Get database session with transaction management"""
        async with self.get_session() as session:
            async with session.begin():
                yield session
    
    async def execute_query(self, query: str, params: Optional[Dict] = None) -> List[Dict]:
        """Execute raw SQL query"""
        async with self.get_session() as session:
            result = await session.execute(text(query), params or {})
            return [dict(row._mapping) for row in result.fetchall()]
    
    async def execute_scalar(self, query: str, params: Optional[Dict] = None) -> Any:
        """Execute scalar query returning single value"""
        async with self.get_session() as session:
            result = await session.execute(text(query), params or {})
            return result.scalar()
    
    async def close(self):
        """Close database connections"""
        if self.engine:
            await self.engine.dispose()
            self.logger.info("Database connections closed")

4. Product Manager (app/business_logic/managers/product_manager.py)
"""
Product manager handling all product-related business logic including
inventory integration, pricing, and category management.
"""

import logging
from typing import List, Optional, Dict, Any
from decimal import Decimal
from app.models.product import Product, ProductVariant, Category
from app.services.product_service import ProductService
from app.services.inventory_service import InventoryService
from app.utils.exceptions import ValidationError, BusinessLogicError
from app.utils.validators import ProductValidator
from app.utils.formatters import format_currency

class ProductManager:
    """Manages product business logic and workflows"""
    
    def __init__(self, app_core: "ApplicationCore"):
        self.app_core = app_core
        self.logger = logging.getLogger(__name__)
        self._product_service = None
        self._inventory_service = None
        self._validator = ProductValidator()
    
    @property
    def product_service(self) -> ProductService:
        if self._product_service is None:
            self._product_service = ProductService(self.app_core.database_service)
        return self._product_service
    
    @property
    def inventory_service(self) -> InventoryService:
        if self._inventory_service is None:
            self._inventory_service = InventoryService(self.app_core.database_service)
        return self._inventory_service
    
    async def create_product(self, product_data: Dict[str, Any]) -> Product:
        """Create new product with validation and inventory setup"""
        try:
            # Validate product data
            validation_result = self._validator.validate_product_data(product_data)
            if not validation_result.is_valid:
                raise ValidationError(validation_result.errors)
            
            # Check for duplicate SKU
            existing_product = await self.product_service.get_by_sku(product_data['sku'])
            if existing_product:
                raise BusinessLogicError(f"Product with SKU {product_data['sku']} already exists")
            
            # Create product
            product = await self.product_service.create(product_data)
            
            # Initialize inventory if tracking is enabled
            if product_data.get('track_inventory', True):
                await self.inventory_service.initialize_product_inventory(
                    product.id,
                    product_data.get('initial_quantity', 0),
                    product_data.get('cost_price', Decimal('0.00'))
                
