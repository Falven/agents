# Variable Types

Pick the smallest Grafana variable type that matches the interaction:

- Query: values come from the datasource. Use this for environments, clusters, jobs, instances, and other live dimensions. Query variables can be chained by referencing another variable inside the query. When the variable drives a Prometheus label filter and should support multi-select or `All`, configure `includeAll: true` and `allValue: ".*"` so downstream queries can use `=~` matching.
- Custom: fixed lists such as `prod,staging,dev` or operator choices like `p50,p95,p99`.
- Text box: free-form input when the dashboard needs an operator-entered string such as a host prefix, tenant ID, or regex fragment.
- Constant: a fixed hidden value reused across queries, links, or repeated titles. Use it when the value should not be edited from the dashboard UI.
- Data source: lets the viewer switch between datasources of the same type. Use sparingly because it changes the whole query context.
- Interval: a selectable duration or step value used for grouping, rollups, or query windows.
- Ad hoc filters: datasource-driven key/value filters that Grafana injects automatically into matching queries. Do not interpolate ad hoc filters manually.
- Switch: a true/false style toggle when the dashboard needs a simple on/off control.

Two related concepts matter even when they are not dashboard-defined variable types:

- Chained variables: query variables whose options depend on another variable, such as `instance` depending on `job`. Use them to narrow large option sets, but keep the dependency graph shallow enough to debug.
- Hidden bridge variables: query variables hidden from the UI are common when a dashboard needs an internal selector for `cluster`, `instance`, or node-to-instance mapping. Keep them when they are part of the variable chain, but do not add them unless they actually unblock another selector or panel.
- Global variables: built-in Grafana values like time range and dashboard metadata. Use them when the need is already covered by Grafana, rather than creating a duplicate custom variable.

Default rules:

- Prefer query over custom when the option set comes from live data.
- Prefer custom over text box when the allowed values are known and small.
- Prefer constant over custom when the value should not be user-facing.
- Add a new variable only if it changes a real dashboard decision; do not template every label.
- Many imported dashboards still use `label_values(...)` for Prometheus query variables. Keep that pattern when preserving upstream behavior, but do not treat it as the only modern option.
