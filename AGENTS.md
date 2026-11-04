# Hướng dẫn cho AI làm việc trong repo

Phạm vi: toàn bộ repo `capcut-cli`. Giao tiếp với người dùng hiện tại bằng tiếng Việt. Đọc tài liệu theo tác vụ; không cần nạp toàn bộ source/draft JSON vào ngữ cảnh.

## Bắt đầu từ đâu

| Công việc | Đọc trước |
|---|---|
| Dựng/chỉnh video, chọn source, bố cục, âm thanh | [Kinh nghiệm dựng video](docs/video-editing-playbook.vi.md), rồi [skill capcut-edit](skills/capcut-edit/SKILL.md) |
| Tiếp tục các video Phú Xuyên | [Nhật ký và bàn giao Phú Xuyên](docs/case-studies/phu-xuyen-2026-11.md) |
| Tìm module để sửa CLI/thư viện | [Bản đồ repo](docs/repository-map.md) |
| Tìm lệnh/flag đúng | `node dist/index.js describe --compact`, sau đó `describe --command <name>`; [command reference](docs/command-reference.md) |
| Draft không mở, sửa không hiện, thiếu media | [Store/version](docs/version-support.md), [pitfalls](skills/capcut-edit/references/pitfalls.md), `diagnose` |
| Đọc cấu trúc draft | [Draft schema](docs/draft-schema/README.md) |
| Ví dụ/quy trình sẵn có | [Examples](examples/README.md), [workflows](skills/capcut-edit/references/workflows.md) |
| Sửa mã nguồn/đóng gói | [CONTRIBUTING](CONTRIBUTING.md), [package.json](package.json), [CI](.github/workflows/ci.yml) |
| Commit/push, chọn file đưa lên GitHub | [Phạm vi đồng bộ GitHub](docs/github-publishing.md), [.gitignore](.gitignore) |

## Khi dựng video cho người dùng này

- Lưu project, media phụ thuộc, bản xem thử và ghi chú ở thư mục bền vững trong thư mục công việc; với Phú Xuyên là `Phú Xuyên/CapCut_Edit`. Không bàn giao draft phụ thuộc `%TEMP%`.
- Bàn giao project chỉnh sửa được và làm nó xuất hiện trên trang chủ CapCut khi tác vụ yêu cầu. Giữ hình, lời thoại, nhạc, SFX, chữ và logo trên các track phù hợp để sửa tiếp.
- Dùng video mẫu để hiểu nhịp kể, điểm gây cười, kiểu chữ và âm nhạc; chọn source theo nội dung/hành động phù hợp. Đọc playbook trước khi áp một preset.
- Rà kỹ đầu/cuối **từng đoạn source được chọn**, kể cả câu thừa nằm sát điểm nối: đếm nhịp, hướng dẫn diễn, câu chào ngoài cảnh, âm tiết còn sót. Giữ đủ lời thoại và phản ứng có chủ đích.
- Sở thích đã xác nhận ở Phú Xuyên: sáng hơn một chút, logo góc trên trái, chữ hạ thấp vừa đủ; chuyển cảnh ngắn ở điểm nối và SFX cho chữ khi có ích. Đây là mặc định cho ca tương tự; yêu cầu mới của người dùng được ưu tiên.
- Người dùng đã tự xuất được video trong CapCut. Phân biệt MP4 xem thử với bản xuất cuối; ghi rõ nếu renderer chỉ mô phỏng hiệu ứng native.

## Khi ghi project thật

1. Kiểm tra `info`, `diagnose`, track/media và phiên bản ứng dụng. Dùng `doctor` khi cần tìm FFmpeg/Whisper.
2. Đóng project trong CapCut trước khi ghi; khi sửa chỉ mục trang chủ, thoát ứng dụng trước. Không dùng `--force-write` để vượt xung đột chưa xử lý.
3. Dùng `loadDraft`/`saveDraft` qua [public library](src/lib.ts) để giữ cơ chế đồng bộ, kiểm tra xung đột và backup. Không sửa mỗi root JSON rồi mặc định active timeline đã đổi.
4. `activeTimeline: true` chỉ dùng sau khi xác minh cấu trúc `Timelines/project.json` và pointer hợp lệ; đừng bật cho mọi folder.
5. Tạo mới từ skeleton của app đang cài khi cần tương thích; không chép timeline/nội dung của donor vào project mới. Donor cụ thể của Phú Xuyên nằm trong nhật ký ca dựng.
6. Quy trình có nhiều lệnh, tính toán hoặc rẽ nhánh phải thành script tham số hóa theo skill. Kiểm tra script cũ có khôi phục backup/đăng ký lại trước khi chạy.
7. Thời gian draft tính bằng microsecond; tính cut bằng frame nguyên của FPS timeline, rồi đổi start/end sang microsecond. `source_duration = target_duration × speed`; audio có `clip: null`.
8. Cẩn thận lỗi alias đường dẫn Windows khi đăng ký: `C:/...` và `C:\...` có thể thành hai mục trang chủ. Đối chiếu ID + đường dẫn chuẩn hóa trước khi đăng ký lại. Xem [ca Phú Xuyên](docs/case-studies/phu-xuyen-2026-11.md) và [factory.ts](src/factory.ts).
9. Không coi JSON hợp lệ là bằng chứng hiệu ứng hiện trong app. Kiểm tra frame, các điểm nối, âm thanh và project native; ghi rõ kiểm tra nào đã làm.
10. Sau chỉnh trực tiếp trong CapCut, xác định draft đang dùng là bản mới nhất rồi đồng bộ lại bản bàn giao. Không chạy lại spec/backup cũ lên bản đã được người dùng chỉnh.

## Khi sửa repo

- Node >=18; mã nguồn TypeScript ở `src/`, `dist/` là build sinh ra. Sửa source rồi build, không vá riêng `dist/`.
- CLI dùng Node built-ins, không thêm runtime dependency nếu chưa có lý do phù hợp nguyên tắc repo.
- Import API từ `dist/lib.js` hoặc package; `src/index.ts`/`dist/index.js` chạy CLI khi import. API nội bộ như factory/decorators cần kiểm tra lại chữ ký khi đổi phiên bản.
- Nguồn sự thật cho lệnh là command contracts và implementation hiện tại. Một số phần prose cũ chưa theo kịp tính năng mới (ví dụ `serve`, transition); đừng suy luận tính năng chỉ từ ghi chú cũ.
- Chạy kiểm tra tương ứng với thay đổi: `npm run build`, `npm run lint`, test tính năng liên quan; sửa chức năng cần test có ý nghĩa. `npm test` build rồi chạy toàn bộ suite. `test:fast` chỉ dùng khi `dist/` đã mới.
- Test cần môi trường editor đã đóng. Trên Windows, wrapper shell cần Git Bash thật trên PATH; alias `WindowsApps/bash.exe` có thể tồn tại nhưng không chạy được các test. Chỉnh PATH cho tiến trình kiểm thử, không cần đổi thiết lập toàn máy.
- Chỉ sửa tài liệu: kiểm tra link, đường dẫn, độ đúng nội dung; không cần render lại video hoặc chạy toàn bộ test mã nguồn.
- Bản ban đầu là thư mục giải nén; ngày 2026-11-04 người dùng yêu cầu đưa lên `https://github.com/piuplatform-hub/Piu-capcut-cli`, nhánh `main`. Kiểm tra `git status` và remote trước mỗi lần đồng bộ; không force-push hoặc ghi đè lịch sử có sẵn.

## Ghi nhớ sau mỗi lần dựng

Người dùng muốn kinh nghiệm được tích lũy qua các lần làm. Sau feedback hoặc phát hiện có giá trị:

1. Thêm/cập nhật nhật ký dưới `docs/case-studies/`: ngày, bối cảnh, feedback, thay đổi, bằng chứng kiểm tra, đường dẫn sản phẩm và giới hạn.
2. Chỉ đưa bài học có thể tái sử dụng vào [playbook](docs/video-editing-playbook.vi.md); tách yêu cầu đã xác nhận, thông số thử nghiệm và giả thuyết.
3. Giữ lịch sử trước/sau và lý do khi thay khuyến nghị. Tránh thêm quy tắc trùng lặp hoặc biến một ca dựng thành chuẩn cho mọi video.
4. Thêm link từ playbook hoặc [mục lục docs](docs/README.md) để AI phiên sau tìm được. Cập nhật bản đồ repo nếu cấu trúc thay đổi.

Các file này là bộ nhớ đọc/ghi của quy trình, không tự huấn luyện mô hình. AI phiên sau cần đọc và cập nhật chúng để kinh nghiệm tiếp tục có tác dụng.
