# Recovery, No Data, and Missing Series

- Recovery threshold and `Keep firing for` are different controls.
- Use recovery threshold to add hysteresis around the firing threshold.
- Use `Keep firing for` to delay resolution after the condition clears.
- `No Data` means the evaluation returned no usable values. `Error` means the evaluation failed.
- `MissingSeries` means one alert instance disappeared while the rule still returns other instances; Grafana later resolves the stale instance and marks the reason.
- Decide `No Data` and `Error` handling explicitly instead of leaving the operational behavior implicit.
