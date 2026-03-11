# Claude + Codex + Gemini Workflow

This repository now has three layers:

- Claude for orchestration
- Codex for implementation and parallel execution
- Gemini for repo context and command-driven coding help

## File Layout

```text
CLAUDE.md
AGENTS.md
GEMINI.md
.claude/
  agents/
  skills/
.gemini/
  commands/
docs/
  orchestration-core.md
  claude-orchestration.md
  templates/
  handoff-templates.md
```

## When To Use Which Tool

Use Claude when:

- the task is still an idea
- you need decomposition or sequencing
- you want multi-agent coordination
- you want cross-step synthesis

Use Codex when:

- the task is already scoped
- you want implementation momentum
- you want to split independent workstreams
- you want a concise implementation-focused pass

Use Gemini when:

- you want fast repo mapping
- you want a command-driven coding workflow
- you want a second opinion on code structure or bug investigation

## Recommended Handoff Pattern

Start with Claude:

```text
/explore-idea Add a lightweight admin panel for refunds.
Turn this into one thin slice with acceptance criteria.
```

Or ask Claude to prepare the next-tool handoff directly:

```text
/emit-codex-handoff Add the first refund approval backend endpoint.
```

```text
/emit-gemini-handoff Review the current working diff for regressions.
```

Then move to Codex:

```text
Use the template in docs/templates/codex-feature-handoff.md.
Paste the filled shared handoff from Claude.
```

Or move to Gemini:

```text
/repo-context Refund admin panel
```

```text
/implement-slice Add the first backend endpoint for refund review.
```

```text
/fix-root-cause Refund approval updates the UI but not the stored status.
```

```text
/review-diff
Focus on regressions and missing tests.
```

## Convenience Layer

Use these files for repeatable handoffs:

- [shared-handoff-template.md](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/docs/templates/shared-handoff-template.md)
- [codex-feature-handoff.md](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/docs/templates/codex-feature-handoff.md)
- [codex-bugfix-handoff.md](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/docs/templates/codex-bugfix-handoff.md)
- [handoff-templates.md](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/docs/handoff-templates.md)

And these Claude skills to emit the handoff directly:

- [emit-codex-handoff](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/.claude/skills/emit-codex-handoff/SKILL.md)
- [emit-gemini-handoff](/Users/oliviercappelle/Projects/ai/claude-orchestrator-setup-2/.claude/skills/emit-gemini-handoff/SKILL.md)

## Practical Rule

Let Claude decide what to do. Let Codex and Gemini do the work they are best at.
