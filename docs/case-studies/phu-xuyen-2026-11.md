# Phú Xuyên — kinh nghiệm và bàn giao, 2026-11-04

Trạng thái: người dùng đã chấp nhận các bản dựng; tự xuất bản cuối trong CapCut. Tài liệu lưu kinh nghiệm của phiên làm việc, không tự chạy lại pipeline hay sửa sản phẩm.

## Bối cảnh và feedback đã xác nhận

- Video dọc ngắn/hài tại cửa hàng, chọn source theo bốn video mẫu. CLI 0.31.1; CapCut Windows 9.7.0.4153 trên máy Hero.
- Người dùng yêu cầu project thật có thể chỉnh sửa, lưu trong Phú Xuyên và xuất hiện ở trang chủ CapCut; không lưu bàn giao ở Temp.
- Sau pilot: tăng sáng một chút, lấy nhạc nền từ mẫu cho pilot. Người dùng tự xuất được và yêu cầu làm tiếp ba video.
- Sau đó: chuyển cảnh ở điểm nối, logo trên trái, hạ chữ, thêm SFX cho chữ khi cần; chú ý câu thừa đầu/cuối source.
- Kết quả cuối được người dùng phản hồi “ổn rồi”. Không suy ra rằng mọi thông số kỹ thuật trong ca này là sở thích cố định.

## Nơi lưu sản phẩm và bản nào là mới nhất

Source root: `D:\C\MKT\T11\Edit\411_phu xuyen\Phú Xuyên`.

Output root: [CapCut_Edit](<D:/C/MKT/T11/Edit/411_phu xuyen/Phú Xuyên/CapCut_Edit>).

| Bản dựng | Thời lượng | Trong output root | Folder trên CapCut |
|---|---|---|---|
| Đồng ý, pilot | 11.2 giây | `Dong_y_v02/PhuXuyen_DongY_v02_editable` | `PhuXuyen_DongY_v02` |
| Như người nhà | 15.6 giây | `02_Nhu_nguoi_nha/editable_project` | `02_Nhu_nguoi_nha_CLI` |
| Sếp bảo là phải nghe | 26.966667 giây | `03_Sep_bao_la_phai_nghe/editable_project` | `03_Sep_bao_la_phai_nghe_CLI` |
| Thế mà lại hay | 20.533333 giây | `04_The_ma_lai_hay/editable_project` | `04_The_ma_lai_hay_CLI` |

CapCut store root: `%LOCALAPPDATA%\CapCut\User Data\Projects\com.lveditor.draft`.

Ba video còn lại có MP4 `<tên_folder>_v02.mp4`, `DELIVERY.json`, `HUONG_DAN.txt`, `revision_v02.json`, `validation_v02.json`, `render_verification_v02.json`, `MUSIC_CREDITS.txt` và ảnh review trong folder tương ứng. Tra thêm `remaining_projects.json`, `BAN_GIAO_3_VIDEO.txt`, `native_home_check.json` ở output root.

**Draft native hiện tại là nguồn sự thật khi dựng tiếp.** `edit.spec.json` của ba video là spec v01, chưa cập nhật hết chỉnh sửa native v02. Đọc draft đang dùng và so thời gian/lịch sử chỉnh sửa trước khi chọn bản để sửa; người dùng có thể đã sửa tiếp từ sau bàn giao.

## Những thay đổi tạo khác biệt

| Trước/phát hiện | Sau và bài học |
|---|---|
| Chữ pilot native size 28 quá lớn | Sửa trong app xuống 14, đậm trắng/viền đen. Ba bản sau dùng title 9, caption khoảng 10.5–12; luôn thử font native trước |
| Logo/chữ chưa đúng ý | Ba bản sau đặt logo trên trái (`x=-0.72, y=0.87, scale=0.14`); hạ upper text 0.13 và lower caption 0.10 đơn vị nửa chiều cao canvas, khoảng 125/96 px ở 1920p |
| Một số câu dài chiếm khung | Ngắt dòng theo nghĩa, ví dụ “Phải biết GIỮ CHÂN / khách hàng”; vàng cho từ khóa, tách track title/caption |
| Cần rõ nhịp nối | Transition native 0.2 giây: Như người nhà 4, Sếp 5, Thế mà lại hay 2; kiểm tra không đổi thời lượng thoại |
| Cần thêm nhấn câu | Pop chữ nhẹ và SFX có chọn lọc; Sếp có 7 điểm pop, Thế mà lại hay có 3; không thêm pop vào tiêu đề tĩnh Như người nhà |
| Source sáng chưa đủ | Chuẩn hóa rotation/FPS và tăng sáng midtone nhẹ, giữ original; thông số cụ thể ở playbook |

Các tọa độ trên là giá trị quan sát trong ca này; cần xác minh chiều/trục transform bằng frame trong app, không suy luận từ hướng trục của renderer khác.

## Rà câu thừa: các quyết định cụ thể

- Như người nhà: C4665 mở cảnh, C4668 gồm các câu chính; bỏ tiếng “Ê!” ngoài nhịp chọn và khoảng chết.
- Sếp: ghép các chỉ dẫn C4684 với minh họa C4686/C4688/C4690. Bỏ “chào các bạn” ở cuối C4686, “OK” ở cuối C4684 và đếm nhịp trước C4690. Trim riêng audio sát biên để bỏ âm “và” của câu tiếp theo mà không dịch hình.
- Thế mà lại hay: C4678 mở tình huống, C4677 hỏi môi trường làm việc, C4679 làm reaction. Bỏ “Đi đi” đầu C4677 và mute câu “tạm biệt” ngoài cảnh ở reaction. Giữ “thôi thôi… được rồi” vì còn thuộc diễn biến hài.
- C4671–C4675 gần như không có âm thanh hữu ích. Không dựa vào ASR để tự bịa thoại cho source im lặng.

## Whisper và công cụ đã dùng

- Đã tìm trong `D:\C\Dev\du an`; script ở repo cũ trỏ cache của user khác không còn tồn tại.
- Model Small thực sự có sẵn trong `_analysis/models` ở thư mục Phú Xuyên, đã copy đầy đủ vào `CapCut_Edit/_tools/whisper-small`.
- Runtime: `C:\Users\Hero\tools\venv-video\Scripts\python.exe`; faster-whisper CPU int8, tiếng Việt, VAD và word timestamps. Chạy offline, không tải âm thanh lên cloud.
- Transcript: `CapCut_Edit/_analysis/transcripts_complete.json`; script cùng folder `transcribe_remaining.py`. ASR có lỗi khi tiếng nhỏ/chồng lời, cần đối chiếu nguồn.
- FFmpeg/ffprobe: `C:\Users\Hero\tools\ffmpeg\bin`; source 59.94 FPS có rotation ±90°, chuẩn hóa 1080×1920 CFR 30.
- Font native: Metropolis Medium từ `CapCut/Apps/9.7.0.4153/Resources/Font/SystemFont/en.ttf`; sample style ở `_work_remaining/native_text_style.json`.

Đường dẫn công cụ là ghi nhận máy này, cần kiểm tra tồn tại/phiên bản khi chạy lại. Python đọc JSON PowerShell bằng `utf-8-sig` khi có BOM; tránh truyền script tiếng Việt qua stdin pipeline PowerShell gây mất dấu. Node ESM trên Windows dùng file URL hoặc `pathToFileURL`, không import trực tiếp chuỗi `D:/...`.

## Lỗi kỹ thuật và cách tránh lặp lại

- **Skeleton:** dùng draft rỗng `1031` do app hiện tại tạo làm template, không dùng mặc định template cũ rồi chỉ thay version. Không mang timeline donor sang project mới.
- **Frame rounding:** start/duration tính độc lập bằng số giây thập phân tạo gap 1 µs. Làm tròn điểm start/end theo frame rồi lấy hiệu để có duration; source duration theo speed. Ba bản v02 lint frame grid sạch.
- **Active timeline:** app có thể tạo `Timelines/` sau khi mở. Chỉ opt-in active timeline khi có pointer hợp lệ; khi lưu lại dùng store API, không sửa root đơn lẻ.
- **Text overlap:** title dài và caption cùng thời điểm cần tách track; short SFX chồng nhau cũng phải sắp track đúng chủ đích, không chỉ nới lint.
- **Đăng ký home bị trùng:** app lưu forward slash, CLI so sánh đường dẫn dạng chuỗi có thể ghi thêm backslash alias cùng `draft_id`. Đã đóng app, backup `root_meta_info.json`, chỉ gộp alias của ba ID thuộc tác vụ, giữ entry canonical và chuẩn hóa path fields về `/`. Không xóa file/draft người dùng.
- **Không chạy register lại tùy tiện:** lỗi alias chưa được sửa trong source repo. Kiểm tra chỉ mục theo ID và đường dẫn chuẩn hóa, bảo toàn các mục khác; mở lại app để xác nhận home.
- **Preview khác native:** FFmpeg xfade chỉ mô phỏng các họ transition. Phải giữ đúng thời lượng/thoại và ghi rõ bản xem thử; người dùng xuất cuối trong CapCut.
- **FFmpeg đã cài:** bản dùng trong ca này không nhận `-filter_complex_script`; truyền `-filter_complex`. Duration literal dùng `0.5`, không `.5`.

## Script có sẵn: đọc trước khi chạy

Các file dưới nằm trong `CapCut_Edit/_work_remaining`, ngoài repo CLI.

| File | Vai trò / lưu ý |
|---|---|
| `make_remaining.py` | Sinh base spec/assets; chạy lại có thể đưa về bố cục/plan cũ |
| `build_remaining.mjs` | Compile và đăng ký ban đầu; có thể tạo lại alias home |
| `revise_layout_transitions.mjs` | Áp v02 từ `before_layout_revision.json`, thêm transition/SFX, register; có thể mất chỉnh sửa mới và wrap chữ |
| `render_v02.py` | Render preview từ draft bàn giao; có lọc theo tên folder, không coi hiệu ứng mô phỏng là native export |
| `finalize_remaining.mjs`, `finish_v02.mjs` | Hoàn thiện/đăng ký/đặt tên ở giai đoạn trước; không chạy lại nguyên trạng sau sửa alias |
| `polish_and_dedupe.mjs` | Đồng bộ native sang bàn giao, wrap caption và gộp alias ba project; chỉ phù hợp trạng thái/ID của ca này |

Nếu cần tái dựng, tạo script mới hoặc sửa script có kiểm soát từ draft hiện tại; không chạy nối toàn bộ script theo tên. Giữ backup trước khi ghi.

## Bằng chứng và giới hạn

- Ba MP4 v02: Full HD dọc 30 FPS H.264/AAC; decode toàn bộ và kiểm tra duration thành công; xem các ảnh review. Lint báo 0 errors/0 warnings theo cấu hình lưu trong log (có ngưỡng dành cho title dài, không phải mọi default).
- Đã xác nhận trang chủ CapCut có ba project v02 riêng biệt, gộp ba alias cũ, giữ file gốc. Pilot cũng đã đồng bộ lại vào thư mục bàn giao sau chỉnh native.
- Sếp v02: đã mở project trong app, chọn transition Pull in 0.2 giây và quan sát radial zoom blur ở điểm nối; kiểm tra logo/chữ. Đây là bằng chứng native cụ thể, không khẳng định đã phát và nghe từng frame của cả ba project trong app.
- Runtime nhận audio để nghe không hỗ trợ trong phiên này; việc rà thoại dựa trên source/ASR word timestamps và phân tích, không ghi là đã nghe toàn bộ bằng tai.
- Nhạc ba video sau dùng Kevin MacLeod, giấy phép/attribution lưu trong `MUSIC_CREDITS.txt`. Pilot theo yêu cầu lấy nhạc mẫu; không suy ra quyền phát hành nhạc đó từ việc có file.

Bài học tái sử dụng được cập nhật vào [playbook](../video-editing-playbook.vi.md); các thông số, ID và script phụ thuộc ca dựng giữ tại đây.
