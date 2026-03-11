---
name: feature-dev
description: Use this skill when the user asks for a scoped feature, bug fix, refactor, or multi-file code change in an existing repository. It guides Gemini through evidence-first context gathering, targeted planning, implementation, debugging, verification, and review.
---

# Feature Development

Use this skill for delivery work that needs repository understanding before code changes. The goal is to move from request to verified diff without skipping the investigation and review steps that prevent avoidable regressions. Once the path is clear, continue into implementation rather than stopping at analysis unless the user asked for planning only.

## When To Use

Use it when the request:

- requires code changes rather than only explanation
- touches multiple files, layers, or behaviors
- needs architecture tradeoffs, debugging, or validation
- benefits from structured investigation before implementation

Skip it for trivial single-line edits where planning overhead is larger than the change.

## Operating Loop

### 1. Frame the task

Turn the request into a concrete target:

- user goal
- constraints and non-goals
- acceptance signals
- likely surfaces in the codebase

If requirements are vague, narrow the problem with evidence from the repo before asking questions.

### 2. Build context from the codebase

Inspect first, edit second.

- find the entry points, data flow, tests, and similar implementations
- read the current behavior before proposing a rewrite
- prefer primary evidence from code, configs, and tests over assumptions
- record unknowns, invariants, and likely blast radius

Output: a short map of relevant files, current behavior, and open risks.

### 3. Choose a delivery shape

Pick the lightest process that fits the work:

- simple change: implement directly after context gathering
- moderate change: write a short plan with explicit verification
- broad change: split discovery and implementation into stages

Keep the scope tight. Defer unrelated cleanup unless it is required to ship the change safely.

### 4. Design before patching

Before editing, decide:

- what will change
- what will stay untouched
- what the failure modes are
- how success will be verified

Prefer the smallest correct design that matches existing patterns in the repo. Introduce new abstractions only when reuse or complexity clearly justifies them.

### 5. Implement in thin slices

Make changes in an order that preserves control:

1. data contracts and invariants
2. core behavior
3. integration points
4. tests and cleanup

If agent or sub-agent workflows are available, use them only for parallelizable, non-overlapping work.

### 6. Debug with evidence

When behavior is wrong:

- reproduce the issue
- narrow it to one layer or assumption
- inspect logs, failing tests, state transitions, and recent edits
- change one thing at a time when isolating the cause

Do not patch around symptoms until the mechanism is understood.

### 7. Verify and review

Run the narrowest useful checks first, then expand if needed:

- targeted tests for the touched area
- lint or type checks if they cover the change
- manual verification for user-facing flows

Then review the diff as if you did not write it:

- look for regressions, missing tests, and edge cases
- check naming, dead paths, and unintended scope growth
- call out anything you could not verify

## Output

Keep these outputs brief and concrete:

- context: relevant files, current behavior, constraints, unknowns
- plan: chosen approach, rejected alternatives if relevant, verification strategy
- implementation: the shipped slice and any deliberate scope cuts
- verification: commands run, results, and remaining gaps
- review: risks, regressions checked, and follow-up work if needed

## Guardrails

- Prefer focused file reads, existing tests, and nearby examples over assumptions.
- Do not invent behavior that the codebase can answer.
- Preserve established conventions unless there is a strong reason to change them.
- Do not revert unrelated user changes.
- Finish with a real verification attempt whenever the environment allows it.
