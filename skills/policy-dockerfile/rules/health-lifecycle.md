---
title: Lifecycle, Signals, and Healthchecks
impact: MEDIUM
impactDescription: clean shutdowns, reliable orchestration, faster failure detection
tags: dockerfile, healthcheck, entrypoint, cmd, signals
---

## Lifecycle, Signals, and Healthchecks

### Use exec-form CMD/ENTRYPOINT

Bad (shell form hides signals):

```dockerfile
CMD node dist/index.js
```

Good:

```dockerfile
CMD ["node", "dist/index.js"]
```

### STOPSIGNAL (when needed)

Set the signal your process expects (org/framework specific). Example:

```dockerfile
STOPSIGNAL SIGTERM
```

### HEALTHCHECK: lightweight and fast

A healthcheck should be:

- low latency
- low CPU
- robust to transient errors

Example:

```dockerfile
HEALTHCHECK --interval=30s --timeout=2s --retries=3 \
  CMD curl -fsS http://127.0.0.1:3000/health || exit 1
```

Don’t:

- run long scripts
- include expensive DB queries
- set huge timeouts

### Ports and docs

- `EXPOSE` only what you actually listen on
- log to stdout/stderr
