# What Is a Container?

> Simply put, **containers are isolated processes**. Each of your app's components
> runs in its own container, isolated from everything else on the machine, yet
> sharing the host's kernel.

That last part is the key difference from a virtual machine. A VM ships a whole
operating system; a container shares the host kernel and only packages your app and
its dependencies. So containers are **smaller**, **start in milliseconds**, and you
can run **many** of them on one machine.

Containers are:

- **Self-contained** — each has everything it needs; no relying on what's preinstalled
- **Isolated** — one container can't interfere with another (or the host)
- **Independent** — start, stop, or delete one without touching the others
- **Portable** — the same container runs on your laptop and in the cloud

## The Docker architecture

Docker uses a **client–server** model:

| Piece | What it is |
|-------|------------|
| **Docker client** (`docker`) | The command you type. It sends requests… |
| **Docker daemon** (`dockerd`) | …to the daemon, which does the real work: building, running, and managing containers |
| **Registry** (e.g. Docker Hub) | Where **images** are stored and shared |

And the three core objects you'll meet everywhere:

- **Image** — a read-only template (your app + its dependencies), built in layers
- **Container** — a running instance of an image
- **Registry** — storage for images, like Docker Hub

## Check your setup

First, confirm the client and daemon are talking to each other:

```bash terminal-id=main
docker version
```

You can see a wider summary — how many images and containers exist, memory, and so
on — with:

```bash terminal-id=main
docker info
```

## Your first container

Time to run something. `docker run` pulls an image (if it isn't already local),
creates a container from it, and runs it:

```bash terminal-id=main
docker run hello-world
```

Read the output — it lists the exact steps Docker just took: the client contacted
the daemon, the daemon pulled the `hello-world` image from Docker Hub, created a
container from it, and streamed the result back to you. That's the whole model in
one command.

Now let's run something you can actually open in a browser. Continue to
**Run Your First Web Server**.
