# Agent Project Setup

An agent skill that prepares a repo for long-running agent-assisted development.

It gives agents a simple local system for project state, plans, decisions, verification, and PR/review follow-through, so each new session can continue from the last one instead of starting from scratch.

## Install

```bash
npx skills add https://github.com/bbssppllvv/agent-project-setup --skill agent-project-setup
```

Restart your agent environment after installing so the new skill is loaded.

## Use

Run this inside a project repo:

```text
Use $agent-project-setup to set up this repo for agent-assisted development.
```

The skill inspects the repo first. If it finds existing project instructions, plans, or docs, it reuses them instead of creating a second planning system. If the project goal or PR workflow is unclear, it asks before writing files.

## The Problem

Agent work breaks down when project memory lives only in chat history.

A new session often has to rediscover:

- what the project is;
- what is being built next;
- which plans are active, blocked, or finished;
- what decisions were already made;
- which checks must pass before work is considered done;
- whether a change needs a branch, PR, review, or user approval.

Without local structure, agents repeat planning work, miss old decisions, leave half-finished plans around, or archive work before review is complete.

Agent Project Setup fixes that by putting the working memory in the repo.

## What Gets Created

```text
AGENTS.md
.agent/
  STATE.md
  DECISIONS.md
  plans/
    TEMPLATE.md
    active/
    backlog/
    blocked/
    archive/
```

## How It Works

`AGENTS.md` tells future agents how to work in the repo: where to start, what commands matter, how plans move, and when to ask before risky actions.

`.agent/STATE.md` is the handoff file. It records the current focus, active plans, blockers, next action, and recent meaningful changes.

`.agent/DECISIONS.md` stores durable decisions that should not be re-argued every session: architecture choices, providers, data model decisions, workflow rules, and similar project commitments.

`.agent/plans/` is the planning system:

- `backlog/` for future plans and shaped ideas;
- `active/` for work that is ready or in progress;
- `blocked/` for plans waiting on a decision or dependency;
- `archive/` for plans that are done, abandoned, or superseded.

Plans include goal, context, non-goals, scope, steps, verification, risks, rollback notes, and PR/review status.

## Plan Lifecycle

1. New plans start in `backlog/` unless work should begin immediately.
2. When work starts, the plan moves to `active/`.
3. If progress is blocked, it moves to `blocked/` with the blocker written down.
4. If a PR or code review is required, the plan stays `active` until review, merge, or explicit acceptance is complete.
5. Finished, abandoned, or superseded plans move to `archive/`.

This keeps old plans from pretending to be current work.

## What This Is Good For

Use it when:

- starting a new project with coding agents;
- turning an existing repo into something agents can work in repeatedly;
- planning several features ahead;
- keeping agent work reviewable through PRs;
- preventing stale notes from becoming fake source of truth;
- preserving decisions without writing a large documentation system.

The default setup is intentionally small. It adds the files agents need to continue work, and avoids creating extra docs until the project actually needs them.
