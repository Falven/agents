# Time Range and Resolution

Many empty, noisy, or contradictory panels are really time and resolution bugs.

## Check In This Order

- Dashboard time range: start from the dashboard's shipped window, then confirm it matches the user report. Official dashboards intentionally vary their defaults across families.
- Timezone: verify browser time versus dashboard time zone before trusting timestamps.
- `Now delay`: check whether the dashboard intentionally shifts "now" back to avoid ingest lag.
- Auto-refresh: disable or slow it while debugging so the target does not move between inspections.
- Treat the shipped refresh cadence as part of the baseline too. A blank or slow refresh on an official dashboard can be intentional.

## Query Resolution

- Check `Max data points`, `Min interval`, and the computed `Interval` before blaming the datasource.
- Too much downsampling hides spikes. Too little downsampling creates noise, gaps, or slow queries.
- Confirm instant versus range behavior matches the panel type and the question being asked.

## Panel Overrides

- Check panel `Relative time` and `Time shift` before editing the query.
- Treat absolute dashboard ranges as a special case. Panel relative-time overrides are easy to misread there, so verify behavior in Explore instead of assuming the override applied.

## Prometheus-Specific Checks

- Compare the effective step with the scrape interval. If step is too small or too large for the scrape cadence, results will look sparse, smeared, or empty.
- If Grafana is forced to a coarse step by datasource or panel limits, short spikes can disappear.
- If the query range is shorter than the scrape or rate window assumptions, counters and rates can look broken even when the query is valid.
