# Thresholds and Value Mappings

Thresholds and value mappings solve different problems. Treat them as separate tools.

## Use Thresholds For State and Severity

Thresholds conditionally style a value or series based on where it lands.

Default Grafana threshold behavior:

- `Base = green`
- `80 = red`
- `Mode = Absolute`
- `Show thresholds = Off` for some visualizations

Key controls:

- `Threshold value`
- `Thresholds mode`
- `Show thresholds`

`Thresholds mode` choices:

- `Absolute` uses concrete values such as `80`.
- `Percentage` uses the field's range.

`Show thresholds` support is visualization-specific. Where it exists, it can usually be:

- `Off`
- `As lines`
- `As filled regions`
- both lines and regions for some visualizations

Use thresholds to show operator meaning, not decoration. If the unit or scale is wrong, thresholds will only make the mistake look more confident.

## Gauge and Stat Bias

Official dashboards use thresholds heavily for bounded metrics, especially gauges.

- Use gauges when the metric has a meaningful floor and ceiling.
- Set explicit `Min` and `Max` so threshold bands read against the right range.
- Keep threshold markers on and threshold labels off unless the text itself adds value.
- For current-state stat tiles, reduce with `lastNotNull` before thresholds and color are applied.

## Use Value Mappings For Text Replacement

Value mappings change what Grafana displays for matching values.

Supported mapping types:

- `Value`
- `Range`
- `Regex`
- `Special`

Use them when the raw value is technically correct but not operator-friendly, such as turning:

- `0` into `Down`
- `1` into `Up`
- a numeric band into `Cold` or `Hot`
- special values like `Null` into `No sample`

Important rule: value mappings bypass standard formatting such as unit and decimal display. If a field has a mapping, Grafana shows the mapped text instead of the usual formatted number.

## Choosing Between Them

- Use thresholds when the number should stay visible and its state should be color-encoded.
- Use value mappings when the displayed text should replace the raw value.
- Use both only when the visualization supports it cleanly and the combined result is still easy to read.

Source: https://grafana.com/docs/grafana/latest/panels-visualizations/configure-thresholds/ and https://grafana.com/docs/grafana/latest/panels-visualizations/configure-value-mappings/
