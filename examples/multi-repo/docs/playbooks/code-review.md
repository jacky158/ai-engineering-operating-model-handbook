---
id: docs-playbooks-code-review
title: Playbook — Code Review
type: playbook
status: draft
owner: TODO
source_of_truth: false
ai_usage: allowed
related_policy: docs/governance/quality-gates.md
related_ai_prompt: .ai/prompts/code-review.md
---

# Playbook — Code Review

> Hướng dẫn cho **con người**. Bản AI: `.ai/prompts/code-review.md` (agent: `.ai/agents/reviewer.md`).

## Purpose
Review diff/PR để bắt lỗi correctness, regression và security sớm, với requirement/impact context — không trở thành bottleneck.

## When to use
Khi có PR chờ merge; cross-repo change cần soát backward compatibility.

## Roles
- Responsible: Reviewer (Tech Lead / Senior Dev của repo)
- Accountable: Reviewer approve — chịu trách nhiệm cho quyết định merge
- Consulted: Security Owner (nếu chạm security/data)
- Informed: Author, QA

## Inputs
- Diff/PR + task gốc; `docs/initiatives/<init>/prd.md`, `repo-impact.md`
- `docs/reference/engineering/coding-standard.md`, `docs/governance/security-policy.md`

## Required context
Load requirement + impact trước khi review (Mục 16.2); high-risk theo Mục 16.3.

## Steps
1. Nạp requirement/impact context — không review "mù".
2. Khớp scope: diff có đúng scope task không.
3. Correctness & regression: logic, edge case, backward compatibility với consumer/contract.
4. Security: secret/PII, authz nếu chạm permission (theo `security-policy.md`).
5. Evidence: có test tương ứng và đã chạy chưa; claim không evidence → chưa xác minh.
6. Depth theo risk; phân biệt finding *confirmed* vs *nghi ngờ*.

## Outputs
Review comment + kết luận: approve / cần sửa / cần thêm approval (high-risk).

## Quality gates
Review gate theo `docs/governance/quality-gates.md` và `risk-level-policy.md`.

## Evidence
Findings đã xử lý, test đã chạy, approver và lý do quyết định.

## Stop conditions
Dừng nếu thiếu requirement/impact context, hoặc evidence test chưa có cho change high-risk.

## Escalation
AI review **không** thay human approval. High-risk hoặc chạm security/contract → escalate Tech Lead / Security Owner
(theo `docs/operating-model/people/roles-and-responsibilities.md`).
