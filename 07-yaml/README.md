# YAML Section

This folder demonstrates a reusable approach for managing environment contracts and GitHub Actions workflows across multiple projects and environments.

## Goals

- Keep secrets out of the repository
- Define a clear `.env.example` contract per project and environment
- Validate that contract in CI without using real secrets
- Generate `.env` only at deploy runtime

## Structure

- `env/`: example environment contracts for each project/environment combination
- `workflows/ci.yml`: validates YAML and `.env.example` conventions on pull requests
- `workflows/deploy.yml`: selects project/environment and generates `.env` at runtime

## Naming Convention

Environment files follow this format:

`<project>.<environment>.env.example`

Examples:

- `dispatch.staging.env.example`
- `dispatch.prod.env.example`
- `portal.staging.env.example`
- `portal.prod.env.example`

Projects included:

- `dispatch`
- `portal`

Environments included:

- `staging`
- `prod`

## `.env.example` Contract Rules

Each file:

- contains only example values or empty placeholders
- never contains real secrets
- groups variables using `# required` and `# optional`
- includes shared Twilio variables for SMS-related integrations
- may include project-specific keys when the applications differ

## CI Validation Scope

The CI workflow is intentionally focused on contract validation rather than real deployment behavior.

It verifies:

- YAML syntax/linting
- the expected `.env.example` file exists for each matrix entry
- key naming and `KEY=value` formatting
- required shared keys such as Twilio credentials
- project-specific required keys
- duplicate key detection

This allows CI to fail when the environment contract is broken, even though no real secrets are available in pull requests.

The `Run tests` step is intentionally left as a placeholder. Since this exercise does not include runnable application code for each project, the CI workflow focuses on validating configuration contracts and reusable workflow structure rather than pretending to run project-specific test suites.

## Deploy Workflow Notes

The deploy workflow is intentionally generic:

- it resolves project and environment from a tag or manual input
- it reads secrets from GitHub Environments at runtime
- it generates a temporary `.env`
- the final deploy command is left as a placeholder on purpose

This keeps the exercise focused on secret handling and workflow structure rather than on any specific deployment technology.

The generated `.env` is also intentionally minimal. It demonstrates the runtime secret-loading pattern and environment resolution logic, but it is not meant to represent a production-ready, exhaustive mapping of every required variable from each `.env.example` file.
