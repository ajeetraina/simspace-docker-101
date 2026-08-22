# Conclusion

You did it. 🎉 You started with *"what is a container?"* and finished by taking a
real application through its entire software development lifecycle — **develop,
build, test, and secure** — all in your browser.

## What you learned

**Part 1 — fundamentals**

| You can now… | Using |
|--------------|-------|
| Understand containers vs. VMs and the client/daemon model | `docker version`, `docker info` |
| Run a container, a web server, and a database | `docker run`, `-d`, `-p`, `-e` |
| Work with images and registries | `docker pull`, `images`, `tag`, `history` |
| Manage the container lifecycle | `docker ps -a`, `logs`, `exec`, `stop`, `rm` |

**Part 2 — the Product Catalog SDLC**

| You can now… | Using |
|--------------|-------|
| Clone and explore a real project | `git clone`, `tree`, `cat` |
| Build an image and run a full stack | `docker build`, `docker compose up` |
| Test against real services | `npm run unit-test` / `integration-test` (Testcontainers) |
| Find vulnerabilities | `docker scout quickview` / `cves` |
| Cut them to near-zero | Docker Hardened Images + `docker scout compare` |

## The one number to remember

| | Baseline (`node:20`) | Hardened (DHI) |
|---|---|---|
| **High CVEs** | 8 | **0** |
| Packages | 431 | 78 |
| Size | 1.1GB | 248MB |

Same app. One change — the base image — and vulnerabilities dropped to near-zero.

## The mental model to keep

- **Image** = the recipe (built in layers, from a `Dockerfile`)
- **Container** = a running instance of an image
- **Registry** = where images are shared (Docker Hub, DHI)
- **Compose** = your whole app, described in one file
- **Scout** = *what's in my image, and what's wrong with it?*
- **DHI** = start from a hardened base, and most of "what's wrong" disappears

## Where to go next

- **Go deeper on supply-chain security** — SBOMs, provenance, signing, and
  policy gates in CI. The natural next lab is
  [**Securing the Agentic Stack**](https://ajeetraina.github.io/simspace-agentic-security/),
  which picks up this exact Product Catalog and hardens the whole pipeline.
- Explore the full [**Docker Workshop**](https://dockerworkshop.vercel.app/) for
  tracks on Docker & AI, MCP, Kubernetes, and more.
- Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) and run
  the Product Catalog for real.

Thanks for working through **Docker 101**. Now go containerise something of your
own. 🐳
