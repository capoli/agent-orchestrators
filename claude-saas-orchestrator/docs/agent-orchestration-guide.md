# Agent Orchestration Playbook

This playbook defines how to use the agents in `.claude/` as a coordinated delivery system rather than a loose set of specialists.

## Core Principle

Use the orchestrator as the default entrypoint for any non-trivial task.

The orchestrator owns:

- framing the problem
- deciding which agents are needed
- sequencing handoffs
- keeping shared memory current
- checking that outputs are consistent and release-ready

The orchestrator does not replace specialist agents. It routes work to them.

## Source Of Truth

Read these before starting material work:

- `.claude/memory/project-context.md`
- `.claude/workflows/saas-build.md`
- the relevant files under `.claude/agents/`
- any existing product, architecture, code, task, QA, security, or deployment artifacts

Update `.claude/memory/project-context.md` after any decision that changes:

- scope
- architecture
- interfaces
- risks
- rollout assumptions

If shared memory is stale, downstream agents will guess. Do not allow that.

## Default Execution Order

Use this sequence unless the task is small enough to justify a subset:

1. Orchestrator frames the objective, constraints, owners, and success criteria.
2. Product manager defines PRD, backlog, feature scope, and acceptance criteria.
3. Architect defines system design, interfaces, and implementation slices.
4. Backend, frontend, and AI engineers implement in parallel only when contracts are stable.
5. QA validates behavior against acceptance criteria and reports release risk.
6. Security reviewer audits architecture and implementation.
7. DevOps prepares deployment, observability, rollback, and environment changes.
8. Orchestrator performs the final consistency and readiness review.

## When To Parallelize

Parallelize only independent workstreams.

Safe examples:

- frontend and backend after API contracts are fixed
- backend and AI after data contracts and service boundaries are fixed
- QA authoring test plans while implementation is in progress

Unsafe examples:

- frontend starting before API behavior is defined
- backend starting before product acceptance criteria exist
- AI behavior design starting before user intent and safety boundaries are clear

If an agent depends on undefined interfaces, route the issue back upstream immediately.

## Agent Responsibilities

### Orchestrator

Use for:

- task intake
- scope framing
- work sequencing
- owner assignment
- cross-agent review
- final readiness decision

Required output:

- short summary of goal, desired outcome, constraints, and open questions
- named owners per deliverable
- definition of done
- next handoff

### Product Manager

Use for:

- PRD creation
- feature scoping
- user stories
- backlog definition
- acceptance criteria

Primary outputs:

- `docs/prd.md`
- `docs/features/<feature-name>.md`
- `tasks/backlog.md`

Do not send implementation work forward until acceptance criteria are explicit.

### Architect

Use for:

- architecture decisions
- service boundaries
- API design
- data model design
- implementation slices for parallel work

Primary outputs:

- `docs/architecture.md`
- `docs/api/<service-or-feature>.md`
- `docs/data-model.md`

Do not let implementation start if the architect has left interface gaps.

### Backend Engineer

Use for:

- APIs
- business logic
- data access
- migrations
- integrations

Inputs:

- PRD
- architecture
- API docs
- data model docs

Required reporting:

- changed files
- test status
- assumptions
- risks
- next recommended owner

### Frontend Engineer

Use for:

- user flows
- UI states
- integration with backend and AI interfaces

Inputs:

- PRD
- architecture
- feature specs
- API docs

Frontend work is not complete unless loading, empty, error, and success states are covered.

### AI Engineer

Use for:

- prompt definitions
- orchestration logic
- retrieval and evaluation setup
- model integration behavior

Inputs:

- PRD
- architecture
- backend contracts
- security constraints

Do not allow AI behavior to ship without measurable evaluation criteria.

### QA Engineer

Use for:

- test planning
- regression validation
- release risk reporting
- automated test updates where appropriate

Primary outputs:

- `qa/test-plan.md`
- `qa/reports/<feature-name>.md`

QA should validate against documented acceptance criteria, not informal expectations.

### Security Reviewer

Use for:

- auth review
- RBAC review
- threat modeling
- data exposure review
- infrastructure and AI risk review

Primary outputs:

- `docs/security-review.md`
- `docs/threat-model.md`

Security findings should include severity, impact, and remediation guidance.

### DevOps Engineer

Use for:

- deployment configuration
- CI or CD updates
- environment setup
- observability
- rollback planning

Primary output:

- `docs/deployment.md`

Release readiness is incomplete without deployment notes and rollback expectations.

## Required Handoff Format

Every orchestrator assignment should include these fields:

1. Objective
2. Inputs to read first
3. Expected deliverables
4. Constraints and non-goals
5. Definition of done
6. Next suggested owner after completion

Use this template:

```text
Owner: architect
Objective: Define the technical design for team invitations.
Inputs to read first: .claude/memory/project-context.md, docs/prd.md
Expected deliverables: docs/architecture.md, docs/api/team-invitations.md, docs/data-model.md
Constraints and non-goals: Use existing auth model. No billing changes. No implementation.
Definition of done: Backend and frontend can implement without guessing.
Next suggested owner after completion: backend-engineer and frontend-engineer
```

Require each specialist to return:

- assumptions
- changed files
- test status
- risks
- recommended next owner

## Minimal Operating Loop

For each substantial request:

1. Read shared memory and relevant artifacts.
2. Have the orchestrator restate the request as a delivery problem.
3. Route work to the correct upstream owner first.
4. Block downstream execution until dependencies are stable enough.
5. Update shared memory after each material decision.
6. Run QA, security, and deployment review before closing the work.
7. Have the orchestrator perform the final consistency check.

## Recommended Prompt Pattern

Use a prompt like this with the orchestrator:

```text
Objective: Add team invitations to the SaaS app.
Constraints: Must use existing auth model. No org billing changes.
Definition of done: PRD, architecture, API contract, UI, tests, security review, deployment notes.
Execution rule: Start with product-manager, then architect. Only parallelize frontend and backend after API and data model are fixed.
```

Then use explicit assignments for each specialist rather than broad requests like "go build this."

## Failure Modes To Avoid

- sending multiple agents after the same deliverable
- starting implementation before scope is stable
- starting frontend or AI work before contracts are defined
- skipping shared memory updates after decisions
- asking QA to test without acceptance criteria
- asking security to review only at the very end
- treating DevOps as an afterthought
- closing work without a final orchestrator review

## Release Readiness Checklist

Do not hand work back as complete until all of the following are explicit:

- product intent is documented
- architecture and interfaces are documented
- implementation ownership is clear and non-overlapping
- acceptance criteria exist
- QA status is recorded
- security findings are resolved or explicitly accepted
- deployment and rollback notes exist
- open risks and follow-up tasks are recorded in shared memory

## Practical Rule

If a downstream agent has to guess, orchestration failed upstream.
