---
id: PLAYBOOK-ai-engineering-operating-model-v1
title: AI Engineering Operating Model Playbook V1
status: proposed
version: 1.1.0
type: playbook
scope: global
source_of_truth: false
owner: engineering-leadership
created_at: 2026-07-13
updated_at: 2026-07-13
review_cycle: quarterly
based_on: ./playbook-specification.md
---

# AI Engineering Operating Model Playbook V1

## 1. Mục đích

Playbook này giúp engineering team áp dụng **AI Engineering Operating Model** vào công việc hằng ngày thông qua workflow, use case và checklist có thể thực hiện trực tiếp.

Tài liệu trả lời:

- Khi nào nên hoặc không nên dùng AI?
- Ai thực hiện, review, approve và chịu trách nhiệm?
- AI cần đọc context nào?
- Output phải được kiểm tra và lưu evidence ra sao?
- Khi nào phải dừng hoặc escalation?
- Xử lý thế nào khi AI sai, thiếu context hoặc vượt scope?

Kiến thức nền và giải thích chi tiết không thuộc Playbook. Nội dung đó sẽ nằm trong Handbook theo [`handbook-specification.md`](./handbook-specification.md).

## 2. Authority và policy dependencies

Playbook đang ở trạng thái `proposed`, dùng cho review và pilot. Playbook không phải source of truth cho risk, security, quality gate hoặc approval authority.

Các policy sau phải tồn tại trước khi Playbook được promote thành `accepted`:

| Dependency | Authority cần cung cấp |
| --- | --- |
| AI governance policy | Quyền tự chủ, forbidden action và human accountability |
| Risk-level policy | Cách phân loại low, medium và high risk |
| Quality-gate policy | Gate bắt buộc theo task và risk |
| Security policy | Tool, dữ liệu, privacy, incident và retention boundary |
| Document standard | Metadata, promotion, freshness và lifecycle |

Cho tới khi policy tồn tại, các nhãn risk/classification trong V1 chỉ là **đề xuất cho pilot**, không phải baseline bắt buộc.

## 3. Quick start

### 3.1. Checklist trước khi bắt đầu

- [ ] Outcome của task đã rõ.
- [ ] In-scope và out-of-scope đã rõ.
- [ ] Accountable owner đã được xác định.
- [ ] Source of truth đã được xác định.
- [ ] Risk đã được phân loại theo policy hoặc pilot rule được phê duyệt.
- [ ] Use case phù hợp đã được chọn.
- [ ] Reviewer/approver và validation đã được xác định.
- [ ] Dữ liệu được phép dùng với AI tool đã được kiểm tra.

Nếu chưa thể đánh dấu một mục, phải làm rõ trước khi yêu cầu AI tạo output quan trọng.

### 3.2. Chọn use case

| Nhu cầu | Use case |
| --- | --- |
| Làm rõ requirement | UC-01 |
| Lập implementation plan | UC-02 |
| Implementation hoặc refactoring | UC-03 |
| Code review | UC-04 |
| Test design | UC-05 |
| Defect analysis và bug fix | UC-06 |
| RFC hoặc ADR | UC-07 |
| Release readiness | UC-08 |
| Incident analysis | UC-09 |
| Knowledge maintenance | UC-10 |

### 3.3. Phân loại quyền sử dụng AI

Mỗi use case dùng một trong bốn nhãn; authority cuối cùng phải lấy từ policy:

- **Recommended** — có thể dùng AI theo workflow chuẩn.
- **Conditional** — chỉ dùng khi đủ context, gate hoặc approval bổ sung.
- **Human-led** — AI hỗ trợ; con người thực hiện quyết định chính.
- **Forbidden** — policy không cho phép giao hành động cho AI.

### 3.4. Thuật ngữ tối thiểu

- **Source of truth**: nguồn chính thức được ưu tiên khi thông tin khác nhau.
- **Context**: thông tin AI cần để hiểu và thực hiện task.
- **Evidence**: test result, log, review hoặc bằng chứng dùng để kiểm chứng output.
- **Quality gate**: điều kiện phải đạt trước khi chuyển bước.
- **Accountable owner**: người chịu trách nhiệm cuối cùng cho outcome.

Các thuật ngữ khác phải liên kết tới glossary canonical khi Handbook được tạo.

## 4. Điểm phải dừng và escalation

Dừng phần công việc liên quan và hỏi role có thẩm quyền khi:

- Requirement, expected behavior hoặc source of truth mâu thuẫn.
- Không xác định được accountable owner hoặc risk.
- Task chạm secret, thông tin định danh cá nhân, production data hoặc security boundary chưa được phép.
- AI đề xuất breaking change, dependency mới hoặc thay đổi ngoài scope.
- Không thể giải thích hoặc kiểm chứng output quan trọng.
- Gate yêu cầu reviewer/approver nhưng chưa có người phù hợp.
- AI và human reviewer bất đồng về quyết định có impact lớn.

| Tình huống | Escalation mặc định |
| --- | --- |
| Business rule/requirement | Product hoặc initiative owner |
| Architecture/technical direction | Tech Lead hoặc architecture owner |
| Test oracle/quality acceptance | QC/QA owner |
| Security/data handling | Security hoặc data owner |
| Scope/capacity/priority | Team Lead hoặc task owner |
| Production incident | Incident Commander |

Tên role có thể khác theo tổ chức; accountable authority không được bỏ trống.

## 5. Context-loading checklist

### 5.1. Mọi task

- [ ] Mục tiêu và expected outcome.
- [ ] In-scope và out-of-scope.
- [ ] Acceptance criteria hoặc Definition of Done.
- [ ] Repo/module/domain bị ảnh hưởng.
- [ ] Engineering convention liên quan.
- [ ] Constraint, risk và decision đã biết.

### 5.2. Theo loại task

| Task | Context bổ sung |
| --- | --- |
| Feature | PRD, business rule, RFC/ADR và API contract liên quan |
| Bug fix | Reproduction, expected behavior, sanitized log và regression history |
| Refactor | Behavior cần bảo toàn, dependency và characterization test |
| Database change | Schema, data volume, migration và rollback constraint |
| Security change | Threat model, data classification và security policy |
| Test design | Acceptance criteria, risk, architecture và defect history |
| Release | Change list, test evidence, dependency, observability và rollback |

### 5.3. Context conflict

Nếu context thiếu, stale hoặc mâu thuẫn:

1. Dừng kết luận phụ thuộc vào thông tin đó.
2. Tách fact, assumption và conflict.
3. Xác định source/owner có authority.
4. Yêu cầu clarification hoặc decision.
5. Cập nhật source of truth trước khi tiếp tục.

Không bắt AI đọc toàn bộ repository theo mặc định. Chỉ mở rộng context khi task, dependency hoặc evidence yêu cầu.

## 6. Standard AI-assisted workflow

```text
Frame → Classify → Load → Plan → Execute → Verify → Promote → Learn
```

- [ ] **Frame** — ghi outcome, scope, owner và Definition of Done.
- [ ] **Classify** — xác định task type, quyền dùng AI và risk.
- [ ] **Load** — nạp context từ source of truth.
- [ ] **Plan** — xác định bước làm, validation và gate.
- [ ] **Execute** — tạo output nhỏ, có thể hiểu và review.
- [ ] **Verify** — chạy test, review và thu evidence.
- [ ] **Promote** — human owner nhận trách nhiệm và cập nhật artifact chính thức.
- [ ] **Learn** — ghi feedback hoặc failure để cải tiến workflow/context.

### Evidence tối thiểu

Với output được commit hoặc dùng để ra quyết định, lưu:

- Task/initiative liên quan.
- Scope và risk/classification.
- Source chính đã sử dụng.
- Assumption hoặc unresolved question quan trọng.
- Validation và kết quả.
- Reviewer/approver theo policy.

Không mặc định lưu toàn bộ raw chat. Lưu rationale và evidence đủ để người khác hiểu và kiểm chứng kết quả.

## 7. Dấu hiệu output không đáng tin cậy

Không promote output nếu:

- AI trình bày assumption như fact nhưng không chỉ source.
- File, API, dependency, test result hoặc tài liệu được nhắc tới không tồn tại.
- Output bỏ qua constraint hoặc tự thay đổi requirement.
- Kết luận thay đổi lớn khi diễn đạt lại prompt nhưng không có evidence mới.
- Code pass một test hẹp nhưng không giải thích được failure path hoặc impact.
- AI khẳng định đã đọc, chạy test hoặc review nguồn mà nó không truy cập.
- Output yêu cầu làm yếu assertion, security control hoặc quality gate.

## 8. Template use case

Mỗi use case trong V1 phải được đọc theo cùng cấu trúc:

1. Mục tiêu.
2. Classification.
3. Khi áp dụng/không áp dụng.
4. Role và accountable owner.
5. Risk/policy reference.
6. Input/source of truth.
7. Workflow checklist.
8. Expected output.
9. Validation/gate.
10. Evidence.
11. Failure/handling.
12. Best practice/anti-pattern.
13. Metric.
14. Related knowledge/policy.

Các policy link chưa tồn tại được ghi là `dependency gap`.

## 9. UC-01 — Phân tích requirement

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Tìm ambiguity, missing information, dependency và risk trước implementation |
| Classification | Recommended |
| Áp dụng | Có task description, Product Brief hoặc PRD |
| Không áp dụng | Không dùng AI tự quyết business rule chưa được owner xác nhận |
| Role | Executor: Developer/QC/Team Lead; Accountable: task owner; Approver clarification: Product owner |
| Risk/policy | Theo risk của initiative; risk policy là dependency gap |
| Input | Requirement, glossary, business rule, decision và constraint liên quan |
| Output | Clarification list, assumption log và impact hypothesis |
| Validation/gate | Owner xác nhận thay đổi requirement |
| Evidence | Link source và câu trả lời authoritative |
| Metric | Clarification trước implementation; rework do requirement gap |
| Related | Handbook problem/context chapters; AI governance policy dependency gap |

Workflow:

- [ ] Tóm tắt mục tiêu mà không thêm requirement.
- [ ] Tách fact, constraint, assumption và open question.
- [ ] Liệt kê acceptance scenario và edge case còn thiếu.
- [ ] Xác định domain/module/dependency có thể ảnh hưởng.
- [ ] Gửi câu hỏi cho owner; không tự trả lời thay owner.
- [ ] Cập nhật source sau khi có xác nhận.

Failure/handling:

- AI thêm requirement → đánh dấu proposal và yêu cầu owner quyết định.
- Source mâu thuẫn → dừng kết luận, chỉ rõ từng source.
- Summary làm mất nuance → đối chiếu từng acceptance criterion.

Best practice: yêu cầu mỗi phát hiện quan trọng trỏ tới source. Anti-pattern: dùng AI summary thay cho source document.

## 10. UC-02 — Lập implementation plan

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Tạo plan nhỏ, reviewable và có validation trước khi sửa code |
| Classification | Recommended cho pilot low/medium; Conditional cho high-risk |
| Áp dụng | Requirement và scope đủ rõ |
| Không áp dụng | Context/code chưa được inspect hoặc high-risk change chưa có reviewer |
| Role | Executor: Developer; Reviewer: Tech Lead/qualified reviewer; Accountable: task owner |
| Risk/policy | Theo thay đổi dự kiến; risk policy là dependency gap |
| Input | Requirement, repo/module map, code, test, convention và ADR/RFC |
| Output | Implementation plan, impact list và test plan sơ bộ |
| Validation/gate | Scope và architecture constraint được reviewer kiểm tra |
| Evidence | Source, affected module và review decision |
| Metric | Plan deviation, review round và rework |
| Related | Handbook context/architecture chapters; quality-gate policy dependency gap |

Workflow:

- [ ] Xác định current behavior từ code và test.
- [ ] Liệt kê file/module dự kiến ảnh hưởng.
- [ ] Chia thành bước có thể verify độc lập.
- [ ] Gắn validation cho từng bước.
- [ ] Nêu migration, compatibility, rollout và rollback nếu liên quan.
- [ ] Review plan trước medium/high-risk execution.

Failure/handling: plan suy đoán code → inspect trước khi chốt; refactor ngoài scope → tách task; thiếu rollback high-risk → dừng và bổ sung.

Best practice: mỗi bước có completion condition. Anti-pattern: plan chỉ ghi “implement, test, deploy”.

## 11. UC-03 — Implementation và refactoring

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Tạo change đúng scope, phù hợp convention và maintainable |
| Classification | Recommended cho change nhỏ; Conditional theo risk |
| Áp dụng | Có plan và validation strategy |
| Không áp dụng | Production/destructive action không approval; breaking change chưa xác nhận |
| Role | Executor/Accountable code: Developer; Reviewer: peer/Tech Lead |
| Risk/policy | Theo impact; AI governance và risk policy là dependency gap |
| Input | Plan, relevant code/test, convention và architecture constraint |
| Output | Code, test và document change cần thiết |
| Validation/gate | Build/lint/test, manual check khi cần và independent review |
| Evidence | Test result, scope deviation và unresolved risk |
| Metric | Diff size, review round, rework và regression |
| Related | Handbook role/failure chapters; engineering standard |

Workflow:

- [ ] Chọn một bước nhỏ trong plan.
- [ ] Nêu scope và convention cụ thể cho AI.
- [ ] Review diff ngay sau mỗi bước.
- [ ] Chạy static check và targeted test.
- [ ] Giải thích behavior, trade-off và failure path.
- [ ] Lặp lại; không tích lũy diff lớn chưa kiểm tra.

Failure/handling: hallucinated API → kiểm tra code/docs; diff vượt scope → tách bỏ; test bị làm yếu → khôi phục và sửa root cause; không hiểu code → không submit.

Best practice: một concern cho mỗi change set. Anti-pattern: chấp nhận code chỉ vì test hẹp đang pass.

## 12. UC-04 — Code review

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Hỗ trợ tìm correctness risk, inconsistency và missing validation |
| Classification | Recommended như review bổ sung; Human-led cho approval |
| Áp dụng | Có requirement, diff và test evidence |
| Không áp dụng | Không dùng AI làm approver duy nhất |
| Role | Executor: reviewer; Accountable: human reviewer theo policy |
| Risk/policy | Theo change; review/quality policy là dependency gap |
| Input | Requirement, plan, diff, tests, convention và ADR |
| Output | Finding có evidence và follow-up đề xuất |
| Validation/gate | Human xác minh finding và review critical path độc lập |
| Evidence | Finding, location, severity và resolution |
| Metric | Confirmed finding rate, noise rate và escaped defect |
| Related | Handbook review failure; quality-gate policy dependency gap |

Workflow:

- [ ] Human đọc mục tiêu và risk trước.
- [ ] Dùng AI kiểm tra correctness, edge case, security, compatibility và test gap.
- [ ] Yêu cầu finding trỏ tới diff/source.
- [ ] Human xác minh finding và loại noise.
- [ ] Review critical path trực tiếp.
- [ ] Human đưa ra decision cuối cùng.

Failure/handling: chỉ nhận xét style → thêm risk checklist; thiếu dependency context → mở rộng có chọn lọc; automation bias → human review độc lập.

Best practice: coi finding là hypothesis. Anti-pattern: approve vì AI không tìm thấy lỗi.

## 13. UC-05 — Test design

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Mở rộng test ideas theo business risk |
| Classification | Recommended |
| Áp dụng | Có acceptance criteria và source xác định expected behavior |
| Không áp dụng | Không giao AI quyền xác định expected truth |
| Role | Executor/Accountable: QC; Consulted: Developer/Product/Tech Lead |
| Risk/policy | Theo feature; test/quality policy là dependency gap |
| Input | Acceptance criteria, business rule, architecture, data constraint và defect history |
| Output | Risk-based test set và traceability matrix |
| Validation/gate | Expected result có source; critical risk có coverage |
| Evidence | Test execution result và defect link |
| Metric | Risk coverage, defect detection và duplicate test rate |
| Related | Handbook QC/failure chapters; testing strategy |

Workflow:

- [ ] Map acceptance criterion tới test objective.
- [ ] Tạo happy, boundary, negative, state-transition và permission scenario.
- [ ] Bổ sung scenario từ architecture và defect history.
- [ ] QC kiểm chứng expected result.
- [ ] Loại test trùng và ưu tiên theo risk.
- [ ] Giữ exploratory testing charter riêng.

Failure/handling: nhiều test nhưng coverage thấp → nhóm theo risk; expected result không có source → hỏi owner; bỏ exploratory test → khôi phục session độc lập.

Best practice: yêu cầu scenario phá vỡ assumption. Anti-pattern: xem generated list là test plan hoàn chỉnh.

## 14. UC-06 — Defect analysis và bug fix

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Tái hiện lỗi, kiểm tra root-cause hypothesis và tạo fix có regression evidence |
| Classification | Recommended cho analysis; Conditional cho fix |
| Áp dụng | Có expected/actual behavior và reproduction evidence |
| Không áp dụng | Không sửa theo log hoặc hypothesis chưa xác minh |
| Role | QC: evidence; Developer: fix; Tech Lead: review theo risk; Accountable: task owner |
| Risk/policy | Theo affected behavior; risk policy là dependency gap |
| Input | Reproduction, environment, sanitized log, recent change và related test |
| Output | Root cause, minimal fix và regression test |
| Validation/gate | Reproduce trước; failing/passing evidence; regression scope |
| Evidence | Fact, hypothesis, experiment và result |
| Metric | Time to reproduce, re-open rate và regression |
| Related | Handbook defect/failure chapters; security policy cho log |

Workflow:

- [ ] Xác nhận reproduction và expected behavior.
- [ ] Tách evidence khỏi hypothesis.
- [ ] Tạo hypothesis có thể falsify.
- [ ] Kiểm tra bằng log, code hoặc experiment.
- [ ] Thêm regression test khi phù hợp.
- [ ] Tạo fix tối thiểu và chạy regression.

Failure/handling: evidence thiếu → thu thêm; fix symptom → kiểm tra causal chain; log nhạy cảm → sanitize/dừng theo security process.

Best practice: ghi hypothesis đã loại. Anti-pattern: áp dụng patch đầu tiên AI đề xuất.

## 15. UC-07 — RFC và ADR

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Hỗ trợ phân tích option/trade-off, giữ decision ở con người |
| Classification | Human-led |
| Áp dụng | Có problem, constraint và decision criteria |
| Không áp dụng | Không yêu cầu AI tự chọn architecture cuối cùng |
| Role | Executor: author; Reviewer/Accountable: Tech Lead/architecture owner |
| Risk/policy | Theo architecture impact; approval policy là dependency gap |
| Input | Current architecture, quality attributes, options và decision history |
| Output | RFC/ADR draft với options, rationale và consequences |
| Validation/gate | Claim được xác minh; qualified human approval |
| Evidence | Review, benchmark/official source và decision record |
| Metric | Decision rework, supersession và implementation deviation |
| Related | Handbook architecture/agent concepts; document standard |

Workflow:

- [ ] Tìm missing constraint và stakeholder concern.
- [ ] Tạo option như hypothesis.
- [ ] So sánh theo criteria đã thống nhất.
- [ ] Xác minh technology claim.
- [ ] Human reviewers thảo luận và quyết định.
- [ ] Ghi rationale, consequence và supersession.

Failure/handling: generic best practice xung đột local constraint → ưu tiên evidence; fabricated claim → loại; decision chỉ ở chat → tạo record trước implementation nếu gate yêu cầu.

Best practice: yêu cầu phản biện option ưu tiên. Anti-pattern: hỏi “kiến trúc tốt nhất” không có criteria.

## 16. UC-08 — Release readiness

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Tổng hợp evidence để human owner quyết định release |
| Classification | Human-led |
| Áp dụng | Có change list và test/release evidence |
| Không áp dụng | AI không tự đưa ra go/no-go |
| Role | Developer/QC: evidence; Team Lead: accountable; QA/Tech Lead: consulted |
| Risk/policy | Theo release; release/quality policy là dependency gap |
| Input | Changes, acceptance, tests, known issue, migration, monitoring và rollback |
| Output | Readiness summary, open risk và release-note draft |
| Validation/gate | Evidence mapping và human go/no-go |
| Evidence | Test links, risk acceptance, approval và rollback |
| Metric | Rollback, escaped defect và missing-gate rate |
| Related | Handbook release/traceability concepts; release policy |

Workflow:

- [ ] Map change tới acceptance và evidence.
- [ ] Tìm missing gate, defect và dependency risk.
- [ ] Xác nhận migration, flag, monitoring và rollback.
- [ ] Draft summary chỉ từ evidence đã xác minh.
- [ ] Human owner quyết định go/no-go.

Failure/handling: claim “all tests passed” thiếu link → loại/bổ sung; known issue bị làm nhẹ → ghi severity/owner; high-risk thiếu rollback → dừng hoặc approved exception.

Best practice: tách fact, risk acceptance và pending action. Anti-pattern: xem release note là approval.

## 17. UC-09 — Incident analysis

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Hỗ trợ triage/hypothesis, giữ production authority ở con người |
| Classification | Conditional và Human-led |
| Áp dụng | Tool/data được phép và Incident Commander kiểm soát workflow |
| Không áp dụng | AI không tự chạy production/destructive action |
| Role | Accountable: Incident Commander; Operators: human; AI: hỗ trợ tổng hợp |
| Risk/policy | High mặc định cho production incident; incident/security policy dependency gap |
| Input | Sanitized alert, timeline, log, metric, topology và runbook |
| Output | Timeline, hypothesis và postmortem draft |
| Validation/gate | Human xác minh trước action; fact/inference được tách |
| Evidence | Actor, action, time, result và source signal |
| Metric | Time to mitigate, false hypothesis và action reversal |
| Related | Handbook incident/risk concepts; incident response policy |

Workflow:

- [ ] Ưu tiên containment và runbook.
- [ ] Lập timeline từ fact đã xác minh.
- [ ] Dùng AI nhóm signal và tạo hypothesis.
- [ ] Human xác minh trước mọi action.
- [ ] Ghi action, actor, timestamp và result.
- [ ] Draft postmortem từ evidence sau incident.

Failure/handling: destructive suggestion → không chạy và escalate; sensitive log → dừng/sanitize; timeline lẫn inference → tách lại.

Best practice: dùng AI giảm tải tổng hợp. Anti-pattern: giao quyền chỉ huy hoặc production access cho AI.

## 18. UC-10 — Knowledge maintenance

| Trường | Nội dung |
| --- | --- |
| Mục tiêu | Đồng bộ source document và AI-facing context sau change |
| Classification | Recommended cho draft/detection; Human-led cho promotion |
| Áp dụng | Có merged change hoặc accepted decision |
| Không áp dụng | Không để AI-facing context mới hơn source of truth |
| Role | Executor: contributor; Accountable: document owner |
| Risk/policy | Theo artifact; document standard là dependency gap |
| Input | Change, decision, current document và metadata |
| Output | Updated official document, context/map và registry |
| Validation/gate | Human semantic review; source cập nhật trước AI layer |
| Evidence | Change/decision link, owner và source revision |
| Metric | Stale-link/context incident và update delay |
| Related | Handbook knowledge concepts; document standard |

Workflow:

- [ ] Xác định document/context bị ảnh hưởng.
- [ ] Đề xuất update và stale link.
- [ ] Human owner kiểm tra semantic accuracy.
- [ ] Cập nhật source of truth trước.
- [ ] Refresh AI-facing summary và revision.
- [ ] Update registry/freshness metadata.

Failure/handling: AI context mới hơn source → không promote; duplicate knowledge → giữ canonical source; thiếu owner → không đánh dấu accepted.

Best practice: document update thuộc Definition of Done khi behavior/decision đổi. Anti-pattern: giữ knowledge chỉ trong chat.

## 19. Xử lý tình huống dùng chung

### 19.1. AI output vượt scope

1. Không chấp nhận scope mới tự động.
2. Tách phần ngoài scope khỏi change hiện tại.
3. Đánh giá proposal bằng task/decision riêng.
4. Ghi failure nếu agent lặp lại hành vi.

### 19.2. AI và human reviewer bất đồng

1. Yêu cầu evidence và criterion từ hai phía.
2. Kiểm tra source, test hoặc experiment độc lập.
3. Escalate tới accountable owner.
4. Ghi decision/rationale nếu ảnh hưởng dài hạn.

### 19.3. Output không qua gate

1. Không làm yếu gate để đạt pass.
2. Xác định lỗi ở output, context, workflow hay gate configuration.
3. Sửa root cause và chạy lại validation.
4. Exception chỉ hợp lệ theo policy có authority, expiry và compensating control.

### 19.4. Model, prompt hoặc tool thay đổi

1. Xác định use case/risk bị ảnh hưởng.
2. Chạy representative evaluation set.
3. So sánh quality, failure, latency và cost với baseline.
4. Pilot giới hạn trước rollout.
5. Chuẩn bị rollback và version record.

### 19.5. Dữ liệu nhạy cảm bị gửi nhầm

1. Dừng workflow và không tiếp tục copy output.
2. Ghi tool, dữ liệu, thời điểm và phạm vi.
3. Báo theo security incident process.
4. Thực hiện revoke/rotation/deletion khi policy yêu cầu.
5. Chỉ tiếp tục khi incident owner cho phép.

## 20. Completion checklist

- [ ] Outcome, scope và accountable owner đã rõ.
- [ ] Risk/classification đã được xác định theo policy/pilot rule.
- [ ] AI chỉ đọc dữ liệu được phép từ source phù hợp.
- [ ] Assumption và unresolved question quan trọng đã được ghi.
- [ ] Output nằm trong scope và tuân thủ convention.
- [ ] Người thực hiện hiểu và giải thích được output.
- [ ] Test, review và gate tương ứng đã hoàn thành.
- [ ] Evidence cần thiết đã được lưu.
- [ ] Official document và AI-facing context bị ảnh hưởng đã cập nhật.
- [ ] Human owner đã quyết định promote hoặc release.

## 21. Feedback loop

Khi workflow phát hiện vấn đề:

1. Ghi evidence và use case liên quan.
2. Nếu lỗi cục bộ, cập nhật use case.
3. Nếu thiếu giải thích/knowledge, cập nhật Handbook sau khi được tạo.
4. Nếu thiếu control/authority, gửi policy owner.
5. Review các use case bị ảnh hưởng.
6. Chạy regression evaluation phù hợp.

## 22. Tài liệu liên quan

- [`playbook-specification.md`](./playbook-specification.md): yêu cầu của Playbook.
- [`documentation-specification.md`](./documentation-specification.md): kiến trúc bộ tài liệu.
- [`handbook-specification.md`](./handbook-specification.md): yêu cầu kiến thức nền.
- [`aiom-document-structure.md`](./aiom-document-structure.md): topology tài liệu đề xuất.
- `AI-engineering-operating-system-open-questions.md`: decision backlog — **chưa tồn tại (dependency gap)**.
