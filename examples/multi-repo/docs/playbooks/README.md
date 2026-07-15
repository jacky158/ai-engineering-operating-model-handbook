---
id: docs-playbooks-README
title: Playbooks — index
status: draft
owner: engineering-leadership
source_of_truth: false
ai_usage: allowed
---

# Playbooks

Hướng dẫn thực thi **cho con người** theo AIOM. Playbook trả lời *"làm thế nào"*; Handbook trả lời *"vì sao/là gì"*;
policy trong `../governance/` quyết định *"điều gì bắt buộc"*.

> Playbook (người) **tách khỏi** workflow (AI) ở `../../.ai/workflows/`. Một playbook có thể được operationalize
> thành `.ai/prompt` + `.ai/workflow`; liên kết bằng frontmatter, **không copy** nội dung (Mục 2.4).

## Danh sách

| Playbook | Dùng khi | AI asset liên quan |
| --- | --- | --- |
| [`requirement-review.md`](./requirement-review.md) | Trước khi implement, làm rõ requirement & assumption | `.ai/prompts/prd-review.md` |
| [`impact-analysis.md`](./impact-analysis.md) | Xác định repo/contract/module bị ảnh hưởng (multi repo) | `.ai/prompts/cross-repo-impact-analysis.md`, `.ai/workflows/cross-repo-impact-analysis.md` |
| [`code-review.md`](./code-review.md) | Review diff/PR trước merge | `.ai/prompts/code-review.md` |
| [`release-precheck.md`](./release-precheck.md) | Trước khi release/deploy | `.ai/prompts/release-precheck.md`, `.ai/workflows/release-flow.md` |

## Khung chuẩn của một playbook

Mỗi playbook có: Purpose · When to use · Roles · Inputs · Required context · Steps · Outputs ·
Quality gates · Evidence · Stop conditions · Escalation.

## Nguyên tắc

- Không hard-code danh sách gate trong playbook; trỏ về `../governance/risk-level-policy.md` và `quality-gates.md`.
- Playbook nêu *stop conditions* và *escalation* rõ để người thực thi không tự quyết vượt thẩm quyền.
- Tạo playbook theo nhu cầu thật, không tạo file rỗng chỉ để đủ danh sách.
