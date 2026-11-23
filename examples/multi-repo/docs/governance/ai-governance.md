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

## 7. Active initiative của session
- Một AI session làm việc trên **đúng một initiative**, và initiative đó do **người dùng chọn**. Bước này đi trước
  context loading: active initiative quyết định context nào được nạp.
- **Chưa chọn thì chưa làm.** Không sửa/tạo file, không chạy lệnh đổi trạng thái, không draft, không khảo sát code
  cho task. Chỉ được đọc `docs/registry/initiative-index.md` để liệt kê lựa chọn.
- **Agent không tự suy ra** initiative từ tên branch, commit, đường dẫn, memory hay session trước. Có thể đặt dự đoán
  lên đầu danh sách; người dùng vẫn là người chọn.
- Câu trả lời hợp lệ: một initiative có sẵn; một initiative **mới** (agent tạo trước, ID theo `document-naming.md`);
  hoặc **"no initiative"** — chỉ khi người dùng nói rõ và việc đó **không tạo commit** (restart service, đọc log,
  pull code, trả lời câu hỏi). Agent không đề xuất lựa chọn này làm mặc định.
- **Thay đổi governance không được miễn.** Sửa `docs/governance/`, `docs/templates/`, `docs/registry/`,
  `.ai/rules/`, `.ai/context/` hoặc adapter (`CLAUDE.md`, `AGENTS.md`) cần một initiative. Nên có một **standing
  initiative** cho governance; thay đổi rule được ghi thành ADR trong initiative đó.
- Sau khi chọn, agent nêu `Active initiative: INIT-…` và nạp folder của initiative. Yêu cầu nằm ngoài initiative →
  dừng và hỏi có chuyển không. Lựa chọn không mang sang session mới.
- **Traceability:** tên branch, commit subject (`docs(INIT-…): …`), tiêu đề PR và evidence trong `.ai/outputs/`
  mang ID của active initiative.

## Liên quan
`risk-level-policy.md`, `security-policy.md`, `quality-gates.md`, `.ai/rules/`.
