---
description: Quickstart for oh-my-code (agent-manager + AGENTS.md)
---

# Quickstart

## Goal
Run a zero-setup multi-agent workflow using the vendored `agent-manager` skill in this repo.

## Prereqs
- `python3`
- `tmux`

## Steps

### 1) List configured agents
```bash
python3 .claude/skills/agent-manager/scripts/main.py list
```

### 2) Start the orchestrator + one reviewer
```bash
python3 .claude/skills/agent-manager/scripts/main.py start sisyphus
python3 .claude/skills/agent-manager/scripts/main.py start oracle
```

### 3) Assign a task to the orchestrator
```bash
python3 .claude/skills/agent-manager/scripts/main.py assign sisyphus <<'EOF'
Task:
- <describe what you want built>

Requirements:
- Follow AGENTS.md
- Split into parallel subtasks (oracle + librarian/explore as needed)
- Provide evidence (commands run, files changed)
EOF
```

### 4) Monitor output
```bash
python3 .claude/skills/agent-manager/scripts/main.py monitor sisyphus --follow
```

## Notes
- If you use a different CLI than `codex`, update `agents/EMP_*.md` `launcher:` fields.
