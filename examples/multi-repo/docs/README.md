---
id: docs-README
title: Workspace docs — mục lục & điều hướng
status: draft
owner: engineering-platform
source_of_truth: false
ai_usage: allowed
---

# Workspace `docs/` (multi repo)

Đây là **control plane cấp workspace** — tài liệu chính thức cho người. `.ai/` (cùng cấp) chỉ tóm tắt/định
tuyến cho AI, **không override** `docs/`. Cấu trúc theo [`aiom-document-structure.md`](../../../aiom-document-structure.md)
(Mục 4.3 + 2.3).

## Hai lớp trong `docs/`

| Lớp | Thư mục | Trả lời câu hỏi |
| --- | --- | --- |
| **Operating Model** — cách làm | `operating-model/` `platform/` `handbook/` `playbooks/` `templates/` `checklists/` | Team cần hiểu gì, theo nguyên tắc/gate nào |
| **Delivery** — đang làm gì | `workspace/` `initiatives/` `domains/` `reference/` `governance/` `registry/` | Đang làm gì, ảnh hưởng đâu |

## Điều hướng nhanh

| Cần gì | Vào đâu |
| --- | --- |
| Hiểu Operating Model, nguyên tắc, role | `operating-model/` |
| Capability & tool được duyệt | `platform/`, `platform/approved-tools.md` |
| Onboarding / Why–What | `handbook/` |
| Các bước thực thi cho người | `playbooks/` |
| Khuôn mẫu tạo artifact | `templates/` |
| Checklist xác minh | `checklists/` |
| Tổng quan workspace, repo map, ownership | `workspace/` |
| Tài liệu một thay đổi cụ thể | `initiatives/<INIT>/` |
| Business rule dài hạn | `domains/<domain>/` |
| Chuẩn architecture/coding/testing/release | `reference/` |
| Policy (risk, security, gate, AI governance) | `governance/` |
| Index & mapping để tra cứu | `registry/` |

## Quy tắc quan trọng

- `docs/` là source of truth cho người; sửa ở đây trước, rồi cập nhật `.ai/` liên quan (hoặc đánh dấu `stale`).
- **Playbook (người) ở `playbooks/`** tách khỏi **workflow (AI) ở `.ai/workflows/`** — liên kết bằng frontmatter, không copy (Mục 2.4).
- Policy authoritative nằm ở `governance/`; `operating-model/governance/` chỉ là model/rationale.
- Multi repo: PRD và RFC/ADR cấp initiative/cross-repo đặt ở workspace-level; repo con (`../backend/docs/`, `../frontend/docs/`) chỉ giữ tài liệu local (Mục 4.5).
- Không tạo file rỗng chỉ để thỏa cấu trúc; tạo tài liệu theo lifecycle của initiative (Mục 3.2, 5.1).

## Repo con (execution area)

- [`../backend/docs/`](../backend/docs/README.md) — build, test, module, migration local
- [`../frontend/docs/`](../frontend/docs/README.md) — build, test, module, state management local

## Liên quan

- [`aiom-document-structure.md`](../../../aiom-document-structure.md) — topology standard
- [`../CLAUDE.md`](../CLAUDE.md), [`../AGENTS.md`](../AGENTS.md) — adapter entry point cho AI tool
- [`../README.md`](../README.md) — giới thiệu scaffold này
