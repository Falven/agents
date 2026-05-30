---
title: Concurrency and Background Work
impact: MEDIUM
impactDescription: improves latency while keeping execution observable and bounded
tags: lua, concurrency, async, background, coordination
---

## Concurrency and Background Work

### Rules

- Encapsulate background work in spawn/wait helpers.
- Join before proceeding when results are required.
- Aggregate results; collect per-task errors.
- Continue where possible, but never hide failures.

### Pattern (conceptual)

```lua
-- pseudo-code; implement with your platform primitives
local function run_parallel(tasks)
  local results = {}
  local errors = {}

  for name, fn in pairs(tasks) do
    -- spawn(fn) -> handle
  end

  for name, handle in pairs(handles) do
    -- wait(handle) -> ok, value_or_err
    -- store results/errors
  end

  return results, errors
end
```

### Request-scoped caches

Use `ctx` to avoid duplicate work during a single operation:

- cache computed values
- deduplicate expensive reads

### Avoid

- fire-and-forget side effects without observability
- background work that can outlive request lifetime without safeguards
- mingling logs from multiple concurrent tasks without trace IDs
