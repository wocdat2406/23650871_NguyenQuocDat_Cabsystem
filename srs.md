Xây dựng một hệ thống cơ bản MVB 
đứng ở vai trò BA
bước 1: đọc và phân tích yêu cầu của khách hàng ở giai đoạn sơ khởi
### Xây dựng hệ thống cơ bản

**Đóng vai trò:** BA (Business Analyst)

#### Bước 1: Phân tích yêu cầu sơ  của khách hàng

Ở giai đoạn sơ khởi (giai đoạn 1), BA cần tập trung vào việc **phân tích và tìm hiểu yêu cầu của khách hàng**.

Mục tiêu chính là hiểu được **Business Context** – tức là **ngữ cảnh của nghiệp vụ**, bao gồm:

- **Khách hàng là ai?**
- **Doanh nghiệp đang giải quyết vấn đề gì?**
- **Mục tiêu kinh doanh (Business Goal) là gì?**
- **Quy trình nghiệp vụ hiện tại (As-Is) đang diễn ra như thế nào?**
- **Những vấn đề hoặc khó khăn đang tồn tại là gì?**
- **Hệ thống cần giải quyết vấn đề nào?**
- **Kết quả mong muốn (To-Be) của khách hàng là gì?**

  ....
  # BƯỚC 1: PHÂN TÍCH YÊU CẦU SƠ KHỞI CỦA KHÁCH HÀNG

## 1. Mục tiêu của bước phân tích

Trong giai đoạn sơ khởi, Business Analyst (BA) chưa đi sâu vào việc thiết kế hệ thống hay lựa chọn công nghệ.

Mục tiêu chính của BA là:

- Hiểu khách hàng và lĩnh vực kinh doanh.
- Hiểu vấn đề mà doanh nghiệp đang gặp phải.
- Xác định mục tiêu kinh doanh.
- Hiểu quy trình nghiệp vụ hiện tại (**As-Is**).
- Xác định các vấn đề và khó khăn trong quy trình hiện tại.
- Xác định hệ thống mới cần giải quyết vấn đề gì.
- Xác định trạng thái mong muốn trong tương lai (**To-Be**).

---

# 2. Khách hàng là ai?

Khách hàng là **Công ty ABC**, một doanh nghiệp hoạt động trong lĩnh vực **cung cấp dịch vụ đặt xe trực tuyến**.

Hiện tại, khách hàng có thể đặt xe thông qua:

- Tổng đài.
- Một ứng dụng đặt xe đơn giản.

Các đối tượng chính tham gia vào hoạt động kinh doanh gồm:

| Đối tượng | Vai trò |
|---|---|
| Customer | Người có nhu cầu đặt xe và sử dụng dịch vụ |
| Driver | Người nhận và thực hiện chuyến đi |
| Operation Staff | Nhân viên quản lý và vận hành hệ thống |
| Management | Ban lãnh đạo theo dõi hoạt động và hiệu quả kinh doanh |

---

# 3. Doanh nghiệp đang giải quyết vấn đề gì?

Về bản chất, Công ty ABC đang cung cấp dịch vụ kết nối giữa:

> **Khách hàng có nhu cầu di chuyển và tài xế có khả năng cung cấp dịch vụ vận chuyển.**

Quy trình kinh doanh cốt lõi có thể được mô tả như sau:

### Bước 2: Xác định các Stakeholders

#### 2.1. Danh sách Stakeholders

| Tên Stakeholders | Vai trò |
|---|---|
| **Khách hàng (Customer)** | Người sử dụng hệ thống để đặt xe, theo dõi chuyến đi, thanh toán và đánh giá dịch vụ. |
| **Tài xế (Driver)** | Nhận yêu cầu chuyến xe, xác nhận chuyến, thực hiện chuyến và cập nhật trạng thái chuyến đi. |
| **Nhân viên vận hành (Operator)** | Theo dõi và điều phối hoạt động đặt xe, hỗ trợ xử lý các vấn đề phát sinh trong quá trình vận hành. |
| **Quản trị viên (Admin)** | Quản lý người dùng, tài xế, phân quyền, cấu hình hệ thống và theo dõi hoạt động của hệ thống. |
| **Quản lý doanh nghiệp (Business Manager)** | Định hướng mục tiêu kinh doanh, theo dõi hiệu quả hoạt động và đưa ra các quyết định liên quan đến hệ thống. |
| **Bộ phận kế toán / tài chính (Finance)** | Quản lý doanh thu, giao dịch, đối soát và các vấn đề liên quan đến thanh toán. |
| **Đội ngũ phát triển (Development Team)** | Phân tích, thiết kế, phát triển, tích hợp và bảo trì hệ thống. |
| **Đội ngũ vận hành hệ thống (DevOps / IT Operations)** | Triển khai, giám sát, đảm bảo tính ổn định, khả năng mở rộng và xử lý sự cố hệ thống. |
| **Cổng thanh toán (Payment Gateway)** | Cung cấp dịch vụ xử lý và xác nhận các giao dịch thanh toán. |
| **Dịch vụ bản đồ / định vị (Map & Location Service)** | Cung cấp dữ liệu bản đồ, vị trí, khoảng cách và hỗ trợ tính toán lộ trình. |
| **Dịch vụ thông báo (Notification Service)** | Gửi thông báo đến khách hàng và tài xế thông qua các kênh như SMS, Email hoặc Push Notification. |

#### 2.2. Stakeholder Matrix

Stakeholder Matrix giúp xác định **mức độ ảnh hưởng (Power)** và **mức độ quan tâm (Interest)** của từng stakeholder đối với hệ thống.

```mermaid
quadrantChart
    title Stakeholder Matrix - CAB System
    x-axis "Mức độ quan tâm thấp" --> "Mức độ quan tâm cao"
    y-axis "Mức độ ảnh hưởng thấp" --> "Mức độ ảnh hưởng cao"
    quadrant-1 "Quản lý chặt chẽ"
    quadrant-2 "Giữ hài lòng"
    quadrant-3 "Theo dõi"
    quadrant-4 "Giữ được thông tin"
    "Quản lý doanh nghiệp": [0.85, 0.95]
    "Nhân viên vận hành": [0.85, 0.75]
    "Quản trị viên": [0.70, 0.80]
    "Khách hàng": [0.90, 0.55]
    "Tài xế": [0.85, 0.55]
    "Finance": [0.55, 0.65]
    "Development Team": [0.65, 0.70]
    "DevOps / IT": [0.55, 0.75]
    "Payment Gateway": [0.35, 0.45]
    "Map Service": [0.30, 0.35]
    "Notification Service": [0.25, 0.30]
