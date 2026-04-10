# Panel Anti-Patterns

- Do not use `Pie chart` for time series or too many categories.
- Do not use `Trend` for real time on the x-axis; use `Time series`.
- Do not use `Time series` when the x-axis is ordered numeric but not time; use `Trend`.
- Do not use `Time series` or `Trend` for arbitrary x/y tabular relationships; use `XY chart`.
- Do not use `Gauge` when the real question is trend or rate of change.
- Do not use `Gauge` or `Bar gauge` when there are no meaningful bounds, targets, or thresholds; use `Stat`.
- Do not treat legacy imported `graph` panels as a separate modern recommendation; map them to `Time series`.
- Do not treat legacy imported `singlestat` panels as a separate modern recommendation; map them to `Stat`.
- Do not use `Bar chart` for dense time data just because bars look right; keep `Time series` and render bars there.
- Do not use `Histogram` for Prometheus classic `*_bucket` series; use `Heatmap` for distributions over time, or `Bar chart`/`Table` for a single bucket snapshot.
- Do not use `Heatmap` when the real question is a single distribution snapshot from raw numeric values; use `Histogram`.
- Do not use `Status history` when you want merged runs of the same state; use `State timeline`.
- Do not use `State timeline` when repeated equal values must remain visibly separate; use `Status history`.
- Do not use `Table` as the primary above-the-fold view when operators need to spot motion quickly; use it for inspection and drill-down.
- Do not use `Logs` or `Heatmap` as generic chart substitutes; they are narrow views for log lines and bucketed distributions over time.
- Do not use `State timeline` or `Status history` as generic defaults; reserve them for explicit discrete-state questions.
- Do not use `Time series` for one-off instant values that should be scanned as KPIs.
- Do not hide label explosion with a cluttered panel; reduce the series count in the query instead.
