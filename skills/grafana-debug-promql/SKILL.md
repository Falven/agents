---
name: grafana-debug-promql
description: Debug PromQL used in Grafana panels. Use when a Prometheus-backed Grafana query returns no data, wrong values, missing series, unstable legends, unexpected spikes, counter mistakes, label-matching errors, step or range problems, or high-cardinality performance issues.
---

# Grafana Debug PromQL

Debug the PromQL and Grafana query path before blaming the panel.

## When to Apply

Use this skill when debugging Prometheus-backed Grafana panels that:

- return no data
- drop expected series
- show wrong values or unstable spikes
- break after label filtering or binary expressions
- depend on the wrong query type, step, or range
- return too many series, too many points, or run too slowly

Do not widen the task beyond Grafana-native PromQL debugging. This skill is for fixing the query and explaining how to verify it in Grafana.

## Workflow

1. State the failure mode: no data, missing subset, wrong values, matching failure, or performance/cardinality.
2. In Grafana, check query type (`Both`, `Range`, `Instant`), datasource, time range, step, and Query Inspector before changing the query. Some dashboards mix Prometheus, Loki, and `__expr__` targets in the same family.
3. Reduce to a raw selector that should return data, then rebuild in this order: range function, aggregation, binary operation, panel-specific shaping.
4. Match the failure mode to one reference file first. Load additional references only when the query crosses concerns.
5. Verify the fix in Grafana with the same panel time range and inspect returned series counts when relevant.

## Reference Map

- [references/no-data.md](references/no-data.md) -> start here when the whole query is empty; covers selector validation, Grafana query type, `$__rate_interval`, scrape-window mismatch, and absent vs stale behavior
- [references/empty-series.md](references/empty-series.md) -> use when the metric exists but some expected label combinations disappear during filtering, aggregation, or binary math
- [references/range-step-debugging.md](references/range-step-debugging.md) -> Grafana query mechanics: `Both`, `Range`, `Instant`, step alignment, Query Inspector, and series-count checks
- [references/label-mismatches.md](references/label-mismatches.md) -> label filters, variable regex mistakes, vector matching, `on`, `ignoring`, `group_left`, `group_right`, and legend explosions
- [references/matching-range-cardinality.md](references/matching-range-cardinality.md) -> use when range selection, vector matching, and cardinality interact in the same ratio or binary expression
- [references/wrong-values.md](references/wrong-values.md) -> use when the query returns data but the numbers are semantically wrong
- [references/promql-pitfalls.md](references/promql-pitfalls.md) -> concise PromQL rules for counter vs gauge, `rate` before aggregate, `irate` vs `rate`, histogram differences, and stale vs absent traps
- [references/performance-cardinality.md](references/performance-cardinality.md) -> slow queries, too many series, too many points, and concrete Grafana-side remediation

## How to Route

- Empty panel or empty expression: start with [references/no-data.md](references/no-data.md).
- Metric exists, but some labels or instances vanished: use [references/empty-series.md](references/empty-series.md).
- Query behaves differently in Grafana than in Prometheus or Explore: use [references/range-step-debugging.md](references/range-step-debugging.md).
- Ratios, joins, or legends look wrong: use [references/label-mismatches.md](references/label-mismatches.md) and then [references/matching-range-cardinality.md](references/matching-range-cardinality.md) if range and cardinality are part of the same failure.
- Values are present but semantically wrong: use [references/wrong-values.md](references/wrong-values.md), then [references/promql-pitfalls.md](references/promql-pitfalls.md) for rule-level checks.
- Query is slow, noisy, or blows up the panel: use [references/performance-cardinality.md](references/performance-cardinality.md).

## Output

Return the root cause, the corrected query or query change, and how to verify the fix in Grafana.
