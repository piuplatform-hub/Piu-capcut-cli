# Phạm vi đồng bộ GitHub

Repo đích: [piuplatform-hub/Piu-capcut-cli](https://github.com/piuplatform-hub/Piu-capcut-cli), nhánh `main`. Khởi tạo theo yêu cầu người dùng ngày 2026-11-04, từ bản capcut-cli 0.31.1 đang dùng để dựng video.

## Giữ trong Git

- Mã TypeScript `src/`, package manifest/lockfile và cấu hình build/lint.
- Test và fixture JSON nhẹ, templates, examples, scripts, skill dựng video.
- `AGENTS.md`, playbook, nhật ký bài học, bản đồ repo và tài liệu upstream.
- Python client, mã nguồn Wasm, CI và các license/notice gốc.

`src/` là mã chương trình cần giữ. “Source” video/footage của các ca dựng là dữ liệu công việc, để ngoài Git.

## Giữ trên máy dựng

- `node_modules/`, `dist/`, virtualenv, cache, logs và backup.
- Video/audio nguồn, nhạc/SFX, MP4 xem thử và bản xuất cuối, project CapCut chứa media.
- Model/weights Whisper và model khác, archive tải về, thông tin đăng nhập/`.env`.
- `media/` minh họa của upstream; README vẫn có thể tham chiếu ảnh/video từ upstream mà không mang file vào repo này.

Quy tắc nằm trong [.gitignore](../.gitignore). Không ignore toàn bộ `*.json` hoặc `*.tmp`: các file như `template-2.tmp` trong fixture là dữ liệu kiểm thử cần thiết. Khi cần fixture audio/video mới, ưu tiên sinh file nhỏ trong test hoặc bổ sung ngoại lệ có chủ đích.

Không track workflow `release.yml` xuất bản package npm của upstream, workflow auto-merge dùng cấu hình tài khoản upstream và `FUNDING.yml` của upstream. Các file gốc vẫn giữ trên máy; nếu cần phát hành Piu phải cấu hình riêng trước. CI kiểm thử vẫn được giữ.

## Khi clone và dùng tiếp

```bash
npm ci
npm run build
node dist/index.js describe --compact
```

Tự cài FFmpeg/Whisper và đặt media trong thư mục công việc. Đường dẫn ổ D:/C: trong [ca Phú Xuyên](case-studies/phu-xuyen-2026-11.md) mô tả máy dựng gốc, không phải file được upload hay tài nguyên có sẵn sau clone.

## Trước mỗi lần push

Xem diff và danh sách staged, đối chiếu các file lớn/secret/artifact, giữ license và kiểm tra liên quan đến thay đổi. Chạy `git check-ignore` để xác minh quy tắc khi thêm loại dữ liệu mới. Không đưa token vào remote URL, script hoặc tài liệu.

Push bình thường lên nhánh đúng; không force-push. Sau push đối chiếu commit local/remote và kiểm tra trạng thái CI. Cập nhật [AGENTS.md](../AGENTS.md) và nhật ký nếu phát hiện bài học mới.

## Xác minh trước lần đồng bộ đầu tiên

2026-11-04, Windows/Node 26.13.0: build và lint thành công; Node test suite 1.292 pass, 40 skip theo điều kiện môi trường, 0 fail; Python client 19 pass. Test chạy khi CapCut đã đóng và dùng Git Bash thật trên PATH. Lượt rà staged kiểm tra file lớn/artifact, mẫu token/private key và liên kết trong tài liệu mới; không phát hiện vấn đề trong phạm vi kiểm tra. Khoảng 4 MiB mã/tài liệu được chọn; video, dependencies và build output giữ trên máy.
