---
id: AI-rules-context-loading-policy
title: context-loading-policy
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

# context-loading-policy

> AI-facing scaffold (multi-repo). Tóm tắt/định tuyến; trỏ về source of truth trong `docs/`, KHÔNG override.

## Step 0 — active initiative (trước mọi việc khác)

Không bắt đầu làm việc khi người dùng chưa chọn active initiative (`docs/governance/ai-governance.md` Mục 7).

1. Request không nêu initiative → **hỏi trước**. Liệt kê ứng viên từ `docs/registry/initiative-index.md` và thêm lựa
   chọn "new initiative". Trước khi có câu trả lời: chỉ đọc registry đó, không thay đổi gì.
2. Không suy ra từ branch, commit, đường dẫn, memory hay session trước. Có thể đặt dự đoán lên đầu danh sách.
3. "No initiative" chỉ hợp lệ khi người dùng nói rõ **và** việc đó không tạo commit. Không đề xuất làm mặc định.
   Mọi thay đổi governance, template, registry, `.ai/rules/`, `.ai/context/` hoặc adapter cần một initiative.
4. Sau khi chọn: nêu `Active initiative: INIT-…` và nạp folder của initiative (`README.md`, `prd.md`, `repo-impact.md`).
5. Request sau đó nằm ngoài initiative → dừng và hỏi có chuyển không.
6. Ghi ID initiative vào tên branch, commit subject, tiêu đề PR và evidence trong `.ai/outputs/`.

<!-- TODO: context tối thiểu theo task type và risk. -->
