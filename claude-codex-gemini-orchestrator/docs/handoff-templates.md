# Handoff Templates

These templates are the convenience layer for moving work between Claude, Codex, and Gemini.

## Files

- [shared-handoff-template.md](./templates/shared-handoff-template.md)
- [codex-feature-handoff.md](./templates/codex-feature-handoff.md)
- [codex-bugfix-handoff.md](./templates/codex-bugfix-handoff.md)

## Recommended Usage

1. Ask Claude to turn the request into a thin slice.
2. Ask Claude to emit the filled shared handoff template with `/emit-codex-handoff` or `/emit-gemini-handoff`.
3. Paste that handoff into Codex with the feature or bugfix prompt template, or into Gemini with `/implement-slice`, `/fix-root-cause`, or `/repo-context`.
4. Use Gemini `/review-diff` when you want a risk-focused review of the current working tree changes.

If Gemini does not show the new command immediately, restart Gemini CLI so it reloads the project commands.

## Example Claude Request

```text
/emit-codex-handoff Add email verification to signup.
Turn this into one thin slice and prepare it for Codex.
```

```text
/emit-gemini-handoff Review the current diff for regressions and missing tests.
Prepare the handoff for Gemini.
```

## Example Gemini Requests

```text
/implement-slice
[Paste the filled shared handoff here]
```

```text
/fix-root-cause
[Paste the filled shared handoff here]
```

```text
/review-diff
Focus on regressions and missing tests.
```
