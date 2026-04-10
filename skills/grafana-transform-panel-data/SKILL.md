---
name: grafana-transform-panel-data
description: Transform and reshape Grafana panel data after the query runs. Use when a panel needs Grafana transformations, calculations, joins, expressions, field organization, structural renaming, reduction, or derived values to turn valid query output into the right final field shape for the chosen visualization. Prefer query shaping first; use panel transforms sparingly and mostly for inspection-table cleanup or narrow derived overview metrics.
---

# Grafana Transform Panel Data

Use this skill to route panel-shaping work to the right Grafana layer after the source query is materially correct.

## When to Apply

Apply this skill when:
- The query returns the right underlying data, but the panel frame shape is wrong.
- The panel needs Grafana-side field shaping, joins, reductions, grouping, or derived fields.
- You need to decide whether the fix belongs in the query, a panel transform, a classic server-side expression, or a SQL expression.

Do not force this skill when:
- The datasource query is still wrong or missing the real business logic.
- A query change is simpler and clearer than any Grafana-side chain.
- The right answer is `no transform`.
- The panel is not an inspection/table-style view that needs post-query frame cleanup.

## Routing Note

| Layer | Use it for | Avoid it when |
| --- | --- | --- |
| Query | Source-owned filtering, grouping, joins, and business semantics | You only need panel-local reshaping |
| Panel transform | Panel-local joins, field shaping, grouping, reduction, and presentation cleanup | The datasource can express the logic more clearly upstream |
| Classic server-side expression | Backend-only Grafana expressions across backend query outputs when `math`, `reduce`, or `resample` is enough | You need richer table shaping, query semantics, or unsupported datasource paths |
| SQL expression | Grafana's SQL expression layer for SQL-style operations across query results when that layer is available and its constraints fit | You only need panel transforms, or the source query already says it more plainly |

## Workflow

1. Route the problem first with [references/expressions-vs-transformations.md](references/expressions-vs-transformations.md).
2. If panel transforms are still the right layer, inspect the current frame shape and the target visualization shape.
   - Official dashboards usually keep transforms sparse.
   - The common post-query pattern is inspection-table cleanup with `organize`, `groupBy`, `labelsToFields`, `merge`, `seriesToColumns`, or `sortBy`.
   - `calculateField` is a narrow pattern for derived utilization/global overview panels, not a general default.
3. Build a strict pipeline with [references/transformation-order.md](references/transformation-order.md). Verify the frame in Table view or transformation debug after each major step.
4. Pick the smallest primitive that matches the job:
   - Use [references/joins-calculations.md](references/joins-calculations.md) for `Add field from calculation`, `Group by`, `Reduce`, `Join by field`, `Join by labels`, and `Merge series/tables`.
   - Use [references/field-shaping.md](references/field-shaping.md) for `Prepare time series`, `Rows to fields`, `Labels to fields`, `Series to rows`, `Organize fields by name`, `Rename by regex`, and `Convert field type`.
   - Use [references/common-transformations.md](references/common-transformations.md) as the quick chooser.
5. Reduce late. Do final organizing and renaming last.

## Reference Map

- [references/expressions-vs-transformations.md](references/expressions-vs-transformations.md) -> route the problem to query, panel transform, classic server-side expression, or SQL expression
- [references/transformation-order.md](references/transformation-order.md) -> keep the pipeline valid and apply the reduce-late rule
- [references/common-transformations.md](references/common-transformations.md) -> quick map from problem shape to Grafana primitive
- [references/joins-calculations.md](references/joins-calculations.md) -> distinguish join operators from calculation primitives
- [references/field-shaping.md](references/field-shaping.md) -> reshape and finish fields for the chosen visualization

## Output

Return one of:
- The minimal panel transformation chain
- `no transform`
- A recommendation to move the work to the query, a classic server-side expression, or a SQL expression

Explain why that layer is the right one and state the expected resulting frame shape.
