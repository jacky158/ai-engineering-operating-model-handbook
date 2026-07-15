---
id: docs-governance-cross-repo-change-policy
title: Cross-Repo Change Policy
type: governance
purpose: policy
status: draft
owner: engineering-platform
source_of_truth: false
scope: workspace
ai_usage: allowed
---

# Cross-Repo Change Policy

**Chỉ dùng cho multi repo.** Source of truth cho thay đổi ảnh hưởng nhiều repo — bổ sung cho
`risk-level-policy.md` và `quality-gates.md` (Mục 4.7).

## 1. Khi nào là cross-repo change (TODO chốt)
Thay đổi chạm shared contract (REST/event/shared package/DB schema/authz) hoặc cần deploy phối hợp nhiều repo.

## 2. Contract source of truth
Mỗi contract có một repo/domain là source of truth. TODO: bảng contract ↔ owner repo.

## 3. Reviewer bắt buộc
Theo repo/domain bị ảnh hưởng (từ `repo-impact.md`). High-risk cần thêm Architecture/Security Owner.

## 4. PR & deploy
- Chia PR theo repo.
- **Thứ tự merge/deploy** để giữ backward compatibility (ví dụ provider trước consumer).
- Rollback khi chỉ một repo lỗi.

## 5. Registry & map
Cập nhật `../registry/repo-index.md`, `../workspace/repo-map.md`, `../workspace/cross-repo-dependencies.md`
trong cùng change.

## 6. AI-facing
Bản operationalize: `.ai/rules/cross-repo-change-rule.md` (trỏ về file này).

## Liên quan
`risk-level-policy.md`, `quality-gates.md`, `../workspace/release-flow.md`, `../playbooks/impact-analysis.md`.
