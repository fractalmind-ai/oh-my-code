# oh-my-code

`oh-my-code` is a turnkey, process-oriented multi-agent setup.

It vendors `agent-manager` under `.claude/skills/agent-manager`, so a plain `git clone` is enough (no `openskills install` required).

## Requirements

- `python3`
- `tmux`

## Quickstart

If your agent CLI supports `.claude/commands`, use:
- `/oh-my-code/quickstart`

To enable/disable the 15-minute scheduled work cycle:
- `/oh-my-code/startup`
- `/oh-my-code/shutdown`

Or run directly from the repo root:

```bash
python3 .claude/skills/agent-manager/scripts/main.py list
python3 .claude/skills/agent-manager/scripts/main.py start sisyphus
python3 .claude/skills/agent-manager/scripts/main.py start oracle
python3 .claude/skills/agent-manager/scripts/main.py assign sisyphus <<'EOF'
Task:
- <what you want done>
EOF
python3 .claude/skills/agent-manager/scripts/main.py monitor sisyphus --follow
```

## Agents

Agents live in `agents/EMP_*.md`:
- `sisyphus`: orchestrator
- `oracle`: architecture/review/strategy
- `librarian`: docs + multi-repo analysis
- `explore`: fast codebase exploration
- `frontend-ui-ux-engineer`: UI/UX specialist
- `document-writer`: writing specialist
- `multimodal-looker`: image/PDF/diagram analysis

To switch CLIs, edit each agent file’s `launcher:` field.