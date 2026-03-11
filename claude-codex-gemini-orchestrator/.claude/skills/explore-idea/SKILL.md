---
name: explore-idea
description: Turn a rough idea into a small, buildable plan using the orchestrator and product-planner.
disable-model-invocation: true
argument-hint: "[idea or outcome]"
---

Use this skill when the user has an idea that is still rough and wants to work it out collaboratively before building.

User input: `$ARGUMENTS`

## Workflow

1. Start with the `orchestrator`.
2. Have the `orchestrator` classify the request, state the goal, and define the minimum useful workflow.
3. Hand off to `product-planner` to turn the idea into a lean brief.
4. Keep the discussion collaborative and concrete.
5. End with one recommended next step.

## Output Expectations

Produce:

- a short summary of the idea
- the lean brief from `product-planner`
- the first thin slice to build
- the biggest open risk or uncertainty
- the recommended next step

## Constraints

- Keep it short and practical.
- Ask clarifying questions only if they block meaningful progress.
- Do not jump into implementation unless the user asks to build now.
