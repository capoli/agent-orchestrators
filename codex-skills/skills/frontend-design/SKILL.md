---
name: frontend-design
description: Use this skill when the user needs UI or UX direction, a screen redesign, interaction improvements, visual hierarchy fixes, or implementation-ready frontend design guidance. It is especially useful when reviewing an existing interface in a repo and turning a product brief into concrete layout, component, state, and accessibility decisions.
---

# Frontend Design

## Overview

Use this skill to turn product requests into stronger interface decisions. Start from the actual UI, challenge weak assumptions, and produce guidance that is specific enough for implementation rather than generic design commentary. If the request is for real code changes, use the design work to drive concrete edits once the direction is clear.

## Use When

- The user wants to design or redesign a screen, flow, or component.
- The request mixes product goals with vague UI direction and needs sharper UX choices.
- You need to review an existing frontend before proposing changes.
- The user wants implementation-ready guidance for layout, states, interactions, copy, responsiveness, or accessibility.

## Workflow

1. Review the current state first.
   Inspect the repo, screenshots, mockups, or live UI before proposing changes. Reuse established patterns when the product already has a coherent design system.

2. Clarify the design target.
   Identify the user, task, success metric, device context, and constraints. If a key constraint is missing, state the assumption explicitly instead of hand-waving around it.

3. Diagnose the real UX problem.
   Separate visual taste from usability issues. Call out problems with hierarchy, density, navigation, feedback, empty states, accessibility, or interaction cost.

4. Push past safe defaults.
   Avoid bland layouts and interchangeable UI patterns. Propose a clear direction with intentional structure, typography, spacing, and interaction behavior. Preserve product fit over novelty.

5. Make the recommendation buildable.
   Express the result in terms engineers can implement: component structure, layout rules, responsive behavior, interaction states, content hierarchy, and accessibility requirements.

6. Implement when requested.
   If the user wants the design applied in the current codebase, carry the work through into concrete edits instead of stopping at critique or mock direction.

## Expected Outputs

Produce a compact design package tailored to the task:

- A brief diagnosis of the current UI or brief.
- A proposed direction with rationale and tradeoffs.
- Concrete recommendations for layout, components, interactions, states, and responsive behavior.
- Accessibility and usability notes where they materially affect the solution.
- An implementation plan or concrete code changes, depending on the request.

## Guardrails

- Respect an existing design system unless there is a clear reason to break from it.
- Do not present generic polish as design thinking.
- Do not skip edge cases such as loading, error, empty, disabled, and mobile states.
- If the current UI is already strong, refine it instead of forcing a full redesign.
