# Managing Containers

You've got `web` and `postgres1` running. Real work means inspecting containers,
reading their output, and cleaning them up when you're done. This is the container
**lifecycle**.

## See everything, including stopped containers

`docker ps` shows only **running** containers. Add `-a` to see **all** of them —
including ones that have exited, like the `hello-world` container from Section 1:

```bash terminal-id=main
docker ps -a
```

Notice `hello-world` sitting there with status `Exited (0)`. A container that
finishes its command stops but isn't deleted — it stays until you remove it.

## Look inside a running container

You already used `docker exec` on Postgres. Here it is again to peek at the files
nginx serves:

```bash terminal-id=main
docker exec web ls /usr/share/nginx/html
```

## Read the logs

```bash terminal-id=main
docker logs web
```

`docker logs` is your first stop whenever a container misbehaves — it shows exactly
what the process printed.

## Stop containers

Stopping a container halts its process but keeps the container around (you could
start it again):

```bash terminal-id=main
docker stop web
```

```bash terminal-id=main
docker stop postgres1
```

Run `docker ps` and you'll see the list is empty — nothing is running now.

```bash terminal-id=main
docker ps
```

## Remove containers

To reclaim the names and clean up, remove the stopped containers:

```bash terminal-id=main
docker rm web
```

```bash terminal-id=main
docker rm postgres1
```

> **Lifecycle in four verbs:** `run` (create + start) → `stop` (halt) → `rm`
> (delete). Add `--rm` to `docker run` and Docker removes the container
> automatically when it exits.

Your machine is clean. Now for the main event — a **real application** you'll take
all the way from source to a hardened, scanned image. Continue to **Meet the
Product Catalog**.
