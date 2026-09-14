---
name: pinterest-quote-post
description: >
  Dựng carousel ảnh-chèn-chữ phong cách Pinterest (mỗi câu/ý một trang, chữ
  trắng đậm canh giữa trên nền ảnh nghệ thuật) để đăng Instagram cho kênh
  @dieuthu.diary. Dùng khi chị gửi nội dung (một chuỗi câu ngắn hoặc một đoạn
  văn cần tách trang) và muốn "làm bài viết chèn ảnh kiểu Pinterest", "làm
  carousel ảnh có chữ", "lên hình cho caption này". Luôn kết thúc bằng dòng
  kêu gọi follow cố định.
---

# Pinterest Quote Post (carousel ảnh-chữ cho Instagram)

## Trước khi làm

Đọc `/core/HO-SO-GOC.md` trước tiên (bắt buộc theo CLAUDE.md của dự án) để
nắm giọng nói, thương hiệu Khuyết, đối tượng mục tiêu. Skill này tạo **kết
quả phụ** — lưu output vào `/scripts-captions/`, không sửa `HO-SO-GOC.md`.

Lưu ý nền tảng: sản phẩm cuối là carousel đăng **Instagram** (kênh
@dieuthu.diary). "Pinterest" ở đây chỉ là tên gọi cho *phong cách* ảnh-chữ
(aesthetic, thơ mộng, tối giản) mượn từ Pinterest — không phải đăng lên
Pinterest thật, đúng theo CLAUDE.md (nền tảng hoạt động chỉ Instagram).

## Mẫu tham chiếu (giữ nguyên font/style)

Chị đã gửi 1 thiết kế Canva mẫu làm chuẩn font chữ:
- Shortlink: https://canva.link/sl9r3fogq83ur0l
- Design ID: `DAHUnCcIGOw`

Style của mẫu: mỗi trang là 1 ảnh nền, đè lên 1 dòng chữ **trắng, đậm, sans-serif,
canh giữa ảnh, có shadow/outline nhẹ để đọc rõ trên mọi nền** — không phải
chữ viết tay/script. Đây là phần "nghệ thuật" chị muốn: cách trình bày sạch,
sang, dễ đọc, không phải kiểu font.

Cách giữ đúng font mà không cần đoán tên font: dùng `copy-design` (Canva MCP)
trên design ID trên để tạo bản sao làm khung mỗi lần chạy skill này, rồi chỉ
sửa text + ảnh nền qua `edit-design` — font/style tự động giữ nguyên như mẫu.
Nếu `copy-design` không tạo đủ số trang cần, nhân bản thêm trang trong lúc
edit rồi áp cùng font/kiểu chữ với các trang gốc.

## Quy trình

1. **Nhận nội dung từ chị.** Nội dung có thể là:
   - Một chuỗi câu ngắn, mỗi câu = 1 trang (giống mẫu: "Mình nói về X / Nhưng
     vẫn Y..."), hoặc
   - Một đoạn văn/caption dài — tự tách thành các ý ngắn, mỗi ý 1 trang (ưu
     tiên câu ngắn, dễ đọc trong 2-3 giây, đúng nhịp giọng Khuyết: nhẹ nhàng,
     chân thành, không gồng).
   Nếu nội dung chị gửi mơ hồ về cách tách trang, hỏi lại trước khi dựng.

2. **Trang cuối luôn cố định** — không tự ý đổi chữ:
   > Follow được nhắc nhở trở thành phiên bản tốt hơn của bạn mỗi ngày

3. **Tìm ảnh cho từng trang.** Chị đã xác nhận: tự tìm ảnh, phong cách
   "Pinterest art" — nghệ thuật, mơ màng, aesthetic, tối giản, hợp tông
   Khuyết (không cần là ảnh đời thường/selfie như mẫu, trừ khi chị gửi kèm
   ảnh cụ thể cho trang nào đó — nếu có thì ưu tiên dùng ảnh chị gửi).
   - Ưu tiên tìm qua `mcp__Canva__get-assets` (thư viện ảnh có sẵn trong
     Canva) bằng từ khóa theo chủ đề/tâm trạng của từng dòng chữ (tiếng Anh
     lẫn tiếng Việt đều thử, vd: "dreamy woman aesthetic", "soft light
     mirror selfie", "minimal feminine lifestyle").
   - Nếu cần ảnh từ nguồn ngoài Canva: theo giới hạn kỹ thuật CLAUDE.md —
     WebFetch chỉ trả tóm tắt chữ, KHÔNG tải được ảnh thật. Phải dùng Bash
     (`curl`/`wget`) tải file ảnh về rồi mới `upload-asset-from-url` /
     Read để kiểm tra ảnh trước khi chèn.
   - Chọn ảnh có vùng nền đủ "sạch" (ít chi tiết rối) ở chỗ đặt chữ để chữ
     trắng vẫn đọc rõ.

4. **Dựng carousel:**
   - `copy-design` từ `DAHUnCcIGOw` để lấy khung font/style.
   - Với mỗi trang: `edit-design` để thay ảnh nền + thay text, giữ nguyên
     vị trí/kiểu chữ như mẫu (trắng, đậm, canh giữa, có shadow).
   - Đọc lại (`read-design` kèm `thumbnails`) để tự kiểm tra: chữ có bị lem
     ra ngoài khung, có đọc được trên nền ảnh không, thứ tự trang có đúng
     mạch nội dung không.

5. **Không tự đăng Instagram.** Đưa link Canva (view/edit) cho chị duyệt —
   đúng giới hạn kỹ thuật #5 trong CLAUDE.md (luôn dừng lại chờ chị duyệt
   thủ công trước khi đăng thật).

6. **Lưu bản ghi** vào `/scripts-captions/YYYY-MM-DD-<slug-noi-dung>.md` gồm:
   - Link Canva (view_url + edit_url)
   - Text từng trang theo đúng thứ tự
   - Nguồn ảnh đã dùng cho từng trang (từ khóa tìm hoặc link ảnh chị gửi)
   - Caption/CTA đi kèm bài đăng Instagram (nếu chị có nhờ viết thêm — ngắn
     gọn, đúng giọng Khuyết, có thể tái dùng skill `khuyet-caption` nếu bài
     liên quan trực tiếp sản phẩm Khuyết; nếu là nội dung cá nhân/tâm sự thì
     giữ giọng gần với ví dụ mẫu, không cần bán hàng).

## Lưu ý MCP

Nếu công cụ Canva MCP đột nhiên báo lỗi giữa chừng: theo CLAUDE.md, chạy
`/doctor` rồi `claude mcp list` để kiểm tra, gõ `/mcp` để kết nối lại — đừng
lặp lại lệnh nhiều lần vì tốn token.
