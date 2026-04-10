# Provisioning and HTTP API

Provisioning, the legacy dashboard API, and the new resource API are different workflows. Do not reuse one payload shape for another without checking.

## File Provisioning

Provisioning is a file-based workflow, not a dashboard API wrapper.

- Provisioned dashboards should usually be stored as clean, reusable dashboard files plus provisioning configuration.
- Provisioning ignores embedded dashboard `version` for update decisions. Do not rely on dashboard `version` to control rollout.
- Keep durable identity with `uid` when you want provisioning to continue managing the same dashboard.
- Treat classic `id` as generated and omit it from provisioned files unless a very specific workflow requires otherwise.
- Provisioning concerns such as folder placement, polling, and update behavior belong to the provisioning workflow, not to legacy API wrapper fields.

## Legacy Dashboard API

The legacy HTTP API uses the classic dashboard wrapper:

```json
{
  "dashboard": { "...classic dashboard JSON..." },
  "folderUid": "observability",
  "overwrite": true,
  "message": "update dashboard"
}
```

- This is the `/api/dashboards/db` workflow.
- The inner `dashboard` body is classic dashboard JSON.
- Dashboard `version` is the dashboard revision used for optimistic concurrency in this workflow.
- `uid` is the durable dashboard identity.
- `id` is database-generated and should not be treated as portable identity.

## New Resource API

The new API uses a Kubernetes-style resource body with separate metadata and spec sections.

- Expect top-level resource fields such as `apiVersion`, `kind`, `metadata`, and `spec`.
- Treat `metadata.resourceVersion` as the concurrency token for this API.
- Do not confuse `metadata.resourceVersion` with classic dashboard `version`.
- Treat API metadata fields as managed unless the endpoint requires them on update.
- Use the body shape expected by the target endpoint or export mode, not the legacy `dashboard` wrapper.

## Practical Rule

- If the target is provisioning, prepare files for provisioning and ignore legacy API wrapper habits.
- If the target is `/api/dashboards/db`, build the classic `dashboard` wrapper and keep dashboard `version` semantics in mind.
- If the target is the new API, build the resource body and keep `metadata.resourceVersion` semantics in mind.
