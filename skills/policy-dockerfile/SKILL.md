---
name: policy-dockerfile
description: |
  Dockerfile and container build policy for small, reproducible, secure images.
  Use when creating/editing Dockerfiles, changing container build pipelines, or
  investigating image size/build performance/startup problems.
  Avoid for non-container tasks.
license: INTERNAL
metadata:
  author: local
  version: "1.0.0"
  argument-hint: <Dockerfile-path>
---

# Dockerfile Policy

Design goal: **small, reproducible, secure images** that build fast and start cleanly.

This skill is intentionally split into small rule files. Prefer to read only the
relevant rule(s) for the change you’re making.

## When to Apply

Use this policy when:

- editing any `Dockerfile`
- adding CI build steps for images
- optimizing cold-start, image size, build time
- adding runtime users, healthchecks, or pinning versions

## How to Use

1. Identify the runtime (Node/Python/OpenResty/etc.) and base image choice.
2. Apply multi-stage builds by default.
3. Pin base image + tooling versions; rely on lockfiles.
4. Optimize layers and caching (BuildKit cache mounts).
5. Use non-root runtime user and least-privilege filesystem permissions.
6. Add correct lifecycle behavior (ENTRYPOINT/CMD/STOPSIGNAL/HEALTHCHECK).
7. Avoid known anti-patterns.

## Rule Index (read only what you need)

### Core (start here)

- `rules/multistage.md` — multi-stage builds, builder vs runtime
- `rules/pinning-reproducibility.md` — pin versions, lockfiles, deterministic builds
- `rules/caching-buildkit.md` — BuildKit caches, layer ordering, dependency installs

### Security

- `rules/security-nonroot.md` — non-root runtime, ownership, secrets hygiene

### OS packages and runtime behavior

- `rules/os-packages-minimal.md` — minimal packages, apt/apk patterns, cleanup
- `rules/health-lifecycle.md` — entrypoints, signals, healthchecks

### Never-do list

- `rules/antipatterns.md` — common Dockerfile anti-patterns

## Quick Checklist

- [ ] `# syntax=docker/dockerfile:1.7` (or repo standard)
- [ ] Base image pinned (no `:latest`)
- [ ] Multi-stage build (builder + runtime)
- [ ] Lockfiles copied early; deps installed before source
- [ ] BuildKit cache mounts used for package managers
- [ ] Runtime runs as non-root user (fixed UID/GID)
- [ ] No secrets baked into image
- [ ] Exec-form `ENTRYPOINT`/`CMD`
- [ ] Appropriate `STOPSIGNAL`
- [ ] Lightweight `HEALTHCHECK` (when applicable)
