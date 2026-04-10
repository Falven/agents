# Range vs Instant

- `Type=Range` evaluates across the selected time range. Use it for trend lines, heatmaps, and anything that should show change over time.
- `Type=Instant` evaluates once at the panel end time. Use it for stat, gauge, or current-value table panels.
- `Type=Both` is useful when Grafana needs both the trend and the current sample. If the panel only needs one shape, pick one.
- Use `rate()` or `increase()` on counters; do not chart raw counters directly unless the point is monotonic growth.
- Prefer `$__rate_interval` over a hard-coded `[5m]` for Grafana dashboard queries.
- Grafana's panel sampling interval can be separate from the PromQL lookback window. Official dashboards often set `interval` from a resolution variable while keeping counter windows on `$__rate_interval`.

Examples:

- Request trend by service: `Type=Range`, `sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Current request rate by service: `Type=Instant`, `sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Requests during the current lookback window: `Type=Instant`, `sum by (service) (increase(http_requests_total[$__rate_interval]))`
