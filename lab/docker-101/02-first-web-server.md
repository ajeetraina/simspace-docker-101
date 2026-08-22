# Run Your First Web Server

`hello-world` printed a message and exited. Real services keep running in the
background and listen for requests. Let's run **nginx**, a popular web server.

## Run nginx in the background

```bash terminal-id=main
docker run --name web -d -p 8080:80 nginx
```

Three new flags — worth knowing by heart:

| Flag | Meaning |
|------|---------|
| `--name web` | Give the container a friendly name (`web`) instead of a random one |
| `-d` | **Detached** — run in the background and return your prompt |
| `-p 8080:80` | **Publish** a port: `host:container`. Traffic to port `8080` on your machine goes to port `80` inside the container |

The long string it prints is the container's unique ID.

## See it running

```bash terminal-id=main
docker ps
```

`docker ps` lists **running** containers. You should see `web`, based on the `nginx`
image, with its port mapping `0.0.0.0:8080->80/tcp`.

## Talk to it

Because you published port `8080`, you can reach the server from the host:

```bash terminal-id=main
curl http://localhost:8080
```

That HTML is nginx's welcome page, served from inside the container. 🎉

## Check the logs

Anything a container writes to stdout/stderr, Docker captures. View it with
`docker logs` and the container's name:

```bash terminal-id=main
docker logs web
```

You'll see nginx's startup lines and the request your `curl` just made.

> **Port mapping is the bridge.** Without `-p`, the container's port 80 is only
> reachable *inside* Docker's network. Publishing it makes it reachable from your
> machine.

Leave `web` running — you'll manage it later. Next, a database. Continue to
**Run a Database**.
