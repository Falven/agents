---
title: Project Setup and Dependency Management with uv
impact: MEDIUM
impactDescription: consistent environments and reproducible installs
tags: python, uv, packaging, lockfiles
---

## Project Setup and Dependency Management with uv

### Rules

- Use `uv` for venv/deps/locking (org default).
- Commit the lockfile (`uv.lock`).
- Prefer uv workspaces (even for single-module repos), following repo conventions.
- Keep configuration in `pyproject.toml`.
- Use Pydantic Settings for configuration management.
- Prefer FastAPI for APIs and Typer for CLIs unless the repo standard differs.

### Dependency hygiene

- Keep runtime deps and dev deps separated.
- Avoid unpinned transient dependency drift by relying on the lockfile.
- Upgrade dependencies intentionally (batch upgrades, run tests).

### Configuration patterns

- Validate env at startup using Pydantic Settings.
- Avoid blanket defaults for required settings.
