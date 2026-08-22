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

| Section | You'll learn to… |
|---------|------------------|
| 1 | Understand containers and run your very first one |
| 2 | Run **nginx** as a web server and publish a port |
| 3 | Run a **PostgreSQL** database and talk to it |
| 4 | Pull, list, and tag **images** from a registry |
| 5 | Inspect, stop, and remove **containers** |
| 6 | **Build your own image** for a real Node.js app |
| 7 | Bring a whole stack up with **Docker Compose** |

You'll finish by containerising the **Product Catalog** — a small Node.js + Postgres
service that's waiting for you in this workspace.

Ready? Continue to **What Is a Container?**
