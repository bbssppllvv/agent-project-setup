---
name: agent-project-setup
description: >
  Create or maintain a lightweight agent-ready project setup for new or
  existing software projects: AGENTS.md, current project state, durable
  decisions, and a multi-plan system with active, backlog, blocked, and
  archived plans. Use when starting a new project, organizing an existing repo
  for coding agents, creating local planning structure, or
  cleaning up stale agent memory and plans.
---

# Agent Project Setup

## Purpose

Use this skill to make a repository easier for coding agents to work in without creating a documentation swamp.

The default setup is intentionally small:

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

Plans can be many. Project memory should stay small.

## Core Rules

- Prefer the existing repo conventions over this template when they are already clear and maintained.
- Do not duplicate the same fact across files. Link instead.
- Treat code, tests, package manifests, and current source files as source of truth. Agent setup files are working memory, not proof.
- Before relying on an implementation claim in an agent setup file, verify it against current files.
- Treat agent-managed memory outside the repo as advisory and potentially stale.
- Create the minimal core first. Add optional folders only when there is real pressure.
- Never overwrite existing `AGENTS.md`, plan files, or decision logs without reading them first.

## Startup Workflow

1. Find the repo root and inspect the current project:
   - `AGENTS.md`, `CLAUDE.md`, `.agent/`
   - `README*`, `docs/`, package/build files
   - existing plan, roadmap, decision, or status files
2. If the project purpose is unclear after inspection, ask a short question before writing files.
3. If no agent project setup exists, create the default structure from the templates in `assets/templates/`.
   - Copy `assets/templates/AGENTS.md` to `AGENTS.md`.
   - Copy `assets/templates/STATE.md` to `.agent/STATE.md`.
   - Copy `assets/templates/DECISIONS.md` to `.agent/DECISIONS.md`.
   - Copy `assets/templates/PLAN.md` to `.agent/plans/TEMPLATE.md`.
   - Create `.agent/plans/{active,backlog,blocked,archive}/`.
4. If an agent project setup exists, update it in place. Do not create parallel systems.
5. If the repo already has `docs/plans`, `docs/decisions`, or similar, either adopt that location or add a short pointer from `.agent/STATE.md`; avoid competing plan roots.

## File Responsibilities

### `AGENTS.md`

Repo-level operating instructions loaded by agents. Keep it short, typically 100-150 lines max.

Include:
- what the project is;
- where to read current state and plans;
- common build/test/dev commands if known;
- plan hygiene and maintenance rules;
- stale-doc policy.

Do not include:
- long architecture essays;
- full roadmaps;
- detailed historical decision records;
- content duplicated from `README.md` or package manifests.

If a project needs Claude Code compatibility, create `CLAUDE.md` only as a redirect:

```markdown
# Claude Code Instructions

Use [`AGENTS.md`](AGENTS.md) as the canonical repo-level instructions.
```

### `.agent/STATE.md`

The current operational state. Update it before handing off any non-trivial work.

Use it for:
- current focus;
- active plan links;
- next action;
- blockers;
- recent meaningful changes.

Keep it short. It should tell the next agent where to look, not retell the whole project.

Use the lightweight template. Do not turn `STATE.md` into a changelog or roadmap.

### `.agent/DECISIONS.md`

Durable decisions that should not be re-litigated every session.

Add an entry only when the work chose between real alternatives, such as:
- framework, database, provider, or package choice;
- architecture boundary;
- data model or API contract;
- workflow, release, or verification policy.

Do not record every task completion here. Link to archived plans when useful.

Use the lightweight entry format. Do not create separate ADR files unless the repo already uses ADRs or a decision needs more detail than a short entry can hold.

### `.agent/plans/`

The plan system is the main working area.

Directories:
- `backlog/` - future plans and shaped ideas.
- `active/` - plans currently ready to execute.
- `blocked/` - plans waiting on a decision or dependency.
- `archive/` - completed, abandoned, or superseded plans.

The folder and frontmatter status must agree.

Allowed statuses:
- `draft` - rough idea, not ready.
- `backlog` - ready future work.
- `active` - currently executable, including implementation and PR/review follow-through.
- `blocked` - cannot proceed without something.
- `done` - completed and verified.
- `superseded` - replaced by another plan.
- `abandoned` - deliberately closed without implementation.

## Plan Quality Bar

A good plan should be short but decision-ready. Include:

- the user-visible or engineering outcome, not just the implementation idea;
- a stable North Star describing the ideal product/user state if the plan succeeds;
- a user/operator story for who benefits and what they can do;
- non-goals that prevent scope creep;
- acceptance criteria that state what must be true when the work is done;
- references to current code/docs/plans that matter;
- concrete steps that can be checked off;
- verification commands or manual checks for proving the acceptance criteria;
- risk and rollback notes for non-trivial changes;
- PR/review expectations when the repo uses branches or reviews.

Do not write speculative architecture documents disguised as plans. If the next agent cannot start implementation or make a clear decision from the plan, sharpen the plan or mark it `draft`.

The North Star is not an implementation summary. Write it in product/user terms: what gets better, what the user can now do, what becomes simpler, safer, faster, clearer, or more reliable. Technical details can change during implementation; the North Star should still tell the agent what outcome to protect.

The user/operator story should stay lightweight. For user-facing work, use "As a [user], I want [capability], so that [outcome]." For internal tools, infrastructure, or agent workflow changes, write the operator/agent equivalent. If there is truly no user or operator behavior, write `N/A` and explain why.

## Plan Hygiene

When creating a plan:
- put it in `backlog/` unless the user clearly wants it started now;
- check existing active/backlog/blocked plans for overlap;
- make scope and non-goals explicit;
- include verification before code is written.

When starting a plan:
- move it to `active/`;
- set `status: active`;
- update `.agent/STATE.md`.

When blocked:
- move it to `blocked/`;
- set `status: blocked`;
- write the blocker and what would unblock it;
- update `.agent/STATE.md`.

When finished:
- write verification notes;
- if a PR or code review is required, keep the plan `active` until the PR is opened and review/merge/acceptance is complete;
- set `status: done` only after required verification and review gates are satisfied;
- move it to `archive/`, normally as `.agent/plans/archive/YYYY-MM-DD-<slug>.md`;
- update `.agent/STATE.md`;
- add to `.agent/DECISIONS.md` only if a durable decision was made.

When obsolete:
- set `status: superseded` or `abandoned`;
- explain why;
- link to the replacement if any;
- move it to `archive/`.

## PR And Review Workflow

Do not force a PR workflow onto every repo. Use the project's established practice.

For small local-only tasks, it may be enough to edit, verify, and update the plan.

For non-trivial changes, prefer a branch/PR when:
- the repo already uses PRs;
- the plan says PR is required;
- the change spans multiple files or subsystems;
- the change affects user-facing behavior, data, security, billing, releases, or agent/tool behavior.

Before pushing or opening a PR, ask the user when:
- the repo has no clear PR convention;
- credentials/remotes are unclear;
- the worktree contains unrelated user changes that affect the PR;
- the change is risky and the user has not asked for implementation yet.

When a PR is required:
- keep the plan in `active/` while review is pending;
- record branch/PR link or number in the plan;
- write the PR summary/test plan from the plan's acceptance criteria and verification notes, not from memory;
- address review feedback in the same plan;
- archive the plan only after review is complete, merged, or explicitly accepted by the user.

## When To Ask Instead Of Guessing

Ask a concise question when:
- the project purpose or first useful outcome is unclear;
- there are multiple plausible agent setup locations and adopting the wrong one would create a parallel system;
- a plan requires a product/architecture decision the current docs do not settle;
- the next action would push, publish, delete, migrate, spend money, or contact external systems;
- review or PR expectations are unclear and the task is not obviously local-only.

## Maintenance Checklist

Before the final response after non-trivial work, check whether to update:

- `.agent/STATE.md` - almost always.
- `.agent/plans/...` - if status, scope, progress, risks, or verification changed.
- `.agent/DECISIONS.md` - if a durable decision was made.
- `AGENTS.md` - only if commands, repo structure, conventions, or agent operating rules changed.

If an agent setup file is wrong, fix it in the same change or mark it stale. Stale-but-authoritative docs are worse than missing docs.

## Agent Memory Consolidation

Many agents keep their own memory outside the repo. Treat that memory as a cache, not as authority.

When visible or referenced:

- use external agent memory only as a lead;
- verify implementation claims against current source before acting;
- do not copy stale or private agent memory into the repo;
- consolidate only durable, verified project facts into the repo setup.

Where to consolidate:

- current work, blockers, and next action -> `.agent/STATE.md`;
- durable decisions and rationale -> `.agent/DECISIONS.md`;
- future or in-progress work -> `.agent/plans/...`;
- agent operating rules, commands, or repo shape -> `AGENTS.md`.

If memory conflicts with current code, prefer current code and update or ignore the memory. If the conflict matters for future agents, record the corrected fact in the appropriate repo file.

## Optional Extensions

Add these only when needed:

```text
.agent/research/          # substantial research notes with source links
.agent/handoffs/          # long multi-session handoffs
.agent/context/           # split out stable context when AGENTS.md is too long
docs/initiatives/<slug>/  # large multi-PR product initiative
scripts/agent/verify.sh   # repeatable local verification command
```

Use `docs/initiatives/<slug>/` only for work that spans many PRs or phases. Otherwise prefer normal `.agent/plans/`.

## Template Use

Templates live in `assets/templates/`:

- `AGENTS.md`
- `STATE.md`
- `DECISIONS.md`
- `PLAN.md`

Copy them, fill placeholders, and delete irrelevant sections. Keep project-specific content concise.
