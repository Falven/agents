---
title: Dockerfile Anti-Patterns
impact: CRITICAL
impactDescription: prevents slow builds, bloated images, and production instability
tags: dockerfile, antipatterns, security, performance
---

## Dockerfile Anti-Patterns (Never)

- `FROM …:latest` or unpinned toolchain versions
- build tools in the runtime stage
- `apt-get update` in one layer and `apt-get install` in another
- copying the entire repo into runtime by default (no `.dockerignore`)
- shell-form `CMD`/`ENTRYPOINT` that hides signals
- big/slow healthcheck scripts or long timeouts
- baking secrets into the image (`ENV`, `ARG` without secure build secrets)
- running as root in production without a strong justification
- installing dev dependencies in runtime (unless explicitly required)
- caching disabled by poor layer ordering (copying source before lockfiles)
