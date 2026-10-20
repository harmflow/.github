# Security Policy

## Supported Versions

Only the `main` branch of each repository is supported. Fixes land on `main`; there are no maintained release
branches. If a repository has its own `SECURITY.md`, that policy takes precedence.

## Reporting a Vulnerability

Never report a vulnerability in a public issue, discussion, or pull request.

harmflow's repositories are private, and GitHub's private vulnerability reporting is only available on public
repositories. Report privately through this public repository instead:

1. Open [a new security advisory for `harmflow/.github`](https://github.com/harmflow/.github/security/advisories/new).
2. Name the affected repository in the title.
3. Include enough detail for the maintainer to reproduce and assess the issue.

The advisory is visible only to you and the organization owner,
[@lpiedade](https://github.com/lpiedade).

## What to Include

- Affected repository and commit, branch, or installed build.
- The affected component — daemon, desktop, installer — and the operating system and version.
- The harness and its version (Claude Code, Codex), when the issue involves running a task.
- A description of the vulnerability and its potential impact.
- Steps to reproduce or proof-of-concept details.
- Any known mitigations.
- Whether the vulnerability is being actively exploited or has been publicly disclosed.

Examples of what to report privately: a way to reach the local API without its authorization, a task acting outside
the permissions it was granted, or credentials and tokens exposed in logs or state files.

## Response Expectations

The maintainer acknowledges valid reports as soon as possible, investigates, and coordinates remediation and
disclosure with the reporter. Timelines vary with severity and complexity.
