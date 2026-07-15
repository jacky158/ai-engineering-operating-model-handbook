# CLAUDE.md — Claude Code entry point

Adapter mỏng cho Claude Code. **Không** chứa policy gốc; trỏ về `.ai/` (source of truth cho AI asset).
Nếu file này lệch `.ai/`, `.ai/` thắng và adapter bị coi là stale (Mục 6.7, 14).

## Trước khi làm bất kỳ task nào

Đọc context tối thiểu cho multi repo (Mục 16.1):

1. `.ai/context/workspace-map.md`
2. `.ai/context/repo-map.md`
3. `.ai/context/coding-conventions.md` — nếu task sửa code
4. `.ai/rules/forbidden-actions.md` — nếu task thao tác file, code, dữ liệu hoặc release

## Rule bắt buộc

- Tuân thủ `.ai/rules/ai-usage-policy.md`, `.ai/rules/context-loading-policy.md`,
  `.ai/rules/quality-gate-policy.md`, `.ai/rules/cross-repo-change-rule.md`.
- `docs/` là source of truth. Không coi tóm tắt trong `.ai/` là nguồn sự thật.
- Không tự mở rộng scope; không commit secret/PII (xem `docs/governance/security-policy.md`).

## Prompt & workflow

Prompt chuẩn ở `.ai/prompts/`, workflow ở `.ai/workflows/`. Playbook cho người ở `docs/playbooks/`.
