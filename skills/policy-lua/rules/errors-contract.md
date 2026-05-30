---
title: Error and Result Contract
impact: CRITICAL
impactDescription: makes failure modes explicit and prevents hidden runtime crashes
tags: lua, errors, contracts, validation
---

## Error and Result Contract

### Core convention

- Success: `(value_or_true, nil)`
- Failure: `(nil, "error_code")`

Only throw/assert for **programmer errors** (bad wiring, missing deps), not expected runtime conditions.

### Validate inputs first

Bad (fails deep inside):

```lua
function M:get_user(ctx, user_id)
  return self._db:query("SELECT ... WHERE id = " .. user_id)
end
```

Good (validate early, safe error code):

```lua
function M:get_user(ctx, user_id)
  if user_id == nil or user_id == "" then
    return nil, "invalid_user_id"
  end
  -- parameterize in adapter; do not concat
  return self._db:get_user_by_id(ctx, user_id)
end
```

### Safe error codes

Use stable, searchable codes like:

- `invalid_user_id`
- `db_timeout`
- `cache_miss`
- `unauthorized`
- `forbidden`

### When it’s okay to throw

Throw only for programmer errors:

- missing required dependency
- impossible internal invariant (truly unreachable)

```lua
assert(self._db ~= nil, "FooService misconfigured: db missing")
```

### Propagation pattern

When calling dependencies:

- return their error codes upward
- add logging context at the boundary (don’t wrap everything into new errors)

```lua
local user, err = self._db:get_user_by_id(ctx, user_id)
if err ~= nil then
  self._logger:warn("db.get_user_by_id failed", { err = err, user_id = user_id })
  return nil, err
end
return user, nil
```
