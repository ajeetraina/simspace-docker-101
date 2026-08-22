# Run a Database

Databases are one of the best reasons to use containers: no local install, no
version conflicts, and you can throw them away when you're done. Let's run
**PostgreSQL** — and to show off container isolation, we'll run **three versions at
once**.

## Start your first Postgres

```bash terminal-id=main
docker run -d --name postgres1 -e POSTGRES_PASSWORD=dev -p 5432:5432 postgres:16
```

The flags:

| Flag | Meaning |
|------|---------|
| `-d` | **Detached** — run in the background |
| `--name postgres1` | Name the container |
| `-e POSTGRES_PASSWORD=dev` | Set an **environment variable** — the Postgres image requires this one |
| `-p 5432:5432` | Publish the port (`host:container`) |
| `postgres:16` | Image **name and tag** — pin the major version instead of `latest` |

## Now run two more — different versions, side by side

Here's the payoff of isolation. Start Postgres **15** and **13** too. Each gets its
own name and its **own host port** (`5433`, `5434`), all mapping to `5432` inside
their container:

```bash terminal-id=main
docker run -d --name postgres2 -e POSTGRES_PASSWORD=dev -p 5433:5432 postgres:15
```

```bash terminal-id=main
docker run -d --name postgres3 -e POSTGRES_PASSWORD=dev -p 5434:5432 postgres:13
```

Three different PostgreSQL versions, running at the same time on one machine,
completely isolated from each other. Try *that* with a traditional install.

## See them all

```bash terminal-id=main
docker ps
```

You'll see `postgres1`, `postgres2`, and `postgres3` (plus the `web` server from
the last section) — each on its own published port.

## Connect and run queries

`docker exec` runs a command **inside** a container. Postgres ships with the `psql`
client, so you can query the database without installing anything locally.

**List the databases** (`\l` is psql's "list databases" meta-command):

```bash terminal-id=main
docker exec postgres1 psql -U postgres -c "\l"
```

**List the schemas** (`\dn`):

```bash terminal-id=main
docker exec postgres1 psql -U postgres -c "\dn"
```

**See what's connected right now** — a real SQL query against the `pg_stat_activity`
system view:

```bash terminal-id=main
docker exec postgres1 psql -U postgres -c "SELECT * FROM pg_stat_activity;"
```

That's the power of `exec`: you didn't need `psql` installed on your machine. It
lives inside the container, and you reached in to run it.

## Clean up

You don't need three databases for the rest of the lab. Because containers are
disposable, tearing them down is one command. `-f` forces removal even though
they're running:

```bash terminal-id=main
docker rm -f postgres1 postgres2 postgres3
```

Gone — no leftover processes, no config to undo. That disposability is the whole
point.

> **Run many versions at once.** Each container is isolated and gets its own
> published port, so `postgres:16`, `:15`, and `:13` never collide. This is how
> teams test against multiple database versions without a mess.

Next, you'll meet the real application you'll spend the rest of this lab on.
Continue to **Meet the Product Catalog**.
