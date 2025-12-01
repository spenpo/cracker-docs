---
title: GraphQL API
sidebar_position: 1
---

Cracker exposes a single flexible **GraphQL** endpoint at `/api/graphql`. This API is the primary method for data fetching and manipulation in the frontend.

## Tech Stack

*   **TypeGraphQL**: The API schema is built using a "code-first" approach. Instead of writing separate `.graphql` schema files, we define TypeScript classes and decorate them. TypeGraphQL generates the schema from these classes.
*   **Apollo Server**: Serves the GraphQL API within a Next.js API route.
*   **GraphQL Codegen**: Generates TypeScript types for the frontend based on the backend schema and client-side queries.

## Workflow

### 1. Defining the Schema (Backend)
Schema definitions and resolvers live in `src/graphql`. When you modify a resolver or input type, you are directly modifying the API contract.

**Example (Conceptual):**
```typescript
@Resolver()
export class CreativityResolver {
  @Query(() => [Metric])
  async getMetrics(): Promise<Metric[]> {
    // Business logic here
  }
}
```

### 2. Generating Types (Frontend)
After modifying the backend schema (resolvers/types), you must regenerate the frontend TypeScript types to ensure type safety across the application.

**Command:**
```bash
yarn codegen
```

> **Requirement:** The development server (`yarn dev`) must be running because the codegen tool introspects the live GraphQL endpoint (usually `http://localhost:3000/api/graphql`).

### 3. Using the API (Frontend)
The frontend uses **Apollo Client** to consume the API. The generated types from step 2 allow for fully typed hooks and queries.

## Endpoint
*   **URL**: `/api/graphql`
*   **Method**: `POST`

## Tools
*   **Playground**: You can explore the API schema and test queries using the GraphQL Playground (or Apollo Sandbox) by visiting `http://localhost:3000/api/graphql` in your browser while the server is running.