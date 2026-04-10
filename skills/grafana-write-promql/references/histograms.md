# Histograms

Decide first whether the metric is a classic histogram or a native histogram.

## Classic Histograms

- Classic histograms expose `_bucket`, `_sum`, and `_count` series.
- Percentiles use `_bucket` data, `rate(...)`, and `sum by (le, ...)` before `histogram_quantile()`.
- Preserve the `le` label until the quantile or distribution step that needs it.
- Example p95: `histogram_quantile(0.95, sum by (le, service) (rate(http_request_duration_seconds_bucket[$__rate_interval])))`
- Example average: `sum by (service) (rate(http_request_duration_seconds_sum[$__rate_interval])) / sum by (service) (rate(http_request_duration_seconds_count[$__rate_interval]))`
- For heatmaps, keep the bucket series and aggregate by `le` first; official dashboards use per-second density `sum by (le) (rate(http_request_duration_seconds_bucket[$__rate_interval]))` or per-window counts `sum by (le) (increase(http_request_duration_seconds_bucket[$__rate_interval]))`.

## Native Histograms

- Native histograms are queried from the base metric directly. Do not append `_bucket`.
- Percentiles operate on histogram samples returned from `rate(metric[$__rate_interval])`.
- Example p95: `histogram_quantile(0.95, sum by (service) (rate(http_request_duration_seconds[$__rate_interval])))`
- Example average: `histogram_avg(sum by (service) (rate(http_request_duration_seconds[$__rate_interval])))`

## Panel Fit

- `Format=Heatmap` is for bucket-shaped output over time, usually classic histogram buckets.
- `Format=Time series` is for quantiles, averages, or SLO ratios plotted as lines.
- `Format=Table` only belongs in a Table panel.
