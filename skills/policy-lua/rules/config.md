---
title: Typed Configuration, Read Once
impact: MEDIUM
impactDescription: prevents per-request overhead and config drift bugs
tags: lua, config, env, validation
---

## Typed Configuration, Read Once

### Rules

- Read env/config once during init, not in hot paths.
- Validate and convert types (bool/number/json).
- Separate configuration from behavior.
- Provide safe defaults only for truly optional fields.

### Pattern

```lua
local function parse_bool(s)
  if s == "1" or s == "true" then return true end
  if s == "0" or s == "false" then return false end
  return nil
end

local function load_config(env)
  local timeout_ms = tonumber(env.TIMEOUT_MS or "")
  if timeout_ms == nil then
    return nil, "missing_timeout_ms"
  end

  local debug = parse_bool(env.DEBUG or "0")
  if debug == nil then
    return nil, "invalid_debug"
  end

  return {
    timeout_ms = timeout_ms,
    debug = debug,
  }, nil
end
```

### Avoid

- reading env vars per request
- silently defaulting required settings
- accepting “truthy”/“falsy” without explicit parsing
