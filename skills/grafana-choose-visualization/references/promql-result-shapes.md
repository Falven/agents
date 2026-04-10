# PromQL Result Shapes

- Range vector from counters, gauges, rates, or derived scalar series -> `Time series`
- Instant scalar after aggregation -> `Stat`; use `Gauge` or `Bar gauge` only when bounds or thresholds are part of the question
- `topk()` or grouped instant vector -> `Bar chart` or `Table`
- Derived percentile or average series from histogram data, such as `histogram_quantile(...)` over time -> `Time series`
- Native histogram data used as a time-evolving distribution -> `Heatmap`
- Classic histogram bucket series such as `*_bucket` with `le` over time -> `Heatmap`
- Classic histogram bucket counts at one instant -> `Bar chart` or `Table` if you must inspect bucket counts directly
- Raw `*_bucket` series are already bucketed counts, not generic numeric observations -> do not send them to `Histogram`
- `Histogram` fits only when the result is a set of numeric observations or values that Grafana itself should rebucket into bins
- Label-rich diagnostic output -> `Table`

If the query returns too many series, fix the query before choosing a denser panel.
