# Conclusion

You did it. 🎉 In one sitting you went from *"what is a container?"* to running a
real, multi-service application defined entirely as code.

## What you learned

| You can now… | Using |
|--------------|-------|
| Understand containers vs. VMs and the client/daemon model | `docker version`, `docker info` |
| Run a container | `docker run`, `hello-world` |
| Run a web server and publish a port | `docker run -d -p`, `curl` |
| Run a database and exec into it | `docker run -e`, `docker exec` |
| Work with images and registries | `docker pull`, `images`, `tag`, `history` |
| Manage the container lifecycle | `docker ps -a`, `logs`, `stop`, `rm` |
| Build your own image from a Dockerfile | `docker build -t` |
| Run a whole stack with one file | `docker compose up` / `down` |

## The mental model to keep

- **Image** = the recipe (built in layers, from a `Dockerfile`)
- **Container** = a running instance of an image
- **Registry** = where images are shared (Docker Hub)
- **Compose** = your whole app, described in one file

That's the foundation everything else builds on.

## Where to go next

- **Multi-stage builds & smaller images** — shrink that `product-catalog` image
  dramatically by separating build tools from the runtime.
- **Volumes & persistence** — keep your database data across container restarts.
- **Networking** — custom networks, service discovery, and connecting stacks.
- **Security & supply chain** — scan images, generate SBOMs, and start from
  hardened base images. A great next lab is
  [**Securing the Agentic Stack**](https://github.com/ajeetraina/simspace-agentic-security),
  which picks up this exact Product Catalog app and hardens it.
- Explore the full [**Docker Workshop**](https://dockerworkshop.vercel.app/) for
  tracks on Docker & AI, MCP, Kubernetes, and more.

## Keep the momentum

Everything you ran here works the same on a real machine — install
[Docker Desktop](https://www.docker.com/products/docker-desktop/) and try building
and running the Product Catalog for real.

Thanks for working through **Docker 101**. Now go containerise something of your
own. 🐳
