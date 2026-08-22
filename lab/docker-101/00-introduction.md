# Docker 101

Welcome. Over the next hour you'll go from *"what is a container?"* to running a
real multi-service application — entirely in your browser. There is **nothing to
install**. Every command in this lab runs against a simulator, so the output is the
same for everyone and nothing can break.

Click the **Run** button on any command block (or type it yourself in the terminal
on the right) and watch it execute.

## Why Docker?

A container packages your application together with everything it needs to run —
the code, a runtime, system tools, and libraries — into a single, portable unit.
That unit runs the same way on your laptop, a teammate's machine, and in
production.

> **Build once, run anywhere.** No more *"but it works on my machine."*

## Inner loop and outer loop

Development has two rhythms, and Docker helps with both:

| Loop | What happens | Pace |
|------|--------------|------|
| **Inner loop** | You write, build, and debug code on your own machine | Fast, frequent changes |
| **Outer loop** | Code is integrated, reviewed, tested, and deployed | Slower, stability-focused |

The **inner loop** is where you'll spend most of this lab — spinning containers up,
inspecting them, and iterating. The same images you build here are exactly what
flow through the outer loop into production.

## What you'll do

**Part 1 — Docker fundamentals**

| Section | You'll learn to… |
|---------|------------------|
| 1 | Understand containers and run your very first one |
| 2 | Run **nginx** as a web server and publish a port |
| 3 | Run **PostgreSQL** — several versions at once — and query it |

**Part 2 — a real app, end to end (the Product Catalog SDLC)**

| Section | You'll learn to… |
|---------|------------------|
| 4 | **Clone** the Product Catalog and explore it |
| 5 | **Build** its image and run the whole stack with **Compose** |
| 6 | **Test** it with unit and integration (Testcontainers) tests |
| 7 | **Scan** it for vulnerabilities with **Docker Scout** |
| 8 | **Harden** it with a **Docker Hardened Image** — vulnerabilities near-zero |

The star of Part 2 is the **Product Catalog** — a real Node.js service (Postgres,
Kafka, LocalStack, WireMock) that's waiting for you in this workspace. You'll follow
it through the whole software development lifecycle: **develop → build → test →
secure**.

Ready? Continue to **What Is a Container?**
