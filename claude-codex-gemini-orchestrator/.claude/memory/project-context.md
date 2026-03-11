# Project Context

Use this file as shared memory for the orchestration flow.

Update it when any of the following change in a meaningful way:

- product direction
- scope
- architectural decisions
- important constraints
- active risks
- open questions that still matter

## Current Project Summary

- Purpose: Set up a cross-tool workflow with Claude as the orchestrator, Codex for implementation, and Gemini for repo-context and command-driven coding help.
- Default entrypoint: `orchestrator`
- Active specialist agents: `product-planner`, `bug-investigator`, `frontend-engineer`, `backend-engineer`, `implementation-engineer`, `reviewer`

## Working Principles

- Keep the system simple and readable.
- Use the fewest agents that can do the job well.
- Prefer small steps and narrow validation.
- Prove bugs before fixing them.

## Active Decisions

- Use project-local `.claude/agents` for specialist roles.
- Use project-local `.claude/skills` as the workflow entrypoints.
- Keep the initial setup small instead of importing a large agent library.
- Prefer explicit frontend and backend ownership when the task boundary is clear.
- Add `AGENTS.md` as the Codex adapter layer.
- Add `GEMINI.md` and `.gemini/commands` as the Gemini adapter layer.
- Use one shared handoff template for Claude -> Codex and Claude -> Gemini transfers.
- Add a Gemini `/review-diff` command for risk-focused diff review.
- Add Claude skills to emit Codex-ready and Gemini-ready handoffs directly.

## Open Questions

- Whether a `qa-engineer` is worth adding after real usage.
- Whether to add repo-specific test and stack conventions after the first few tasks.
