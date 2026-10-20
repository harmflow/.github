# Commit Conventions

All blindbet repositories follow [Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/).

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
| `docs` | Documentation only — README, `CLAUDE.md`, ADRs, specs, runbooks |
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
| `adr`, `spec`, `runbook` | Records in `blindbet/docs` |
| `db` | Schemas and migrations |
| `web`, `bff` | `control-plane-ui` packages |

## Rules

1. Subject line at most 72 characters, imperative mood ("add", not "added" or "adds"), no trailing period.
2. The body is optional. When present, its bullets explain *why*, not what — the diff shows the what.
3. Wrap the body at 72 columns.
4. Never add the `Co-Authored-By: Claude ...` trailer; remove it if a tool inserts one.
5. All issues live in [`blindbet/docs`](https://github.com/blindbet/docs/issues). Reference them in the footer
   by full form — `Closes blindbet/docs#42`. A bare `#42` resolves against the local repository.
6. Breaking changes: add `!` after the type or scope, and a `BREAKING CHANGE:` footer that says how to migrate.
7. Merge commits created by GitHub (`Merge pull request #N ...`) are exempt; the pull request title must itself
   be a valid subject.

## Examples

```
ci(github): open a tracking issue when CI breaks on main
docs(adr): propose ADR-0043 listed options scope from Stage 3
feat(dashboard): wire StrategyPnlPanel to live per-strategy P&L
fix(qarp-ibov): correct IBOV constituent list to official B3 composition
chore(claude): enable graphify native RAG integration
```

With a body:

```
docs(claude): fix title, Java setup, and service commands

- The file was titled trading-engine and had no overview of this
  service
- make restart-risk and scripts/restart.sh do not exist; point at
  scripts/run.sh and infra's services.sh instead
```
