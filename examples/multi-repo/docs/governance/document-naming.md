---
id: docs-governance-document-naming
title: Document Naming Policy
type: governance
purpose: standard
status: draft
owner: engineering-platform
source_of_truth: false
scope: global
ai_usage: allowed
---

# Document Naming Policy

Source of truth cho **cách đặt tên** file, folder và `id`. Topology chỉ nêu format tối thiểu (Mục 9).

## 1. Initiative & artifact có prefix
```text
INIT-<YEAR>-<NUMBER>-<short-slug>/
rfc/RFC-<YEAR>-<NUMBER>-<short-slug>.md
adr/ADR-<YEAR>-<NUMBER>-<short-slug>.md
PRD-<YEAR>-<NUMBER>   PROP-<YEAR>-<NUMBER>   PBR-<YEAR>-<NUMBER>
```

## 2. Tên ổn định trong initiative
`product-brief.md · proposal.md · prd.md · impact-analysis.md · repo-impact.md · test-plan.md · release-note.md · decision-log.md`

## 3. Singleton & ID ngắn
Governance/domain/repo-level doc dùng `<PREFIX>-<slug>`, ví dụ `GOV-document-structure`, `DOMAIN-permission-business-rules`.

## 4. AI-facing derivative
Phải phân biệt được với bản gốc khi grep. TODO: chốt hậu tố (ví dụ `-context-map.md`) và reserved names.

## 5. TODO
- Bảng prefix đầy đủ theo `type`.
- Quy tắc numbering (per-year, zero-pad), slug (kebab, độ dài).
- Exception và migration rule.

## Liên quan
`document-standard.md`, `document-structure.md`.
