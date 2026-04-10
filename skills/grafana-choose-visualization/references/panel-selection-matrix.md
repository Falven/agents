# Panel Selection Matrix

Start with the x-axis semantics or data shape, then pick the panel:

| Shape or semantics | Primary panel | Use when | Prefer instead of |
| --- | --- | --- | --- |
| `time` | `Time series` | The x-axis is real time and the question is trend, rate, seasonality, spikes, or comparison over time | `Trend` for time data |
| `categorical` | `Bar chart` | You are comparing categories, labels, or top N groups in one dataset | `Time series` unless the data is actually time-based |
| `sequential numeric non-time` | `Trend` | The x-axis is ordered numeric progression but not time, such as step, percentile, build number, or block height | `Time series` when there is no clock on the x-axis |
| `arbitrary x/y` | `XY chart` | The data is tabular x/y pairs or scatter-style points where either axis can be numeric | `Time series` when x is not time and `Trend` when the relationship is not a simple sequence |
| `single value` | `Stat` | The question is the latest, current, total, average, or other single KPI | `Gauge` or `Bar gauge` unless the value needs to be judged against bounds, capacity, or thresholds |
| `distribution` | `Histogram` or `Heatmap` | Use `Histogram` to rebucket numeric values into a distribution snapshot; use `Heatmap` for how the distribution changes over time | Generic `Bar chart` for bucketed distributions over time |
| `discrete state` | `State timeline` or `Status history` | Use `State timeline` for state-change views; use `Status history` when each sampled interval matters and equal consecutive values should stay separate | Dense `Table` output for state changes |
| `logs/traces/topology` | `Logs`, `Traces`, `Node graph`, or `Flame graph` | The data is already log lines, spans, dependency topology, or profiling stacks | Generic charts for observability-native data |

Additional selection rules:

- Use `Stat` for a single value by default. Switch to `Gauge` or `Bar gauge` only when the value is being judged against bounds, capacity, or thresholds.
- Use `Time series` as the default starting point for time-indexed official dashboards.
- Treat legacy imported `graph` panels as `Time series` and legacy `singlestat` panels as `Stat`.
- Use `Table` for inspection and drill-down, not as the primary above-the-fold panel.
- Use `Bar chart` for categories and one dataset. If the data is dense over time, stay in `Time series` and render bars there instead of moving to `Bar chart`.
- Use `Histogram` for raw numeric values that need bucketing. Use `Heatmap` for distributions over time, especially when the source is already bucketed by time.
- Keep `Logs`, `Heatmap`, `State timeline`, and `Status history` narrow and intent-driven rather than generic defaults.
- Use `State timeline` when merged runs of the same value help the reader see state changes. Use `Status history` when those repeats should remain visible as separate intervals.

Choose readability over novelty. If two panels fit, prefer the one that answers the user's question faster.
