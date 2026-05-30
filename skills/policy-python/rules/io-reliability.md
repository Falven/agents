---
title: I/O Reliability: Timeouts, Retries, Streaming
impact: HIGH
impactDescription: prevents hangs and reduces memory blow-ups
tags: python, io, reliability, timeouts, retries, streaming
---

## I/O Reliability: Timeouts, Retries, Streaming

### Rules

- Always set timeouts for network I/O.
- Use retries only when safe (idempotent operations) and cap them.
- Never fail silently; surface actionable errors.
- Prefer streaming/generators for large data instead of loading everything into memory.
- Use context managers for resources (files, network clients).

### Timeout guideline

Any external call (HTTP, DB, cache, filesystem operations that can hang) should have a timeout.

### Retry guideline

Retries should be:

- limited (small retry count)
- bounded (backoff/jitter)
- safe (idempotent requests, or designed-to-retry operations)

### Streaming guideline

If data can be large:

- iterate line-by-line
- stream responses
- avoid `response.text` for huge bodies
- avoid reading entire files into memory unless necessary

### Error discipline

- Do not write `except: pass`
- On failure, raise a typed exception or return a typed error object at your boundary
- Log failures with `logger.exception(...)` and safe context

### Example: streaming a file

```py
from pathlib import Path
from typing import Iterator

def read_lines(path: Path) -> Iterator[str]:
    with path.open("r", encoding="utf-8") as f:
        for line in f:
            yield line.rstrip("\n")
```
