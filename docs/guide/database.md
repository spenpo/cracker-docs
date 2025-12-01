---
title: Database & Infrastructure
sidebar_position: 4
---

Cracker utilizes a robust local infrastructure managed via Docker Compose. This ensures that all necessary databases and caching services are available without manual installation.

## Services Overview

The platform relies on three primary backend services:

| Service | Type | Port | Usage |
| :--- | :--- | :--- | :--- |
| **PostgreSQL** | Relational DB | `5432` | Primary application data (Users, Metrics). |
| **MongoDB** | NoSQL DB | `27017` | Unstructured data and logs. |
| **Redis** | Key-Value Store | `6379` | Caching and session storage. |

## Access & Credentials

For local development, the following credentials are pre-configured in the docker-compose setup:

### PostgreSQL
*   **User**: `postgres`
*   **Password**: `postgres`
*   **Database**: `postgres`
*   **Port**: `5432`

### MongoDB
*   **User**: `mongo`
*   **Password**: `mongo`
*   **Port**: `27017`

### Redis
*   **Port**: `6379`
*   (No default password for local dev)

## Administration Tools

The project includes web-based administration tools for managing the databases. These are started automatically with `yarn start:server`.

### pgAdmin (PostgreSQL)
*   **URL**: [http://localhost:4000](http://localhost:4000)
*   **Login Email**: `spope@blockchains.com`
*   **Login Password**: `password`

### Mongo Express (MongoDB)
*   **URL**: [http://localhost:8081](http://localhost:8081)
*   **Credentials**: (Check `docker-compose.yml` if prompted, usually `admin` / `pass` or similar defaults).

## Management Commands

*   **Start Services**: `yarn start:server`
*   **Access Postgres Shell**: `yarn it:db`
*   **Access Redis CLI**: `yarn it:cache`