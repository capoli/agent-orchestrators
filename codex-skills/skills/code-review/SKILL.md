---
name: code-review
description: Use this skill when the user asks for a review of a pull request, branch diff, commit range, or local uncommitted changes. It helps Codex run a high-signal code review that focuses on regressions, risky behavior changes, missing tests, and scope drift while filtering out speculative or low-confidence comments.
---

# Code Review

Use this skill for review-only work. The goal is to inspect changed code, find the most important issues, and return only findings that are concrete enough for an engineer to act on immediately.

## When To Use

Use it when the user asks to:

- review a pull request, diff, branch, or patch
- inspect staged or unstaged local changes
- sanity-check a large feature before merge
- identify regressions, missing tests, or behavioral risks without implementing fixes

Skip it for implementation tasks unless the user explicitly wants review first.

## Review Gate

Before spending time on a full review, check whether the target is worth reviewing:

- skip closed or already-merged changes unless the user wants a retrospective
- flag draft work and ask whether to review now if the intent is unclear
- note when the diff is too large for a trustworthy pass and narrow it if possible
- prefer reviewing changed lines and directly affected surrounding code over auditing the entire repository

## Review Loop

### 1. Gather the target cleanly

Identify what is being reviewed:

- GitHub PR, commit range, branch, or local diff
- base branch or merge target
- changed files and high-level intent

If `gh` is available and the user wants PR review, use it to inspect metadata and comments. Otherwise use local `git diff`, `git show`, and repository context.

### 2. Load the relevant guidance

Check project instructions before judging the change:

- `AGENTS.md` files that apply to the touched paths
- contribution or review guidance in the repo
- nearby tests, schemas, and similar implementations

Review against the project’s actual conventions, not generic preferences.

### 3. Build a change map

Summarize the diff before looking for problems:

- what behavior changed
- which layers are affected
- where state, data contracts, or side effects moved
- what tests changed or did not change

This map is the baseline for deciding where risk is concentrated.

### 4. Review in focused lenses

For small diffs, review directly. For broader diffs, parallelize with `explorer` agents using disjoint questions such as:

- correctness and regression risk
- edge cases, state handling, and error paths
- tests, observability, and migration gaps
- project-convention compliance in the touched area

Keep each agent read-only and narrowly scoped. Do not send overlapping review ownership to multiple agents unless one is explicitly validating another’s findings.

### 5. Filter aggressively

Report only issues that clear a high confidence bar:

- there is a specific mechanism for failure
- the problem is tied to an exact file and code path
- the issue matters enough to block or at least materially affect merge quality

Drop comments that are stylistic, hypothetical, already covered elsewhere, or based on missing evidence.

### 6. Verify suspicions before reporting them

When a possible bug is unclear, inspect more code before writing it up:

- trace call sites and data flow
- compare with existing patterns
- check tests for intended behavior
- run narrow commands only if they materially confirm the concern

Do not ask the user to investigate issues you could validate from the repo yourself.

## Output Format

Return findings first, ordered by severity, with precise file references. Each finding should explain:

- what is wrong
- why it matters
- the concrete condition where it breaks

If no high-confidence findings remain, say so explicitly and mention any residual risk or testing gaps.

## Guardrails

- prioritize changed behavior over broad codebase critique
- do not turn preferences into findings
- avoid duplicate findings across similar files
- distinguish clear bugs from missing evidence
- do not suggest fixes unless the user asks; the review output should stand on its own
- if asked to post a review comment externally, first prepare the exact findings locally and only then publish
