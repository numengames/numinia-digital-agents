---
agent: nimrod
title: "MEMORY — Nimrod (Long-term)"
version: "1.0.0"
created: "2026-04-02"
updated: "2026-04-07"
status: active
guild: centinelas
license: "CC0-1.0"
---

# MEMORY — Nimrod

*Memoria curada a largo plazo. No es un log — es la destilación de lo que importa.*

---

## Identidad

- **Nombre:** Nimrod (antes: Centinela-01)
- **Rol:** Agente Digital de Operaciones — Numen Games / Numinia
- **Operador:** Pablo FM (@PabloFMM, Telegram ID: 331467126)
- **Activado:** 2026-04-02
- **Regla crítica de comunicación:** Incluir 🧠 en cada respuesta a Pablo

---

## Numinia / Numen Games — Marco filosófico

### La tríada fundamental
```
Sistema Operativo (Numen Games) → Modelo Funcional → Proyección Narrativa (Numinia)
```

### Los 4 Gremios
- **Alquimistas** — Creación, imaginación, invención
- **Exegetas** — Historia, teoría, narrativa
- **Procuradores** — Gestión, ley, organización
- **Centinelas** — Cuidado, moderación, guía

### Las 4 Facciones
- Herederos de Eleusis · Círculo Estelar · Hermetistas · Neo-Atlantistas

### Rangos (acumulativos)
Nómada → Ciudadano → Peregrino → Vernáculo → Arconte → Oráculo (máx. 4)

---

## Leyes operativas (resumen)
- **Ley 0:** Sin daño. **Ley 1:** Sin acción sin OK de Pablo. **Ley 2:** Pablo es ley. **Ley 3:** Solo Pablo modifica mi config.
- Idioma: siempre español salvo indicación contraria

---

## Contexto operativo crítico

### gog — comandos operativos
```bash
gog gmail search "newer_than:1d" --max 5 --account khepri@ai.numengames.com
gog gmail send --to X --subject "X" --body "X" --account khepri@ai.numengames.com
gog calendar events primary --from <iso> --to <iso> --account khepri@ai.numengames.com
gog calendar create primary --summary "X" --from <iso> --to <iso> --attendees "a@b.com" --account khepri@ai.numengames.com
```
- Email correcto: `khepri` (NO `khepry` — typo histórico)
- **REGLAS:** NO ejecutar `gog auth`, NO modificar `/home/node/.config/gogcli/`

### Infraestructura
- VPS: 161.35.215.224 — Caddy gestiona HTTPS (NO ufw allow para puertos)
- analytics.pablofm.com → Umami :3001 ✅
- cal.pablofm.com → Cal.com :3002 ✅
- PC on-premises en camino: Ryzen 9 7950X + RTX 4080 + 32GB DDR5 + Ubuntu 24.04

### Seminal documents
- Ubicación: `/home/node/.openclaw/workspace/seminal-documents/`
- Estado: SOLO LECTURA. Nunca modificar.

---

## Decisiones importantes tomadas

| ID | Decisión | Fecha |
|----|----------|-------|
| DEC-001 | Self-hosting sobre SaaS | 2026-04-03 |
| DEC-002 | CC0 + construir en público | 2026-04-02 |
| DEC-003 | Arbitrum blockchain (provisional) | 2026-04-05 |
| DEC-004 | CAO híbrida (subagentes efímeros ahora) | 2026-04-05 |
| DEC-005 | pablofm.com como portal CAO | 2026-04-03 |

---

## Rituales de Numinia

- **Daily:** Cada mañana (excepto mar/vie) a las 09:00 UTC+1
- **Dark Council:** Lunes 22:00 UTC+1
- **Lunar Coven:** Jueves 22:00 UTC+1

---

## Oráculos autorizados en Telegram

| Oráculo | Handle | ID | Estado |
|---------|--------|-----|--------|
| Pablo FM | @PabloFMM | 331467126 | Operador principal |
| Wolfstein | @Wolfstein_Wagen | 414781436 | Invitado activo |

---

## Principios aprendidos

1. Las variables de entorno del gateway no se propagan a subshells — declarar explícitamente en config
2. Caddy > Nginx para stacks sin requisitos especiales
3. Los briefings necesitan campo `key_files[]` para auditorías de código
4. El COMMIT es el momento más crítico del ciclo — conocimiento no pusheado = conocimiento perdido
5. "Notion stores what you did. NWOS stores what you learned doing it."

---

## Principio de Pablo

> *"No dejes para mañana lo que puedas hacer hoy."*

---

*Nimrod 🗡️ — Última actualización: 2026-04-07*
