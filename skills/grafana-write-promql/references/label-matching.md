# Label Matching

- Binary operations match series by labels. By default, Prometheus matches on the full label set shared by both sides.
- Unmatched series are dropped. If a ratio or join is missing lines, suspect label mismatch first.
- Use `on(...)` to match only the labels that should participate in the operation.
- Use `ignoring(...)` to ignore labels such as `status`, `method`, or `instance` when they should not participate in the match.
- Use `group_left` when the left-hand side has more series per match and you want to keep the left-side extra labels.
- Use `group_right` when the right-hand side has more series per match and you want to keep the right-side extra labels.
- Group only by labels the user actually needs to compare.
- If a legend is unreadable, reduce the grouping labels in the query before changing the panel.

Examples:

- Per-service error ratio: `sum by (service) (rate(http_requests_total{status=~"5.."}[$__rate_interval])) / on (service) sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Per-status share of service traffic: `sum by (service, status) (rate(http_requests_total[$__rate_interval])) / ignoring(status) group_left sum by (service) (rate(http_requests_total[$__rate_interval]))`
