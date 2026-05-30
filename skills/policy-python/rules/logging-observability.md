---
title: Logging and Observability
impact: HIGH
impactDescription: makes failures diagnosable and prevents silent breakage
tags: python, logging, observability, errors
---

## Logging and Observability

### Rules

- Configure logging once at process start (entrypoint), not in libraries.
- Use module loggers:
  - `logger = logging.getLogger(__name__)`
- Log key boundaries:
  - start/finish of major operations
  - external I/O calls
  - major decisions
- Use `logger.exception(...)` inside `except` blocks.
- Never log secrets/tokens/PII.

### Minimal configuration pattern (entrypoint)

```py
import logging
import sys

def configure_logging() -> None:
    logging.basicConfig(
        level=logging.INFO,
        format="%(asctime)s %(levelname)s %(name)s: %(message)s",
        stream=sys.stdout,
    )
```

### Module usage pattern

```py
import logging
logger = logging.getLogger(__name__)

def do_work(user_id: str) -> None:
    logger.info("do_work.start", extra={"user_id": user_id})
    try:
        # ...
        logger.info("do_work.success", extra={"user_id": user_id})
    except Exception:
        logger.exception("do_work.failed", extra={"user_id": user_id})
        raise
```

### Guidance

- Prefer structured fields via `extra=...` where your logging stack supports it.
- If you must include identifiers, consider redaction (truncate/hash).
- Do not swallow exceptions. Handle, rethrow, or surface with context.
