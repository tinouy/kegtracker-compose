# kegtracker-compose

This repository contains the **Docker Compose** configuration to run the full **KegTracker** system — a platform for managing kegs and breweries.

## Services

| Service   | Description              | Local Port |
|-----------|--------------------------|------------|
| Backend   | API built with FastAPI   | 8000       |
| Frontend  | Web app built in React   | 8080       |

## Requirements

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- A `.env` file with required variables (see below)

## Environment Variables

Create a `.env` file in the root with:

```env
# Backend
BACKEND_HOST=kegtracker-backend
BACKEND_PORT=8000
DB_ENGINE=sqlite
DB_URL=sqlite://./app/kegtracker.db
SECRET_KEY=your_secure_secret_key

# SMTP
SMTP_HOST=smtp.your-provider.com
SMTP_PORT=587
SMTP_USER=user@your-provider.com
SMTP_PASS=your-smtp-password
SMTP_FROM=KegTracker <no-reply@your-domain.com>

# Frontend
FRONTEND_HOST=kegtracker-frontend
FRONTEND_PORT=8080
FRONTEND_FQDN=http://localhost:8080
```

# Usage

```env
git clone https://github.com/youruser/kegtracker-deploy.git
cd kegtracker-deploy
cp .env.example .env  # if an example is available
# Edit .env
docker compose up -d
```

Then open:

- Frontend: http://localhost:8080/initialize
- Backend API (docs): http://localhost:8000/docs

# Persistence

SQLite database is stored as kegtracker.db in the root directory.
Backend is mounted with a volume for hot-reloading in development.

## Licencia

This software is distributed under the AGPL-3.0 license with an additional non-compete clause.
See [LICENSE](../LICENSE) for more details.

---

**Author:** tinouy 