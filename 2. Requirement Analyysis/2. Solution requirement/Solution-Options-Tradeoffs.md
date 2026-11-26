# Notice Hub — Các phương án và trade-off

**Mục đích:** So sánh ngắn các hướng tổ chức sản phẩm và triển khai. Đây là tài liệu thảo luận, chưa phải quyết định kiến trúc.

## Bối cảnh đã thống nhất

- CIP hiện xử lý gửi/nhận Knox Mail và Knox Message.
- Knox Mail đi qua API chính thống.
- Với Knox Message, CIP thao tác với ứng dụng như bên thứ ba; đây không phải tích hợp API chính thống.
- Trang mới dự kiến phục vụ người dùng soạn mẫu và chiến dịch gửi. eVoucher và các tính năng khác cũng có thể được quản lý trong cùng một hub.
- Dự kiến deploy cùng máy với CIP Notice; cần chọn cách truy cập bằng domain, subdomain, path hoặc port.

## Phương án sản phẩm

| Phương án | Mô tả | Trade-off |
|---|---|---|
| **A. Hub chung, chia feature** | Một cổng chung; người dùng vào các feature như Gửi Knox và eVoucher. CIP tiếp tục là dịch vụ thực thi gửi. | Trải nghiệm và quản lý tập trung; cần thống nhất đăng nhập, phân quyền, điều hướng và ranh giới giữa các feature. |
| **B. Trang Gửi Knox riêng** | Xây riêng giao diện soạn mẫu/chiến dịch, kết nối CIP; eVoucher giữ độc lập. | Phạm vi ban đầu gọn; người dùng có thể phải vào nhiều hệ thống và một số chức năng quản trị có thể trùng lặp. |
| **C. Mở rộng eVoucher thành cổng chung** | Đặt chức năng Gửi Knox và các feature khác trong hệ thống eVoucher hiện có. | Có thể tận dụng hệ thống sẵn có; mức phù hợp phụ thuộc kiến trúc, quyền sở hữu và khả năng mở rộng của eVoucher. |

## Phương án truy cập / triển khai

| Cách triển khai | Ưu điểm | Trade-off |
|---|---|---|
| **Cùng máy, subdomain riêng** | URL riêng, dễ nhận biết ứng dụng; có thể cấu hình qua reverse proxy. | Cần cấu hình DNS, chứng chỉ và proxy theo hạ tầng hiện có. |
| **Cùng domain, path riêng** | Ví dụ `/notice-hub`; ít thêm tên miền. | Cần kiểm tra routing, xác thực và cấu hình ứng dụng dưới path con. |
| **Cùng máy, port riêng** | Có thể tách service và cấu hình ban đầu đơn giản. | URL có port; cần mở/cấp quyền port và kiểm soát truy cập phù hợp. |
| **Máy chủ riêng** | Cách ly tài nguyên và vòng đời triển khai. | Thêm hạ tầng, vận hành và cấu hình kết nối; chưa thấy yêu cầu bắt buộc trong thông tin hiện có. |

## Ranh giới tích hợp đề xuất để thảo luận

- Hub quản lý giao diện, mẫu, dữ liệu người nhận, lịch gửi và theo dõi chiến dịch.
- CIP tiếp tục thực hiện luồng gửi Knox hiện tại; hub gọi CIP qua cơ chế tích hợp được CIP hỗ trợ.
- Không xây lại xử lý Knox trong hub trước khi xác nhận API và trách nhiệm vận hành của CIP.
- Với Knox Message, cần ghi nhận phụ thuộc vào thao tác ứng dụng của CIP và cách CIP trả kết quả.

## Hướng ưu tiên để đánh giá

Đánh giá trước **Phương án A: hub chung, chia feature**, triển khai cùng máy với CIP Notice qua **subdomain hoặc path riêng**. Chỉ chọn hướng này nếu có thể tái sử dụng đăng nhập/phân quyền và CIP có giao diện tích hợp phù hợp. Nếu chưa, giữ trang Gửi Knox độc lập theo Phương án B để khoanh phạm vi.

Đây là hướng cần đánh giá, chưa phải quyết định cuối cùng. Chưa đủ thông tin để kết luận nên dùng subdomain hay path; port riêng là lựa chọn triển khai cần IT xác nhận.

## Cần chốt với IT / Product

1. CIP có API hoặc cơ chế tích hợp được hỗ trợ cho việc tạo yêu cầu gửi và lấy trạng thái không?
2. CIP trả những trạng thái nào cho Knox Mail và Knox Message?
3. Hub có dùng chung đăng nhập và phân quyền với CIP/eVoucher không?
4. eVoucher có thuộc cùng phạm vi hub hay chỉ liên kết sang hệ thống riêng?
5. Hạ tầng hiện tại hỗ trợ subdomain, path hay port nào?
6. Ai sở hữu vận hành CIP và feature hub sau khi go-live?
