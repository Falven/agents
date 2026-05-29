# Overview and Architecture

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/README.md
- https://github.com/agent-substrate/substrate/blob/main/docs/architecture.md
- https://github.com/agent-substrate/substrate/blob/main/docs/roadmap.md

## Project Stance

Substrate is a Kubernetes-based system for running agent-like workloads with fewer always-on workers than logical actors. It focuses on runtime and control-plane concerns: keeping a warm worker pool, assigning actors to workers on demand, routing traffic, suspending and resuming actor state, and exposing lifecycle APIs.

Substrate is intentionally not an agent SDK. It is meant to sit below frameworks such as ADK, LangChain, Claude Code, or Codex and provide runtime primitives they can integrate with.

The repository is in early development. APIs, manifests, storage contracts, and operational flows may change. Prefer current README, API guide, CLI docs, and demo READMEs over roadmap or architecture text when they disagree.

## Mental Model

- Actor: the logical, addressable unit of work. Actors can be created, resumed, suspended, deleted, listed, and inspected through Substrate's control plane.
- Worker: the running compute slot that can host an actor. Workers are managed as warm capacity and are fewer than the total number of actors.
- WorkerPool: the Kubernetes custom resource that defines warm worker capacity and runtime configuration.
- ActorTemplate: the Kubernetes custom resource that defines how a class of actors should be launched and resumed.
- Control plane: the API and controllers that track actors, workers, snapshots, assignment, and lifecycle state.
- Routing layer: the network path that maps actor DNS names to the currently assigned worker.
- State store: the control-plane backing store. Current docs refer to ValKey/Redis-backed storage for actor and worker records.

Actors and workers are not Kubernetes CRDs. `WorkerPool` and `ActorTemplate` are Kubernetes resources; actor and worker records live in Substrate control-plane storage and should be inspected through `kubectl ate`.

## Lifecycle

The lifecycle contract to preserve in answers and code guidance is:

1. Create an actor from an `ActorTemplate`.
2. Resume the actor onto an available worker.
3. Route traffic to the actor while it is running.
4. Suspend the actor and preserve state through the configured snapshot path.
5. Resume the actor later from its snapshot.
6. Delete the actor when it is no longer needed.

Current API docs also expose get/list operations for actors and list operations for workers.

## Architecture Themes

- Warm capacity: `WorkerPool` keeps ready workers available so activation does not always require creating new pods.
- Suspend/resume: the system is optimized around moving logical actors in and out of active workers while preserving state.
- Focused control plane: Substrate centralizes lifecycle decisions instead of spreading actor state across ad hoc app code.
- Uniform routing: actor traffic should be addressable through predictable actor DNS names.
- State-first operation: control-plane state, snapshot metadata, and worker assignment are core runtime data.
- Runtime modularity: docs discuss multiple runtime and sandboxing options, including ateom and gVisor-related paths.

## Personas

The docs describe several audiences:

- User: runs demos, creates actors, sends traffic, and observes lifecycle behavior.
- Operator: sets up local kind or GKE environments, deploys Substrate, manages capacity, watches logs, and debugs routing or tracing.
- Framework integrator: adapts agent frameworks to Substrate's Control API, identity, lifecycle, and routing model.
- Contributor: changes code in ateapi, atelet, atenet, ateom, controllers, demos, docs, or tooling.

## North-Star Metrics

Architecture docs describe aspirational scale and performance targets, including low-latency actor activation, very large actor counts, and high wakeup rates. Treat these as directional goals, not guaranteed current behavior.

When asked about performance, distinguish:

- Documented target or roadmap priority.
- Current operational path that can be tested in the repo.
- Measurement the user should run in their environment.

## Roadmap Priorities

Roadmap themes include:

- Actor versioning and lifecycle reliability.
- Worker autoscaling and warm capacity management.
- Control-plane authorization and CLI polish.
- Standard DNS mesh behavior.
- Storage model decisions and state-store reliability.
- Security, identity, and policy.
- Observability, performance, tests, integrations, and operability.

Use the roadmap to explain where the project is going, but do not use it as a source of exact commands or manifest fields unless current operational docs confirm them.
