# Bối cảnh dự án: AI Content Team

Đây là dự án xây dựng đội ngũ AI hỗ trợ nội dung cho kênh cá nhân — chủ đề kinh doanh tính nữ.
Nền tảng hoạt động: chỉ Instagram (không còn dùng YouTube).

## ĐỌC TRƯỚC KHI LÀM BẤT KỲ VIỆC GÌ

`/core/HO-SO-GOC.md` là nguồn sự thật duy nhất về bản thân chị và việc kinh
doanh (danh tính, câu chuyện, thương hiệu Khuyết, kênh Instagram, đối tượng
mục tiêu, giọng nói cốt lõi). Mọi agent, mọi phiên làm việc PHẢI đọc file đó
trước khi tạo bất kỳ output nào (content, hình ảnh, video, báo cáo...).
Các thư mục `/voice-bible`, `/research`, `/scripts-captions`, `/thumbnails`,
`/video-edits`, `/reports` chỉ chứa **kết quả phụ** do agent B–F tạo ra —
không phải nơi lưu thông tin gốc.

## Cấu trúc đội ngũ agent

| Agent | Nhiệm vụ | Output |
|---|---|---|
| A. Voice & Channel Analyst | Phân tích kênh của chị + kênh tham chiếu để hiểu giọng nói, niềm tin | "Voice bible" |
| B. Trend & Competitor Research | Tìm creator nổi bật trong ngành, phân tích công thức viral (không sao chép nguyên văn) | Danh sách video viral + phân tích công thức |
| C. Script/Caption Rewriter | Viết lại kịch bản/caption theo giọng của chị, dựa trên voice bible + công thức viral | Kịch bản, caption, tiêu đề |
| D. Thumbnail Reference | Tìm thumbnail nổi bật (ưu tiên creator nhỏ, tương tác cao), gợi ý restyle | Gợi ý bố cục/tiêu đề thumbnail |
| E. Video Editing (Kling) | Chỉnh sửa video theo brand kit bằng Kling API | Video đã edit — luôn chờ chị duyệt trước khi đăng Instagram |
| F. Reporting | Tổng hợp kết quả mỗi ngày | File Excel hoặc email tóm tắt |

## Voice bible (điền sau khi hoàn thành Bước 1 — để trống nếu chưa có)
- Giọng nói:
- Chủ đề chính:
- Niềm tin cốt lõi:
- Đối tượng hướng tới:

## Thông tin vận hành (điền khi có)
- Kling API key: (KHÔNG lưu key thật vào file này — dùng biến môi trường, ví dụ KLING_API_KEY trong .env hoặc shell profile)
- Brand kit (màu sắc, phong cách):

## Kết nối MCP server
Gmail, Google Calendar, Google Drive, Notion, Canva được đăng ký ở scope user (dùng mọi project).
Kling API và Instagram Graph API KHÔNG có MCP server chính thức — gọi trực tiếp qua HTTP (Bash + curl,
hoặc script Python/Node), API key/token đọc từ biến môi trường, không hard-code.

## Giới hạn kỹ thuật đã biết — LUÔN áp dụng, không hỏi lại

1. Ảnh từ web: WebFetch chỉ trả về tóm tắt dạng chữ, KHÔNG tải được file ảnh thật.
   Muốn tải ảnh: dùng Bash chạy curl/wget tải file về, sau đó Read để xem.
2. Video: không có công cụ đọc video trực tiếp.
   Muốn xem nội dung video: dùng ffmpeg (qua Bash) tách khung hình thành ảnh, rồi Read từng ảnh.
3. Dán ảnh (paste) hay lỗi: ưu tiên kéo-thả file ảnh vào cửa sổ, hoặc đưa đường dẫn file trực tiếp.
4. MCP server có thể tự ngắt giữa phiên (lỗi đã biết của Claude Code).
   Nếu một công cụ kết nối đột nhiên báo lỗi, chạy /doctor rồi claude mcp list để kiểm tra, gõ /mcp
   để kết nối lại — đừng lặp lại lệnh nhiều lần vì tốn token.
5. Đăng bài lên Instagram: luôn dừng lại để chị duyệt thủ công trước khi đăng thật.

## Quy tắc làm việc
- Không sao chép nguyên văn kịch bản/caption của người khác — chỉ lấy công thức, cấu trúc, rồi viết lại theo giọng của chị.
- Ưu tiên chia nhỏ nhiệm vụ theo từng agent (A–F) trong các phiên riêng, tránh giao tất cả cùng lúc.
