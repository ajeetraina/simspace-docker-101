# Images & Registries

Every container you've run started from an **image**. An image is a read-only
template — your app plus its dependencies — built up in **layers**. Containers are
just running instances of images.

Images live in **registries**. The default is [Docker Hub](https://hub.docker.com),
a public registry with official images for nginx, Postgres, Node.js, and thousands
more.

## Pull an image

`docker run` pulls automatically, but you can fetch an image ahead of time with
`docker pull`:

```bash terminal-id=main
docker pull redis:7
```

Watch it download layer by layer. If you pull again, Docker reuses the layers it
already has — that's the layer cache at work.

## List your local images

```bash terminal-id=main
docker images
```

This shows every image on the machine, with its **repository**, **tag**, **image
ID**, and **size**. Notice how much bigger a database image (`postgres`) is than
`hello-world`.

## Tag an image

A tag is just a human-friendly pointer to an image. You'll tag images to give them a
name for your own registry, or to mark a version. The form is
`docker tag SOURCE TARGET`:

```bash terminal-id=main
docker tag nginx myname/nginx:v1
```

Run `docker images` again and you'll see `myname/nginx:v1` pointing at the **same
image ID** as `nginx` — a tag doesn't copy anything, it just adds a name.

## Peek inside the layers

Every line in a Dockerfile becomes a layer. See them with `docker history`:

```bash terminal-id=main
docker history nginx
```

Each row is a layer, its size, and the instruction that created it. This layered
structure is why images are efficient to store and fast to pull — shared layers are
only downloaded once.

> **Tag on purpose.** `latest` is convenient but moves over time. Pin a real tag
> (like `postgres:16`) so your builds are reproducible.

Now that you understand images, let's tidy up the containers you started. Continue
to **Managing Containers**.
