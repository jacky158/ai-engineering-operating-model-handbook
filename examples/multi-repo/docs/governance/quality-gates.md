---
id: docs-governance-quality-gates
title: Quality Gates Policy
type: governance
purpose: policy
status: draft
owner: engineering-leadership
source_of_truth: false
scope: global
ai_usage: allowed
---

# Quality Gates Policy

Source of truth cho **quality gate** — điều kiện phải đạt trước khi chuyển bước. Gate gắn với risk
(`risk-level-policy.md`), không đồng nhất cho mọi task.

## 1. Gate theo giai đoạn SDLC (TODO chốt điều kiện)
| Gate | Trước bước | Điều kiện tối thiểu | Evidence |
| --- | --- | --- | --- |
| Requirement clarity | implementation | acceptance criteria testable, assumption đã chốt | review note |
| Design approval | implementation (high-risk) | RFC/ADR approved | ADR link |
| Implementation readiness | code | scope rõ, impact analysis xong | impact-analysis/repo-impact |
| Code review | merge | findings xử lý, test đã chạy | PR review + test result |
| Test readiness | release | coverage vs risk đạt, oracle có nguồn | test-plan + result |
| Release readiness | deploy | regression + rollback plan + security check | release checklist |

## 2. Nguyên tắc
- Gate quá yếu → tăng failure risk; quá nặng → tạo bypass. Cân theo risk và review bằng evidence.
- AI review **không** thay human approval ở gate high-risk.
- Không hard-code danh sách gate trong template/prompt; trỏ về file này.

## 3. Ba lớp thực thi
`docs/` (policy) · `.ai/rules/quality-gate-policy.md` (AI-facing) · CI/CD (gate tự động).

## Liên quan
`risk-level-policy.md`, `../reference/testing/testing-strategy.md`, `../reference/release/release-gate.md`.
