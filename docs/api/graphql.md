---
title: GraphQL Reference
sidebar_position: 1
---

Cracker exposes a single GraphQL endpoint at `/api/graphql` (relative to the Next.js deployment domain).

> All examples below assume the server is running at `http://localhost:3000`.

## Tooling

You can explore the schema with:

* **GraphiQL** – open [http://localhost:3000/api/graphql](http://localhost:3000/api/graphql) in the browser.
* **Apollo Studio** – import the endpoint and introspect.
* **VS Code GraphQL** extension – auto-complete & linting powered by the same schema.

## Schema Quick Look

```graphql
# src/graphql/schemas/index.ts gets auto-merged into this printable schema

"""A user in the system"""
type User {
  id: ID!
  email: String!
  createdAt: DateTime!
  plan: Plan!
}

"""Single track entry"""
type Track {
  id: ID!
  userId: ID!
  hours: Int!
  rating: Int!
  createdAt: DateTime!
}

"""Aggregate metrics for the dashboard"""
type DashboardMetrics {
  daysOfUse: Int!
  avgHours: Float!
  ratings: RatingsBreakdown!
}

# ... plus ~30 more types, inputs & enums
```

## Common Operations

### Register

```graphql
mutation Register($email: String!, $password: String!) {
  register(input: { email: $email, password: $password }) {
    user {
      id
      email
    }
    errors {
      field
      message
    }
  }
}
```

### Add a Track

```graphql
mutation AddTrack($hours: Int!, $rating: Int!) {
  uploadTracker(hours: $hours, rating: $rating) {
    track {
      id
      hours
      rating
    }
    errors {
      field
      message
    }
  }
}
```

### Get Dashboard Metrics

```graphql
query Metrics($runningAvg: String!) {
  dashboardMetrics(runningAvg: $runningAvg) {
    dashboardMetrics {
      daysOfUse
      avgHours
      ratings {
        countNegTwo
        countZero
        countPlusTwo
      }
    }
  }
}
```

## Error Handling Strategy

Each operation returns `{ data, errors }` following the Apollo-friendly pattern. Errors include a `field` key whenever possible, so you can map them to individual input components.

## Pagination

List fields are paginated with Relay-style connections (`edges`, `pageInfo`). Cursor-based pagination keeps requests fast even on large tables.

## Rate Limiting & Caching

* Heavy aggregation queries (e.g., `dashboardMetrics`) are cached in Redis under the key pattern `dashboardMetrics:<userId>:<runningAvg>`.
* Mutations automatically invalidate affected caches.

---

The full schema is generated at build time and committed under `app/generated/graphql.schema.json` – import it in your favourite tooling for type-safety! 