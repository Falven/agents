# Transformations and Field Config

If the raw query is right, inspect what happens after the query returns.

## Transformations

- Check transform order first. Early joins, reductions, filters, or organize steps can destroy the shape needed by later steps.
- Use transformation debug or disable controls where available. Turn transforms off one at a time until the data becomes correct again.
- Use Table view while debugging transforms. It exposes the frame shape more clearly than the rendered panel.

## Field and Display Config

- Separate source data from display config. Standard options and overrides can change meaning without changing the underlying query result.
- Check units, decimals, min/max, value calculations, display names, and field overrides before rewriting queries.
- If a Stat, Gauge, or Bar Gauge looks wrong, verify which reduction or calculation is being displayed, not just which series was queried.

## Root-Cause Split

- Wrong before transforms means the issue is still query, time, or variable context.
- Wrong after a specific transform means fix that transform or its order.
- Right after transforms but wrong on screen means field config or panel semantics is now the likely cause.
