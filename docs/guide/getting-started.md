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
git clone https://github.com/<you>/cracker-web.git
cd cracker-web

# Install dependencies
yarn
```

## 3. Configure Environment Variables

Copy the example files and tweak if necessary:

```bash
cp .env.example .env
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

The repository ships with a ready-to-go `docker-compose.yml`:

```bash
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
yarn dev
```

Open `http://localhost:3000` in your browser — you should see Cracker running locally.

---

🎉 That's it! You have a fully-functioning Cracker stack running locally. 