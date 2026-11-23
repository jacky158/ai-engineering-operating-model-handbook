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
INIT-<YEAR>-<TOKEN>-<short-slug>/
rfc/RFC-<YEAR>-<TOKEN>[x]-<short-slug>.md
adr/ADR-<YEAR>-<TOKEN>[x]-<short-slug>.md
PRD-<YEAR>-<TOKEN>   PROP-<YEAR>-<TOKEN>   PBR-<YEAR>-<TOKEN>
```

- `<TOKEN>` là **6 chữ cái in hoa ngẫu nhiên `A`–`Z`** (ví dụ `KQZTBM`), **không phải số thứ tự**. Số thứ tự phải
  được cấp từ một trạng thái dùng chung; các branch song song không thấy nhau nên hai người (hoặc hai AI session) có
  thể cùng lấy một số và phải đổi tên toàn bộ file khi merge.
- Sinh token bằng lệnh, không tự chọn: `LC_ALL=C tr -dc 'A-Z' </dev/urandom | head -c 6`. Trước khi dùng, kiểm tra
  chưa tồn tại: `grep -r "<TOKEN>" docs/initiatives docs/registry` không trả kết quả. Token không bao giờ dùng lại.
- Tài liệu trong initiative dùng chung token. RFC/ADR thứ hai trở đi thêm một chữ thường ngay sau token
  (`ADR-2026-KQZTBMb`, `…c`). Tài liệu khác (`test-plan.md`, `repo-impact.md`, …) có ID riêng trên cùng token.
- Thứ tự thời gian lấy từ `created_at`, không lấy từ ID.
- Workspace đã có ID dạng số từ trước thì giữ nguyên các ID đó, không đổi tên và không cấp thêm số mới.
- Pattern kiểm tra folder: `^INIT-\d{4}-(\d{3}|[A-Z]{6})-[a-z0-9]+(-[a-z0-9]+)*$`.

## 2. Tên ổn định trong initiative
`product-brief.md · proposal.md · prd.md · impact-analysis.md · repo-impact.md · test-plan.md · release-note.md · decision-log.md`

## 3. Singleton & ID ngắn
Governance/domain/repo-level doc dùng `<PREFIX>-<slug>`, ví dụ `GOV-document-structure`, `DOMAIN-permission-business-rules`.

## 4. AI-facing derivative
Phải phân biệt được với bản gốc khi grep. TODO: chốt hậu tố (ví dụ `-context-map.md`) và reserved names.

## 5. TODO
- Bảng prefix đầy đủ theo `type`.
- Quy tắc slug (kebab, độ dài).
- Exception và migration rule.

## Liên quan
`document-standard.md`, `document-structure.md`.
