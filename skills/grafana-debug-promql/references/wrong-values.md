# Wrong Values

Use this when data is present but the numbers are wrong.

## Counter vs Gauge

- Counters usually need `rate()` or `increase()` before you graph a change over time
- Gauges should not be wrapped in `rate()` just because the line looks noisy
- If a metric can go down naturally, treat it like a gauge until proven otherwise
- Queue-depth panels such as `workqueue_depth` are gauges in upstream dashboards; `rate(workqueue_depth[...])` is the wrong shape

## Rate Before Aggregate

Bad:

```promql
rate(sum by (job) (http_requests_total)[$__rate_interval])
```

Good:

```promql
sum by (job) (rate(http_requests_total[$__rate_interval]))
```

Apply `rate()` to each counter series before aggregating, or resets get hidden and values go wrong.

## `irate()` vs `rate()`

- Use `rate()` for dashboards and alerts that should be stable across the selected window
- Use `irate()` only when you explicitly want the most recent, more volatile change
- If a dashboard looks jumpy for a slow-moving service, replace `irate()` with `rate()`

## Histograms

- Classic histograms use `_bucket` series and need `le` preserved until after bucket aggregation
- Example:

```promql
histogram_quantile(
  0.95,
  sum by (job, le) (rate(http_request_duration_seconds_bucket[$__rate_interval]))
)
```

- Native histograms are not classic `_bucket` series and should not be debugged with classic `le` assumptions
- If the metric is native histogram data, use histogram-aware functions and keep the debugging path separate from classic bucket guidance
- For heatmap or bucket panels, confirm whether the dashboard intends `rate()` or `increase()` before changing the query; both appear upstream, but they answer different questions

## Panel-State Logic

- Comparisons like `> 0` and `== 1` are part of the query semantics, not just filters
- `clamp_max()` caps values and can hide the real magnitude
- `or on() vector(0)` is often intentional to keep an empty panel visible
- Treat these as shaping operators when debugging confusing values, especially in stat or status panels

## Window and Unit Checks

- Too-short windows make low-volume services look bursty or empty
- Too-long windows can hide changes and make current behavior look stale
- Check unit mismatches before editing panel display settings or rewriting the query
