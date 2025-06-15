---
title: Getting Started
sidebar_position: 2
---

Learn how to set up Cracker for local development in less than 5 minutes.

## 1. Prerequisites

• Node.js ≥ 18 (use `nvm` or Volta).
• Yarn (recommended) or npm.
• Docker Desktop (to spin up Postgres & Redis automatically).

## 2. Clone & Install

```bash
# HTTPS or SSH — your choice
git clone https://github.com/<you>/cracker-mono.git
cd cracker-mono

# Install top-level dependencies (only Docusaurus right now)
yarn

# Install app/ dependencies
yarn --cwd app install
```

## 3. Configure Environment Variables

Copy the example files and tweak if necessary:

```bash
cp app/.env.example app/.env
```

`app/.env.example` already contains sane defaults for running everything against the local Docker network.

Important variables:

| Variable | Description |
| --- | --- |
| `DATABASE_URL` | Postgres connection string (set by `docker-compose`). |
| `REDIS_URL` | Redis connection string. |
| `NEXTAUTH_SECRET` | Used to encrypt session cookies. |
| `NEXTAUTH_URL` | Full URL of the Next.js server. |

## 4. Spin Up the Database Layer

Inside `app/` we provide a ready-to-go `docker-compose.yml`:

```bash
cd app
docker compose up -d postgres redis
```

This will start:

* **Postgres** ‑ `localhost:5432` (username: `postgres`, password: `postgres`).
* **Redis** ‑ `localhost:6379`.

## 5. Generate the Prisma Client & DB schema

```bash
# Still inside app/
yarn prisma migrate dev --name init
```

## 6. Run the Development Servers

```bash
# Start the Next.js webapp
cd app && yarn dev

# In a new terminal, start the docs site
cd docs && yarn start
```

Navigate to:

* `http://localhost:3000` – Cracker app.
* `http://localhost:3001` – Docs site (hot-reloading).

---

🎉 That's it! You have a fully-functioning Cracker stack running locally. 