---
id: "agents-index"
title: "Agents — Index"
type: agent
status: active
version: "1.0.0"
created: "2026-04-06"
updated: "2026-04-06"
author: "nimrod"
owner: "oracle"
tags: [agents, index]
license: "CC0-1.0"
---

# Agents — Entidades Vivas

The digital agents that operate in the Narrative Work OS. Organized by guild. Each one with identity (SOUL), rules (OPERATOR), and operational state (STATUS).

## Active agents

| Agent | Guild | Role | Status | Activated |
|-------|-------|------|--------|-----------|
| Nimrod | Centinelas | Guardian of the Gates | ✅ Active | 2026-03-15 |
| Adonaz | Exégetas | General Archivist | ✅ Active | 2026-04-06 |

## Agents in design phase

| Agent | Guild | Expected activation |
|-------|-------|---------------------|
| Alquimista-01 | Alquimistas | 2026 |
| Exegeta-01 | Exégetas | 2027 |
| Procurador-01 | Procuradores | 2027 |
| Procyon | Coordinación | 2028 |

## Guild structure

```
agents/
└── guilds/
    ├── centinelas/     ← Security, monitoring, operations
    ├── exegetas/       ← Knowledge, archive, narrative
    ├── alquimistas/    ← Code, creation, engineering
    ├── procuradores/   ← Management, law, organization
    └── coordinacion/   ← Coordination (Procyon)
```

## Rule

Agents never modify their own SOUL.md or OPERATOR.md. That is like an employee rewriting their own contract. Only Oracle can modify identity and operational rules.
