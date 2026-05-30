---
title: External I/O and Dependency Adapters
impact: HIGH
impactDescription: keeps I/O safe, time-bounded, and testable
tags: lua, io, adapters, http, db, cache
---

## External I/O and Dependency Adapters

### Rules

- Wrap external systems behind small adapters (`DbService`, `CacheService`, `HttpClient`).
- Always set timeouts.
- Parameterize inputs (no string concatenation SQL).
- Handle pooling/keepalive via helpers.
- On I/O failure:
  - return `(nil, "error_code")`
  - log with context (redacted)
  - never leak raw exceptions to callers

### Adapter example (shape)

```lua
-- db_service.lua
local DbService = {}
DbService.__index = DbService

function DbService:new(deps)
  assert(deps.pg ~= nil, "deps.pg required")
  local self = setmetatable({}, DbService)
  self._pg = deps.pg
  return self
end

function DbService:get_user_by_id(ctx, user_id)
  -- parameterize using your driver API; never concatenate SQL
  local res, err = self._pg:query("SELECT id, name FROM users WHERE id = $1", { user_id })
  if err ~= nil then
    return nil, "db_query_failed"
  end
  if res == nil or #res == 0 then
    return nil, "not_found"
  end
  return res[1], nil
end

return DbService
```

### Timeouts

Every external call should have a timeout configured in the client/driver layer.
If the driver doesn’t support timeouts, wrap calls with a timeout mechanism in your platform (OpenResty timers, etc.) and return a stable error code like `timeout`.

### Avoid

- direct calls to external libraries scattered across business logic
- silent retries with no logging
- unbounded I/O in request handlers
