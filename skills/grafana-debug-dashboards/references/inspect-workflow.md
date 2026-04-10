# Inspect Workflow

Treat Inspect plus Explore as the default loop. Do not start by editing panel options.

## Canonical Loop

1. Reproduce the exact dashboard state: time range, timezone, refresh, variables, repeated panels, `var-` URL params, and whether the content lives in `rows[]` instead of top-level `panels[]`.
2. Open panel Inspect and check tabs in this order: `Error`, `Query`, `Data`, `Stats`, `JSON`.
3. Open the same query in Explore to confirm datasource, range, interval, instant/range mode, and raw response outside panel presentation.
4. Split the failure into one of three layers: raw query result is wrong in Explore, transformed result is wrong after panel transforms, or formatted result is wrong only after field or display config.
5. Use Table view to flatten rendering issues before blaming the query.
6. Change one thing at a time and re-run Inspect. Verify whether the fix changed raw data, transformed data, or only presentation.

## What Each Surface Tells You

- `Error`: hard failures, datasource errors, parser errors, auth problems.
- `Query`: final query text and interpolated context. Use this to catch wrong variables, interval, or time overrides.
- `Data`: what the panel is actually consuming after the query returns.
- `Stats`: cost and size. Use it for duration, rows, series, and point-volume clues when panels are slow or oversized.
- `JSON`: panel structure, `rows[]` vs `panels[]`, datasource inheritance or overrides, transformations, field config, links, and time settings.

## Fast Split

- Wrong in Explore means query, datasource, time, or variable context is still wrong.
- An empty-looking dashboard can still be healthy if the real panels are in `rows[]` or if the top level is just section scaffolding.
- Do not trust the panel datasource badge alone; some official dashboards inherit datasource from targets, use `-- Mixed --`, or omit `.datasource.type`.
- Right in Explore but wrong in panel data means inspect transformations next.
- Right in panel data but misleading on screen means inspect field config and panel semantics next.
