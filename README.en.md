# SDD by role · role-based feature specs with Claude Code

*[Українська версія](README.md) — the framework itself (rules, templates, skills) is in Ukrainian.*

A ready-to-clone framework for teams that want to agree on **what** and **why** before writing
code. Each role owns one layer of the spec, and [Claude Code](https://claude.com/claude-code)
interviews people, writes the files and handles git and the tracker (GitLab or GitHub) for
them — product managers and business analysts don't need to know git, and the PM doesn't need
to know the code.

## Layers and roles

| File | Answers | Written by | Approved by |
|---|---|---|---|
| `proposal.md` | **Why** and **what changes** for the business | PM | customer |
| `spec.md` | **What exactly** the user sees and does: rules (EARS), texts, edge cases, acceptance criteria (Given / When / Then) | BA | PM, QA |
| `design.md` | **How**: facts from the code, data, APIs, contracts, settings | developers | BA cross-checks against the spec |
| `SDD/<product>/system/` | **How the system works today** — verified facts from code | developers | — |

The key rule is the **what / how boundary**: anything a customer can't see on screen or check by
hand (tables, APIs, role codes, timeouts, queues) belongs to `design.md`, never to the proposal
or spec. Facts about the existing system are never guessed — they come from the code via a
dedicated developer step.

## Pipeline

1. `/sdd-pm` — PM turns an idea or an issue into `proposal.md` (and can create the issue).
2. `/sdd-code-check` — a developer answers the PM's and BA's questions with facts from the code.
3. `/sdd-ba` — BA writes `spec.md`, walking through an edge-case checklist.
4. Review in a merge/pull request → **Gate 1** (PM merges: ready for development).
5. `/sdd-design` — developers write the solution and contracts → **Gate 2** (full mode only).
6. Code and tests against `spec.md`, acceptance by criteria.

`/sdd-status` shows every feature in progress and who is next. One issue = one folder = one
branch = one merge request; Claude switches branches automatically.

## Getting started

1. **Team admin, once:** clone, push to your own GitLab/GitHub repo and fill in the team
   settings in `CLAUDE.md` — see [docs/customize.md](docs/customize.md).
2. **Each team member:** [docs/setup.md](docs/setup.md), then a 45-minute
   [solo walkthrough](docs/solo-walkthrough.md) playing every role on a training feature.

To use the framework in another language, translate `SDD/` templates, `.claude/skills/` and
`CLAUDE.md` — Claude Code can do it for you.

## License

[MIT](LICENSE)
