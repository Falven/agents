# API and Manifests

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/docs/api-guide.md

## Source Priority

For manifest fields, lifecycle semantics, DNS names, and service methods, prefer `docs/api-guide.md` over architecture or roadmap docs. Architecture text may describe intended direction that is not yet the current API.

## WorkerPool

`WorkerPool` is a Kubernetes custom resource that defines warm worker capacity for a class of actor workloads.

Important fields from the API guide:

- `spec.replicas`: number of workers to keep ready.
- `spec.ateomImage`: image used for the ateom runtime layer.

Use `kubectl` to create, inspect, and wait on `WorkerPool` resources:

```bash
kubectl apply -f <workerpool.yaml>
kubectl get workerpools -A
kubectl describe workerpool <name> -n <namespace>
```

## ActorTemplate

`ActorTemplate` is a Kubernetes custom resource that defines how actors of a given type are run and resumed.

Required or central fields from the API guide:

- `spec.containers`: workload containers to run for actors.
- `spec.workerPoolRef`: target `WorkerPool`.
- `spec.snapshotsConfig`: snapshot behavior used for suspend/resume.
- `spec.pauseImage`: pause image used by runtime plumbing.
- `spec.runsc`: runsc/gVisor runtime configuration.

Use `kubectl` for template resources:

```bash
kubectl apply -f <actortemplate.yaml>
kubectl get actortemplates -A
kubectl describe actortemplate <name> -n <namespace>
```

Actors created from an `ActorTemplate` should be managed with `kubectl ate`, not `kubectl`.

## Golden Snapshot and Resume Lifecycle

The API guide describes a golden snapshot path for fast actor startup. The template and snapshot configuration define how worker state is initialized, suspended, and resumed.

When planning a workload:

- Define a `WorkerPool` with enough warm capacity.
- Define an `ActorTemplate` that points to the pool and includes snapshot/runtime settings.
- Create actors through the Control API or `kubectl ate`.
- Resume actors before sending traffic.
- Suspend actors to persist state when they should leave active workers.
- Delete actors only when their lifecycle is complete.

## DNS Mesh

The current uniform actor DNS format is:

```text
<actor-id>.actors.resources.substrate.ate.dev
```

For local testing through a port-forwarded router, send the actor DNS value as the `Host` header:

```bash
kubectl port-forward -n ate-system svc/atenet-router 8000:80
curl -H "Host: <actor-id>.actors.resources.substrate.ate.dev" http://localhost:8000/
```

Some older demo text may show a different suffix. Prefer the current API guide suffix unless a checked-in manifest or environment-specific docs prove otherwise.

## Control API

The gRPC Control API includes actor lifecycle and discovery methods:

- `CreateActor`
- `ResumeActor`
- `SuspendActor`
- `DeleteActor`
- `GetActor`
- `ListActors`
- `ListWorkers`

Use these method names when discussing framework integration, API clients, or code changes. Preserve the lifecycle contract: create, resume, suspend, delete, get/list actors, and list workers.

Actor IDs should be DNS-1123-compatible because they are used in actor DNS names.

## Session Identity

The API guide describes `SessionIdentity` capabilities:

- `MintJWT`
- `MintCert`

Use these when a task involves identity propagation, per-session credentials, framework integration, or secure actor calls. For code changes, inspect the current proto/API definitions before editing because identity behavior is still evolving.

## Framework Integration Notes

Substrate is intended to support integration with agent frameworks such as ADK, LangChain, Claude Code, and Codex. For these tasks:

- Keep framework logic outside Substrate unless the repo already has a demo or integration point.
- Use the Control API for actor lifecycle.
- Use actor DNS for traffic routing.
- Use Session Identity when the framework needs per-session credentials.
- Verify with a real actor lifecycle command or demo request instead of only compiling code.

## Manifest Authoring Checklist

When authoring or reviewing manifests:

1. Confirm the namespace and names are DNS-safe.
2. Confirm the `WorkerPool` exists or is included.
3. Confirm `ActorTemplate.spec.workerPoolRef` points to the intended pool.
4. Confirm containers, images, ports, and runtime settings match the workload.
5. Confirm snapshot settings support the intended suspend/resume behavior.
6. Apply the manifests, wait for template readiness if supported, then create and resume an actor with `kubectl ate`.
