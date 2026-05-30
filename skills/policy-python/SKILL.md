---
name: policy-python
description: |
  Python engineering policy: typed boundaries, Pydantic v2 models, logging,
  I/O reliability, uv-based project setup, and the default AI stack.
  Use when editing Python code, APIs, CLIs, or Python infra.
  Avoid for non-Python tasks.
license: INTERNAL
metadata:
  author: local
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

# Python Engineering Policy

This skill provides **Python-specific** engineering rules:

- typed, validated boundaries (Pydantic v2)
- small, composable functions
- strong logging/observability
- reliable I/O (timeouts, retries, streaming)
- uv-based dependency management
- default AI stack: Azure OpenAI + LlamaIndex Core

## When to Apply

Use when:

- editing `**/*.py`
- adding/refactoring FastAPI/Typer code
- building data pipelines or services
- touching external I/O boundaries (HTTP/DB/files)
- implementing AI/LLM workflows in Python

## How to Use

1. Apply architecture rules first: flat modules, pure functions, small boundaries.
2. Use Pydantic models at edges; keep internals type-sound.
3. Add logging at boundaries and failures; never use `print` for logging.
4. Ensure timeouts/retries for network I/O and stream data where possible.
5. Use uv for project setup and lockfiles.
6. For AI workflows, default to Azure OpenAI + LlamaIndex Core.

## Rule Index

- `rules/architecture.md`
- `rules/typing-boundaries-pydantic.md`
- `rules/logging-observability.md`
- `rules/io-reliability.md`
- `rules/project-setup-uv.md`
- `rules/ai-stack-azure-llamaindex.md`

## Non-negotiables (quick)

- Explicit return types on public APIs.
- No `print` for logging.
- No broad `except:` and no silent exception swallowing.
- No mutable default args.
- Validate external inputs at the edges with Pydantic v2.
