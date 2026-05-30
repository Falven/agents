---
title: Module Design and Dependency Injection
impact: HIGH
impactDescription: keeps Lua code testable, composable, and side-effect free
tags: lua, modules, dependency-injection, architecture
---

## Module Design and Dependency Injection

### Rules

- One responsibility per module.
- No globals. Everything is `local`.
- Each module returns a table exposing its public API.
- Prefer dependency injection over hidden imports/state.
- Pass request/operation context (`ctx`) for caches/tracing.

### Recommended shape

```lua
-- foo_service.lua
local FooService = {}
FooService.__index = FooService

function FooService:new(deps)
  assert(deps ~= nil, "deps required")
  assert(deps.db ~= nil, "deps.db required")
  assert(deps.logger ~= nil, "deps.logger required")

  local self = setmetatable({}, FooService)
  self._db = deps.db
  self._logger = deps.logger
  return self
end

function FooService:do_thing(ctx, user_id)
  -- validate inputs early
  if user_id == nil or user_id == "" then
    return nil, "invalid_user_id"
  end

  -- use ctx for request-scoped cache / tracing if provided
  local trace_id = ctx and ctx.trace_id or nil
  self._logger:info("FooService.do_thing", { trace_id = trace_id, user_id = user_id })

  -- ...
  return true, nil
end

return FooService
```

### Optional: lazy singleton (only when justified)

If you truly need a singleton, make it explicit:

```lua
local instance = nil

function FooService:get_instance(deps)
  if instance == nil then
    instance = FooService:new(deps)
  end
  return instance
end
```

Guideline:

- prefer explicit instance passing (cleaner tests)
- if you use a singleton, it must still be dependency-injected

### Avoid

- importing deep graphs of modules as implicit dependencies
- hidden I/O at module import time
- “utility modules” that become a grab bag
