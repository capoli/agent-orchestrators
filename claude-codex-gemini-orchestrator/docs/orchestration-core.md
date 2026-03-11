# Cross-Tool Orchestration Core

This is the shared workflow used across Claude, Codex, and Gemini.

## Tool Roles

- Claude: primary orchestrator for idea shaping, planning, and multi-agent coordination
- Codex: primary implementation engine for scoped work and parallel execution
- Gemini: primary repo-context and command-driven coding assistant

## Shared Rules

- Work in small, testable increments.
- Prove the problem before fixing bugs.
- Use one clear owner per deliverable.
- Parallelize only independent work with stable interfaces.
- Prefer explicit acceptance criteria before implementation.
- Return changed files, validation, risks, and the next step.

## Recommended Flow

1. Start in Claude when the request is still fuzzy.
2. Turn the request into a thin slice with clear acceptance criteria.
3. Hand implementation to Codex when the work is ready to build.
4. Use Gemini when fast repo understanding or command-driven coding help is more useful than orchestration.
5. Bring results back into Claude when you want synthesis, review, or the next coordination step.

## Parallelization Rules

Safe:

- frontend and backend after the contract is fixed
- independent bug investigations
- implementation and follow-up documentation when the scope is stable

Unsafe:

- coding before scope is stable
- frontend and backend before interfaces are clear
- multiple agents touching the same files

## Handoff Template

When handing work from one tool to another, include:

- objective
- acceptance criteria
- constraints and non-goals
- relevant files or file areas
- definition of done
- current risks or open questions

Use the shared ready-to-fill file at [shared-handoff-template.md](./templates/shared-handoff-template.md) when you want a direct Claude -> Codex or Claude -> Gemini handoff.
