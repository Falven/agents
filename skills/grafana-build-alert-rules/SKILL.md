---
name: grafana-build-alert-rules
description: Build Grafana-managed alert rules from dashboard or Prometheus queries. Use when turning a panel query into an alert, defining reduce, math, threshold, or recovery conditions, choosing evaluation behavior, or checking whether a query and datasource are safe and meaningful for Grafana alerting.
---

# Grafana Build Alert Rules

Build or review Grafana-managed alert rules from a panel or query. Keep the rule tied to one failure mode, one condition, clear recovery behavior, and explicit no-data handling.

## When to Apply

Reference this skill when:

- Converting a Grafana panel query into a Grafana-managed alert rule
- Reviewing a Grafana-managed rule for query, expression, or condition correctness
- Deciding whether logic belongs in PromQL or in Grafana expressions
- Defining recovery threshold, `Keep firing for`, and `No Data` or `Error` behavior
- Checking labels, annotations, and template variables for multi-instance alerts

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | `rule-shape` | HIGH | `rule-shape-` |
| 2 | `query-expression` | HIGH | `query-expression-` |
| 3 | `recovery-states` | HIGH | `recovery-states-` |
| 4 | `promql-patterns` | MEDIUM | `promql-patterns-` |

## Quick Reference

### 1. Rule Shape (HIGH)

- `reduce-before-threshold` - Grafana-managed rules have one condition; reduce each series or table row into the value that condition evaluates.
- `labels-and-template-caveats` - Stable labels are part of alert correctness, and `$values` is usually the right template input.

### 2. Query Expression (HIGH)

- `use-promql-before-grafana-expressions` - Keep rate, ratio, and histogram logic in PromQL when possible; use Grafana expressions for the final alert-specific shaping.
- Dashboard panel shortcuts like `instant`, `__expr__`, `or on() vector(0)`, `== 1`, `> 0`, or `clamp_max` are visualization shaping, not a ready-made alert condition.

### 3. Recovery States (HIGH)

- `recovery-no-data-missing-series` - Treat recovery threshold, `Keep firing for`, `No Data`, `Error`, and `MissingSeries` as separate controls.

### 4. PromQL Patterns (MEDIUM)

- `references/alert-design-patterns.md` - Concrete ratio, histogram quantile, and missing-series alert shapes.

## How to Use

Read the matching file in `rules/` first for the main decision, then load the matching file in `references/` for the mechanics that justify it.

Return:

- The alert query or expression chain
- The final condition shape in plain language
- Recovery behavior, including whether recovery threshold or `Keep firing for` is needed
- Explicit `No Data` and `Error` handling
- One note on label identity, alert-instance fanout, or likely noise

## Reference Map

- `references/alert-rule-shape.md` - one-condition model, alert instances, labels, and templating
- `references/queries-conditions-expressions.md` - time series vs table inputs, `Reduce`, `Math`, `Resample`, `Threshold`, and classic condition limits
- `references/alerting-caveats.md` - datasource constraints, fixed relative time ranges, and alert state caveats
- `references/alert-design-patterns.md` - concrete PromQL alert patterns for ratios, latency histograms, and missing series
