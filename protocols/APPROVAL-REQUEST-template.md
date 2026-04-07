---
id: "APR-TEMPLATE"
title: "Approval Request — Template"
type: template
status: active
version: "1.0.0"
created: "2026-04-07T12:56:00Z"
updated: "2026-04-07T12:56:00Z"
author: "nimrod"
owner: "oracle"
tags: [template, approval, human-in-the-loop]
license: "CC0-1.0"
---

# Template — Solicitud de Aprobación

*Copia este template cuando necesites aprobación humana. Rellena todas las secciones.*

---

```markdown
---
id: "APR-{YYYYMMDD}-{NNN}"
type: approval-request
agent: "{nombre-agente}"
mission: "{MIS-NNNNN o N/A}"
score: {1-10}
created: "{YYYY-MM-DDTHH:MM:SSZ}"
status: pending
oracle_response: ""
---

## 🔔 SOLICITUD DE APROBACIÓN

**Agente:** {nombre} | **Misión:** {MIS-NNNNN} | **Score:** {X}/10

---

### CONTEXTO MÍNIMO
> Lo que necesitas saber para no estar volando a ciegas.

{2-4 frases. Estado actual / por qué surge ahora / qué lo originó.}

---

### ACCIÓN PROPUESTA

{Descripción exacta de lo que se va a ejecutar. Sin ambigüedad.}

**Alternativas descartadas:**
- {Opción A descartada — por qué}
- {Opción B descartada — por qué}

---

### VALOR EPISTÉMICO
> ¿Qué aprendemos si se ejecuta?

- **Si sale bien:** {hipótesis validada / conocimiento confirmado}
- **Si sale mal:** {qué revela del sistema}
- **Si no se ejecuta:** {qué permanece desconocido}

---

### VALOR PRAGMÁTICO
> ¿Qué impacto tiene en el mundo real?

- **Impacto inmediato:** {cambios en archivos / sistemas / personas}
- **Impacto diferido:** {consecuencias a 24h / 1 semana}
- **Reversibilidad:** {reversible | parcialmente reversible | irreversible}

---

### EJEMPLO PRÁCTICO *(omitir si la acción es obvia)*

{Un caso concreto donde esto marca la diferencia.}

---

### COSTE DE NO DECIDIR

{¿Qué pasa si no hay respuesta en 48h?}

---

### SCORE DE IMPORTANCIA: {X}/10

**Escala:**
- 1-2: Rutina — no requiere aprobación
- 3-4: Operativo — impacto limitado, reversible (24h)
- 5-6: Táctico — impacto moderado (24h)
- 7-8: Estratégico — afecta arquitectura (12h)
- 9: Sistémico — canon / OPERATOR / seguridad (inmediato)
- 10: Fundacional — irreversible / reputación / dinero (inmediato + reunión)

**Justificación del score:** {Una frase que explica por qué este número.}

---

**¿Apruebas?**
- [ ] Sí — procedo
- [ ] No — documento en decisions/ y archivo
- [ ] Defiero hasta: {fecha}
- [ ] Modificar: {instrucciones}
```

---

## Ejemplo completado — score 8/10

```markdown
---
id: "APR-20260407-001"
type: approval-request
agent: "nimrod"
mission: "MIS-00057"
score: 8
created: "2026-04-07T12:56:00Z"
status: approved
oracle_response: "Aprobado — go"
---

## 🔔 SOLICITUD DE APROBACIÓN

**Agente:** Nimrod | **Misión:** MIS-00057 | **Score:** 8/10

---

### CONTEXTO MÍNIMO

La arquitectura actual organiza los agentes bajo `agents/guilds/`. Esto causó un bug: 
Nimrod existe en dos rutas simultáneas (sentinels/ y centinelas/ — el mismo gremio en 
dos idiomas). La solución es mover los agentes a una capa raíz independiente.

---

### ACCIÓN PROPUESTA

Migrar todos los archivos de agentes a `agents/{nombre-agente}/` y crear `guilds/` 
con solo charter.md y roster.md por gremio. Actualizar P-001, README y agents/INDEX.md.

**Alternativas descartadas:**
- Mantener la estructura actual — perpetúa el bug y viola el modelo conceptual
- Solo eliminar la duplicación — parche sin resolver la causa raíz

---

### VALOR EPISTÉMICO

- **Si sale bien:** Confirma que la arquitectura flat escala a multi-guild sin duplicación
- **Si sale mal:** Revela dependencias ocultas en P-001 o herramientas que asumen la ruta actual
- **Si no se ejecuta:** El bug crece con cada nuevo agente que se active

---

### VALOR PRAGMÁTICO

- **Impacto inmediato:** ~15 archivos movidos, 3 documentos actualizados
- **Impacto diferido:** Cualquier agente nuevo se crea en la estructura correcta desde el principio
- **Reversibilidad:** Reversible con git revert, pero requiere avisar a agentes activos

---

### COSTE DE NO DECIDIR

El bug sentinels/centinelas persiste. Cualquier nuevo agente hereda la misma confusión. 
Cuando haya 5+ agentes activos, la deuda arquitectónica será mucho más cara de resolver.

---

### SCORE DE IMPORTANCIA: 8/10

Afecta el protocolo de arranque (P-001) de todos los agentes futuros y codifica 
la distinción semántica agente-guild que es central al modelo del NWOS.

---

**¿Apruebas?**
- [x] Sí — procedo
```
