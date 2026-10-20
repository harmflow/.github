# CLAUDE.md

> This file provides context and guidance for Claude working in any repository under the **blindbet** GitHub organization.
> Individual repositories may add their own `CLAUDE.md` to override or extend these defaults.

---

## Project Overview

**Name:** blindbet / `.github`

**Purpose:** Holds GitHub org-level defaults — community health files, issue/PR templates, and AI guidance — for the *blindbet* organization. Individual repos override by placing the same file at the same path inside their own repository.

**Owner / Team:** @lpiedade

**Type:** GitHub organization defaults repository (meta-repo, no deployable code)

---

## Repository Structure

```
.github/
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── config.yml      # Org-wide issue chooser: points every repo at blindbet/docs
├── profile/                # GitHub org profile README
├── CLAUDE.md               # ← you are here (org-level AI guidance)
├── CODE_OF_CONDUCT.md
├── COMMIT_CONVENTION.md    # Canonical commit type/scope reference
├── CONTRIBUTING.md
├── LICENSE
├── PULL_REQUEST_TEMPLATE.md
├── README.md
├── SECURITY.md
└── SUPPORT.md
```

---

## Getting Started

### Prerequisites

```bash
git  # that's all — no build or install step
```

### Validate the issue template config (optional)

```bash
# Requires Node on PATH. Checks YAML syntax only; GitHub validates the schema when it renders the chooser.
npx js-yaml .github/ISSUE_TEMPLATE/config.yml
```

---

## Code Style & Conventions

### General

- **Language**: All documentation must be written in **en-US**.
- **Formatting**: CommonMark Markdown; keep lines under 120 characters where practical.
- **YAML**: Issue template files must follow GitHub's issue template schema — validate before committing.

### Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Markdown files | UPPER_SNAKE_CASE | `COMMIT_CONVENTION.md` |
| Issue templates | snake_case | `bug_report.yml` |
| Branch names | `<type>/<short-description>`, `<type>` from [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md) | `feat/strategy-catalog-endpoint`, `ci/issue-on-failure` |

---

## Commit Conventions

The full reference is [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md). A summary follows.

- Conventional Commits: `<type>(<scope>): <subject>`. Types: `feat`, `fix`, `docs`, `refactor`, `test`, `perf`,
  `ci`, `chore`.
- The scope is optional and free-form: the area the change touches, in lower-case kebab-case. Reuse the scopes
  the repository already uses (`claude`, `github`, `adr`, `db`, …).
- Subject at most **72 characters**, imperative mood ("add", not "added"), no trailing period.
- Body bullets explain *why*, not what — the diff shows the what. Wrap the body at 72 columns.
- Do **not** add the `Co-Authored-By: Claude ...` trailer. If a tool inserts it, remove it before committing.
- Reference issues by full form in the footer: `Closes blindbet/docs#42`.
- Breaking changes: `!` after the type or scope, plus a `BREAKING CHANGE:` footer.

---

## Pull Request Guidelines

1. Branch off `main` in the repository itself (no forks) using `<type>/<short-description>`.
2. Keep PRs focused — one logical change per PR. The PR title is a valid Conventional Commits subject.
3. Link the issue in the PR body with the full form: `Closes blindbet/docs#42`.
4. All CI checks must pass before merging. Branch protection is unavailable for private repositories on the
   free plan, so this is enforced by convention, not by GitHub.
5. Merge with a merge commit (GitHub's default `Merge pull request #N` button); do not squash or rebase.

---

## Issue tracker

**All issues for the blindbet platform live in [`blindbet/docs`](https://github.com/blindbet/docs/issues).**
No other repository in the org keeps its own issue backlog.

### Why one repo

blindbet is a multi-repo platform: many repositories, one system. A per-repo tracker splits the backlog
across one board per repository, so nobody can answer "what is open right now" without visiting all of
them, and work that spans services (most of it) has no natural home. Centralizing in `docs` buys a single
prioritizable queue, one place where specs and ADRs sit next to the issues that implement them, and
cross-service dependencies that GitHub can express natively instead of as prose.

`docs` is the right host because it already carries the specs (`spec/`), the decisions (`adr/`), and the
`ready-for-agent` triage flow the issues are graded against.

### Rules

1. **Create every issue in `docs`**, from any repo: `gh issue create --repo blindbet/docs ...`.
   `gh` infers the current clone when `--repo` is omitted, so pass it explicitly, always.
2. **Label the affected service** with `repo:<name>`. This is what keeps the central backlog filterable per
   service — it replaces the repo boundary you gave up. Cross-cutting work carries one label per touched
   service.
3. **Pull requests stay in their own repo.** Only issues are centralized; a PR belongs where the code is.
4. **Cross-reference with the full form** `blindbet/docs#42`. A bare `#42` in a commit or PR body resolves
   against the local repo and will silently point at the wrong thing.
5. **Never enable or reopen a per-repo backlog.** If you find issues in a service repo, migrate the open ones
   to `docs` and close the originals with a pointer comment.

### Known exception: CI failure issues

Service repos whose `.github/workflows/ci.yml` opens a `ci-failure` issue when `build & test` breaks on
`main` still file it in the service repo: the workflow authenticates with the built-in `GITHUB_TOKEN`,
which is scoped to its own repository and cannot create issues elsewhere.

Redirecting them to `docs` requires an org-scoped PAT stored as an org secret. Until that secret exists, leave
the workflows alone — pointing them at `docs` without it makes CI fail on the failure handler itself.

---

## Important Files & Docs

| Resource | Link |
|---|---|
| Issue backlog (all repos) | [`blindbet/docs` issues](https://github.com/blindbet/docs/issues) |
| Commit conventions (canonical) | [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md) |
| Contribution guide | [`CONTRIBUTING.md`](CONTRIBUTING.md) |
| Contribution workflow decision | [`blindbet/docs` → `decisions/`](https://github.com/blindbet/docs/tree/main/decisions) |
| ADRs | [`blindbet/docs` → `adr/`](https://github.com/blindbet/docs/tree/main/adr) |
| Repository overview | [`README.md`](README.md) |
| Security reporting | [`SECURITY.md`](SECURITY.md) |

---

## Known Gotchas & Context

- This repo is the **fallback** for the entire org. Changes here affect every repository that has not overridden the file locally — review carefully before merging.
- A file only becomes an org default if no repository defines its own copy. A repo-level `CONTRIBUTING.md` or
  `.github/ISSUE_TEMPLATE/` silently shadows the default here — check before assuming a change reaches a repo.
- Default issue templates are read from `.github/ISSUE_TEMPLATE/` **inside** this repository; an
  `ISSUE_TEMPLATE/` folder at the root is ignored. The issue forms themselves live in `blindbet/docs`, the only
  repository that accepts issues.
- Malformed issue template YAML silently breaks the issue creation UI without any visible error.
- Claude Code reads `CLAUDE.md` only from the working directory upward, never this file from another
  repository. A rule that must bind elsewhere has to be restated in that repository's `CLAUDE.md`.
- `LICENSE` is a proprietary notice — do not alter it. GitHub does not inherit `LICENSE` from this repository,
  so every repository keeps its own copy.

---

## Out of Scope

- Do **not** add service-specific instructions here — each repo should have its own `CLAUDE.md`.
- Do **not** modify `LICENSE`.
- Do **not** change GitHub Actions secrets, branch protection rules, or org-level settings from this file.
- Do **not** commit generated files or secrets.

---

*Last updated: October 13, 2026 by [@lpiedade](https://github.com/lpiedade)*
