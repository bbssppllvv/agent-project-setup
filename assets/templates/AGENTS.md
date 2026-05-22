# Agent Instructions

This file is the canonical repo-level operating guide for coding agents.

If another local memory file conflicts with this file, prefer this file and the current source code.

## Project

Name: {{PROJECT_NAME}}

Purpose:

{{PROJECT_PURPOSE}}

## Start Here

Before non-trivial work:

1. Read `.agent/STATE.md`.
2. Read the relevant plan in `.agent/plans/active/`, if one exists.
3. Check current source files before relying on older notes.

## Project Shape

- App/source:
- Tests:
- Docs:
- Build/config:

## Common Commands

```bash
# TODO: add project-specific commands
```

## Agent Working Rules

- Preserve user and other-agent changes. Inspect dirty worktrees before editing.
- Prefer existing project patterns over new abstractions.
- Keep changes scoped to the task or active plan.
- Verify with the most relevant command or manual check before handing off.
- If verification is blocked, record the blocker and artifact paths if any.
- Ask before pushing, publishing, deleting, migrating data, spending money, or opening a PR when the repo convention is unclear.

## Plan Hygiene

- Plans live in `.agent/plans/`.
- Create new plans in `.agent/plans/backlog/` unless the user clearly wants work started now.
- Move a plan to `.agent/plans/active/` and set `status: active` when starting it.
- Move blocked plans to `.agent/plans/blocked/`, set `status: blocked`, and write the blocker.
- Move finished, abandoned, or superseded plans to `.agent/plans/archive/`.
- Keep the plan folder and frontmatter `status` in sync.
- Keep plans `active` while required PR/code review work is pending.
- Update `.agent/STATE.md` before handing off non-trivial work.

## PR And Review

- Use the repo's existing branch and PR workflow when one exists.
- For non-trivial work, prefer a PR if the change spans multiple files/subsystems or affects user-facing behavior, data, security, billing, releases, or agent/tool behavior.
- If PR expectations are unclear, ask before pushing or opening one.
- Do not mark a plan `done` or archive it until required verification and review/merge/acceptance are complete.

## Documentation Maintenance

- Code and tests are the source of truth. Treat `.agent/*` as working memory, not proof.
- Before relying on a documented implementation claim, verify it against current source.
- Update `.agent/STATE.md` when current focus, blockers, active plan, or next action changes.
- Update `.agent/DECISIONS.md` only for durable decisions between real alternatives.
- Update this file only when commands, repo shape, conventions, or agent operating rules change.
- Do not create new planning/docs systems unless the existing agent setup cannot hold the information cleanly.

## Agent Memory

- Treat agent-managed memory outside the repo as advisory and potentially stale.
- Verify external memory against current source before acting on it.
- Consolidate durable, verified facts into this repo instead of relying on private agent memory.
- Use `.agent/STATE.md` for current work, `.agent/DECISIONS.md` for durable decisions, and `.agent/plans/` for future or in-progress work.

## Stale Docs Policy

If a doc is wrong, fix it in the same change or mark it stale with a dated note. Do not let stale docs remain authoritative.
