# Variable Syntax and Formatting

Prefer Grafana's current interpolation forms:

- Use `$var` when the variable stands alone in the string.
- Use `${var}` when the variable touches other text, such as `cpu_${env}`.
- Use `${var:option}` when the interpolation must be formatted explicitly.
- Treat `[[var]]` as legacy syntax. It still appears in older dashboards, but do not teach it as the default form.

Use the smallest formatter that matches the query or link shape:

- `raw`: inserts the value without Grafana's datasource-specific escaping. Use it only when the query already needs literal text.
- `regex`: turns a multi-value selection into a regex-safe alternation. Use this with Prometheus label matchers and `=~`.
- `queryparam`: expands the variable into URL query parameters for dashboard links.
- `csv`: useful when a target expects comma-separated values, but do not use it by default in Prometheus queries.
- `json`: useful when a target expects a JSON array or JSON string content, but keep it as a niche formatter.

Examples:

- Query label matcher: `job=~"${job:regex}"`
- Metric name suffix: `http_requests_total{env="${env}"}`
- Dashboard link: `/d/abc123/service?${service:queryparam}`
- Raw interpolation: `${label:raw}`

Keep syntax decisions explicit in the answer. If the query only works because of a formatter, name that formatter and why it is required.
