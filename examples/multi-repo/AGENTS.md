# AGENTS.md — entry point cho Codex và agent theo chuẩn AGENTS.md

Adapter mỏng, tool-neutral. Nguồn gốc rule/context là `.ai/`; file này chỉ định tuyến (Mục 6.7).

## Active initiative — bắt buộc trước mọi việc

Mỗi session gắn với **một initiative do người dùng chọn** (`docs/governance/ai-governance.md` Mục 7;
`.ai/rules/context-loading-policy.md` Step 0).

- Request không nêu initiative → hỏi trước, liệt kê từ `docs/registry/initiative-index.md` và thêm "new initiative".
  Trước khi có câu trả lời chỉ đọc registry đó.
- Không suy ra từ branch, commit, đường dẫn, memory hay session trước.
- "No initiative" chỉ hợp lệ khi người dùng nói rõ và việc đó không tạo commit. Thay đổi governance cần initiative.
- Sau khi chọn: nêu `Active initiative: INIT-…`; ID đó đi vào branch, commit subject, tiêu đề PR và evidence.

## Context tối thiểu (multi repo — Mục 16.1)

1. `.ai/context/workspace-map.md`
2. `.ai/context/repo-map.md`
3. `.ai/context/coding-conventions.md` — nếu sửa code
4. `.ai/rules/forbidden-actions.md` — nếu thao tác file/code/dữ liệu/release

## Nguyên tắc

- `docs/` = source of truth; `.ai/` = summary/routing, không override.
- Cross-repo change: tuân thủ `.ai/rules/cross-repo-change-rule.md` và
  `docs/governance/cross-repo-change-policy.md`.
- Output đi qua quality gate phù hợp risk; tạo evidence, không thay human approval.

## Tài sản

- Rules: `.ai/rules/`  ·  Context: `.ai/context/`  ·  Prompts: `.ai/prompts/`
- Workflows: `.ai/workflows/`  ·  Agent roles: `.ai/agents/`  ·  Playbook (người): `docs/playbooks/`
