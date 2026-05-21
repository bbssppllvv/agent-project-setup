# Agent Project Setup

Stop re-explaining your repo to every coding agent.

Agent Project Setup is a Codex skill that creates a small working memory for software projects: current state, plans, decisions, and review rules. It is built for repos where agents write code over many sessions and need to continue work without guessing what happened last time.

## Why This Exists

Coding agents lose time in two predictable ways:

- They rediscover the same project context every session.
- They trust old notes that no longer match the code.

This skill sets up a middle path. It gives agents enough local structure to plan, continue, verify, and archive work, while keeping code and tests as the source of truth.

## What It Adds

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

Each file has a job:

- `AGENTS.md` tells agents how to work in the repo.
- `.agent/STATE.md` says what is happening now.
- `.agent/DECISIONS.md` records durable decisions worth remembering.
- `.agent/plans/` keeps many plans sorted by status.

Plans stay active until implementation, verification, and required PR/code review are complete. Finished, abandoned, or superseded plans move to `archive/`.

## What It Avoids

This skill does not create a large docs system by default.

No default research folder.  
No default roadmap package.  
No separate plan board to keep in sync.

Optional folders are added only when the project actually needs them.

## Install

```bash
npx skills add https://github.com/bbssppllvv/agent-project-setup --skill agent-project-setup
```

Restart Codex after installing.

## Use

In a project repo, ask Codex:

```text
Use $agent-project-setup to set up this repo for agent-assisted development.
```

The skill will inspect the repo first. If it finds an existing planning system, it will reuse or point to it instead of creating a competing one. If the project goal or PR workflow is unclear, it will ask before writing structure.

## Best For

- new product repos;
- side projects that will be built over many agent sessions;
- existing repos where plans and decisions are scattered;
- teams that want agents to update plans, wait for review, and archive finished work.
