# PromQL Histograms and Percentiles

Call out early whether the metric is a classic histogram or a native histogram. The query shape changes.

## Classic Histogram Patterns

- Aggregate buckets before `histogram_quantile()` at the same label granularity you want to plot.
- Keep `le` in the grouping until the quantile step.
- Use `_sum` and `_count` for averages when percentile detail is not required.
- For heatmaps, keep the bucket series instead of reducing to a percentile; official dashboards use `sum by (le) (rate(..._bucket[$__rate_interval]))` for density and `sum by (le) (increase(..._bucket[$__rate_interval]))` for per-window counts.

Examples:

- P95 latency: `histogram_quantile(0.95, sum by (le, service) (rate(http_request_duration_seconds_bucket[$__rate_interval])))`
- Average latency: `sum by (service) (rate(http_request_duration_seconds_sum[$__rate_interval])) / sum by (service) (rate(http_request_duration_seconds_count[$__rate_interval]))`
- SLO ratio at an exact bucket boundary: `sum by (service) (rate(http_request_duration_seconds_bucket{le="0.2"}[$__rate_interval])) / sum by (service) (rate(http_request_duration_seconds_count[$__rate_interval]))`

## Native Histogram Patterns

- Query the base metric directly.
- Use histogram functions on the histogram samples returned by `rate(...)`.

Examples:

- P95 latency: `histogram_quantile(0.95, sum by (service) (rate(http_request_duration_seconds[$__rate_interval])))`
- Average latency: `histogram_avg(sum by (service) (rate(http_request_duration_seconds[$__rate_interval])))`

## `histogram_fraction()` Caution

- `histogram_fraction()` on classic histograms is estimate-based because it interpolates between bucket boundaries.
- If the threshold you care about matches an actual classic bucket boundary, direct bucket arithmetic is safer and easier to explain than `histogram_fraction()`.
- Use `histogram_fraction()` more confidently with native histograms, or with classic histograms only when you accept interpolation error.
