---
title: Deployment
sidebar_position: 4
---

Cracker is a standard Next.js application, which makes it flexible to deploy on various platforms. However, it requires access to running PostgreSQL, MongoDB, and Redis instances.

## Prerequisites

Before deploying the application code, ensure you have the following managed services (or containers) running and accessible:

*   **PostgreSQL**: Primary database.
*   **MongoDB**: Log database.
*   **Redis**: Cache store.

Set the connection strings for these services as environment variables (see [Environment Variables](/docs/guide/environment)) in your deployment target.

## Deployment Options

### 1. Vercel (Recommended for Frontend/API)

The easiest way to deploy the Next.js application is via [Vercel](https://vercel.com/).

1.  **Connect Repo**: Import your Cracker repository into Vercel.
2.  **Configure Envs**: Add `DATABASE_URL`, `MONGODB_URI`, and `REDIS_URL` to the project settings.
3.  **Deploy**: Vercel will automatically detect the Next.js framework and build the application.

> **Note**: You will need to host your databases (Postgres/Mongo/Redis) separately (e.g., via Supabase, MongoDB Atlas, Upstash) and provide the connection strings to Vercel.

### 2. Docker (Self-Hosted)

You can containerize the entire application for deployment on any VPS or container platform (AWS ECS, DigitalOcean, Fly.io).

**Build the Image:**

```bash
docker build -t cracker-app .
```

**Run the Container:**

Ensure the container has access to the network where your databases are running.

```bash
docker run -p 3000:3000 \
  -e DATABASE_URL=... \
  -e MONGODB_URI=... \
  -e REDIS_URL=... \
  cracker-app
```

### 3. Static Export (Not Supported)

Because Cracker relies on server-side GraphQL API routes and runtime database connections, `next export` (static site generation) is **not** fully supported for the entire application. The frontend can be statically optimized, but the `/api` routes require a Node.js runtime.

```