---
title: Typed Boundaries with Pydantic v2
impact: CRITICAL
impactDescription: prevents untyped dict/Any from leaking across module boundaries
tags: python, typing, pydantic, validation, boundaries
---

## Typed Boundaries with Pydantic v2

### Rules

- Define boundaries with Pydantic v2 models.
- Validate at the edges (env/network/user input).
- Do not pass untyped `dict` or `Any` across module/API boundaries.
- Keep internal code type-sound (no “stringly typed” payloads flowing around).

### Example: request boundary

```py
from pydantic import BaseModel, ConfigDict, Field

class CreateUserRequest(BaseModel):
    model_config = ConfigDict(extra="forbid")

    email: str = Field(min_length=3, max_length=320)
    name: str = Field(min_length=1, max_length=100)

class CreateUserResponse(BaseModel):
    id: str
    email: str
    name: str
```

### Example: validating untyped input

```py
from typing import Any

def parse_create_user(data: Any) -> CreateUserRequest:
    # Raises ValidationError for invalid input (edge of system)
    return CreateUserRequest.model_validate(data)
```

### Guidance

- Use `extra="forbid"` for external inputs unless you explicitly accept unknown fields.
- Prefer explicit types for IDs (string) and normalize/validate them early.
- For internal-only data structures, Pydantic is optional, but module boundaries should remain typed.
