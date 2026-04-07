---
id: "MIS-00056"
title: "i18n — Documentación y sistema bilingüe ES + EN"
type: mission
status: backlog
version: "1.0.0"
created: "2026-04-07T00:00:00Z"
updated: "2026-04-07T00:00:00Z"
author: "pablo-fm"
owner: "oracle"
tags: [documentation, i18n, spanish, english, nwos]
license: "CC0-1.0"
area: "Documentación"
guild: "Exegetas"
tipo: "híbrido"
priority: "high"
effort: "L"
---

# MIS-056 — i18n — Documentación y sistema bilingüe ES + EN

**Area:** Documentación · **Gremio:** Exegetas · **Tipo:** 🔀 Híbrido · **Prioridad:** 🟠 Alta · **Esfuerzo:** L

---

## Origen

Decisión tomada el 2026-04-07. Todo el sistema NWOS — documentación, páginas web, archivos .md del repo — debe estar disponible en español e inglés desde ahora.

El español es el idioma operativo interno. El inglés es el idioma de adopción externa.

Idiomas futuros (no inmediatos): 日本語, 한국어, 中文, Português.

---

## Historia

Como organización que construye en público y quiere adopción internacional, quiero que toda la documentación del NWOS esté en español e inglés, para que cualquier equipo del mundo pueda leer y adoptar el sistema sin barreras de idioma.

---

## Criterios de aceptación

### Repo (numinia-digital-agents)
- [ ] Convención de naming definida: `archivo.md` (ES) + `archivo.en.md` (EN) — o estructura de carpetas `es/` + `en/`
- [ ] README.md en inglés (ya existe) + README.es.md en español
- [ ] SOUL.md, OPERATOR.md de cada agente en ambos idiomas
- [ ] Misiones nuevas desde ahora: frontmatter bilingüe + cuerpo en ES, traducción EN al cerrar
- [ ] Documentos existentes: traducción progresiva por orden de importancia

### Web (pablofm.com)
- [ ] Decisión de arquitectura i18n: Astro i18n nativo vs. rutas `/es/` vs. toggle de idioma
- [ ] Páginas prioritarias en EN: /nwos, /wardley, /idioma, /agente
- [ ] Toggle de idioma visible en la navegación
- [ ] Páginas operativas (misiones, reportes, decisiones) pueden quedarse en ES

### Estándar desde ahora
- [ ] Toda página nueva en pablofm.com: versión ES + EN
- [ ] Todo documento nuevo en el repo: al menos el frontmatter en EN, cuerpo en ES

---

## Valor epistémico

El idioma en que documenta un sistema define quién puede contribuir a él. ES + EN desde el principio evita deuda técnica de traducción y abre el sistema al mercado anglófono desde el primer día.

## Valor pragmático

- Adopción internacional sin fricción
- Inversores, partners y clientes en inglés pueden leer el sistema directamente
- Consistente con CC0 — si construimos en abierto, construimos para todos

---

## Prioridad de traducción (orden sugerido)

1. /nwos — ya en inglés ✅
2. /wardley — ya en inglés ✅  
3. /agente — nuevo, construir en ES + EN simultáneo
4. /idioma — traducir a EN
5. README.md del repo — ya en inglés ✅
6. WARDLEY-MAP.md — ya en inglés ✅
7. Misiones críticas (MIS-001 a 010) — traducir
8. Resto progresivo

---

*Nimrod 🗡️ — 2026-04-07*
