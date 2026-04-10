# Transformation Order

Grafana transformations are a strict pipeline. Each step receives the output of the previous step.

Recommended order:

1. Route first. If the query, a classic server-side expression, or a SQL expression is the cleaner layer, stop there.
2. Normalize shape early with `Prepare time series`, `Rows to fields`, `Labels to fields`, `Series to rows`, `Series to columns`, or `Convert field type`.
3. Combine frames only after keys and types line up with `Join by field`, `Join by labels`, or `Merge series/tables`.
4. Add derived fields or grouped aggregates with `Add field from calculation` or `Group by`.
5. Reduce late. Use `Reduce` only after every field needed by later joins, labels, or calculations already exists. Official dashboards rarely need it outside summary or utilization-style panels.
6. Finish with presentation cleanup like `Sort by`, `Rename by regex`, or `Organize fields by name`.

Checks after major steps:

- Inspect Table view or transformation debug after each major shape change.
- Confirm whether the result is still a time series, a grouped table, or a reduced summary.
- If a step destroys fields needed later, move it later or remove it.
