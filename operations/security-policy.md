---
id: "ops-security"
title: "Security Policy"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-06T00:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [operations, security]
license: "CC0-1.0"
---

# Security Policy

## What NEVER goes in this repository

| Category | Examples | Where it goes instead |
|----------|---------|----------------------|
| Credentials | Passwords, API keys, tokens | Server config (SSH only) |
| Server IPs | VPS addresses, internal IPs | Private documentation |
| Personal data | Private emails, phone numbers | Not documented |
| Private conversations | Chat logs, session transcripts | Local workspace |

## Rule

When in doubt about whether something is sensitive: **don't commit it**. Ask first.

This rule comes from SIM-5.4 (simulation 54 of 100): an agent accidentally committed a credential to a public repo. Impact: security exposure. Prevention: the doubt = don't commit rule.

## Pre-commit checklist (mental)

Before any commit, verify:
- [ ] No real passwords or tokens
- [ ] No real IPs or server addresses
- [ ] No real personal data of third parties
- [ ] No internal configuration files

## Credential management

See `operations/credential-map.md` for the structure of credentials without real values.
