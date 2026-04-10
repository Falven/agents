# Dashboard Query Style

Start from the panel output, then write the PromQL.

## Pick Query `Type`

- `Range` for time-based plots and anything that should show change over time.
- `Instant` for a single current value or current ranking. It returns one value per series at the evaluation timestamp.
- `Both` only when the panel or workflow needs both the plotted series and the current sample from the same expression.

## Pick Query `Format`

- `Time series` for most Prometheus queries, including lines, bars, stats, and gauges.
- `Table` only when the panel is a Table panel.
- `Heatmap` for Prometheus histogram bucket output that should render as a heatmap.

## Practical Rules

- Prefer rates, ratios, and aggregates that stay readable at dashboard scale.
- Keep legend labels short and stable.
- Aggregate before visualizing if raw cardinality would overwhelm the panel, but do `rate()` before aggregation on counters.
- Keep the PromQL lookback window on `$__rate_interval` for counter trends, even when the panel sampling interval is driven by a separate step variable such as `$resolution`.
- Shape and aggregate in PromQL first; use Grafana transformations only when the panel needs presentation-only cleanup.
- Use `Format=Heatmap` for histogram bucket data, not percentile lines.
- Heatmaps can also show per-window bucket counts with `increase(...[$__rate_interval])` grouped by `le`.
- If a Prometheus Grafana variable allows multi-value or all-value selection, use a regex matcher such as `{service=~"$service"}` instead of `{service="$service"}`.

## Examples

- Current request rate stat: `Type=Instant`, `Format=Time series`, `sum(rate(http_requests_total[$__rate_interval]))`
- Latency heatmap from classic buckets: `Type=Range`, `Format=Heatmap`, `sum by (le) (rate(http_request_duration_seconds_bucket[$__rate_interval]))`
- Latency heatmap from per-window bucket counts: `Type=Range`, `Format=Heatmap`, `sum by (le) (increase(http_request_duration_seconds_bucket[$__rate_interval]))`
- Current error table by service: `Type=Instant`, `Format=Table`, `topk(10, sum by (service) (rate(http_requests_total{status=~"5.."}[$__rate_interval])) / sum by (service) (rate(http_requests_total[$__rate_interval])))`
