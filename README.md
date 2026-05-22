# Agent Project Setup

Coding agents lose project context when memory lives only in chat history. Agent Project Setup adds a small repo-local working memory system so future agents can resume current work, follow plans, preserve decisions, and keep PR/review status visible.

It does not scaffold application code, install dependencies, configure devcontainers, or choose a tech stack. It prepares the repo for repeated agent work.

## Install

```bash
npx skills add https://github.com/bbssppllvv/agent-project-setup --skill agent-project-setup
```

Restart your agent environment after installing so the new skill is loaded.

## Use

Inside a project repo, ask an agent environment that supports skills:

```text
Use $agent-project-setup to set up this repo for agent-assisted development.
```

The skill inspects the repo first. If it finds existing project instructions, plans, or docs, it reuses them instead of creating a second planning system. If the project goal or PR workflow is unclear, it asks before writing files.

## What It Creates

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

## How Agents Use It

- `AGENTS.md` tells future agents where to start, which commands matter, and how to maintain the setup.
- `.agent/STATE.md` keeps the current handoff short: active plans, blockers, next action, and recent meaningful changes.
- `.agent/DECISIONS.md` records durable decisions so agents do not re-argue them every session.
- `.agent/plans/` holds many plans with clear statuses: `backlog`, `active`, `blocked`, and `archive`.
- Plans stay active while required PR, review, merge, or explicit acceptance is still pending.

## Why It Helps

Use it for repos where agents work across multiple sessions, features, or PRs. It keeps current state and decisions in version-controlled files, while avoiding a large documentation system that will go stale.
