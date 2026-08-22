# Run a Database

Databases are one of the best reasons to use containers: no local install, no
version conflicts, and you can throw them away when you're done. Let's run
**PostgreSQL**.

## Start Postgres

```bash terminal-id=main
docker run --name postgres1 -d -e POSTGRES_PASSWORD=dev -p 5432:5432 postgres:16
```

One new flag joins the ones you already know:

| Flag | Meaning |
|------|---------|
| `-e POSTGRES_PASSWORD=dev` | Set an **environment variable** inside the container. The Postgres image requires this one to initialise |
| `postgres:16` | The image **name and tag** — pin the major version instead of `latest` |

## Both containers are running now

You started `web` in the last section and `postgres1` just now. Confirm both:

```bash terminal-id=main
docker ps
```

Two containers, side by side, fully isolated from each other — each on its own
published port (`8080` and `5432`).

## Run a command inside the container

`docker exec` runs a command **inside** an already-running container. Let's list
the databases Postgres created, using its built-in `psql` client:

```bash terminal-id=main
docker exec postgres1 psql -U postgres -c "\l"
```

That's the power of `exec` — you didn't need `psql` installed on your machine. It
lives inside the container, and you reached in to run it.

> **Run many versions at once.** Because each container is isolated and gets its own
> published port, you could start `postgres:16`, `postgres:15`, and `postgres:13`
> together — on ports `5432`, `5433`, `5434` — without them ever colliding.

Leave both containers running. Next you'll look at the images they came from.
Continue to **Images & Registries**.
