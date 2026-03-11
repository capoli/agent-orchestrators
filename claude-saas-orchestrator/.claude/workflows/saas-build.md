workflow: saas-build

purpose:

Provide the default execution order for building or extending a SaaS product with multiple specialist agents.

shared_artifacts:

- `.claude/memory/project-context.md`
- `docs/prd.md`
- `docs/architecture.md`
- `tasks/backlog.md`
- QA, security, and deployment reports produced during execution

default_sequence:

1. Orchestrator frames the objective, constraints, owners, and success criteria.
2. Product manager defines the PRD, feature scope, backlog, and acceptance criteria.
3. Architect defines architecture, interfaces, data model, and implementation slices.
4. Backend, frontend, and AI engineers implement in parallel where contracts are stable.
5. QA validates against acceptance criteria and reports regressions or release risk.
6. Security reviewer audits architecture and implementation for exploitable gaps.
7. DevOps prepares deployment, observability, rollback, and environment updates.
8. Orchestrator performs final consistency review and decides whether the work is ready to hand back.

execution_rules:

- Do not skip shared context updates after material decisions.
- Do not parallelize work that depends on undefined interfaces.
- If a downstream agent finds a blocking ambiguity, route it back to the upstream owner immediately.
- Every phase must leave artifacts that the next phase can consume without guessing.
- Release readiness requires product acceptance criteria, QA status, security findings status, and deployment notes.
