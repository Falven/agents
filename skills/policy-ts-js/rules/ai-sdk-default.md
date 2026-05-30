---
title: Default AI/LLM Stack: AI SDK
impact: MEDIUM
impactDescription: consistent AI integration and reduced surface area
tags: typescript, ai, llm, sdk, architecture
---

## Default AI/LLM Stack: AI SDK

### Rule

Default to the project’s **AI SDK** for LLM features unless the task explicitly requires a different stack.

### When to apply

Use when implementing:

- chat endpoints
- streaming UI interactions
- tool/function calling patterns
- structured outputs

### Guidelines

- Prefer the repo’s existing patterns (providers, middleware, error handling).
- Keep AI logic behind a small boundary:
  - request validation
  - prompt construction
  - model call
  - output validation/normalization
- Validate external inputs (Zod) and validate structured outputs when downstream code relies on shape.

### Avoid

- wiring new providers ad hoc across many files
- mixing prompt construction with UI logic
- unbounded logs of prompts/responses (privacy + cost)

### If you must deviate

Deviate from the default SDK only if:

- the repo already standardizes on another approach, or
- a required feature is not supported and you document why.
