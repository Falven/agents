---
name: grafana-write-promql
description: Write PromQL for Grafana dashboard panels. Use when creating Prometheus-backed dashboard queries for time series, stat, gauge, bar chart, histogram, heatmap, or table panels, especially for latency, throughput, error rate, saturation, utilization, top-N, and SLO-style views.
---

# Grafana Write PromQL

Write PromQL that is correct for Grafana panels, not just valid in Prometheus.

## When to Apply

- Writing or reviewing PromQL for Grafana panels backed by Prometheus.
- Translating a dashboard question into a ready-to-paste query plus the right panel query settings.
- Building time series, stat, gauge, bar chart, heatmap, histogram, or table views for rates, ratios, latency, saturation, top-N, or SLO-style panels.

## Workflow

1. Restate the metric question in plain language before writing the query.
2. Choose the Grafana query shape first. Use [references/range-vs-instant.md](references/range-vs-instant.md) for query `Type` (`Range`, `Instant`, `Both`) and [references/dashboard-query-style.md](references/dashboard-query-style.md) for `Format` (`Time series`, `Table`, `Heatmap`).
3. Use [references/promql-patterns.md](references/promql-patterns.md) to choose the starting pattern.
4. Refine the query with the narrowest relevant reference:
   - counters, rates, resets, and `$__rate_interval` -> [references/promql-counters-rates.md](references/promql-counters-rates.md)
   - classic vs native histograms -> [references/histograms.md](references/histograms.md)
   - percentiles, averages, and SLO-style bucket math -> [references/promql-histograms-percentiles.md](references/promql-histograms-percentiles.md)
   - grouping, joins, and binary matching -> [references/label-matching.md](references/label-matching.md)
   - aggregation shape and label retention -> [references/promql-aggregation-labels.md](references/promql-aggregation-labels.md)
   - dashboard query `Type`/`Format` and panel-oriented PromQL shapes -> [references/dashboard-query-style.md](references/dashboard-query-style.md)
5. Return a ready-to-paste Grafana query plus only the panel notes that matter: query `Type`, `Format`, legend, unit, variable matcher assumptions, or histogram type.

## Reference Map

- [references/dashboard-query-style.md](references/dashboard-query-style.md) -> Grafana panel habits, query `Type`, query `Format`, legends, and variable matchers
- [references/range-vs-instant.md](references/range-vs-instant.md) -> when to use `Range`, `Instant`, or `Both`
- [references/promql-patterns.md](references/promql-patterns.md) -> starting patterns for common dashboard questions
- [references/promql-counters-rates.md](references/promql-counters-rates.md) -> `rate`, `irate`, `increase`, reset-safe ordering, and `$__rate_interval`
- [references/histograms.md](references/histograms.md) -> branch early between classic and native histograms
- [references/promql-histograms-percentiles.md](references/promql-histograms-percentiles.md) -> percentiles, averages, bucket arithmetic, and `histogram_fraction()` caveats
- [references/label-matching.md](references/label-matching.md) -> `on`, `ignoring`, `group_left`, `group_right`, and dropped unmatched series
- [references/promql-aggregation-labels.md](references/promql-aggregation-labels.md) -> aggregation shape, kept labels, and ratio alignment

## Output

Return:

- one ready-to-paste query
- the intended Grafana query `Type` and `Format` when they matter
- the assumption behind the rate window, usually `$__rate_interval`
- the panel sampling interval when it is separate from the PromQL lookback window
- any required follow-on panel configuration such as legend, unit, or "use `=~` for the Grafana variable"
