# Bản đồ repo capcut-cli

Rà soát ngày 2026-11-04, package 0.31.1. Đã liệt kê cây mã nguồn, test/fixture, tài liệu, skill, examples, scripts, cấu hình và các package phụ; đọc các entry point và luồng liên quan. Đây là bản đồ điều hướng, không phải khẳng định mọi nhánh mã đã được audit.

## Điểm vào và luồng chính

```text
CLI: src/index.ts → command-specs + module chức năng
Thư viện: src/lib.ts → loadDraft / saveDraft / lintDraft / runCommand
Draft: store.ts (phát hiện/chọn timeline) → draft.ts (đọc/ghi)
       → atomic-write + journal/history + version/write checks
Tạo project: compile.ts → factory.ts + decorators.ts → draft/store
Xem thử: render.ts → probe/FFmpeg
```

`index.ts` tự chạy CLI khi import; dùng `lib.ts` cho thư viện. `lib.ts` là tập public exports hẹp hơn toàn bộ module nội bộ. Build TypeScript sinh `dist/`; các lệnh tại máy này chạy bằng `node dist/index.js`.

## Mã nguồn theo việc cần làm

| Việc | File chính |
|---|---|
| Lệnh, parsing, dispatch và command contracts | [index.ts](../src/index.ts), [command-specs.ts](../src/command-specs.ts), [runner.ts](../src/runner.ts) |
| Kiểu draft, tìm segment/material, đọc/ghi | [draft.ts](../src/draft.ts), [segment-lookup.ts](../src/segment-lookup.ts), [lib.ts](../src/lib.ts) |
| Canonical file, active timeline, mirror và editor checks | [store.ts](../src/store.ts), [version.ts](../src/version.ts), [app-versions.ts](../src/app-versions.ts) |
| Ghi atomic, backup/khôi phục, BOM | [atomic-write.ts](../src/atomic-write.ts), [history-integrity.ts](../src/history-integrity.ts), [journal-digest.ts](../src/journal-digest.ts), [bom.ts](../src/bom.ts) |
| Compile spec, tạo/trim/duplicate, register/rename, asset copy | [compile.ts](../src/compile.ts), [factory.ts](../src/factory.ts) |
| Material liên kết, đổi/relink source | [materials-register.ts](../src/materials-register.ts), [relink.ts](../src/relink.ts), [replace.ts](../src/replace.ts) |
| Keyframe, transition, mask, text styling/animation | [decorators.ts](../src/decorators.ts), [mask-fields.ts](../src/mask-fields.ts), [preset.ts](../src/preset.ts) |
| Enum, catalogue, effect slug | [enums.ts](../src/enums.ts), [enums.json](../src/enums.json), [user-enums.ts](../src/user-enums.ts), [catalogue.ts](../src/catalogue.ts) |
| Timing/FPS và kiểm tra timeline | [time.ts](../src/time.ts), [lint.ts](../src/lint.ts) |
| Caption, ASR và đồng bộ | [caption.ts](../src/caption.ts), [whisper.ts](../src/whisper.ts), [capcut-cloud-asr.ts](../src/capcut-cloud-asr.ts), [align.ts](../src/align.ts) |
| SRT/ASS, offset style, phân nhóm/ngôn ngữ chữ | [srt.ts](../src/srt.ts), [ass.ts](../src/ass.ts), [text-offsets.ts](../src/text-offsets.ts), [script.ts](../src/script.ts) |
| Dịch, TTS, từ điển phát âm | [translate.ts](../src/translate.ts), [tts.ts](../src/tts.ts), [lexicon.ts](../src/lexicon.ts) |
| FFmpeg/probe/render, loudness và SFX | [probe.ts](../src/probe.ts), [render.ts](../src/render.ts), [ffmpeg-pass.ts](../src/ffmpeg-pass.ts), [loudness.ts](../src/loudness.ts), [sfx.ts](../src/sfx.ts) |
| Tìm khoảng lặng, cảnh, lần diễn lại | [silence.ts](../src/silence.ts), [scenes.ts](../src/scenes.ts), [retakes.ts](../src/retakes.ts) |
| Chroma, matting | [chroma.ts](../src/chroma.ts), [matting.ts](../src/matting.ts) |
| Import/export timeline và batch export | [interchange.ts](../src/interchange.ts), [export-batch.ts](../src/export-batch.ts) |
| Chẩn đoán môi trường, fixture, migration/encryption | [doctor.ts](../src/doctor.ts), [fixture.ts](../src/fixture.ts), [migrate.ts](../src/migrate.ts), [decrypt.ts](../src/decrypt.ts) |
| Job server, quickstart, tìm media Wikimedia | [serve.ts](../src/serve.ts), [quickstart.ts](../src/quickstart.ts), [wikimedia.ts](../src/wikimedia.ts) |

Lỗi project hiện trùng ở home: bắt đầu từ `factory.ts` (`registerDraftInIndex`, `planDraftRegistration`), đối chiếu các phép so sánh `draft_fold_path` với đường dẫn app đã lưu. Kinh nghiệm xử lý trên máy người dùng nằm trong [ca Phú Xuyên](case-studies/phu-xuyen-2026-11.md); đây chưa phải bản sửa source CLI.

## Thư mục hỗ trợ và tài liệu

| Đường dẫn | Nội dung |
|---|---|
| [README](../README.md), [docs](README.md) | Tổng quan, cài/chạy và mục lục |
| [command-reference.md](command-reference.md), [JSON contract](command-reference.json) | Tài liệu lệnh sinh bằng [generate-command-docs.mjs](../scripts/generate-command-docs.mjs); không sửa tay file sinh |
| [draft-schema](draft-schema/README.md) | Tracks/segments, materials, keyframes, effects và khác biệt phiên bản |
| [version-support](version-support.md), [encryption](jianying-encryption.md) | Mức bằng chứng tương thích và hạn chế format |
| [skills/capcut-edit](../skills/capcut-edit/SKILL.md) | Workflow, pitfalls, API reference, shell wrappers và assets mẫu |
| [examples](../examples/README.md) | Dựng từ đầu, caption, narration, keyframe, reusable title, automation |
| [templates](../templates) | Text template và skeleton `_init`; skeleton cũ không mặc định phù hợp app mới |
| [test](../test), [helpers](../test/helpers), [fixtures](../test/fixtures) | Node test suite, helper CLI/draft, fixture thật và tổng hợp |
| [python](../python/README.md) | Python client gọi CLI; tests ở `python/tests` |
| [wasm/capcut-core](../wasm/capcut-core/README.md) | Component cô lập để inspection; build/test/parity và MCP verification riêng |
| [scripts](../scripts) | Generate docs/enums và smoke-test package |
| [.github/workflows](../.github/workflows), [.husky/pre-commit](../.husky/pre-commit) | CI, release và kiểm tra trước commit |
| [.claude-plugin](../.claude-plugin), [hooks](../hooks/hooks.json) | Plugin manifest và SessionStart hook cài CLI; không chạy hook chỉ để đọc repo |
| `media/`, `dist/`, `node_modules/` (chỉ trên máy, không track) | Media minh họa, build output và dependencies; build/cài lại khi clone |
| [CONTRIBUTING](../CONTRIBUTING.md), [CHANGELOG](../CHANGELOG.md), [PLAN](../PLAN.md) | Nguyên tắc đóng góp, lịch sử và kế hoạch; prose cũ có thể khác implementation hiện tại |

Phạm vi bản Piu đưa lên GitHub và các cấu hình upstream được loại riêng ghi tại [github-publishing.md](github-publishing.md).

## Chọn kiểm tra theo phạm vi

- Mã TypeScript: `npm run build`, `npm run lint`, test liên quan dưới `test/`; `npm test` chạy build và toàn suite.
- Ví dụ test riêng sau build: `node --test test/register.test.mjs test/frame-grid.test.mjs`. Chọn tên test đúng tính năng sửa, không mặc định chỉ chạy hai file này.
- Shell wrappers: xem `_test.sh` trong skill; chạy trong môi trường có shell tương ứng.
- Trên Windows, đóng CapCut trước test và kiểm tra `bash` là Git Bash hoạt động được, không phải alias WindowsApps chưa có runtime. Có thể thêm `C:\Program Files\Git\bin` vào PATH riêng của tiến trình test.
- Python client: `python -m unittest discover -s python/tests -v`.
- Wasm: `npm run wasm:verify`; xem package con cho MCP verification/dependencies cần thiết.
- Đóng gói: `npm run smoke:package -- <tarball.tgz>` sau build/pack, theo CI.
- Tài liệu: kiểm tra links, đường dẫn và ví dụ lệnh; không cần chạy cả suite khi chỉ đổi Markdown.

Trên PowerShell, dùng `rg --files --hidden` khi cần thấy cấu hình ẩn và loại `node_modules`, `.git`, `dist` khỏi lượt tìm source. Tìm trong thư mục bằng `rg ... docs/draft-schema -g '*.md'` thay vì dựa vào shell mở rộng glob kiểu Unix.
