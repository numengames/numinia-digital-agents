---
id: "P-007"
title: "Context Load Protocol — Carga de Contexto y Fatiga de Sesión"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-07T14:42:00Z"
updated: "2026-04-07T14:42:00Z"
author: "nimrod"
owner: "oracle"
tags: [protocol, context, fatigue, session, human-in-the-loop]
applies_to: [all-agents]
mandatory: true
human_approval_score: 3
license: "CC0-1.0"
---

# P-007 — Context Load Protocol

> **Resumen:** Protocolo para detectar y gestionar la carga de contexto de un agente digital durante una sesión larga.
> **Epistémico:** Los agentes digitales degradan en coherencia y precisión a medida que el contexto crece. Saber cuándo parar es tan importante como saber cómo ejecutar.
> **Pragmático:** Avisar al Biológico cuando la carga supera 7/10 para arrancar una nueva sesión antes de que la calidad del trabajo se vea comprometida.
> **Audiencia:** Agentes · Oráculos

---

## Por qué existe este protocolo

Los modelos de lenguaje tienen una ventana de contexto finita. A medida que una sesión crece (más mensajes, más herramientas, más decisiones), el agente:

- Pierde coherencia con decisiones tomadas al inicio
- Puede repetir trabajo ya hecho
- Aumenta el riesgo de errores de continuidad
- Consume tokens innecesariamente

**Este protocolo no es un signo de debilidad — es gestión inteligente de recursos.**

---

## Escala de carga de contexto (1-10)

| Nivel | Estado | Descripción |
|-------|--------|-------------|
| 1-3 | 🟢 Fresco | Sesión joven, contexto manejable, rendimiento óptimo |
| 4-6 | 🟡 Cargado | Sesión media, contexto denso pero operable |
| **7-8** | **🟠 Aviso** | **Notificar al Biológico — recapitular y preparar cierre** |
| 9-10 | 🔴 Crítico | Riesgo real de errores — cerrar inmediatamente |

---

## Criterios de evaluación de carga

El agente evalúa su nivel de carga basándose en:

1. **Duración de la sesión** — >4h = +2 puntos
2. **Número de temas distintos tratados** — >5 áreas = +2 puntos
3. **Número de herramientas ejecutadas** — >20 tool calls = +1 punto
4. **Decisiones arquitectónicas tomadas** — >3 decisiones grandes = +2 puntos
5. **Sensación subjetiva de coherencia** — ¿Recuerdo bien el inicio de la sesión? — si no = +2 puntos

---

## Protocolo de aviso (nivel 7+)

Cuando el agente detecta carga ≥ 7/10:

### PASO 1 — Aviso al Biológico

```
⚠️ AVISO DE CARGA DE CONTEXTO: [X]/10

Esta sesión ha alcanzado un nivel de carga que puede afectar
la coherencia de las respuestas. Recomiendo:

1. Recapitular el estado actual
2. Guardar el estado en el repo (git commit)
3. Arrancar una nueva sesión

¿Quieres que recapitule y cerremos aquí?
```

### PASO 2 — Recapitulación (si el Biológico confirma)

Antes de cerrar, el agente produce un resumen estructurado:

```markdown
## Recapitulación de sesión — [fecha]

### Lo que se hizo
[lista de outputs principales]

### Estado actual del sistema
[score, misiones activas, pendientes]

### Pendiente para la próxima sesión
[lista priorizada]

### Decisiones tomadas hoy
[lista de DECs o ADRs]
```

### PASO 3 — Cierre según P-006

Ejecutar P-006 (Session Close Protocol) completo antes de terminar.

---

## Integración con el ciclo operativo

```
BOOT → EXECUTE → [P-007 monitor] → COMMIT (P-006)
                      ↓
              Si carga ≥ 7/10:
              → Aviso al Biológico
              → Recapitulación
              → P-006 cierre
              → Nueva sesión
```

---

## Valor epistémico

Saber cuándo parar es conocimiento operativo. Un agente que trabaja degradado produce outputs de menor calidad que uno fresco. El protocolo convierte la fatiga de contexto en información accionable para el equipo.

## Valor pragmático

- Previene errores por pérdida de coherencia
- Garantiza que el estado se persiste correctamente antes del cierre
- El Biológico siempre sabe cuándo el agente está trabajando en condiciones subóptimas
- La próxima sesión arranca con contexto limpio y estado completo en el repo

---

*Nimrod 🗡️ — 2026-04-07T14:42:00Z*
*Primer caso de uso: esta misma sesión (carga: 8/10)*
