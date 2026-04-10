# Panel Semantics

Presentation bugs are real bugs. Correct source data can still communicate the wrong thing.

## Meaning Checks

- Verify units first. A seconds value shown as milliseconds, or an epoch shown with the wrong unit, can make healthy data look broken.
- Check `No value` behavior so missing data is not silently presented as a real zero or friendly placeholder.
- Thresholds and value mappings can relabel correct values into the wrong state.

## Visual Semantics

- `Connect null` can invent continuity that the source data does not support.
- Stacking can hide individual series behavior or create misleading totals when the intent was comparison.
- If the panel type hides the signal, change the panel before rewriting the query.
- Mixed metrics/logs dashboards and annotations can be deliberate. Validate the intended datasource mix before treating them as contamination.
- `text` panels with blank titles or empty content are often section scaffolding or layout debt, not query failures.

## Practical Rule

- If the raw and transformed data are correct, treat the panel as the bug surface until proven otherwise.
