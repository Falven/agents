# Dashboard JSON Model

There are two materially different dashboard shapes. Identify which one you have before editing anything.

## Classic Dashboard JSON

Classic dashboard JSON is the traditional dashboard object used by most exports, imports, and the legacy dashboard API.

- Typical top-level fields include `title`, `uid`, `tags`, `timezone`, `schemaVersion`, `version`, `templating`, `annotations`, `time`, `rows`, and `panels`.
- Official exports can be rooted in legacy `rows[]`, modern `panels[]`, or a hybrid shape where `panels[]` contains `type: row` containers with nested `panels`.
- Layout is usually driven by `panels[].gridPos`.
- Queries usually live in `panels[].targets`.
- Variables usually live under `templating`.
- `uid` is the durable dashboard identity.
- `schemaVersion` is the schema revision for the dashboard model.
- `schemaVersion` is not a proxy for panel modernity. Newer exports can still contain legacy panel types such as `graph` or `singlestat`.
- `version` is the dashboard revision, not the schema version.
- `id` is database-generated and should not be treated as portable identity.

## Schema v2

Schema v2 is a different structure, currently used for newer resource-oriented workflows and preview-era dashboards.

- Expect structures such as `elements`, `layout`, `timeSettings`, and `variables`.
- Do not look for classic `panels`, `gridPos`, or top-level `templating` as the primary edit surface.
- Placement lives in the layout structure, not classic panel `gridPos`.
- Query and visualization configuration live inside element definitions, not classic panel objects.

## Editing Rules

- Do not translate classic fields into schema v2 mechanically.
- Do not confuse classic numeric `schemaVersion` with "schema v2" as a workflow choice. They are different concepts.
- Preserve the existing shape of templating variable queries. In upstream exports, `templating.list[].query` can be a legacy string or a structured query object.
- Keep layout edits separate from query or identity edits when possible.
- If the structure is ambiguous, say which shape you think it is and why before editing.
