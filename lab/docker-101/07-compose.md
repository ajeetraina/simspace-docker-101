# Multi-Container Apps with Compose

The Product Catalog is really **two** services: the API you built, and the Postgres
database it talks to. Starting each one with a long `docker run` command — remembering
every flag, name, and port — gets old fast.

**Docker Compose** lets you describe the whole application in one file and bring it
all up with a single command.

## Describe the stack

A `compose.yaml` file lists your **services**, how to build or pull each one, their
ports, environment, and how they depend on each other. Save this one:

```yaml save-as=compose.yaml
services:
  backend:
    build: .                       # build from the Dockerfile you just wrote
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgres://postgres:dev@db:5432/postgres
    depends_on:
      - db

  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: dev
```

Two things to notice:

- The backend reaches the database at the hostname **`db`** — Compose puts every
  service on a shared network where they find each other **by service name**. No IP
  addresses, no `-p` needed between them.
- `depends_on` tells Compose to start `db` before `backend`.

## Bring it all up

One command builds what needs building and starts everything:

```bash terminal-id=main
docker compose up -d
```

Both containers start together. Check them with Compose's own status view:

```bash terminal-id=main
docker compose ps
```

## It works the same way

The API is published on port `3000`, exactly as before — but now its database came
up alongside it, wired together automatically:

```bash terminal-id=main
curl http://localhost:3000/api/products
```

View the combined logs from every service in one stream:

```bash terminal-id=main
docker compose logs
```

## Tear it down

When you're done, one command stops and removes the whole stack — containers and
network:

```bash terminal-id=main
docker compose down
```

> **One file, one command.** `compose.yaml` is the same whether you're on your
> laptop or wiring the app into CI. Check it into your repo and anyone can bring the
> entire application up with `docker compose up`.

You've come full circle — from a single `hello-world` to a multi-service app defined
as code. Continue to the **Conclusion**.
