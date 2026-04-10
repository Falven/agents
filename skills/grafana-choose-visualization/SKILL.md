---
name: grafana-choose-visualization
description: Choose the right Grafana visualization or panel type from data shape, x-axis semantics, and dashboard intent. Use when deciding between Time series, Trend, XY chart, Stat, Gauge, Bar chart, Histogram, Heatmap, Table, State timeline, Status history, Logs, Traces, Node graph, and other built-in panels before tuning panel options or layout. Useful when a query or dataset already exists but the best panel is unclear.
---

# Grafana Choose Visualization

Choose the panel type from the data shape, the meaning of the x-axis, and the question being answered.

## When to Apply

Use this skill when:

- A query, result set, or table already exists and the main question is which Grafana panel fits it
- The user needs one primary panel recommendation, optionally with one fallback
- The work is panel selection, not detailed field overrides, thresholds, or layout tuning

## Workflow

1. Classify the result shape and x-axis semantics first: `time`, `categorical`, `sequential numeric non-time`, `arbitrary x/y`, `single value`, `distribution`, `discrete state`, or `logs/traces/topology`.
2. Read [references/panel-selection-matrix.md](references/panel-selection-matrix.md) to map intent to a primary panel.
3. Read [references/promql-result-shapes.md](references/promql-result-shapes.md) when the query is PromQL.
4. Read [references/built-in-visualizations.md](references/built-in-visualizations.md) when you need a quick reminder of nearby built-in alternatives.
5. Check [references/panel-anti-patterns.md](references/panel-anti-patterns.md) to rule out misleading choices.
6. Return one primary panel recommendation and, when helpful, one fallback.

## Official Dashboard Pattern

- The official upstream Grafana dashboards here are overwhelmingly `Time series`-first for time-indexed operational data.
- Legacy imported `graph` panels should usually be read as modern `Time series`, and legacy `singlestat` panels as modern `Stat`.
- Treat `Table`, `Logs`, `Heatmap`, `State timeline`, and `Status history` as intent-specific views for inspection, log review, distribution over time, or discrete state history.

## Reference Map

- [references/built-in-visualizations.md](references/built-in-visualizations.md) -> fast inventory of the built-in Grafana panels relevant to dashboard creation
- [references/panel-selection-matrix.md](references/panel-selection-matrix.md) -> choose the panel from data shape, x-axis semantics, and analytical goal
- [references/promql-result-shapes.md](references/promql-result-shapes.md) -> map common PromQL result shapes to the right visualization
- [references/panel-anti-patterns.md](references/panel-anti-patterns.md) -> avoid misleading or unreadable panel choices

## Output

Return the chosen panel, why it fits, what it emphasizes, what tradeoff it makes, and which configuration skill should be used next.
