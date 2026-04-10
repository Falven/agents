# Time Range and Refresh

- Grafana's documented dashboard defaults are `from=now-6h`, `to=now`, timezone `browser`, and no auto-refresh unless someone sets it.
- Choose defaults per dashboard family, not per arbitrary template. The upstream set mixes `now-30m`, `now-1h`, `now-3h`, `now-6h`, `now-24h`, and refresh cadences from none to `1m`.
- Choose a default time range that matches the signal speed and operating cadence. Fast-moving service views often need shorter windows than capacity, cost, or planning views.
- Keep no auto-refresh as the default unless the dashboard is used for active monitoring. Diagnostics and post-incident dashboards usually do not need automatic refresh.
- When refresh is needed, pick the slowest valid refresh interval that still answers the question in time. Do not choose an aggressive cadence just because the datasource can tolerate it.
- Use `Now delay` when ingestion lag or metric backfill makes the freshest edge misleading. State the delay explicitly instead of letting users infer why the right edge looks stale.
- Use `hideTimepicker` only when the dashboard should enforce a fixed operational window. Otherwise leave the time picker visible so operators can widen or narrow scope during diagnosis.
- Call out when one dashboard mixes panels that want very different time horizons. If the mismatch is structural, split the dashboard instead of forcing one default to fit all panels badly.
