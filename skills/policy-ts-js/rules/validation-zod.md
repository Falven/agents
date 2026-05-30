---
title: Validate External Inputs with Zod
impact: HIGH
impactDescription: prevents malformed inputs from corrupting internal logic
tags: typescript, validation, zod, boundaries
---

## Validate External Inputs with Zod

### Rules

- Validate all external inputs:
  - environment variables
  - network payloads (requests/responses)
  - user inputs
- Validate at the edges; keep internal code type-sound.
- Prefer schemas that:
  - forbid unknown fields (when appropriate)
  - coerce primitives only when intended
  - provide useful error messages

### Example: request body validation

```ts
import { z } from "zod";

const CreateUserSchema = z
  .object({
    email: z.string().email(),
    name: z.string().min(1).max(100),
  })
  .strict();

type CreateUser = z.infer<typeof CreateUserSchema>;

export const parseCreateUser = (input: unknown): CreateUser => {
  return CreateUserSchema.parse(input);
};
```

### Example: env validation

```ts
import { z } from "zod";

const EnvSchema = z
  .object({
    NODE_ENV: z.enum(["development", "test", "production"]),
    PORT: z.coerce.number().int().min(1).max(65535),
  })
  .passthrough(); // or .strict() if you want to forbid extra vars

export const env = EnvSchema.parse(process.env);
```

### Guidance

- Prefer `.safeParse` when you need to return a typed error result instead of throwing.
- Avoid scattering schema definitions; centralize boundary schemas.
