---
id: "ops-governance"
title: "Governance — Operations"
type: protocol
status: active
version: "1.0.0"
created: "2026-04-06T00:00:00Z"
author: "nimrod"
owner: "oracle"
tags: [operations, governance]
license: "CC0-1.0"
---

# Governance — Operations

See root GOVERNANCE.md for the complete permissions table.

## Quick reference — Who can do what

**Oracle (Pablo FM):** Everything. Final authority.
**Custodian (Adonaz):** Document management, INDEX files, CHANGELOG.
**Active Agent (Nimrod):** Own files, assigned missions, reports.
**System (CI/CD):** Auto-merge of daily reports only.

## Critical constraint

`canon/` is immutable. No exceptions. No overrides. This is enforced at the technical level via CODEOWNERS.
