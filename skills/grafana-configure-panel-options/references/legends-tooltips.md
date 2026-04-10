# Legends and Tooltips

Use legends and tooltips to improve scannability after units, naming, and color semantics are already correct.

## Upstream Bias

The official dashboards in this repo usually treat dense time-series panels the same way:

- `drawStyle = line`
- `stacking = none` unless the chart is meant to show composition
- `legend = table` when operators need a few useful calcs to compare series
- `tooltip = multi` when hover should compare multiple series at the same timestamp

Use `Mode = List` when names matter more than calculations. Use `Mode = Table` when the legend itself needs to carry the comparison.

## Legend Controls

Legend options are more concrete than "show a legend" or "hide a legend."

Primary controls:

- `Visibility`
- `Mode`
- `Placement`
- `Width`
- `Values`

Operational guidance:

- Use `Mode = List` when names matter more than side-by-side comparison.
- Use `Mode = Table` when operators need calculations such as last, min, max, mean, or total in the legend itself.
- Use `Placement` and `Width` to keep the panel readable instead of letting the legend crowd the plot.
- Keep `Values` limited to the calculations that support the panel's decision. Extra columns make comparison slower.

Support caveats:

- Not every visualization with a legend supports every legend control.
- Geomap and heatmap legends are especially limited.
- Sorting legend values in table mode is only supported on some visualizations.

## Tooltip Controls

Tooltip controls determine how much detail appears on hover and how aggressively it appears.

Primary controls:

- `Tooltip mode`
- `Values sort order`
- `Hide zeros`
- `Hover proximity`
- `Max width`
- `Max height`

Operational guidance:

- Use `Tooltip mode = Single` when hover should stay focused on one series.
- Use `Tooltip mode = All` when cross-series comparison at a timestamp matters.
- Use `Values sort order` when the operator should see the largest or smallest contributors first.
- Use `Hide zeros` with `All` mode to keep sparse panels readable.
- Use `Hover proximity` to reduce noisy hover behavior on dense charts.

Support caveats:

- Not all visualizations expose a configurable `Tooltip` section.
- Some visualizations have tooltips but no tooltip controls.
- Heatmap adds tooltip-specific options beyond the common controls.
- Geomap handles tooltip behavior differently under map controls.

Source: https://grafana.com/docs/grafana/latest/panels-visualizations/configure-legend/ and https://grafana.com/docs/grafana/latest/visualizations/panels-visualizations/configure-tooltips/
