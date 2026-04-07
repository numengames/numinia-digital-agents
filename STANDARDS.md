---
id: "STANDARDS"
title: "Standards — Narrative Work OS"
type: meta
status: active
version: "1.0.0"
created: "2026-04-07T12:56:00Z"
updated: "2026-04-07T12:56:00Z"
author: "nimrod"
owner: "oracle"
tags: [standards, conventions, meta, nwos]
license: "CC0-1.0"
---

# STANDARDS — Narrative Work OS

> **Resumen:** Fuente de verdad de todas las convenciones técnicas del sistema NWOS.
> **Epistémico:** Qué estándar usar para timestamps, IDs, idiomas, frontmatter, commits, frameworks y documentos.
> **Pragmático:** Antes de crear cualquier documento o tomar una decisión de convención, consultar este archivo.
> **Audiencia:** Agentes · Oráculos

*Este documento es la fuente de verdad de todas las convenciones técnicas del sistema NWOS.*

**Regla de oro:** Antes de usar un nuevo estándar, documéntalo aquí. Antes de cambiar uno existente, crea una decisión ADR que lo justifique.

---

## 1. Timestamps

**Estándar:** ISO 8601 completo con timezone explícito.

```yaml
# ✅ Correcto
created: "2026-04-07T12:56:00Z"        # UTC (recomendado para campos de sistema)
updated: "2026-04-07T14:23:00+02:00"   # Con timezone local (para campos visibles al humano)

# ❌ Incorrecto
created: "2026-04-07T00:00:00Z"                   # Fecha sin hora — ambiguo
updated: "07/04/2026"                   # Formato no estándar
```

**Política:**
- Campos internos del sistema (git, logs, frontmatter): **UTC (`Z`)**
- Campos visibles al usuario (reportes, UI): **UTC+2 Madrid en horario de verano, UTC+1 en invierno**
- Nunca omitir la hora en campos `created` y `updated`

**Referencia:** [RFC 3339](https://www.rfc-editor.org/rfc/rfc3339) / [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)

---

## 2. Identificadores

### 2A. Display IDs (legibles por humanos)

**Formato:** `{TIPO}-{NNNNN}` — 5 dígitos con zero-padding.

```yaml
# Misiones
id: "MIS-00037"     # ✅ — orden lexicográfico correcto hasta 99.999
id: "MIS-037"       # ❌ — rompe sort lexicográfico después de MIS-999

# Decisiones
id: "DEC-00001"

# Reportes
id: "RPT-2026-04-07"   # reportes usan fecha, no número secuencial

# Protocolos
id: "P-006"            # protocolos usan número corto — max ~50
```

**Prefijos registrados:**

| Prefijo | Tipo | Ejemplo |
|---------|------|---------|
| `MIS-` | Misión | MIS-00037 |
| `DEC-` | Decisión | DEC-00001 |
| `ADR-` | ADR técnico | ADR-001 |
| `RPT-` | Reporte | RPT-2026-04-07 |
| `P-` | Protocolo | P-006 |
| `S-` | Seminal | S-003 |
| `BP-` | Blueprint/Plano | BP-cao |
| `APR-` | Approval Request | APR-20260407-001 |

### 2B. Canonical IDs (sistema interno)

**Formato:** UUID v7 (RFC 9562) — time-ordered, sortable, collision-free.

```yaml
# Frontmatter de cualquier documento
uid: "018e8f30-0000-7000-8000-000000000001"   # UUID v7
```

**Cuándo usar:**
- APIs futuras que consuman el Archive
- Cuando múltiples instancias NWOS necesiten interoperar
- Cross-references en el Knowledge Graph

**Implementación:** El `uid` es generado una vez al crear el documento y nunca cambia, aunque el `id` display cambie.

**Referencia:** [RFC 9562 — UUID v7](https://www.rfc-editor.org/rfc/rfc9562)

---

## 3. Idiomas

**Política:** Todo documento nuevo en el sistema debe tener versión en **español (ES)** e **inglés (EN)**.

```
# Convención de naming
documento.md          # Versión primaria (ES para docs operativos internos)
documento.en.md       # Versión EN explícita

# O estructura de carpetas cuando haya muchos docs
es/documento.md
en/documento.md
```

**Prioridad de idioma por contexto:**

| Contexto | Idioma primario | Idioma secundario |
|----------|----------------|-------------------|
| Operaciones internas (SOUL, OPERATOR, logs) | ES | EN |
| Documentación pública (README, web) | EN | ES |
| Seminales/Canon | EN (original) | ES (pendiente) |
| Misiones | ES | EN al cerrar |
| Reportes diarios | ES | — |

**Idiomas futuros (no inmediatos):** 日本語, 한국어, 中文, Português.

**Misión relacionada:** MIS-00056 (i18n ES+EN)

---

## 4. Estructura de archivos

### 4A. Agentes

```
agents/
├── {nombre-agente}/
│   ├── SOUL.md       # Identidad, valores, voz
│   ├── OPERATOR.md   # Leyes operativas
│   ├── STATUS.md     # Estado actual, métricas, pendientes
│   └── MEMORY.md     # Memoria curada a largo plazo
└── _template/        # Template base

guilds/
├── {nombre-guild}/
│   ├── charter.md    # Misión y dominio del gremio
│   └── roster.md     # Referencias a agentes (no archivos)
```

**Regla:** Los archivos del agente viven en `agents/{nombre}/`. Los gremios no contienen agentes — los referencian.

### 4B. Misiones

```
missions/
├── backlog/   # No empezadas
├── active/    # En curso
└── done/      # Completadas
```

### 4C. Decisiones

```
decisions/
├── ADR-001-*.md   # Decisiones técnicas de arquitectura
└── DEC-00001-*.md # Decisiones estratégicas/operativas
```

---

## 5. Frontmatter

**Schema mínimo requerido** para cualquier documento:

```yaml
---
id: "{TIPO}-{ID}"
uid: "{UUID-v7}"                    # pendiente de implementar en todos
title: "{Título del documento}"
type: "{mission|decision|report|protocol|blueprint|seminal|meta|agent}"
status: "{active|draft|done|archived|deprecated}"
version: "1.0.0"                    # semver
created: "YYYY-MM-DDTHH:MM:SSZ"    # ISO 8601 UTC
updated: "YYYY-MM-DDTHH:MM:SSZ"    # ISO 8601 UTC
author: "{agent-id|oracle-id}"
owner: "{oracle|agent}"
tags: [tag1, tag2]
license: "CC0-1.0"
---
```

**Schema extendido para misiones:**

```yaml
area: "{Producto|Infraestructura|CAO|Ventas|Contenido|Financiación|Documentación|Operaciones}"
guild: "{Centinelas|Alquimistas|Exegetas|Procuradores}"
tipo: "{biológico|digital|híbrido}"
priority: "{critical|high|medium|low}"
effort: "{XS|S|M|L|XL}"
phase: "{backlog|active|done|cancelled|blocked}"
human_approval_score: {1-10}
started: "YYYY-MM-DDTHH:MM:SSZ"    # null si no empezada
completed: "YYYY-MM-DDTHH:MM:SSZ"  # null si no completada
```

---

## 6. Commits de git

**Formato:** Conventional Commits adaptado al NWOS.

```
{tipo}({scope}): {descripción en ≤72 chars}

{cuerpo opcional — lista de cambios}

{footer opcional — references, breaking changes}
```

**Tipos registrados:**

| Tipo | Uso |
|------|-----|
| `feat` | Nueva feature, nuevo documento, nueva misión |
| `fix` | Corrección de error |
| `docs` | Documentación pura |
| `refactor` | Reestructuración sin cambio funcional |
| `session` | Cierre de sesión (P-006) |
| `qa` | Cambios derivados de QA |
| `standards` | Adopción o cambio de estándar |
| `canon` | Modificación de documentos canónicos (requiere Oracle) |

**Scopes comunes:** `nimrod`, `missions`, `decisions`, `canon`, `guilds`, `protocols`, `web`

**Ejemplos:**
```bash
feat(missions): add MIS-00037 Archive Summa
fix(nimrod): resolve duplicate agents/guilds/sentinels bug
session(nimrod): close 2026-04-07 afternoon session
standards: adopt ISO 8601 timestamps and UUID v7
canon(index): update to 10 seminal documents
```

---

## 7. Frameworks y metodologías adoptadas

### 7A. BDD — Behavior-Driven Development

**Herramienta:** Cucumber + Gherkin  
**Alcance:** Tests de aceptación de misiones digitales y features web  
**Idioma de los escenarios:** Español  
**Ubicación:** `/tests/features/*.feature` por repo

```gherkin
# Ejemplo en español
Característica: Sistema de misiones
  Escenario: Cerrar una misión con Ejecución Real
    Dado que existe la misión "MIS-00037" en estado "active"
    Cuando el agente completa los criterios de aceptación
    Y documenta la sección "Ejecución Real"
    Entonces el estado de la misión cambia a "done"
    Y el commit incluye la fecha de cierre
```

**Convención:** Cada misión digital de complejidad M+ debe tener al menos 3 escenarios Cucumber antes de empezar.

### 7B. ADR — Architecture Decision Records

**Formato:** Propio del NWOS (ver `decisions/ADR-001`)  
**Cuándo crear:** Ante cualquier decisión técnica que afecte la arquitectura  
**Numeración:** `ADR-NNN` para decisiones técnicas puras, `DEC-NNNNN` para decisiones estratégicas

### 7C. Wardley Mapping

**Uso:** Análisis estratégico de posicionamiento de componentes  
**Documento de referencia:** `blueprints/WARDLEY-MAP.md`  
**Cadencia:** Revisar y actualizar cada trimestre

### 7D. DORA Metrics

**KPIs de ingeniería a implementar (MIS-00049):**
- Deployment Frequency
- Lead Time for Changes
- Change Failure Rate
- Mean Time to Recovery (MTTR)

### 7E. Conventional Commits

**Ver sección 6 de este documento.**

### 7G. Active Inference & Free Energy Principle

**Marco teórico:** Karl Friston, Active Inference Institute  
**Aplicación en NWOS:** El ciclo BOOT/EXECUTE/COMMIT es un ciclo de inferencia activa.

| Fase NWOS | Fase Active Inference | Descripción |
|-----------|----------------------|-------------|
| BOOT | Carga del modelo generativo | El agente carga sus priors (SOUL.md, OPERATOR.md, MEMORY.md) |
| EXECUTE | Reducción de energía libre | El agente actúa o percibe para minimizar sorpresa |
| COMMIT | Actualización del modelo | El agente actualiza sus beliefs con la experiencia nueva |

**Campos opcionales en misiones y decisiones:**

```yaml
# Pensamiento Bayesiano / Active Inference
hypothesis: "descripción de la hipótesis que esta acción valida"
confidence_before: 7   # 1-10 — confianza antes de ejecutar
confidence_after: null  # rellenar al cerrar — cómo actualizó nuestra creencia
free_energy_reduced: null  # qué sorpresa/incertidumbre se redujo
```

**Referencia:** Active Inference Institute (partner de Numen Games)  
**Nota:** El Active Inference Institute es un posible usuario del NWOS — ya colaboramos en el diseño de su Discord.

### 7H. OODA Loop (Observe → Orient → Decide → Act)

**Autor:** John Boyd (originally for aerial combat, now universal)  
**Aplicación en NWOS:**

| OODA | NWOS | Descripción |
|------|------|-------------|
| Observe | BOOT | Leer el Archive, cargar contexto |
| Orient | Inicio EXECUTE | Entender la misión, leer briefing |
| Decide | EXECUTE | Elegir cómo abordar |
| Act | EXECUTE + COMMIT | Ejecutar y persistir el conocimiento |

El valor del OODA sobre BOOT/EXECUTE/COMMIT es el **re-loop explícito**: después de ACT vuelves a OBSERVE. El COMMIT deja el sistema en un estado que el próximo BOOT observa. El ciclo es continuo, no lineal.

### 7I. Build-Measure-Learn (Lean Startup)

**Aplicación en NWOS:** Misiones de producto y experimentos.  
**Campo opcional:**

```yaml
generates_mission: "MIS-00059"  # misión que nace de lo aprendido en esta
```

El valor epistémico de la misión es el "Measure". La Ejección Real es el "Learn". El `generates_mission` cierra el loop: el aprendizaje genera la siguiente hipótesis.

### 7F. Semantic Versioning (SemVer)

**Formato:** `MAJOR.MINOR.PATCH`  
**Aplicación:** Versión de todos los documentos del sistema  
- MAJOR: cambio incompatible (ej: refactor de arquitectura)
- MINOR: nueva funcionalidad sin romper existente
- PATCH: corrección o actualización menor

**Referencia:** [semver.org](https://semver.org)

### ⚠️ Política de autorización por nivel de versión

| Nivel | Ejemplo | Puede ejecutar | Requiere |
|-------|---------|---------------|----------|
| PATCH | 1.0.0 → 1.0.1 | Agente digital | Solo |
| MINOR | 1.0.0 → 1.1.0 | Agente digital | Solo |
| **MAJOR** | **1.0.0 → 2.0.0** | **Agente biológico (Oráculo)** | **Aprobación explícita obligatoria** |

**Regla:** El primer dígito de cualquier versión (MAJOR) nunca puede incrementarse sin autorización explícita de un Oráculo (agente biológico). Aprobación score 9/10.

*Establecido por Pablo FM — 2026-04-07*

---

## 8. Convención de documentos — Estructura estándar

Todo documento del NWOS debe comenzar con una **tarjeta de contexto** inmediatamente después del frontmatter. Esto permite al lector humano decidir en 3 segundos si el documento le merece atención, y al agente identificar el propósito del archivo sin leer el cuerpo completo.

### Opción C — Estándar completo (todos los documentos)

```markdown
---
[frontmatter YAML]
---

# Título del documento

> **Resumen:** Una frase que describe QUÉ ES este documento.
> **Epistémico:** Qué aprendes o qué pregunta responde leerlo.
> **Pragmático:** Qué puedes hacer con este documento una vez leído.
> **Audiencia:** Agentes · Oráculos · Externos  *(marcar los relevantes)*

---

[Cuerpo del documento]
```

### Variante mínima (templates, índices, documentos muy cortos)

```markdown
> **Epistémico:** Qué aprendes.
> **Pragmático:** Qué puedes hacer.
```

### Reglas

1. La tarjeta de contexto va **siempre después del `# Título`**, antes del cuerpo
2. El **Resumen** es una frase, no un párrafo
3. **Epistémico** y **Pragmático** son obligatorios en todos los documentos operativos
4. **Audiencia** es opcional pero recomendado en documentos públicos o multi-audiencia
5. Documentos nuevos deben incluir la tarjeta desde su creación
6. Documentos existentes se actualizan progresivamente (no retroactivo masivo)

### Alineación con Active Inference

La tarjeta de contexto es una **reducción de energía libre** para el lector:
- **Resumen** = prior sobre el contenido
- **Epistémico** = qué sorpresa se reduce al leerlo
- **Pragmático** = qué acción habilita la lectura

---

## 9. Escala de aprobación humana (Human-in-the-Loop)

| Score | Categoría | Descripción | Tiempo de respuesta |
|-------|-----------|-------------|---------------------|
| 1-2 | Rutina | Sin riesgo, reversible al instante | No requiere aprobación |
| 3-4 | Operativo | Impacto limitado, reversible | 24h |
| 5-6 | Táctico | Impacto moderado, parcialmente reversible | 24h |
| 7-8 | Estratégico | Afecta múltiples sistemas o agentes | 12h |
| 9 | Sistémico | Modifica canon, OPERATOR, seguridad | Inmediato |
| 10 | Fundacional | Irreversible, reputación, dinero real | Inmediato + reunión |

**Template de solicitud:** ver `protocols/APPROVAL-REQUEST-template.md`

---

## Historial de cambios

| Versión | Fecha | Cambio |
|---------|-------|--------|
| 1.0.0 | 2026-04-07T12:56:00Z | Creación inicial — timestamps ISO 8601, UUID v7, arquitectura agentes, idiomas, frontmatter, commits, frameworks (BDD/Cucumber, ADR, Wardley, DORA, SemVer) |
| 1.1.0 | 2026-04-07T14:07:00Z | §7G Active Inference & Free Energy Principle (partner: AII) + §7H OODA + §7I Build-Measure-Learn + §8 Convención de documentos Opción C (tarjeta de contexto: Resumen + Epistémico + Pragmático + Audiencia) |

---

*Nimrod 🗡️ + Alquimista-01 + Exégeta-01 + Procurador-01 — 2026-04-07*  
*"Un estándar no documentado no es un estándar — es una costumbre."*
