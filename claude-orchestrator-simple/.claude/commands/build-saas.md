# Command: build-saas
Description: Initiates the end-to-end SaaS build workflow managed by the Orchestrator.

## Usage
`invoke-command build-saas [feature_description]`

## Steps
1. **Bootstrap:** Orchestrator loads `project-context.md` and `saas-build.md`.
2. **Analysis:** Orchestrator parses the `feature_description` and maps it to the PRD.
3. **Execution:** Orchestrator sequences agent tasks per the `SaaS Build` workflow.
4. **Validation:** All gates in the workflow must be satisfied.
5. **Finalization:** Update `project-context.md` with the new feature state.

## Parameters
- `feature_description`: Text description of the feature to be built or updated.
- `force`: Optional flag to bypass non-critical review gates (default: false).