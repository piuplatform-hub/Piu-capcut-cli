# Kinh nghiệm dựng video bằng capcut-cli

Cập nhật: 2026-11-04. Điểm vào cho AI dựng tiếp: [AGENTS.md](../AGENTS.md). Ca đã dùng để đúc kết: [Phú Xuyên](case-studies/phu-xuyen-2026-11.md).

Mục tiêu là video có nhịp rõ, hình/chữ dễ nhìn, thoại dễ nghe và project dễ sửa. Thông số dưới đây là điểm khởi đầu đã dùng trong ca cụ thể; quyết định cuối dựa trên source, video mẫu và feedback mới.

## 1. Hiểu mẫu rồi chọn source

- Xem cấu trúc mẫu: mở đầu thu hút bằng gì, bao nhiêu nhịp thoại/hành động, lúc nào đổi cảnh, câu chốt và khoảng giữ phản ứng cuối.
- Lập bảng chọn source ngắn: tên file, nhân vật/hành động, câu thoại, source in/out, lý do ghép vào nhịp nào của mẫu. Không chọn chỉ vì hình giống mà lời/hành động lệch ý.
- Probe FPS, rotation, độ dài, âm thanh trước khi dựng. Có hình tốt không có nghĩa là có thoại dùng được; Phú Xuyên có nhiều file gần như im lặng.
- Làm một bản thử đại diện và dùng feedback để chốt hướng cho loạt. Giữ nhịp hài theo hành động, tránh ép mọi video về cùng độ dài.

## 2. Cắt sạch đầu/cuối mà vẫn giữ câu chuyện

Đây là yêu cầu người dùng nhắc riêng: source thường có câu thừa ở đầu và cuối.

1. Dùng ASR có timestamp để tìm câu; đối chiếu waveform/âm thanh gốc và hình. ASR là công cụ dò, không phải bản chép chính xác tuyệt đối, nhất là tiếng nhỏ hoặc chồng lời.
2. Rà vài giây quanh cả hai đầu mỗi đoạn chọn. Tìm đếm “một, hai, ba”, “OK”, hướng dẫn “đi đi”, câu chào/tạm biệt ngoài cảnh, lần diễn lại và âm tiết của câu kế tiếp.
3. Đặt cut ở khoảng ngắt tự nhiên; giữ phụ âm đầu/cuối, đủ thời gian thấy phản ứng và hiểu câu chốt. Không cắt “thôi thôi…” nếu đó là lời nhân vật trong tình huống hài.
4. Nếu hình cần giữ nhưng thoại thừa đã lọt vào, trim/mute riêng audio ở biên thay vì dịch toàn bộ hình và làm lệch nhịp. Tránh tạo tiếng bật ở điểm cắt bằng fade ngắn khi cần.
5. Kiểm tra lại các biên trong bản mix hoàn chỉnh. Câu thừa có thể nằm giữa timeline do ghép nhiều source, không chỉ ở đầu/cuối video thành phẩm.

Không đoán rồi sửa câu ASR kém tin cậy để đưa lên chữ. Nếu môi trường không nghe được âm thanh, ghi rõ giới hạn xác minh; không báo đã nghe toàn bộ.

## 3. Bố cục và chữ cho video dọc

- Dựng ở canvas đích rồi xem frame đủ kích thước và bản thu nhỏ như khi xem điện thoại. Đọc chữ nhanh và thấy mặt/hành động quan trọng là tiêu chí chính.
- Logo nhỏ, có khoảng thở, không che mặt hoặc nội dung; mặc định Phú Xuyên đặt góc trên trái. Không kéo dãn sai tỷ lệ.
- Chia vai trò chữ: tiêu đề giải thích tình huống; caption ngắn nhấn câu/hành động; từ khóa đổi màu khi giúp hiểu ý. Tách track cho tiêu đề tồn tại lâu và caption chồng thời gian có chủ đích.
- Ngắt dòng theo cụm nghĩa, thường một đến hai dòng; bớt chữ trước khi giảm font quá nhỏ. Kiểm tra dấu tiếng Việt, viền, ngắt dòng, tên riêng và phần chữ gần mép.
- Chữ trắng đậm + viền đen đã đọc tốt trên áo xanh/nền sáng Phú Xuyên; vàng dành cho một vài từ khóa. Không biến cả câu thành nhiều màu.
- Người dùng yêu cầu hạ chữ so với bản thử. Hạ vừa đủ để cân bố cục nhưng vẫn tránh mặt, bàn tay và vùng giao diện nền tảng. Không sao chép tọa độ mà không xem frame.
- Font size trong draft native khác pixel render. Ca này font native 28 quá lớn; cần thử trong CapCut trước khi nhân ra cả loạt. Font Metropolis Medium, tiêu đề size 9 và caption khoảng 10.5–12 phù hợp ba bản v02; đây không phải đơn vị pixel chung.

## 4. Nhịp dựng và chuyển cảnh

- Điểm nối phục vụ thay đổi ý/hành động. Giữ reaction đủ để gây cười; cắt khoảng chết nhưng tránh thoại bị dồn hoặc mọi cảnh cùng một nhịp.
- Theo feedback Phú Xuyên, dùng chuyển cảnh ngắn ở các điểm nối. Pull in/Pull out khoảng 0.2 giây hợp nhịp hài; blur cho thay đoạn gần nhau; black fade khi kết/chuyển ý phù hợp.
- Chọn ít họ hiệu ứng để video có sự nhất quán. Chuyển cảnh không được che mất biểu cảm, từ khóa hoặc phần kết của hành động.
- Xác minh hiệu ứng có tải/cache và thực sự chạy trong app. Không kết luận chỉ vì `materials.transitions` tồn tại.
- Xử lý handle và duration theo loại transition đang dùng. Tránh làm ngắn thoại hoặc lệch tổng thời lượng do renderer xfade tự trừ overlap. FFmpeg preview có thể chỉ mô phỏng native CapCut; ghi rõ khác biệt.
- Pop chữ nhẹ đã dùng: scale 0.92 → 1.04 → 1.00 trong khoảng 0.13 giây. Chỉ áp vào chữ cần nhấn; không làm tiêu đề tĩnh rung liên tục.

## 5. Hình ảnh

- Chuẩn hóa rotation trước; kiểm tra người đứng thẳng, tỷ lệ và crop đúng. Với Phú Xuyên: source 59.94 FPS có rotation metadata được chuẩn hóa thành 1080×1920, CFR 30.
- Tăng sáng nhẹ ở midtone, kiểm tra da mặt và áo trắng để tránh cháy. Đồng nhất sáng/màu giữa các cảnh trước khi thêm hiệu ứng.
- Curve ca Phú Xuyên: `0/0 0.25/0.275 0.5/0.54 0.75/0.78 1/1`, saturation 1.015. Đây là thiết lập của source đó, không phải preset cho mọi máy quay.
- Giữ source gốc; nếu bake chỉnh sáng/rotation vào media chuẩn hóa, lưu rõ bước xử lý. Track vẫn chỉnh được nhưng hiệu chỉnh đã bake không còn là filter native có thể tắt riêng.

## 6. Thoại, nhạc và SFX

- Thoại là ưu tiên trong video diễn/tư vấn. Nghe thử ở âm lượng nhỏ: vẫn hiểu lời mà không cần căng tai.
- Nhạc theo sắc thái từng video, có điểm vào/ra gọn và fade hợp lý. Có thể dùng nhạc từ mẫu khi được yêu cầu; ghi nguồn và kiểm tra quyền dùng khi đăng tải, không mặc định nhạc trong mẫu là miễn phí.
- Nhạc hài nhẹ đã dùng: Monkeys Spinning Monkeys và Sneaky Snitch của Kevin MacLeod; lưu credit/license cùng project. Nhạc khác phải có ghi chú nguồn tương ứng.
- Chuẩn hóa mức nhạc rồi mới cân với thoại. Mức gain 0.25 sau normalize -18 LUFS đã dùng trong ca này chỉ là điểm thử; độ rõ lời và peak bản mix mới quyết định mức cuối.
- Pop/boop cho từ khóa hoặc câu chốt, whoosh ngắn cho chuyển cảnh khi hợp. Không thêm SFX cho mọi chữ hay để âm thanh đến sớm làm lộ punchline.
- Tách thoại, nhạc và SFX thành track dễ chỉnh. Tránh chồng nhiều tiếng ở cùng một nhịp và clipping sau khi trộn.

## 7. Project bền vững và kiểm tra trước bàn giao

Đọc [skill](../skills/capcut-edit/SKILL.md) và [pitfalls](../skills/capcut-edit/references/pitfalls.md) khi viết draft. Chỉ sửa khi project đã đóng; dùng store API để đồng bộ các timeline/mirror.

| Nội dung | Điều cần xác minh |
|---|---|
| Nội dung/nhịp | Đúng source, đủ ý, bỏ cue thừa; reaction và câu chốt còn tự nhiên |
| Hình/chữ | Logo đúng góc, chữ vừa khung, dấu Việt đúng, sáng nhất quán, không che hành động |
| Âm thanh | Không sót âm tiết/câu ngoài cảnh, thoại rõ, nhạc/SFX vừa phải, không clipping |
| Timeline | Frame grid đúng, không gap/overlap ngoài chủ đích, source range hợp lệ, không đuôi đen |
| Media | File tham chiếu tồn tại ở thư mục bền vững; không phụ thuộc Temp; giữ original |
| Native app | Project hiện một lần ở home; mở được, media/chữ sửa được; hiệu ứng đại diện đã xem trong app |
| MP4 xem thử | Đúng kích thước/FPS/thời lượng; decode hết không lỗi; xem đầu/cuối và các điểm nối |
| Bàn giao | Draft mới nhất, MP4, hướng dẫn, credits và ghi chú kiểm tra khớp nhau |

Lint sạch giúp tìm lỗi cấu trúc, không thay đánh giá hình/âm thanh. Không tăng ngưỡng lint chỉ để làm sạch báo cáo; nếu tiêu đề tĩnh dài hơn caption thông thường thì ghi rõ phạm vi/ngưỡng kiểm tra.

## 8. Tích lũy kinh nghiệm sau mỗi ca

Thêm ca mới dưới `docs/case-studies/` và link vào danh sách dưới. Chỉ cập nhật khuyến nghị chung sau khi biết bối cảnh và kết quả. Phân biệt **người dùng đã yêu cầu**, **đã quan sát/xác minh**, **chưa thử**.

Mẫu ghi ngắn:

```markdown
# <Dự án> — <ngày>
- Bối cảnh: thể loại, mẫu, canvas/FPS, phiên bản app/CLI.
- Feedback: người dùng muốn sửa điểm nào; điều gì đã được chấp nhận.
- Trước → sau: thay đổi cụ thể và lý do.
- Kết quả: đã kiểm tra bằng cách nào, bằng chứng/file nào; giới hạn còn lại.
- Tái sử dụng: bài học nào nên đưa vào playbook; thông số nào chỉ riêng ca này.
- Bàn giao: đường dẫn draft/media/preview mới nhất; script nào có thể ghi đè.
```

Nhật ký hiện có:

- [Phú Xuyên — 2026-11-04](case-studies/phu-xuyen-2026-11.md): video hài ngắn, sửa bố cục/nhịp/âm thanh, kiểm tra native và xử lý mục home bị trùng.
