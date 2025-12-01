---
title: Getting Started
sidebar_position: 2
---

This guide will help you set up the Cracker development environment on your local machine.

## Prerequisites

Ensure you have the following installed before proceeding:

*   **Node.js** (v18+ recommended)
*   **Yarn** (or npm)
*   **Docker & Docker Compose** (Required for backend services)

## Installation & Setup

Follow these steps to get the application running:

### 1. Install Dependencies

Navigate to the project root and install the required packages:

```bash
yarn install
```

### 2. Start Backend Infrastructure

Spin up the required backend services (PostgreSQL, MongoDB, Redis) using Docker Compose. This command also starts the admin tools (pgAdmin and Mongo Express).

```bash
yarn start:server
```

> **Note:** Ensure Docker Desktop (or the Docker daemon) is running before executing this command.

### 3. Start Development Server

Launch the Next.js development server:

```bash
yarn dev
```

You can now access the application at [http://localhost:3000](http://localhost:3000).

### 4. Generate GraphQL Types

Cracker uses `graphql-codegen` to generate TypeScript types from the GraphQL schema. Since the codegen process introspects the running GraphQL endpoint, **the development server must be running** (Step 3) for this to work.

In a separate terminal window, run:

```bash
yarn codegen
```

## Key Commands

Here are the most common commands you'll use during development:

| Command | Description |
| :--- | :--- |
| `yarn dev` | Starts the Next.js development server. |
| `yarn build` | Builds the application for production. |
| `yarn start:server` | Starts backend services (DBs, Cache) via Docker Compose. |
| `yarn codegen` | Generates GraphQL types based on schema and operations. |
| `yarn lint` | Runs ESLint. |
| `yarn it:db` | Access the running PostgreSQL container shell. |
| `yarn it:cache` | Access the running Redis CLI. |