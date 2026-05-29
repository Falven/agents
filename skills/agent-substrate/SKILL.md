---
name: agent-substrate
description: Work with agent-substrate/substrate as a user, operator, or contributor. Use when setting up or tearing down local kind or GKE Substrate environments, deploying demos, authoring WorkerPool or ActorTemplate manifests, managing actors with kubectl ate, debugging routing, logs, traces, snapshots, or state-store behavior, understanding architecture and roadmap docs, or modifying Substrate code/docs around ateapi, atelet, atenet, ateom, Control API, Session Identity, ValKey/Redis, and runtime contracts.
---

# Agent Substrate

Use this skill for work with `agent-substrate/substrate` as a user, operator, or contributor. Keep `SKILL.md` as the router; load the relevant reference before giving commands, manifests, debugging steps, or edit guidance.

## Workflow

1. Classify the request as operational, API/manifest, observability, demo, contributor, or conceptual.
2. Read the matching reference before proposing commands or edits.
3. Prefer current API, CLI, and demo docs over aspirational architecture or roadmap text when they disagree.
4. Preserve the actor lifecycle contract: create, resume, suspend, delete, get/list actors, and list workers.
5. Prefer `kubectl ate` for actor and worker state because actors and workers live in Substrate control-plane storage, not Kubernetes CRDs.
6. Return exact commands or edit surfaces, affected subsystem, assumptions, and a verification path.

## Task Routing

- Setup, teardown, GKE or kind, CLI usage, actor lifecycle, logs, and admin commands: read [operations-and-cli.md](references/operations-and-cli.md).
- `WorkerPool`, `ActorTemplate`, snapshots, DNS mesh, Control API, and Session Identity: read [api-and-manifests.md](references/api-and-manifests.md).
- Logs, metrics, tracing, Jaeger, Cloud Trace, and actor observability: read [observability.md](references/observability.md).
- Counter, Sandbox, Claude Code Multiplex, or Secret Agent demos: read [demos.md](references/demos.md).
- Repo layout, code edits, tracing conventions, ValKey direct access, contribution workflow, and verify/update scripts: read [contributor-guide.md](references/contributor-guide.md).
- Concepts, architecture, personas, roadmap, and early-stage caveats: read [overview-and-architecture.md](references/overview-and-architecture.md).

## Ground Rules

- Say when guidance is directional because it comes from architecture or roadmap docs.
- Do not treat actors or workers as Kubernetes CRDs. Use `kubectl ate get actors`, `kubectl ate get actor <id>`, and `kubectl ate get workers`.
- Use plain `kubectl` for Kubernetes resources such as `WorkerPool`, `ActorTemplate`, namespaces, services, port-forwards, and waits.
- For edits, name the likely subsystem first: `ateapi`, `atelet`, `atenet`, `ateom`, CLI, manifests, demos, docs, or tooling.
- For verification, choose the narrowest useful check: CLI command, `kubectl wait`, demo request, trace inspection, targeted Go test, or repo verify script.
