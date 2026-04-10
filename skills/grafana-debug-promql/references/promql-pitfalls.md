# Common PromQL Pitfalls

Use this as a short semantic cross-check after you have localized the failure.

## Rules

- Do not use `rate()` or `increase()` on gauges
- Apply `rate()` to counters before aggregation
- Use `irate()` for volatile, near-now inspection; use `rate()` for stable dashboards and alerts
- Unmatched series disappear by default in binary operations
- Classic histograms and native histograms do not follow the same debugging rules

## Examples

Bad:

```promql
sum by (job) (irate(cpu_temperature_celsius[$__rate_interval]))
```

This is a gauge forced through `irate()`.

Bad:

```promql
rate(sum by (job) (http_requests_total)[$__rate_interval])
```

This hides resets.

Better:

```promql
sum by (job) (rate(http_requests_total[$__rate_interval]))
```

## Histogram Distinction

- Classic histogram percentile queries use `_bucket` metrics and keep `le` until after bucket aggregation
- Native histograms are a different metric type and should not be forced into classic bucket patterns
- If `histogram_quantile()` is wired to a non-bucket classic metric, the query shape is wrong

## Absent and Staleness

- `absent()` is a selector check at one evaluation time
- `absent_over_time()` checks an entire range
- A stale series is not the same thing as a selector that never matched

## Final Reminder

- Treat panel units as a presentation concern until the PromQL itself is proven wrong
- Treat empty results after binary math as a matching problem before assuming ingestion broke
