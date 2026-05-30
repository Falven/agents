---
title: Run as Non-Root and Avoid Baking Secrets
impact: CRITICAL
impactDescription: reduces blast radius and prevents accidental secret disclosure
tags: dockerfile, security, nonroot, secrets, least-privilege
---

## Run as Non-Root and Avoid Baking Secrets

### Non-root runtime user (fixed UID/GID)

**Rule:** Final runtime stage runs as a non-root user.

```dockerfile
RUN groupadd -g 10001 app && useradd -m -u 10001 -g 10001 app
USER app
```

If your base image uses `adduser`/`addgroup` (Alpine):

```dockerfile
RUN addgroup -g 10001 -S app && adduser -u 10001 -S app -G app
USER app
```

### Ownership and writable paths

**Rule:** Only make writable what needs to be writable. Prefer `COPY --chown`.

```dockerfile
WORKDIR /app
COPY --chown=app:app --from=builder /app/dist ./dist
```

### Secrets hygiene

**Rule:** Never bake secrets into images:

- do not `ENV` secrets
- do not `ARG` secrets unless your build system mounts them securely
- prefer runtime mounts / secret stores

Bad:

```dockerfile
ARG DATABASE_URL
ENV DATABASE_URL=$DATABASE_URL
```

Good:

- inject at runtime via orchestrator secrets
- keep secrets out of layers and build logs

### Principle of least privilege

- minimize OS packages in runtime
- copy only artifacts you need
- avoid shells in runtime if not needed (optional, org-specific)
