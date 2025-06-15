---
title: Overview
sidebar_position: 1
---

This page gives you a bird's-eye view of the Cracker codebase.

```mermaid
graph TD
    subgraph Frontend
        A[Next.js 14] -- Apollo Client --> B[GraphQL API]
        A -- REST \n Auth --> C[/api/auth]
    end
    subgraph Backend
        B -- TypeGraphQL --> D[Resolvers]
        D --> E[Prisma ORM]
        D --> F[Raw SQL Pool]
        E --> G[(Postgres)]
        F --> G
        D --> H[Redis Cache]
    end
```

## Key Packages

| Location | Tech | Purpose |
| --- | --- | --- |
| `app/` | Next.js, TypeScript | Web UI & API routes |
| `app/graphql` | TypeGraphQL | GraphQL schema & resolvers |
| `app/prisma` | Prisma | Database schema & migrations |
| `app/utils` | Redis, Postgres pool | Cross-cutting utilities |
| `docs/` | Docusaurus | This documentation site |

## Data Flow

1. The React UI issues GraphQL operations via Apollo.
2. API requests hit `/api/graphql` (Next.js edge-compatible handler).
3. Resolvers execute business logic, fetching data from Postgres either through Prisma or raw SQL functions.
4. Frequently accessed payloads are cached in Redis.
5. Responses are returned to the client; the UI updates optimistically.

## Domain Modules

* **Track** – capture daily creative hours & rating.
* **Dashboard** – compute aggregated metrics (via SQL Stored Procedures).
* **Auth** – powered by NextAuth with JWT sessions.
* **Feature Flags** – simple on/off flags stored in the database and piped to the client.

## Serverless Friendly

All heavyweight resources (Postgres, Redis) live outside the Next.js runtime — you can deploy the app to Vercel, Fly, or any serverless platform without changes.

## Future Improvements

* Adopt **tRPC** for type-safe API calls.
* Introduce **Vitest** for unit & integration tests.
* Add **OpenTelemetry** instrumentation for end-to-end tracing.

---

For implementation details jump into the source folders or continue with the [API docs](/docs/api/graphql). 