---
id: docs-operating-model-people-roles-and-responsibilities
title: roles-and-responsibilities
status: draft
owner: engineering-platform
source_of_truth: false
ai_usage: allowed
---

# roles-and-responsibilities

Hai nhóm role tồn tại song song: role của người sở hữu tài liệu và quyết định, và role của AI agent tham gia SDLC
dưới sự giám sát của con người.

## Role của người

| Role | Sở hữu |
| ---- | ------ |
| `engineering-platform` | Workspace docs, governance, registry, phần lớn operating-model docs |
| `tech-lead` | RFC, ADR, business rule (cùng PO/BA), architecture docs (cùng architect); chủ các repo backend và frontend, tài liệu repo-level của chúng, và là reviewer bắt buộc cho thay đổi ở đó |
| `product-team` / PO / BA | Product brief, proposal, PRD, business rule |
| `architect` | RFC, ADR, architecture docs, workspace overview |
| `mobile-lead` | Ảnh hưởng mobile của một initiative: mobile API và mobile client; reviewer bắt buộc cho thay đổi chạm vào đó |
| `domain-owner` | Nội dung `docs/domains/<domain>/` |
| `devops` | Release docs, `docs/workspace/release-flow.md`, operations docs |
| `ai-platform-owner` | `.ai/rules/`, `.ai/prompts/`, `.ai/agents/` |
| `qa` (QA / QC) | Testing docs |

- Không định nghĩa role riêng `backend-lead`, `frontend-lead` hay "repo owner"; trách nhiệm đó thuộc `tech-lead`.
- Tài liệu chỉ ghi **role**. Ai giữ role nào tra ở `../../workspace/ownership.md` — nơi duy nhất ánh xạ role → người.
- `approved_by` của tài liệu `accepted` vẫn ghi người cụ thể (xem `../../governance/document-standard.md`).

## Role của AI agent (`.ai/agents/`)

| Agent | Trách nhiệm |
| ----- | ----------- |
| Planner | Biến request/PRD/bug/incident thành scope, repo/module bị ảnh hưởng và risk; viết `repo-impact.md` hoặc implementation plan. Không sửa code, không commit. |
| Implementer | Đề xuất hoặc thực hiện thay đổi code theo plan của Planner. |
| Reviewer | Review code về correctness, risk, regression, security. |
| Tester | Sinh test case, test matrix, regression checklist. |
| Architect | Review design, RFC, ADR. |
| QA | Review acceptance criteria và test coverage. |
| Arbiter | Phân xử khi output hoặc hướng đi của AI mâu thuẫn — xem `../process/escalation.md`. |

## Ranh giới

Role của người luôn giữ các điểm approval trong `../../governance/ai-governance.md`: promote AI output vào `docs/`,
chấp nhận quyết định, merge, release và mọi thứ chạm production hoặc PII. Không agent role nào được tự vượt ranh giới đó.
