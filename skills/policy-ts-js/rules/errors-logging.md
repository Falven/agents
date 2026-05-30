---
title: Errors and Logging
impact: HIGH
impactDescription: prevents silent failures and makes debugging possible
tags: typescript, javascript, errors, logging, observability
---

## Errors and Logging

### Rules

- Throw `Error` objects (not strings).
- Use typed errors (custom `Error` subclasses) when it meaningfully improves handling.
- Never swallow errors; handle, rethrow, or surface with context.
- Attach safe, non-PII context for observability.
- Mirror repo logging conventions; avoid noisy logs.

### Example: typed error

```ts
export class NotFoundError extends Error {
  public readonly code = "not_found" as const;
  constructor(message: string) {
    super(message);
    this.name = "NotFoundError";
  }
}
```

### Example: boundary handling

```ts
const getUserOrThrow = async (id: string): Promise<User> => {
  const user = await db.getUser(id);
  if (user === null) {
    throw new NotFoundError(`User ${id} not found`);
  }
  return user;
};
```

### Anti-pattern: swallowing errors

Bad:

```ts
try {
  await doThing();
} catch {
  // ignore
}
```

Good:

```ts
try {
  await doThing();
} catch (err) {
  logger.error({ err }, "doThing failed"); // repo logger, or minimal console fallback
  throw err;
}
```

### Security note

Never log:

- tokens
- cookies
- secrets
- raw auth headers
- PII unless explicitly required and approved
