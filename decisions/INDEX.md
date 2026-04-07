---
id: "decisions-index"
title: "Decisions — Index"
type: adr
status: active
version: "1.0.0"
created: "2026-04-06T00:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [decisions, index, adr]
license: "CC0-1.0"
---
# Decisions — Voluntad Cristalizada

> **Resumen:** Documento del sistema NWOS — Decisions — Index.
> **Epistémico:** Qué se decidió, por qué, y qué alternativas se descartaron.
> **Pragmático:** Consultar antes de tomar decisiones en el mismo dominio.
> **Audiencia:** Agentes · Oráculos

---


Architectural Decision Records (ADR) of the Narrative Work OS. These records are:
- **Append-only** — never delete
- **Supersedable** — a new ADR can supersede a previous one, but the original remains
- **Permanent** — even cancelled decisions stay for historical record

## Active decisions

| ID | Decisión | Estado | Fecha |
|---|---|---|---|
| ADR-001 | GitHub as Archive Summa | ✅ Active | 2026-04-06 |
| ADR-002 | Markdown as universal format | ✅ Active | 2026-04-06 |
| DEC-001 | Self-hosting sobre SaaS | ✅ Activa | 2026-04-03 |
| DEC-002 | Construir en público con licencia CC0 | ✅ Activa | 2026-04-02 |
| DEC-003 | Arbitrum como blockchain de Numinia | ⚠️ Provisional | 2026-04-05 |
| DEC-004 | Arquitectura CAO híbrida | ✅ Activa | 2026-04-05 |
| DEC-005 | pablofm.com como portal público de la CAO | ✅ Activa | 2026-04-03 |

## How to create an ADR

1. Copy the frontmatter template from any existing ADR
2. Assign the next sequential number
3. Fill context, decision, and consequences
4. Open PR with label `decision`
5. Oracle approves and merges
