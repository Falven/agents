---
title: Type Safety Rules
impact: CRITICAL
impactDescription: prevents runtime failures and makes refactors safe
tags: typescript, types, safety, correctness
---

## Type Safety Rules

### Rules

- Prefer **TypeScript** over JavaScript unless the repo requires otherwise.
- In `.js/.jsx`, add JSDoc types when editing.
- Exported/public APIs must specify parameter and return types.
- Do not use:
  - `any`
  - `as unknown as ...`
  - non-null assertions (`!`)
    unless all other designs fail (and justify why in context).
- Do not rely on generic truthiness for control flow:
  - use explicit comparisons (`value != null`, `count > 0`, etc.)

### Example: avoid non-null assertions

Bad:

```ts
const el = document.getElementById("root")!;
el.innerHTML = "ok";
```

Good:

```ts
const el = document.getElementById("root");
if (el === null) {
  throw new Error("Missing #root element");
}
el.innerHTML = "ok";
```

### Example: prefer explicit null/undefined checks

Bad:

```ts
if (value) {
  /* ... */
} // value might be 0, "", false
```

Good:

```ts
if (value != null) {
  /* ... */
} // null/undefined only
```

### Recommended TS features

- `unknown` + narrowing for untrusted inputs
- `never` for exhaustiveness
- `satisfies` for constraint checks
- `as const` for literals

Exhaustiveness pattern:

```ts
type Kind = "a" | "b";
const handle = (k: Kind): number => {
  switch (k) {
    case "a":
      return 1;
    case "b":
      return 2;
    default: {
      const _exhaustive: never = k;
      return _exhaustive;
    }
  }
};
```
