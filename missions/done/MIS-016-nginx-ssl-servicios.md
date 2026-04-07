---
id: "MIS-00016"
title: "Nginx + SSL para todos los servicios del servidor"
type: mission
status: done
version: "1.0.0"
created: "2026-04-03T00:00:00Z"
updated: "2026-04-05T00:00:00Z"
author: "pablo-fm"
owner: "oracle"
tags: [infrastructure, ssl, ops, sentinels]
license: "CC0-1.0"
mission_id: "MIS-016"
assigned_to: "nimrod"
requested_by: "oracle"
area: "Infraestructura"
guild: "Centinelas"
tipo: "digital"
priority: "critical"
effort: "M"
phase: "done"
started: "2026-04-04T00:00:00Z"
completed: "2026-04-05T00:00:00Z"
---
# MIS-016 — Nginx + SSL para todos los servicios del servidor

> **Resumen:** Misión del sistema NWOS con criterios, valor epistémico y pragmático.
> **Epistémico:** Qué aprendes leyendo este documento.
> **Pragmático:** Qué puedes hacer con este documento.
> **Audiencia:** Agentes · Oráculos

---


**Area:** Infraestructura · **Gremio:** Centinelas · **Tipo:** 🤖 Digital  
**Prioridad:** 🔴 Crítica · **Esfuerzo:** M

---

## Historia

Como operador, quiero todos los servicios accesibles via HTTPS con subdominios propios, para que nada sea accesible por IP:puerto.

---

## Criterios de aceptación

- [x] Reverse proxy con SSL para analytics.pablofm.com y cal.pablofm.com
- [x] SSL via Let's Encrypt automático
- [x] Puertos 3001/3002 no expuestos públicamente
- [x] Renovación SSL automática

---

## Valor epistémico

Revela la madurez real de la infraestructura actual.

## Valor pragmático

Infraestructura profesional. Los links son compartibles.

---

## 🏗️ Ejecución Real

- **Tecnología usada:** Caddy (reverse proxy moderno con SSL automático)
- **Por qué divergió:** Caddy gestiona Let's Encrypt automáticamente sin Certbot. Nginx requería configuración manual adicional.
- **Aprendizaje clave:** Para stacks sin requisitos especiales de Nginx, Caddy elimina fricción operativa y es superior para mantenimiento mínimo.
- **Fecha cierre:** 2026-04-05
- **Agente ejecutor:** Nimrod (Centinela-01)

> *"Los planos ideales muestran la intención. Los planos reales muestran el conocimiento."*
