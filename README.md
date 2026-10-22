# app-dev-project-cs-3-1

A monorepo containing a Laravel backend and a Next.js frontend.

> **Note:** `frontend/` and `backend/` are both tracked in this one repository. There are no
> nested Git repositories or submodules — the whole stack lives in this single repo and is
> committed and pushed together on the `main` branch.

## Requirements

- PHP 8.2+ with Composer
- Node.js 20+ with npm
- MySQL (for the `app_dev_project` database)

## Repository layout

```
.
├── backend/    # Laravel 12 (PHP) API
├── frontend/   # Next.js (TypeScript) app
└── README.md
```

---

## Backend (`backend/`)

Laravel 12 API server with Sanctum API token authentication.

```bash
cd backend

# Install PHP dependencies
composer install

# Create your environment file
copy .env.example .env        # Windows
# cp .env.example .env        # macOS / Linux

# Generate the application key
php artisan key:generate

# Run the database migrations
php artisan migrate

# Start the development server on http://localhost:8000
php artisan serve
```

The API is served from `http://localhost:8000`, with routes under `http://localhost:8000/api`.

### Backend environment

`backend/.env.example` ships with:

| Key | Value |
| --- | --- |
| `DB_CONNECTION` | `mysql` |
| `DB_DATABASE` | `app_dev_project` |
| `FRONTEND_URL` | `http://localhost:3000` |
| `SANCTUM_STATEFUL_DOMAINS` | `localhost:3000` |

Create the MySQL database before migrating:

```sql
CREATE DATABASE app_dev_project;
```

---

## Frontend (`frontend/`)

Next.js 16 App Router frontend written in TypeScript.

```bash
cd frontend

# Install dependencies
npm install

# Create your environment file
copy .env.example .env.local  # Windows
# cp .env.example .env.local  # macOS / Linux

# Start the development server on http://localhost:3000
npm run dev
```

The app is served from `http://localhost:3000`.

### Frontend environment

`frontend/.env.example` ships with:

| Key | Value |
| --- | --- |
| `NEXT_PUBLIC_API_URL` | `http://localhost:8000/api` |

---

## Running both together

Open two terminals:

```bash
# Terminal 1
cd backend && php artisan serve      # http://localhost:8000

# Terminal 2
cd frontend && npm run dev           # http://localhost:3000
```

CORS is configured in `backend/config/cors.php` to allow the frontend origin
`http://localhost:3000`.

---

## Git

Both `backend/` and `frontend/` are committed to this repository. Sensitive and generated
files are excluded via `.gitignore`:

- `backend/.env` and `backend/vendor/` are never tracked
- `frontend/node_modules/` and `frontend/.env.local` are never tracked
- `.env.example` files **are** tracked as templates
