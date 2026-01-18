---
description: Enable scheduled jobs (sync to crontab)
---

# Enable Schedules

## What this does
Syncs all enabled agent schedules (from `agents/EMP_*.md`) into your user crontab.

## Commands

### 1) Preview configured schedules
```bash
python3 .claude/skills/agent-manager/scripts/main.py schedule list
```

### 2) Dry-run the crontab content
```bash
python3 .claude/skills/agent-manager/scripts/main.py schedule sync --dry-run
```

### 3) Apply (write to crontab)
```bash
python3 .claude/skills/agent-manager/scripts/main.py schedule sync
```
