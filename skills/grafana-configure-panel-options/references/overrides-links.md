# Overrides and Data Links

Use overrides when a few fields need exceptions. Use data links when the next operator action is to investigate somewhere else.

## Override Matchers

Grafana supports five override matchers:

- `Fields with name`
- `Fields with name matching regex`
- `Fields with type`
- `Fields returned by query`
- `Fields with values`

Apply the narrowest matcher that captures the real exception.

Important caveat: the regex matcher selects fields, but it does not rename them. If the real need is renaming, use the `Rename by regex` transformation instead.

## Override Usage

Typical override use cases:

- a different unit for one field
- a distinct color for one series
- axis placement for one metric
- hiding a field from legend or tooltip
- field-specific decimals, min and max, or mappings

Do not use overrides for broad cleanup that the query, transformation, or standard options should handle once.

## Data Links

Data links belong to display configuration, not true panel options.

Common link behavior:

- Link to another dashboard
- Link to Explore or logs
- Link to an external runbook or incident tool
- Pass field, series, label, or time-range context through variables in the URL

Concrete controls to name when recommending a link:

- `Title`
- `URL`
- variable insertion in the URL
- `Open in a new tab`
- `One click`

Important caveats:

- Only one data link can have `One click` enabled at a time.
- `One click` is only supported for some visualizations.
- If multiple links exist and `One click` is not used, Grafana shows a link menu instead.

Source: https://grafana.com/docs/grafana/latest/panels-visualizations/configure-overrides/ and https://grafana.com/docs/grafana/latest/panels-visualizations/configure-data-links/
