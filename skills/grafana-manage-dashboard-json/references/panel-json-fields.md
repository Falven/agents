# Panel JSON Fields

Panel editing depends on whether the dashboard is classic JSON or schema v2.

## Classic Panel Editing

For classic dashboards, the main edit surface is `panels[]`.

- Common fields are `type`, `title`, `datasource`, `targets`, `options`, `fieldConfig`, and `gridPos`.
- `targets` carry query semantics. Keep changes there tightly scoped.
- `gridPos` affects layout only. Do not mix layout edits with query changes unless the task requires both.
- `fieldConfig`, thresholds, overrides, and options affect presentation more than query meaning.
- Some dashboards still root layout in `rows[]`, and others use row panels inside `panels[]`. Edit the actual panel object rather than assuming a flat list.
- `datasource` can be a string, an object without `type`, or omitted on the panel when targets inherit it.
- When a panel has per-target datasource fields, treat the target-level datasource as authoritative for that query.
- Some panels are effectively mixed or inherited-datasource panels. Do not force a single panel-level datasource if the targets intentionally vary.

## Schema v2 Editing

For schema v2 dashboards, do not search for classic panel fields first.

- Visualization and query definitions live in `elements`.
- Placement lives in `layout`.
- Time defaults live in `timeSettings`.
- Variables live in `variables`.
- A schema v2 layout change should usually stay inside the layout structure, not invent a classic `gridPos`.

## Routing Rule

- If the user asks to move a panel, resize a panel, or edit a query in classic JSON, work in `panels[]`.
- If the artifact instead exposes `elements` and `layout`, treat those as the edit surface and avoid backporting classic field names into it.
- If a change is easier or safer in the Grafana UI than by hand, say so explicitly.
