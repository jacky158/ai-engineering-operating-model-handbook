---
id: docs-playbooks-requirement-review
title: Playbook — Requirement Review
type: playbook
status: draft
owner: TODO
source_of_truth: false
ai_usage: allowed
related_policy: docs/governance/quality-gates.md
related_ai_prompt: .ai/prompts/prd-review.md
---

# Playbook — Requirement Review

> Hướng dẫn cho **con người**. Bản AI: `.ai/prompts/prd-review.md` (liên kết bằng frontmatter, không copy — Mục 2.4).

## Purpose
Làm rõ requirement và assumption **trước khi implement**, để không lan lỗi xuống code/test/review (Handbook Ch 13).

## When to use
Khi PRD/requirement sẵn sàng cho engineering phân tích, trước khi chia task và code.

## Roles
- Responsible: Developer / Tech Lead phân tích
- Accountable: Product Owner (nội dung requirement), Tech Lead (tính khả thi)
- Consulted: Domain Owner, QC
- Informed: Team Lead

## Inputs
- `docs/initiatives/<init>/prd.md`, `product-brief.md`/`proposal.md` (nếu có)
- `docs/domains/<domain>/business-rules.md`

## Required context
Related initiative + domain (Mục 16.2); không dùng chat history làm nguồn.

## Steps
1. Đọc requirement từ source of truth, không từ tóm tắt AI.
2. Liệt kê acceptance criteria; kiểm tra từng cái **testable**.
3. Truy tìm **assumption ẩn** và edge case chưa định nghĩa (ví dụ user thuộc nhiều đơn vị).
4. Đối chiếu domain rule; ghi mâu thuẫn giữa requirement và rule hiện tại.
5. Ghi **open questions** và gán người trả lời.
6. Kết luận: requirement sẵn sàng implement hay cần clarification.

## Outputs
Ghi chú review đính vào initiative (open questions + assumption đã chốt); cập nhật `prd.md` nếu cần.

## Quality gates
Requirement-clarity gate theo `docs/governance/quality-gates.md`. Không tự chế danh sách gate ở đây.

## Evidence
Danh sách assumption đã xác nhận + ai xác nhận + open questions đã đóng.

## Stop conditions
Dừng nếu acceptance criteria không testable, hoặc requirement mâu thuẫn domain rule chưa được giải quyết.

## Escalation
Mâu thuẫn requirement/scope → Product Owner; ảnh hưởng architecture/cross-repo → Tech Lead / Architecture Owner
(theo `docs/operating-model/people/roles-and-responsibilities.md`).
