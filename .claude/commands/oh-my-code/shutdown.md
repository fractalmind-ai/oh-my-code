---
description: Disable scheduled jobs (remove agent-manager crontab section)
---

# Disable Schedules

## What this does
Removes the `agent-manager schedules` section from your user crontab (it does not edit agent configs).

## Commands

### 1) Show currently installed agent-manager cron section
```bash
python3 - <<'PY'
import sys
from pathlib import Path

scripts = Path('.claude/skills/agent-manager/scripts').resolve()
sys.path.insert(0, str(scripts))

from schedule_helper import get_current_crontab, _get_agent_manager_section

section = _get_agent_manager_section(get_current_crontab())
print(section if section.strip() else '(no agent-manager schedules installed)')
PY
```

### 2) Remove it from crontab
```bash
python3 - <<'PY'
import sys
from pathlib import Path

scripts = Path('.claude/skills/agent-manager/scripts').resolve()
sys.path.insert(0, str(scripts))

from schedule_helper import get_current_crontab, remove_agent_manager_section, set_crontab

current = get_current_crontab()
new = remove_agent_manager_section(current)

if new and not new.endswith('\n'):
    new = new + '\n'

ok = set_crontab(new)
print('OK' if ok else 'FAILED')
PY
```
