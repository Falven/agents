# PromQL Patterns

- Throughput trend -> `sum by (service) (rate(counter_total[$__rate_interval]))`
- Total events in the current lookback window -> `sum by (service) (increase(counter_total[$__rate_interval]))`
- Volatile counter view -> `sum by (instance) (irate(counter_total[$__rate_interval]))`
- Error ratio -> `sum by (service) (rate(errors_total[$__rate_interval])) / sum by (service) (rate(requests_total[$__rate_interval]))`
- Classic histogram percentile -> `histogram_quantile(0.95, sum by (le, service) (rate(duration_bucket[$__rate_interval])))`
- Native histogram percentile -> `histogram_quantile(0.95, sum by (service) (rate(duration[$__rate_interval])))`
- Classic histogram heatmap density -> `sum by (le) (rate(duration_bucket[$__rate_interval]))`
- Classic histogram heatmap counts -> `sum by (le) (increase(duration_bucket[$__rate_interval]))`
- Classic histogram SLO ratio at `0.2s` -> `sum by (service) (rate(duration_bucket{le="0.2"}[$__rate_interval])) / sum by (service) (rate(duration_count[$__rate_interval]))`
- Saturation or utilization -> aggregate the busy resource metric and normalize if needed; for gauges like `workqueue_depth`, do not use `rate()`
- Top N -> `topk(5, sum by (service) (rate(counter_total[$__rate_interval])))`

Start from the user's question, then choose the smallest pattern that answers it.

- If a Grafana Prometheus variable supports multi-value or all-value selection, use `=~` in the label matcher.
- For joins or ratios that are not matching cleanly, read [label-matching.md](label-matching.md) and [promql-aggregation-labels.md](promql-aggregation-labels.md).
