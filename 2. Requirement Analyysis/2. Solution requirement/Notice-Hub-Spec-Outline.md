# Notice Hub — Khung spec rút gọn

**Trạng thái:** Bản nháp; phương án triển khai chưa chốt

## 1. Bối cảnh và mục tiêu

Samsung muốn thay SMS bằng Knox Message/Mail cho một số chương trình, hiện có **Cặp lá yêu thương** và **Chúc mừng sinh nhật kèm voucher Got It**. Spec này mô tả nhu cầu gửi và theo dõi thông báo; phương án xây mới hay mở rộng hệ thống hiện có vẫn cần quyết định.

Thông tin tài khoản đã nêu: thương hiệu **SRV**, tài khoản gửi **SRV CONNECT** và **SRV EEP**.

## 2. Phạm vi chức năng theo prototype

### Soạn và gửi

- Chọn Knox Message hoặc Knox Mail.
- Soạn nội dung hoặc chọn mẫu sự kiện.
- Thêm người nhận, nhập tay hoặc import Excel.
- Ánh xạ các trường dữ liệu vào biến trong nội dung. Prototype đang dùng `field1`, `field2`, `field3`.
- Chọn tài khoản gửi, xem trước và gửi ngay hoặc lên lịch.
- Lưu chiến dịch ở trạng thái **Nháp**.

### Mẫu sự kiện

Quản lý mẫu cho **Cặp lá yêu thương** và **Chúc mừng sinh nhật**. Mẫu sinh nhật có nội dung voucher Got It và link nhận quà.

### Tài khoản gửi

Hiển thị và chọn tài khoản SRV CONNECT hoặc SRV EEP phù hợp với kênh gửi.

### Lịch sử và báo cáo

Tra cứu chiến dịch, thời gian gửi, số người nhận và trạng thái. Xem thống kê kết quả gửi.

## 3. Luồng nghiệp vụ chính

1. Người dùng chọn chương trình, kênh gửi và tài khoản.
2. Chọn mẫu hoặc soạn nội dung.
3. Nhập danh sách hoặc import Excel, ánh xạ dữ liệu vào biến.
4. Xem trước nội dung, lưu nháp, gửi ngay hoặc lên lịch.
5. Tra cứu trạng thái và kết quả gửi.

## 4. Ba phương án đang cân nhắc

1. Xây Notice Hub chuyên gửi Knox Message/Mail và có thể cung cấp API cho hệ thống khác.
2. Làm tool nhỏ cho Cặp lá yêu thương và voucher Got It.
3. Mở rộng hệ thống eVoucher đang có chức năng gửi Mail.

**Phương án triển khai chưa chốt.** Cần xác nhận khả năng eVoucher hỗ trợ Knox và nhu cầu các hệ thống khác trước khi chốt.

## 5. Cần xác nhận trước khi hoàn thiện spec

- Chọn phương án 1, 2 hay 3.
- Người dùng được chọn Knox Message, Knox Mail hoặc cả hai cho mỗi chương trình.
- Email là khóa định danh người nhận cho cả Knox Message và Knox Mail.
- Người dùng tự chuẩn bị danh sách nhân viên và dữ liệu biến trong file Excel.
- Link Got It và dữ liệu liên quan đã có sẵn; hệ thống dùng dữ liệu đó để gửi.
- Cặp lá yêu thương chỉ gửi thông báo về khoản khấu trừ lương; không xử lý thêm nghiệp vụ payroll.
- Trạng thái gửi nào Knox trả về và cần hiển thị trong lịch sử.
- Không yêu cầu duyệt trước khi gửi.

## 6. Tiêu chí nghiệm thu sơ bộ

- Người dùng tạo được nội dung theo mẫu và xem trước với dữ liệu người nhận.
- Import Excel hiển thị dữ liệu để kiểm tra trước khi gửi.
- Người dùng chọn được tài khoản gửi đã thống nhất.
- Chiến dịch có thể lưu nháp, gửi ngay hoặc lên lịch.
- Lịch sử hiển thị kết quả theo thông tin trạng thái mà Knox cung cấp.

## 7. Tài liệu liên quan

Prototype UI: `2. Requirement Analyysis/3. UI Design/notice-hub-prototype.html`

