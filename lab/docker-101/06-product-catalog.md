# Meet the Product Catalog

You've learned the fundamentals on ready-made images. Now you'll apply them to a
**real application** and follow it through the whole software development lifecycle:
**develop → build → test → secure**.

## The app

The **Product Catalog** (`catalog-service-node`) is a small but realistic
microservice. It's a Node.js REST API over a PostgreSQL product database, wired to a
few supporting services — exactly the shape of a real backend:

| Piece | Technology | Role |
|-------|-----------|------|
| Backend API | Node.js + Express | Serves `/api/products` |
| Database | PostgreSQL | Stores the products |
| Events | Kafka | Publishes "product created" messages |
| Object storage | LocalStack (S3) | Stores product images |
| Upstream API | WireMock | Mocks an external pricing service |
| Frontend | React (Vite) | A simple web client |

## Clone it

Grab the project — the same way you would on a real laptop:

```bash terminal-id=main
git clone $$repo$$
```

## Look around

The project is now in your workspace. Get the lay of the land:

```bash terminal-id=main
tree
```

It ships with a **`Dockerfile`** and a **`compose.yaml`** already — so someone has
containerised it. Read the Dockerfile to see how:

```bash terminal-id=main
cat Dockerfile
```

Notice `FROM node:20` — a full Node base image. It works, but as you'll see when
you scan it later, "works" and "secure" are not the same thing.

Now open the service code that turns a request into a database query and a Kafka
event:

```bash terminal-id=main
cat src/services/ProductService.js
```

That's the app. Over the next four sections you'll **build** it, **run** the whole
stack, **test** it, **scan** it, and **harden** it.

Continue to **Build & Run with Compose**.
