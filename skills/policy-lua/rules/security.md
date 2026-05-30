---
title: Security and Input Sanitization
impact: CRITICAL
impactDescription: prevents injection bugs and secret leakage
tags: lua, security, sanitization, secrets, validation
---

## Security and Input Sanitization

### Rules

- Sanitize/normalize user-supplied fields before use.
- Validate claims/IDs; map external identifiers to internal ones.
- Keep secrets in config; never return or log them.
- Prevent injection:
  - do not concat SQL
  - validate and escape any string used in templates/paths/commands
- Apply least privilege:
  - only access required data
  - separate auth/authorization checks from business logic

### Example: validate and normalize

```lua
local function normalize_id(s)
  if type(s) ~= "string" then return nil end
  if #s == 0 or #s > 128 then return nil end
  -- apply stricter patterns if your IDs have a known shape
  return s
end
```

### Secret hygiene

Never log:

- Authorization headers
- session cookies
- tokens
- full request bodies that may contain PII

If debugging requires identifiers:

- log a hash or a truncated value
