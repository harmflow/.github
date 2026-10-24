# Commit Conventions

All harmflow repositories follow [Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/).

## Format

```
<type>(<scope>): <subject>

[body]

[footer]
```

## Types

| Type | Use for |
|---|---|
| `feat` | A new capability or behavior |
| `fix` | A bug fix |
| `docs` | Documentation only — README, `CLAUDE.md`, ADRs, specs, decisions, runbooks |
| `refactor` | A code change that neither fixes a bug nor adds behavior |
| `test` | Adding or correcting tests, with no production change |
| `perf` | A change whose purpose is performance |
| `ci` | CI/CD pipelines (`.github/workflows/`) |
| `chore` | Build, dependencies, tooling, and repository housekeeping |

## Scope

The scope is optional. When present, it names the area the change touches — a module, package, component,
or document family — in lower-case kebab-case. There is no fixed list: reuse the scopes the repository
already uses.

```bash
git log --format=%s | grep -oE '^[a-z]+\([^)]+\)' | sort | uniq -c | sort -rn
```

Scopes in common use across the org:

| Scope | Area |
|---|---|
| `claude` | `CLAUDE.md` and Claude Code configuration |
| `github` | GitHub Actions workflows and repository templates |
| `readme`, `adr`, `spec`, `decisions`, `architecture`, `runbook` | Documents in the private documentation repository |
| `daemon`, `desktop`, `installers` | Components of `harmflow-app` |

## Rules

1. Subject line at most 72 characters, imperative mood ("add", not "added" or "adds"), no trailing period.
2. The body is optional. When present, its bullets explain *why*, not what — the diff shows the what.
3. Wrap the body at 72 columns.
4. Never add the `Co-Authored-By: Claude ...` trailer; remove it if a tool inserts one.
5. Each repository tracks its own issues. Reference an issue in the footer: `Closes #42` when it lives in the same
   repository, the full form `Closes harmflow/harmflow-site#42` when it lives in another. A bare `#42` always resolves
   against the local repository. A commit in a public repository never references a private repository's issue, and
   never cites a private record by ID, link, or path: it describes the reason in plain words.
6. Breaking changes: add `!` after the type or scope, and a `BREAKING CHANGE:` footer that says how to migrate.
7. Pull requests are merged with **Rebase and merge**, so every commit lands on `main` unchanged: each commit in
   a pull request must be a valid Conventional Commit, and the pull request title must itself be a valid subject.
   Never use **Squash and merge** or a merge commit. Fold review fixes into the commits they belong to
   (`git commit --fixup` + `git rebase -i --autosquash`) before merging.

## Examples

```
docs(adr): record harmflow-app as a monorepo for daemon and desktop
docs(decisions): settle failover triggers and continuation
docs(spec): make tasks general-purpose with type-specific parameters
feat(daemon): load task definitions from the YAML directory
fix(desktop): keep the dashboard connected after the daemon restarts
```

With a body:

```
docs: track issues per repository instead of centrally in docs

- harmflow keeps each repository's issues in its own tracker, so docs
  no longer claims to be the platform-wide backlog
- Keep repo:docs on every issue here to flag documentation work
```
