# Repeating Panels and Rows

Use repetition when side-by-side or stacked comparison is the point of the dashboard, not as a substitute for a better overview panel.

Prerequisites:

- Repeat panels, rows, and tabs from a variable that can yield multiple values.
- In practice, that means using a variable configured for multi-value selection, or another setup that can expand to more than one value.
- Make sure the repeated panel or row title includes the repeated variable so each copy stays identifiable.

Layout behavior:

- Horizontal repeats are best for a small bounded set of comparable panels.
- Vertical repeats are better when each panel needs full width or when the set may be longer.
- Horizontal repeats cannot share the same row with unrelated panels. Plan the row around the repeated panel only.
- Keep the repeated panel simple because every query, legend, and transformation multiplies across the repeat count.

Scope rules:

- Use repetition on bounded sets. Repeating over a large fleet creates noise and high query fan-out.
- Prefer one overview panel plus drill-down links when repetition would generate a wall of nearly identical panels.
- Check the default selection so the dashboard does not open in an unusable repeated state.

Caveat:

- With the `Dashboard` datasource, repeated rows still reference the original row's source panel. If the repeated copy appears to show the wrong source data, check whether the repeat is still bound to the original panel selection.
