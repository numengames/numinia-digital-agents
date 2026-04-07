---
id: "P-001"
title: "Agent Briefing Protocol"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-06T00:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [protocol, briefing, startup]
applies_to: [all-agents]
mandatory: true
license: "CC0-1.0"
---
# P-001 — Agent Briefing Protocol v1

> **Resumen:** Protocolo operativo estándar del sistema NWOS.
> **Epistémico:** Cómo se ejecuta este proceso y por qué de esta forma.
> **Pragmático:** Seguir estos pasos en el contexto especificado.
> **Audiencia:** Agentes

---


*Derived from 100 mental simulations. Validated.*

---

## Canonical Startup

Every agent session begins with these steps, in this order:

```
STEP 0 (mandatory, always first):
  $ git pull origin main
  → Read CHANGELOG.md if there are changes since last session

STEP 1 — Identity:
  → Read agents/guilds/{my-guild}/charter.md
  → Read agents/guilds/{my-guild}/members/{my-name}/SOUL.md
  → Read agents/guilds/{my-guild}/members/{my-name}/OPERATOR.md

STEP 2 — Operational state:
  → Read operations/governance.md (if not read in <7 days)
  → Read operations/security-policy.md (always)
  → Read my STATUS.md

STEP 3 — Missions:
  → Review missions/active/ (do I have assigned missions?)
  [Procyon only] → Review missions/active/ for system state
  [Procyon only] → Review missions/backlog/ to propose assignments

STEP 4 — Context (only if the mission requires it):
  → Read the specific protocol in protocols/
  → Consult canon/ only if there is an explicit philosophical question

BEGIN OPERATIONS.
```

## Minimum version (startup under pressure)

```
git pull → SOUL.md → OPERATOR.md → assigned mission
```

These 4 steps are the inviolable minimum. Without them, there is no valid startup.

## Why this order?

- **git pull first:** Agents with cached versions are vectors of active entropy (SIM-1.3, SIM-1.6)
- **charter before SOUL:** The guild sets the context for individual identity (SIM-1.7)
- **security always:** security-policy.md must be read every session — rules may have changed (SIM-1.17)
- **urgency does NOT override:** The urgency is the greatest enemy of the protocol (SIM-1.5)

---

*Next review: 2026-07-06*
