Below is a ready-to-drop-in `docker-compose.dev.yml` that spins up every **server-side dependency** required by SG-POS during local development.  
It is intentionally verbose and heavily commented so new contributors understand *why* each setting exists.

```yaml
###############################################################################
# SG-POS : Development Docker Compose Stack
# ---------------------------------------------------------------------------
#  • PostgreSQL 15 (primary datastore)
#  • Redis 7          (async task queue / cache)
#  • MailHog          (local SMTP sink for e-mail previews)
#  • pgAdmin 4        (optional DB GUI)
#  • App Worker       (background tasks & CLI entry-point)
#
#  NOTE: The PySide6 desktop client is usually executed natively
#        on the host for hot-reload comfort, but we still provide an
#        `app` container to run Alembic migrations, seed scripts, or
#        headless batch jobs during development.
###############################################################################
version: "3.9"

############################
# 1) Global settings
############################
x-env-common: &env-common
  PGHOST: db
  PGPORT: "5432"
  PGUSER: sgpos
  PGPASSWORD: sgpos
  PGDATABASE: sgpos_dev
  DB_URI: postgresql+asyncpg://sgpos:sgpos@db:5432/sgpos_dev
  REDIS_URL: redis://redis:6379/0
  TZ: Asia/Singapore
  PYTHONUNBUFFERED: "1"

############################
# 2) Services
############################
services:
  # -------------------------------------------------------------------------
  # 2.1  PostgreSQL
  # -------------------------------------------------------------------------
  db:
    image: postgres:15-alpine
    container_name: sgpos_db
    restart: unless-stopped
    environment:
      POSTGRES_USER: sgpos
      POSTGRES_PASSWORD: sgpos
      POSTGRES_DB: sgpos_dev
      PGDATA: /var/lib/postgresql/data/pgdata
      TZ: Asia/Singapore
    volumes:
      - pgdata:/var/lib/postgresql/data
      - ./schema.sql:/docker-entrypoint-initdb.d/00_schema.sql:ro # auto-load
    ports:
      - "5432:5432"
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U sgpos"]
      interval: 5s
      timeout: 3s
      retries: 20

  # -------------------------------------------------------------------------
  # 2.2  Redis (async task queue / cache)
  # -------------------------------------------------------------------------
  redis:
    image: redis:7-alpine
    container_name: sgpos_redis
    restart: unless-stopped
    command: ["redis-server", "--appendonly", "yes"]
    volumes:
      - redisdata:/data
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 3s
      retries: 20

  # -------------------------------------------------------------------------
  # 2.3  MailHog – catch outgoing mail in development
  #         Web UI  : http://localhost:8025
  #         SMTP    : localhost:1025
  # -------------------------------------------------------------------------
  mailhog:
    image: mailhog/mailhog:v1.0.1
    container_name: sgpos_mailhog
    restart: unless-stopped
    ports:
      - "1025:1025"   # SMTP
      - "8025:8025"   # Web UI

  # -------------------------------------------------------------------------
  # 2.4  pgAdmin (optional but handy)
  # -------------------------------------------------------------------------
  pgadmin:
    image: dpage/pgadmin4:8
    container_name: sgpos_pgadmin
    restart: unless-stopped
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@sgpos.dev
      PGADMIN_DEFAULT_PASSWORD: admin
      TZ: Asia/Singapore
    volumes:
      - pgadmindata:/var/lib/pgadmin
    ports:
      - "5050:80"
    depends_on:
      db:
        condition: service_healthy

  # -------------------------------------------------------------------------
  # 2.5  App Worker
  #   • Runs Alembic migrations on start
  #   • Provides an interactive shell for scripts:
  #       docker compose exec app poe shell
  #   • Executes background tasks (Celery-if-present / custom asyncio worker)
  # -------------------------------------------------------------------------
  app:
    build:
      context: .
      dockerfile: Dockerfile
      target: dev  # ← multi-stage Dockerfile with `dev` stage
    container_name: sgpos_app
    ## To save start-up time we mount source code for live-reload
    volumes:
      - ./:/app
    command: |
      bash -c "
        poetry run alembic upgrade head &&
        echo '💾  Database migrated.' &&
        while true; do sleep 3600; done
      "
    env_file:                # keep secrets out of repo; optional
      - .env.dev             # fallback to values in &env-common
    environment:
      <<: *env-common
      EMAIL_HOST: mailhog
      EMAIL_PORT: "1025"
      LOG_LEVEL: DEBUG
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    profiles: ["tools"]       # not started by default without --profile tools

############################
# 3) Networks & Volumes
############################
networks:
  default:
    name: sgpos-net

volumes:
  pgdata:
  redisdata:
  pgadmindata:
```

### How to Use

1. **Start dependencies only**

   ```bash
   docker compose -f docker-compose.dev.yml up -d db redis mailhog
   ```

   That is usually enough to run the desktop client natively (`poetry run python app/main.py`).

2. **Start *all* services, including pgAdmin & app worker**

   ```bash
   docker compose -f docker-compose.dev.yml --profile tools up -d
   ```

3. **Run one-off commands inside `app`**

   ```bash
   docker compose exec app poetry run python scripts/seed_demo_data.py
   ```

4. **Tail logs**

   ```bash
   docker compose logs -f db app redis
   ```

### Why so many comments?

The goal is to make onboarding effortless for newcomers—every field answered *before* they have to ask. Feel free to strip comments once you are comfortable, but please keep them in the repository so the next contributor feels as welcomed as you did. 😉

Happy hacking!
