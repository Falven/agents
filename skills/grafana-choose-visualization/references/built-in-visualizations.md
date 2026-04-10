# Built-In Visualizations

Use these groups as the first pass when narrowing the panel:

Official upstream dashboards in this repo are mostly `Time series`-first. Read legacy imported `graph` as `Time series` and legacy `singlestat` as `Stat`.

- Axis semantics:
  - `Time series` for real time on the x-axis
  - `Trend` for ordered numeric x-axis data that is not time
  - `XY chart` for arbitrary x/y pairs, scatter plots, and tabular relationships
- Single-value:
  - `Stat` for one current or aggregate value
  - `Gauge` for one value relative to bounds or thresholds
  - `Bar gauge` for one or several values relative to bounds, especially when ranking matters
- Category comparison:
  - `Bar chart` for categorical comparisons and top N groups
  - `Pie chart` only for small share-of-whole slices
  - `Table` for label-heavy inspection or drill-down output
- Distribution:
  - `Histogram` for numeric values rebucketed into a distribution
  - `Heatmap` for bucketed density over time
- Discrete state:
  - `State timeline` for state changes with merged runs
  - `Status history` for per-interval status without merging consecutive equal values
- Specialized: `Candlestick`, `Geomap`, `Node graph`, `Logs`, `Traces`, `Flame graph`
- Utility widgets: `Text`, `Dashboard list`, `Alert list`, `Annotations list`, `News`

Prefer the simplest panel that answers the question clearly.
