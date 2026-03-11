# Codex Working Agreement

This repository uses a multi-tool workflow:

- Claude is the primary orchestrator.
- Codex is the primary implementation and parallel execution engine.
- Gemini is the repo-context and command-driven coding assistant.

Read `docs/orchestration-core.md` for the shared workflow rules.

## Codex Role

Use Codex for:

- implementing a clearly scoped feature slice
- fixing a bug after the problem is reproduced or narrowed down
- parallel execution when workstreams are independent
- targeted reviews and follow-up fixes

Do not default to high-level orchestration here when Claude has already done the planning.

## Skills

If the user explicitly names a Codex skill, or the request clearly matches one, use the relevant installed skill.

Known high-value skills for this environment:

- `skill-creator` for creating or updating Codex skills
- `skill-installer` for listing or installing Codex skills from curated sources or GitHub

When using a skill:

- read only the relevant `SKILL.md`
- follow the skill workflow instead of recreating it from scratch
- keep the context small and load only the files you need

## Default Behavior

- If a Claude brief or acceptance criteria exist, treat them as the source of truth.
- If the input follows the shared handoff format in `docs/templates/shared-handoff-template.md`, treat it as the handoff contract.
- If the request is still vague, produce the smallest workable brief before coding.
- Keep changes narrow and validate the smallest relevant increment.
- Prefer explicit ownership if frontend and backend can be separated cleanly.
- Parallelize only independent work with stable interfaces.

## Convenience Templates

Copy-paste templates for Claude -> Codex handoffs live here:

- `docs/templates/codex-feature-handoff.md`
- `docs/templates/codex-bugfix-handoff.md`

## Parallel Execution Rules

Good candidates:

- frontend and backend after the contract is clear
- implementation and documentation when the docs depend only on known changes
- one bug investigation and one unrelated feature slice

Bad candidates:

- frontend and backend before API behavior is agreed
- multiple agents editing the same files
- implementation before the root cause is understood

## Response Format

When finishing a task, include:

- goal
- changed files
- validation performed
- remaining risks
- recommended next step
