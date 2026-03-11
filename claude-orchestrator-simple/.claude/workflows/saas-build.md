name: SaaS Build
description: End-to-end workflow for building and deploying a SaaS application feature.

steps:
  - id: 1
    agent: product-manager
    action: "Create/Update `docs/prd.md` and `tasks/backlog.md` based on feature request."
    output: [docs/prd.md, tasks/backlog.md]

  - id: 2
    agent: architect
    action: "Review PRD and create `docs/architecture.md`, `docs/database-schema.md`, and `docs/api-spec.json`."
    input: [docs/prd.md]
    output: [docs/architecture.md, docs/api-spec.json]

  - id: 3
    agent: security-reviewer
    action: "Review architecture for vulnerabilities and perform threat modeling."
    input: [docs/architecture.md, docs/api-spec.json]
    output: [docs/security-audit.md]

  - id: 4
    agent: orchestrator
    action: "Sync engineers (Backend, Frontend, AI) to align on `docs/api-spec.json`."
    gate: "All engineers must approve the API contract."

  - id: 5
    agent: [backend-engineer, frontend-engineer, ai-engineer]
    action: "Parallel implementation of features following the API spec."
    input: [docs/api-spec.json, docs/architecture.md]
    output: [src/*, tests/*]

  - id: 6
    agent: qa-engineer
    action: "Execute `docs/test-plan.md` and report results in `tasks/bug-reports.md`."
    input: [src/*, tests/*]
    output: [tasks/bug-reports.md]

  - id: 7
    agent: security-reviewer
    action: "Perform final code audit and RBAC verification."
    input: [src/*]
    output: [docs/security-audit.md]

  - id: 8
    agent: devops-engineer
    action: "Deploy to staging/production via CI/CD pipelines."
    gate: "Must have approvals from QA and Security Reviewer."
    output: [infra/deploy-logs.txt]

  - id: 9
    agent: orchestrator
    action: "Finalize `project-context.md` and notify the user of completion."