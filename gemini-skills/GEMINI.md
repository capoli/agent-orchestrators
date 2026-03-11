# Gemini Workspace Guidance

This repository provides three installable Gemini Agent Skills:

- `frontend-design`
- `feature-dev`
- `code-review`

Use the matching skill when the request is clearly about design, implementation, or review. Use the guidance below as the default operating standard across all three.

## General

- Inspect before editing. Build context from actual code, tests, configuration, screenshots, or running UI before proposing changes.
- Prefer the smallest correct change. Keep scope tight and avoid unrelated cleanup unless it is required for safety.
- Preserve existing conventions. Match the repository’s architecture, naming, and patterns unless there is a strong reason to change them.
- Be explicit about uncertainty. State assumptions, unknowns, and verification gaps instead of hand-waving.
- Verify real behavior. Run the narrowest useful checks first, then expand if needed.

## Designing

- Review the current interface before redesigning it. Avoid designing from abstraction when the real UI can be inspected.
- Clarify the user, task, device context, constraints, and success metric before changing layout or interaction patterns.
- Diagnose the actual UX problem before changing visuals. Focus on hierarchy, flows, states, density, navigation, feedback, and accessibility.
- Make recommendations implementation-ready. Specify layout structure, components, states, responsive behavior, interaction details, and accessibility requirements.
- Cover edge cases when they matter: loading, empty, error, disabled, mobile, keyboard, and screen-reader behavior.
- Avoid generic, interchangeable layouts. Push toward a clear visual direction when the product allows it, but respect an existing design system unless it is the problem.

## Developing

- Search broadly and read narrowly. Find the right entry points and nearby examples before editing.
- Design before patching. Decide what changes, what stays stable, failure modes, and how success will be verified.
- Prefer simple designs over new abstractions unless reuse or complexity clearly justifies them.
- Implement in thin slices when the change is non-trivial.
- Keep public contracts, data flow, and side effects explicit.
- Do not invent behavior the codebase can answer.
- Do not revert unrelated user changes.
- Validate the result with targeted tests, linting, type checks, or manual verification as appropriate.

## Reviewing

- Findings first. Prioritize bugs, regressions, risky behavior changes, missing tests, and scope drift.
- Report only high-confidence issues. Tie each finding to a concrete failure mode and exact file reference.
- Review changed code and directly affected context before expanding scope.
- Do not turn style preferences into findings unless they violate project rules or create real risk.
- If no high-confidence findings remain, say so explicitly and mention residual risk or testing gaps.
