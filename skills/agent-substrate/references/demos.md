# Demos

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/demos/counter/README.md
- https://github.com/agent-substrate/substrate/blob/main/demos/sandbox/README.md
- https://github.com/agent-substrate/substrate/blob/main/demos/claude-code-multiplex/README.md
- https://github.com/agent-substrate/substrate/blob/main/demos/agent-secret/README.md

## General Demo Rules

- Install the Substrate system before installing demos.
- Use `kubectl` for namespaces, services, pods, `WorkerPool`, and `ActorTemplate`.
- Use `kubectl ate` for actor create, resume, suspend, delete, get/list, and logs.
- Port-forward `atenet-router` when testing HTTP routing locally.
- Prefer the current DNS suffix `<actor-id>.actors.resources.substrate.ate.dev`; call out older demo docs that use another suffix.

## Counter Demo

What it proves:

- Basic actor lifecycle.
- Actor routing through `atenet-router`.
- Stateful counter behavior across requests and lifecycle operations.

Install:

```bash
./hack/install-ate.sh --deploy-demo-counter
```

Wait for template readiness:

```bash
kubectl wait --for=condition=Ready actortemplate/counter -n ate-demo-counter --timeout=5m
```

Create and run an actor:

```bash
kubectl ate create actor my-counter-1 --template ate-demo-counter/counter
kubectl ate resume actor my-counter-1
```

Test traffic:

```bash
kubectl port-forward -n ate-system svc/atenet-router 8000:80
curl -H "Host: my-counter-1.actors.resources.substrate.ate.dev" http://localhost:8000/
```

Inspect and clean up:

```bash
kubectl ate get actor my-counter-1
kubectl ate suspend actor my-counter-1
kubectl ate delete actor my-counter-1
./hack/install-ate.sh --delete-demo-counter
```

## Sandbox Demo

What it proves:

- Running command-like workloads inside Substrate actors.
- Client interaction with the Control API and router.
- Sandbox-style execution boundaries.

Security note: the demo README warns that it can run arbitrary commands and is not an authenticated production service. Treat it as a local or controlled-environment demo.

Install:

```bash
./hack/install-ate.sh --deploy-demo-sandbox
```

Wait for template readiness:

```bash
kubectl wait --for=condition=Ready actortemplate/sandbox-template -n ate-demo-sandbox --timeout=5m
```

Create and run an actor:

```bash
kubectl ate create actor my-sandbox-1 --template ate-demo-sandbox/sandbox-template
kubectl ate resume actor my-sandbox-1
```

Port-forward services:

```bash
kubectl port-forward -n ate-system svc/api 8080:443
kubectl port-forward -n ate-system svc/atenet-router 8000:80
```

Build and run the client:

```bash
go build -o bin/sandbox-client ./demos/sandbox/client
./bin/sandbox-client --ateapi=localhost:8080 --atenet=localhost:8000 --id=my-sandbox-1
```

Clean up:

```bash
kubectl ate suspend actor my-sandbox-1
kubectl ate delete actor my-sandbox-1
./hack/install-ate.sh --delete-demo-sandbox
```

## Claude Code Multiplex Demo

What it proves:

- Multiple Claude Code actors sharing fewer worker pods.
- Actor multiplexing against a small worker pool.
- A UI-driven workflow that uses the Control API.

Important caveat: the README marks the demo as draft and references open blockers. Verify the current README and issues before treating it as a polished path.

Common requirements:

- Anthropic API key.
- GCS bucket for demo state.
- `KO_DOCKER_REPO`.
- Docker buildx.
- Substrate system installed.

Install:

```bash
ANTHROPIC_API_KEY=<key> BUCKET_NAME=<bucket> ./hack/install-ate.sh --deploy-demo-claude-code-multiplex
```

Known demo namespace and templates:

- Namespace: `claude-multiplex-demo`.
- ActorTemplates: `luna`, `mars`, `orion`.

Port-forward the API service:

```bash
kubectl port-forward svc/ateapi 8080:8080 -n ate-system
```

Run the UI:

```bash
cd demos/claude-code-multiplex/ui
PORT=8090 ATEAPI_ADDR=localhost:8080 go run .
```

Useful UI environment variables:

- `PORT`
- `ATEAPI_ADDR`
- `DEMO_NAMESPACE`

Clean up:

```bash
./hack/install-ate.sh --delete-demo-claude-code-multiplex
```

## Secret Agent Demo

What it proves:

- Self-suspending actors.
- Preserving a secret in actor memory/state across suspend and resume.
- Multiplexing actor sessions over workers.

Install:

```bash
./hack/install-ate.sh --deploy-demo-agent-secret
```

Scale worker capacity if needed:

```bash
kubectl patch workerpool agent-secret -n ate-demo-secret-agent-v2 --type='merge' -p '{"spec":{"replicas":8}}'
```

Create and run an actor:

```bash
kubectl ate create actor my-agent --template ate-demo-secret-agent-v2/agent-secret
kubectl ate resume actor my-agent
```

Test traffic through the router:

```bash
kubectl port-forward -n ate-system svc/atenet-router 8000:80
curl -H "Host: my-agent.actors.resources.substrate.ate.dev" http://localhost:8000/
```

The demo README may show the older host suffix `actors.resources.substrate.k8s.io`. Prefer the current API-guide suffix unless the deployed demo manifests require the older value.

Watch actor records:

```bash
kubectl ate get actors
kubectl ate get actor my-agent
```

Clean up:

```bash
kubectl ate suspend actor my-agent
kubectl ate delete actor my-agent
```

If many session actors were created, list actors first and delete only the demo actors that belong to this run.
