---
name: feature-dev
description: Use this skill when the user asks for a scoped feature, bug fix, refactor, or multi-file code change in an existing repository. It guides Codex through evidence-first context gathering, targeted planning, optional parallel sub-agents, implementation, debugging, testing, and review.
---

# Feature Dev

Use this skill for delivery work that needs repository understanding before code changes. The goal is to move from request to verified diff without skipping the investigation and review steps that prevent avoidable regressions. Once the path is clear, continue into implementation rather than stopping at analysis unless the user asked for planning only.

## When To Use

Use it when the request:

- requires code changes rather than only explanation
- touches multiple files, layers, or behaviors
- needs architecture tradeoffs, debugging, or validation
- benefits from parallel context gathering before implementation

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

- use fast search to find the entrypoints, data flow, tests, and similar implementations
- read the current behavior before proposing a rewrite
- prefer primary evidence from code, configs, and tests over assumptions
- record unknowns, invariants, and likely blast radius

Output: a short map of relevant files, current behavior, and open risks.

### 3. Choose a delivery shape

Pick the lightest process that fits the work:

- simple change: implement directly after context gathering
- moderate change: write a short plan with explicit verification
- broad change: split discovery and implementation into stages

Keep the scope tight. Defer unrelated cleanups unless they are required to ship the change safely.

### 4. Use sub-agents only when the work is parallelizable

Use sub-agents to reduce latency, not to hide uncertainty.

- use an `explorer` agent for read-only investigation, dependency tracing, or test discovery
- use a `worker` agent for isolated implementation or focused debugging in disjoint files
- give each sub-agent one precise question, relevant paths, and a clear ownership boundary
- never assign the same file to multiple agents
- rescan the affected files yourself before final edits

If the task is small or tightly coupled, stay single-threaded.

### 5. Design before patching

Before editing, decide:

- what will change
- what will stay untouched
- what the failure modes are
- how success will be verified

Prefer the smallest correct design that matches existing patterns in the repo. Introduce new abstractions only when reuse or complexity clearly justifies them.

### 6. Implement in thin slices

Make changes in an order that preserves control:

1. data contracts and invariants
2. core behavior
3. integration points
4. tests and cleanup

After each slice, compare the result against the original acceptance signals.

### 7. Debug with evidence

When behavior is wrong:

- reproduce the issue
- narrow it to one layer or assumption
- inspect logs, failing tests, state transitions, and recent edits
- change one thing at a time when isolating the cause

Do not patch around symptoms until you understand the mechanism.

### 8. Verify and review

Run the narrowest useful checks first, then expand if needed:

- targeted tests for the touched area
- lint or type checks if they cover the change
- manual verification for user-facing flows

Then review the diff as if you did not write it:

- look for regressions, missing tests, and edge cases
- check naming, dead paths, and unintended scope growth
- call out anything you could not verify

## Phase Outputs

Keep these outputs brief and concrete:

- context: relevant files, current behavior, constraints, unknowns
- plan: chosen approach, rejected alternatives if relevant, verification strategy
- implementation: the shipped slice and any deliberate scope cuts
- verification: commands run, results, and remaining gaps
- review: risks, regressions checked, and follow-up work if needed

## Guardrails

- prefer `rg`, focused file reads, and existing tests over broad scanning
- do not invent behavior that the codebase can answer
- preserve established conventions unless there is a strong reason to change them
- keep sub-agent tasks independent and easy to merge
- finish with a real verification attempt whenever the environment allows it
