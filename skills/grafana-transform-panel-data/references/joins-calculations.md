# Joins and Calculations

These primitives are not interchangeable. Pick the one that matches the output shape you need.

## Calculation primitives

- `Add field from calculation`: Add a derived field from existing fields in the current frame. Use it when you still want the original rows or series plus a new calculated value.
- `Group by`: Group rows on key fields, then compute aggregates inside each group. Use it when the grouped keys must remain visible in the result.
- `Reduce`: Collapse each field or series to summary values. Use it only when the panel needs a reduced result, not when later steps still need the unreduced frame.

## Join and combine primitives

- `Join by field`: Explicitly join query results on a shared field.
- `Join by field` with `INNER`: Keep only matching keys.
- `Join by field` with `OUTER (TIME SERIES)`: Preserve a time-series union across timestamps.
- `Join by field` with `OUTER (TABULAR)`: Preserve a tabular union across join keys.
- `Join by labels`: Align series by label sets instead of a field column.
- `Merge series/tables`: Combine frames with matching fields when you want one merged frame, not explicit join semantics.

Checks:

- Join only when two results genuinely need to be viewed together.
- Align field keys and types before attempting a join.
- After each calculation or join, state whether the output is still a time series, a grouped table, or a reduced summary.
