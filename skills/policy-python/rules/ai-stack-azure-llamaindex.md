---
title: Default AI Stack: Azure OpenAI + LlamaIndex Core
impact: MEDIUM
impactDescription: consistent AI integration and minimal dependency footprint
tags: python, ai, llm, azure, llamaindex
---

## Default AI Stack: Azure OpenAI + LlamaIndex Core

### Defaults

- Provider: **Azure OpenAI** (org default)
- Orchestration: **LlamaIndex Core**
- Install non-core LlamaIndex integrations only when a feature explicitly requires them.

### Rules

- Keep AI code behind a small abstraction boundary (one module/service).
- Validate inputs/outputs at boundaries (Pydantic models).
- Prefer structured outputs when downstream code needs strict fields.
- Set timeouts/retries on network calls (see `io-reliability.md`).
- Avoid global singletons for clients; inject dependencies where possible.

### Suggested layering

- `ai/client.py` — initializes the provider client (Azure)
- `ai/models.py` — request/response Pydantic models
- `ai/service.py` — high-level functions (summarize, extract, classify)
- `ai/prompts/` — prompt templates (if stored)

### When to deviate

Deviate from Azure + LlamaIndex Core only if:

- the repo already standardizes on another stack, or
- a requirement can’t be met (and you document why).
