# Contributing to blindbet

blindbet is proprietary (see `LICENSE`): contributions come from authorized collaborators only. This guide is the
default workflow for every repository in the `blindbet` organization. A repository may add its own rules in its
`README.md` or `CLAUDE.md`.

## Issues

All issues live in [`blindbet/docs`](https://github.com/blindbet/docs/issues), whichever repository the work
lands in.

- Search existing issues before opening a new one.
- Label the issue with `repo:<name>` for every repository it touches.
- For larger changes, agree on the approach in the issue before writing code.

## Workflow

1. Branch off `main` in the repository itself — there are no forks.
2. Name the branch `<type>/<short-description>`, with a type from [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md):
   `feat/strategy-catalog-endpoint`, `fix/orders-ui-strategy`, `docs/adr-0043-options-scope`,
   `ci/issue-on-failure`.
3. Make one focused change. Add or update tests when behavior changes.
4. Run the repository's documented checks locally (see its `README.md` or `CLAUDE.md`).
5. Open a pull request in the same repository and link its issue with the full form:
   `Closes blindbet/docs#<number>`.

## Commits

Follow [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md): Conventional Commits, an imperative subject of at most
72 characters, a body that explains *why*, and no `Co-Authored-By: Claude ...` trailer.

## Pull Requests

Pull requests should be small enough to review comfortably. The title is itself a valid commit subject, and the
description includes:

- A summary of what changed and why.
- How the change was tested.
- Screenshots or recordings for user-facing UI changes.
- Any follow-up work or known limitations.

## Reviews and Merging

- Every CI check must be green before merging. Branch protection is unavailable for private repositories on the
  free plan, so this is enforced by convention, not by GitHub.
- Merge with a merge commit (GitHub's default button); do not squash or rebase.
- A pull request may be closed if it is inactive, out of scope, or superseded by another approach.

## Coding Conventions

- Follow the style, architecture, and tooling already present in the repository.
- Prefer clear names and simple control flow.
- Keep unrelated refactors out of feature and bug-fix pull requests.
- Document behavior that is non-obvious or important for maintainers.
- Do not commit secrets, private keys, credentials, or generated local configuration.
