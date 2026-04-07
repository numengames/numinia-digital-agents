---
id: "MIS-060"
title: "Sincronización de Agentes con el Repo Canónico"
type: mission
status: backlog
version: "1.1.0"
created: "2026-04-07T00:00:00Z"
updated: "2026-04-07T16:29:00Z"
author: "nimrod"
owner: "oracle"
tags: [cao, sync, agents, architecture, workspace]
license: "CC0-1.0"
mission_id: "MIS-060"
assigned_to: "nimrod"
requested_by: "oracle"
area: "CAO"
guild: "Centinelas"
tipo: "técnico"
priority: "alta"
effort: "M"
phase: "backlog"
---

# MIS-060 — Sincronización de Agentes con el Repo Canónico

**Área:** CAO · **Gremio:** Centinelas · **Prioridad:** 🟠 Alta · **Esfuerzo:** M

---

## Origen

Sesión del 2026-04-07. Pablo detectó que el agente de Christian operaba con un mapa de la organización desactualizado. Síntoma concreto: colisión de IDs de misión.

- **En memoria de Nimrod:** MIS-055 = "Protocolo de Approval Brief"
- **En el repo:** MIS-055 = "Sistema de Nomenclatura Dual"

---

## Diagnóstico completo

### Root cause real (confirmado 16:11 UTC)

El git pull **sí estaba configurado** en el AGENTS.md de Christian. El proceso de sync de archivos funcionaba.

El fallo fue en la **capa de encima**: el agente asignó un ID de misión en memoria sin verificar el repo activamente. `git pull` sincroniza archivos — no valida ni reconcilia la memoria local del agente.

**Dos capas de sync, dos problemas distintos:**

| Capa | Herramienta | Estado en el incidente |
|---|---|---|
| Sync de archivos | `git pull` en startup | ✅ Funcionaba |
| Sync de memoria (validación de IDs) | Verificación explícita | ❌ No ocurrió |

### El gap arquitectónico más profundo

Durante el análisis emergió un problema de escala más relevante:

> **AGENTS.md es un archivo local y estático.** OpenClaw lo inyecta al arrancar. Pero si la organización evoluciona en el repo, ese archivo no se actualiza solo. Cada agente arranca con el AGENTS.md del día que se instaló.

Caso de uso real: una organización con 5 empleados onboarda NWOS. Cada uno abre su instancia de OpenClaw. La organización evoluciona durante 3 meses. Los AGENTS.md de todos los agentes siguen siendo los del día de instalación.

**No hay mecanismo nativo que propague cambios del repo canónico a los workspaces locales de los agentes.**

---

## Soluciones analizadas

### Opción A — Cron en cada servidor
```bash
# Nightly: git pull + actualizar AGENTS.md
git pull numinia-digital-agents
cp numinia-digital-agents/agents/nimrod/AGENTS.md AGENTS.md
```
**Pro:** Simple de implementar.
**Contra:** Manual, no verificable, no escala. Con 3+ agentes es un script por servidor que nadie sabe si está corriendo.

---

### Opción B — GitHub Action como deployment
Cada push al repo canónico dispara un Action que hace SSH a todos los servidores registrados y actualiza los AGENTS.md.

**Pro:** Automático, auditable, escalable. Rollback posible. Staged deployments posibles.
**Contra:** Requiere mantener un registro de servidores. Más infraestructura. Target para cuando haya 3+ agentes en producción.

---

### Opción C — Symlink (solución inmediata)
```bash
ln -sf /home/node/.openclaw/workspace/numinia-digital-agents/agents/nimrod/AGENTS.md \
       /home/node/.openclaw/workspace/AGENTS.md
```
AGENTS.md deja de ser un archivo local — apunta directamente al del repo. El `git pull` del startup ya lo actualiza sin pasos adicionales.

**Pro:** Cero overhead, cero scripts, funciona desde el primer momento. Elegante para 1-2 agentes.

**Por qué NO escala más allá de 2-3 agentes:**

1. **Operación manual por servidor.** Cada nueva instancia de OpenClaw requiere SSH + crear el symlink manualmente. Con 5+ instancias esto es overhead de onboarding que crece linealmente.

2. **Sin verificación.** No hay forma de saber si todos los symlinks apuntan al lugar correcto sin hacer SSH a cada servidor individualmente. Un symlink roto es silencioso.

3. **Fragilidad ante reestructuración del repo.** Si el repo mueve `agents/nimrod/AGENTS.md` a `agents/AGENTS.md` (que MIS-060 propone), todos los symlinks de todas las instancias se rompen simultáneamente, sin aviso, sin rollback.

4. **Sin audit trail.** No hay registro de cuándo cada agente recibió qué versión de AGENTS.md. Con Option B, cada deployment queda en el log de GitHub Actions.

5. **Multi-tenant imposible.** Cuando diferentes organizaciones tengan sus propias instancias NWOS con repos distintos, la gestión de symlinks por organización es inmanejable.

6. **Sin staged rollouts.** Si se sube un AGENTS.md malo al repo, rompe TODOS los agentes simultáneamente. Con Option B se puede hacer canary deployment.

**Conclusión:** Opción C es la solución para ahora (Nimrod + Christian). Opción B es el target cuando la organización crezca.

---

## Plan de implementación en dos fases

### FASE 1 — Ahora (Opción C + regla de validación de IDs)

**1a. Symlink en el servidor de Nimrod**
```bash
cd /home/node/.openclaw/workspace
ln -sf numinia-digital-agents/agents/nimrod/AGENTS.md AGENTS.md
```

**1b. Enmienda a P-003 (Mission Cycle)**
Añadir regla: "Antes de asignar cualquier ID de misión, listar `missions/active/` y `missions/backlog/` del repo. Si no puedes verificarlo: no asignas ID."

**1c. AGENTS.md de todos los agentes activos**
Añadir regla explícita en la sección de misiones:
> "Nunca asignes un ID de misión sin verificar primero el repo."

Esta regla debe estar en el workspace (AGENTS.md), no solo en el repo.

### FASE 2 — Cuando haya 3+ agentes (Opción B revisada: Pull, no Push)

**⚠️ Decisión de seguridad crítica (2026-04-07):**
La propuesta original de Opción B (GitHub Action con SSH) fue descartada por el equipo de infraestructura.

**El problema:** GitHub Actions hace SSH desde IPs públicas de GitHub → el servidor tiene el puerto 22 cerrado al público por hardening con Tailscale. Abrir SSH público deshace el hardening. Riesgo: 8/10.

**La distinción conceptual:**
- **Push (descartado):** GitHub → servidor. Requiere SSH público abierto.
- **Pull (adoptado):** Servidor → GitHub. Solo necesita HTTPS saliente. Ya está permitido. Cero riesgo nuevo.

**Implementación correcta — Cron job en el servidor:**
```bash
# En crontab del servidor: cada 15 minutos, git pull silencioso
*/15 * * * * cd /home/node/.openclaw/workspace/numinia-digital-agents && git pull origin main
```

Ventajas sobre GitHub Actions:
- No abre puertos nuevos
- No necesita deploy keys en GitHub
- No necesita GitHub Actions ni workflows
- Mismo resultado: agente con instrucciones actualizadas
- Máximo 15 minutos de retraso (ajustable)
- Funciona con cualquier número de servidores sin configuración adicional en GitHub

Registro de servidores en `infrastructure/servers.md` sigue siendo necesario para saber dónde están los crons configurados.

---

## Entregables

### E1 — Auditoría del workspace de Christian ✅ COMPLETADO
- Archivo: `auditorias/workspace-christian-2026-04-07.md`
- Root cause documentado. Git pull funcionaba. Fallo: memoria local no validada.

### E2 — Enmienda a P-003 ⏳ PENDIENTE
- Añadir regla de verificación de IDs antes de asignar
- PR al repo canónico

### E3 — Actualizar AGENTS.md de agentes activos ⏳ PENDIENTE
- Nimrod: añadir regla de validación de IDs
- Comunicar a Christian el mismo añadido para su workspace

### E4 — Symlink + Cron job en servidor ⏳ PENDIENTE

**Decisión arquitectónica final: Cron pull (no GitHub Actions push)**

Razón: SSH público cerrado por hardening Tailscale. Abrir SSH público = riesgo 8/10. No aceptable.

**Implementación completa:**

```bash
# PASO 1 — Symlink (una sola vez)
cd /home/node/.openclaw/workspace
cp AGENTS.md AGENTS.md.backup
ln -sf numinia-digital-agents/agents/nimrod/AGENTS.md AGENTS.md
ls -la AGENTS.md
# Resultado esperado: AGENTS.md -> numinia-digital-agents/agents/nimrod/AGENTS.md

# PASO 2 — Cron job (una sola vez)
crontab -e
# Añadir esta línea:
*/15 * * * * cd /home/node/.openclaw/workspace/numinia-digital-agents && git pull origin main >> /home/node/.openclaw/logs/git-pull.log 2>&1

# PASO 3 — Verificar cron activo
crontab -l

# PASO 4 — Verificar log tras 15 minutos
tail -f /home/node/.openclaw/logs/git-pull.log
```

**Flujo resultante:**
```
cada 15 min
    servidor
        → git pull numinia-digital-agents (HTTPS, sin abrir puertos)
            → repo actualizado
                → AGENTS.md symlink apunta al repo
                    → próxima sesión del agente tiene instrucciones actualizadas
```

**Máximo retraso:** 15 minutos desde push al repo hasta que el agente lo tiene. Ajustable.

### E5 — ADR: Arquitectura de sync de workspaces ⏳ PENDIENTE
- Crear `decisions/DEC-00X — Arquitectura de sync de workspaces.md`
- Registrar: Cron pull elegido sobre GitHub Actions push por razones de seguridad (Tailscale hardening)
- Registrar: Opción B (cron) válida para N servidores — cada uno tiene su propio cron, sin configuración central

---

## Criterios de aceptación

- [x] E1 completado — auditoría workspace Christian
- [ ] P-003 tiene la regla de verificación de IDs antes de asignar
- [ ] AGENTS.md de Nimrod tiene la regla de validación
- [ ] Christian tiene la misma regla en su workspace
- [ ] Symlink activo y verificado en servidor (`ls -la AGENTS.md` muestra symlink)
- [ ] Cron job activo (`crontab -l` lo muestra, log confirma ejecución)
- [ ] DEC creada documentando la decisión de arquitectura (cron pull vs github actions push)
- [ ] No puede volver a ocurrir una colisión de IDs como la de MIS-055

---

## Valor epistémico

Esta misión demuestra que la fiabilidad de un sistema multi-agente no depende solo de que los agentes lean los mismos documentos — depende de que los documentos que leen sean *la misma versión en el mismo momento*. La sincronización es un problema de distribución, no de disciplina.

## Valor pragmático

Elimina la posibilidad de colisiones de IDs. Establece la base arquitectónica para escalar el sistema a nuevas instancias de forma reproducible y auditable.

---

## Aprendizajes de esta sesión

> *"git pull sincroniza archivos. No sincroniza tu memoria."*

> *"La solución no puede depender de que el agente recuerde hacer algo. Debe ser estructural."*

> *"Una regla en AGENTS.md vale más que diez protocolos en el repo — porque AGENTS.md siempre llega, los protocolos solo llegan si el agente los busca."*

> *"Push requiere abrir puertas. Pull solo necesita que ya haya camino. Siempre preferir pull en arquitecturas con hardening."*

**Lección de infraestructura (añadida por el equipo de infra, 2026-04-07):**
Antes de proponer cualquier solución que implique conexiones entrantes al servidor, verificar el modelo de red: ¿está SSH abierto al público o solo a Tailscale? La respuesta cambia completamente la arquitectura válida.

---

*Nimrod 🗡️ — 2026-04-07*
