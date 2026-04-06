---
id: "decisions-index"
title: "Decisions — Index"
type: adr
status: active
version: "1.0.0"
created: "2026-04-06"
author: "nimrod"
owner: "oracle"
tags: [decisions, index, adr]
license: "CC0-1.0"
---

# Decisions — Voluntad Cristalizada

Architectural Decision Records (ADR) of the Narrative Work OS. These records are:
- **Append-only** — never delete
- **Supersedable** — a new ADR can supersede a previous one, but the original remains
- **Permanent** — even cancelled decisions stay for historical record

## Active decisions

| ADR | Decision | Status |
|-----|---------|--------|
| ADR-001 | GitHub as Archive Summa | ✅ Active |
| ADR-002 | Markdown as universal format | ✅ Active |

## How to create an ADR

1. Copy the frontmatter template from any existing ADR
2. Assign the next sequential number
3. Fill context, decision, and consequences
4. Open PR with label `decision`
5. Oracle approves and merges
