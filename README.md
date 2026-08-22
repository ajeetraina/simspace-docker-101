# Docker 101

An interactive, fully in-browser lab built on
[Simspace](https://github.com/dockersamples/simspace). Everything in the terminal
is simulated — no real Docker daemon, no images to pull, no network — so it runs
the same for everyone, with nothing to install. Click **Run** on any command and
watch it happen.

It's the hands-on companion to the **Docker 101** track of the
[Docker Workshop](https://dockerworkshop.vercel.app/) — the same concepts (inner
vs. outer loop, containers, Postgres, and the Product Catalog sample app), turned
into buttons you can click.

**What you learn**, across nine short sections:

1. **What Is a Container?** — the client/daemon model, and your first `docker run`
2. **Run Your First Web Server** — nginx, port publishing, `docker ps`, logs
3. **Run a Database** — Postgres with env vars and volumes, `docker exec`
4. **Images & Registries** — `pull`, `images`, `tag`, `history`
5. **Managing Containers** — `ps -a`, `logs`, `exec`, `stop`, `rm`
6. **Build Your Own Image** — write a Dockerfile for the Product Catalog and `docker build`
7. **Multi-Container Apps with Compose** — one file, the whole stack, `docker compose up`
8. **Conclusion** — where to go next

The lab lives under [`lab/docker-101/`](lab/docker-101/): `labspace.yaml` (config +
seeded virtual filesystem), `simulator.yaml` (command behaviour), and one markdown
file per section. It's loaded at runtime by a prebuilt image, so there's no build
step for content.

## Author locally

You only need Docker.

```bash
docker compose up dev              # live preview at http://localhost:5173
docker compose run --rm validate   # lint the lab (fails on errors)
```

Edit the files under `lab/docker-101/` and refresh the browser to see changes:

- `labspace.yaml` — title, terminals, seed files, sections, variables
- `simulator.yaml` — what each command does (scenarios)
- `*.md` — one file per section of instructions

Pin the toolchain to a released version for reproducibility:

```bash
export SIMSPACE_AUTHORING_IMAGE=dockersamples/simspace-authoring:1
```

## Deploy

**GitHub Pages (default):** enable Pages (Settings → Pages → Source: "GitHub
Actions"), then push to `main`. The workflow in
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) validates the lab
and publishes it. Pin `runtime-tag` there to a released version for a stable lab.
Pull requests are validated first by
[`.github/workflows/validate.yml`](.github/workflows/validate.yml).

**As a container:** the [`Dockerfile`](Dockerfile) bases on the runtime image and
swaps in your lab.

```bash
docker build -t docker-101-lab .
docker run --rm -p 8080:80 docker-101-lab    # http://localhost:8080
```

## Authoring with an AI agent

This repo is set up for agent authoring. In Claude Code, an `authoring-lab` skill
(under `.claude/`) knows the workflow, `docker compose` / `validate-lab` are
pre-allowed, and a hook auto-validates the lab after every edit under `lab/`.
[`CLAUDE.md`](CLAUDE.md) loads the guide automatically.

## Learn more

See [`AGENTS.md`](AGENTS.md) for an authoring cheat-sheet, and the
[Simspace specs](https://github.com/dockersamples/simspace/tree/main/spec) for the
full `simulator.yaml` / `labspace.yaml` reference.
