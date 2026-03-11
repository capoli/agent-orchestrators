---
name: build-feature
description: Build one feature with a small orchestration flow: scope, implement, review.
disable-model-invocation: true
argument-hint: "[feature to build]"
---

Use this skill when the user wants to implement one feature cleanly without setting up a large delivery process.

User input: `$ARGUMENTS`

## Workflow

1. Start with the `orchestrator`.
2. If the scope is fuzzy, use `product-planner` first. If it is already clear, keep the planning step minimal.
3. Hand off to `frontend-engineer`, `backend-engineer`, or both for the first useful slice. Use `implementation-engineer` only for a very small mixed-scope task.
4. Hand off to `reviewer` before treating the task as complete.

## Output Expectations

Produce:

- the short working frame from `orchestrator`
- the implementation summary
- validation performed
- reviewer findings, or explicit confirmation that none were found
- the next smallest follow-up if the feature should continue in another step

## Constraints

- Keep the work narrow.
- Prefer one vertical slice over a broad partial implementation.
- Validate each meaningful change.
