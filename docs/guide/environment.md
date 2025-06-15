---
title: Environment Variables
sidebar_position: 3
---

A quick reference of all environment variables used across the monorepo.

## Next.js App (`app/.env`)

| Variable | Example | Required | Notes |
| --- | --- | :---: | --- |
| `NODE_ENV` | `development` | ✓ | Set automatically by the framework.
| `PORT` | `3000` |  | Custom port for Next.js server. |
| `DATABASE_URL` | `postgresql://postgres:postgres@localhost:5432/cracker` | ✓ | Used by Prisma & raw SQL pool. |
| `REDIS_URL` | `redis://localhost:6379` | ✓ | Used for caching & sessions. |
| `NEXTAUTH_SECRET` | `super-secret-key` | ✓ | Should be random & unique per environment. |
| `NEXTAUTH_URL` | `http://localhost:3000` | ✓ | Public URL where NextAuth callbacks will redirect. |
| `GRAPHQL_ENDPOINT` | `/api/graphql` |  | Used by Apollo Client on the frontend. |

## Docs Site (`docs/.env`)

No runtime secrets are required. All content is static and is compiled at build time. If you plan to deploy the docs separately you can manipulate:

| Variable | Default | Notes |
| --- | --- | --- |
| `SITE_URL` | `https://docs.cracker.dev` | Used for SEO and sitemap generation. |

## CI/CD Secrets

When deploying to hosted environments (e.g. Vercel, Railway) remember to provide the same variables in the dashboard or via your CI provider's secret store.

👉 Tip: use a `.env.local` file for overrides that should **never** be committed to Git. 