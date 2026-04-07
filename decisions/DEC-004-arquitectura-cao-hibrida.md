---
id: "DEC-004"
title: "Arquitectura CAO híbrida"
type: decision
status: active
version: "1.0.0"
created: "2026-04-05"
updated: "2026-04-05"
author: "pablo-fm"
owner: "oracle"
tags: [decisions, cao, agents, architecture]
area: "CAO / Sistema de agentes"
superseded_by: null
license: "CC0-1.0"
---

# DEC-004 — Arquitectura CAO híbrida

## Contexto

La CAO necesitaba definir cómo operar los agentes digitales. ¿Sesiones persistentes o subagentes bajo demanda?

## Decisión

**Arquitectura híbrida: subagentes efímeros para misiones ahora, sesiones persistentes cuando el sistema madure.**

## Por qué

- Los subagentes funcionan hoy sin configuración adicional (probado con MIS-001)
- Las sesiones persistentes requieren más infraestructura
- Mínima complejidad que funciona — no sobreingeniería prematura
- El sistema de misiones .md funciona igual con ambos modelos

## Alternativas descartadas

- **Sesiones persistentes desde el inicio** — riesgo de romper config, coste fijo sin uso
- **Un solo agente generalista** — no escala, pierde especialización

## Pros / Contras

**Pros:** Funciona hoy · Coste proporcional al uso · Sin riesgo de config  
**Contras:** Sin memoria entre misiones (mitigado con briefing protocolo)

---

*Oracle: Pablo FM — 2026-04-05*
