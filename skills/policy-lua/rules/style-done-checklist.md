---
title: Definition of Done (Lua)
impact: MEDIUM
impactDescription: consistent quality bar for Lua changes
tags: lua, checklist, quality
---

## Definition of Done (Lua)

Use this checklist before finalizing Lua changes:

- [ ] No globals; everything is `local`.
- [ ] Module returns its public table (clear public API).
- [ ] Inputs validated early; explicit error codes on failure.
- [ ] Result convention used consistently: success `(value_or_true, nil)`, failure `(nil, "error_code")`.
- [ ] Logs concise, prefixed, structured, and redaction-safe.
- [ ] Config typed/validated and separated from logic; no env reads in hot paths.
- [ ] External calls are time-bounded, pooled/kept alive appropriately, and parameterized.
- [ ] Concurrency joined; partial failures handled; no invisible background side effects.
- [ ] Utilities pure; no hidden I/O.
- [ ] User input sanitized/normalized before use; claims/IDs validated.
- [ ] Public functions documented (LuaDoc-style) where appropriate.
- [ ] Code compiles/runs deterministically without warnings.
