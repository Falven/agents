# Contributor Guide

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/CONTRIBUTING.md
- https://github.com/agent-substrate/substrate/blob/main/docs/dev/code-layout.md
- https://github.com/agent-substrate/substrate/blob/main/docs/dev/best-practices/tracing.md
- https://github.com/agent-substrate/substrate/blob/main/docs/dev/valkey-direct-access.md
- https://github.com/agent-substrate/substrate/blob/main/hack/verify/README.md
- https://github.com/agent-substrate/substrate/blob/main/hack/update/README.md

## Contribution Expectations

The contributor docs expect standard Google open source contribution practices:

- Sign the Contributor License Agreement when required.
- Follow the Google Open Source Community Guidelines.
- Prefer small, focused pull requests.
- Discuss larger or new-direction contributions before investing heavily.
- Include appropriate tests for code changes.
- Run relevant verification before submitting.
- Keep copyright boilerplate consistent with repository tooling.

## Code Surface Routing

Use the repository layout docs to choose edit surfaces:

- `cmd/`: binaries and their command-specific wiring.
- `cmd/<binary>/internal/`: logic local to one binary.
- `internal/`: shared implementation packages not exported as public API.
- `pkg/`: public packages with stronger compatibility expectations; use sparingly.
- `docs/`: user, operator, and developer documentation.
- `hack/`: repository automation for install, verify, update, and development tasks.
- `manifests/`: Kubernetes manifests and deployment resources.
- `demos/`: demo workloads and demo-specific clients or UIs.
- `benchmarking/`: performance and load-test assets.
- `tools/`: developer or setup tools, including GCP setup.
- `bin/`: local generated binaries or build outputs.

Command ownership areas called out in docs include:

- `cmd/ateapi`: Control API server.
- `cmd/atelet`: worker-side lifecycle/runtime agent.
- `cmd/atecontroller`: Kubernetes controller integration.
- `cmd/atenet`: routing layer.
- `cmd/ateom-gvisor`: gVisor/ateom runtime path.
- `cmd/podcertcontroller`: pod certificate controller.
- `cmd/kubectl-ate`: CLI.
- `tools/setup-gcp`: GCP setup helper.
- `demos/`: demo implementations.

Before moving code into `pkg/`, verify that it is intended to become public API. Prefer `internal/` for shared repo implementation.

## Tracing Conventions

For tracing changes, follow `docs/dev/best-practices/tracing.md`:

- Initialize OpenTelemetry tracing in server processes.
- Use `OTEL_EXPORTER_OTLP_ENDPOINT` for exporter endpoint configuration.
- Add gRPC server instrumentation with `otelgrpc.NewServerHandler`.
- Wrap HTTP handlers with `otelhttp.NewHandler`.
- Provide client-side tracing options where a component makes outbound calls.
- Shut down tracer providers cleanly.
- Name spans so actor lifecycle, routing, and control-plane operations can be understood in Jaeger or Cloud Trace.

Likely edit surfaces:

- Control API behavior: `cmd/ateapi` and related internal packages.
- Worker lifecycle behavior: `cmd/atelet`.
- Router behavior: `cmd/atenet`.
- Runtime/sandbox behavior: `cmd/ateom-gvisor` or ateom-related packages.
- CLI trace flag behavior: `cmd/kubectl-ate`.

Verification can include a focused Go test plus a traced CLI operation:

```bash
kubectl ate get actor <actor-id> --trace
```

## Direct ValKey Access

Use direct ValKey access only for debugging. Prefer `kubectl ate` for normal actor and worker inspection.

Documented access command:

```bash
kubectl exec -n=ate-system -it valkey-cluster-0 -- valkey-cli -h valkey-cluster-service -c --tls --cacert /etc/valkey-ca/ca.crt --cert /run/servicedns.podcert.ate.dev/credential-bundle.pem --key /run/servicedns.podcert.ate.dev/credential-bundle.pem
```

Cautions:

- Treat direct state-store inspection as read-only unless explicitly doing a controlled development reset.
- Do not mutate actor or worker records manually.
- Capture exact keys or records inspected when reporting findings.
- If state looks inconsistent, compare `kubectl ate get actor <id>`, `kubectl ate get workers`, pod state, and relevant component logs before suggesting storage changes.

## Verify Workflow

The `hack/verify/README.md` describes the verify script family. Prefer targeted verification for the edited area, then broader checks when the change crosses subsystem boundaries.

Use the README to discover exact scripts in the current checkout:

```bash
ls hack/verify
```

Common pattern:

```bash
./hack/verify/<script-name>.sh
```

When unsure which verify script applies, inspect `hack/verify/README.md` and nearby script names instead of inventing a new command.

## Update Workflow

The `hack/update/README.md` describes generated update script entrypoints. These scripts typically pair with verify scripts.

Use the README to discover exact scripts in the current checkout:

```bash
ls hack/update
```

Common pattern:

```bash
./hack/update/<script-name>.sh
```

Use update scripts when generated files, boilerplate, manifests, or codegen outputs are expected to change. After running an update script, inspect the diff and run the corresponding verify script.

## Contributor Verification Patterns

- Docs-only change: run markdown or docs checks if the repo provides one; otherwise inspect links and formatting manually.
- CLI change: run targeted Go tests for `cmd/kubectl-ate`, then exercise a read-only command such as `kubectl ate get actors` if a cluster is available.
- API change: run targeted tests around API/proto/server packages and verify lifecycle commands if a cluster is available.
- Routing change: run targeted tests, deploy a demo actor, port-forward `atenet-router`, and send a request with the actor `Host` header.
- Tracing change: run targeted tests, invoke a CLI command with `--trace`, and inspect Jaeger or Cloud Trace.
- Manifest/demo change: apply or install the demo, wait for `ActorTemplate` readiness, create/resume an actor, send traffic, then clean up.
