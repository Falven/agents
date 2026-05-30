---
title: Core Style: Functional, Modular, Flat
impact: HIGH
impactDescription: prevents accidental complexity and keeps diffs small
tags: typescript, javascript, style, architecture, composition
---

## Core Style: Functional, Modular, Flat

### Rules

- Keep code **flat**, **small**, **single-purpose**, **composable**.
- Prefer **pure functions + composition**; avoid OOP.
- Do not introduce classes unless required for:
  - state/lifecycle
  - interoperability (e.g., `Error` subclasses, SDK wrappers)
- Prefer modern ESNext syntax when available.
- Prefer arrow functions; exceptions:
  - hoisted function declarations
  - generators
  - `this`-bound methods (rare)

### Avoid “god modules”

Bad:

- a file that mixes validation, data fetching, business logic, and rendering
- cross-cutting helpers with hidden side effects

Good:

- separate boundaries:
  - `validate.ts`
  - `service.ts`
  - `routes.ts`
  - `ui.tsx`

### Example: composable functions

```ts
type User = { id: string; email: string };

const normalizeEmail = (email: string): string => email.trim().toLowerCase();

const requireUser = (user: User | null): User => {
  if (user === null) {
    throw new Error("User required");
  }
  return user;
};

const getUserEmail = (user: User | null): string =>
  normalizeEmail(requireUser(user).email);
```

### Failure discipline

- Fail fast with explicit, actionable errors.
- Never swallow exceptions silently.
- Prefer narrow, typed errors and boundary handling (see `errors-logging.md`).
