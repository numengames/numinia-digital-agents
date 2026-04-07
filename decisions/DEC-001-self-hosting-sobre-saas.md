---
id: "DEC-001"
title: "Self-hosting sobre SaaS para infraestructura"
type: decision
status: active
version: "1.0.0"
created: "2026-04-03"
updated: "2026-04-03"
author: "pablo-fm"
owner: "oracle"
tags: [decisions, infrastructure, self-hosting, philosophy]
area: "Infraestructura / Filosofía"
superseded_by: null
license: "CC0-1.0"
---

# DEC-001 — Self-hosting sobre SaaS para infraestructura

## Contexto

Numen Games necesitaba analytics y sistema de contacto para pablofm.com. Las opciones eran servicios SaaS o soluciones self-hosted.

## Decisión

**Self-hosting.** Umami para analytics, Cal.com para reservas, ambos en el servidor propio.

## Por qué

- Filosofía ZK de Pablo: los datos no deben salir de donde no necesitan salir
- Coste 0 vs. SaaS de pago a escala
- Coherencia con los valores de Numinia: soberanía digital

## Alternativas descartadas

- **Google Analytics** — cede datos a Google, requiere banner de cookies
- **Formspree** — sin control, endpoint puede desaparecer
- **Calendly** — de pago a partir de cierto uso

## Pros / Contras

**Pros:** Control total de datos · Privacidad real · Coste operativo 0  
**Contras:** Mantenimiento propio · Requiere infraestructura operativa

---

*Oracle: Pablo FM — 2026-04-03*
