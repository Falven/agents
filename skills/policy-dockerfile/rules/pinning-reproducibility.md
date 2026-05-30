---
title: Pin Versions and Preserve Reproducibility
impact: CRITICAL
impactDescription: prevents “works on my machine” and supply-chain drift
tags: dockerfile, pinning, reproducibility, lockfiles, supply-chain
---

## Pin Versions and Preserve Reproducibility

**Rule:** Pin everything that can drift:

- base images
- package manager behavior
- OS packages (when practical)
- toolchain versions (node/python/etc.)

### Base image pinning

Bad:

```dockerfile
FROM node:latest
FROM python:3
```

Good:

```dockerfile
FROM node:20-bookworm
FROM python:3.13-slim
```

If your org standard is digest pinning, use:

```dockerfile
FROM node:20-bookworm@sha256:<digest>
```

### Lockfiles are mandatory

- Node: `pnpm-lock.yaml` / `package-lock.json`
- Python: `uv.lock` / equivalent
- Rust: `Cargo.lock`
- Go: `go.sum`

**Rule of thumb:** copy lockfiles first and install deps before copying source.

### Toolchain pinning via ARGs (when useful)

```dockerfile
ARG NODE_VERSION=20
FROM node:${NODE_VERSION}-bookworm AS builder
```

Guideline:

- allow ARG overrides for controlled upgrades
- keep defaults pinned and review changes intentionally

### Determinism checklist

- [ ] no `latest`
- [ ] lockfile present and used
- [ ] dependency install step is cacheable
- [ ] build output is reproducible from same inputs
