---
id: "P-008"
title: "Approval Brief Protocol"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-07T15:00:00Z"
updated: "2026-04-07T15:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [approval, human-in-the-loop, security, protocol]
license: "CC0-1.0"
---

# P-008 — Protocolo de Approval Brief

> **Resumen:** Estándar de comunicación para solicitudes de aprobación de agentes digitales a agentes biológicos.
> **Epistémico:** Qué principios gobiernan la relación de aprobación humano–máquina en la CAO.
> **Pragmático:** Formato exacto que usa todo agente digital antes de ejecutar una acción que requiera OK humano.
> **Audiencia:** Agentes · Oráculos

---

## Motivación

Un agente digital pide aprobación varias veces al día. Sin estructura, eso se convierte en ruido — el agente biológico aprueba sin entender, o rechaza por miedo a lo desconocido. Ninguna de las dos es una buena respuesta.

El objetivo es que **cada solicitud de aprobación sea una unidad de información completa**: el agente biológico sabe exactamente qué se va a hacer, por qué, y qué tan importante es que lo piense bien.

Este protocolo es un wrapper operativo sobre `APPROVAL-REQUEST-template.md` — el template canónico. Para aprobaciones formales complejas (score ≥7), usar el template completo. Para aprobaciones de chat/Telegram, usar el formato compacto de este protocolo.

---

## Tipos de aprobación

| Tipo | Cuándo usar | Tiene comando |
|---|---|:---:|
| **Ejecución** | Antes de ejecutar un comando con efecto real | ✅ sí |
| **Diseño UX/UI** | Antes de implementar un cambio visual o de interacción | ❌ no — propuesta descriptiva |

---

## Formato compacto — Ejecución (chat/Telegram)

```
🔔 SOLICITUD DE APROBACIÓN — Score {X}/10
━━━━━━━━━━━━━━━━━━━━━━━━
Agente: {nombre} | Misión: {MIS-NNN} ← OBLIGATORIO
━━━━━━━━━━━━━━━━━━━━━━━━
Contexto:    [2 frases — estado actual / por qué surge ahora]
Acción:      [Qué se va a ejecutar exactamente]
Epistémico:  [Qué aprendemos si se ejecuta]
Pragmático:  [Impacto inmediato + reversibilidad]
Sin decidir: [Qué pasa si no hay respuesta]
━━━━━━━━━━━━━━━━━━━━━━━━
Score {X}/10 — [justificación en una frase]
[comando exacto si aplica]
¿Apruebas? Sí / No / Defiero / Modificar
```

## Formato compacto — Diseño UX/UI (chat/Telegram)

```
🎨 APROBACIÓN DE DISEÑO UX/UI
━━━━━━━━━━━━━━━━━━━━━━━━
Agente: {nombre} | Misión: {MIS-NNN} ← OBLIGATORIO
━━━━━━━━━━━━━━━━━━━━━━━━
Resumen:    [Qué cambio visual/interactivo se propone]
Epistémico: [Por qué este diseño — qué principio lo justifica]
Pragmático: [Qué experimenta el usuario si se aprueba]
Audiencia:  [Quién interactúa con este elemento]
Propuesta:
  [Mockup en texto, descripción del comportamiento, o ambos]
━━━━━━━━━━━━━━━━━━━━━━━━
¿Aprobamos este diseño antes de implementar?
```

---

## Escala de Score

| Score | Nivel | Tiempo de respuesta esperado |
|---|---|---|
| 1–2 | Rutina — no requiere aprobación | — |
| 3–4 | Operativo — impacto limitado, reversible | 24h |
| 5–6 | Táctico — impacto moderado | 24h |
| 7–8 | Estratégico — afecta arquitectura | 12h |
| 9 | Sistémico — canon / OPERATOR / seguridad | Inmediato |
| 10 | Fundacional — irreversible / reputación / dinero | Inmediato + reunión |

---

## Principio de responsabilidad — grabado a fuego

> **El score orienta la atención del agente biológico — no exime de responsabilidad.**

El agente digital **informa** y **propone**. El agente biológico **decide**. Siempre.

Un score 3 aprobado es tan responsabilidad del agente biológico como un score 9. La diferencia está en cuánta energía cognitiva merece la decisión, no en quién la toma.

Este principio no puede ser modificado por ningún agente digital. Solo el Oracle puede cambiar este protocolo.

---

## Relación con otros protocolos

- **APPROVAL-REQUEST-template.md** — template canónico para aprobaciones formales (score ≥7)
- **P-005-escalation-v1.md** — si la aprobación no llega en el tiempo esperado, escalar según P-005
- **P-007-context-load-v1.md** — si el contexto de la sesión es ≥7, avisar antes de pedir aprobaciones complejas

---

*Nimrod 🗡️ — Guardián de las Puertas — Numen Games · v1.0.0 · 2026-04-07*
