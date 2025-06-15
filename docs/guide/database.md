---
:title: Database
:sidebar_position: 4
---

# Database

Cracker stores data in a relational database accessed through **Prisma ORM** plus a few raw SQL calls.

## Supported engines

* **MySQL 8** – officially supported and used in production.
* **PostgreSQL 15** – works as well, but you need to tweak the Prisma schema (see `schema.prisma`).

## Local development

1. Create an empty database.
2. Fill `DATABASE_URL` (and `DIRECT_URL` if you use Prisma Accelerate) in `.env`.
3. Run `yarn prisma migrate reset --force` – this recreates all 7 tables defined in `/prisma/migrations/`.

## Prisma Accelerate (optional)

In production we plan to use [Prisma Accelerate](https://www.prisma.io/docs/accelerate) to improve query performance. That's why the default `.env.example` shows a `prisma://…` URL. For local development you can simply point both `DATABASE_URL` and `DIRECT_URL` at the same MySQL connection string.

## Baseline migrations

The very first migration (`0_init`) is the **baseline** that mirrors the current production schema. After cloning a prod database remember to run `prisma migrate diff` if you need to baseline it again.

## Docker images (⚠️ WIP)

There are Dockerfiles and SQL scripts in `server/database/` for both MySQL and Postgres. They build successfully, but the accompanying `docker-compose.yml` still needs adjustments. Feel free to contribute fixes!

## WordPress content

Some pages inside the app pull blog content from a WordPress install (see `WP_ROOT` env var). This is **optional** and can be stripped out if you don't need embedded blog posts. 