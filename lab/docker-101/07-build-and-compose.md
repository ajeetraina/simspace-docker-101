# Build & Run with Compose

Time to turn source into a running application. First you'll **build** the image,
then bring the **whole stack** up with Compose.

## Build the image

The `docker build` command reads the `Dockerfile` and produces an image. `-t` tags
it (`catalog-service:baseline`), and the `.` is the build context — the current
directory:

```bash terminal-id=main
docker build -t catalog-service:baseline .
```

It resolves several hundred npm packages and bakes them into the image. When it
finishes, confirm it exists:

```bash terminal-id=main
docker images
```

There's `catalog-service:baseline` — **1.1GB**. Hold that number; it matters later.

## One app, many services

The Product Catalog isn't just the API — it needs Postgres, Kafka, LocalStack, and
WireMock, plus a web client. Starting all of those with `docker run` by hand would
be painful. That's what **Docker Compose** is for: the `compose.yaml` in this
project describes every service, its image or build, ports, and how they depend on
each other.

Bring the entire stack up with one command:

```bash terminal-id=main
docker compose up -d
```

Compose starts every service on a shared network where they find each other by
name (the backend reaches the database at the hostname `postgres`, not an IP). Check
what's running:

```bash terminal-id=main
docker compose ps
```

## Use it

The API is published on port `3000`. Ask it for the products:

```bash terminal-id=main
curl http://localhost:3000/api/products
```

The stack also exposes some handy UIs (in a real Docker Desktop you'd open these in
a browser):

| URL | What |
|-----|------|
| http://localhost:5173 | Web client — create and view products |
| http://localhost:5050 | pgAdmin — inspect the PostgreSQL database |
| http://localhost:8080 | Kafka UI — watch "product created" events |

Tail the combined logs from every service in one stream:

```bash terminal-id=main
docker compose logs
```

> **`compose.yaml` is your app as code.** The same file works on your laptop and in
> CI. Anyone can bring the whole system up with `docker compose up`.

The app builds and runs. But does it actually *work correctly*? Let's prove it.
Continue to **Test the App**.
