---
description: Assign a task to the orchestrator (sisyphus)
---

# Agents: Assign (Sisyphus)

```bash
python3 .claude/skills/agent-manager/scripts/main.py assign sisyphus <<'EOF'
Task:
- <what you want done>

Must:
- Follow AGENTS.md
- Decompose into parallel subtasks
- Ask oracle for review on risky decisions
- Report evidence: commands run + files changed
EOF
```
