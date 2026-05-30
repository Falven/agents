---
title: Minimal OS Packages with Proper Cleanup
impact: MEDIUM
impactDescription: smaller images, fewer CVEs, faster builds
tags: dockerfile, apt, apk, packages, cleanup
---

## Minimal OS Packages with Proper Cleanup

### Debian/Ubuntu: install minimal and clean apt lists

Bad:

```dockerfile
RUN apt-get update
RUN apt-get install -y curl
```

Good:

```dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates curl \
    && rm -rf /var/lib/apt/lists/*
```

### Alpine: use `--no-cache`

```dockerfile
RUN apk add --no-cache ca-certificates curl
```

### Keep build tooling out of runtime

- compilers, headers, build essentials belong in builder stage
- runtime should only contain runtime libs

### Prefer distroless/minimal when appropriate

If your app doesn’t need a shell and your org supports it, a distroless runtime can reduce attack surface.
