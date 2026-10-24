# CLAUDE.md

> This file provides context and guidance for Claude working in any repository under the **harmflow** GitHub organization.
> Individual repositories may add their own `CLAUDE.md` to override or extend these defaults.

---

## Project Overview

**Name:** harmflow / `.github`

**Purpose:** Holds GitHub org-level defaults — community health files, issue/PR templates, and AI guidance — for the *harmflow* organization. Individual repos override by placing the same file at the same path inside their own repository.

**Owner / Team:** @lpiedade

**Type:** GitHub organization defaults repository (meta-repo, no deployable code)

---

## Repository Structure

```
.github/
├── .github/
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.yml       # Default bug form for repos without their own forms
│       ├── config.yml           # Default issue chooser: no blank issues, security contact link
│       └── feature_request.yml  # Default feature form for repos without their own forms
├── profile/
│   ├── README.md           # Org profile shown at github.com/harmflow
│   └── assets/             # SVG banner and diagram the profile embeds
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

### Validate the issue templates (optional)

```bash
# Requires Node on PATH. Checks YAML syntax only; GitHub validates the schema when it renders the chooser.
for f in .github/ISSUE_TEMPLATE/*.yml; do npx js-yaml "$f"; done
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
| Branch names | `<type>/<short-description>`, `<type>` from [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md) | `feat/task-yaml-loader`, `docs/harmflow-app-monorepo` |

---

## Commit Conventions

The full reference is [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md). A summary follows.

- Conventional Commits: `<type>(<scope>): <subject>`. Types: `feat`, `fix`, `docs`, `refactor`, `test`, `perf`,
  `ci`, `chore`.
- The scope is optional and free-form: the area the change touches, in lower-case kebab-case. Reuse the scopes
  the repository already uses (`claude`, `github`, `adr`, `spec`, `decisions`, …).
- Subject at most **72 characters**, imperative mood ("add", not "added"), no trailing period.
- Body bullets explain *why*, not what — the diff shows the what. Wrap the body at 72 columns.
- Do **not** add the `Co-Authored-By: Claude ...` trailer. If a tool inserts it, remove it before committing.
- Reference issues in the footer: `Closes #42` for an issue in the same repository, the full form
  `Closes harmflow/harmflow-site#42` for one in another repository. A public repository never references a private
  repository's issue, and never cites a private record by ID, link, or path.
- Breaking changes: `!` after the type or scope, plus a `BREAKING CHANGE:` footer.

---

## Pull Request Guidelines

1. Branch off `main` in the repository itself (no forks) using `<type>/<short-description>`.
2. Keep PRs focused — one logical change per PR. The PR title is a valid Conventional Commits subject.
3. Link the issue in the PR body: `Closes #42` in the same repository, `Closes harmflow/<repo>#42` across
   repositories — never a private repository's issue from a public one.
4. All CI checks must pass before merging. On the free plan, branch protection is available on the public
   repositories but not on private ones, where this is enforced by convention only.
5. Merge with **Rebase and merge** to keep `main` linear; never use Squash and merge or create merge commits
   (`gh pr merge --rebase`). Every commit in the PR lands on `main` as-is, so each one must be a valid
   Conventional Commit — fold review fixes into their commits (`--fixup` + `rebase -i --autosquash`) first.

---

## Issue tracker

**Every harmflow repository tracks its own issues.** An issue lives in the repository where its fix lands.

| Repository | Its tracker holds |
|---|---|
| [`harmflow/harmflow-app`](https://github.com/harmflow/harmflow-app/issues) | The daemon, the desktop, the installers, and their tests, in one monorepo. **Public**: anyone can read its issues |
| [`harmflow/harmflow-site`](https://github.com/harmflow/harmflow-site/issues) | The public product website and its build and deployment. **Public**: anyone can read its issues |
| The private documentation repository | Documentation only: a wrong, missing, stale, or contradictory document, labelled `repo:docs` |

### Rules

1. **File the issue where the fix lands.** Always pass `--repo` to `gh`: it infers the current clone when
   `--repo` is omitted, which is wrong whenever you work from another repository.
   `gh issue create --repo harmflow/<repo> ...`.
2. **Move misfiled issues** with `gh issue transfer <number> harmflow/<repo> --repo harmflow/<current>` instead
   of working them where they landed.
3. **Split work that crosses repositories.** A code change that requires a document change (an ADR, an
   architecture update) is one issue in each repository. Two public issues link each other in full form; a private
   issue links the public one, never the reverse.
4. **Cross-reference other public repositories with the full form** `harmflow/harmflow-site#42`. A bare `#42` in a
   commit or PR body resolves against the local repo and will silently point at the wrong thing.
5. **Never cite a private record.** A public issue, PR, commit, or file — code, comments, and test names included —
   never names a specification, ADR, or decision of the private documentation repository by ID, link, or path, and
   never references a private repository's issue, `Closes` lines included. Describe what the work needs in plain
   words; a neutral term such as "the specification" or "a decision" is fine. Traceability runs one way: the private
   documentation links the public issue or PR.
6. **Use the canonical triage labels** in every tracker: `needs-triage`, `needs-info`, `ready-for-agent`,
   `ready-for-human`, `wontfix`. Create them in a new repository before triaging there.

---

## Important Files & Docs

| Resource | Link |
|---|---|
| Code issues | [`harmflow/harmflow-app` issues](https://github.com/harmflow/harmflow-app/issues) |
| Website issues | [`harmflow/harmflow-site` issues](https://github.com/harmflow/harmflow-site/issues) |
| Commit conventions (canonical) | [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md) |
| Contribution guide | [`CONTRIBUTING.md`](CONTRIBUTING.md) |
| Specifications, ADRs, decisions, domain glossary | Private documentation repository — never cited from a public repository by ID, link, or path |
| Repository overview | [`README.md`](README.md) |
| Security reporting | [`SECURITY.md`](SECURITY.md) |

---

## Known Gotchas & Context

- This repo is the **fallback** for the entire org. Changes here affect every repository that has not overridden the file locally — review carefully before merging.
- A file only becomes an org default if no repository defines its own copy. A repo-level `CONTRIBUTING.md` or
  `.github/ISSUE_TEMPLATE/` silently shadows the default here — check before assuming a change reaches a repo.
  The private documentation repository already overrides the issue forms with documentation-only ones.
- Default issue templates are read from `.github/ISSUE_TEMPLATE/` **inside** this repository; an
  `ISSUE_TEMPLATE/` folder at the root is ignored. The folder is inherited as a whole: a repository with any
  form of its own gets none of the defaults, including `config.yml`.
- `config.yml` disables blank issues. Removing the default forms while keeping it leaves every inheriting
  repository with no way to open an issue — and each repository tracks its own.
- Malformed issue template YAML silently breaks the issue creation UI without any visible error.
- `harmflow-app`, `harmflow-site`, and this repository are **public**, history and issues included; the
  documentation repository is private. A public issue that mirrors private work states only what that work needs, in
  plain words, and cites none of the private records by ID, link, or path — unannounced features, internal decisions,
  secrets, and personal identifiers (task-manager project or task IDs, account IDs, personal e-mail addresses) never
  land in a public repository, its `CLAUDE.md` included.
- `profile/README.md` renders on the organization page, outside this repository, so its links and images use
  absolute URLs. Its SVGs load from `raw.githubusercontent.com` on `main`: a new or changed image shows only after it
  is merged. They load as `<img>`, so no scripts or web fonts — system font stacks and CSS animations only, stopped
  under `prefers-reduced-motion`. Their look borrows the desktop's cyberpunk inspiration. The logo in `profile/assets/`
  is the official HarmFlow logo, and `logo.svg` is the avatar's own source: the app's icons are drawn from a static
  master in `harmflow-app`. The banner and the diagram are not the official visual identity, whose palette is still
  open.
- Claude Code reads `CLAUDE.md` only from the working directory upward, never this file from another
  repository. A rule that must bind elsewhere has to be restated in that repository's `CLAUDE.md`.
- `LICENSE` is a proprietary notice — do not alter it. GitHub does not inherit `LICENSE` from this repository,
  so every repository keeps its own copy. The product's eventual license is still open; changing it is a decision in
  the private documentation repository first.

---

## Out of Scope

- Do **not** add service-specific instructions here — each repo should have its own `CLAUDE.md`.
- Do **not** modify `LICENSE`.
- Do **not** change GitHub Actions secrets, branch protection rules, or org-level settings from this file.
- Do **not** commit generated files or secrets.

---

*Last updated: October 24, 2026 by [@lpiedade](https://github.com/lpiedade)*
