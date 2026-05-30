---
title: Architecture: Small, Flat, Composable
impact: HIGH
impactDescription: reduces complexity and improves testability
tags: python, architecture, functional, composition
---

## Architecture: Small, Flat, Composable

### Rules

- Prefer small, single-purpose functions and modules.
- Keep code flat; avoid deep package hierarchies.
- Avoid classes unless needed for:
  - preserving state across calls
  - encapsulating a clear abstraction boundary
  - implementing a protocol/interface
- Prefer composition over inheritance.
- Prefer stdlib and modern Python features over custom plumbing:
  - `pathlib`, `tomllib`, `itertools`, `functools`, `enum`, pattern matching
  - `typing`: `Protocol`, `TypedDict`, `Annotated`, `Literal`

### Class avoidance example

Bad (stateful class for stateless logic):

```py
class Slugifier:
    def slugify(self, s: str) -> str:
        return s.lower().replace(" ", "-")
```

Good (pure function):

```py
def slugify(s: str) -> str:
    return s.lower().replace(" ", "-")
```

### Framework defaults

Prefer well-maintained frameworks over bespoke plumbing:

- HTTP APIs: FastAPI
- CLIs: Typer

If you choose differently, include a one-line justification in the code review context (or commit message).
