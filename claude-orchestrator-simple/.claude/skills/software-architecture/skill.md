software-architecture

description: Design overall application architecture for
maintainability, scale, and clarity.

when_to_use: Use this skill when the task directly involves software
architecture responsibilities, decisions, implementation, or validation.

tools_allowed: - read_files - write_files - create_files - run_shell

context_to_load: - docs/prd.md - docs/architecture.md -
docs/api-spec.md - docs/db-schema.md - tasks/backlog.md -
.claude/memory/project-context.md - relevant source directories

inputs: - task description - relevant project files - architecture
context - related documentation

outputs: - implementation plan - proposed changes - code or
configuration when applicable - validation steps

execution_rules: 1. Read the relevant docs and code before proposing
changes. 2. Keep outputs deterministic and structured. 3. Prefer
production-ready patterns over placeholders. 4. State assumptions when
required context is missing. 5. Name files explicitly when generating or
modifying artifacts.

required_output_format: ### Summary What is being done and why.

Plan

Ordered implementation steps.

Artifacts

Files to create or modify.

Implementation

Concrete code, config, or content.

Validation

How to verify correctness.

Risks

Potential issues, edge cases, or follow-up items.