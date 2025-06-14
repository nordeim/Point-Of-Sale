```toml
###############################################################################
#  SG-POS • pyproject.toml
#  ---------------------------------------------------------------------------
#  • Poetry-managed project metadata and dependency manifest
#  • Tooling configuration for Black, Ruff, MyPy, PyTest, Sphinx, etc.
#  • Developer task aliases via Poethepoet
#
#  Minimum Python version: 3.11  (tested up to 3.12-beta)
###############################################################################
[build-system]
requires      = ["poetry-core>=1.8.1"]
build-backend = "poetry.core.masonry.api"

###############################################################################
#  1. Project Metadata
###############################################################################
[tool.poetry]
name        = "sg-pos"
version     = "0.8.0-beta.0"
description = "Singapore-first, cross-platform, offline-capable Point-of-Sale system built with Python, Qt 6 & PostgreSQL."
readme      = "README.md"
license     = "MIT"
keywords    = ["POS", "Retail", "Singapore", "GST", "PySide6", "PostgreSQL"]
homepage    = "https://sg-pos.dev"
repository  = "https://github.com/acme/sg-pos"
documentation = "https://acme.github.io/sg-pos/"
authors     = ["SG-POS Core Team <core@sg-pos.dev>"]
classifiers = [
    "Development Status :: 4 - Beta",
    "Environment :: X11 Applications :: Qt",
    "Framework :: AsyncIO",
    "Framework :: PySide6",
    "Intended Audience :: Developers",
    "Intended Audience :: Retailers",
    "License :: OSI Approved :: MIT License",
    "Operating System :: MacOS :: MacOS X",
    "Operating System :: POSIX :: Linux",
    "Operating System :: Microsoft :: Windows",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
    "Topic :: Office/Business :: Financial :: Point-Of-Sale",
]

###############################################################################
#  2. Runtime Dependencies
###############################################################################
[tool.poetry.dependencies]
python           = ">=3.11,<3.13"

# — GUI & Desktop
PySide6          = ">=6.6,<6.8"

# — Database & ORM
SQLAlchemy       = {version = ">=2.0.29,<2.1", extras = ["asyncio"]}
asyncpg          = "^0.29"        # async PostgreSQL driver
psycopg2-binary  = {version = "^2.9", optional = true}  # optional sync access for scripts

# — Data Validation / Serialization
pydantic         = "^2.7"

# — Dependency Injection / Tasks
injector         = "^0.21"        # lightweight, used under the hood by ApplicationCore

# — Async Ecosystem
aiohttp          = "^3.9"
tenacity         = "^8.3"         # retry helper
redis            = "^5.0"

# — Observability
structlog        = "^24.1"
opentelemetry-api = "^1.25"
opentelemetry-sdk = "^1.25"
sentry-sdk       = {version = "^2.0", extras = ["aiohttp"]}

# — Security / Crypto
cryptography     = "^42.0"
python-dotenv    = "^1.0"

# — Misc Utilities
python-dateutil  = "^2.9"
pendulum         = "^3.0"
tabulate         = "^0.9"
rich             = "^13.7"

###############################################################################
#  3. Optional / Extra Groups
###############################################################################
[tool.poetry.extras]
psycopg-sync = ["psycopg2-binary"]

###############################################################################
#  4. Development / Test / Docs Dependencies
###############################################################################
[tool.poetry.group.dev.dependencies]  # ➜ poetry install --with dev
pytest                = "^8.2"
pytest-asyncio        = "^0.23"
pytest-cov            = "^5.0"
hypothesis            = "^6.100"

black                 = "^24.4"
ruff                  = "^0.4"
mypy                  = "^1.10"
isort                 = "^5.13"

pre-commit            = "^3.7"
commitizen            = "^3.20"
poethepoet            = "^0.25"

coverage              = "^7.5"
bandit                = "^1.7"

watchdog              = "^4.0"     # hot-reload during dev

[tool.poetry.group.docs.dependencies]
sphinx                = "^7.3"
myst-parser           = "^2.0"
sphinx-rtd-theme      = "^2.0"

###############################################################################
#  5. Executable Entry-Points
###############################################################################
[tool.poetry.scripts]
sgpos-main   = "app.main:main"
sgpos-seed   = "scripts.seed_demo_data:main"
sgpos-migrate = "scripts.db_migrate:cli"

###############################################################################
#  6. Tooling Configuration
###############################################################################

# ------------------------------- Black -------------------------------
[tool.black]
line-length = 100
target-version = ["py311"]
color = true

# ------------------------------- Ruff -------------------------------
[tool.ruff]
line-length = 100
target-version = "py311"
exclude = ["tests/data/*", "app/ui/resources_rc.py"]
lint.select = [
    "E", "F", "W",  # Pyflakes / Pycodestyle
    "I",            # isort-like import rules
    "UP",           # pyupgrade
    "B",            # bugbear
    "C4",           # comprehensions
    "SIM",          # simplicity
    "T20",          # print debug
]
lint.ignore = ["E501"]  # Black already enforces line length
format = "grouped"

# ------------------------------- MyPy -------------------------------
[tool.mypy]
python_version        = "3.11"
strict                = true
ignore_missing_imports = true
plugins = ["pydantic.mypy"]

# ------------------------------- isort -------------------------------
[tool.isort]
profile = "black"
line_length = 100
known_first_party = ["app", "scripts", "tests"]
multi_line_output = 3

# ------------------------------- PyTest ------------------------------
[tool.pytest.ini_options]
minversion = "8.0"
addopts    = "-ra -q --cov=app --cov-report=term-missing"
testpaths  = ["tests"]
asyncio_mode = "auto"

# ------------------------------- Coverage ----------------------------
[tool.coverage.run]
branch = true
source = ["app"]
omit   = ["*/__init__.py", "app/ui/resources_rc.py"]

# ------------------------------- Commitizen --------------------------
[tool.commitizen]
name = "cz_conventional_commits"
version = "0.8.0-beta.0"
tag_format = "v$version"
update_changelog_on_bump = true

# ------------------------------- PoeThePoet --------------------------
[tool.poe.tasks]
lint   = { cmd = "ruff check ." }
format = { shell = "black . && isort ." }
type   = { cmd = "mypy app" }
test   = { cmd = "pytest" }
ci     = { sequence = ["lint", "type", "test"], help = "Run full CI checks locally." }
shell  = { cmd = "ipython -i -c 'import app, asyncio'" }

###############################################################################
#  7. End-of-File
###############################################################################
```

**Highlights & Rationale**

• **Poetry** drives packaging, isolation and publishing.  
• **Extras** allow opt-in sync PostgreSQL driver if needed for legacy scripts.  
• **Groups** separate core, dev/test, and docs dependencies; install selectively.  
• Out-of-the-box tasks via **PoeThePoet** (`poe ci`, `poe format`, `poe shell`).  
• Opinionated static analysis suite: **Black + Ruff + MyPy**—zero-warning merges.  
• End-user runnable entry-point `sgpos-main` starts the Qt desktop client with a single command.

Drop this `pyproject.toml` into your repo root, then bootstrap with:

```bash
# install ALL dependencies (main + dev + docs)
poetry install --all-extras --with dev,docs

# run desktop app
poetry run sgpos-main
```
