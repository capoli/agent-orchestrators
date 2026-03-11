# Codex Bugfix Handoff Prompt

Use this when Claude has already reproduced or narrowed down a bug and you want Codex to fix it.

```text
Use the shared handoff below as the source of truth.

Follow a root-cause-first workflow.
Do not guess and do not broaden the fix unnecessarily.
Implement the smallest safe change that addresses the evidence provided.
Validate the smallest relevant check after the fix.

Return:
- goal
- changed files
- validation performed
- remaining risks
- recommended next step

[Paste the filled shared handoff here]
```
