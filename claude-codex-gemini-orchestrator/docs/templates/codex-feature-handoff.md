# Codex Feature Handoff Prompt

Use this when Claude has already scoped a feature slice and you want Codex to implement it.

```text
Use the shared handoff below as the source of truth.

Implement the smallest useful feature slice.
Keep the change narrow and easy to review.
If frontend and backend are independent after the contract is clear, split the work cleanly and parallelize only if the file ownership does not overlap.
Validate the smallest relevant increment.

Return:
- goal
- changed files
- validation performed
- remaining risks
- recommended next step

[Paste the filled shared handoff here]
```
