---
id: "DEC-003"
title: "Arbitrum como blockchain de Numinia"
type: decision
status: provisional
version: "1.0.0"
created: "2026-04-05"
updated: "2026-04-05"
author: "pablo-fm"
owner: "oracle"
tags: [decisions, product, tech, blockchain, arbitrum]
area: "Producto / Tech"
pending_dark_council: true
superseded_by: null
license: "CC0-1.0"
---

# DEC-003 — Arbitrum como blockchain de Numinia

> ⚠️ **Estado: Provisional** — Pendiente de ratificación en Dark Council

## Contexto

Numinia necesita una blockchain para NFTs, smart contracts de sellos y Digital Goods.

## Decisión

**Arbitrum One (L2 sobre Ethereum).**

## Por qué

- Fees muy bajos — viable para microtransacciones
- EVM compatible — stack conocido, Solidity, herramientas maduras
- Ecosistema de grants activo (AGV, DAO Grants)
- Propiedad de su comunidad (DAO governance)

## Alternativas descartadas

- **Ethereum mainnet** — fees prohibitivos para el caso de uso
- **Solana** — ecosistema diferente, menos tooling EVM
- **Polygon** — similar pero ecosistema de grants menos activo en gaming
- **Base / Optimism** — válidos, menor tracción en gaming

## Pros / Contras

**Pros:** Fees bajos · Grants disponibles · EVM conocido  
**Contras:** Menor velocidad que Solana · Dependencia del ecosistema Ethereum

---

*Oracle: Pablo FM — 2026-04-05*
