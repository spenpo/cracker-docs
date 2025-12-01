---
title: Environment Variables
sidebar_position: 3
---

Cracker relies on several environment variables to configure connections to its backend services.

## Core Variables

These variables are typically set in your `.env` file or your deployment platform's dashboard.

| Variable | Description | Default (Local) |
| :--- | :--- | :--- |
| `DATABASE_URL` | Connection string for the PostgreSQL database. | `postgresql://postgres:postgres@localhost:5432/postgres` |
| `MONGODB_URI` | Connection string for the MongoDB instance (used for logs). | `mongodb://mongo:mongo@localhost:27017` |
| `REDIS_URL` | Connection string for the Redis cache. | `redis://localhost:6379` |
| `NODE_ENV` | The current Node.js environment. | `development` |

## Optional / Feature Flags

| Variable | Description |
| :--- | :--- |
| `PORT` | The port the Next.js server listens on (default: 3000). |
| `NEXT_PUBLIC_ANALYTICS_ID` | (Example) Public ID for analytics services. |

## Configuration for Docker

When running with `docker-compose`, these variables are often injected automatically or defined in the `docker-compose.yml` file within the `/server` directory.