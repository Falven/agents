---
title: Logging Conventions
impact: HIGH
impactDescription: improves debuggability without leaking secrets
tags: lua, logging, observability, security
---

## Logging Conventions

### Rules

- Prefix logs with module/function name.
- Use structured fields (tables) rather than string concatenation.
- Levels:
  - INFO: milestones / successful boundaries
  - WARN: recoverable failures / retries / invalid inputs
  - ERR: failures that abort an operation
- Never log secrets/tokens/cookies/PII.
- Redact identifiers where appropriate.

### Example

```lua
self._logger:info("Composer.submit.start", {
  trace_id = ctx.trace_id,
  user_id = ctx.user_id, -- consider redaction if sensitive
})

-- On failure:
self._logger:error("Composer.submit.failed", {
  trace_id = ctx.trace_id,
  err = err,
})
```

### Redaction strategy

- Prefer logging stable internal IDs rather than emails/usernames.
- If you must include identifiers, truncate or hash them.
- Never log raw tokens, auth headers, or session cookies.

### Boundary logging

Log at boundaries:

- external I/O calls (db/cache/http)
- start/end of major operations
- retries/timeouts
