# Variables and Links

Treat variables and links as part of the query path, not as dashboard chrome.

## Variable Checks

- Use variable preview first. Confirm the option list and current value match the datasource state.
- Check the variable refresh mode. Stale variables can make correct panels look broken.
- Verify multi-value escaping and formatting. Some queries need raw format instead of datasource-specific quoting or regex wrapping.
- Inspect custom `All` values. A bad `All` expansion can silently query nothing or far too much.
- For chained variables, verify parent refresh order before touching child queries.
- When a selector or link fails on one sibling dashboard but not another, compare the variable name and the selector metric in the variable query first; the break often lives there, not in the panel query.

## Repetition and URL Context

- Broken repetition often comes from variable values that expand panel count or produce empty child variables.
- For multi-select links, expect repeated `var-name=value` URL params rather than a single combined value.
- Compare linked dashboards for variable name mismatches, missing defaults, and missing refresh triggers.
- Propagate both time range and template variables through links when the destination dashboard must preserve context.

## Ad Hoc Filters

- Check ad hoc filters separately from named variables. They can change the final query without obvious panel-level clues.
- If a panel disagrees with Explore, confirm the same ad hoc filter state exists in both places.
