# Claude + Codex + Gemini Orchestrator

This directory packages a small multi-tool workflow for:

- exploring an idea and turning it into a thin slice
- implementing one feature end to end
- debugging one bug at a time
- handing work cleanly between Claude, Codex, and Gemini

The setup is intentionally small. Claude handles orchestration, Codex handles implementation and parallel execution, and Gemini handles repo-context and command-driven coding help.

## Tool Roles

- Claude: planning, decomposition, sequencing, and cross-step synthesis
- Codex: scoped implementation, follow-up fixes, and parallel execution when workstreams are independent
- Gemini: fast repo mapping, command-driven coding, root-cause-first debugging, and diff review

## Core Working Rules

- Work in small, testable increments.
- Prefer explicit acceptance criteria before implementation.
- Use one clear owner per deliverable.
- For bugs, prove the problem before fixing it.
- Parallelize only independent work with stable interfaces.
- Return changed files, validation, risks, and the next step.

These rules are defined in `docs/orchestration-core.md`.

## Repository Layout

```text
AGENTS.md
CLAUDE.md
GEMINI.md
.claude/
  agents/
    orchestrator.md
    product-planner.md
    bug-investigator.md
    frontend-engineer.md
    backend-engineer.md
    implementation-engineer.md
    reviewer.md
  skills/
    explore-idea/SKILL.md
    build-feature/SKILL.md
    fix-bug/SKILL.md
    emit-codex-handoff/SKILL.md
    emit-gemini-handoff/SKILL.md
  memory/
    project-context.md
  settings.json
.gemini/
  commands/
    repo-context.toml
    implement-slice.toml
    fix-root-cause.toml
    review-diff.toml
docs/
  orchestration-core.md
  claude-orchestration.md
  multi-tool-workflow.md
  handoff-templates.md
  templates/
```

## Typical Workflow

1. Start in Claude when the request is still fuzzy.
2. Turn the request into one thin slice with acceptance criteria.
3. Use Claude to emit a short shared handoff for the next tool.
4. Move to Codex for implementation, or Gemini for repo-context, debugging, or review.
5. Bring results back to Claude when you want synthesis, review, or the next coordinated step.

## Claude Entry Points

Claude is the default starting point for non-trivial work. The included skills are:

- `/explore-idea`
- `/build-feature`
- `/fix-bug`
- `/emit-codex-handoff`
- `/emit-gemini-handoff`

Example prompts:

```text
/explore-idea Build a lightweight internal admin for customer refunds.
```

```text
/build-feature Add email verification to signup.
```

```text
/fix-bug Login succeeds but users are redirected back to the login page.
```

```text
/emit-codex-handoff Add the first refund approval backend endpoint.
```

```text
/emit-gemini-handoff Review the current diff for regressions and missing tests.
```

Included Claude agents:

- `orchestrator`
- `product-planner`
- `bug-investigator`
- `frontend-engineer`
- `backend-engineer`
- `implementation-engineer`
- `reviewer`

If Claude does not immediately pick up the project agents or skills, restart the session or use `/agents` to reload them.

## Codex Usage

Use Codex when the task is already scoped and ready to build. Good fits:

- implementing a clearly defined feature slice
- fixing a bug after the evidence and likely root cause are known
- splitting independent workstreams with clean file ownership
- doing a concise implementation-focused pass

When handing work into Codex, use the shared handoff template as the source of truth and then wrap it with:

- `docs/templates/codex-feature-handoff.md`
- `docs/templates/codex-bugfix-handoff.md`

## Gemini Usage

Use Gemini when you want a command-driven workflow or fast repo understanding. Preferred commands:

- `/repo-context`
- `/implement-slice`
- `/fix-root-cause`
- `/review-diff`

Example requests:

```text
/repo-context Refund admin panel
```

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

If Gemini does not show the new project commands immediately, restart Gemini CLI so it reloads them.

## Handoffs

The shared handoff contract lives in `docs/templates/shared-handoff-template.md`.

Use it for Claude -> Codex and Claude -> Gemini transitions. A good handoff includes:

- objective
- task type
- acceptance criteria
- constraints and non-goals
- relevant files
- current state or evidence
- validation
- definition of done
- risks or open questions
- suggested owner

Keep handoffs short and focused on one thin slice.

## Documentation Guide

- `AGENTS.md`: Codex-oriented working agreement for this repo
- `CLAUDE.md`: Claude routing rules, agent responsibilities, and reporting format
- `GEMINI.md`: Gemini role, default behavior, and preferred commands
- `docs/orchestration-core.md`: shared cross-tool rules and recommended flow
- `docs/claude-orchestration.md`: the small-agent Claude setup and entrypoints
- `docs/multi-tool-workflow.md`: the overall Claude/Codex/Gemini workflow
- `docs/handoff-templates.md`: how to use the handoff templates in practice
- `docs/templates/`: ready-to-fill templates for shared, Codex feature, and Codex bugfix handoffs

## Practical Rule

Let Claude decide what to do next. Let Codex and Gemini do the work they are best at.
