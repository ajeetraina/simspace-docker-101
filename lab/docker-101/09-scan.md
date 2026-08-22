# Scan for Vulnerabilities

Your image builds, runs, and passes its tests. But **what's inside it?** A
`FROM node:20` base image pulls in an entire operating system and hundreds of
packages — most of which you never chose, and any of which could carry a known
vulnerability (a **CVE**).

**Docker Scout** answers the question *"what's in it, and what's wrong with it?"*

## A quick view

Point Scout at the image you built:

```bash terminal-id=main
docker scout quickview catalog-service:baseline
```

Read the vulnerability summary — the four numbers are **C**ritical / **H**igh /
**M**edium / **L**ow. You'll see something like `0C   8H   41M   93L`:

> **8 High** and dozens of Medium/Low vulnerabilities.

You didn't write a single
insecure line — these came in with the base image and the 431 packages it drags
along.

## Look at the actual CVEs

`quickview` gives the headline; `cves` names names:

```bash terminal-id=main
docker scout cves catalog-service:baseline
```

Each finding is a real, published CVE in a specific package and version. Some you
could fix by upgrading a dependency; many live in the base OS itself.

## The reactive treadmill

You *could* chase these one by one — upgrade a package, rebuild, rescan, repeat. But
new CVEs are published every day, and most of these vulnerabilities have nothing to
do with your code. You'd be patching an operating system you didn't want in the
first place.

> **The base image is the problem.** When ~90% of your vulnerabilities come from the
> base and packages you never use, the highest-leverage fix isn't patching — it's
> **starting from something smaller and hardened.**

That's exactly what you'll do next. Continue to **Harden It with DHI**.
