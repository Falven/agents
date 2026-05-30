---
name: policy-lua
description: |
  Lua authoring policy: module boundaries, error contracts, logging, configuration,
  and safe I/O. Use when writing or refactoring Lua (especially OpenResty/Nginx Lua).
  Avoid for non-Lua tasks.
license: INTERNAL
metadata:
  author: local
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

# Lua Authoring Policy

This skill defines how Lua code should be authored:

- composable, dependency-injected modules
- no globals; explicit interfaces
- consistent error/value return contract
- safe logging and safe external I/O
- concurrency patterns that are joined and observable

## When to Apply

Use when:

- editing `**/*.lua`
- writing OpenResty handlers/middleware/services
- introducing adapters for DB/cache/HTTP systems
- refactoring for correctness, observability, or safety

## How to Use

1. Read the rule(s) relevant to what you’re changing.
2. Enforce the error contract and input validation early.
3. Wrap external systems behind tiny adapters.
4. Keep modules small; avoid hidden state.
5. Verify “Definition of Done” checklist for Lua.

## Rule Index

### Core module patterns

- `rules/module-design.md` — module shape, dependency injection, no globals

### Errors and logging

- `rules/errors-contract.md` — return conventions, validation, when to throw
- `rules/logging.md` — structured logs, redaction, levels

### Config and dependencies

- `rules/config.md` — typed config, read once, separate from behavior
- `rules/io-deps.md` — timeouts, pooling, parameterization, adapters

### Concurrency and security

- `rules/concurrency.md` — spawn/join, partial failures, per-task errors
- `rules/security.md` — sanitize inputs, secrets hygiene, injection prevention

### Checklists

- `rules/style-done-checklist.md` — definition of done for Lua changes

## Non-negotiables (quick)

- No globals; everything `local`.
- Modules return a table exposing public API.
- Public functions validate inputs first; return `(value, nil)` or `(nil, "error_code")`.
- Never log secrets/tokens/PII; redact identifiers.
- External calls have timeouts and return safe error codes.
