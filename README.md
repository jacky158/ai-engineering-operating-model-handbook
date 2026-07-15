# AI Engineering Operating Model

Bộ tài liệu và scaffold tham khảo giúp engineering team áp dụng AI vào vòng đời phát triển phần mềm (SDLC) một cách nhất quán, có kiểm soát và có thể kiểm chứng.

Repository tập trung vào ba lớp nội dung:

- **Handbook — Why / What:** giải thích bối cảnh, khái niệm, nguyên tắc và trách nhiệm.
- **Playbook — When / How:** hướng dẫn workflow, use case, validation, evidence và escalation.
- **Governance & document structure:** xác định source of truth, cấu trúc tài liệu, metadata, quality gate và cách cung cấp context cho AI.

> Các tài liệu chính hiện chủ yếu ở trạng thái `draft` hoặc `proposed`, phù hợp cho review và pilot. Nội dung chưa mặc nhiên là policy bắt buộc của tổ chức.

## Bắt đầu nhanh

Chọn lộ trình phù hợp với nhu cầu:

| Nhu cầu | Tài liệu nên đọc |
| --- | --- |
| Hiểu tổng quan và vocabulary chung | [Handbook V1](./handbook-v1.md) |
| Áp dụng AI vào công việc hằng ngày | [Playbook V1](./playbook-v1.md) |
| Thiết kế `docs/`, `.ai/` cho single-repo hoặc multi-repo | [Document Structure](./aiom-document-structure.md) |
| Xem một workspace multi-repo hoàn chỉnh | [Multi-repo scaffold](./examples/multi-repo/README.md) |
| Review mục tiêu và phạm vi toàn bộ tài liệu | [Documentation Specification](./documentation-specification.md) |

Lộ trình khuyến nghị cho người mới:

1. Đọc **Handbook V1** để hiểu Operating Model và các nguyên tắc nền tảng.
2. Chọn một use case nhỏ trong **Playbook V1** để pilot.
3. Dùng **Document Structure** để xác định source of truth và context AI cần đọc.
4. Tham khảo **Multi-repo scaffold** khi triển khai cấu trúc vào dự án thực tế.

## Nguyên tắc cốt lõi

```text
docs/ là source of truth cho người và tổ chức.
.ai/ là AI-facing operating layer dùng để tóm tắt và định tuyến context.
```

`.ai/` không thay thế hoặc override `docs/`. Output do AI tạo ra vẫn cần human ownership, validation và quality gate tương ứng với mức độ rủi ro.

Mô hình tài liệu tách rõ:

```text
Operating Model layer  -> cách team làm việc với AI
Delivery layer         -> initiative, domain và reference của dự án
Execution area         -> source code, test và thay đổi thực tế
```

## Cấu trúc repository

```text
.
├── README.md
├── documentation-specification.md   # specification tổng thể
├── handbook-specification.md        # yêu cầu nội dung Handbook
├── handbook-v1.md                   # bản Handbook dùng để review/pilot
├── playbook-specification.md        # yêu cầu nội dung Playbook
├── playbook-v1.md                   # bản Playbook dùng để review/pilot
├── aiom-document-structure.md        # topology và governance tài liệu
├── examples/
│   └── multi-repo/                  # scaffold workspace multi-repo
└── assets/                           # hình minh hoạ
```

## Quan hệ giữa các tài liệu

| Tài liệu | Vai trò | Trạng thái hiện tại |
| --- | --- | --- |
| `documentation-specification.md` | Vision và phạm vi của bộ tài liệu | `draft` |
| `handbook-specification.md` | Tiêu chí và cấu trúc bắt buộc của Handbook | `accepted` |
| `handbook-v1.md` | Nội dung nền tảng Why / What | `proposed` |
| `playbook-specification.md` | Tiêu chí và cấu trúc bắt buộc của Playbook | `draft` |
| `playbook-v1.md` | Hướng dẫn thực hành When / How | `proposed` |
| `aiom-document-structure.md` | Chuẩn đề xuất cho cấu trúc và lifecycle tài liệu | `proposed` |

Frontmatter ở đầu mỗi tài liệu cung cấp metadata như `status`, `owner`, `version`, `scope` và `source_of_truth`. Hãy kiểm tra metadata này trước khi dùng một tài liệu làm căn cứ quyết định.

## Ví dụ multi-repo

[`examples/multi-repo`](./examples/multi-repo/README.md) minh hoạ mô hình **Hybrid + `.ai` Operating Layer**, bao gồm:

- `docs/` cho Operating Model và delivery source of truth;
- `.ai/context`, `.ai/rules`, `.ai/prompts` và `.ai/workflows` cho AI;
- adapter cho agent/tool qua `AGENTS.md`, `CLAUDE.md`, `.cursor/` và `.claude/`;
- tài liệu cục bộ của các repo `backend` và `frontend`;
- template, checklist, registry và một initiative mẫu có traceability.

Scaffold này dùng để tham khảo và pilot. Khi áp dụng vào dự án thật, chỉ tạo artifact có nhu cầu rõ ràng; không tạo file rỗng chỉ để khớp cấu trúc.

## Trạng thái và đóng góp

Repository đang trong giai đoạn xây dựng và review. Khi đề xuất thay đổi:

1. Xác định tài liệu canonical và tránh lặp lại nội dung ở nhiều nơi.
2. Cập nhật frontmatter, liên kết và các AI-facing derivative liên quan.
3. Nêu rõ thay đổi ảnh hưởng tới Handbook, Playbook, governance hay scaffold.
4. Kiểm tra các liên kết Markdown và tính nhất quán của thuật ngữ trước khi merge.
