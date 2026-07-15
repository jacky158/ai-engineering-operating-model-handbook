---
id: docs-governance-document-standard
title: Document Standard Policy
type: governance
purpose: standard
status: draft
owner: engineering-platform
source_of_truth: false
scope: global
ai_usage: allowed
---

# Document Standard Policy

Source of truth cho **metadata schema, validation và lifecycle** của tài liệu. Topology chỉ nêu field tối thiểu;
chi tiết required/optional, enum và transition rule thuộc file này (Mục 10–11 của topology standard).

## 1. Metadata schema
Bảng field với required/optional theo `type`. TODO điền đầy đủ.

| Field | Áp dụng cho | Required? | Enum/format |
| --- | --- | --- | --- |
| `id`, `title`, `type`, `status`, `owner` | mọi doc | required | — |
| `created_at`, `updated_at` | mọi doc | required | YYYY-MM-DD |
| `canonical_path` | doc chính thức | required | path |
| `source_of_truth` | mọi doc | required | true chỉ khi `accepted` |
| `source_policy` / `source_context` / `source_updated_at` / `source_revision` / `stale` | AI-facing derivative | required | — |
| `version` / `last_evaluated_at` / `evaluation_dataset` / `success_rate` | AI asset (prompt/workflow/agent) | conditional | — |
| `approved_by`, `accepted_at` | khi promote sang accepted | required | — |

<!-- TODO: bổ sung ý nghĩa và validation từng field. -->

## 2. Lifecycle & status enum
`draft → proposed → accepted → (deprecated | superseded)`; `rejected`. AI asset có thể thêm `pilot`.

| Transition | Điều kiện |
| --- | --- |
| → accepted | human approval, ghi `approved_by` + `accepted_at`, `source_of_truth: true` |
| → superseded | ghi `superseded_by` |

## 3. Validation
TODO: rule cho CI (frontmatter bắt buộc, enum hợp lệ, stale detection, registry đồng bộ frontmatter).

## Liên quan
`document-structure.md`, `document-naming.md`.
