---
id: AI-rules-document-naming-policy
title: document-naming-policy
type: ai-asset
status: draft
owner: ai-platform-owner
source_of_truth: false
source_context:
  - docs/governance/document-naming.md
source_updated_at: 2026-11-23
source_revision:
stale: false
---

# document-naming-policy

> AI-facing scaffold (multi-repo). Tóm tắt/định tuyến; trỏ về source of truth trong `docs/`, KHÔNG override.

## Naming quick reference

- Initiative folder: `INIT-<YEAR>-<TOKEN>-<short-slug>/`. `<TOKEN>` là 6 chữ cái in hoa ngẫu nhiên
  (`LC_ALL=C tr -dc 'A-Z' </dev/urandom | head -c 6`), không phải số thứ tự và không tự chọn. Kiểm tra chưa dùng
  (`grep -r <TOKEN> docs/initiatives docs/registry`) trước khi tạo.
- PRD: `PRD-<YEAR>-<TOKEN>`. RFC/ADR: `rfc/RFC-<YEAR>-<TOKEN>[x]-<slug>.md`, `adr/ADR-<YEAR>-<TOKEN>[x]-<slug>.md`;
  `[x]` là chữ thường (`b`, `c`, …) cho RFC/ADR thứ hai trở đi.
- ID dạng số có sẵn: giữ nguyên, không đổi tên, không cấp thêm số mới.
