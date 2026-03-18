# Agent Orchestrators

This repository collects small agent orchestration projects and skills packs for Claude, Codex, and Gemini. The documented subdirectories span three orchestration styles and one reusable Gemini skills library.

## Subdirectories With READMEs

| Directory | Focus | What it includes |
| --- | --- | --- |
| [claude-orchestrator-simple](./claude-orchestrator-simple/README.md) | Lightweight orchestration pattern | Operational guidance for using an orchestrator as the single entry point, keeping shared project context current, respecting handoff gates, and parallelizing only after the API contract is stable. |
| [claude-saas-orchestrator](./claude-saas-orchestrator/README.md) | Full SaaS delivery workflow | A Claude-centered delivery setup with a nine-agent team, reusable skills, shared project memory, workflow and command entrypoints, and explicit release-readiness artifacts. |
| [claude-codex-gemini-orchestrator](./claude-codex-gemini-orchestrator/README.md) | Cross-tool orchestration | A small workflow where Claude scopes and sequences work, Codex handles implementation and parallel execution, and Gemini provides repo mapping, debugging, and diff review. |
| [gemini-skills](./gemini-skills/README.md) | Gemini CLI skills library | Gemini-ready `frontend-design`, `feature-dev`, and `code-review` skills packaged as top-level folders for CLI discovery. |

## Common Patterns

Across the documented subdirectories, the recurring ideas are:

- one clear orchestrator or owner for sequencing
- shared project context or memory that stays current
- gated handoffs before downstream implementation starts
- parallel execution only when interfaces are stable
- explicit validation, review, and release-readiness checks

## Choosing A Starting Point

- Start with [claude-orchestrator-simple](./claude-orchestrator-simple/README.md) if you want the lightest operating model.
- Start with [claude-saas-orchestrator](./claude-saas-orchestrator/README.md) if you want a fuller Claude-only delivery scaffold.
- Start with [claude-codex-gemini-orchestrator](./claude-codex-gemini-orchestrator/README.md) if you want Claude-led planning with Codex and Gemini handoffs.
- Start with [gemini-skills](./gemini-skills/README.md) if you mainly want reusable Gemini CLI skills rather than a full orchestration repo.

Each subdirectory keeps its own README for the local workflow details, commands, and supporting docs.
