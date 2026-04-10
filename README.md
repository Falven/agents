# agents

Repository for installable agent skills and future agent-related artifacts.

Current v1 scope lives under `skills/`.

## Layout

```text
skills/
  grafana-choose-visualization/
  grafana-write-promql/
  ...
```

## Conventions

- Keep every skill self-contained and installable by folder path.
- Keep `SKILL.md` thin; put detailed guidance in small files under `references/`.
- Add `scripts/` or `assets/` only when a skill genuinely needs them.
- Keep repo-level files minimal. Do not add empty future directories.

## Install

Use the GitHub directory URL or `owner/repo` plus the skill path with `$skill-installer`.
