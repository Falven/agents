# Standard Options

Use standard options first. They solve most display problems without changing the query and without reaching for overrides too early.

## What This Section Owns

- `Unit`
- `Min`
- `Max`
- `Field min/max`
- `Decimals`
- `Display name`
- `Color scheme`
- `No value`

These are field and display controls, not true panel options.

## Unit

Set the unit before touching thresholds, legends, or tooltip wording.

- Use Grafana's built-in unit when it exists.
- Use `Misc > String` when Grafana should stop numeric formatting entirely.
- Use a custom unit when the built-in catalog is close but not exact.
- Official dashboards usually prefer the most specific built-in or custom unit that matches the metric semantics. Avoid generic units like `short` or `none` when the meaning is already known.

Useful custom-unit patterns:

- `suffix:req/s`
- `prefix:$`
- `currency:USD`
- `count:req`
- `si:mF`
- `time:YYYY-MM-DD`
- freeform custom text such as `widgets`

If the unit is wrong, every downstream choice reads wrong.

## Min, Max, and Field Min/Max

- `Min` and `Max` set the comparison range explicitly.
- `Field min/max` tells Grafana to calculate min and max per field instead of across the full panel.

Use explicit `Min` and `Max` when cross-series comparability matters.
Use `Field min/max` when each field should scale to its own range.
Do not mix them casually, because they answer different comparison questions.

## Decimals and String

- `Decimals` controls numeric precision.
- `String` disables numeric formatting entirely, including decimal trimming.

Use fewer decimals when the panel is for scanning.
Use more decimals only when the extra precision changes an operator decision.

## Display Name

Use `Display name` to make field titles readable without changing the query.

Common expressions:

- `${__field.displayName}`
- `${__field.name}`
- `${__field.labels}`
- `${__field.labels.instance}`
- `${__field.labels.__values}`

If an expression renders to an empty string for a field, Grafana falls back to its default display naming.

## Color Scheme

Color scheme is still part of standard options, even when thresholds later drive the final color behavior.

Common choices:

- `Single color`
- `Shades of a color`
- `From thresholds (by value)`
- `Classic palette`
- `Classic palette (by series name)`
- `Multiple continuous colors (by value)`
- `Single continuous color (by value)`

The exact list and effect vary by visualization. Confirm visualization-specific support before making a precise claim.

## No Value

`No value` controls what Grafana shows for empty or null values. The default is `-`.

Use it when:

- `-` is too ambiguous
- an explicit placeholder such as `No data` or `N/A` is clearer
- you need missing values to read differently from zero

Source: https://grafana.com/docs/grafana/latest/panels-visualizations/configure-standard-options/
