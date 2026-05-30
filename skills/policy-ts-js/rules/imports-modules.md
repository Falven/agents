---
title: Imports and Modules
impact: MEDIUM
impactDescription: faster builds, clearer dependencies, fewer bundle surprises
tags: typescript, javascript, imports, esm, modules
---

## Imports and Modules

### Rules

- Use ESM syntax (`import/export`).
- Prefer named imports over namespace/default when possible.
- Keep imports minimal and specific; avoid importing whole modules for one symbol.
- Use `import type` for types to avoid runtime import costs.
- Prefer direct imports over barrel imports when bundle/build performance matters.
  - If working on React/Next performance, also consult `$vercel-react-best-practices`.

### Examples

Prefer:

```ts
import { z } from "zod";
import type { User } from "./types";
```

Avoid:

```ts
import * as z from "zod"; // namespace when not needed
import { thing } from "./index"; // barrel import if it pulls a lot
```

### Guidance

- Keep side-effect imports rare and explicit.
- Don’t rely on module initialization side effects for correctness.
