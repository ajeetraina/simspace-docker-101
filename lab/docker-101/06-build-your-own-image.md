# Build Your Own Image

So far you've run images other people built. Now you'll build one — for a **real
application** sitting in this workspace: the **Product Catalog**, a Node.js REST API
backed by PostgreSQL.

## Explore the project

Have a look at what's here:

```bash terminal-id=main
tree
```

It's a normal Node.js app — a `package.json`, source under `src/`, a database
schema, and a `frontend/`. Read the entry point:

```bash terminal-id=main
cat src/index.js
```

Notice one thing: **there's no Dockerfile.** The app can't be containerised until
you write one. Let's do that.

## Write a Dockerfile

A **Dockerfile** is a recipe: each line is an instruction that becomes an image
layer. Save this one to the project root by clicking **Save**:

```dockerfile save-as=Dockerfile
# Start from an official Node.js base image (slim = smaller).
FROM node:20-slim

# Everything below happens inside this directory in the image.
WORKDIR /app

# Copy just the manifests first, so the slow npm install layer is cached
# and only re-runs when dependencies actually change.
COPY package*.json ./
RUN npm install --production

# Now copy the rest of the source.
COPY . .

# Document the port the app listens on.
EXPOSE 3000

# The command that runs when a container starts.
CMD ["node", "src/index.js"]
```

Each instruction earns its place:

| Instruction | What it does |
|-------------|--------------|
| `FROM` | The base image to build on |
| `WORKDIR` | Sets the working directory inside the image |
| `COPY` | Copies files from your project into the image |
| `RUN` | Executes a command at **build** time (here, installing dependencies) |
| `EXPOSE` | Documents which port the app uses |
| `CMD` | The command that runs when the container **starts** |

## Build the image

`docker build` reads the Dockerfile and produces an image. `-t` **tags** it with a
name, and the `.` tells Docker to build using the current directory as context:

```bash terminal-id=main
docker build -t $$image$$ .
```

Watch each instruction become a build step. When it finishes, your image exists:

```bash terminal-id=main
docker images
```

There's `product-catalog` at the top of the list — an image **you** built.

## Run your image

```bash terminal-id=main
docker run --name catalog -d -p 3000:3000 $$image$$
```

Confirm it's up, then call its API:

```bash terminal-id=main
docker ps
```

```bash terminal-id=main
curl http://localhost:3000/api/products
```

The JSON came from **your** container. And if anything looked off, you already know
where to look:

```bash terminal-id=main
docker logs catalog
```

> You built an image from source and ran it — the same artifact that would flow
> through CI into production. That's the inner loop meeting the outer loop.

But this app needs a database to be truly useful, and starting each container by
hand gets tedious. There's a better way. Continue to **Multi-Container Apps with
Compose**.
