---
name: emit-codex-handoff
description: Turn the current task into a Codex-ready handoff using the shared handoff template.
disable-model-invocation: true
argument-hint: "[task, brief, feature, or bug]"
---

Use this skill when the user wants Claude to prepare work for Codex instead of implementing it directly.

User input: `$ARGUMENTS`

## Workflow

1. Read `docs/templates/shared-handoff-template.md`.
2. If the task is still vague, reduce it to one thin slice with explicit acceptance criteria.
3. Classify the task as `feature`, `bugfix`, `review`, or `repo-context`.
4. Fill the shared handoff template completely.
5. Recommend the correct Codex companion prompt:
   - `docs/templates/codex-feature-handoff.md`
   - `docs/templates/codex-bugfix-handoff.md`

## Output Expectations

Produce:

- a one-line handoff summary
- the recommended Codex template
- the filled shared handoff block

## Constraints

- Do not implement code.
- Keep the handoff focused on one thin slice.
- For bugfixes, include evidence and likely root cause if known. If not known, say so explicitly.
