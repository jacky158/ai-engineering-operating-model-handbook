# AGENTS.md — entry point cho Codex và agent theo chuẩn AGENTS.md

Adapter mỏng, tool-neutral. Nguồn gốc rule/context là `.ai/`; file này chỉ định tuyến (Mục 6.7).

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
