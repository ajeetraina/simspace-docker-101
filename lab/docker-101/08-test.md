# Test the App

Building and running an app proves it *starts*. Tests prove it *works*. The Product
Catalog has two kinds, and Docker makes both painless.

## Unit tests

Unit tests check individual functions in isolation — no database, no network. They
run in milliseconds:

```bash terminal-id=main
npm run unit-test
```

Fast and focused: they verify the business logic (like rejecting a duplicate SKU)
without any infrastructure.

## Integration tests with Testcontainers

Real bugs often hide in the *seams* between your app and the services it depends on —
the database, the message queue, object storage. To catch those, you need to test
against the **real** services, not mocks.

This is where Docker shines. The integration tests use **Testcontainers**: a library
that spins up throwaway Docker containers for Postgres, Kafka, and LocalStack, runs
the tests against them, then tears everything down automatically.

```bash terminal-id=main
npm run integration-test
```

Watch what happens:

1. **Testcontainers starts** real `postgres`, `kafka`, and `localstack` containers
2. It wires their **mapped ports** into the app's config (`DATABASE_URL`, `KAFKA_BROKER`)
3. The tests run against those **live services** — creating products, checking Kafka
   messages, uploading to S3
4. Every container is **torn down** at the end — no leftovers

> **Why this matters:** you get the fidelity of testing against real Postgres and
> real Kafka, with the convenience and isolation of containers. Every developer — and
> every CI run — gets the exact same environment, created fresh and thrown away.

The app is built, running, and verified correct. But there's a question we haven't
asked yet: **is it safe to ship?** Continue to **Scan for Vulnerabilities**.
