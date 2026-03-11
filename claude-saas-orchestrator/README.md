# Claude SaaS Orchestrator

This directory contains a Claude-centered multi-agent SaaS delivery setup. It is designed for taking a SaaS request from problem framing through release readiness with explicit owners, shared artifacts, and ordered handoffs.

The default operating rule is simple: the orchestrator delegates, specialists implement.

## What This Includes

- a nine-agent team under `.claude/agents/`
- a reusable skills library under `.claude/skills/`
- a default delivery workflow in `.claude/workflows/saas-build.md`
- a command entrypoint in `.claude/commands/build-saas.md`
- shared project memory in `.claude/memory/project-context.md`
- reference docs and exported repo-spec bundles in the root directory

## Default Operating Model

Use the `orchestrator` as the default entrypoint for any non-trivial task. The orchestrator owns:

- framing the problem
- choosing the required agents
- sequencing handoffs
- keeping shared memory current
- checking that outputs are consistent and release-ready

Specialist agents then own their respective deliverables.

## Agent Roster

- `orchestrator`: coordinates the full delivery pass and final readiness review
- `product-manager`: defines PRD, scope, backlog, user stories, and acceptance criteria
- `architect`: defines architecture, interfaces, and implementation slices
- `backend-engineer`: builds APIs, business logic, data access, and integrations
- `frontend-engineer`: builds user flows, UI states, and backend integration
- `ai-engineer`: owns prompts, orchestration logic, retrieval, and evaluation
- `qa-engineer`: validates behavior, regressions, and release risk
- `security-reviewer`: reviews auth, RBAC, threat model, and exposure risks
- `devops-engineer`: handles deployment, CI/CD, observability, and rollback planning

## Default Delivery Sequence

The standard flow in `.claude/workflows/saas-build.md` is:

1. Orchestrator frames the objective, constraints, owners, and success criteria.
2. Product manager defines the PRD, feature scope, backlog, and acceptance criteria.
3. Architect defines architecture, interfaces, data model, and implementation slices.
4. Backend, frontend, and AI engineers implement in parallel only when contracts are stable.
5. QA validates behavior against acceptance criteria.
6. Security reviewer audits architecture and implementation.
7. DevOps prepares deployment, observability, rollback, and environment updates.
8. Orchestrator performs the final consistency and readiness review.

If a downstream agent has to guess, orchestration failed upstream.

## Shared Artifacts

The workflow expects these artifacts to stay current:

- `.claude/memory/project-context.md`
- `docs/prd.md`
- `docs/architecture.md`
- `tasks/backlog.md`
- QA, security, and deployment reports created during execution

Update `.claude/memory/project-context.md` after any material decision that changes scope, architecture, interfaces, risk, or rollout assumptions.

## How To Use It

Start with the orchestrator or the `build-saas` command.

If your Claude setup loads project commands, use:

```text
/build-saas
Objective: Add team invitations to the SaaS app.
Constraints: Must use existing auth model. No org billing changes.
Definition of done: PRD, architecture, API contract, UI, tests, security review, deployment notes.
Execution rule: Start with product-manager, then architect. Only parallelize frontend and backend after API and data model are fixed.
```

If you prefer a direct prompt, give the orchestrator the same structure:

```text
Objective: Add team invitations to the SaaS app.
Constraints: Must use existing auth model. No org billing changes.
Definition of done: PRD, architecture, API contract, UI, tests, security review, deployment notes.
Execution rule: Start with product-manager, then architect. Only parallelize frontend and backend after API and data model are fixed.
```

Every handoff should include:

1. Objective
2. Inputs to read first
3. Expected deliverables
4. Constraints and non-goals
5. Definition of done
6. Next suggested owner after completion

## Skills Library

The skills under `.claude/skills/` cover the main SaaS delivery disciplines, including:

- planning and orchestration
- product strategy and PRD generation
- software architecture and system design
- API and database design
- backend implementation
- frontend implementation
- AI and retrieval workflows
- testing and evaluation
- security and threat modeling
- infrastructure and CI/CD

Use the skills referenced by each specialist agent rather than inventing a new workflow mid-task.

## File Guide

- [docs/agent-orchestration-guide.md](./docs/agent-orchestration-guide.md): primary guide for orchestration rules, sequencing, and failure modes
- [claude-saas-orchestrator/.claude/workflows/saas-build.md](./.claude/workflows/saas-build.md): default execution order and release-readiness rules
- [claude-saas-orchestrator/.claude/commands/build-saas.md](./.claude/commands/build-saas.md): command entrypoint for the standard delivery pass
- [claude-saas-orchestrator/.claude/memory/project-context.md](./.claude/memory/project-context.md): shared context that all agents should read and update
- [claude_full_production_repo.txt](./claude_full_production_repo.txt): exported scaffold of the baseline `.claude` repo
- [claude_full_production_repo_with_skills.txt](./claude_full_production_repo_with_skills.txt): expanded scaffold that also includes the full skill definitions
- [claude_skills_only.txt](./claude_skills_only.txt): extracted skill library reference

## Release Readiness

Do not treat work as complete until these are explicit:

- product intent is documented
- architecture and interfaces are documented
- implementation ownership is clear
- acceptance criteria exist
- QA status is recorded
- security findings are resolved or explicitly accepted
- deployment and rollback notes exist
- open risks and follow-up tasks are recorded in shared memory
