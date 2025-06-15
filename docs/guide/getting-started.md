---
title: Getting Started
sidebar_position: 2
---

Learn how to set up Cracker for local development in less than 5 minutes.

## 1. Prerequisites

• Node.js ≥ 18 (use `nvm` or Volta).
• Yarn (recommended) or npm.
• MySQL ≥ 8 (or Postgres 15).
• Redis ≥ 7.
• Docker Desktop (optional) if you prefer containers for MySQL/Redis.

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

If you prefer containers, there's a partial **work-in-progress** compose file under `server/`. It currently needs a little debugging for MySQL support — contributions welcome! In the meantime you can start both services manually:

```bash
# Redis
docker run --name redis -p 6379:6379 -d redis:7

# MySQL 8 (with a blank root password for local dev)
docker run --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -p 3306:3306 -d mysql:8
```

## 5. Generate the Prisma Client & DB schema

# Initialize the schema (creates 7 tables)
yarn prisma migrate reset --force

## 6. Run the Development Servers

```bash
# Start the Next.js webapp
yarn dev
```

Open `http://localhost:3000` in your browser — you should see Cracker running locally.

> ⚠️  Some advanced features (e.g. Docker Compose setup, WP-powered content pages) are **work in progress**. Check the README or open issues for the latest status.

---

🎉 That's it! You have a fully-functioning Cracker stack running locally. 