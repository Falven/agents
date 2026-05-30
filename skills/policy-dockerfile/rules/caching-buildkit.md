---
title: Cache Smartly with BuildKit
impact: HIGH
impactDescription: faster CI builds and local iteration
tags: dockerfile, buildkit, cache, performance, ci
---

## Cache Smartly with BuildKit

**Rule:** Structure Dockerfiles for maximum cache hits and use BuildKit cache mounts for package managers.

### 1) Copy lockfiles before source

Bad (cache busts on every source change):

```dockerfile
COPY . .
RUN pnpm install
```

Good:

```dockerfile
COPY package.json pnpm-lock.yaml ./
RUN corepack enable && pnpm install --frozen-lockfile
COPY . .
```

### 2) Use BuildKit cache mounts (when supported)

Node/pnpm example:

```dockerfile
# syntax=docker/dockerfile:1.7
RUN --mount=type=cache,target=/root/.local/share/pnpm/store \
    corepack enable && pnpm install --frozen-lockfile
```

Python/uv example:

```dockerfile
RUN --mount=type=cache,target=/root/.cache/uv \
    uv sync --frozen
```

### 3) Keep layers stable

- avoid embedding timestamps into build outputs
- avoid “download latest” steps without pinning
- avoid copying `.git` unless required

### 4) Prefer cacheable install patterns

- install deps in one layer
- build in a later layer
- copy artifacts into runtime stage

### 5) CI tip

If CI supports registry cache export/import, use it; otherwise BuildKit cache mounts still help significantly on the same runner.
