# Alerting Caveats

## Datasource and Evaluation Limits

- Grafana-managed rules require backend, alerting-enabled datasources. Frontend-only transforms, browser-evaluated queries, and unsupported plugins are not valid alert inputs.
- Advanced mode uses fixed relative time ranges per query. Choose them deliberately; too-short windows create `No Data`, and too-wide windows increase latency and timeout risk.
- Dashboard panels that rely on `instant` mode, mixed datasource wiring, or `__expr__` math should be rewritten as alert-ready source queries plus explicit alert expressions instead of copied wholesale.
- If a dashboard query only makes sense as a visual exploration aid, say so and do not force it into an alert.

## Operational States

- `No Data` means evaluation succeeded but returned no series, no rows, or all-null values.
- `Error` means evaluation failed, timed out, or exhausted retries.
- `MissingSeries` means a previously seen alert instance disappeared while the rule still returns other series. Grafana later resolves the stale instance and annotates it with `grafana_state_reason=MissingSeries`.
- Decide explicitly how `No Data` and `Error` should behave. `Keep Last State` reduces flapping, but it can also hide longer outages.
- If `No Data` or `Error` is configured to alert, Grafana can emit separate `DatasourceNoData` or `DatasourceError` alerts with their own labels and without waiting through the original rule's pending period.

## Recovery and Noise

- Recovery threshold and `Keep firing for` solve different problems. Recovery threshold adds hysteresis around the condition value; `Keep firing for` delays resolution after the condition clears.
- High-cardinality query output creates many alert instances. Remove dimensions responders do not page on before the condition step.
- Grafana-side expressions are harder to port than datasource-native PromQL. Prefer source-query logic when the query language already expresses the alert cleanly.
