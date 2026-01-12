
# oh-my-code (Process-Oriented Agent Rules)

This project exists to replicate the *final working effect* of `oh-my-opencode` **without** relying on in-session hooks/tools.

Instead, we enforce a high-quality, repeatable engineering workflow via:
- `AGENTS.md` rules + templates (session-internal discipline)
- `agent-manager` + tmux sessions (session-external parallelism)

## Scope Rules (Anti-Drift)
- Do only what the user asked; stop exploring once you have enough context to proceed.
- Never modify unrelated repositories or paths outside the task scope.
- Before any work that changes files, capture baseline: `git status --porcelain`.

## Startup (Required)
1. Read nearest `AGENTS.md` (this file).
2. Confirm prerequisites:
   - `python3` available
   - `tmux` available
   - you are at repo root (`pwd` shows the `oh-my-code` directory)

## Target Effects (What we replicate)
- Parallelize work across multiple CLI agents (dev/qa/etc) using separate tmux sessions.
- Prevent drift by enforcing scope rules + evidence.
- Make outputs verifiable and repeatable via a strict output contract.
- Ensure quality gates are run and reported.

## Roles (Recommended)
- **sisyphus**: the orchestrator (recommended model: anthropic/claude-opus-4-5)
- **oracle**: architecture, code review, strategy (recommended model: openai/gpt-5.2)
- **librarian**: multi-repo analysis, doc lookup (recommended model: opencode/glm-4.7-free)
- **explore**: fast codebase exploration (recommended model: grok/gemini/haiku)
- **frontend-ui-ux-engineer**: UI/UX specialist (recommended model: google/gemini-3-pro-preview)
- **document-writer**: technical writing (recommended model: google/gemini-3-flash)
- **multimodal-looker**: PDF/image analysis (recommended model: google/gemini-3-flash)

## Multi-Agent Protocol (agent-manager)
Use `agent-manager` to run workers in separate tmux sessions, then feed tasks in parallel.

This repo vendors `agent-manager` under `.claude/skills/agent-manager`, so it works after a plain git clone (no `openskills install` required). You only need `python3` and `tmux` available.

If you are using a different CLI (e.g. `droid` or `claude`), update `agents/EMP_0001.md` and `agents/EMP_0002.md` to point `launcher:` to your CLI.

### Commands
```bash
# list agents
python3 .claude/skills/agent-manager/scripts/main.py list

# start if needed
python3 .claude/skills/agent-manager/scripts/main.py start sisyphus
python3 .claude/skills/agent-manager/scripts/main.py start oracle

# assign tasks (stdin)
python3 .claude/skills/agent-manager/scripts/main.py assign sisyphus <<'EOF'
<task>
EOF

# monitor
python3 .claude/skills/agent-manager/scripts/main.py monitor sisyphus --follow

# stop
python3 .claude/skills/agent-manager/scripts/main.py stop sisyphus
```

## Task Decomposition Template
When you are orchestrator, produce a short split like:
- Subtask A (Dev): implement
- Subtask B (QA): validate + edge cases
- Subtask C (Optional): quick research

Each subtask must have:
- Objective
- Exact deliverable(s)
- “Done” criteria

## Output Contract (Mandatory)
Every agent response must end with:
1. **Summary**: 1–3 bullets.
2. **Evidence**: exact commands run + brief outcome.
3. **Files Changed**: paths.
4. **Risks/Assumptions**: anything uncertain.
5. **Next Step**: what to do next (or “ready for review”).

## Quality Gates
- If code changed: run the project’s relevant `format/lint/typecheck/test/build` commands and report results.
- If only docs/rules changed: at minimum ensure the file is readable and references valid paths.

## Safety
- Never commit or push unless explicitly asked.
- Never add secrets/keys; never paste tokens into logs.

