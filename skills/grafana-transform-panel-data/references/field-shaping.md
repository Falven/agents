# Field Shaping

Use shape transforms to produce the frame the visualization expects before final cleanup. In the official dashboards, these are usually table/inspection helpers, not a substitute for query-side shaping.

## Structural reshaping

- `Prepare time series`: Convert between wide, long, or multi-frame time-series shapes for the target panel.
- `Rows to fields`: Turn row values into separate fields when the panel expects fields instead of rows.
- `Labels to fields`: Promote labels into fields when label metadata needs to become tabular columns or field names.
- `Series to rows`: Flatten series into row-oriented output for table-style inspection or downstream shaping.
- `Series to columns`: Pivot series into columns when the inspection table needs one field per series or label value.

## Field cleanup

- `Convert field type`: Fix types before later joins, calculations, or visualization rules depend on them.
- `Rename by regex`: Rename fields structurally when names follow a stable pattern.
- `Organize fields by name`: Reorder, hide, and rename final fields for a single-query result. Use it as late cleanup, not as a join or calculation tool.

Keep field shaping close to the visualization's required frame shape. Do not reduce early if later shape steps still need the original fields. When the result is an inspection table, `Sort by` and `Organize fields by name` are usually the last steps.
