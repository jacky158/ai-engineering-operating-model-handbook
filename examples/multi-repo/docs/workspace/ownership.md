---
id: docs-workspace-ownership
title: ownership
status: draft
owner: engineering-platform
source_of_truth: false
ai_usage: allowed
---

# ownership

## Repo và branch

Mỗi repo trong workspace là một git repository độc lập. Xác định repo sở hữu file trước khi commit; không stage thay
đổi của repo con qua repo cha. Danh sách repo, remote và branch: `../registry/repo-index.md`.

## Role holders

Tài liệu ghi role, không ghi người (`owner:`, reviewer bắt buộc). Bảng này là **nơi duy nhất** ánh xạ role → người;
khi đổi người chỉ sửa ở đây. Ghi handle của hệ thống quản lý source, không ghi email.

| Role | Holder |
| ---- | ------ |
| `engineering-platform` | `<handle>` |
| `tech-lead` | `<handle>` hoặc "any team member" |
| `mobile-lead` | `<handle>` |
| `architect`, `product-team`, `domain-owner`, `devops`, `qa`, `ai-platform-owner` | `<handle>` hoặc "not assigned" |

- Role chưa có người giữ phải ghi rõ "not assigned" thay vì bỏ trống: gate cần role đó hiện chưa thể đạt.
- Nếu một role được giữ bởi "any team member", gate cần role đó được thoả bởi review của bất kỳ thành viên nào. Cần
  quyết định riêng việc tác giả có được tự review thay đổi của mình hay không.
- Người approve dữ liệu PII/production: xem `../governance/security-policy.md`.
