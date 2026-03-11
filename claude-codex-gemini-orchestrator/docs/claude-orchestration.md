# Simple Claude Agent Orchestration

This setup takes the useful pattern from the articles and repo you shared, then trims it down to something practical:

- one coordinator
- a few specialist agents
- five workflow entrypoints

The goal is not to simulate a full company org chart. The goal is to help you think through ideas, build one feature, or fix one bug without losing clarity.

## Why This Is Small

The repo you shared includes many agents and many skills. That can be useful later, but it is too much for a starting point.

This setup keeps only the roles that directly support your stated workflows:

- `orchestrator`
- `product-planner`
- `bug-investigator`
- `frontend-engineer`
- `backend-engineer`
- `implementation-engineer`
- `reviewer`

The main Claude skills are now:

- `explore-idea`
- `build-feature`
- `fix-bug`
- `emit-codex-handoff`
- `emit-gemini-handoff`

## File Layout

```text
CLAUDE.md
.claude/
  agents/
    orchestrator.md
    product-planner.md
    bug-investigator.md
    frontend-engineer.md
    backend-engineer.md
    implementation-engineer.md
    reviewer.md
  skills/
    explore-idea/SKILL.md
    build-feature/SKILL.md
    fix-bug/SKILL.md
    emit-codex-handoff/SKILL.md
    emit-gemini-handoff/SKILL.md
  memory/
    project-context.md
```

## How To Use It

Claude's current docs now recommend project `skills` as the main way to expose slash-invocable workflows. That is why this setup uses `.claude/skills` instead of relying on the older `.claude/commands` pattern from some examples.

Because the subagents were added manually as files, restart your Claude session or use `/agents` to load them immediately.

Agent Teams are also enabled locally in `.claude/settings.local.json` with:

- `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
- `teammateMode: in-process`

That means team sessions will open in the current terminal UI by default. If you later want pane-based teammates, change `teammateMode` to `auto` or `tmux`.

Use these entrypoints:

- `/explore-idea Build a lightweight internal admin for customer refunds`
- `/build-feature Add email verification to signup`
- `/fix-bug Login succeeds but users are redirected back to the login page`
- `/emit-codex-handoff Add email verification to signup`
- `/emit-gemini-handoff Review the current diff for regressions`

You can also ask Claude directly:

- "Use the orchestrator and help me work through this idea..."
- "Use the build-feature skill for this request..."
- "Use the fix-bug skill for this issue..."

## Recommended Operating Style

- Start with `explore-idea` when the request is still fuzzy.
- Use `build-feature` when the scope is already small enough to build.
- Use `fix-bug` when the problem needs evidence before code changes.
- Prefer `frontend-engineer` or `backend-engineer` when one side clearly owns the work.
- Use `implementation-engineer` only when the change is tiny or genuinely mixed-scope.
- Keep most work to 2 or 3 agents.
- Add more specialist agents only after a repeated need shows up.

## Good Next Additions

Only add one of these after you feel the current setup is too small:

- `qa-engineer` if validation keeps getting missed
