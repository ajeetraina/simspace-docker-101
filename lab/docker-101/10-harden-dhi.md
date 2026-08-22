# Harden It with DHI

The baseline image had **8 High** vulnerabilities — almost all from a big `node:20`
base and packages you never chose. Instead of patching them one by one, you'll swap
the foundation.

## What's a Docker Hardened Image?

**Docker Hardened Images (DHI)** are minimal, security-first base images maintained
by Docker. In a nutshell, they are:

- **Minimal** — only what's needed to run your app, so far fewer packages (and far
  fewer CVEs)
- **Distroless at runtime** — no shell, no package manager, runs as non-root, so
  there's very little to attack
- **Near-zero known vulnerabilities** — continuously scanned and patched

You don't need to learn the internals here. The point of this section is simple:
**see what happens to the numbers when you start from a hardened base.**

## Write a hardened Dockerfile

This is a **multi-stage** build: a `-dev` variant (with the toolchain) installs
dependencies, then only the app and its `node_modules` are copied into a tiny,
distroless runtime. Save it:

```dockerfile save-as=Dockerfile.dhi
# --- build stage: has a shell, npm, and build tools ---
FROM dhi.io/node:24-debian13-dev AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --production --ignore-scripts

# --- runtime stage: distroless, non-root, no shell, no npm ---
FROM dhi.io/node:24-debian13
WORKDIR /app
COPY --from=build /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
CMD ["node", "src/index.js"]
```

## Build the hardened image

```bash terminal-id=main
docker build -t catalog-service:dhi -f Dockerfile.dhi .
```

## Measure it

Run the exact same scan you ran before — this time on the hardened image:

```bash terminal-id=main
docker scout quickview catalog-service:dhi
```

This time the summary reads `0C   0H   1M   4L`.

> From **8 High** to **0 High**. Same application, different foundation.

## See the before/after side by side

```bash terminal-id=main
docker scout compare catalog-service:dhi --to catalog-service:baseline
```

Look at the deltas:

| | Baseline | DHI |
|---|---|---|
| **High CVEs** | 8 | **0** |
| Medium | 41 | 1 |
| Low | 93 | 4 |
| Packages | 431 | **78** |
| Size | 1.1GB | **248MB** |

Confirm both images are on your machine:

```bash terminal-id=main
docker images
```

> **This is the payoff.** You didn't rewrite the app or chase individual CVEs. You
> changed one thing — the base image — and the vulnerability count fell to
> near-zero while the image got **77% smaller**. Starting from a hardened base is
> the highest-leverage security decision you can make.

You've taken a real app through the entire lifecycle. Continue to the
**Conclusion**.
