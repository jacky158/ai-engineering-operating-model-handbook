---
id: docs-operating-model-process-ai-assisted-sdlc
title: AI-assisted SDLC
type: operating-model
status: draft
owner: engineering-leadership
source_of_truth: false
scope: global
ai_usage: allowed
source_context:
  - docs/operating-model/principles.md
  - docs/governance/quality-gates.md
  - docs/governance/risk-level-policy.md
---

# AI-assisted SDLC

Mô tả **vòng đời phát triển có AI tham gia** ở mức Operating Model (thành phần Process): mỗi giai đoạn AI hỗ trợ
gì, con người giữ trách nhiệm gì, source of truth nào, gate và evidence nào. Đây là *cách làm* chung; các bước
chi tiết nằm ở `../../playbooks/`, bản AI ở `../../../.ai/`.

## Nguyên tắc xuyên suốt
- **Outcome before output**: đánh giá kết quả, không chỉ lượng nội dung AI tạo.
- **Source of truth first**: AI đọc `docs/`, không coi chat history/summary là nguồn.
- **Human accountability**: AI hỗ trợ, không nhận accountability; high-risk cần human approval + segregation of duties.
- **Evidence over confidence**: mỗi bước để lại evidence kiểm chứng được.
- **Small & reviewable**: chia nhỏ để dễ hiểu và kiểm chứng.

## Các giai đoạn

| Giai đoạn | AI hỗ trợ (agent/prompt) | Con người giữ | Source of truth | Gate | Artifact |
| --- | --- | --- | --- | --- | --- |
| Requirement | prd-review · Planner | Chốt requirement, làm rõ assumption | `prd.md`, domain `business-rules.md` | Requirement clarity | review note, `prd.md` |
| Design (RFC/ADR) | rfc/adr-review · Architect | Quyết định architecture, ghi ADR | `reference/architecture/`, domain `architecture.md` | Design approval (high-risk) | RFC/ADR |
| Planning & Impact | Planner · cross-repo-impact-analysis | Chốt scope, ưu tiên | `cross-repo-dependencies.md` | Implementation readiness | `repo-impact.md` |
| Implementation | Implementer · implementation-plan | Ownership code, giữ scope | `coding-standard.md`, `api-contracts.md` | Code review gate | diff/PR + validation evidence |
| Test | Tester · test-generation | Kiểm chứng oracle, kết luận pass/fail | acceptance criteria, `test-notes.md` | Test readiness | `test-plan.md` + result |
| Review | Reviewer · code-review | Approve, chịu accountability merge | `security-policy.md`, `risk-level-policy.md` | Review gate | review findings |
| Release | release-precheck · release-flow | Go/no-go, deploy order | `release-flow.md`, `release-gate.md` | Release readiness | release checklist |
| Operations/Incident | incident-analysis · incident-flow | Điều phối incident, quyết định | `operations/`, `security-policy.md` | — | postmortem |

Playbook (người) tương ứng ở `../../playbooks/`; workflow/prompt (AI) ở `../../../.ai/`. Liên kết bằng
frontmatter, không copy (Mục 2.4).

## Handoff giữa các giai đoạn
Mỗi handoff phải mang theo **source, assumption và evidence**. Không chuyển AI summary thay source; không để
assumption ẩn đi tiếp xuống giai đoạn sau.

## Vì sao nhiều lớp review vẫn bỏ sót (Handbook Ch 13)
Các role **không độc lập** nếu dùng chung một context thiếu — code và test do cùng AI sinh từ cùng assumption
có thể cùng sai. Vì vậy control phải xuất hiện ở nhiều điểm:
- Clarification **trước** implementation.
- Domain rule làm source of truth.
- **Test oracle độc lập** với implementation.
- Review có requirement + impact context.
- Evidence trace từ acceptance → test → release.

## Đặc thù multi repo
- Impact xuyên repo qua `repo-impact.md`; contract có repo source-of-truth (`cross-repo-change-policy.md`).
- Release cần **thứ tự deploy** và rollback per repo.
- Chỉ một `.ai/` ở workspace root điều phối agent cho mọi repo.

## Liên quan
`../principles.md`, `handoff-and-review.md`, `escalation.md`,
`../../governance/quality-gates.md`, `../../playbooks/`, `../../../.ai/agents/`.
