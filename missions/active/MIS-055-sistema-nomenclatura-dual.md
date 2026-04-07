---
id: "MIS-055"
title: "Sistema de Nomenclatura Dual — Narrative Dial + Gamification Dial"
type: mission
status: en-curso
version: "1.0.0"
created: "2026-04-07"
updated: "2026-04-07"
author: "pablo-fm"
owner: "oracle"
tags: [cao, nwos, nomenclature, gamification, narrative, system-design]
license: "CC0-1.0"
mission_id: "MIS-055"
assigned_to: "nimrod"
requested_by: "oracle"
area: "CAO"
guild: "Exegetas"
tipo: "híbrido"
priority: "critical"
effort: "L"
phase: "active"
started: "2026-04-07"
completed: null
---

# MIS-055 — Sistema de Nomenclatura Dual

**Area:** CAO · **Gremio:** Exegetas · **Tipo:** 🔀 Híbrido · **Prioridad:** 🔴 Crítica · **Esfuerzo:** L

---

## Origen

Surgido en el Dark Council / sesión El Velo — 2026-04-06.

Consenso de agentes digitales y biológicos: entre la capa narrativa y la capa operacional existe un problema de primera impresión. La narrativa Numinia (nivel 10/10) actúa como barrera de adopción para organizaciones que solo quieren el sistema operativo, no el mundo narrativo.

**Solución acordada:** Dos diales de ajuste independientes por organización.

---

## Historia

Como organización que quiere adoptar el NWOS, quiero poder elegir el nivel de narrativa y de gamificación de mi implementación, para que el sistema hable mi idioma sin perder ninguna funcionalidad.

---

## Los dos diales

### 🎭 Narrative Dial (1–10)
Controla el vocabulario y la identidad semántica del sistema.

- **1** = Idioma de negocio puro. Proyectos, departamentos, roles corporativos.
- **5** = Idioma mixto. Metáforas suaves sin lore explícito.
- **10** = Numinia completo. Gremios, Oráculos, misiones, el Velo.

### 🎮 Gamification Dial (1–10) — 5 umbrales reales
Controla los mecánicos de juego, progresión y recompensa.

La gamificación tiene saltos cualitativos, no curva suave. Se definen 5 umbrales con nombre; los niveles intermedios son blends sin nombre propio.

| Nivel | Nombre | Lo que cambia |
|---|---|---|
| **1** | None | Solo el OS. Sin mecánicas de ningún tipo. |
| **3** | Visibility | Progreso visible. Dashboards, completion %, streaks. La gente ve el estado del sistema. |
| **5** | Achievement | Logros, badges, hitos reconocidos. El sistema celebra. |
| **7** | Progression | Rangos, trayectoria, reputación acumulada. El sistema recuerda y recompensa la historia. |
| **10** | Full Economy | Tokens, Prism Cells, recompensas reales. El sistema tiene peso económico. |

> Cara externa: 5 umbrales con nombre (más comprensible para el cliente).
> Internamente: mapeado a escala 1-10 para configuración técnica granular.

> **Numinia** = Narrative 10 · Gamification en diseño (objetivo: 10)
> **Corp estándar** = Narrative 1 · Gamification 1–3

---

## Criterios de aceptación

- [ ] Tabla de equivalencias completa: vocabulario Numinia ↔ vocabulario negocio para los 5 niveles
- [ ] Propuesta de nomenclatura Nivel 1 (Business) documentada y aprobada por Pablo
- [ ] Propuesta de nomenclatura Nivel 5 (Mixed) documentada
- [ ] Página pública `/idioma` en pablofm.com explicando el sistema
- [ ] Decisión DEC-006 creada una vez validado el modelo
- [ ] Integrar en `/nwos` como feature de adaptabilidad

---

## Equivalencias propuestas — Narrative Dial

### Agentes / Roles

| Numinia (10) | Mixed (5) | Business (1) |
|---|---|---|
| Oráculo | Fundador | Executive / C-Suite |
| Centinela | Operations Lead | Head of Operations |
| Alquimista | Innovation Lead | CTO / Head of Product |
| Exégeta | Knowledge Lead | Chief of Staff / Head of Content |
| Procurador | Business Lead | COO / Head of Business |
| Procyon | Sistema de Inteligencia | AI Orchestration Layer |
| Nómada | Nuevo miembro | Onboarding |
| Ciudadano | Miembro | Team Member |
| Peregrino | Senior | Senior Member |
| Vernáculo | Experto | Expert / Principal |
| Arconte | Líder | Lead / Director |
| Agente digital | Agente IA | AI Agent / Digital Coworker |

### Estructuras

| Numinia (10) | Mixed (5) | Business (1) |
|---|---|---|
| Gremio | Equipo | Department / Team |
| Facción | Área | Division |
| CAO | Centro de Operaciones | Operations Center |
| Plano | Mapa del sistema | System Blueprint |
| Archivo / Archive | Base de conocimiento | Knowledge Base |
| Decisión / Piedra del Camino | Decisión arquitectónica | Decision Record |
| Reporte | Informe | Report |
| Protocolo | Procedimiento | Process / SOP |

### Acciones / Rituales

| Numinia (10) | Mixed (5) | Business (1) |
|---|---|---|
| Misión | Iniciativa | Project / Initiative |
| Daily | Daily | Daily Standup |
| Dark Council | Estrategia semanal | Weekly Strategy |
| Lunar Coven | Sesión creativa | Creative Session |
| Session Zero | Onboarding | Onboarding Workshop |
| Aventura | Proyecto narrativo | Campaign / Program |
| Temporada | Ciclo de producto | Season / Quarter |

### Sistema / Producto

| Numinia (10) | Mixed (5) | Business (1) |
|---|---|---|
| Narrative Work OS | Work OS narrativo | Work Operating System |
| El Velo | El sistema | The System |
| Numinia | La ciudad | The Organization |
| Prism Cell | Token de membresía | Membership Token |
| Sello | Certificado | Badge / Certificate |

---

## Valor epistémico

El sistema de nomenclatura dual demuestra que el NWOS no es un producto con una identidad fija — es un framework adaptable cuyo valor no depende del idioma en que se exprese. Esto resuelve la Tensión #1 del Wardley Map.

## Valor pragmático

- Desbloquea ICPs que rechazaban el NWOS por el vocabulario narrativo
- Permite presentar el sistema a directivos corporativos sin pérdida de funcionalidad
- El Narrative Dial convierte la narrativa en una feature, no en un requisito
- Abre el mercado PYME tradicional (10% éxito actual → potencial de escala)

---

## Decisión pendiente

Una vez validado, crear **DEC-006 — Sistema de Nomenclatura Dual** que modifique parcialmente la arquitectura del NWOS para incluir los dos diales como configuración de implementación.

---

## Notas

El Gamification Dial se discutirá en una sesión dedicada posterior.
El Narrative Dial es la prioridad inmediata — resuelve el problema de adopción más urgente.

---

*Nimrod 🗡️ + Equipo — 2026-04-07*
