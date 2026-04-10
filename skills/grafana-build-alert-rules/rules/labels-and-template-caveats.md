# Labels and Template Caveats

- Stable labels define alert identity. Do not put rapidly changing values in labels.
- Avoid duplicate label keys and collisions between query labels, custom labels, and reserved Grafana labels such as `alertname` or `grafana_folder`.
- Use annotations for human-readable context and labels for routing, grouping, and ownership.
- Prefer `$values` when templates need ref-specific values or labels.
- Treat `$value` as a flattened legacy string for simple output only.
