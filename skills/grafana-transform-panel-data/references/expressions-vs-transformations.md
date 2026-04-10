# Expressions vs Transformations

Use the lightest layer that expresses the job clearly. Official Grafana dashboards bias query-first and only reshape in Grafana when the post-query frame is still wrong.

| Layer | Best fit | Caveats |
| --- | --- | --- |
| Query | Source-owned filtering, grouping, joins, and business semantics | Prefer this whenever the datasource can express the logic clearly |
| Panel transform | Panel-local shaping, joining, grouping, reduction, and field cleanup after the query runs | Do not move core query semantics here just because Grafana can do it; most official uses are inspection-table cleanup or a narrow derived overview metric |
| Classic server-side expression | Backend-only Grafana expression layer for derived results across backend query outputs when `math`, `reduce`, or `resample` is enough | Limited surface area; not a replacement for rich table shaping or general query logic |
| SQL expression | Grafana's separate SQL expression layer for SQL-style operations across query results when available | Has its own constraints and supported shapes; it is not the datasource query and not the panel transform pipeline |

Decision rules:

- Use the query when the datasource can state the logic plainly.
- Use panel transforms when the data is already correct and only the panel frame shape is wrong.
- Use classic server-side expressions when you need backend-computed math, reduction, or resampling across backend query outputs.
- Use SQL expressions when you need Grafana-side SQL-style operations and that layer fits better than panel transforms.
- Use `Add field from calculation`/`calculateField` only for narrow derived values like utilization-style overview panels, not as the default way to add computed fields.
- If none of those is clearly better, return `no transform` or recommend the simpler upstream layer instead of forcing a transformation chain.
