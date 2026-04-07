---
id: "MIS-00048"
title: "Sistema de costes por agente"
type: mission
status: backlog
created: "2026-04-04T00:00:00Z"
area: "Operaciones"
guild: "Centinelas"
tipo: "digital"
priority: "critical"
effort: "M"
license: "CC0-1.0"
---

# MIS-048 — Sistema de costes por agente

**Area:** Operaciones · **Gremio:** Centinelas · **Tipo:** 🤖 Digital · **Prioridad:** 🔴 Crítica · **Esfuerzo:** M

## Historia

Como Pablo, quiero saber exactamente cuánto gasta cada agente por día y por misión, para optimizar costes y justificar la inversión.

## Criterios de aceptación

- [ ] API de Anthropic conectada para datos de uso real
- [ ] Coste por misión registrado en logs
- [ ] Coste diario visible en reporte de las 8am
- [ ] Dashboard /cao actualizado con coste real

## Valor epistémico

Sin datos de coste reales, no se puede optimizar.

## Valor pragmático

Diferencia entre gasto controlado y gasto opaco.

## Notas

Bloqueado por: API key Anthropic con usage permissions (se configura por SSH, nunca por chat).
