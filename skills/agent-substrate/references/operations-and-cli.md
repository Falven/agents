# Operations and CLI

Curated from:

- https://github.com/agent-substrate/substrate/blob/main/README.md
- https://github.com/agent-substrate/substrate/blob/main/cmd/kubectl-ate/README.md
- https://github.com/agent-substrate/substrate/blob/main/tools/setup-gcp
- setup and teardown entrypoints under `hack/`

## Operational Rule

Actors and workers are not Kubernetes CRDs. Use `kubectl ate` for actor and worker records because they live in Substrate control-plane storage. Use plain `kubectl` for Kubernetes resources such as namespaces, services, pods, `WorkerPool`, and `ActorTemplate`.

## Local kind Setup

From the repository root:

```bash
./hack/create-kind-cluster.sh
./hack/install-ate-kind.sh --deploy-ate-system
./hack/install-ate-kind.sh --deploy-demo-counter
go install ./cmd/kubectl-ate
```

Create and test a counter actor:

```bash
kubectl ate create actor my-counter-1 --template ate-demo-counter/counter
kubectl ate resume actor my-counter-1
kubectl port-forward -n ate-system svc/atenet-router 8000:80
curl -H "Host: my-counter-1.actors.resources.substrate.ate.dev" http://localhost:8000/
kubectl ate get actor my-counter-1
```

Tear down local kind resources:

```bash
./hack/delete-kind-cluster.sh
```

## GKE Setup

The root quickstart expects a GCP project, Application Default Credentials, and repository environment variables.

Typical sequence:

```bash
cp .ate-dev-env.sh.example .ate-dev-env.sh
source .ate-dev-env.sh
gcloud auth application-default login --project="${PROJECT_ID}"
go run ./tools/setup-gcp --all
./hack/install-ate.sh --deploy-ate-system
./hack/install-ate.sh --deploy-demo-counter
```

Tear down cloud resources with care:

```bash
./hack/teardown.sh --all
```

Use the setup and teardown scripts as entrypoints instead of reconstructing GCP resource creation manually.

## CLI Installation and Connection

Install the CLI:

```bash
go install ./cmd/kubectl-ate
```

For development, run it without installing:

```bash
go run ./cmd/kubectl-ate <command>
```

The CLI normally discovers the API server through the current kubeconfig and can port-forward to `ate-api-server`. Use `--endpoint` when connecting to an explicit API endpoint.

Global flags:

- `--kubeconfig`: path to kubeconfig.
- `--endpoint`: explicit Control API endpoint.
- `--output` or `-o`: output format where supported.
- `--trace`: enable tracing for supported CLI calls.

## Actor and Worker Inspection

List actors:

```bash
kubectl ate get actors
```

Inspect one actor:

```bash
kubectl ate get actor <actor-id>
kubectl ate get actor <actor-id> -o yaml
```

List workers:

```bash
kubectl ate get workers
```

Use plain `kubectl` for CRDs:

```bash
kubectl get workerpools -A
kubectl get actortemplates -A
kubectl describe actortemplate <name> -n <namespace>
```

## Actor Lifecycle

Create an actor:

```bash
kubectl ate create actor my-actor --template=ate-demo-counter/counter-template
```

Resume an actor:

```bash
kubectl ate resume actor my-actor
```

Suspend an actor:

```bash
kubectl ate suspend actor my-actor
```

Delete an actor:

```bash
kubectl ate delete actor my-actor
```

The API guide says `DeleteActor` applies to suspended actors. If deletion fails, suspend first and then retry deletion.

## Logs

Current CLI docs use a resource-type subcommand for actor logs:

```bash
kubectl ate logs actors my-actor
```

Actor logs are streamable while the actor is running. If an actor is not in a running status, resume it or inspect historical logs through the configured log backend if one exists.

## Admin Commands

The CLI docs include admin-oriented commands:

```bash
kubectl ate make-ca-pool
kubectl ate make-jwt-pool
kubectl ate debug-flush-redis
```

Use these only when the task explicitly involves control-plane certificates, JWT pools, or clearing Redis/ValKey-backed state in a development environment. Warn before suggesting destructive state reset commands such as `debug-flush-redis`.

## Setup and Teardown Entry Points

Use these documented script entrypoints when relevant:

- `./hack/create-kind-cluster.sh`: create local kind cluster.
- `./hack/delete-kind-cluster.sh`: delete local kind cluster.
- `./hack/install-ate-kind.sh --deploy-ate-system`: install Substrate on kind.
- `./hack/install-ate-kind.sh --deploy-demo-counter`: install the counter demo on kind.
- `./hack/install-ate.sh --deploy-ate-system`: install Substrate for the configured non-kind environment.
- `./hack/install-ate.sh --deploy-demo-<name>`: install demo resources where supported.
- `./hack/install-ate.sh --delete-demo-<name>`: remove demo resources where supported.
- `./hack/teardown.sh --all`: tear down configured GCP/cloud resources.

## Verification Patterns

- Cluster install: `kubectl get pods -n ate-system`.
- Template readiness: `kubectl wait --for=condition=Ready actortemplate/<name> -n <namespace> --timeout=5m`.
- Actor lifecycle: create, resume, `kubectl ate get actor <id>`, suspend, delete.
- Routing: port-forward `atenet-router`, send a request with the actor `Host` header.
- CLI connection: run a read-only command such as `kubectl ate get actors`.
