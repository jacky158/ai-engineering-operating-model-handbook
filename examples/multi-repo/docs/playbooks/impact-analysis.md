---
id: docs-playbooks-impact-analysis
title: Playbook — Impact Analysis (multi repo)
type: playbook
status: draft
owner: TODO
source_of_truth: false
ai_usage: allowed
related_policy: docs/governance/risk-level-policy.md
related_ai_prompt: .ai/prompts/cross-repo-impact-analysis.md
related_ai_workflow: .ai/workflows/cross-repo-impact-analysis.md
---

# Playbook — Impact Analysis (multi repo)

> Hướng dẫn thực thi cho **con người**. Bản operationalize cho AI nằm ở
> `.ai/prompts/cross-repo-impact-analysis.md` + `.ai/workflows/cross-repo-impact-analysis.md`
> (liên kết bằng frontmatter, không copy nội dung — Mục 2.4).

## Purpose
Xác định repo/contract/module nào bị ảnh hưởng trước khi implement, để review và release có đủ context.

## When to use
Khi một initiative bước vào implementation và có khả năng ảnh hưởng nhiều repo hoặc shared contract.

## Roles
- Responsible: Developer / Tech Lead của repo bị ảnh hưởng
- Accountable: Tech Lead initiative
- Consulted: Domain Owner, Security Owner (nếu chạm security/data)
- Informed: Team Lead, QA

## Inputs
- `docs/initiatives/<init>/prd.md`
- `docs/domains/<domain>/business-rules.md`, `api-contracts.md`
- `docs/workspace/cross-repo-dependencies.md`

## Required context
Xem `.ai/rules/context-loading-policy.md`; với high-risk theo Mục 16.3.

## Steps
1. Liệt kê repo bị ảnh hưởng và lý do.
2. Xác định contract thay đổi (REST/event/shared package/DB schema/authz).
3. Ghi per-repo impact: module, layer, data/API/security, local evidence.
4. Phân loại risk theo `docs/governance/risk-level-policy.md`.
5. Xác định reviewer bắt buộc theo repo/domain.
6. Ghi thứ tự deploy và cách rollback từng repo.

## Outputs
`docs/initiatives/<init>/repo-impact.md` (theo template
`docs/templates/impact-analysis-template.md`).

## Quality gates
Gate theo risk-level-policy + phần cross-repo trong `docs/governance/cross-repo-change-policy.md`.
Không hard-code lại danh sách gate ở đây.

## Evidence
`repo-impact.md` đã review; link tới per-repo evidence (`backend/docs/testing.md`, ...).

## Stop conditions
Dừng nếu: contract source-of-truth chưa rõ; thiếu domain rule; chạm production data chưa có approval.

## Escalation
Vượt thẩm quyền repo → escalate Architecture Owner / Security Owner (Handbook Ch 8.3).
