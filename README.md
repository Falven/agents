# agents

Repository for installable agent skills and future agent-related artifacts.

### Operator Install With `skills`

Install `prompt-guidance` globally from the remote repo to all agents supported by the `skills` CLI:

```bash
skills add Falven/agents -g --agent '*' --skill prompt-guidance -y
```

You can also install from the direct GitHub skill URL:

```bash
skills add https://github.com/Falven/agents/tree/main/skills/prompt-guidance -g --agent '*' -y
```

Install the same skill from a local checkout when you want local changes to drive the installed copy:

```bash
skills add /path/to/agents -g --agent '*' --skill prompt-guidance -y
```

- `-g` installs at user scope so the skill is available across projects.
- `--agent '*'` targets every agent integration supported by the local `skills` CLI.
- `skills ls -g` lists globally installed skills.
