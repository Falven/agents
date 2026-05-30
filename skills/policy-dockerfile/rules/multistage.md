---
title: Multi-Stage Builds by Default
impact: HIGH
impactDescription: smaller images, faster pulls, reduced attack surface
tags: dockerfile, multistage, build, security, performance
---

## Multi-Stage Builds by Default

**Rule:** Use multi-stage builds unless you have a strong reason not to.

### Why

- builder contains compilers and tooling; runtime stays minimal
- smaller images = faster CI + deploy + cold start
- fewer packages in runtime = fewer CVEs

### Pattern

```dockerfile
# syntax=docker/dockerfile:1.7

FROM node:20-bookworm AS builder
WORKDIR /app

# Install deps first (cache-friendly)
COPY package.json pnpm-lock.yaml ./
RUN corepack enable && pnpm install --frozen-lockfile

# Copy source and build
COPY . .
RUN pnpm build

FROM node:20-bookworm-slim AS runtime
WORKDIR /app

# Copy only runtime artifacts
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package.json ./package.json

# Install production deps only (optional)
# COPY package.json pnpm-lock.yaml ./
# RUN corepack enable && pnpm install --frozen-lockfile --prod

CMD ["node", "dist/index.js"]
```

### Guidance

- Builder stage: install build tooling, compile assets, run `pnpm build`, etc.
- Runtime stage: copy only what you need to run (compiled output, minimal config).
- Do not copy the entire repo into runtime unless necessary.
- Use `.dockerignore` aggressively.

### When a single-stage build is acceptable

- tiny scripts with no build tooling
- extreme simplicity where multi-stage adds more complexity than value
- still: pin versions and run as non-root when possible
