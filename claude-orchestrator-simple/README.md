To effectively use this multi-agent orchestration system, follow these operational patterns:


  1. The Entry Point: The Orchestrator
  Always treat the Orchestrator as your single point of contact. Instead of giving instructions to individual engineers, invoke the build-saas command via the Orchestrator with a high-level feature description.


   * Example: invoke-command build-saas "Add a subscription billing system using Stripe"
   * Why: The Orchestrator will automatically sequence the Product Manager to define requirements and the Architect to design the API before any code is written.


  2. The Shared Brain: project-context.md
  This file is the "source of truth." Before starting any major task, ensure the Orchestrator updates this file.
   * Verification: If an agent seems "lost" or suggests an incompatible tech stack, check if project-context.md reflects your latest architectural decisions.
   * Usage: Agents are instructed to read this file first to understand the "Phase" and "Active Task" of the project.


  3. Respecting the Handoff Gates
  The workflow defines "Gates" (Validation points). Never bypass these unless for rapid prototyping.
   * Design Gate: Ensure the Security Reviewer audits the docs/architecture.md before the Backend Engineer starts coding.
   * API Gate: The Frontend and Backend engineers must both "approve" the docs/api-spec.json created by the Architect. This prevents "integration hell" later.
   * Quality Gate: The QA Engineer must verify the tasks/bug-reports.md is empty (or resolved) before DevOps is permitted to deploy.


  4. Parallel Execution
  The system is designed for concurrency. Once the api-spec.json is finalized:
   * The Backend Engineer builds the logic.
   * The Frontend Engineer builds the UI.
   * The AI Engineer builds the RAG pipelines.
   * Action: You can ask the Orchestrator to "Run implementation agents in parallel" to speed up the development cycle.


  5. Managing Feedback Loops
  If an agent fails a review (e.g., Security finds a flaw):
   1. The Orchestrator sends the task back to the owner with the review log.
   2. Do not manually fix the code; let the specific agent (e.g., Backend Engineer) perform the remediation to ensure documentation and tests are also updated.


  Summary of Workflow
   1. Define: User -> Orchestrator -> PM (prd.md).
   2. Design: Architect -> Security (architecture.md, api-spec.json).
   3. Build: Backend + Frontend + AI (Parallel implementation).
   4. Verify: QA + Security (Testing and Audit).
   5. Deliver: DevOps (Deployment).

