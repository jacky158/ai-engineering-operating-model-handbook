---
id: HANDBOOK-ai-engineering-operating-model-v1
title: AI Engineering Operating Model Handbook V1
status: proposed
version: 1.2.0
type: handbook
scope: global
source_of_truth: false
owner: engineering-leadership
created_at: 2026-07-13
updated_at: 2026-07-13
review_cycle: quarterly
based_on: ./handbook-specification.md
---

# AI Engineering Operating Model Handbook V1

## 1. Mục đích của Handbook

Handbook này giúp engineering team hiểu **AI Engineering Operating Model** trước khi áp dụng vào công việc hằng ngày.

Sau khi đọc Handbook, người đọc có thể:

1. Giải thích được vì sao engineering team cần AI Engineering Operating Model.
2. Hiểu AI Engineering Operating Model bao gồm những thành phần và phạm vi nội dung nào.
3. Hiểu các khái niệm chính và mối quan hệ giữa chúng để có thể đọc tiếp Playbook hoặc governance policy phù hợp.

Handbook giải thích **Why / What**. Khi cần các bước thực hiện, use case hoặc checklist, sử dụng [`playbook-v1.md`](./playbook-v1.md). Khi cần biết rule nào bắt buộc, sử dụng governance policy authoritative tương ứng.

## 2. Bắt đầu ở đây

### 2.1. Nếu bạn là người mới

Đọc theo thứ tự:

1. Chương 4 — Operating Model là gì?
2. Chương 5 — Vì sao team cần Operating Model?
3. Chương 6 — Mười nguyên tắc nền tảng.
4. Chương 8 — Guidance cho role của bạn.
5. Chương 14 — Bắt đầu pilot.
6. Chuyển sang Playbook để chọn use case thực hành.

### 2.2. Nếu bạn cần tra cứu nhanh

| Nhu cầu | Chương nên đọc |
| --- | --- |
| Hiểu Operating Model và Platform khác nhau thế nào | Chương 4 |
| Nhận diện vấn đề của team | Chương 5 và 7 |
| Tìm guidance theo role | Chương 8 |
| Hiểu `docs/`, `.ai/` và source of truth | Chương 9 |
| Hiểu context engineering | Chương 10 |
| Hiểu risk và quality gate | Chương 11 |
| Phân biệt prompt, workflow và agent | Chương 12 |
| Tổ chức pilot và measurement | Chương 14–15 |
| Thực hiện task cụ thể | Chuyển sang Playbook |

## 3. Glossary

| Thuật ngữ | Giải thích đơn giản |
| --- | --- |
| Artificial Intelligence (AI) | Hệ thống tạo, phân tích hoặc biến đổi nội dung để hỗ trợ con người |
| AI-assisted engineering | Công việc engineering do con người thực hiện với AI hỗ trợ |
| Operating Model | Cách tổ chức con người, workflow, knowledge, control và trách nhiệm |
| Engineering Platform | Công cụ và hạ tầng cung cấp capability cho engineering |
| Software Development Life Cycle (SDLC) | Vòng đời từ ý tưởng, phát triển, kiểm thử tới release và vận hành |
| AI agent | Phần mềm dùng AI để thực hiện một chuỗi bước trong phạm vi được giao |
| Prompt | Chỉ dẫn hoặc yêu cầu được gửi cho AI |
| Context | Thông tin AI cần để hiểu và thực hiện task |
| Source of truth | Nguồn chính thức được ưu tiên khi thông tin khác nhau |
| Output | Nội dung AI tạo ra, ví dụ analysis, code, test hoặc document draft |
| Evidence | Bằng chứng dùng để kiểm chứng output, ví dụ test result, log hoặc review |
| Validation | Hoạt động kiểm tra output có đúng và phù hợp hay không |
| Quality gate | Điều kiện phải đạt trước khi chuyển sang bước tiếp theo |
| Risk | Khả năng và mức độ thiệt hại nếu output hoặc quyết định sai |
| Traceability | Khả năng lần theo requirement, decision, code, test và release |
| Promotion | Quá trình biến draft thành artifact chính thức có human owner |
| Quality Control (QC) | Kiểm soát chất lượng đầu ra qua test và defect validation |
| Quality Assurance (QA) | Bảo đảm chất lượng quy trình, strategy và cải tiến hệ thống |
| Product Requirements Document (PRD) | Tài liệu mô tả requirement và acceptance criteria |
| Request for Comments (RFC) | Tài liệu dùng để thảo luận technical design |
| Architecture Decision Record (ADR) | Tài liệu ghi quyết định kiến trúc và rationale |
| Personally Identifiable Information (PII) | Dữ liệu có thể nhận diện một cá nhân |

Thuật ngữ canonical cần được tách thành glossary riêng khi bộ tài liệu được promote thành `accepted`.

## 4. AI Engineering Operating Model là gì?

### 4.1. Mục tiêu học tập

Sau chương này, người đọc có thể:

- Giải thích Operating Model bằng ngôn ngữ đơn giản.
- Phân biệt Operating Model với Engineering Platform.
- Nhận diện các thành phần cần phối hợp khi AI tham gia SDLC.

### 4.2. Định nghĩa

AI Engineering Operating Model là cách một tổ chức sắp xếp con người, quy trình, knowledge, tool, AI agent, control và feedback để sử dụng AI trong engineering.

Operating Model không chỉ hỏi “dùng model nào?”. Nó hỏi:

- Công việc nào phù hợp với AI?
- Ai chịu trách nhiệm cho outcome?
- AI phải đọc nguồn nào?
- Output được kiểm chứng thế nào?
- Khi nào cần review hoặc approval?
- Evidence nào cần giữ?
- Team học từ success và failure như thế nào?

### 4.3. Các thành phần

```text
People       → role, skill, ownership, accountability
Process      → workflow, handoff, review, escalation
Knowledge    → source of truth, context, document lifecycle
Technology   → model, tool, platform, agent runtime
Governance   → risk, security, gate, approval, evidence
Improvement  → pilot, metric, feedback, evaluation
```

Một thành phần mạnh không bù được cho thành phần khác bị thiếu. Ví dụ, model tốt không thể sửa requirement mâu thuẫn; automation nhanh không thể thay thế accountable owner.

### 4.4. Operating Model và Engineering Platform

| Khía cạnh | Operating Model | Engineering Platform |
| --- | --- | --- |
| Trọng tâm | Cách team tổ chức và kiểm soát công việc | Công cụ và hạ tầng hỗ trợ |
| Thành phần | Role, workflow, knowledge, policy, metric | Model gateway, IDE, agent runtime, CI/CD |
| Câu hỏi | Ai làm gì, khi nào và chịu trách nhiệm ra sao? | Capability được cung cấp và vận hành thế nào? |
| Kết quả | Hành vi và quy trình nhất quán | Capability kỹ thuật có thể sử dụng |

Platform có thể enforce một số control nhưng không thay thế business judgment, technical ownership hoặc human approval.

### 4.5. Ví dụ

Một coding assistant có thể tạo code từ task description. Đó là capability của Platform.

Operating Model xác định Developer phải đọc PRD và ADR nào, change thuộc risk nào, reviewer là ai, test evidence cần có và khi nào code được promote. Nếu thiếu phần này, capability mạnh chỉ làm output được tạo nhanh hơn, không bảo đảm outcome tốt hơn.

### 4.6. Hiểu nhầm thường gặp

- **“Mua AI tool là đã có Operating Model.”** Tool chỉ là một thành phần.
- **“Operating Model là bộ prompt chuẩn.”** Prompt không xác định ownership, gate và evidence đầy đủ.
- **“AI tốt hơn thì cần ít review hơn.”** Review depth phụ thuộc risk và evidence, không chỉ capability của model.
- **“Operating Model càng nhiều tài liệu càng tốt.”** Chỉ nên tạo artifact giải quyết coordination hoặc risk rõ ràng.

### 4.7. Điều cần nhớ

- Operating Model kết nối People, Process, Knowledge, Technology và Governance.
- Platform cung cấp capability; Operating Model định hướng cách capability được sử dụng.
- Human accountability không được chuyển cho AI.

Đọc tiếp: Chương 5 để hiểu vấn đề Operating Model cần giải quyết; Playbook Mục 6 để xem workflow thực hành.

## 5. Vì sao team cần Operating Model?

### 5.1. Mục tiêu học tập

Nhận diện lý do productivity cá nhân có thể tăng trong khi outcome của team giảm.

### 5.2. Từ output nhanh tới bottleneck downstream

AI giúp tạo code, test và document nhanh. Tuy nhiên, review, validation và approval vẫn cần thời gian. Nếu tốc độ tạo output tăng nhanh hơn năng lực kiểm chứng, bottleneck chuyển sang downstream.

Ví dụ:

1. Developer tạo một diff lớn trong vài giờ.
2. Reviewer cần nhiều ngày để hiểu assumption và impact.
3. QC tạo test từ cùng requirement chưa rõ nên không phát hiện assumption sai.
4. Defect xuất hiện sau release.

Lead time tổng thể không giảm; chi phí chỉ chuyển từ implementation sang review và rework.

### 5.3. Tối ưu cục bộ và outcome toàn hệ thống

Các metric như số dòng code, số task có AI hoặc số prompt không cho biết:

- Requirement có được hiểu đúng không?
- Code có maintainable không?
- Test có phát hiện đúng risk không?
- Review có đủ evidence không?
- Defect và rework có tăng không?

Operating Model hướng team từ “AI tạo bao nhiêu?” sang “AI giúp outcome tốt hơn thế nào?”.

### 5.4. Điều cần nhớ

- Tốc độ tạo output không đồng nghĩa tốc độ giao giá trị.
- Cần kiểm soát toàn bộ flow, không chỉ bước dùng AI.
- Outcome phải được đánh giá cùng quality, rework và risk.

Đọc tiếp: Chương 7 về failure chain; Chương 15 về measurement.

## 6. Nguyên tắc nền tảng

### 6.1. Mục tiêu học tập

Hiểu các nguyên tắc dùng để định hướng judgment khi chưa có use case chi tiết.

### 6.2. Mười nguyên tắc

1. **Outcome before output** — đánh giá outcome và chất lượng, không chỉ lượng nội dung AI tạo.
2. **Human accountability** — AI không phải accountable owner hoặc approver cuối cùng.
3. **Source of truth first** — ưu tiên nguồn authoritative, không coi chat history là nguồn sự thật.
4. **Risk-based control** — validation, evidence và approval tăng theo risk.
5. **Explicit scope** — AI không tự mở rộng task hoặc quyết định ngoài scope.
6. **Evidence over confidence** — lời giải thích tự tin không thay thế test, log hoặc review.
7. **Small and reviewable** — output nhỏ dễ hiểu và kiểm chứng hơn.
8. **Security by default** — chỉ cung cấp dữ liệu được phép cho tool được phê duyệt.
9. **Promote, do not copy blindly** — AI draft chỉ thành official artifact sau human validation.
10. **Learn through feedback** — failure phải quay lại cải tiến knowledge, workflow hoặc control.

### 6.3. Ví dụ

AI đề xuất thêm một dependency mới để giải quyết task. “Explicit scope” yêu cầu không tự chấp nhận thay đổi. “Evidence over confidence” yêu cầu kiểm tra capability, license và impact. “Human accountability” yêu cầu technical owner đưa ra quyết định.

### 6.4. Hiểu nhầm thường gặp

- Principle không phải checklist thay cho use case.
- Principle không tự tạo authority cho hành động bị kiểm soát.
- “Human in the loop” không có nghĩa một người chỉ bấm approve mà không hiểu output.

### 6.5. Điều cần nhớ

Nguyên tắc giúp định hướng; Playbook hướng dẫn thực hiện; policy quyết định điều bắt buộc.

Đọc tiếp: [`playbook-v1.md`](./playbook-v1.md) để áp dụng nguyên tắc vào use case.

## 7. Failure modes chung

### 7.1. Mục tiêu học tập

Nhận diện dấu hiệu team đang sử dụng AI thiếu coordination hoặc control.

### 7.2. Các failure mode cần nhận diện

| Failure mode | Ví dụ | Dấu hiệu | Impact | Đọc tiếp |
| --- | --- | --- | --- | --- |
| Mục tiêu không thống nhất | Report tuần chỉ khoe số prompt, không có số liệu rework | Đo adoption bằng số prompt; không có baseline; bỏ qua review/rework | Tối ưu output cá nhân thay vì outcome của team | Chương 14–15 |
| Context phân mảnh | Developer và QC làm việc trên hai bản summary requirement khác nhau | Mỗi role có summary khác nhau; source stale; rationale chỉ nằm trong chat | Output không nhất quán và khó tái dựng quyết định | Chương 9–10; Playbook UC-01 |
| Ownership không rõ | PRD do AI draft được merge nhưng không ai đứng tên owner | Không ai nhận artifact; handoff thiếu assumption; AI summary thay source | Decision không có accountable owner | Chương 8, 11; Playbook Mục 4 |
| Gate không theo risk | Thay đổi payment logic đi qua cùng review flow với sửa typo | Critical change và typo dùng cùng flow; AI review thay approval | Review thiếu hoặc overhead không cần thiết | Chương 11; Playbook Mục 2 |
| Thiếu traceability | Release note khẳng định đã test nhưng không link tới evidence | Claim không có evidence; draft được promote không owner | Khó audit, tìm root cause và cải tiến | Chương 9, 11; Playbook Mục 6 |
| Security, privacy và IP | Paste production log chứa PII vào tool chưa được duyệt | Paste log thật; không rõ approved tool; không kiểm tra license | Lộ dữ liệu, vi phạm policy hoặc provenance | Chương 11; Playbook Mục 4, 19 |
| Knowledge debt | Quyết định kiến trúc chỉ còn trong lịch sử chat của một cá nhân | Decision không có record; knowledge nằm trong chat; code không maintain được | Phụ thuộc cá nhân/tool và context nhanh stale | Chương 9; Playbook UC-10 |
| Handoff và bottleneck | Diff 2000 dòng sinh trong buổi sáng nhưng reviewer cần cả tuần | Output sinh nhanh hơn review/test; role dùng source khác nhau | Rework chuyển downstream, lead time không giảm | Chương 13; Playbook UC-04/05/08 |

### 7.3. Điều cần nhớ

Failure mode thường liên kết với nhau. Context kém có thể dẫn tới output sai, review quá tải, test không đúng oracle và knowledge debt.

Đọc tiếp: Chương 8 cho role guidance; Playbook Mục 4, 7 và 19 cho handling.

## 8. Guidance theo role

### 8.1. Mục tiêu học tập

Hiểu mỗi role có mục tiêu, failure mode và accountability khác nhau khi sử dụng AI.

### 8.2. Guidance theo role

| Role | Mục tiêu | Failure modes chính | Trách nhiệm không chuyển cho AI | Playbook liên quan |
| --- | --- | --- | --- | --- |
| Developer | Tăng chất lượng phân tích/execution và giữ ownership code | Code trước khi hiểu requirement; diff vượt scope; code/test cùng assumption; không debug được output | Hiểu behavior; giữ scope; chứng minh validation; sửa root cause | UC-01/02/03/04/06 |
| QC | Mở rộng test ideas nhưng giữ expected truth ở con người | Test từ requirement thiếu; happy-path bias; expected result không source; giảm exploratory test | Kiểm chứng oracle; ưu tiên theo risk; giữ defect evidence; kết luận từ evidence | UC-01/05/06/08 |
| Team Lead | Điều phối adoption theo outcome của team | AI bù planning yếu; thiếu review capacity; shadow workflow; không thấy downstream cost | Pilot scope; accountable owner; capacity; outcome/safety feedback | UC-01/08; Mục 21 |
| QA | Bảo đảm workflow có control, evidence và improvement loop | Policy không thành control; metric che quality debt; thiếu audit; không regression-evaluate | Quality strategy; audit requirement; failure-pattern analysis; policy improvement | UC-05/08; Mục 21 |
| Tech Lead | Giữ architecture integrity và technical quality | Local optimization; decision trong chat; review bottleneck; pattern inconsistency | Technical direction; review depth; dependency/contract decision; high-impact evidence | UC-02/04/07/08 |

### 8.3. Role ngoài core team

Một số use case cần Product Owner, Security Owner, Data Owner, Architecture Owner hoặc Incident Commander. Tên role có thể khác theo tổ chức, nhưng authority phải rõ. Không ép Developer, QC hoặc Team Lead tự quyết vấn đề ngoài thẩm quyền chỉ vì AI đã đưa ra recommendation.

### 8.4. Điều cần nhớ

- AI hỗ trợ role; không nhận accountability thay role.
- Handoff phải mang theo source, assumption và evidence.
- Use case xuyên role quan trọng hơn tối ưu output của một cá nhân.

## 9. Knowledge và document concepts

### 9.1. Mục tiêu học tập

Hiểu AI cần knowledge được tổ chức thế nào và vì sao AI output không mặc định là official document.

### 9.2. `docs/` và `.ai/`

Mô hình đề xuất:

```text
docs/ = source of truth cho tài liệu chính thức
.ai/  = operating layer giúp AI tìm context, rule và workflow
```

`.ai/` có thể tóm tắt hoặc định tuyến nhưng không âm thầm override `docs/`.

Chi tiết topology nằm trong [`aiom-document-structure.md`](./aiom-document-structure.md).

### 9.3. Các loại tài liệu

| Artifact | Câu hỏi chính |
| --- | --- |
| Product Brief | Vấn đề/cơ hội và outcome là gì? |
| Proposal | Những phương án nào đang được cân nhắc? |
| PRD | Requirement và acceptance criteria là gì? |
| RFC | Technical design nào cần thảo luận? |
| ADR | Quyết định kiến trúc nào đã được chọn và vì sao? |
| Decision Log | Những quyết định nào đã được đưa ra, khi nào và bởi ai? |
| Test Plan | Risk nào cần test và evidence nào cần có? |
| AI Output | AI đã đề xuất hoặc phân tích điều gì? |

AI Output là draft hoặc evidence trung gian. Nó chỉ thành official artifact sau human validation, ownership và promotion theo document policy.

### 9.4. Initiative và domain knowledge

- **Initiative knowledge** giải thích một thay đổi cụ thể: mục tiêu, scope, plan, test và decision.
- **Domain knowledge** lưu business rule và architecture dài hạn của một lĩnh vực.

Nếu chỉ lưu knowledge trong initiative, team có thể mất kiến thức dài hạn sau khi initiative đóng. Nếu chỉ lưu ở domain, người thực hiện khó trace một thay đổi cụ thể. Hai lớp cần liên kết nhưng không copy toàn bộ nội dung.

### 9.5. Freshness

Document có thể tồn tại nhưng đã stale. Freshness cần owner, review cycle, source revision và supersession relation. AI-facing summary đặc biệt dễ stale vì source thay đổi nhưng summary không được refresh.

### 9.6. Hiểu nhầm thường gặp

- “AI đã tóm tắt nên không cần đọc source.”
- “File trong `.ai/` luôn mới hơn và chính xác hơn.”
- “Generated document trở thành official khi được commit.”
- “Copy nội dung sang nhiều nơi giúp AI tìm dễ hơn.”

### 9.7. Điều cần nhớ

Knowledge tốt cần canonical source, owner, lifecycle và traceability. AI output cần được promote, không được copy blindly.

Đọc tiếp: Playbook UC-10 và `aiom-document-structure.md`.

## 10. Context engineering

### 10.1. Mục tiêu học tập

Hiểu context ảnh hưởng output thế nào và tại sao “càng nhiều context càng tốt” là một hiểu nhầm.

### 10.2. Context là gì?

Context là thông tin được cung cấp hoặc cho phép AI truy cập để thực hiện task: requirement, code, test, rule, architecture, log, decision và constraint.

AI không tự biết context nội bộ nếu không được cung cấp hoặc kết nối. Khi context thiếu, AI thường lấp khoảng trống bằng pattern phổ biến; pattern đó có thể không đúng với hệ thống cụ thể.

### 10.3. Bốn vấn đề context

| Vấn đề | Hệ quả |
| --- | --- |
| Thiếu | AI phải suy đoán requirement hoặc constraint |
| Stale | Output phù hợp hệ thống cũ nhưng sai với hiện tại |
| Mâu thuẫn | AI chọn nguồn tùy ý hoặc tạo kết luận không nhất quán |
| Dư thừa | Signal quan trọng bị chìm, chi phí và noise tăng |

### 10.4. Context theo task

Task khác nhau cần context khác nhau. Bug fix cần reproduction và log; architecture decision cần quality attributes và constraint; test design cần acceptance criteria và defect history.

Do đó context-loading nên phụ thuộc task type, risk và impact, không dùng một bộ context cố định cho mọi việc.

### 10.5. Ví dụ

Yêu cầu “thêm trường trạng thái vào API” chưa đủ để implementation. AI còn cần biết compatibility rule, consumer, schema, migration, enum convention và rollback. Nếu thiếu, AI có thể tạo breaking change dù code compile.

### 10.6. Điều cần nhớ

- Context đúng quan trọng hơn context nhiều.
- Source authoritative quan trọng hơn summary tiện lợi.
- Khoảng trống phải được nêu như unknown, không biến thành fact.

Đọc tiếp: Playbook Mục 5 về context-loading checklist.

## 11. Governance, risk và quality gate

### 11.1. Mục tiêu học tập

Hiểu vì sao control cần thay đổi theo risk và tại sao Handbook không phải policy authority.

### 11.2. Risk-based control

Không phải mọi task đều cần cùng mức review. Documentation typo dễ đảo ngược khác với permission, payment hoặc data migration.

Risk thường tăng khi:

- Blast radius lớn.
- Khó rollback.
- Chạm security, privacy hoặc production data.
- Thay đổi public contract hoặc architecture dài hạn.
- Evidence khó thu thập.

Risk threshold và classification rule cụ thể phải nằm trong risk policy. Hiện policy này là dependency gap.

### 11.3. Quality gate

Quality gate là điều kiện phải đạt trước bước tiếp theo, ví dụ design approval, test evidence hoặc release readiness. Gate giúp ngăn output chưa đủ evidence được promote chỉ vì AI tạo ra nhanh hoặc tự tin.

Gate quá yếu làm tăng failure risk. Gate quá nặng tạo overhead và khuyến khích bypass. Vì vậy gate cần gắn với risk và được review bằng evidence.

### 11.4. Human accountability

“Human in the loop” chỉ có ý nghĩa khi người đó:

- Có đủ authority và expertise.
- Có source/evidence để review.
- Hiểu quyết định đang approve.
- Có quyền dừng workflow.

Một thao tác bấm approve mang tính hình thức không tạo accountability thực chất.

Với change có risk cao, accountability còn cần **segregation of duties**: người tạo output không đồng thời là người approve cuối cùng cho chính change đó. Tách vai trò giúp tránh việc một cá nhân (hoặc một AI agent) vừa sinh vừa tự phê duyệt mà không có kiểm tra độc lập. Mức độ tách quyền cụ thể do policy authoritative quy định.

### 11.5. Security và privacy

AI làm tăng số nơi dữ liệu có thể đi qua. Governance phải xác định tool nào được phép, loại dữ liệu nào được dùng, retention thế nào và xử lý incident ra sao.

Handbook không định nghĩa các rule đó. Security policy authoritative hiện là dependency gap.

### 11.6. Evidence và audit

Không phải task nào cũng cần lưu toàn bộ chat. Evidence cần đủ để trả lời:

- Source nào đã được dùng?
- Assumption nào quan trọng?
- Validation nào đã chạy?
- Ai review/approve?
- Vì sao quyết định được đưa ra?

### 11.7. Điều cần nhớ

- Risk quyết định độ sâu của control.
- Policy tạo authority; Playbook operationalize policy.
- AI confidence không thay evidence.

Đọc tiếp: Playbook Mục 2, 4, 6 và 20.

## 12. Prompt, workflow và agent

### 12.1. Mục tiêu học tập

Phân biệt ba khái niệm thường bị dùng lẫn nhau.

### 12.2. Prompt

Prompt là chỉ dẫn cho một interaction. Prompt tốt giúp làm rõ mục tiêu, context, constraint và output format, nhưng không tự tạo ownership, approval hoặc lifecycle.

### 12.3. Workflow

Workflow là chuỗi bước của con người và AI, gồm prerequisite, input, output, validation, evidence và handling. Một prompt có thể là một bước trong workflow.

### 12.4. Agent

Agent là phần mềm dùng AI để thực hiện nhiều bước, có thể đọc context, gọi tool và điều chỉnh hành động dựa trên kết quả. Agent làm tăng capability nhưng cũng tăng blast radius nếu scope và permission không rõ.

### 12.5. So sánh

| Khía cạnh | Prompt | Workflow | Agent |
| --- | --- | --- | --- |
| Phạm vi | Một interaction | Chuỗi bước | Thực thi chuỗi bước có mức tự chủ |
| Ownership | Người gửi prompt | Workflow owner | Agent owner + task owner |
| Validation | Theo output | Được thiết kế trong flow | Cần cả step-level và end-to-end |
| Risk | Thường hẹp | Theo task | Có thể tăng vì tool access và autonomy |

### 12.6. Single-agent và multi-agent

Nhiều agent không tự động tạo independent review. Nếu các agent dùng cùng model, context và assumption, chúng có thể lặp lại cùng lỗi. Independence cần khác biệt về role, evidence hoặc validation, không chỉ khác tên agent.

### 12.7. Model và tool change

Prompt/workflow có thể thay đổi behavior khi model hoặc tool đổi. Vì vậy workflow quan trọng cần representative evaluation set và version record. “Model mới hơn” không bảo đảm phù hợp hơn với use case cụ thể.

### 12.8. Điều cần nhớ

- Prompt là một phần nhỏ của workflow.
- Agent autonomy phải đi cùng scope, permission và evidence.
- Multi-agent không thay human accountability hoặc independent validation.

Đọc tiếp: Playbook Mục 6 và các use case; governance policy cho agent authority.

## 13. Failure chain xuyên SDLC

### 13.1. Mục tiêu học tập

Hiểu một lỗi ban đầu có thể lan qua nhiều role và artifact.

### 13.2. Case study

Giả sử requirement “user chỉ xem được dữ liệu thuộc đơn vị của mình” chưa định nghĩa cách xử lý user thuộc nhiều đơn vị.

1. AI tóm tắt requirement và chọn assumption “một user chỉ thuộc một đơn vị”.
2. Developer tạo implementation theo assumption đó.
3. AI sinh unit test từ implementation nên test cũng dùng cùng assumption.
4. QC dùng cùng summary và không có domain rule đầy đủ nên không tạo multi-unit scenario.
5. Tech Lead review diff nhưng thiếu original requirement và decision context.
6. Team Lead thấy task hoàn thành nhanh.
7. Production có user nhiều đơn vị và permission hoạt động sai.
8. QA thiếu traceability nên khó xác định assumption xuất hiện ở đâu.

### 13.3. Vì sao nhiều lớp review vẫn bỏ sót?

Các role không độc lập nếu dùng cùng context thiếu. Nhiều lần review không bù được một source-of-truth gap chung.

Control cần xuất hiện tại nhiều điểm:

- Clarification trước implementation.
- Domain rule làm source of truth.
- Test oracle độc lập với implementation.
- Review có requirement và impact context.
- Evidence trace từ acceptance tới test.

Các bước cụ thể nằm trong Playbook, không được duy trì lại tại Handbook.

### 13.4. Điều cần nhớ

- Failure thường xuyên role và xuyên artifact.
- Independence đến từ source, role và evidence, không chỉ số lượt AI review.
- Root-cause improvement có thể cần sửa knowledge, workflow hoặc policy.

Đọc tiếp: Playbook UC-01, UC-03, UC-05 và Mục 21.

## 14. Adoption và pilot

### 14.1. Mục tiêu học tập

Hiểu cách bắt đầu nhỏ và tránh áp dụng AI trên diện rộng trước khi có evidence.

### 14.2. Chọn pilot

Pilot tốt thường có:

- Tần suất đủ cao để quan sát pattern.
- Risk thấp hoặc trung bình theo policy/pilot rule.
- Output và quality có thể đo.
- Owner và reviewer sẵn sàng.
- Baseline trước AI.

Ví dụ phù hợp để cân nhắc:

- Phân tích task và clarification.
- Lập implementation plan.
- Sinh test ideas từ acceptance criteria.
- Draft release note từ evidence đã xác minh.

### 14.3. Tránh rollout theo tool

Không bắt đầu bằng “cấp tool cho toàn bộ team rồi đo adoption”. Hãy bắt đầu bằng use case, outcome, risk và evidence. Một tool có thể phù hợp với code explanation nhưng không phù hợp với security-sensitive incident.

### 14.4. Capability và training

Training không nên chỉ dạy prompt. Người dùng cần biết:

- Chọn source/context.
- Nhận diện hallucination và uncertainty.
- Review output theo domain.
- Giữ data boundary.
- Escalate khi vượt authority.

### 14.5. Điều kiện mở rộng

Chỉ mở rộng khi:

- Quality không giảm so với baseline.
- Rework và review cost được hiểu.
- Failure có handling rõ.
- Policy và tool boundary đủ dùng.
- Team có capacity hỗ trợ adoption.

### 14.6. Điều cần nhớ

- Pilot use case, không pilot “AI nói chung”.
- Bắt đầu nhỏ, đo end-to-end và giữ feedback loop.
- Adoption rate không phải success metric độc lập.

Đọc tiếp: Playbook UC-01/02/05 và Mục 21.

## 15. Measurement và continuous improvement

### 15.1. Mục tiêu học tập

Hiểu cách đánh giá AI dựa trên outcome thay vì activity.

### 15.2. Baseline

Không có baseline, team không biết AI tạo improvement hay chỉ chuyển chi phí. Baseline cần phản ánh cùng loại task và quality expectation.

### 15.3. Nhóm metric

| Nhóm | Ví dụ |
| --- | --- |
| Flow | Lead time, cycle time, review wait time |
| Quality | Rework, escaped defect, rollback, test effectiveness |
| Review | Diff size, review round, confirmed finding, noise rate |
| Knowledge | Context retrieval time, stale-context incident |
| Adoption | Use case completion, exception và abandonment rate |
| Safety | Policy violation, sensitive-data incident, gate bypass |
| Cost | Tool cost, review cost và maintenance cost |

### 15.4. Metric dễ gây hiểu nhầm

- Số dòng code.
- Số prompt.
- Số người đã mở tool.
- Số task tự khai báo “có AI”.
- Thời gian generation nhưng không tính review/rework.

Các metric này có thể là telemetry nhưng không nên được dùng độc lập để kết luận productivity.

### 15.5. Feedback loop

Kết quả pilot có thể dẫn tới ba loại thay đổi:

- **Knowledge gap** → cập nhật Handbook hoặc source context.
- **Workflow gap** → cập nhật Playbook use case.
- **Control gap** → policy owner xem xét thay đổi rule/gate.

### 15.6. Điều cần nhớ

- Đo end-to-end outcome và downstream cost.
- Kết hợp metric định lượng với feedback theo role.
- Failure lặp lại phải dẫn tới thay đổi có owner.

Đọc tiếp: Playbook Mục 21 về feedback; documentation specification về traceability.

## 16. Tiêu chí tự kiểm tra sau khi đọc Handbook

Người đọc nên có thể trả lời:

1. Operating Model khác Platform ở điểm nào?
2. Vì sao AI output nhanh có thể làm lead time của team tăng?
3. Source of truth và AI-facing context khác nhau thế nào?
4. Tại sao code và test do cùng AI sinh có thể cùng sai?
5. Khi nào cần chuyển từ Handbook sang Playbook?
6. Khi nào cần policy owner thay vì tự quyết?
7. Role của mình giữ accountability nào?
8. Metric nào phản ánh outcome tốt hơn số prompt hoặc dòng code?

Nếu chưa trả lời được, quay lại chapter liên quan hoặc trao đổi với role owner trước khi tham gia high-risk use case.

## 17. Authority và dependency gaps

Handbook đang ở trạng thái `proposed`; các nội dung mô tả risk, security và quality gate chỉ giải thích rationale.

Các dependency cần được tạo trước khi Handbook trở thành baseline chính thức:

- AI governance policy.
- Risk-level policy.
- Quality-gate policy.
- Security/data-handling policy.
- Document standard và glossary canonical.
- Approval/exception authority.

Khi policy chưa tồn tại, không được diễn giải nội dung Handbook như rule đã được tổ chức phê duyệt.

## 18. Tài liệu liên quan

- [`handbook-specification.md`](./handbook-specification.md): yêu cầu nội dung và chất lượng Handbook.
- [`documentation-specification.md`](./documentation-specification.md): kiến trúc bộ tài liệu.
- [`playbook-v1.md`](./playbook-v1.md): workflow, use case và checklist thực hành.
- [`playbook-specification.md`](./playbook-specification.md): yêu cầu nội dung Playbook.
- [`aiom-document-structure.md`](./aiom-document-structure.md): topology tài liệu đề xuất.
- [`AI-engineering-operating-system-open-questions.md`](./AI-engineering-operating-system-open-questions.md): decision backlog.
