# Performance Checks

Treat dashboard speed as part of correctness.

## Start With Inspect

- Use Inspect `Stats` and `Query` before guessing. Identify which panels are slow, large, or repeatedly issuing the same expensive query shape.
- Compare one slow panel against one cheap panel with similar intent before editing globally.

## Reduce Cost At The Source

- Reduce time range first when debugging. If the panel becomes healthy, the issue is often point volume, not logic.
- Reduce returned series and points before tweaking refresh or panel cosmetics.
- Check whether repeated panels or repeated variables multiply the same expensive query across the dashboard.

## Remove Duplicate Work

- Look for panels that re-run the same query just to present it differently.
- When multiple panels need the same result, reuse it through the `Dashboard` datasource instead of duplicating backend cost.
- Duplicate-panel cost is still real cost even when each single panel looks acceptable in isolation.
