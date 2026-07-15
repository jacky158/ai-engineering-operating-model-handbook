---
id: docs-governance-ai-governance
title: AI Governance Policy
type: governance
purpose: policy
status: draft
owner: ai-platform-owner
source_of_truth: false
scope: global
ai_usage: allowed
---

# AI Governance Policy

Source of truth cho **cách dùng AI, trách nhiệm, giới hạn và audit**. Là `source_policy` cho các file
AI-facing trong `.ai/`.

## 1. AI được dùng vào việc gì
TODO: danh sách use case cho phép / cần approval / cấm, theo risk và loại dữ liệu.

## 2. Human accountability (Handbook Ch 6, 11)
- AI **không** là accountable owner hoặc approver cuối.
- Human-in-the-loop phải có authority, expertise, evidence và quyền dừng workflow.
- Segregation of duties cho high-risk: người tạo output ≠ người approve cuối.

## 3. Giới hạn tự chủ của agent
- Scope, permission và tool access phải khai báo; `.ai/rules/forbidden-actions.md` liệt kê việc AI không được tự làm.
- Multi-agent không tạo independence nếu cùng model/context/assumption.

## 4. Context & source of truth
AI đọc context theo risk/task (Mục 16); không coi tóm tắt `.ai/` hay chat history là nguồn sự thật.

## 5. Model/tool change
Workflow quan trọng cần evaluation set + version record (`.ai/` eval metadata). "Model mới hơn" không mặc định tốt hơn.

## 6. Audit & evidence
TODO: evidence tối thiểu cần lưu (source dùng, assumption, validation, approver, lý do). Retention theo `security-policy.md`.

## Liên quan
`risk-level-policy.md`, `security-policy.md`, `quality-gates.md`, `.ai/rules/`.
