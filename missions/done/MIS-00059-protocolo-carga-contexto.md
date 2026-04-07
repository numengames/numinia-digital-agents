---
id: "MIS-00059"
title: "P-007 — Protocolo de Carga de Contexto"
type: mission
status: done
version: "1.0.0"
created: "2026-04-07T14:42:00Z"
updated: "2026-04-07T14:42:00Z"
author: "pablo-fm"
owner: "oracle"
tags: [protocol, context, fatigue, session]
license: "CC0-1.0"
area: "CAO"
guild: "Centinelas"
tipo: "digital"
priority: "high"
effort: "S"
phase: "done"
completed: "2026-04-07T14:45:00Z"
---

# MIS-00059 — P-007 Protocolo de Carga de Contexto

> **Resumen:** Crear el protocolo que define cuándo y cómo un agente avisa al Biológico sobre fatiga de sesión.
> **Epistémico:** Los agentes degradan en coherencia a medida que el contexto crece. Detectarlo y comunicarlo es gestión inteligente de recursos.
> **Pragmático:** Previene errores por pérdida de coherencia y garantiza cierres limpios con estado persistido.
> **Audiencia:** Agentes · Oráculos

## Historia

Como agente digital, quiero saber cuándo mi carga de contexto es demasiado alta y avisar al Biológico, para cerrar la sesión ordenadamente antes de que la calidad del trabajo se degrade.

## Criterios de aceptación

- [x] P-007 creado en protocols/
- [x] Escala 1-10 de carga de contexto definida
- [x] Umbral de aviso: 7/10
- [x] Protocolo de aviso + recapitulación + P-006
- [x] Integrado con el ciclo BOOT/EXECUTE/COMMIT

## 🏗️ Ejecución Real

- **Tecnología usada:** Markdown + criterios cualitativos (sin instrumentación automática aún)
- **Por qué divergió:** El primer caso de uso fue la propia sesión que creó el protocolo — 8/10 de carga
- **Aprendizaje clave:** El agente puede autoevaluar su carga con criterios cualitativos simples. La instrumentación automática (contar tokens, tool calls) puede añadirse en v1.1.0
- **Fecha cierre:** 2026-04-07
- **Agente ejecutor:** Nimrod 🗡️

> *"Los planos ideales muestran la intención. Los planos reales muestran el conocimiento."*
