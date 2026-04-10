# Import and Export Workflows

Use this file when the user is moving a dashboard through the Grafana UI rather than only editing the dashboard content.

## Export Modes

- `Classic JSON` exports a classic dashboard object intended for direct inspection, hand-editing, classic import flows, and the legacy dashboard API's inner `dashboard` body.
- `V1 Resource` exports a resource-style body for resource-oriented workflows while still representing classic dashboard content.
- `V2 Resource` exports a resource-style body for schema v2 workflows.

## Import Routing

- If the target import expects classic dashboard JSON, provide the classic dashboard object shape.
- If the target import expects a resource body, provide the matching resource export shape rather than a classic object.
- Do not assume a resource export can be pasted into the legacy `dashboard` wrapper unchanged.

## Sharing and Deployment Concerns

- UI export modes may include sharing or deployment options that change how instance-specific data is represented.
- Datasource references may need remapping during import. Do not hard-code datasource assumptions without checking the target environment.
- Portability can break on hardcoded datasource UIDs in panels or on pinned variable datasource refs under `templating`.
- Check both panel-level and target-level datasource references before assuming a dashboard is portable as-is.
- A file that is good for ad hoc UI import is not automatically the best file for provisioning or API submission.

## Practical Rule

- For hand edits and classic dashboard workflows, start from `Classic JSON`.
- For resource-oriented workflows, keep the resource envelope intact and match V1 versus V2 to the target system.
- If the user says "import this into Grafana," ask or infer whether they mean classic dashboard import, resource import, provisioning, legacy API, or new API.
