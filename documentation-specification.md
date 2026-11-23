---
id: SPEC-ai-engineering-operating-model-documentation
title: AI Engineering Operating Model Documentation Specification
status: draft
type: specification
scope: global
source_of_truth: false
---

# AI Engineering Operating Model Documentation Specification

## 1. Vision

Xây dựng một bộ tài liệu giúp engineering team hiểu và áp dụng **AI Engineering Operating Model** vào công việc hằng ngày.

Bộ tài liệu gồm:

- **Handbook** — giải thích bối cảnh, khái niệm, vấn đề và nguyên tắc: **Why / What**.
- **Playbook** — hướng dẫn use case, workflow, validation và xử lý: **When / How**.
- **Governance policies** — định nghĩa rule bắt buộc, authority và control.

## 2. Problem statement

Khi mỗi thành viên tự sử dụng AI mà không có Operating Model chung, năng suất cục bộ có thể tăng nhưng chi phí và rủi ro thường chuyển sang review, testing, integration, maintenance hoặc production.

Team cần đồng thời giải quyết:

- Cách hiểu và vocabulary không thống nhất.
- Context và source of truth phân mảnh.
- Ownership và accountability không rõ.
- Review và quality gate không tương ứng với risk.
- Thiếu traceability và audit evidence.
- Rủi ro security, privacy và intellectual property.
- Knowledge debt và phụ thuộc công cụ.
- Handoff không nhất quán giữa Developer, QC, Team Lead, QA và Tech Lead.

Bộ tài liệu phải xử lý các vấn đề này mà không tạo ra lượng quy trình và artifact lớn hơn giá trị thu được.

## 3. Mục tiêu

1. Tạo vocabulary và mental model thống nhất.
2. Giúp người mới hiểu hiện trạng và failure mode khi engineering team dùng AI.
3. Xác định ranh giới trách nhiệm giữa con người, AI và platform.
4. Chuyển nguyên tắc thành use case có thể thực hiện và kiểm chứng.
5. Kết nối workflow với policy, source of truth và quality gate.
6. Duy trì traceability giữa problem, knowledge, policy, use case và evidence.
7. Hỗ trợ pilot, measurement và continuous improvement.

## 4. Non-goals

Bộ tài liệu không nhằm:

- Thay thế engineering standard, security policy hoặc quality process hiện hành.
- Biến AI thành owner hoặc accountable party.
- Bắt mọi task sử dụng AI hoặc cùng một tool/model.
- Mô tả chi tiết cách triển khai một Engineering Platform cụ thể.
- Xem AI-generated output là đúng nếu chưa được validation.
- Gom toàn bộ knowledge, workflow và policy vào một tài liệu duy nhất.

## 5. Kiến trúc tài liệu

```text
documentation-specification.md
        │
        ├── handbook-specification.md
        │          ↓
        │      handbook-v1.md
        │
        ├── playbook-specification.md
        │          ↓
        │      playbook-v1.md
        │
        └── governance policies
                   ↑
             authority chung
```

### 5.1. Handbook

Handbook là nguồn giải thích canonical cho:

- Khái niệm và vocabulary.
- Bối cảnh và problem framing.
- Failure mode chung và theo role.
- Quan hệ giữa con người, workflow, knowledge, tool và agent.
- Role guidance, adoption và maturity.
- Rationale của governance policy.

Yêu cầu chi tiết nằm trong [`handbook-specification.md`](./handbook-specification.md).

### 5.2. Playbook

Playbook là nguồn hướng dẫn canonical cho:

- Quick start và cách chọn use case.
- Context-loading checklist.
- Standard AI-assisted workflow.
- Use case theo SDLC và role.
- Validation, evidence và quality gate trong từng use case.
- Exception, recovery và escalation handling.

Yêu cầu chi tiết nằm trong [`playbook-specification.md`](./playbook-specification.md).

### 5.3. Governance policies

Policy là nguồn authoritative cho:

- Risk threshold và classification rule.
- Quality gate bắt buộc.
- Security và data handling.
- Forbidden action.
- Approval, exception và promotion authority.
- Document metadata và lifecycle.

Handbook giải thích policy. Playbook operationalize policy. Khi có xung đột về rule bắt buộc, policy authoritative thắng.

## 6. Quy tắc phân loại nội dung

| Câu hỏi của nội dung | Artifact canonical |
| --- | --- |
| Vì sao vấn đề này quan trọng? | Handbook |
| Khái niệm này có nghĩa gì? | Handbook/glossary |
| Failure mode này xảy ra như thế nào? | Handbook |
| Khi nào dùng AI cho task này? | Playbook |
| Thực hiện theo bước nào? | Playbook |
| Kiểm tra và xử lý output thế nào? | Playbook |
| Điều gì bắt buộc hoặc bị cấm? | Governance policy |
| Ai có authority approve exception? | Governance policy |

## 7. Quy tắc tránh duplicate

- Khái niệm chỉ được định nghĩa đầy đủ trong Handbook hoặc glossary canonical.
- Workflow và checklist chỉ được định nghĩa đầy đủ trong Playbook.
- Rule bắt buộc chỉ được định nghĩa đầy đủ trong policy authoritative.
- Artifact khác được phép tóm tắt nhưng phải liên kết tới canonical source.
- Handbook không copy toàn bộ workflow từ Playbook.
- Playbook không copy toàn bộ kiến thức nền từ Handbook.
- Khi policy thay đổi, Playbook phải được freshness-review; Handbook chỉ cập nhật nếu rationale hoặc explanation bị ảnh hưởng.

## 8. Khả năng sử dụng độc lập

- Người đọc Handbook phải hiểu khái niệm mà không cần thực hiện workflow.
- Người dùng Playbook phải thực hiện được use case cơ bản mà không phải đọc toàn bộ Handbook.
- Playbook phải giải thích ngắn hoặc liên kết trực tiếp tới thuật ngữ prerequisite.
- Cả hai tài liệu phải chỉ rõ status và authority của nội dung tham chiếu.
- Link hỏng hoặc policy chưa tồn tại phải được coi là dependency gap, không được âm thầm thay bằng rule tự định nghĩa.

## 9. Phong cách chung

- Viết cho người mới nhưng không làm mất độ chính xác chuyên môn.
- Bắt đầu từ vấn đề và outcome, không bắt đầu từ tool.
- Giải thích thuật ngữ ở lần xuất hiện đầu tiên.
- Phân biệt rõ `phải`, `nên`, `có thể` và `không được`.
- Dùng ví dụ và phản ví dụ có input, output và validation.
- Dùng dữ liệu giả lập hoặc đã sanitize.
- Chỉ dùng sơ đồ khi quan hệ khó hiểu hơn nếu mô tả bằng văn bản.
- Không khẳng định AI luôn cải thiện năng suất.

## 10. Traceability

- Mỗi problem area phải liên kết tới chapter Handbook tương ứng.
- Khi problem có hành động xử lý, chapter phải liên kết tới use case Playbook.
- Mỗi use case phải tham chiếu risk/control và policy liên quan.
- Mỗi câu hỏi đã giải quyết phải trỏ tới source canonical có owner và status.
- Registry hoặc index nên liên kết problem → handbook → policy → playbook → evidence.

## 11. Deliverables

1. `handbook-specification.md`.
2. `playbook-specification.md`.
3. `handbook-v1.md`.
4. `playbook-v1.md`.
5. Governance policy skeleton tối thiểu.
6. Glossary canonical.
7. Registry/index liên kết các artifact.

## 12. Tiêu chí hoàn thành

- Handbook, Playbook và policy có phạm vi cùng authority rõ ràng.
- Handbook và Playbook đáp ứng specification riêng.
- Người đọc phân biệt được nội dung để học, để thực hiện và rule bắt buộc.
- Người mới dùng được learning path của Handbook.
- Người mới thực hiện được use case cơ bản trong Playbook mà không phải đọc toàn bộ Handbook.
- Không duy trì khái niệm, workflow hoặc policy đầy đủ tại nhiều source cạnh tranh.
- Các dependency chưa tồn tại và open question được nhận diện rõ.

## 13. Tài liệu liên quan

- [`handbook-specification.md`](./handbook-specification.md): yêu cầu nội dung và chất lượng Handbook.
- [`playbook-specification.md`](./playbook-specification.md): yêu cầu nội dung và chất lượng Playbook.
- [`aiom-document-structure.md`](./aiom-document-structure.md): topology tài liệu đề xuất.
- `AI-engineering-operating-system-open-questions.md`: decision backlog — **chưa tồn tại (dependency gap)**.
