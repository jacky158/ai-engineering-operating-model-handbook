# Multi-repo scaffold (AIOM)

Scaffold minh hoạ cấu trúc tài liệu cho **trường hợp multi-repo** theo
[`aiom-document-structure.md`](../../aiom-document-structure.md):

- **Mục 4.3** — cấu trúc chốt multi-repo (workspace + delivery + repo con)
- **Mục 2.3** — lớp Operating Model trong `docs/`
- **Mục 6.7** — tool-adapter layer (`.cursor/`, `.claude/`, `CLAUDE.md`, `AGENTS.md`)

## Ba tầng trong scaffold này

```text
workspace-root/            # control plane (thư mục này)
  docs/                    # source of truth cho người
    operating-model/  platform/  handbook/  playbooks/  templates/  checklists/   ← lớp Operating Model (cách làm)
    workspace/  initiatives/  domains/  reference/  governance/  registry/         ← lớp Delivery (đang làm gì)
  .ai/                     # AI operating layer (tóm tắt/định tuyến, không override docs/)
  .cursor/  .claude/  CLAUDE.md  AGENTS.md    # adapter cho từng tool
  backend/  frontend/      # execution area — repo con, chỉ giữ docs/ local
```

## Lưu ý

- Đây là **scaffold placeholder**: mỗi file có frontmatter tối thiểu + một dòng mục đích + `TODO`.
  Trong dự án thật, áp dụng nguyên tắc *"không tạo file rỗng chỉ để thỏa cấu trúc"* (Mục 3.2, 5.1) —
  chỉ tạo tài liệu khi initiative bước vào lifecycle tương ứng.
- File trong `.ai/` là AI-facing derivative: phải trỏ `source_context`/`source_policy` về `docs/`
  và ghi `source_updated_at`/`source_revision` để phát hiện stale (Mục 10, 14).
- Chỉ có **một** `.ai/` ở workspace root; repo con (`backend/`, `frontend/`) không tạo `.ai/` riêng (Mục 4.2).
- Muốn bản nhẹ để bắt đầu? Xem cấu trúc pilot tối thiểu ở **Mục 4.8**.

## File đã có nội dung mẫu (không phải placeholder)

- `docs/playbooks/impact-analysis.md` — khung playbook chuẩn cho người
- `docs/templates/prd-template.md` — template PRD
- `CLAUDE.md`, `AGENTS.md` — adapter entry point
