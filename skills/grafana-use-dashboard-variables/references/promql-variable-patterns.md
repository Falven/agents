# PromQL Variable Patterns

Use variables in Prometheus queries only where they map to a real label or time-window decision.

Variable queries:

- Prefer the Prometheus query variable mode that uses `query_result(...)` when the option list depends on the current time range or on computed query output.
- Use `Refresh = On time range change` for time-aware `query_result(...)` variables so the option list tracks the active dashboard range.
- Treat classic query syntax as legacy. It still exists, but it is the weaker default for new work.
- Many imported Grafana dashboards still use `label_values(...)` to populate Prometheus variables. Keep that shape when mirroring upstream behavior, but prefer `query_result(...)` when the list really needs time-aware or computed values.

PromQL interpolation rules:

- Use `=` only for single concrete values.
- Use `=~` when the variable supports multi-value selection or `All`.
- With Prometheus, regex matches are anchored. Write the regex to match the full label value you want, not a loose substring.
- Pair `=~` with `${var:regex}` when multiple selected values must become a safe alternation.

Examples:

- Single value: `up{job="$job"}`
- Multi-value or `All`: `up{job=~"${job:regex}"}`
- Chained variable query: `label_values(up{job=~"${job:regex}"}, instance)`
- Time-aware computed list:
  `query_result(topk(10, sum by (instance) (rate(http_requests_total[$__range]))))`

Range and rate guidance:

- Use `$__rate_interval` inside `rate()` and `increase()` unless there is a deliberate reason to hardcode the window.
- Keep interval variables such as `resolution` for panel step, sampling, aggregation windows, or grouping choices, not as a replacement for `$__rate_interval`.

Guardrails:

- Keep variable-driven label filters aligned with labels the metric actually exposes.
- Avoid variableizing every label. It makes dashboards slower and harder to read.
- If the query only works because the interpolation is complicated, simplify the variable model first.
