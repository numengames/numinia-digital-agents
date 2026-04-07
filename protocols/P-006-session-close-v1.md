---
id: "P-006"
uid: "018e9000-0006-7000-8000-000000000006"
title: "Session Close Protocol"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-07T12:56:00Z"
updated: "2026-04-07T12:56:00Z"
author: "alquimista-01"
owner: "oracle"
tags: [protocol, session, commit, memory, close]
applies_to: [all-agents]
mandatory: true
human_approval_score: 7
license: "CC0-1.0"
---
# P-006 — Session Close Protocol v1

> **Resumen:** Protocolo operativo estándar del sistema NWOS.
> **Epistémico:** Cómo se ejecuta este proceso y por qué de esta forma.
> **Pragmático:** Seguir estos pasos en el contexto especificado.
> **Audiencia:** Agentes

---


*Todo lo que no se escribe, no ocurrió.*

---

## Cuándo ejecutar este protocolo

- Al final de cualquier sesión de trabajo
- Al detectar que la sesión va a interrumpirse (timeout, error, cambio de contexto)
- Antes de pasar una misión activa a otro agente
- Antes de cerrar la jornada

---

## Los 5 pasos de cierre

### PASO 1 — Inventario de estado

Antes de commitear, responde estas preguntas:

```
¿Hay misiones activas a medias?
  → Actualizar divergence_log en el .md de la misión
  → Si está completa: ejecutar cierre de misión (P-003)

¿Se tomaron decisiones durante la sesión no documentadas?
  → Crear nota en decisions/ o en la misión correspondiente

¿El STATUS.md refleja el estado actual?
  → Actualizar métricas, misiones activas, pendientes
```

### PASO 2 — Persistencia de memoria

```
¿Aprendí algo que debo recordar en la próxima sesión?
  → Escribir en MEMORY.md si es conocimiento de largo plazo
  → Escribir en STATUS.md (sección session_notes) si es contexto de sesión

¿Hay contexto que no está en ningún archivo?
  → NUNCA dejar esto como "nota mental" — escribirlo o se pierde para siempre
```

### PASO 3 — Git commit (formato obligatorio)

```bash
# Añadir todos los cambios
git add -A

# Commit con formato estándar (STANDARDS.md §6)
git commit -m "session(nimrod): resumen de lo hecho en ≤72 chars

- cambio 1
- cambio 2
- cambio 3

session_end: YYYY-MM-DDTHH:MM:SSZ"

# Push
git push origin main
```

**Formato de commit de sesión:**
- Prefijo obligatorio: `session({nombre-agente}):`
- Body: lista de cambios principales
- Última línea del footer: `session_end: {timestamp ISO 8601 UTC}`

**Ejemplo real:**
```bash
git commit -m "session(nimrod): QA profundo + arquitectura agentes + STANDARDS.md

- STANDARDS.md v1.0.0 creado con 8 secciones
- P-006 (session close) creado
- Arquitectura agentes migrada a flat (agents/nimrod/)
- canon/INDEX.md actualizado a 10 seminales
- Bug sentinels/centinelas resuelto

session_end: 2026-04-07T13:30:00Z"
```

### PASO 4 — Verificación mínima

```
[ ] STATUS.md refleja el estado actual de todas las misiones activas
[ ] No hay trabajo sin commitear que deba persistir
[ ] Misiones en progreso tienen divergence_log al día
[ ] Próximos pasos documentados en las misiones activas
[ ] git push completado y confirmado
```

### PASO 5 — Declaración de cierre

```
SESIÓN CERRADA
Agente: {nombre}
Timestamp: {YYYY-MM-DDTHH:MM:SSZ}
Misiones activas al cerrar: {lista o "ninguna"}
Próximo paso recomendado: {una línea}
```

---

## Versión mínima (cierre de emergencia)

Cuando la sesión va a interrumpirse sin tiempo para el cierre completo:

```bash
git add -A && git commit -m "session({agente}): emergency close — {timestamp}" && git push origin main
```

**Sin este mínimo, no hay cierre válido.**

---

## Por qué este protocolo importa

Sin P-006, cada sesión empieza desde cero con solo lo que hay en git.

El ciclo de vida del agente es:
```
BOOT (P-001) → cargar identidad del repo
    ↓
EXECUTE (P-003) → ejecutar misiones
    ↓
COMMIT (P-006) → persistir conocimiento al repo  ← este protocolo
    ↓
(next session) → BOOT carga lo que P-006 dejó
```

**El COMMIT es el momento más crítico del ciclo.** El conocimiento que no se hace commit desaparece cuando la sesión termina. No hay amnesia gradual — hay pérdida total.

---

## Valor epistémico

Cada cierre de sesión es un acto de convertir experiencia efímera en memoria institucional. El agente que cierra bien deja al siguiente agente más inteligente que él.

## Valor pragmático

- Cero pérdida de conocimiento entre sesiones
- Continuidad total si hay fallo de infraestructura
- Auditoría completa de qué hizo qué agente y cuándo
- El Archive Summa es fiel reflejo del sistema en todo momento

---

*Autoría: Alquimista-01 (propuesta) + Nimrod (validación) — 2026-04-07*  
*Próxima revisión: 2026-07-07*
