---
title: Deployment
sidebar_position: 4
---

Production deployment can be done in multiple ways. Below are the officially supported targets — feel free to adapt to your stack of choice.

## Vercel (recommended)

The repository already contains a `vercel.json` file that configures:

* A single **Next.js** build with environment variables taken from the dashboard.
* An automatic production deployment on pushes to the `main` branch.

### Steps

1. Import the repo at <https://vercel.com/new>.
2. Add the environment variables listed in the [Env Vars](/docs/guide/environment) page.
3. Choose the `app/` directory as the root of the project (Vercel detects Next.js automatically).
4. Hit **Deploy**.

Vercel will:

* Run `yarn install` in `app/`.
* Build & cache the Next.js output.
* Run `prisma generate` automatically.

The GraphQL endpoint will live at `/api/graphql` and will be server-side rendered.

## Docker Compose (self-hosting)

Inside `app/server/` you can find a `docker-compose.production.yml` file that starts:

* `cracker_web` – Next.js app built for production.
* `postgres` – Postgres 15 with the same schema used in dev.
* `redis` – Redis 7.2 for caching.

```bash
cd app/server
docker compose -f docker-compose.production.yml up --build -d
```

The site will be available at `http://localhost:8080` (proxied through Nginx).

## Railway / Render / Fly.io

Because the repository is _container-ready_ you can deploy to any platform that supports Docker images. Use the provided `Dockerfile` in `app/` as your image source.

## Docs Site

The documentation is a static site; it can be deployed almost anywhere:

```bash
cd docs
yarn build # ⏱ creates static files in build/
```

Upload the `build/` directory to Vercel, Netlify, S3, Cloudflare Pages – you name it.

---

Need more guidance? Create an issue or open a discussion 🙌 