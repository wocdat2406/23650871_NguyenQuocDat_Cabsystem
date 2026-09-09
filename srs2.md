# Bước 1: Phân tích yêu cầu sơ khởi

## 1.1. Business Context

- **Khách hàng:** Công ty ABC – doanh nghiệp cung cấp dịch vụ đặt xe trực tuyến.
- **Dự án:** Xây dựng CAB System – nền tảng đặt xe.
- **Thời gian thực hiện:** 7 tuần.
- **Hệ thống hiện tại:** Khách hàng đặt xe qua tổng đài hoặc ứng dụng đơn giản.
- **Người dùng chính:**
  - Khách hàng.
  - Tài xế.
  - Nhân viên vận hành.

### Quy trình nghiệp vụ chính

1. Khách hàng gửi yêu cầu đặt xe.
2. Hệ thống tìm và phân công tài xế phù hợp.
3. Tài xế nhận và thực hiện chuyến đi.
4. Khách hàng theo dõi trạng thái chuyến đi.
5. Hệ thống tính cước sau khi hoàn thành chuyến.
6. Khách hàng thanh toán.
7. Khách hàng đánh giá tài xế.

---

## 1.2. Business Problem

Các vấn đề chính của hệ thống hiện tại:

- Việc **phân công tài xế chủ yếu thực hiện thủ công**.
- Khách hàng **khó theo dõi trạng thái chuyến đi**.
- Thông tin **thanh toán chưa được quản lý tập trung**.
- Nhân viên vận hành **khó theo dõi và quản lý chuyến đi, tài xế**.
- Hệ thống hiện tại **khó mở rộng khi số lượng khách hàng và tài xế tăng**.
- Một số thông tin nghiệp vụ như **cách tính cước, tiêu chí chọn tài xế, chính sách hủy chuyến** vẫn chưa được xác định rõ và cần BA làm rõ với khách hàng.

---

## 1.3. Vấn đề cốt lõi cần giải quyết

> Công ty ABC cần một hệ thống đặt xe mới có khả năng tự động hóa việc tìm và phân công tài xế, giúp khách hàng theo dõi chuyến đi, quản lý thanh toán tập trung và hỗ trợ doanh nghiệp mở rộng hệ thống trong tương lai.
