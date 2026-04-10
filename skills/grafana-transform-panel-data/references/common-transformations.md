# Common Transformations

Start with the smallest primitive that matches the job. In the official dashboards, these are used sparingly and mostly for inspection-table shaping or narrow overview calculations.

## Calculation primitives

- `Add field from calculation`: Create a new field from existing fields in the current frame. Use it for panel-local derived values without collapsing the frame. In exported dashboard JSON this often appears as `calculateField`; treat it as a narrow pattern for utilization-style panels, not a general default.
- `Group by`: Group rows by key fields, then calculate per-group aggregates. Use it when the grouped keys still matter in the output.
- `Reduce`: Collapse fields or series to summary values. Use it only when the panel truly needs a reduced result.

## Join and combine primitives

- `Join by field`: Join query results on a shared field.
- `Join by labels`: Align series by label sets instead of a field column.
- `Merge series/tables`: Combine frames with matching fields when you need a merged result, not explicit join semantics.

## Shape and presentation primitives

- `Prepare time series`: Convert between time-series frame shapes for the target panel.
- `Rows to fields`: Turn row values into separate fields.
- `Labels to fields`: Promote labels into fields.
- `Series to rows`: Flatten series into row-oriented output.
- `Series to columns`: Pivot repeated series into fields when a table-style inspection view needs one column per series or label.
- `Convert field type`: Fix field types before later transforms depend on them.
- `Rename by regex`: Rename fields structurally.
- `Organize fields by name`: Reorder, hide, and rename final fields for a single-query result.
- `Sort by`: Order the final inspection table after the shape is settled.

If multiple primitives seem possible, use [joins-calculations.md](joins-calculations.md) and [field-shaping.md](field-shaping.md) before chaining them.
