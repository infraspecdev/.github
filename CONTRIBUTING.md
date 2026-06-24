# Contributing to infraspecdev projects

> This is an org-wide default. Any infraspecdev repo without its own `CONTRIBUTING.md` inherits this one. Repos may override it with project-specific guidance.

Thanks for contributing! These are the baseline conventions across infraspecdev repositories.

## Getting Started

1. Fork (external) or branch (internal) from the default branch.
2. Create a topic branch: `git checkout -b <type>/<short-description>` (e.g. `feat/json-output`, `fix/timeout`).
3. Make focused, logically-grouped commits. One logical change per commit, tests included.
4. Open a Pull Request against the default branch and fill in the PR template.

## Commit & PR Conventions

- Keep PRs small and reviewable — prefer several small PRs over one large one.
- Write a clear PR description: what changed, why, and how to verify.
- Ensure CI is green (build, tests, linters) before requesting review.
- Update the README and `CHANGELOG.md` when behavior, inputs, or usage change.

## Code Quality

- Match the surrounding code's style, naming, and structure.
- Add or update tests for any behavior change.
- Run the repo's linters/formatters locally before pushing.

## Documentation

- Every repo follows the [infraspecdev README template](./README.template.md) — copy it and delete the sections that don't apply.
- For Terraform modules, never hand-edit the Inputs/Outputs tables — they regenerate via `terraform-docs`.

## Reporting Issues

- **Bugs / features:** open a GitHub issue with reproduction steps and expected vs actual behavior.
- **Security vulnerabilities:** do **not** open a public issue — follow the [Security Policy](./SECURITY.md).

## Code of Conduct

By participating, you agree to abide by our [Code of Conduct](./CODE_OF_CONDUCT.md).
