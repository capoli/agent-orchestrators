---
name: frontend-design
description: Use this skill when the user needs UI or UX direction, a screen redesign, interaction improvements, visual hierarchy fixes, or implementation-ready frontend design guidance. It is especially useful when reviewing an existing interface in a repo and turning a product brief into concrete layout, component, state, and accessibility decisions.
---

# Frontend Design

Use this skill to turn product requests into stronger interface decisions. Start from the actual UI, challenge weak assumptions, and produce guidance that is specific enough for implementation rather than generic design commentary. If the request is for real code changes, use the design work to drive concrete edits once the direction is clear.

## When To Use

Use it when the user asks to:

- design or redesign a screen, flow, or component
- improve hierarchy, usability, density, navigation, or interaction cost
- turn a rough product brief into implementation-ready frontend direction
- review an existing interface before making code changes

## Workflow

### 1. Review the real interface first

Inspect the repo, screenshots, mockups, or live UI before proposing changes. Reuse established patterns when the product already has a coherent design system.

### 2. Clarify the design target

Identify:

- user and task
- success metric
- device context
- constraints and non-goals

If a key constraint is missing, state the assumption explicitly instead of hand-waving around it.

### 3. Diagnose the actual UX problem

Separate visual taste from usability issues. Look for problems with:

- hierarchy and information density
- navigation and flow
- feedback and affordances
- empty, loading, error, and disabled states
- accessibility and keyboard behavior

### 4. Propose a clear direction

Avoid bland layouts and interchangeable UI patterns. Recommend a specific direction for:

- layout and content structure
- typography, spacing, and rhythm
- interaction behavior and motion
- responsive behavior across desktop and mobile

Preserve product fit over novelty.

### 5. Make the result buildable

Express the recommendation in terms engineers can implement:

- component structure
- state handling
- interaction rules
- content hierarchy
- accessibility requirements

### 6. Implement when requested

If the user wants the design applied in the current codebase, carry the work through into concrete edits instead of stopping at critique.

## Output

Produce a compact design package tailored to the task:

- a brief diagnosis of the current UI or brief
- a proposed direction with rationale and tradeoffs
- concrete recommendations for layout, components, interactions, states, and responsive behavior
- accessibility notes where they materially affect the solution
- implementation guidance or code changes, depending on the request

## Guardrails

- Respect an existing design system unless there is a clear reason to break from it.
- Do not present generic polish as design thinking.
- Do not skip edge cases such as loading, error, empty, disabled, and mobile states.
- If the current UI is already strong, refine it instead of forcing a full redesign.
