# agents

Repository for installable agent skills and future agent-related artifacts.

### Install All Skills Globally

With Node.js and npm installed, run this command from the repo:

```bash
npm run install:skills
```

This installs all skills from the local checkout at user scope for every agent supported by the `skills` CLI. No separate `npm install` is needed.

### Operator Install With `skills`

Install `prompt-guidance` globally from the remote repo to all agents supported by the `skills` CLI:

```bash
skills add Falven/agents -g --agent '*' --skill prompt-guidance -y
```

You can also install from the direct GitHub skill URL:

```bash
skills add Falven/agents -g --agent '*' --skill '*' -y
```

Install the same skill from a local checkout when you want local changes to drive the installed copy:

```bash
skills add /path/to/agents -g --agent '*' --skill prompt-guidance -y
```

- `-g` installs at user scope so the skill is available across projects.
- `--agent '*'` targets every agent integration supported by the local `skills` CLI.
- `skills ls -g` lists globally installed skills.

To remove:

```bash
skills remove -g crawlee-python-docs grafana-build-alert-rules grafana-choose-visualization grafana-compose-dashboards grafana-configure-panel-options grafana-debug-dashboards grafana-debug-promql grafana-manage-dashboard-json grafana-transform-panel-data grafana-use-dashboard-variables grafana-write-promql policy-dockerfile policy-lua policy-python policy-ts-js prompt-guidance -y
```
