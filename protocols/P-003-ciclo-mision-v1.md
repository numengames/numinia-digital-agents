---
id: "P-003"
title: "Mission Cycle Protocol"
type: protocol
status: active
version: "1.1.0"
created: "2026-04-06T00:00:00Z"
updated: "2026-04-07T18:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [protocol, missions, cycle]
applies_to: [all-agents]
mandatory: true
license: "CC0-1.0"
---
# P-003 — Mission Cycle Protocol v1

> **Summary:** Standard operational protocol for the NWOS system.
> **Epistemic:** How this process is executed and why in this way.
> **Pragmatic:** Follow these steps in the specified context.
> **Audience:** Agents

---

## Mission states

```
backlog/ → active/ → done/
              ↓
           blocked (stays in active/ with status: blocked)
              ↓
           cancelled (moves to done/ with status: cancelled)
```

## Creating a mission (Oracle or Procyon)

1. Use TEMPLATE.md — PRs rejected without correct format
2. Fill all required frontmatter fields
3. **Before assigning an ID: list `missions/active/` and `missions/backlog/` to verify the next available number**
4. Set `phase: backlog`
5. Create in `missions/backlog/{mission-id}.md`
6. Commit and open PR to main

## Activating a mission (Oracle or Procyon)

1. Move file from `backlog/` to `active/`
2. Set `phase: active`
3. Set `executor: {agent-id}` — only ONE executor
4. Set `started: {YYYY-MM-DD}`
5. Commit and merge

## Executing a mission (Executor agent)

1. Read the mission completely
2. Verify there are no contradictions with canon/ (if there are, escalate via P-005)
3. Execute
4. Document progress in the mission file
5. If the plan changes, document in `divergence_log`

## Completing a mission (Executor agent)

1. Verify ALL acceptance criteria are met
2. Fill `execution_log` with what was done
3. Fill `divergence_log` if the execution diverged from the plan
4. Set `phase: done`, `completed: {YYYY-MM-DD}`
5. Move file from `active/` to `done/`
6. Commit and open PR to main
7. Oracle reviews and merges — `done/` is immutable

## Blocking a mission

1. Set `status: blocked`
2. Fill `blocked_reason` with the exact blocker
3. Notify Procyon or Oracle
4. Do not abandon — the mission stays in active/ until resolved

## Critical rules

- `done/` files are immutable once merged
- Only the executor edits an active mission (SIM-2.13)
- `divergence_log` is mandatory when execution deviated (P-10)
- A cancelled mission goes to `done/` — NEVER deleted (SIM-2.7)
- **Never assign a mission ID without verifying the repo first** — git pull syncs files, not your local memory

---

## Version history

- v1.0.0 (2026-04-06) — Initial creation.
- v1.1.0 (2026-04-07) — Added ID verification rule. Translated to English (MIS-056).

*Next review: 2026-07-06*
