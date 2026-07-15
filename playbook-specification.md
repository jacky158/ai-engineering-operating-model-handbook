---
id: SPEC-ai-engineering-operating-model-playbook
title: AI Engineering Operating Model Playbook Specification
status: draft
type: specification
scope: global
source_of_truth: false
parent_specification: ./documentation-specification.md
---

# AI Engineering Operating Model Playbook Specification

## 1. Vision

Xây dựng một Playbook thực hành giúp engineering team lựa chọn, thực hiện, kiểm chứng và xử lý các AI-assisted use case xuyên suốt SDLC bằng workflow và checklist nhất quán.

Playbook trả lời **When / How**. Người dùng phải thực hiện được một use case cơ bản mà không cần đọc toàn bộ Handbook.

## 2. Đối tượng sử dụng

- Developer.
- QC.
- Team Lead.
- QA.
- Tech Lead.
- Reviewer, approver và role chuyên môn liên quan tới từng use case.

## 3. Mục tiêu

Playbook phải:

1. Cung cấp quick start và cách chọn use case.
2. Xác định prerequisite, role, risk và source context cho từng tình huống.
3. Cung cấp workflow có thể thực hiện từng bước.
4. Xác định output, validation, evidence và quality gate.
5. Chỉ rõ điểm phải dừng, escalation và forbidden condition.
6. Hướng dẫn xử lý output sai, thiếu, không chắc chắn hoặc vượt scope.
7. Kết nối use case tới Handbook và governance policy canonical.
8. Cung cấp completion checklist trước khi promote hoặc release.

## 4. Non-goals

Playbook không:

- Giải thích đầy đủ lý thuyết hoặc lịch sử của Operating Model.
- Duy trì glossary, failure-mode analysis hoặc role guide đầy đủ.
- Tự định nghĩa risk threshold, forbidden action hoặc approval authority.
- Thay thế Handbook, policy hoặc engineering standard.
- Cung cấp prompt rời rạc không gắn với workflow và validation.
- Giả định AI output đúng vì tool thể hiện độ tự tin cao.

## 5. Cấu trúc Playbook

### 5.1. Quick start

- Cách chọn use case theo outcome, lifecycle và role.
- Checklist trước khi bắt đầu.
- Thuật ngữ prerequisite tối thiểu hoặc link trực tiếp tới Handbook.
- Cách xác định accountable owner.
- Điểm phải dừng và escalation route.

### 5.2. Nội dung vận hành dùng chung

- Context-loading checklist theo task type và risk.
- Standard AI-assisted workflow.
- Evidence checklist tối thiểu.
- Dấu hiệu output không đáng tin cậy.
- Exception và failure handling.
- Completion checklist.

### 5.3. Use case catalog theo SDLC

Catalog tối thiểu bao phủ:

1. Discovery và problem analysis.
2. Product Brief, Proposal và PRD.
3. Technical design, RFC và ADR.
4. Planning, breakdown và estimation.
5. Implementation và refactoring.
6. Code review và architecture review.
7. Test planning, design và generation.
8. Test execution, defect analysis và regression.
9. Release readiness, release note và rollback.
10. Incident analysis, troubleshooting và postmortem.
11. Documentation, knowledge maintenance và context refresh.

### 5.4. Tổ chức theo role

Mỗi use case phải xác định trách nhiệm của:

- Executor.
- Reviewer.
- Approver nếu cần.
- Accountable owner.
- Consulted specialist khi cần.

Playbook phải có use case xuyên role cho planning, handoff, review, release và incident.

### 5.5. Phân loại quyền dùng AI

Mỗi use case phải ánh xạ tới policy và thuộc một nhóm:

- **Recommended** — dùng theo workflow chuẩn.
- **Conditional** — cần context, gate hoặc approval bổ sung.
- **Human-led** — AI hỗ trợ; con người thực hiện quyết định chính.
- **Forbidden** — policy không cho phép giao hành động cho AI.

Playbook mô tả cách áp dụng classification, không tự định nghĩa authority của classification.

## 6. Cấu trúc chuẩn của một use case

Mỗi use case phải có đủ:

1. **Mục tiêu** — outcome cần đạt.
2. **Khi nào áp dụng** — trigger và prerequisite.
3. **Khi nào không áp dụng** — limitation và forbidden condition.
4. **Vai trò** — executor, reviewer, approver và accountable owner.
5. **Risk** — level và policy reference.
6. **Input/source of truth** — context bắt buộc.
7. **Workflow checklist** — bước của con người và AI.
8. **Expected output** — artifact hoặc decision.
9. **Validation/quality gate** — cách kiểm tra.
10. **Evidence/traceability** — thông tin phải lưu.
11. **Failure modes** — lỗi và dấu hiệu nhận biết.
12. **Recovery/handling** — cách xử lý.
13. **Best practices** — cách làm khuyến nghị.
14. **Anti-patterns** — cách làm cần tránh.
15. **Metrics** — tín hiệu đánh giá khi phù hợp.
16. **Related knowledge/policy** — link tới Handbook và policy.

## 7. Tình huống xử lý bắt buộc

Playbook phải có hướng dẫn cụ thể cho:

- Context thiếu, stale hoặc mâu thuẫn.
- Output không chắc chắn hoặc không nhất quán.
- AI tự mở rộng task hoặc thay đổi ngoài scope.
- Output vi phạm architecture, security hoặc engineering standard.
- Dữ liệu nhạy cảm bị cung cấp sai cho AI tool.
- Generated code/test không thể giải thích hoặc kiểm chứng.
- Model, tool, prompt hoặc agent workflow thay đổi.
- Human reviewer và AI đưa ra kết luận khác nhau.
- Output không qua quality gate.
- Không xác định được owner, reviewer hoặc policy áp dụng.

## 8. Phong cách viết

- Ưu tiên câu ngắn, chủ thể và hành động rõ.
- Dùng checklist cho workflow.
- Đưa prerequisite và điểm dừng trước các bước thực hiện.
- Phân biệt rõ `phải`, `nên`, `có thể` và `không được`.
- Mỗi ví dụ có input, action, output và validation.
- Prompt mẫu chỉ xuất hiện trong workflow, không được trình bày như công thức dùng cho mọi task.
- Giải thích ngắn thuật ngữ bắt buộc và liên kết tới Handbook.
- Nội dung nâng cao hoặc high-risk phải được đánh dấu rõ.

## 9. Feedback loop

Khi use case phát hiện vấn đề mới:

1. Ghi nhận evidence.
2. Xác định lỗi cục bộ, knowledge gap hay control gap.
3. Sửa use case nếu là lỗi cục bộ.
4. Cập nhật Handbook nếu là knowledge gap.
5. Cập nhật policy qua owner có authority nếu là control gap.
6. Review các use case bị ảnh hưởng và chạy regression evaluation phù hợp.

## 10. Tiêu chí hoàn thành

- Có quick start và cách chọn use case rõ ràng.
- Use case catalog bao phủ lifecycle tối thiểu.
- Mọi use case tuân thủ cấu trúc ở Mục 6.
- Workflow có checklist và accountable owner.
- Risk, policy, validation và evidence được liên kết rõ.
- Người mới thực hiện được một use case low-risk mà không cần đọc toàn bộ Handbook.
- Không chứa phần giải thích nền dài hoặc role guide bị trùng với Handbook.
- Không tự định nghĩa policy authority.
- Link tới Handbook, policy và source context hợp lệ hoặc được đánh dấu dependency gap.

## 11. Tài liệu liên quan

- [`documentation-specification.md`](./documentation-specification.md): specification cấp bộ tài liệu.
- [`handbook-specification.md`](./handbook-specification.md): kiến thức nền và role guidance.
- [`playbook-v1.md`](./playbook-v1.md): bản Playbook V1 hiện tại cần được căn chỉnh theo specification này.
