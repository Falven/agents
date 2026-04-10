# Queries, Conditions, and Expressions

## Query Input

- Grafana-managed rules only work with backend, alerting-enabled datasources.
- Advanced mode evaluates queries with fixed relative time ranges. It does not inherit the dashboard time picker or a panel's ad hoc exploration window.
- Dashboard queries often use `instant` mode or `__expr__` nodes to simplify the panel. Rebuild the alert rule from the underlying datasource queries and keep the datasource explicit.
- `$__rate_interval` is a dashboard default for counter graphs, not an alerting default. Use it as a clue about the metric type, then choose the alert window and reduction deliberately.
- Start with the query that directly captures the symptom. Keep panel-only transforms and presentation logic out of the rule.

## Time Series vs Table

- Time series queries return one or more labeled series over time. `Reduce` collapses each series across the evaluation window into one number such as `Last`, `Min`, `Max`, or `Mean`.
- Table queries are valid when Grafana can identify one numeric field to evaluate and other stable fields to use as labels.
- After reduction or row selection, the condition works on single numbers. It does not evaluate a raw time window directly.

## Expression Semantics

- `Reduce` is the normal bridge from time series to alert condition. It preserves per-series fanout while turning each series into one value.
- `Math` combines numeric outputs from queries or expressions. It matches items by labels, not by query order, so incompatible label sets can disappear or join in surprising ways.
- `Resample` realigns timestamps before `Math` when two time series would otherwise not line up in time. Use it only to solve timestamp alignment problems.
- `Threshold` compares single numbers and returns `1` when true and `0` when false. When it is the alert condition, firing happens when the result is `1`.
- Recovery threshold belongs to the same `Threshold` expression as hysteresis. Do not model it as a second condition.
- Dashboard-style boolean shaping such as `== 1`, `> 0`, `clamp_max`, or `or on() vector(0)` is often there to make a panel render cleanly or preserve compatibility. Translate it deliberately for alerting rather than copying it as-is.

## Classic Condition

- Classic condition is legacy and should be avoided when possible.
- It checks whether any time series matches the condition and always produces one alert instance, even if many series match.
- Prefer `Reduce -> Threshold` when you need multi-dimensional alerts, readable expression chains, or recovery threshold support.
