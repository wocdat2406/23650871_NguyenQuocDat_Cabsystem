# BƯỚC 1: PHÂN TÍCH YÊU CẦU SƠ KHỞI

## 1.1. Business Context

### Khách hàng là ai?
- **Công ty ABC** là doanh nghiệp cung cấp dịch vụ đặt xe trực tuyến.
- Doanh nghiệp hiện phục vụ khách hàng thông qua tổng đài và một ứng dụng đặt xe đơn giản.
- Công ty muốn xây dựng **CAB System – Nền tảng đặt xe** mới để thay thế và cải tiến hệ thống hiện tại.

### Các nhóm người dùng chính
Hệ thống dự kiến phục vụ ít nhất 3 nhóm người dùng:

| Người dùng | Vai trò |
|---|---|
| Khách hàng | Đặt xe, theo dõi chuyến đi, thanh toán và đánh giá tài xế |
| Tài xế | Nhận chuyến, thực hiện chuyến và cập nhật trạng thái chuyến đi |
| Nhân viên vận hành | Quản lý khách hàng, tài xế, phương tiện, chuyến đi và xử lý sự cố |

### Quy trình nghiệp vụ chính
Quy trình đặt xe cơ bản được hiểu như sau:

1. Khách hàng đăng nhập vào hệ thống.
2. Khách hàng nhập điểm đón, điểm đến và lựa chọn loại xe.
3. Khách hàng gửi yêu cầu đặt xe.
4. Hệ thống tìm các tài xế phù hợp.
5. Tài xế nhận thông báo và chấp nhận hoặc từ chối chuyến.
6. Nếu tài xế từ chối hoặc không phản hồi, hệ thống tiếp tục tìm tài xế khác.
7. Khi có tài xế nhận chuyến, khách hàng được thông báo.
8. Tài xế đến điểm đón và cập nhật trạng thái chuyến đi.
9. Tài xế thực hiện chuyến đi.
10. Khi chuyến hoàn thành, hệ thống tính cước.
11. Khách hàng thanh toán bằng tiền mặt hoặc thanh toán điện tử.
12. Hệ thống lưu thông tin chuyến đi và thanh toán.
13. Khách hàng có thể đánh giá tài xế.

---

## 1.2. Business Problem

Hệ thống hiện tại của Công ty ABC đang tồn tại một số vấn đề chính:

### BP01 – Phân công tài xế thủ công
Việc phân công tài xế hiện nay chủ yếu do con người thực hiện, dẫn đến:
- Mất nhiều thời gian.
- Khó lựa chọn tài xế gần khách hàng.
- Khó xử lý khi số lượng yêu cầu đặt xe tăng cao.

### BP02 – Khách hàng khó theo dõi chuyến đi
Khách hàng chưa có khả năng theo dõi đầy đủ:
- Hệ thống đã tiếp nhận yêu cầu hay chưa.
- Hệ thống đang tìm tài xế hay không.
- Tài xế nào đã nhận chuyến.
- Thời gian dự kiến tài xế đến.
- Trạng thái hiện tại của chuyến đi.

### BP03 – Quản lý thanh toán chưa tập trung
Thông tin thanh toán chưa được quản lý tập trung, gây khó khăn trong:
- Theo dõi giao dịch.
- Tra cứu lịch sử thanh toán.
- Quản lý doanh thu.
- Xử lý giao dịch thanh toán thất bại.

### BP04 – Khó mở rộng hệ thống
Hệ thống hiện tại gặp khó khăn khi:
- Số lượng khách hàng tăng.
- Số lượng tài xế tăng.
- Lượng yêu cầu đặt xe tăng cao.
- Cần bổ sung các chức năng hoặc dịch vụ mới.

### BP05 – Khó quản lý hoạt động vận hành
Nhân viên vận hành chưa có công cụ tập trung để:
- Theo dõi các chuyến đang diễn ra.
- Kiểm tra trạng thái tài xế.
- Quản lý khách hàng và phương tiện.
- Xử lý các chuyến gặp lỗi.
- Tra cứu lịch sử giao dịch.

### BP06 – Thiếu dữ liệu hỗ trợ quản lý
Ban lãnh đạo chưa có đầy đủ báo cáo để theo dõi:
- Số lượng chuyến.
- Doanh thu.
- Tỷ lệ hoàn thành chuyến.
- Tỷ lệ hủy chuyến.
- Hiệu quả hoạt động của tài xế.

### BP07 – Rủi ro khi một chức năng gặp sự cố
Nếu các chức năng như thanh toán hoặc thông báo xảy ra lỗi, hệ thống hiện tại có nguy cơ ảnh hưởng đến toàn bộ quy trình đặt xe.

---

## 1.3. Business Goal

Từ các vấn đề trên, hệ thống CAB hướng đến các mục tiêu nghiệp vụ sau:

| Mã | Business Goal |
|---|---|
| BG01 | Tự động tìm kiếm và phân công tài xế phù hợp cho khách hàng. |
| BG02 | Cho phép khách hàng theo dõi trạng thái chuyến đi theo từng giai đoạn. |
| BG03 | Hỗ trợ thanh toán bằng tiền mặt và thanh toán điện tử. |
| BG04 | Quản lý tập trung thông tin khách hàng, tài xế, phương tiện, chuyến đi và giao dịch. |
| BG05 | Hỗ trợ nhân viên vận hành theo dõi và xử lý các chuyến đi gặp sự cố. |
| BG06 | Cung cấp báo cáo phục vụ quản lý và đánh giá hoạt động kinh doanh. |
| BG07 | Đảm bảo hệ thống có khả năng phục vụ số lượng lớn khách hàng và tài xế. |
| BG08 | Cho phép các thành phần của hệ thống mở rộng độc lập khi tải tăng. |
| BG09 | Đảm bảo bảo mật dữ liệu và kiểm soát quyền truy cập. |
| BG10 | Xây dựng nền tảng linh hoạt để có thể bổ sung dịch vụ và chức năng mới trong tương lai. |

---

## 1.4. As-Is Process

Quy trình hiện tại của doanh nghiệp có thể khái quát như sau:

```mermaid
flowchart TD
    A[Khách hàng có nhu cầu đặt xe] --> B[Liên hệ tổng đài hoặc ứng dụng đơn giản]
    B --> C[Gửi thông tin yêu cầu chuyến đi]
    C --> D[Nhân viên/Hệ thống tiếp nhận yêu cầu]
    D --> E[Phân công tài xế chủ yếu thủ công]
    E --> F[Tài xế nhận chuyến]
    F --> G[Thực hiện chuyến đi]
    G --> H[Khách hàng thanh toán]
    H --> I[Thông tin chuyến và thanh toán được lưu]
