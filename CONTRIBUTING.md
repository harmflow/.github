# Contributing to harmflow

This guide is the default workflow for every repository in the `harmflow` organization. A repository may add its own
rules in its `README.md` or `CLAUDE.md`.

## Who can contribute

harmflow intends to accept outside contributions while reserving commercial exploitation to its owner (`D-055` in
`harmflow/harmflow-docs`). The license and contributor agreement that make this possible are not published yet
([`decisions/licensing-and-contributions.md`](https://github.com/harmflow/harmflow-docs/blob/main/decisions/licensing-and-contributions.md)
in `harmflow/harmflow-docs`). Until they are, every repository is proprietary (see its `LICENSE`) and contributions come from
authorized collaborators only; pull requests from anyone else are not accepted yet.

## Issues

Each repository tracks its own issues. File an issue in the repository where the fix lands: `harmflow-app` for the
daemon, the desktop, the installers, and their tests; `harmflow-docs` for documentation; `harmflow-site` for the
public product website. `harmflow-app` and `harmflow-site` are public, so their issues never restate private work —
link it instead.

- Search existing issues before opening a new one.
- When the work also needs a change in another repository, open an issue there too and link the two in full form
  (`harmflow/harmflow-docs#42`).
- For larger changes, agree on the approach in the issue before writing code.

## Workflow

1. Branch off `main` in the repository itself — there are no forks.
2. Name the branch `<type>/<short-description>`, with a type from [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md):
   `feat/task-yaml-loader`, `fix/dashboard-reconnect`, `docs/harmflow-app-monorepo`, `ci/build-matrix`.
3. Make one focused change. Add or update tests when behavior changes.
4. Run the repository's documented checks locally (see its `README.md` or `CLAUDE.md`).
5. Open a pull request in the same repository and link its issue: `Closes #<number>` in the same repository,
   `Closes harmflow/<repo>#<number>` across repositories.

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

- Every CI check must be green before merging. On the free plan, branch protection is available on the public
  repositories but not on the private `harmflow-docs`, where this is enforced by convention only.
- Merge with **Rebase and merge** to keep `main` linear; never use Squash and merge or create merge commits.
  Every commit in the pull request lands on `main`, so each one must follow
  [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md). Fold review fixes into the commits they belong to before merging.
- A pull request may be closed if it is inactive, out of scope, or superseded by another approach.

## Coding Conventions

- Follow the style, architecture, and tooling already present in the repository.
- Use the domain terms of [`CONTEXT.md`](https://github.com/harmflow/harmflow-docs/blob/main/CONTEXT.md) in `harmflow/harmflow-docs`
  for names in code, issues, and documents.
- Prefer clear names and simple control flow.
- Keep unrelated refactors out of feature and bug-fix pull requests.
- Document behavior that is non-obvious or important for maintainers.
- Do not commit secrets, private keys, credentials, or generated local configuration.
