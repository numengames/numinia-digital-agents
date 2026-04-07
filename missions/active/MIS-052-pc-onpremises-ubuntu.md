---
id: "MIS-052"
title: "Infraestructura on-premises — PC dedicado"
type: mission
status: en-curso
version: "1.0.0"
created: "2026-04-05"
updated: "2026-04-06"
author: "pablo-fm"
owner: "oracle"
tags: [infrastructure, hardware, ollama, sentinels]
license: "CC0-1.0"
mission_id: "MIS-052"
assigned_to: "nimrod"
requested_by: "oracle"
area: "Infraestructura"
guild: "Centinelas"
tipo: "digital"
priority: "high"
effort: "L"
phase: "active"
started: null
completed: null
blocked_reason: "PC en camino — pendiente de llegada física"
---

# MIS-052 — Infraestructura on-premises — PC dedicado

**Area:** Infraestructura · **Gremio:** Centinelas · **Tipo:** 🤖 Digital  
**Prioridad:** 🟠 Alta · **Esfuerzo:** L

---

## Historia

Como operador, quiero un PC dedicado on-premises con Ubuntu 24.04 y Ollama, para reducir costes de inferencia en un 60-70% ejecutando modelos locales.

---

## Criterios de aceptación

- [ ] Ubuntu 24.04 LTS instalado en Ryzen 9 7950X + RTX 4080
- [ ] NVIDIA drivers + CUDA configurados
- [ ] Ollama instalado con Mistral 7B, Qwen2.5 14B
- [ ] OpenClaw conectado al nodo local
- [ ] Migración de servicios del servidor VPS

---

## Valor epistémico

Determina qué modelos caben en 16 GB VRAM y qué tareas pueden migrar a local.

## Valor pragmático

Reducción drástica de coste mensual en API de Anthropic (~60-70%).

---

## Hardware

- **CPU:** AMD Ryzen 9 7950X
- **GPU:** RTX 4080 (16 GB VRAM)
- **RAM:** 32 GB DDR5
- **SSD:** Corsair MP600 2TB NVMe
- **Placa:** ASUS PRIME X670E-PRO WIFI
- **SO:** Ubuntu 24.04 LTS

---

## Notas

PC en camino. Cuando llegue: instalar Ubuntu → CUDA → Ollama → conectar a OpenClaw como nodo local.
