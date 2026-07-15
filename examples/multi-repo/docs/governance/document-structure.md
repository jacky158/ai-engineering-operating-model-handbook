---
id: docs-governance-document-structure
title: Document Structure Policy
type: governance
purpose: standard
status: draft
owner: engineering-platform
source_of_truth: false        # → true khi accepted
scope: global
ai_usage: allowed
---

# Document Structure Policy

> Vị trí canonical của topology standard. Nội dung đầy đủ hiện đang staging tại
> [`aiom-document-structure.md`](../../../../aiom-document-structure.md); khi `accepted`, chuyển về file này.

## Phạm vi
Quy định topology thư mục và vị trí canonical của tài liệu cho single-repo và multi-repo.
**Không** là source of truth chi tiết cho naming, metadata, risk gate, security — xem các policy tương ứng.

## Nội dung bắt buộc (tham chiếu topology standard)
- Ba tầng / hai lớp: Operating Model layer vs Delivery layer trong `docs/`; `.ai/` operating layer; execution area.
- Cấu trúc single repo (Mục 3) và multi repo (Mục 4).
- Vai trò `docs/initiatives|domains|reference|governance|registry/` và `.ai/`.
- Quy tắc tránh duplicate docs↔.ai, tool-adapter layer.

## Liên quan
`document-standard.md`, `document-naming.md`, `quality-gates.md`, `risk-level-policy.md`,
`ai-governance.md`, `security-policy.md`, `cross-repo-change-policy.md`.

<!-- TODO: khi promote — copy nội dung từ aiom-document-structure.md, set status: accepted, source_of_truth: true, approved_by, accepted_at. -->
