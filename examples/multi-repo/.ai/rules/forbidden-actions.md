---
id: AI-rules-forbidden-actions
title: forbidden-actions
type: ai-asset
status: draft
owner: ai-platform-owner
source_of_truth: false
source_context:
  - docs/governance/ai-governance.md
source_updated_at: 2026-11-23
source_revision:
stale: false
---

# forbidden-actions

> AI-facing scaffold (multi-repo). Tóm tắt/định tuyến; trỏ về source of truth trong `docs/`, KHÔNG override.

## Session scope

- **Không bắt đầu làm việc khi chưa có active initiative do người dùng chọn.** Không sửa file, không chạy lệnh đổi
  trạng thái, không draft, không khảo sát cho task. Hỏi; không tự suy ra. Xem `context-loading-policy.md` Step 0.
- **Không sửa governance dưới "no initiative".** "No initiative" chỉ dành cho việc không tạo commit.
- **Không âm thầm làm việc xuyên initiative.** Request nằm ngoài active initiative → dừng và hỏi có chuyển không.

## Đặt tên

- **Không cấp ID initiative theo số thứ tự.** Dùng token ngẫu nhiên theo `document-naming-policy.md`.

<!-- TODO: các nhóm còn lại (git/repo boundary, dữ liệu, release). -->
