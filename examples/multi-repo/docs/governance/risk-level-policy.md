---
id: docs-governance-risk-level-policy
title: Risk Level Policy
type: governance
purpose: policy
status: draft
owner: engineering-leadership
source_of_truth: false
scope: global
ai_usage: allowed
---

# Risk Level Policy

Source of truth cho **phân loại risk** và gate tối thiểu theo risk. Là nơi duy nhất định nghĩa ngưỡng;
`impact-analysis.md`/`repo-impact.md` chỉ tham chiếu, không hard-code lại.

## 1. Trục đánh giá risk (Handbook Ch 11.2)
- Blast radius (số user/module/repo ảnh hưởng).
- Độ khó rollback.
- Chạm security / privacy / production data.
- Thay đổi public contract hoặc architecture dài hạn.
- Độ khó thu thập evidence.

## 2. Phân loại
| Level | Đặc điểm (TODO chốt ngưỡng) | Gate tối thiểu |
| --- | --- | --- |
| Low | Dễ rollback, blast radius nhỏ, không chạm security | TODO |
| Medium | Ảnh hưởng nhiều module/consumer, rollback trung bình | TODO |
| High | Khó rollback, chạm security/data/public contract/migration | TODO — bắt buộc human approval, segregation of duties |

<!-- TODO: định nghĩa ngưỡng định lượng cho từng trục; cần owner phê duyệt. -->

## 3. Gate mapping
Liên kết mỗi risk level tới gate cụ thể trong `quality-gates.md`. Multi repo bổ sung theo `cross-repo-change-policy.md`.

## 4. AI-facing
Bản operationalize cho AI: `.ai/rules/risk-level-rule.md` (phải trỏ về file này, ghi `source_updated_at`).

## Liên quan
`quality-gates.md`, `security-policy.md`, `cross-repo-change-policy.md`.
