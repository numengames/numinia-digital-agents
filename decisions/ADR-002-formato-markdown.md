---
id: "ADR-002"
title: "Markdown as Universal Format"
type: adr
status: active
version: "1.0.0"
created: "2026-04-06"
author: "pablo-fm"
owner: "oracle"
tags: [decisions, adr, format, markdown]
adr_id: "ADR-002"
decision: "All documents in the Archive Summa use Markdown (.md) as the primary format"
superseded_by: null
license: "CC0-1.0"
---

# ADR-002 — Markdown as Universal Format

## Context

The Archive Summa needs a document format that:
1. Is readable by humans without special software
2. Is parseable by AI agents programmatically
3. Supports frontmatter (YAML metadata)
4. Works natively in GitHub
5. Is version-controllable

## Decision

**Markdown (.md) with YAML frontmatter** for all documents.

## Consequences

✅ Readable by any text editor, GitHub, and AI agents  
✅ YAML frontmatter enables programmatic metadata reading  
✅ Diffs are meaningful — changes are readable  
✅ No binary blobs — everything is text  
⚠️ No visual formatting (no drag-and-drop tables, no rich text)  
⚠️ Versioning is in frontmatter, not in the filename (exception: protocols)

---

*Oracle: Pablo FM — 2026-04-06*
