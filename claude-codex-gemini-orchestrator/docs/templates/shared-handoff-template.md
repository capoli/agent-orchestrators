# Shared Handoff Template

Claude can emit this block directly when handing work to Codex or Gemini.

Copy the template, fill it in, and paste it as-is into the next tool.

```text
Objective:
[one clear task]

Task Type:
[idea | feature | bugfix | review | repo-context]

Acceptance Criteria:
- [criterion]
- [criterion]

Constraints And Non-Goals:
- [constraint or non-goal]
- [constraint or non-goal]

Relevant Files:
- [path or file area]
- [path or file area]

Current State Or Evidence:
- [known context, reproduction notes, or current implementation state]

Validation:
- [smallest relevant checks to run]

Definition Of Done:
- [what must be true when finished]

Risks Or Open Questions:
- [risk or unknown]

Suggested Owner:
[Codex implementation | Codex review | Gemini repo-context | Gemini implement-slice | Gemini fix-root-cause | Gemini review-diff]
```

## Notes

- Keep it short.
- Prefer one thin slice per handoff.
- For bugs, include reproduction evidence before asking for a fix.
