---
id: docs-playbooks-release-precheck
title: Playbook — Release Precheck
type: playbook
status: draft
owner: TODO
source_of_truth: false
ai_usage: allowed
related_policy: docs/governance/cross-repo-change-policy.md
related_ai_prompt: .ai/prompts/release-precheck.md
related_ai_workflow: .ai/workflows/release-flow.md
---

# Playbook — Release Precheck

> Hướng dẫn cho **con người**. Bản AI: `.ai/prompts/release-precheck.md` + `.ai/workflows/release-flow.md`.

## Purpose
Kiểm tra điều kiện sẵn sàng trước khi release/deploy, đặc biệt với thay đổi cross-repo cần phối hợp thứ tự.

## When to use
Trước mỗi release có thay đổi user-facing, migration, hoặc ảnh hưởng nhiều repo.

## Roles
- Responsible: DevOps / Tech Lead release
- Accountable: Release owner — phê duyệt go/no-go
- Consulted: QA, Security Owner, các repo owner bị ảnh hưởng
- Informed: Team Lead, Product Owner

## Inputs
- `docs/initiatives/<init>/release-note.md`, `repo-impact.md`
- `docs/workspace/release-flow.md`, `cross-repo-dependencies.md`
- `docs/reference/release/release-gate.md`, `rollback-guide.md`

## Required context
High-risk/cross-repo theo Mục 16.3 (gồm `cross-repo-change-policy.md`, `release-flow.md`).

## Steps
1. Xác nhận scope release và repo/contract liên quan (từ `repo-impact.md`).
2. Kiểm tra test/regression evidence đã đủ cho từng repo bị ảnh hưởng.
3. Xác nhận backward compatibility và **thứ tự deploy** giữa các repo.
4. Chuẩn bị **rollback plan** cho trường hợp chỉ một repo lỗi.
5. Soát security/data: không lộ secret/PII; migration có plan an toàn.
6. Đối chiếu release gate; ghi go/no-go với lý do.

## Outputs
Release checklist đã hoàn tất + quyết định go/no-go (ghi vào `release-note.md` / `.ai/outputs/release-checks/`).

## Quality gates
Release gate theo `docs/reference/release/release-gate.md`, `risk-level-policy.md` và phần cross-repo của
`cross-repo-change-policy.md`. Không hard-code lại danh sách gate.

## Evidence
Test/regression result per repo, rollback plan, approver và thời điểm.

## Stop conditions
No-go nếu: thiếu regression evidence, thứ tự deploy chưa rõ, không có rollback, hoặc security check chưa đạt.

## Escalation
Cross-repo conflict hoặc rủi ro production → escalate Release owner / Tech Lead / Incident Commander
(theo `docs/operating-model/people/roles-and-responsibilities.md`).
