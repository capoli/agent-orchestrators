---
name: emit-gemini-handoff
description: Turn the current task into a Gemini-ready handoff using the shared handoff template.
disable-model-invocation: true
argument-hint: "[task, brief, feature, bug, or review goal]"
---

Use this skill when the user wants Claude to prepare work for Gemini instead of implementing it directly.

User input: `$ARGUMENTS`

## Workflow

1. Read `docs/templates/shared-handoff-template.md`.
2. If the task is still vague, reduce it to one thin slice with explicit acceptance criteria.
3. Classify the task as `repo-context`, `feature`, `bugfix`, or `review`.
4. Fill the shared handoff template completely.
5. Recommend the correct Gemini command:
   - `/repo-context`
   - `/implement-slice`
   - `/fix-root-cause`
   - `/review-diff`

## Output Expectations

Produce:

- a one-line handoff summary
- the recommended Gemini command
- the filled shared handoff block

## Constraints

- Do not implement code.
- Keep the handoff focused on one thin slice.
- For bugfixes, include evidence and likely root cause if known. If not known, say so explicitly.
