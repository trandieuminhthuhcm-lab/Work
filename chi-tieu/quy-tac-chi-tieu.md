# Quy tắc ghi sổ chi tiêu

Sổ chính: Google Sheets "Chi tiêu năm 2026", mỗi tháng một tab ("Tháng 10", "Tháng 11"...).
Link: https://docs.google.com/spreadsheets/d/1hEWfbRhrWTYZFSEvDlFr-NmbvxGqn-OYrbZsOz560Rk/edit

## Cách ghi trong sổ
- Số tiền ghi theo đơn vị nghìn đồng (70 = 70.000đ).
- Cột D: hình thức trả (tm, ck, momo, shopee, thẻ). Cột E: ngày dạng chữ "dd/mm". Cột F: món. Cột L: ghi chú.
- Tiền trả bằng tiền mặt, chuyển khoản, ví, thẻ VCB ghi ở cột H. Cà **thẻ khác** (không trừ vào tài khoản VCB, ví dụ Kingfood) ghi ở cột I.
- Ba mục: Nhu cầu (ăn uống ngoài, cà phê, ship, Grab), Đi chợ (thực phẩm, đồ dùng bếp, siêu thị), Tạp hóa (mua sắm, dịch vụ, vải, Netflix, Claude...).
- Tiền vào ghi ở bảng "Nguồn" (cột O–R).
- Dòng 139 ("Tổng"), đã sửa từ Tháng 9 trở đi:
  - I139 (tổng thẻ khác) `=SUM(I2:I41,I43:I98,I100:I138)`
  - K139 (tổng chi thực tế) `=SUM(M1,M42,M99)+I139`
  - M139 (tiền vào) `=sum(Q56:Q138)`, N139 (còn lại) `=M139-K139`
  - C139 (% chi so với thu) `=IF(M139=0,0,K139/M139)`
  Tạo tab tháng mới bằng cách nhân bản tab tháng trước rồi xóa dữ liệu cũ, để giữ công thức này.

## Quy tắc nhận diện giao dịch
- Nạp ví (MoMo/ShopeePay) **17.000đ hoặc 26.000đ** = **phí ship Grab** mặc định.
- Chuyển khoản cho **Nguyễn Mạnh Tuấn (QR 90073, VietinBank)** = **đi cà phê** (mục Nhu cầu).
- Chuyển khoản cho **Cao Thị Mỹ Linh (nội dung QR "KOVQR…")** = **sữa chua** (mục Đi chợ).
- Đơn siêu thị: số tiền **trùng** với một giao dịch trong sao kê/ví = chuyển khoản (hoặc MoMo); **không trùng** = cà thẻ khác.
- Cùng một món nhưng **khác ngày** là mua nhiều lần, không phải mua trùng.
- Đơn TikTok/Shopee đã hủy hoặc trả hàng thì **không tính**. Tiền hoàn TikTok có thể vào **ví TikTok**.
- Nạp ví rồi được hoàn/thất bại (ví dụ Grab thất bại) thì chỉ tính lần trả thành công.
- Thông báo ngân hàng trùng: kiểm tra số dư, nếu số dư chỉ giảm một lần thì chỉ ghi một lần.
