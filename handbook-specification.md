---
id: SPEC-ai-engineering-operating-model-handbook
title: AI Engineering Operating Model Handbook Specification
status: accepted
type: specification
scope: global
source_of_truth: true
parent_specification: ./documentation-specification.md
---

# AI Engineering Operating Model Handbook Specification

## 1. Vision

Xây dựng một Handbook giúp các vai trò trong engineering hiểu AI Engineering Operating Model, nhận diện vấn đề khi sử dụng AI thiếu kiểm soát và hình thành vocabulary, nguyên tắc cùng nhận thức chung trước khi áp dụng vào công việc.

Handbook trả lời **Why / What**. Handbook không phải tài liệu thao tác và không tạo authority cho policy.

## 2. Đối tượng sử dụng

- Người mới tiếp cận AI-assisted engineering.
- Developer và QC cần hiểu context, risk và trách nhiệm.
- Team Lead cần định hướng adoption và phối hợp team.
- QA cần thiết kế quality strategy và improvement loop.
- Tech Lead cần giữ architecture integrity và engineering standard.
- Stakeholder cần hiểu giá trị, giới hạn và rủi ro của Operating Model.

## 3. Mục tiêu

Handbook phải giúp người đọc:

1. Giải thích được vì sao engineering team cần AI Engineering Operating Model.
2. Hiểu AI Engineering Operating Model bao gồm những thành phần và phạm vi nội dung nào.
3. Hiểu các khái niệm chính và mối quan hệ giữa chúng để có thể đọc tiếp Playbook hoặc governance policy phù hợp.

## 4. Non-goals

Handbook không:

- Cung cấp workflow chi tiết để thực hiện task.
- Duy trì checklist hoặc use case canonical.
- Định nghĩa risk threshold, forbidden action hoặc approval authority.
- Thay thế governance policy hoặc engineering standard.
- Phụ thuộc vào một model, vendor hoặc tool cụ thể.

## 5. Cấu trúc nội dung bắt buộc

### 5.1. Learning path và glossary

- Điểm bắt đầu cho người mới.
- Lộ trình đọc theo role và nhu cầu.
- Glossary canonical hoặc liên kết tới glossary canonical.
- Giải thích chữ viết tắt ở lần xuất hiện đầu tiên.
- Bản đồ liên kết tới Playbook và policies.

### 5.2. Khái niệm và Operating Model

- Định nghĩa AI Engineering Operating Model.
- Ranh giới với AI Engineering Platform.
- Quan hệ giữa con người, process, knowledge, document, tool và agent.
- Vai trò của Operating Model trong SDLC.
- Human accountability và giới hạn tự chủ của AI.
- Giá trị kỳ vọng và cách tránh productivity theatre.

### 5.3. Hiện trạng và vấn đề chung

Handbook phải giải thích tối thiểu:

- Mục tiêu và cách sử dụng AI không thống nhất.
- Context phân mảnh và output không nhất quán.
- Ownership và accountability không rõ.
- Review và quality gate không theo risk.
- Thiếu traceability và auditability.
- Security, privacy và intellectual-property risk.
- Knowledge debt và phụ thuộc công cụ.
- Handoff và bottleneck xuyên role.

Mỗi vấn đề phải có ví dụ, dấu hiệu nhận biết, impact và liên kết tới control/use case liên quan.

### 5.4. Vấn đề và guidance theo role

Bao phủ tối thiểu:

- Developer.
- QC.
- Team Lead.
- QA.
- Tech Lead.
- Role khác khi workflow yêu cầu, ví dụ Product Owner, Security Owner hoặc Incident Commander.

Mỗi role guide phải mô tả mục tiêu, failure mode, trách nhiệm không được chuyển cho AI và Playbook use case liên quan.

### 5.5. Failure chain xuyên SDLC

Giải thích cách một context hoặc assumption sai có thể đi qua requirement, implementation, test, review, release và operations. Nội dung phải thể hiện vì sao control cục bộ ở một role là chưa đủ.

### 5.6. Knowledge và document concepts

- `docs/`, `.ai/` và source of truth.
- Initiative, domain và lifecycle knowledge.
- Product Brief, Proposal, PRD, RFC, ADR và Decision Log.
- Metadata, freshness, deprecation và promotion ở mức khái niệm.
- AI output và official artifact khác nhau thế nào.

Chi tiết topology phải tham chiếu [`aiom-document-structure.md`](./aiom-document-structure.md).

### 5.7. Context engineering

- Context là gì và ảnh hưởng output như thế nào.
- Context thiếu, dư thừa, stale hoặc mâu thuẫn.
- Quan hệ giữa task, source, domain và repo/module.
- Freshness và ownership của AI-facing context.
- Vì sao Playbook cần context-loading checklist.

### 5.8. Governance và risk concepts

Handbook giải thích rationale, không định nghĩa rule authoritative:

- Risk-based control.
- Quality gate.
- Human approval và segregation of duties.
- Security/privacy/data boundary.
- Evidence, audit và traceability.
- Exception, incident và promotion.

Mỗi nội dung phải liên kết tới policy authoritative hoặc đánh dấu dependency chưa tồn tại.

### 5.9. Prompt, workflow và agent concepts

- Prompt, workflow và agent khác nhau thế nào.
- Input/output contract và evidence.
- Single-agent và multi-agent.
- Agent role, scope và failure mode.
- Vì sao model/tool change cần regression evaluation.

Workflow thực thi phải liên kết tới Playbook.

### 5.10. Adoption, pilot và measurement

- Cách chọn pilot scope.
- Baseline và success criteria.
- Metric về flow, quality, rework, safety và maintenance cost.
- Feedback theo role.
- Maturity và điều kiện mở rộng automation/multi-agent.

## 6. Phong cách viết

- Bắt đầu mỗi chapter bằng vấn đề thực tế và điều người đọc sẽ học được.
- Trình bày: khái niệm → ví dụ → failure mode → điều cần nhớ → đọc tiếp.
- Mỗi chapter lớn có tóm tắt.
- Giải thích thuật ngữ bằng ngôn ngữ đơn giản trước khi dùng jargon.
- Dùng case study xuyên role khi quan hệ khó hiểu.
- Đánh dấu rõ nội dung cơ bản, nâng cao và tool-specific.
- Không trình bày recommendation như policy bắt buộc.

## 7. Cấu trúc chuẩn của một chapter

1. Mục tiêu học tập.
2. Vấn đề hoặc bối cảnh.
3. Khái niệm chính.
4. Ví dụ.
5. Failure mode hoặc hiểu nhầm thường gặp.
6. Điều cần nhớ.
7. Liên kết tới Playbook/policy liên quan.

## 8. Tiêu chí hoàn thành

- Bao phủ các nội dung bắt buộc ở Mục 5.
- Người mới giải thích lại được khái niệm và failure chain cốt lõi.
- Mỗi problem area liên kết tới use case hoặc policy xử lý tương ứng.
- Không chứa workflow/checklist canonical bị trùng với Playbook.
- Không tự tạo policy authority.
- Ít nhất một người mới đọc thử và không gặp thuật ngữ quan trọng chưa giải thích.
- Link tới Playbook, policy và source document hợp lệ hoặc được đánh dấu dependency gap.

## 9. Tài liệu liên quan

- [`documentation-specification.md`](./documentation-specification.md): specification cấp bộ tài liệu.
- [`playbook-specification.md`](./playbook-specification.md): specification của tài liệu thực hành.
- [`AI-engineering-operating-system-open-questions.md`](./AI-engineering-operating-system-open-questions.md): decision backlog.
