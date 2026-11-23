---
id: GOV-document-structure
title: Document Structure for AI Engineering Operating Model
canonical_path: docs/governance/document-structure.md
status: proposed
owner: engineering-platform
created_at: 2026-07-09
updated_at: 2026-11-23
type: governance
purpose: standard
scope: global
source_of_truth: false
proposed_source_of_truth_for:
  - document-structure
ai_usage: allowed
freshness:
  review_cycle: quarterly
  last_reviewed_at:
---

# Document Structure for AI Engineering Operating Model

## Mục Lục

- [1. Mục đích](#1-mục-đích)
- [2. Nguyên tắc chung](#2-nguyên-tắc-chung)
- [3. Cấu trúc cho single repo](#3-cấu-trúc-cho-single-repo)
- [4. Cấu trúc cho multi repo](#4-cấu-trúc-cho-multi-repo)
- [5. Vai trò các thư mục chung](#5-vai-trò-các-thư-mục-chung)
- [6. Vai trò của `.ai/`](#6-vai-trò-của-ai)
- [7. Quy tắc đặt tài liệu](#7-quy-tắc-đặt-tài-liệu)
- [8. Quality Gate](#8-quality-gate)
- [9. Naming Convention](#9-naming-convention)
- [10. Metadata chuẩn cho tài liệu](#10-metadata-chuẩn-cho-tài-liệu)
- [11. Document Lifecycle](#11-document-lifecycle)
- [12. Traceability](#12-traceability)
- [13. Ownership](#13-ownership)
- [14. Quy tắc tránh duplicate](#14-quy-tắc-tránh-duplicate)
- [15. Security Rules](#15-security-rules)
- [16. Quy tắc AI đọc context](#16-quy-tắc-ai-đọc-context)
- [17. Quyết định áp dụng](#17-quyết-định-áp-dụng)

Các anchor trong mục lục dùng format GitHub Markdown. Nếu tài liệu được publish qua renderer hoặc tooling không hỗ trợ anchor tiếng Việt có dấu, cần chuyển mục lục sang anchor ASCII ổn định trong bước publish.

## 1. Mục đích

Định nghĩa topology tài liệu, trách nhiệm của từng thư mục và quy tắc xác định vị trí canonical của tài liệu trong single-repo và multi-repo.

Tài liệu áp dụng cho hai trường hợp repo:

- **Single repo**: một repository vừa là control plane vừa là execution area.
- **Multi repo**: một workspace root quản lý nhiều repository con.

Trong `docs/` của mỗi project, tài liệu tách một **lớp Operating Model** — nơi lưu Operating Model, Platform, Handbook và Playbook — khỏi lớp delivery (initiative/domain/reference). Chi tiết ở Mục 2.2–2.4.

Mục tiêu là giúp team:

- Chuẩn hóa nơi lưu Product Brief, Proposal, PRD, RFC, ADR, impact analysis, test plan, release note và decision log.
- Tách bạch tài liệu chính thức cho con người và tài liệu vận hành cho AI.
- Giúp AI/agent có context rõ ràng khi tham gia planning, implementation, review, testing và release.
- Giảm rủi ro duplicate, outdated document và sai lệch source of truth.
- Hỗ trợ traceability từ initiative tới domain, repo/module, Jira, code, test và release.
- Tạo nền tảng cho AI-assisted development và multi-agent workflow có kiểm soát.
- Tách lớp Operating Model (cách tổ chức làm việc với AI) khỏi lớp delivery (initiative/domain/reference) ngay trong `docs/` của project.

---

## 2. Nguyên tắc chung

Mô hình được chọn:

```text
Hybrid + .ai Operating Layer
```

Nguyên tắc quan trọng:

```text
docs/ là source of truth.
.ai/ là AI-facing operating layer.
```

`.ai/` không thay thế `docs/`. Các file trong `.ai/` phải tóm tắt, định tuyến hoặc hướng dẫn AI dựa trên tài liệu chính thức trong `docs/`.

Tài liệu này đang là bản staging tại `aiom-document-structure.md`. Khi được chấp nhận, file này phải được chuyển tới `docs/governance/document-structure.md` để khớp `canonical_path`.

Khi `status: accepted`, tài liệu này là source of truth cho cấu trúc thư mục và vị trí đặt tài liệu. Nó không phải source of truth chi tiết cho naming, metadata schema, risk gate hoặc AI governance:

- Naming chi tiết: `docs/governance/document-naming.md`
- Metadata schema, validation và lifecycle chi tiết: `docs/governance/document-standard.md`
- Risk gate chi tiết: `docs/governance/risk-level-policy.md`
- AI governance chi tiết: `docs/governance/ai-governance.md`
- Security chi tiết (secrets, PII, log, production data, sanitize, retention): `docs/governance/security-policy.md`

Trước khi promote tài liệu này sang `accepted`, các tài liệu governance được reference ở trên phải tồn tại ít nhất ở mức skeleton có owner, status và phạm vi rõ ràng. Nếu chưa tồn tại, phần tương ứng trong tài liệu này chỉ được hiểu là boundary và vị trí lưu, không phải policy chi tiết có thể enforce.

Vì tài liệu này đang ở trạng thái `proposed`, `source_of_truth` phải là `false`. Các câu mang tính bắt buộc như "phải", "không được", "required" hoặc "MUST" được hiểu là chuẩn đề xuất cho review/pilot, không phải baseline bắt buộc. Sau khi tài liệu được chuyển sang `accepted`, các quy tắc đó mới trở thành baseline bắt buộc cho dự án áp dụng, `source_of_truth` mới được đổi thành `true`, và `proposed_source_of_truth_for` được đổi thành `source_of_truth_for`. Bước promote sang `accepted` phải ghi `approved_by` và `accepted_at` để có audit trail; định nghĩa và validation của hai field này thuộc `docs/governance/document-standard.md`.

### 2.1. Phân biệt theo loại repository

| Trường hợp  | Control plane  | Execution area | Impact chính             |
| ----------- | -------------- | -------------- | ------------------------ |
| Single repo | Repo root      | Repo root      | Module / domain / layer  |
| Multi repo  | Workspace root | Repo con       | Repo / module / contract |

Quy tắc chuyển đổi:

```text
Multi repo cần quản lý repo impact.
Single repo cần quản lý module impact.
```

### 2.2. Các lớp tài liệu trong project

`docs/` của project chứa hai lớp nội dung, tách theo **mục đích**, cộng execution area bên dưới:

```text
Operating Model layer  → cách tổ chức làm việc với AI (Operating Model, Platform, Handbook, Playbook, templates, checklists)
Delivery layer         → delivery của dự án (initiative, domain, reference, governance, registry)
Execution area         → source code, nơi thay đổi thật diễn ra
```

| Lớp             | Vị trí                                                                     | Chứa gì                         | Trả lời câu hỏi                       |
| --------------- | -------------------------------------------------------------------------- | ------------------------------- | ------------------------------------- |
| Operating Model | `docs/operating-model \| platform \| handbook \| playbooks \| templates \| checklists/` | Cách vận hành AI engineering | Team cần hiểu gì, theo nguyên tắc/gate nào |
| Delivery        | `docs/initiatives \| domains \| reference \| governance \| registry/`      | Tài liệu của một dự án          | Đang làm gì, ảnh hưởng đâu            |
| Execution       | repo con / source code                                                     | Code, test, local docs          | Hiện thực thay đổi                    |

Cả hai lớp trong `docs/` đều là source of truth cho người và được `.ai/` tóm tắt/định tuyến cho AI. Vị trí `docs/`: repo root cho single repo, workspace root cho multi repo (Mục 3–4).

Vì lớp Operating Model đặt trong `docs/` của project, mỗi project/workspace giữ bản riêng. Nếu tổ chức có nhiều workspace và muốn tránh phân kỳ, chọn một project làm canonical và project khác trỏ tới bằng frontmatter `source_context`, hoặc chấp nhận per-project theo chủ đích.

### 2.3. Lớp Operating Model trong `docs/`

Operating Model, Platform, Handbook và Playbook mô tả **cách tổ chức làm việc với AI**. Chúng đặt thành các area riêng trong `docs/`, tách khỏi lớp delivery (initiative/domain/reference) để không lẫn "cách làm" với "đang làm gì".

Áp dụng đúng nguyên tắc "không tạo file rỗng" (Mục 3.2, 5.1): chỉ tạo tài liệu khi có nhu cầu thật; các nhánh `people/`, `process/`... bắt đầu tối thiểu rồi bổ sung theo pilot.

```text
docs/
  operating-model/                     # Operating Model gồm gì (6 thành phần)
    README.md
    operating-model-overview.md
    principles.md
    people/                            # role, ownership, skill
      roles-and-responsibilities.md
      ownership-and-accountability.md
      skills-and-enablement.md
    process/                           # workflow, handoff, escalation
      ai-assisted-sdlc.md
      handoff-and-review.md
      escalation.md
    knowledge/                         # source of truth, context, lifecycle
      source-of-truth.md
      context-management.md
      knowledge-lifecycle.md
    technology/                        # capability, platform requirement, tool selection
      capability-model.md
      platform-requirements.md
      tool-selection-principles.md
    governance/                        # model/rationale — KHÔNG phải policy authoritative
      risk-and-control-model.md
      human-approval-model.md
      evidence-and-audit.md
    improvement/                       # pilot, adoption, metric, feedback
      pilot.md
      adoption.md
      metrics.md
      feedback-and-evaluation.md

  platform/                            # Platform cung cấp capability nào, vận hành ra sao
    README.md
    platform-overview.md
    capability-catalog.md
    approved-tools.md
    architecture.md
    model-and-ai/                      # model gateway, routing, evaluation
    developer-experience/              # IDE/assistant, prompt-skill library, onboarding
    agent-runtime/                     # runtime, orchestration, tool access
    delivery/                          # CI/CD, automated gate, release integration
    operations/                        # observability, cost, incident, SLO
    security/                          # access control, audit logging, data protection

  handbook/                            # Why/What — onboarding, alignment
    README.md
    # canonical hiện đang staging tại handbook-v1.md

  playbooks/                           # hướng dẫn thực thi cho CON NGƯỜI
    README.md
    # canonical hiện đang staging tại playbook-v1.md

  templates/                           # khuôn mẫu tạo artifact
    prd-template.md
    adr-template.md
    rfc-template.md
    impact-analysis-template.md
    test-plan-template.md
    release-note-template.md
    ai-evidence-template.md

  checklists/                          # checklist xác minh hoàn thành
    before-ai-task.md
    prd-review.md
    pull-request.md
    release-readiness.md
    incident-analysis.md

  # initiatives/ domains/ reference/ governance/ registry/ — xem Mục 3–5
  # AI-asset index đặt trong docs/registry/ (ai-asset-index, playbook-index, platform-capability-index, policy-to-rule-map) — xem Mục 5.5
```

Ghi chú:

- `handbook-v1.md`, `playbook-v1.md` và chính `aiom-document-structure.md` hiện là **bản staging ở repo root**. Khi được `accepted`, chúng chuyển tới `docs/handbook/`, `docs/playbooks/` và `docs/governance/document-structure.md` theo `canonical_path` tương ứng.
- `operating-model/governance/` chỉ chứa **model và rationale** (giống Handbook Ch 11), **không thay** policy authoritative. Policy risk/security/quality-gate/AI-governance vẫn ở `docs/governance/` theo Mục 5.4, 8, 15, 16.
- `templates/` và `checklists/` là canonical trong project; initiative tham chiếu, không copy.

### 2.4. Quan hệ giữa lớp Operating Model và lớp Delivery

Hai lớp cùng trong `docs/` nhưng khác vai trò; áp dụng mô hình source-of-truth như docs↔.ai (Mục 14):

- `docs/operating-model | platform | handbook | playbooks/` là source of truth cho **cách làm**. Lớp delivery (initiative/domain) **dùng** chúng qua link, không copy nội dung.
- Nếu cần AI đọc nhanh, tạo summary trong `.ai/context/` trỏ tới bằng frontmatter `source_context`, ví dụ `operating-model-summary.md`, `platform-capability-map.md`, `role-map.md`, `quality-gate-map.md`. Summary không override `docs/`.
- Policy authoritative (risk, security, quality gate, AI governance) vẫn ở `docs/governance/`; `operating-model/governance/` chỉ là model/rationale.
- **Playbook (cho người) ở `docs/playbooks/` tách khỏi workflow (cho AI) ở `.ai/workflows/`.** Một playbook có thể được operationalize thành `.ai/prompt` + `.ai/workflow`; liên kết bằng frontmatter, không copy nội dung.
- Khi tài liệu lớp Operating Model đổi, `.ai/` summary/adapter liên quan phải cập nhật hoặc đánh dấu `stale` (Mục 10, 14).

Mapping ví dụ:

```text
docs/playbooks/impact-analysis.md              # người: steps, gate, evidence, escalation
  → .ai/prompts/impact-analysis.md             # AI: prompt
  → .ai/workflows/... (impact analysis)        # AI: workflow

docs/operating-model/governance/risk-and-control-model.md  # model/rationale
  → docs/governance/risk-level-policy.md        # policy authoritative
  → .ai/rules/risk-level-rule.md                # AI-facing rule
```

---

## 3. Cấu trúc cho single repo

### 3.1. Khi nào dùng

Dùng cấu trúc single repo khi:

- Dự án chỉ có một repository chính.
- Backend, frontend, package hoặc service cùng nằm trong một repo.
- Không cần quản lý dependency, release và ownership giữa nhiều repo độc lập.

Single repo vẫn có thể là monorepo lớn. Khi đó vẫn cần quản lý module impact, domain impact, dependency map và API map, nhưng không cần cross-repo policy.

### 3.2. Cấu trúc chốt

Không cần tạo toàn bộ file ngay từ đầu. Initiative folder nên bắt đầu bằng bộ tối thiểu, sau đó bổ sung tài liệu theo risk, phạm vi và nhu cầu review.

Không tạo file rỗng chỉ để thỏa cấu trúc. Các file được đánh dấu required chỉ bắt buộc khi initiative bước vào lifecycle tương ứng như implementation, release hoặc audit.

```text
repo-root/
  docs/
    README.md

    operating-model/          # lớp Operating Model — xem Mục 2.3
    platform/                 # xem Mục 2.3
    handbook/                 # xem Mục 2.3
    playbooks/                # xem Mục 2.3 (hướng dẫn cho người)
    templates/                # xem Mục 2.3
    checklists/               # xem Mục 2.3

    initiatives/
      INIT-2026-001-user-permission-rework/
        README.md
        prd.md
        impact-analysis.md
        test-plan.md

        product-brief.md        # optional: khi cần làm rõ product intent
        proposal.md             # optional: khi có nhiều hướng giải quyết cần so sánh
        release-note.md         # optional: khi chuẩn bị release
        decision-log.md         # optional: khi có nhiều quyết định nhỏ

        rfc/                    # optional: khi cần thảo luận technical design
          RFC-2026-001-permission-model.md

        adr/                    # optional: khi có quyết định architecture dài hạn
          ADR-2026-001-use-policy-based-permission.md

    domains/
      permission/
        README.md
        business-rules.md
        architecture.md
        api-contracts.md
        test-notes.md
        decision-index.md

    reference/
      glossary.md
      architecture/
        system-overview.md
        backend-overview.md
        frontend-overview.md
        deployment-overview.md

      engineering/
        coding-standard.md
        api-guidelines.md
        database-migration-guidelines.md
        frontend-state-management.md

      testing/
        testing-strategy.md
        regression-checklist.md
        test-case-standard.md

      release/
        release-process.md
        release-gate.md
        rollback-guide.md

      operations/
        runbook-index.md
        troubleshooting.md
        incident-process.md
        postmortem-template.md

    governance/
      document-structure.md
      document-standard.md
      document-naming.md
      quality-gates.md
      risk-level-policy.md
      ai-governance.md
      security-policy.md

    registry/
      initiative-index.md
      domain-index.md
      prd-index.md
      rfc-index.md
      adr-index.md
      jira-map.md
      module-index.md

  .ai/
    README.md

    context/
      repo-map.md
      module-map.md
      domain-map.md
      initiative-map.md
      business-glossary.md
      coding-conventions.md
      testing-context.md
      api-map.md
      dependency-map.md

    rules/
      ai-usage-policy.md
      context-loading-policy.md
      document-naming-policy.md
      quality-gate-policy.md
      risk-level-rule.md
      forbidden-actions.md

    prompts/
      product-brief-review.md
      proposal-review.md
      prd-review.md
      rfc-review.md
      adr-review.md
      implementation-plan.md
      impact-analysis.md
      code-review.md
      test-generation.md
      release-precheck.md
      incident-analysis.md

    workflows/
      product-brief-to-proposal.md
      proposal-to-prd.md
      prd-to-jira.md
      jira-to-implementation.md
      bugfix-flow.md
      release-flow.md
      incident-flow.md

    agents/
      planner.md
      implementer.md
      reviewer.md
      tester.md
      architect.md
      qa.md
      arbiter.md

    outputs/
      README.md
      impact-analysis/
      review-notes/
      test-suggestions/
      release-checks/
```

### 3.3. Phần không cần trong single repo

Single repo không cần các thành phần chuyên cho multi repo:

```text
docs/workspace/
docs/governance/cross-repo-change-policy.md
.ai/context/workspace-map.md
.ai/context/cross-repo-map.md
.ai/rules/cross-repo-change-rule.md
repo-impact.md
```

Thay vào đó, single repo tập trung vào:

```text
module-map
domain-map
dependency-map
api-map
impact-analysis.md
quality-gates
module-index.md
```

### 3.4. `impact-analysis.md`

Trong single repo, mỗi initiative nên dùng:

```text
docs/initiatives/<initiative>/impact-analysis.md
```

Mục tiêu là xác định ảnh hưởng theo module, domain, layer, data, API, security, testing và release.

Nội dung nên gồm:

```md
# Impact Analysis

## Affected modules

| Module          | Impact | Reason                   | Required reviewer |
| --------------- | ------ | ------------------------ | ----------------- |
| Auth            | high   | Permission policy change | tech-lead         |
| User Management | medium | UI permission display    | tech-lead         |

## Affected layers

- Backend API: yes
- Frontend UI: yes
- Database migration: yes
- Permission/security logic: yes
- Background jobs: no
- Third-party integration: no

## Risk level

High

## Required gates

Áp dụng gate theo `docs/governance/risk-level-policy.md`.
Với high-risk change, dùng danh sách chuẩn trong `docs/governance/risk-level-policy.md` và không hard-code lại danh sách riêng trong `impact-analysis.md`.
```

### 3.5. Cấu trúc tối thiểu cho pilot single repo

Nếu muốn pilot nhẹ, chỉ cần bắt đầu như sau:

```text
repo-root/
  docs/
    initiatives/
      INIT-2026-002-sample/
        README.md
        prd.md
        impact-analysis.md
        test-plan.md

    domains/
      permission/
        README.md
        business-rules.md

    reference/
      architecture/
        system-overview.md
      engineering/
        coding-standard.md
      testing/
        testing-strategy.md
      release/
        release-process.md

    governance/
      document-structure.md
      document-standard.md
      document-naming.md
      quality-gates.md
      risk-level-policy.md
      ai-governance.md
      security-policy.md

    registry/
      initiative-index.md
      module-index.md
      prd-index.md
      rfc-index.md
      adr-index.md
      jira-map.md

  .ai/
    README.md
    context/
      repo-map.md
      module-map.md
      domain-map.md
      initiative-map.md
      coding-conventions.md
    rules/
      ai-usage-policy.md
      context-loading-policy.md
      quality-gate-policy.md
      forbidden-actions.md
    prompts/
      prd-review.md
      implementation-plan.md
      impact-analysis.md
      code-review.md
      test-generation.md
    workflows/
      jira-to-implementation.md
      bugfix-flow.md
      release-flow.md
```

Pilot tree cố ý bỏ một số registry như `domain-index.md` để giảm chi phí khởi tạo. Thêm các registry còn lại khi cần trace domain chính thức hoặc khi automation registry được bật.

---

## 4. Cấu trúc cho multi repo

### 4.1. Khi nào dùng

Dùng cấu trúc multi repo khi:

- Một workspace chứa nhiều repository con.
- Initiative có thể ảnh hưởng nhiều repo.
- Cần quản lý cross-repo dependency, ownership, release flow hoặc version coordination.
- Repo con có build/test/local development riêng.

### 4.2. Nguyên tắc riêng cho multi repo

```text
workspace-root = control plane
repo con       = execution area
.ai/           = AI operating layer
```

Trong đó:

| Khu vực                | Vai trò                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| `workspace-root/docs/` | Tài liệu chính thức cấp workspace, product, governance, domain, release |
| `workspace-root/.ai/`  | Context, prompt, workflow, rule và agent definition cho AI              |
| `<repo>/docs/`         | Tài liệu local của repo con: build, test, module, constraints           |
| `<repo>/source code`   | Execution area nơi thay đổi code thật diễn ra                           |

Nguyên tắc quan trọng:

```text
workspace-root/docs/ là source of truth cấp workspace.
<repo>/docs/ là source of truth cho thông tin local của repo đó.
.ai/ là AI-facing operating layer.
```

Trong multi repo chỉ có một `.ai/` operating layer, đặt ở workspace root. Repo con không tạo `.ai/` riêng; nếu cần rule hoặc context đặc thù cho một repo, vẫn khai báo trong `.ai/` workspace và trỏ tới repo tương ứng.

PRD cấp initiative luôn đặt ở workspace-level. RFC/ADR ảnh hưởng cross-repo, product architecture hoặc quyết định dài hạn cấp hệ thống cũng đặt ở workspace-level.

RFC/ADR thuần repo-local có thể đặt trong `<repo>/docs/` nếu chỉ ảnh hưởng repo đó. Khi quyết định repo-local có ảnh hưởng tới release, dependency, contract hoặc audit trail cấp workspace, repo-level docs phải link về workspace registry hoặc workspace initiative tương ứng.

### 4.3. Cấu trúc chốt

Không cần tạo toàn bộ file ngay từ đầu. Initiative folder nên bắt đầu bằng bộ tối thiểu, sau đó bổ sung tài liệu theo risk, phạm vi và nhu cầu review.

```text
workspace-root/
  docs/
    README.md

    operating-model/          # lớp Operating Model — xem Mục 2.3
    platform/                 # xem Mục 2.3
    handbook/                 # xem Mục 2.3
    playbooks/                # xem Mục 2.3 (hướng dẫn cho người)
    templates/                # xem Mục 2.3
    checklists/               # xem Mục 2.3

    workspace/
      workspace-overview.md
      repo-map.md
      cross-repo-dependencies.md
      ownership.md
      release-flow.md

    initiatives/
      INIT-2026-003-sample/
        README.md
        prd.md
        repo-impact.md
        test-plan.md

        product-brief.md        # optional: khi cần làm rõ product intent
        proposal.md             # optional: khi có nhiều hướng giải quyết cần so sánh
        release-note.md         # optional: khi chuẩn bị release
        decision-log.md         # optional: khi có nhiều quyết định nhỏ

        rfc/                    # optional: khi cần thảo luận technical design
          RFC-2026-001-sample-technical-design.md

        adr/                    # optional: khi có quyết định architecture dài hạn
          ADR-2026-001-sample-architecture-decision.md

    domains/
      permission/
        README.md
        business-rules.md
        architecture.md
        api-contracts.md
        test-notes.md
        decision-index.md

    reference/
      glossary.md
      architecture/
        system-overview.md
        backend-overview.md
        frontend-overview.md
        deployment-overview.md

      engineering/
        coding-standard.md
        api-guidelines.md
        database-migration-guidelines.md
        frontend-state-management.md

      testing/
        testing-strategy.md
        regression-checklist.md
        test-case-standard.md

      release/
        release-process.md
        release-gate.md
        rollback-guide.md

      operations/
        runbook-index.md
        troubleshooting.md
        incident-process.md
        postmortem-template.md

    governance/
      document-structure.md
      document-standard.md
      document-naming.md
      quality-gates.md
      risk-level-policy.md
      ai-governance.md
      security-policy.md
      cross-repo-change-policy.md

    registry/
      initiative-index.md
      domain-index.md
      prd-index.md
      rfc-index.md
      adr-index.md
      jira-map.md
      repo-index.md

  .ai/
    README.md

    context/
      workspace-map.md
      repo-map.md
      cross-repo-map.md
      module-map.md
      domain-map.md
      initiative-map.md
      business-glossary.md
      coding-conventions.md
      testing-context.md
      api-map.md
      dependency-map.md

    rules/
      ai-usage-policy.md
      context-loading-policy.md
      document-naming-policy.md
      quality-gate-policy.md
      risk-level-rule.md
      forbidden-actions.md
      cross-repo-change-rule.md

    prompts/
      product-brief-review.md
      proposal-review.md
      prd-review.md
      rfc-review.md
      adr-review.md
      implementation-plan.md
      cross-repo-impact-analysis.md
      code-review.md
      test-generation.md
      release-precheck.md
      incident-analysis.md

    workflows/
      product-brief-to-proposal.md
      proposal-to-prd.md
      prd-to-jira.md
      jira-to-implementation.md
      cross-repo-impact-analysis.md
      bugfix-flow.md
      release-flow.md
      incident-flow.md

    agents/
      planner.md
      implementer.md
      reviewer.md
      tester.md
      architect.md
      qa.md
      arbiter.md

    outputs/
      README.md
      impact-analysis/
      review-notes/
      test-suggestions/
      release-checks/

  backend/
    docs/
      README.md
      module-overview.md
      local-development.md
      testing.md
      migration-notes.md

  frontend/
    docs/
      README.md
      module-overview.md
      local-development.md
      state-management.md
      testing.md
```

### 4.4. Workspace-level `docs/`

`workspace-root/docs/` là nơi lưu trữ tài liệu chính thức cấp workspace.

Các tài liệu trong `workspace-root/docs/` phục vụ:

- Product team
- Engineering team
- QA/QC
- Tech Lead
- Architect
- DevOps
- Stakeholder
- Người mới onboarding
- Reviewer
- Auditor nếu cần
- AI/agent cần hiểu context trước khi sửa nhiều repo

### 4.5. Repo-level `docs/`

Repo-level docs đặt trong từng repo con:

```text
backend/docs/
frontend/docs/
backend/packages/<package>/docs/
frontend/packages/<package>/docs/
```

Chỉ dùng cho tài liệu local của repo:

```text
Cách build repo
Cách test repo
Module overview local
Local development
Migration note local
State management local
Known constraints
```

Không dùng repo-level docs để lưu Product Brief, Proposal hoặc PRD cấp initiative. RFC/ADR cấp initiative, cross-repo hoặc system-level vẫn thuộc workspace-level. RFC/ADR thuần repo-local có thể nằm trong repo-level docs, nhưng phải link về workspace registry hoặc initiative nếu ảnh hưởng release, dependency, contract hoặc audit trail cấp workspace.

Repo-level docs nên có:

| File                   | Mục đích                                                    |
| ---------------------- | ----------------------------------------------------------- |
| `README.md`            | Tổng quan tài liệu local của repo                           |
| `module-overview.md`   | Module local, folder chính, dependency nội bộ               |
| `local-development.md` | Cách setup, chạy, debug, seed data                          |
| `testing.md`           | Cách chạy test local, test scope, fixture, known flaky test |
| `migration-notes.md`   | Ghi chú migration local cho backend hoặc database           |
| `state-management.md`  | Quy ước state management local cho frontend                 |

### 4.6. `repo-impact.md`

Trong multi repo, mỗi initiative nên dùng:

```text
docs/initiatives/<initiative>/repo-impact.md
```

Mục tiêu là xác định repo nào bị ảnh hưởng, contract nào thay đổi, thứ tự deploy, risk, test và release coordination. `repo-impact.md` cũng phải đủ sâu để reviewer thấy module, layer, data, security và test impact trong từng repo bị ảnh hưởng; nếu chi tiết này đã nằm ở repo-level document khác, `repo-impact.md` phải link trực tiếp tới tài liệu đó.

Nội dung nên gồm:

```md
# Repo Impact

## Affected repos

| Repo     | Impact | Reason                           | Required reviewer |
| -------- | ------ | -------------------------------- | ----------------- |
| backend  | high   | Permission API and policy change | tech-lead         |
| frontend | medium | Permission UI behavior change    | tech-lead         |

## Affected contracts

- REST API: yes
- Event contract: no
- Shared package: yes
- Database schema: yes
- Authentication/authorization model: yes

## Per-repo impact detail

| Repo     | Affected modules/layers                | Data/API/Security impact              | Required local evidence  |
| -------- | -------------------------------------- | ------------------------------------- | ------------------------ |
| backend  | Auth API, permission policy, migration | API and authorization behavior change | backend/docs/testing.md  |
| frontend | Permission UI, route guard             | UI authorization display change       | frontend/docs/testing.md |

## Risk level

High

## Required gates

Áp dụng gate theo `docs/governance/risk-level-policy.md` và `docs/governance/cross-repo-change-policy.md`.
Với high-risk cross-repo change, dùng danh sách chuẩn trong `docs/governance/risk-level-policy.md` và phần bổ sung cross-repo trong `docs/governance/cross-repo-change-policy.md`.
```

### 4.7. Cross-repo change policy

Multi repo cần policy riêng khi thay đổi ảnh hưởng nhiều repo.

Vị trí:

```text
docs/governance/cross-repo-change-policy.md
.ai/rules/cross-repo-change-rule.md
```

Policy này nên quy định:

- Khi nào một thay đổi được xem là cross-repo.
- Repo nào là source of truth cho contract.
- Reviewer bắt buộc theo repo/domain.
- Cách chia PR theo repo.
- Thứ tự merge/deploy.
- Cách rollback khi chỉ một repo lỗi.
- Cách update registry, repo map và cross-repo dependency map.

### 4.8. Cấu trúc tối thiểu cho pilot multi repo

Không cần tạo toàn bộ ngay. Bản pilot nên tạo trước:

```text
workspace-root/
  docs/
    workspace/
      workspace-overview.md
      repo-map.md
      cross-repo-dependencies.md
      ownership.md

    initiatives/
      INIT-2026-004-sample/
        README.md
        prd.md
        repo-impact.md
        test-plan.md

    domains/
      permission/
        README.md
        business-rules.md

    reference/
      architecture/
        system-overview.md
      engineering/
        coding-standard.md
      testing/
        testing-strategy.md

    governance/
      document-structure.md
      document-standard.md
      document-naming.md
      quality-gates.md
      risk-level-policy.md
      ai-governance.md
      security-policy.md
      cross-repo-change-policy.md

    registry/
      initiative-index.md
      repo-index.md
      prd-index.md
      rfc-index.md
      adr-index.md

  .ai/
    README.md
    context/
      workspace-map.md
      repo-map.md
      module-map.md
      domain-map.md
    rules/
      ai-usage-policy.md
      context-loading-policy.md
      quality-gate-policy.md
      forbidden-actions.md
      risk-level-rule.md
      cross-repo-change-rule.md
    prompts/
      prd-review.md
      implementation-plan.md
      cross-repo-impact-analysis.md
      code-review.md
      test-generation.md
    workflows/
      jira-to-implementation.md
      cross-repo-impact-analysis.md
      release-flow.md
```

---

## 5. Vai trò các thư mục chung

### 5.1. `docs/initiatives/`

Chứa tài liệu theo từng initiative, feature lớn, epic hoặc change package.

Vai trò:

- Gom context theo một đơn vị thay đổi có mục tiêu rõ ràng.
- Giúp AI và reviewer hiểu nhanh feature đang làm.
- Lưu trace từ product intent tới requirement, design, implementation, test và release.
- Lưu các RFC/ADR gắn trực tiếp với initiative đó.
- Với single repo: xác định module nào bị ảnh hưởng.
- Với multi repo: xác định repo nào bị ảnh hưởng và reviewer nào bắt buộc.

Các tài liệu nên được tạo theo nhu cầu, không tạo rỗng chỉ để đủ cấu trúc. Nhãn `required` trong bảng dưới đây nghĩa là bắt buộc khi initiative bước vào lifecycle tương ứng, không phải yêu cầu scaffold file ngay khi tạo repository hoặc workspace:

| File                 | Single repo                           | Multi repo                            | Khi nào cần                                                                                                                                                                   |
| -------------------- | ------------------------------------- | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `README.md`          | minimum                               | minimum                               | Luôn cần để tóm tắt initiative, scope, trạng thái, owner và link tới tài liệu con                                                                                             |
| `prd.md`             | required when entering implementation | required when entering implementation | Khi requirement đủ rõ để engineering phân tích, chia task, implement và test                                                                                                  |
| `impact-analysis.md` | required when entering implementation | no                                    | Single repo cần phân tích ảnh hưởng module/layer/data/API/security/test/release trước khi implement                                                                           |
| `repo-impact.md`     | no                                    | required when entering implementation | Multi repo cần phân tích ảnh hưởng repo/contract/version/deploy/test/release trước khi implement, gồm cả module/layer impact theo từng repo hoặc link tới repo-level evidence |
| `test-plan.md`       | required for implementation/release   | required for implementation/release   | Khi initiative đi vào implementation hoặc có regression risk                                                                                                                  |
| `product-brief.md`   | conditional                           | conditional                           | Khi cần làm rõ cơ hội, vấn đề, mục tiêu business, target user, expected outcome                                                                                               |
| `proposal.md`        | conditional                           | conditional                           | Khi có nhiều hướng giải quyết cần so sánh trade-off                                                                                                                           |
| `release-note.md`    | required when entering release        | required when entering release        | Khi chuẩn bị release hoặc có thay đổi user-facing/migration/rollback                                                                                                          |
| `decision-log.md`    | conditional                           | conditional                           | Khi có nhiều quyết định nhỏ không đủ mức tạo ADR                                                                                                                              |
| `rfc/`               | conditional                           | conditional                           | Khi cần thảo luận technical design trước khi chốt                                                                                                                             |
| `adr/`               | conditional                           | conditional                           | Khi có quyết định architecture dài hạn cần ghi nhận                                                                                                                           |

`decision-log.md` là nhật ký quyết định nhỏ trong phạm vi một initiative. `docs/domains/<domain>/decision-index.md` là index dài hạn của domain, dùng để trỏ tới ADR hoặc decision log liên quan.

### 5.2. `docs/domains/`

Chứa tài liệu chính thức theo business domain hoặc bounded context.

Vai trò:

- Lưu business rule sống lâu hơn từng initiative.
- Mô tả kiến trúc domain, API contract, integration point và test note.
- Là nơi cập nhật khi một initiative làm thay đổi rule hoặc behavior dài hạn.
- Giúp team tránh để business rule chỉ tồn tại trong source code, ticket hoặc prompt AI.

Các file trong domain:

| File                | Mục đích                                                                      |
| ------------------- | ----------------------------------------------------------------------------- |
| `README.md`         | Tổng quan domain, owner, repo/module liên quan, link tới initiative liên quan |
| `business-rules.md` | Source of truth cho business logic của domain                                 |
| `architecture.md`   | Kiến trúc domain, component, data flow, dependency quan trọng                 |
| `api-contracts.md`  | API contract, event contract, integration contract liên quan domain           |
| `test-notes.md`     | Test note, edge case, regression scope đặc thù của domain                     |
| `decision-index.md` | Danh sách quyết định quan trọng, link tới ADR hoặc decision-log liên quan     |

### 5.3. `docs/reference/`

Chứa tài liệu nền tảng dùng chung cho toàn repo hoặc workspace.

| Thư mục                   | Mục đích                                                                                                                                        |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `reference/glossary.md`   | Business glossary / terminology dùng chung; là nguồn gốc cho `.ai/context/business-glossary.md`. Tạo theo nhu cầu, không bắt buộc scaffold ngay |
| `reference/architecture/` | System overview, backend overview, frontend overview, deployment                                                                                |
| `reference/engineering/`  | Coding standard, API guideline, database migration, state pattern                                                                               |
| `reference/testing/`      | Testing strategy, regression checklist, test case standard                                                                                      |
| `reference/release/`      | Release process, release gate, rollback guide                                                                                                   |
| `reference/operations/`   | Runbook, troubleshooting, incident process, postmortem                                                                                          |

### 5.4. `docs/governance/`

Chứa các quy định vận hành và chuẩn tài liệu.

| File                          | Mục đích                                                                                  |
| ----------------------------- | ----------------------------------------------------------------------------------------- |
| `document-structure.md`       | Quy định cấu trúc thư mục tài liệu                                                        |
| `document-standard.md`        | Quy định format, metadata, lifecycle của tài liệu                                         |
| `document-naming.md`          | Quy định cách đặt tên PRD, RFC, ADR, Proposal, Product Brief                              |
| `quality-gates.md`            | Quy định các quality gate trong quy trình phát triển                                      |
| `risk-level-policy.md`        | Quy định phân loại rủi ro Low / Medium / High                                             |
| `ai-governance.md`            | Quy định cách dùng AI, trách nhiệm, giới hạn và audit                                     |
| `security-policy.md`          | Quy định xử lý secrets, PII, log, production data, sanitize, secret-scanning và retention |
| `cross-repo-change-policy.md` | Chỉ dùng cho multi repo                                                                   |

### 5.5. `docs/registry/`

Chứa các index và mapping giúp truy vết tài liệu, repo/module, Jira và quyết định.

| File                  | Single repo | Multi repo | Mục đích                                         |
| --------------------- | ----------- | ---------- | ------------------------------------------------ |
| `initiative-index.md` | yes         | yes        | Danh sách initiative, trạng thái, owner          |
| `domain-index.md`     | yes         | yes        | Danh sách domain, owner, tài liệu liên quan      |
| `prd-index.md`        | yes         | yes        | Index PRD                                        |
| `rfc-index.md`        | yes         | yes        | Index RFC                                        |
| `adr-index.md`        | yes         | yes        | Index ADR                                        |
| `jira-map.md`         | yes         | yes        | Mapping Jira với initiative/PRD/module/repo      |
| `module-index.md`     | yes         | optional   | Mapping module, owner, domain                    |
| `repo-index.md`       | no          | yes        | Mapping repo, owner, tech stack, deployment unit |
| `ai-asset-index.md`             | optional | optional | Index prompt/workflow/agent trong `.ai/`                   |
| `playbook-index.md`             | optional | optional | Index playbook (cho người) trong `docs/playbooks/`         |
| `platform-capability-index.md`  | optional | optional | Capability ↔ tool ↔ role ↔ gate                            |
| `policy-to-rule-map.md`         | optional | optional | Map `docs/governance/` ↔ `.ai/rules/`                      |

Registry nên được cập nhật trong cùng PR với tài liệu hoặc code liên quan. Nếu có automation, registry có thể được generate từ metadata của tài liệu.

Quy tắc đồng bộ registry:

- Frontmatter trong tài liệu gốc là source of truth cho `id`, `status`, `owner`, `updated_at`, `initiative`, `affected_domains`, `affected_modules` và `affected_repos`.
- Registry là index tổng hợp để tra cứu nhanh, không được override frontmatter.
- Nếu registry lệch frontmatter, CI hoặc reviewer phải coi registry là stale và yêu cầu cập nhật/generate lại trong cùng PR.
- Nếu registry được generate tự động, không sửa tay registry trừ khi sửa source metadata hoặc script generate.
- Với multi repo, chỉ thêm `module-index.md` khi workspace cần truy vết module xuyên repo hoặc repo con không có module registry local đủ tin cậy.

---

## 6. Vai trò của `.ai/`

`.ai/` là AI Operating Layer.

Nó chứa các file giúp AI/agent làm việc đúng với codebase, quy trình và governance.

`.ai/` phục vụ:

- Claude Code
- Codex
- Gemini
- Antigravity CLI
- Cursor
- Internal AI agent
- CI-based AI reviewer
- AI-assisted testing/release workflow

### 6.1. `.ai/context/`

Chứa context map tối ưu cho AI.

Các file này không thay thế tài liệu chính thức trong `docs/`. Đây là bản tóm tắt, định tuyến hoặc index giúp AI đọc đúng context nhanh hơn.

Mỗi file trong `.ai/context/` phải có frontmatter tối thiểu theo Section 10 (đủ để phát hiện stale) và phần body trỏ về source of truth:

```md
---
id: AI-CTX-<subject>-map
type: ai-context
source_of_truth: false
source_context:
  - docs/domains/<domain>/business-rules.md
  - docs/reference/architecture/system-overview.md
source_updated_at: 2026-07-10
source_revision: commit-sha-or-version-if-available
stale: false
---

## Source of truth

- docs/domains/<domain>/business-rules.md
- docs/reference/architecture/system-overview.md
- docs/initiatives/<initiative>/prd.md

## Purpose

This file is an AI-facing summary.
Do not treat it as the official business rule or architecture decision.
```

### 6.2. `.ai/rules/`

Chứa rule mà AI phải tuân thủ.

| File                        | Mục đích                                                            |
| --------------------------- | ------------------------------------------------------------------- |
| `ai-usage-policy.md`        | Quy định AI được dùng vào việc gì                                   |
| `context-loading-policy.md` | Quy định AI cần đọc context nào trước khi làm task                  |
| `document-naming-policy.md` | Bản AI-facing của quy định đặt tên tài liệu                         |
| `quality-gate-policy.md`    | Rule để AI tự kiểm tra output theo gate                             |
| `risk-level-rule.md`        | Bản AI-facing của risk policy, dùng để AI phân loại rủi ro task     |
| `forbidden-actions.md`      | Những việc AI không được tự ý làm                                   |
| `cross-repo-change-rule.md` | Bản AI-facing của cross-repo change policy, chỉ dùng cho multi repo |

### 6.3. `.ai/prompts/`

Chứa prompt chuẩn cho các giai đoạn phát triển.

Prompt nên được version và review như tài sản chung, tránh mỗi người viết prompt một kiểu.

### 6.4. `.ai/workflows/`

Chứa workflow AI-assisted execution.

Mỗi workflow nên mô tả:

- Input
- Required context
- AI steps
- Human approval point
- Output
- Quality gate
- Risk handling

### 6.5. `.ai/agents/`

Chứa định nghĩa vai trò cho multi-agent workflow.

| Agent       | Vai trò                                                           |
| ----------- | ----------------------------------------------------------------- |
| Planner     | Phân tích requirement, chia task, xác định affected repos/modules |
| Implementer | Đề xuất hoặc thực hiện code change                                |
| Reviewer    | Review code, risk, regression, security                           |
| Tester      | Sinh test case, test matrix, regression checklist                 |
| Architect   | Review design, RFC, ADR                                           |
| QA          | Review acceptance criteria và test coverage                       |
| Arbiter     | Phân xử khi có nhiều hướng hoặc output AI mâu thuẫn               |

### 6.6. `.ai/outputs/`

Chứa output tạm thời hoặc evidence do AI tạo ra.

```text
.ai/outputs/ không mặc định là tài liệu chính thức.
```

Nếu output nào cần trở thành tài liệu chính thức, cần được review và chuyển sang `docs/`.

Về git:

- `.ai/rules/`, `.ai/context/`, `.ai/prompts/`, `.ai/agents/`, `.ai/workflows/` là tài sản chung và nên được commit.
- `.ai/outputs/` là evidence tạm thời nên có chính sách retention rõ ràng. Scratch output có thể gitignore; evidence dùng cho audit/release nên được commit hoặc promote sang `docs/`.

### 6.7. Tool-adapter layer

`.ai/` là operating layer **trung lập với tool**. Mỗi AI tool đọc cấu hình ở vị trí riêng của nó; cần một lớp adapter mỏng trỏ về `.ai/` thay vì lặp lại nội dung.

```text
.ai/          = AI-tool-neutral operating layer (source of truth cho AI asset)
.cursor/      = adapter cho Cursor (rules/)
.claude/      = adapter cho Claude Code (skills/, settings)
CLAUDE.md     = entry point cho Claude Code
AGENTS.md     = entry point cho Codex và agent theo chuẩn AGENTS.md
```

Nguyên tắc:

- Adapter **không** chứa policy hoặc nội dung gốc; chỉ trỏ hoặc được generate từ `.ai/rules`, `.ai/context`, `.ai/prompts`.
- Khi `.ai/` đổi, adapter phải được regenerate hoặc đánh dấu stale. Nếu adapter được generate tự động, không sửa tay; sửa nguồn trong `.ai/` rồi generate lại.
- Adapter đặt ở tầng nơi tool đọc file: project root cho single repo; workspace root và/hoặc repo con cho multi repo tùy tool.
- Nếu adapter lệch `.ai/`, `.ai/` thắng và adapter bị coi là stale (giống quy tắc docs↔.ai tại Mục 14).

---

## 7. Quy tắc đặt tài liệu

### 7.1. Product Brief / Proposal / PRD / RFC / ADR cấp initiative

Tài liệu Product Brief, Proposal, PRD, RFC và ADR cấp initiative đặt theo initiative:

```text
docs/initiatives/<initiative>/
  product-brief.md
  proposal.md
  prd.md
  rfc/
  adr/
```

Lý do:

- Một initiative có thể chứa đầy đủ context từ product tới technical decision.
- AI chỉ cần load một initiative folder là hiểu feature đang làm.
- Review và audit dễ theo dõi theo một change package.

RFC/ADR thuần repo-local trong multi repo tuân thủ quy tắc tại Section 4.2 và Section 4.5.

### 7.2. Business rule lâu dài

Đặt theo domain:

```text
docs/domains/<domain>/business-rules.md
```

Lý do:

- Business rule sống lâu hơn từng initiative.
- Một rule có thể được thay đổi bởi nhiều initiative khác nhau.
- Domain document là nơi ổn định để onboarding, review và audit.

### 7.3. Kiến trúc, coding, testing, release, operations chuẩn

Đặt trong reference:

```text
docs/reference/architecture/
docs/reference/engineering/
docs/reference/testing/
docs/reference/release/
docs/reference/operations/
```

Lý do:

- Đây là tài liệu dùng chung cho toàn repo hoặc toàn workspace.
- Không nên duplicate trong từng initiative hoặc từng domain nếu nội dung áp dụng toàn hệ thống.

### 7.4. Governance

Đặt trong:

```text
docs/governance/
```

### 7.5. AI layer

Đặt trong:

```text
.ai/
```

---

## 8. Quality Gate

Quality gate là bắt buộc trong AI Engineering Operating Model.

AI có thể hỗ trợ nhanh, nhưng các thay đổi quan trọng phải có điểm kiểm soát rõ ràng.

Quality gate tồn tại ở ba lớp:

```text
docs/      = policy chính thức
.ai/       = rule/checklist cho AI
CI/CD      = gate tự động
```

### 8.1. Vị trí lưu quality gate

```text
docs/governance/quality-gates.md
docs/governance/risk-level-policy.md
docs/reference/testing/testing-strategy.md
docs/reference/release/release-gate.md

.ai/rules/quality-gate-policy.md
.ai/rules/risk-level-rule.md
.ai/prompts/release-precheck.md
.ai/prompts/code-review.md
```

Multi repo bổ sung:

```text
docs/governance/cross-repo-change-policy.md
.ai/rules/cross-repo-change-rule.md
```

### 8.2. Gate theo risk level

Không hard-code danh sách gate theo risk level trong tài liệu cấu trúc.

Source of truth:

- `docs/governance/risk-level-policy.md`
- `docs/governance/cross-repo-change-policy.md` với multi repo

Tài liệu này chỉ định nghĩa vị trí lưu và quan hệ giữa policy chính thức, AI-facing rule và CI/CD gate. Các template như `impact-analysis.md` và `repo-impact.md` chỉ được reference policy này, không tự duy trì danh sách gate riêng.

---

## 9. Naming Convention

Section này chỉ mô tả naming tối thiểu để hiểu cấu trúc thư mục. Chi tiết đầy đủ về prefix, numbering, slug, exception, validation và migration rule thuộc `docs/governance/document-naming.md`.

### 9.1. Format tối thiểu

Initiative folder nên dùng format:

```text
INIT-<YEAR>-<TOKEN>-<short-slug>/
```

`<TOKEN>` là 6 chữ cái in hoa ngẫu nhiên `A`–`Z` (ví dụ `KQZTBM`), không phải số thứ tự — để nhiều người/nhiều session tạo initiative song song không trùng ID. Các initiative cũ dạng số (`INIT-2026-001` … `029`) được giữ nguyên. Cách sinh token và quy tắc đầy đủ: `docs/governance/document-naming.md` Section 2.

RFC/ADR trong initiative folder nên dùng tên có prefix vì một initiative có thể có nhiều RFC/ADR:

```text
rfc/RFC-<YEAR>-<TOKEN>[x]-<short-slug>.md
adr/ADR-<YEAR>-<TOKEN>[x]-<short-slug>.md
```

Ví dụ:

```text
INIT-2026-KQZTBM-user-permission-rework/
rfc/RFC-2026-KQZTBM-permission-model.md
adr/ADR-2026-KQZTBM-use-policy-based-permission.md
adr/ADR-2026-KQZTBMb-cache-permission-matrix.md
```

### 9.2. Tên file ổn định trong initiative

Trong initiative folder, các tài liệu chính có thể dùng tên ổn định để AI và con người dễ tìm:

```text
product-brief.md
proposal.md
prd.md
impact-analysis.md
repo-impact.md
test-plan.md
release-note.md
decision-log.md
```

Không cần tạo thư mục `rfc/` hoặc `adr/` nếu initiative chưa có RFC/ADR.

### 9.3. Singleton và ID ngắn

Governance doc là singleton, nên dùng tên file mô tả:

```text
document-structure.md
document-standard.md
document-naming.md
quality-gates.md
risk-level-policy.md
ai-governance.md
cross-repo-change-policy.md
```

ID cho singleton, domain document và repo-level document có thể dùng format ngắn nếu `document-naming.md` cho phép:

```text
<PREFIX>-<slug>
```

Ví dụ:

```text
GOV-document-structure
DOMAIN-permission-business-rules
REPO-backend-local-development
```

Quy tắc đầy đủ cho prefix, slug, reserved names và exception thuộc `docs/governance/document-naming.md`.

---

## 10. Metadata chuẩn cho tài liệu

Section này chỉ mô tả metadata tối thiểu để cấu trúc tài liệu có thể vận hành. Chi tiết đầy đủ về required/optional matrix, conditional fields, enum, validation và lifecycle thuộc `docs/governance/document-standard.md`.

Frontmatter metadata là bắt buộc cho:

- Tài liệu chính thức trong `docs/`.
- Repo-level docs được commit trong `<repo>/docs/`.
- File shared trong `.ai/context/`, `.ai/rules/`, `.ai/prompts/`, `.ai/workflows/` và `.ai/agents/`.
- File trong `.ai/outputs/` nếu được dùng làm audit evidence hoặc release evidence.

Frontmatter là optional với scratch output trong `.ai/outputs/` nếu output đó không được commit hoặc không dùng làm evidence.

### 10.1. Field tối thiểu cần nhận diện

Các field sau là nhóm tối thiểu mà tài liệu cấu trúc cần biết để routing, traceability và AI lookup hoạt động:

```text
id
title
canonical_path
type
purpose
status
owner
created_at
updated_at
approved_by
accepted_at
scope
source_of_truth
source_of_truth_for
proposed_source_of_truth_for
ai_usage
freshness
initiative
jira_epic
related_product_brief
related_proposal
related_prd
related_rfc
related_adr
related_initiatives
target_release
decision_required
decision_date
domain
repo
risk_level
affected_domains
affected_modules
affected_repos
source_policy
source_context
source_updated_at
source_revision
stale
last_evaluated_at
evaluation_dataset
success_rate
```

Ý nghĩa, required/optional status, enum hợp lệ và validation rule của từng field thuộc `docs/governance/document-standard.md`.

Quan hệ giữa tài liệu dùng flat fields như `initiative`, `jira_epic`, `related_prd`, `related_rfc`. Không dùng nested `links:` trong frontmatter chuẩn, trừ khi `document-standard.md` định nghĩa một schema mới và migration rule rõ ràng.

`source_of_truth: true` chỉ dùng khi tài liệu đã `accepted` và authoritative cho subject tương ứng. Tài liệu `draft`, `proposed`, summary/index hoặc AI-facing derivative phải dùng `source_of_truth: false`.

Với AI-facing derivative trong `.ai/context/`, `.ai/rules/`, `.ai/prompts/`, `.ai/workflows/` và `.ai/agents/`, metadata phải đủ để reviewer hoặc CI phát hiện stale:

```yaml
source_policy: docs/governance/risk-level-policy.md
source_context:
  - docs/reference/testing/testing-strategy.md
source_updated_at: 2026-07-10
source_revision: commit-sha-or-version-if-available
stale: false
```

Nếu source document thay đổi sau `source_updated_at` hoặc khác `source_revision`, file AI-facing liên quan phải được review lại hoặc đánh dấu `stale: true`.

### 10.2. Ví dụ metadata tối thiểu

```yaml
id: PRD-2026-001
title: User Permission Rework
canonical_path: docs/initiatives/INIT-2026-001-user-permission-rework/prd.md
type: prd
purpose: implementation
status: draft
owner: product-team
created_at: 2026-07-09
updated_at: 2026-07-10
scope: initiative
freshness:
  review_cycle: quarterly
  last_reviewed_at:
source_of_truth: false
ai_usage: allowed
initiative: INIT-2026-001
jira_epic: AUTH-120
```

### 10.3. Ví dụ AI-facing rule

```yaml
id: AI-RULE-risk-level-policy
title: AI Risk Level Policy
type: ai-rule
purpose: review
status: accepted
owner: ai-platform-owner
created_at: 2026-07-09
updated_at: 2026-07-10
scope: ai
source_of_truth: false
source_policy: docs/governance/risk-level-policy.md
source_updated_at: 2026-07-10
source_revision: commit-sha-or-version-if-available
stale: false
ai_usage: allowed
freshness:
  review_cycle: quarterly
  last_reviewed_at: 2026-07-10
```

File AI-facing không phải authoritative policy trừ khi được promote rõ ràng vào `docs/`. Các file này phải trỏ tới `source_policy` hoặc `source_context` khi tóm tắt, định tuyến hoặc operationalize tài liệu chính thức, đồng thời ghi `source_updated_at` hoặc `source_revision` để kiểm tra stale.

### 10.4. Metadata evaluation cho AI asset

Các field ở Mục 10.1 theo dõi **source drift** (`source_updated_at`, `source_revision`, `stale`) nhưng không theo dõi **chất lượng** của prompt/workflow/agent. Với `.ai/prompts/`, `.ai/workflows/`, `.ai/agents/` và playbook được operationalize cho AI, bổ sung nhóm field evaluation:

```yaml
version:
status:                 # theo document-standard.md; AI asset có thể thêm trạng thái `pilot`
owner:
last_evaluated_at:
evaluation_dataset:     # link tới representative eval set
success_rate:
related_playbook:
related_policy:
```

Lý do: prompt/workflow có thể đổi hành vi khi model hoặc tool thay đổi. Không có eval set và bản ghi version, "model mới hơn" không bảo đảm phù hợp hơn với use case cụ thể. Đây là **AI-asset lifecycle** song song với document lifecycle (Mục 11), nhưng đo bằng **evaluation** thay vì review cycle. Enum status hợp lệ là source of truth tại `docs/governance/document-standard.md`; ý nghĩa `pilot` khớp với giai đoạn thử nghiệm trong Handbook.

---

## 11. Document Lifecycle

Section này chỉ mô tả lifecycle tối thiểu để hiểu trạng thái tài liệu trong cấu trúc thư mục. Chi tiết đầy đủ về status enum, transition rule, approval rule, deprecation và supersede thuộc `docs/governance/document-standard.md`.

Mỗi tài liệu nên có trạng thái rõ ràng.

### 11.1. Status đề xuất

Danh sách dưới đây là enum tham chiếu tối thiểu cho tài liệu này. Source of truth cho enum hợp lệ là `docs/governance/document-standard.md`.

```text
draft
proposed
accepted
rejected
deprecated
superseded
```

| Status       | Ý nghĩa                            |
| ------------ | ---------------------------------- |
| `draft`      | Đang soạn                          |
| `proposed`   | Đã đề xuất, đang chờ duyệt         |
| `accepted`   | Đã được chấp nhận                  |
| `rejected`   | Không được chấp nhận               |
| `deprecated` | Không còn khuyến nghị sử dụng      |
| `superseded` | Đã được thay thế bởi tài liệu khác |

Tri thức chưa `accepted` không được dùng như nguồn sự thật nếu chưa có human approval.

### 11.2. Quy tắc superseded

Nếu tài liệu bị thay thế, không xóa ngay. Cập nhật metadata:

```yaml
status: superseded
superseded_by: ADR-2026-009
```

### 11.3. Quy tắc cập nhật domain document

Khi một initiative thay đổi business rule, architecture, API contract hoặc test behavior dài hạn của domain:

- Cập nhật tài liệu trong `docs/domains/<domain>/`.
- Ghi link initiative liên quan trong metadata hoặc phần history.
- Cập nhật `decision-index.md` nếu có quyết định dài hạn.
- Cập nhật registry tương ứng nếu có thay đổi index.

### 11.4. Quy tắc cập nhật repo-level document

Chỉ áp dụng cho multi repo.

Khi một initiative làm thay đổi cách build, test, migration, local development hoặc module overview của repo:

- Cập nhật `<repo>/docs/` tương ứng.
- Ghi rõ thay đổi đó local cho repo nào.
- Không chuyển requirement cấp product hoặc decision cấp initiative/cross-repo/system-level xuống repo-level docs.

---

## 12. Traceability

Traceability giúp trả lời:

- Requirement này đến từ đâu?
- Jira nào implement requirement này?
- Repo/module nào bị ảnh hưởng?
- Domain nào bị thay đổi?
- RFC/ADR nào liên quan?
- Test nào cover requirement này?
- Release nào đưa thay đổi này ra production?

### 12.1. Traceability trong initiative

Mỗi initiative nên có trace rõ:

```text
Product Brief
  -> Proposal
  -> PRD
  -> RFC
  -> ADR
  -> Impact Analysis (impact-analysis.md hoặc repo-impact.md)
  -> Jira
  -> Pull Request
  -> Test Plan
  -> Release Note
```

Multi repo nên trace thêm:

```text
repo-impact.md
  -> Pull Request per repo
  -> Release Coordination
```

### 12.2. Traceability qua metadata

Mọi tài liệu quan trọng nên liên kết với nhau qua metadata:

```yaml
initiative: INIT-2026-001
related_product_brief: PBR-2026-001
related_proposal: PROP-2026-001
related_prd: PRD-2026-001
related_rfc: RFC-2026-001
related_adr: ADR-2026-001
jira_epic: AUTH-120
affected_domains:
  - permission
affected_modules:
  - backend:Auth
affected_repos:
  - backend
```

`affected_repos` chỉ bắt buộc với multi repo.

### 12.3. Traceability qua registry

Registry không thay thế metadata trong từng tài liệu. Registry là lớp tổng hợp để con người và AI tra cứu nhanh.

---

## 13. Ownership

### 13.1. Ownership cho `docs/`

| Loại tài liệu     | Owner chính                               |
| ----------------- | ----------------------------------------- |
| Workspace docs    | Engineering Platform Owner / Architect    |
| Initiative README | Product / Engineering Manager             |
| Product Brief     | Product / PO / BA                         |
| Proposal          | Product / Tech Lead / Engineering Manager |
| PRD               | Product / PO / BA                         |
| RFC               | Tech Lead / Architect                     |
| ADR               | Architect / Tech Lead                     |
| Business rules    | PO / BA + Tech Lead                       |
| Domain docs       | Domain Owner / Tech Lead                  |
| Testing docs      | QA / QC                                   |
| Release docs      | DevOps / Tech Lead                        |
| Operations docs   | DevOps / SRE / Tech Lead                  |
| Architecture docs | Architect / Senior Developer              |
| Governance docs   | Engineering Platform Owner                |
| Registry          | Engineering Platform Owner / Tech Lead    |

`Workspace docs` chỉ áp dụng cho multi repo.

### 13.2. Ownership cho repo-level `docs/`

Chỉ áp dụng cho multi repo.

| Loại tài liệu          | Owner chính                |
| ---------------------- | -------------------------- |
| Repo README            | Tech Lead                  |
| Module overview        | Tech Lead / Senior Dev     |
| Local development      | Tech Lead                  |
| Testing local          | Tech Lead + QA             |
| Migration notes        | Tech Lead                  |
| State management local | Tech Lead                  |
| Product package notes  | Product module owner       |

### 13.3. Ownership cho `.ai/`

| Loại file         | Owner chính                     |
| ----------------- | ------------------------------- |
| AI rules          | AI Platform Owner / Tech Lead   |
| Context map       | Tech Lead / AI Champion         |
| Prompt library    | AI Platform Owner / AI Champion |
| Agent definitions | AI Platform Owner               |
| Workflows         | Tech Lead + QA + DevOps         |
| Generated outputs | Người chạy task hoặc automation |

---

## 14. Quy tắc tránh duplicate

### 14.1. Single repo

```text
docs/        = nguồn chính thức.
.ai/context/ = bản tóm tắt tối ưu cho AI.
```

### 14.2. Multi repo

```text
workspace-root/docs/ = nguồn chính thức cấp workspace
<repo>/docs/         = nguồn chính thức cho thông tin local của repo
.ai/context/         = bản tóm tắt tối ưu cho AI
```

Quy tắc:

- Không để business rule chỉ tồn tại trong `.ai/`.
- `.ai/context/business-glossary.md` chỉ là bản tóm tắt AI-facing; terminology gốc phải nằm trong `docs/reference/glossary.md`.
- Không để architecture decision chỉ tồn tại trong prompt.
- Không duplicate toàn bộ nội dung dài từ `docs/` sang `.ai/context/`.
- `.ai/context/` nên tóm tắt, gắn link source of truth và nêu khi nào cần đọc tài liệu gốc.
- Khi tài liệu chính thức thay đổi, file liên quan trong `.ai/context/`, `.ai/rules/`, `.ai/prompts/`, `.ai/workflows/` và `.ai/agents/` phải được cập nhật hoặc đánh dấu stale.
- `.ai/rules/` chỉ được chứa bản AI-facing của policy. Nếu khác với `docs/governance/`, `docs/governance/` thắng và `.ai/rules/` bị coi là stale.
- `.ai/prompts/`, `.ai/workflows/` và `.ai/agents/` phải trỏ tới source policy/context tương ứng và ghi `source_updated_at` hoặc `source_revision` để reviewer biết prompt/workflow đang dựa trên phiên bản nào.
- AI không được enforce rule từ `.ai/` nếu file đó bị đánh dấu stale hoặc source policy liên quan đã thay đổi nhưng chưa được review lại.
- Nếu `docs/` và `.ai/` có file cùng tên như `repo-map.md`, bản trong `docs/` hoặc `docs/workspace/` là tài liệu gốc; bản trong `.ai/context/` chỉ là summary/index cho AI.
- Tooling và reviewer phải map quan hệ docs↔.ai bằng frontmatter `source_policy` hoặc `source_context`, không map bằng tên file. Tên trùng chỉ là tiện lợi cho người đọc, không phải khóa liên kết.
- Bản `.ai/` phản chiếu một tài liệu gốc phải phân biệt được với bản gốc để tránh nhầm khi grep. Pattern đặt tên cụ thể (ví dụ hậu tố `-context-map.md`) thuộc `docs/governance/document-naming.md`; tài liệu này chỉ quy định nguyên tắc phân biệt.
- Với multi repo, không đặt PRD hoặc RFC/ADR cấp initiative, cross-repo hoặc system-level trong repo con.
- Với multi repo, RFC/ADR thuần repo-local được phép ở repo-level docs nếu tuân thủ quy tắc tại Section 4.2 và 4.5.
- Với multi repo, repo-level docs chỉ ghi thông tin local của repo.

---

## 15. Security Rules

Tài liệu này chỉ nêu bright-line và vị trí lưu security policy, không hard-code chi tiết. Source of truth chi tiết cho phân loại dữ liệu nhạy cảm, sanitize, approval, secret-scanning và retention là `docs/governance/security-policy.md`.

Bright-line không đổi:

- Không commit secrets hoặc credential vào `docs/`, repo-level docs hoặc `.ai/` (production secrets, API token, password, private key, credential nội bộ, third-party access token).
- Customer PII, raw production log chứa dữ liệu nhạy cảm và dữ liệu thật từ production/third-party chỉ được đưa vào tài liệu hoặc prompt AI sau khi sanitize và có approval theo `docs/governance/security-policy.md`.
- AI-generated output trong `.ai/outputs/` tuân thủ cùng quy tắc. Scratch output bị gitignore vẫn phải được secret-scan và có retention rule theo `security-policy.md`, không được coi là vùng miễn kiểm tra.

Chi tiết phân loại dữ liệu, quy trình sanitize, role được phép approve, secret-scanning trong CI và retention thuộc `docs/governance/security-policy.md`. Các template như `impact-analysis.md`, `repo-impact.md` và prompt trong `.ai/` chỉ reference policy này, không tự duy trì danh sách riêng.

---

## 16. Quy tắc AI đọc context

Section này chỉ mô tả context-loading tối thiểu để hiểu cách AI dùng cấu trúc thư mục. Các danh sách dưới đây là minh hoạ, không phải policy chi tiết. Source of truth cho AI context-loading là `docs/governance/ai-governance.md`; bản AI-facing operationalize rule đó là `.ai/rules/context-loading-policy.md`. Khi hai nơi lệch nhau, `docs/governance/ai-governance.md` thắng và `.ai/rules/context-loading-policy.md` bị coi là stale.

File AI-facing:

```text
.ai/rules/context-loading-policy.md
```

Nội dung nên quy định theo risk, loại task và repo/module bị ảnh hưởng, không bắt mọi task đọc toàn bộ tài liệu.

### 16.1. Context tối thiểu cho mọi task

Single repo:

```text
1. .ai/context/repo-map.md
2. .ai/context/module-map.md nếu task liên quan code/module
3. .ai/context/coding-conventions.md nếu task có sửa code
4. .ai/rules/forbidden-actions.md nếu task có thao tác file, code, dữ liệu hoặc release
```

Multi repo:

```text
1. .ai/context/workspace-map.md
2. .ai/context/repo-map.md
3. .ai/context/coding-conventions.md nếu task có sửa code
4. .ai/rules/forbidden-actions.md nếu task có thao tác file, code, dữ liệu hoặc release
```

### 16.2. Context cho feature hoặc initiative task

Single repo:

```text
1. Related initiative under docs/initiatives/
2. Related domain under docs/domains/
3. Relevant reference docs
4. Relevant governance rules
5. Relevant AI rules
```

Multi repo:

```text
1. Related initiative under docs/initiatives/
2. Related domain under docs/domains/
3. .ai/context/cross-repo-map.md nếu nhiều repo bị ảnh hưởng
4. Relevant repo-level docs under affected repos
5. Relevant reference docs
6. Relevant governance rules
7. Relevant AI rules
```

### 16.3. Context cho high-risk task

Single repo:

```text
1. docs/governance/quality-gates.md
2. docs/governance/risk-level-policy.md
3. docs/reference/testing/testing-strategy.md
4. docs/reference/release/release-gate.md
5. initiative impact-analysis.md
6. related domain business-rules.md
7. related RFC/ADR nếu có
```

Multi repo:

```text
1. docs/governance/quality-gates.md
2. docs/governance/risk-level-policy.md
3. docs/governance/cross-repo-change-policy.md
4. docs/workspace/cross-repo-dependencies.md
5. docs/workspace/release-flow.md
6. docs/reference/testing/testing-strategy.md
7. docs/reference/release/release-gate.md
8. initiative repo-impact.md
9. related domain business-rules.md
10. related RFC/ADR nếu có
11. affected repo-level docs
```

### 16.4. Context cho vận hành hoặc sự cố

```text
1. docs/reference/operations/runbook-index.md
2. docs/reference/operations/troubleshooting.md
3. docs/reference/operations/incident-process.md
4. related release note hoặc deployment overview
5. related domain/module/repo docs
6. .ai/rules/forbidden-actions.md
```

---

## 17. Quyết định áp dụng

### 17.1. Chọn single repo nếu

- Dự án có một repo chính.
- Không cần workspace-level control plane.
- Impact chủ yếu là module/domain/layer.
- Release và rollback diễn ra trong cùng repo.

AI cần hiểu:

```text
Đang làm initiative nào
Liên quan domain nào
Ảnh hưởng module nào
Risk level là gì
Quality gate nào phải qua
Test/release impact ra sao
```

### 17.2. Chọn multi repo nếu

- Workspace chứa nhiều repo con.
- Initiative có thể ảnh hưởng nhiều repo.
- Có cross-repo dependency, shared contract hoặc release coordination.
- Repo con có owner, build/test/deploy riêng.

AI cần hiểu:

```text
Đang làm initiative nào
Liên quan domain nào
Ảnh hưởng repo nào
Ảnh hưởng module nào
Cross-repo dependency là gì
Risk level là gì
Quality gate nào phải qua
Test/release impact ra sao
```

Nguyên tắc quan trọng nhất:

```text
Không để AI thay thế source of truth.
Hãy để AI đọc source of truth, tạo output có evidence, và đi qua quality gate phù hợp.
```
