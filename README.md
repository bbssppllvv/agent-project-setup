# Agent Project Setup

A Codex skill for setting up lightweight project structure for agent-assisted software development.

## Problem

Coding agents work better when a repo has a small amount of durable local context:

- where the current plan lives;
- what is in progress, blocked, or done;
- which decisions should not be re-litigated;
- what needs verification or code review before work is archived.

Without this, every new session re-discovers the project from scratch. With too much documentation, agents start trusting stale notes. This skill creates a small middle ground: useful planning memory without a documentation swamp.

## What It Creates

Default structure:

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

The skill emphasizes:

- minimal project memory;
- many plans with clear statuses;
- archive flow for completed or obsolete plans;
- PR/review gates before marking plans done;
- stale-doc rules that keep code and tests as source of truth.

## Install

Install the skill with one command:

```bash
npx skills add https://github.com/bbssppllvv/agent-project-setup --skill agent-project-setup
```

Then restart Codex so the new skill is loaded.

If `npx skills add` is unavailable in your Codex build, ask Codex to install it:

```text
Use $skill-installer to install bbssppllvv/agent-project-setup from GitHub.
```

## Use

In Codex:

```text
Use $agent-project-setup to set up an agent-ready project structure for this repo.
```

The skill will inspect the existing repo first, avoid creating parallel planning systems, and ask when the project purpose or PR workflow is unclear.
