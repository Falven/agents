---
name: policy-ts-js
description: |
  TypeScript/JavaScript engineering policy: functional modular code, strong typing,
  safe async/concurrency, minimal imports, Zod validation at boundaries, and
  explicit error handling. Use when editing TS/JS/TSX/JSX code.
  Avoid for non-TS/JS tasks.
license: INTERNAL
metadata:
  author: local
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

# TypeScript / JavaScript Policy

This skill contains the detailed TS/JS rules that should _not_ live in always-on
AGENTS instructions.

## When to Apply

Use when:

- editing `**/*.ts`, `**/*.tsx`, `**/*.js`, `**/*.jsx`
- adding public APIs, endpoints, or library code
- doing refactors that might affect correctness/performance
- dealing with async workflows, fetches, and concurrency

If the task is React/Next.js performance or composition-heavy, also consider:

- `$vercel-react-best-practices`
- `$vercel-composition-patterns`

## Priorities (when rules conflict)

TypeScript/JavaScript priority:

1. Type-safety → 2) Clarity → 3) Correctness → 4) Performance → 5) Brevity

## How to Use

1. Apply style/core architecture rules first (small, composable, flat).
2. Enforce type safety on public boundaries; avoid `any` and non-null assertions.
3. Validate external inputs with Zod.
4. Structure async work for concurrency (`Promise.all`), avoid waterfalls.
5. Keep imports minimal and explicit.
6. Use explicit error types and never swallow failures.

## Rule Index

### Core

- `rules/style-core.md`
- `rules/types-safety.md`
- `rules/validation-zod.md`

### Execution model

- `rules/async-concurrency.md`
- `rules/loops-control-flow.md`

### Imports and errors

- `rules/imports-modules.md`
- `rules/errors-logging.md`

### Project/tooling defaults

- `rules/project-setup-pnpm-turbo.md`
- `rules/ai-sdk-default.md`
