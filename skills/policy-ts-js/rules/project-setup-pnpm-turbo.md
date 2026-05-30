---
title: Project Setup: pnpm + Turborepo
impact: MEDIUM
impactDescription: consistent tooling and predictable workspace structure
tags: typescript, javascript, pnpm, turborepo, monorepo
---

## Project Setup: pnpm + Turborepo

### Defaults

- Use **pnpm** for package manager commands.
- Use **turborepo** workspace structure (follow repo conventions; if none, default to turbo).

### Rules

- Do not introduce npm/yarn commands into scripts unless the repo already uses them.
- Add new packages/apps to the existing workspace structure.
- Prefer workspace-local dependencies and explicit package boundaries.

### Guidance

- Keep `package.json` scripts small; delegate to turbo pipelines where appropriate.
- Avoid adding heavyweight tooling unless necessary.
- Prefer incremental builds and cacheable tasks.
