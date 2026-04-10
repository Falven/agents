---
name: grafana-use-dashboard-variables
description: Design and apply Grafana dashboard variables and templating. Use when creating or debugging query, custom, text box, constant, data source, interval, ad hoc filter, or switch variables, wiring variables into PromQL, configuring chained variables, or setting up repeating panels or rows whose behavior depends on variable selection.
---

# Grafana Use Dashboard Variables

Use variables to make dashboards navigable and reusable without hiding what the query is doing. Keep the variable model explicit because it changes query semantics, panel titles, repeat behavior, and dashboard cost.

## When to Apply

Use this skill when the dashboard problem is primarily about:

- Choosing the right Grafana variable type.
- Interpolating variables into queries, titles, and links.
- Making Prometheus-backed variables behave correctly with multi-select, `All`, or time-aware lists.
- Repeating panels or rows from a variable.
- Debugging dashboards whose output changes with variable state.

## Workflow

1. Decide what the user should be able to filter or compare.
2. Pick the simplest variable type that supports that interaction.
3. Decide whether the variable is standalone, chained from another variable, or already covered by a Grafana global variable.
4. Wire the variable into PromQL, titles, and links with explicit interpolation syntax.
5. Use repetition only when comparison value outweighs layout cost.
6. Check defaults, `All`, multi-value expansion, and dependency refresh behavior.

## Reference Map

- `references/variable-types.md` -> variable types, chained variables, and when Grafana globals matter.
- `references/variable-syntax-and-formatting.md` -> interpolation forms and the formatter subset this skill should teach.
- `references/promql-variable-patterns.md` -> Prometheus-specific variable queries and PromQL interpolation rules.
- `references/repeating-panels-and-rows.md` -> prerequisites, layout constraints, and repeat caveats.
- `references/variable-debugging.md` -> preview values, dependencies, ad hoc filters, and repeat failures.

## Output

Return the proposed variable design, the exact interpolation pattern to use, the query and title implications, and any repeat or performance tradeoff that materially affects the dashboard.
