# Claude Working Agreement

## Goal

Use a small agent system to help with:

- exploring an idea and turning it into a workable plan
- implementing one feature end to end
- debugging and fixing one bug at a time

## Tool Roles

- Claude is the primary orchestrator.
- Codex is the primary implementation and parallel execution engine.
- Gemini is the repo-context and command-driven coding assistant.

## Cross-Tool Handoffs

- When handing work to Codex or Gemini, prefer the shared format in `docs/templates/shared-handoff-template.md`.
- Use `/emit-codex-handoff` when the next step should happen in Codex.
- Use `/emit-gemini-handoff` when the next step should happen in Gemini.
- Keep handoffs short and focused on one thin slice.
- For implementation handoffs, include acceptance criteria, constraints, relevant files, and the smallest validation steps.
- For bugfix handoffs, include concrete evidence and the likely root cause before asking for code changes.

## Default Behavior

- Start with the `orchestrator` for any non-trivial request.
- Keep plans small. For most work, use no more than 2 or 3 agents.
- Work in small increments and validate after each meaningful change.
- Prefer current stable APIs and the patterns already used by the codebase.
- Keep solutions simple. Avoid unnecessary abstraction or defensive code.
- For bugs, prove the problem before fixing it.

## Routing Rules

- Vague idea -> `orchestrator` -> `product-planner`
- Feature request -> `orchestrator` -> `product-planner` -> `frontend-engineer` and/or `backend-engineer` -> `reviewer`
- Bug report -> `orchestrator` -> `bug-investigator` -> `frontend-engineer` or `backend-engineer` -> `reviewer`
- Small full-stack change -> `orchestrator` -> `implementation-engineer` -> `reviewer`

## Agent Rules

- One owner per deliverable.
- The `orchestrator` coordinates. It should not do specialist work unless the task is tiny.
- The `product-planner` defines scope and acceptance criteria before implementation starts.
- The `bug-investigator` must show evidence and a likely root cause before code changes.
- The `frontend-engineer` owns UI behavior, states, and frontend integration.
- The `backend-engineer` owns APIs, business logic, data changes, and backend integration.
- The `implementation-engineer` makes the smallest useful change first, then validates it.
- The `reviewer` checks for regressions, missing tests, and obvious risks.

## Reporting Format

When an agent finishes, include:

- goal
- assumptions
- changed files or proposed files
- validation performed
- remaining risks
- recommended next step or next owner

## Shared Memory

Keep `.claude/memory/project-context.md` updated when scope, decisions, constraints, or open questions change in a meaningful way.
