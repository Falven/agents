# Observability

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/docs/observability.md
- https://github.com/agent-substrate/substrate/blob/main/cmd/kubectl-ate/README.md
- https://github.com/agent-substrate/substrate/blob/main/docs/dev/best-practices/tracing.md

## Actor Metadata Labels

Substrate attaches actor-aware metadata to runtime logs and telemetry where supported:

- `ate.dev/actor_id`
- `ate.dev/actor_template`
- `ate.dev/actor_namespace`

Use these labels when filtering logs, building dashboards, or correlating actor behavior across components.

## Logs

Current CLI docs use:

```bash
kubectl ate logs actors <actor-id>
```

Actor logs are directly streamable while the actor is running. For non-running actors, historical logs require a centralized logging backend. If no log backend is configured, inspect current actor state and reproduce after resuming the actor.

The observability docs may show older shorthand syntax:

```bash
kubectl ate logs <actor-id> --follow
```

Prefer the current CLI README syntax with the `actors` resource type unless the installed CLI help says otherwise.

## Metrics Status

The observability docs describe foundational OpenTelemetry system and server metrics. Actor-level metrics and higher-level dashboards are described as evolving work. When asked for metrics:

- Start by confirming which metrics backend is installed.
- Use Kubernetes and OTel collector status to verify the pipeline.
- Avoid promising actor-specific metrics unless current manifests or code expose them.
- Recommend adding actor labels to metric attributes when implementing new instrumentation.

## Local Jaeger Tracing

For local tracing, port-forward Jaeger:

```bash
kubectl port-forward -n otel-system svc/jaeger 16686:16686
```

Open Jaeger at:

```text
http://localhost:16686
```

Generate a traced operation through the CLI:

```bash
kubectl ate get actor <actor-id> --trace
kubectl ate suspend actor <actor-id> --trace
```

If traces are missing, verify the OTel collector pods, Jaeger service, CLI `--trace` flag, and the service name emitted by the component under test.

## Cloud Trace and Managed OpenTelemetry

The CLI docs mention Cloud Trace and Managed OpenTelemetry setup. For GKE or GCP environments:

1. Confirm the Cloud Trace API is enabled for the project.
2. Confirm Workload Identity or credentials allow trace export.
3. Confirm the Managed OpenTelemetry collector is installed and healthy.
4. Run a CLI command with `--trace`.
5. Search Cloud Trace for the service/span names involved.

When implementing tracing, the dev docs use `OTEL_EXPORTER_OTLP_ENDPOINT` as the endpoint configuration hook.

## Tracing Implementation Notes

For contributor work, use the tracing conventions in `docs/dev/best-practices/tracing.md`:

- Initialize OTel tracing in servers.
- Add gRPC server stats handling with `otelgrpc.NewServerHandler`.
- Wrap HTTP handlers with `otelhttp.NewHandler`.
- Provide tracing options for clients.
- Shut down tracer providers cleanly.
- Keep span names stable and useful for actor lifecycle debugging.

Likely edit surfaces:

- `cmd/ateapi` and related packages for Control API tracing.
- `cmd/atelet` for worker and actor lifecycle traces.
- `cmd/atenet` for routing traces.
- CLI code for `--trace` behavior.

## Debugging Checklist

For a missing or confusing trace:

1. Re-run the operation with `--trace` if it is a CLI call.
2. Confirm the actor exists with `kubectl ate get actor <actor-id>`.
3. Confirm relevant pods are running with `kubectl get pods -A`.
4. Confirm the OTel collector or Jaeger service is reachable.
5. Check actor-aware labels and service names.
6. If editing code, verify instrumentation at server and client boundaries.
