<p align="center">
  <img src="https://raw.githubusercontent.com/harmflow/.github/main/profile/assets/banner.svg"
       alt="HarmFlow — local-first automation manager for AI coding agents" width="100%">
</p>

<p align="center">
  <img alt="Status: in development"
       src="https://img.shields.io/badge/status-in%20development-f59e0b?style=flat-square&labelColor=0b1020">
  <img alt="Built for macOS, Linux, and Windows"
       src="https://img.shields.io/badge/built%20for-macOS%20%C2%B7%20Linux%20%C2%B7%20Windows-22d3ee?style=flat-square&labelColor=0b1020">
  <img alt="Harnesses: Claude Code and Codex"
       src="https://img.shields.io/badge/harnesses-Claude%20Code%20%C2%B7%20Codex-8b5cf6?style=flat-square&labelColor=0b1020">
</p>

<p align="center">
  <b>Schedule, run, and monitor the AI coding agents already on your machine.</b><br>
  HarmFlow is an orchestration and desktop layer over the harnesses you use — Claude Code and OpenAI Codex first.<br>
  Not a new model, and not a replacement for them.
</p>

> [!NOTE]
> HarmFlow is in early development and nothing is released yet. Watch
> [`harmflow-app`](https://github.com/harmflow/harmflow-app) to follow along.

## Why HarmFlow

Agent harnesses can already implement an issue or fix a failing test. Running them **every night, across several
repositories, without babysitting** usually takes cron jobs, home-made scripts, and terminals checked by hand.
HarmFlow turns that into one product: define a task once, let it run on your own computer, and follow every result.

## How it is designed to work

<p align="center">
  <img src="https://raw.githubusercontent.com/harmflow/.github/main/profile/assets/flow.svg"
       alt="A task file goes to the daemon, which schedules it and starts Claude Code or Codex within the task's
            permissions. The result is a draft pull request that you review and merge; unfinished work resumes from
            checkpoints. The desktop dashboard talks to the daemon through a local API." width="100%">
</p>

## Principles

<table>
  <tr>
    <td width="33%" valign="top">
      <code>01</code> <b>Local-first</b><br>
      Runs on your computer, with the harnesses you already installed and signed in to. The daemon keeps working
      when the dashboard is closed.
    </td>
    <td width="33%" valign="top">
      <code>02</code> <b>Bring your own agent</b><br>
      Claude Code and Codex first, each behind an adapter. When one runs out of quota, a task can continue on the
      next.
    </td>
    <td width="33%" valign="top">
      <code>03</code> <b>Plain YAML</b><br>
      Every task is a file you can read, diff, and keep in Git — and edit from the desktop app as well.
    </td>
  </tr>
  <tr>
    <td width="33%" valign="top">
      <code>04</code> <b>Observable</b><br>
      Live and past executions, with their events, raw output, changed files, and commands.
    </td>
    <td width="33%" valign="top">
      <code>05</code> <b>Governed</b><br>
      Each task carries its own file, command, and network permissions, and the agent works inside them.
    </td>
    <td width="33%" valign="top">
      <code>06</code> <b>You merge</b><br>
      Code tasks end in a draft pull request — even when tests fail, with the failures written down. HarmFlow
      never merges.
    </td>
  </tr>
</table>

## A task is a file

```yaml
# A sketch of the idea; the task schema is not final.
apiVersion: harmflow/v1alpha1
name: nightly-issues
type: github-issue-implementation   # the first task type
schedule: "0 2 * * 1-5"             # weeknights at 02:00
missedRun: run-on-resume            # laptop asleep at 02:00? run when it wakes
harness:
  primary: claude-code
  fallback: [codex]                 # quota exhausted → continue on Codex
params:
  repositories: [acme/api, acme/web]
  labels: [ready-for-agent]
```

Implementing GitHub issues is the first task type. The task model itself is general-purpose: other recurring agent
work fits it with different parameters.

## Repositories

| Repository | What lives there |
|---|---|
| [`harmflow-app`](https://github.com/harmflow/harmflow-app) | The daemon, the desktop app, and the installers, in one monorepo |
| [`harmflow-site`](https://github.com/harmflow/harmflow-site) | The product website |
| [`.github`](https://github.com/harmflow/.github) | Organization defaults: contribution guide, issue forms, security policy |

## Get involved

- **Follow along** — watch [`harmflow-app`](https://github.com/harmflow/harmflow-app) for progress.
- **Ask or suggest** — open an issue in the repository it concerns;
  [Support](https://github.com/harmflow/.github/blob/main/SUPPORT.md) says which one.
- **Report a vulnerability** — privately, never in a public issue; see the
  [security policy](https://github.com/harmflow/.github/blob/main/SECURITY.md).
- **Contribute code** — pull requests are open to authorized collaborators only for now; see the
  [contribution guide](https://github.com/harmflow/.github/blob/main/CONTRIBUTING.md).

Everyone taking part follows the [Code of Conduct](https://github.com/harmflow/.github/blob/main/CODE_OF_CONDUCT.md).

<p align="center"><sub>Automate the repetitive. Amplify what matters.</sub></p>
