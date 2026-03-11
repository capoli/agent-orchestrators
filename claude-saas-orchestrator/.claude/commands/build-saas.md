command: build-saas

intent:

Execute the standard multi-agent SaaS delivery workflow from problem framing through release readiness.

steps:

1. Read `.claude/memory/project-context.md` and summarize the latest known state.
2. Run the orchestrator to define the objective, owners, constraints, and definition of done.
3. Execute `.claude/workflows/saas-build.md` in order, parallelizing only when interfaces are stable.
4. Require each agent to publish deliverables, assumptions, risks, changed files, and next recommended owner.
5. Before completion, confirm product scope, architecture, QA status, security status, and deployment status are all represented in shared memory.

expected_result:

A coordinated SaaS delivery pass with explicit handoffs, traceable decisions, and clear release readiness status.
