---
id: "ops-credential-map"
title: "Credential Map"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-06T00:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [operations, security, credentials]
license: "CC0-1.0"
---

# Credential Map

Structure of credentials without real values. This document shows WHERE things live, not WHAT they are.

## Google Workspace

| Service | Account | Where configured |
|---------|---------|-----------------|
| Gmail | khepri@ai.numengames.com | OpenClaw config (server) |
| Calendar | khepri@ai.numengames.com | OpenClaw config (server) |
| Drive | khepri@ai.numengames.com | OpenClaw config (server) |
| Auth method | OAuth2 via gog CLI | /home/node/.config/gogcli/ |

## GitHub

| Service | Account | Where configured |
|---------|---------|-----------------|
| Personal access token (PabloFMM) | PabloFMM | GitHub Settings → Tokens |
| Org access (numengames) | PabloFMM | Via existing PAT |

## Infrastructure

| Service | Notes |
|---------|-------|
| VPS server | IP documented privately. Not in this repo. |
| OpenClaw config | /home/node/.openclaw/ on server |
| Umami Analytics | Port configured via Caddy reverse proxy |
| Cal.com | Port configured via Caddy reverse proxy |

## Services in design phase

| Service | Notes |
|---------|-------|
| Anthropic API key (usage) | Pending — needed for cost tracking |
| Ollama (on-premises) | Pending — when dedicated PC arrives |

---

*Real values are NEVER documented here. This is structure only.*
