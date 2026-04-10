# Alert Design Patterns

## Ratio Alerts

Use ratios instead of raw counts when traffic volume changes.

```promql
sum by (job) (rate(http_requests_total{job="api", code=~"5.."}[5m]))
/
sum by (job) (rate(http_requests_total{job="api"}[5m]))
> 0.05
```

- Apply `rate()` to counters before `sum by (...)` or other aggregation.
- Keep the routing labels you actually want to alert on. Dropping extra labels before the condition reduces noisy fanout.

## Histogram Quantiles

Use histogram buckets, not precomputed percentiles, when building PromQL-backed latency alerts.

```promql
histogram_quantile(
  0.95,
  sum by (le, job) (
    rate(http_request_duration_seconds_bucket{job="api"}[5m])
  )
)
> 0.75
```

- Keep `le` in the aggregation for classic histograms.
- Do not average already computed percentiles across instances.
- Prefer PromQL for the histogram math, then use Grafana only for the final alert condition or recovery threshold.

## Missing Data and Missing Series

Use PromQL absence checks when the signal itself disappearing is the failure mode.

```promql
absent_over_time(up{job="api"}[10m])
```

- `absent_over_time()` detects a whole signal disappearing over the chosen window.
- Grafana `MissingSeries` handling is different: it resolves stale per-instance alerts after a series disappears, but it does not replace explicit absence logic when missing data is the thing you want to alert on.

If only some expected targets can disappear, compare the observed series against a stable inventory metric or discovery metric.

```promql
kube_pod_info{namespace="prod", pod=~"api-.*"}
unless on(namespace, pod)
max_over_time(up{job="kubernetes-pods", namespace="prod", pod=~"api-.*"}[10m])
```

- This pattern returns expected pods that stopped producing `up` samples.
- Use explicit `on(...)` matching so the missing dimension is clear.
