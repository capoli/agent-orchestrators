---
name: fix-bug
description: Fix one bug using a strict flow: prove it, fix it, review it.
disable-model-invocation: true
argument-hint: "[bug description]"
---

Use this skill when the user reports a bug and wants a disciplined debugging workflow.

User input: `$ARGUMENTS`

## Workflow

1. Start with the `orchestrator`.
2. Hand off to `bug-investigator` to reproduce the issue and identify the likely root cause.
3. Only after evidence exists, hand off to `frontend-engineer`, `backend-engineer`, or `implementation-engineer` for the smallest safe fix.
4. Hand off to `reviewer` before closing the task.

## Output Expectations

Produce:

- the short working frame from `orchestrator`
- bug reproduction status
- root-cause evidence
- the fix summary
- validation performed
- reviewer findings, or explicit confirmation that none were found

## Constraints

- Do not guess.
- Do not apply broad workarounds before understanding the cause.
- Prefer one targeted fix over a large cleanup.
