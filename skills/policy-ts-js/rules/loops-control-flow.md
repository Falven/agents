---
title: Control Flow and Loops
impact: MEDIUM
impactDescription: reduces nesting and prevents accidental inefficiencies
tags: typescript, javascript, loops, control-flow, readability
---

## Control Flow and Loops

### Rules

- Avoid deep nesting; prefer early returns/guard clauses.
- Prefer `for` / `for…of` for iteration (especially for side effects/perf).
- Use `map/filter/reduce` only when you immediately use return values.
- Cache loop invariants (like `arr.length`) in hot paths.

### Example: early returns

Bad:

```ts
const handle = (user: User | null): string => {
  if (user !== null) {
    if (user.email !== "") {
      return user.email;
    } else {
      return "missing";
    }
  } else {
    return "missing";
  }
};
```

Good:

```ts
const handle = (user: User | null): string => {
  if (user === null) return "missing";
  if (user.email === "") return "missing";
  return user.email;
};
```

### Example: loop invariants

Bad:

```ts
for (let i = 0; i < arr.length; i++) {
  sum += arr[i];
}
```

Good:

```ts
const n = arr.length;
for (let i = 0; i < n; i++) {
  sum += arr[i];
}
```
