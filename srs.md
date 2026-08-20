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

```text
Khách hàng có nhu cầu di chuyển
        ↓
Tạo yêu cầu đặt xe
        ↓
Tìm tài xế phù hợp
        ↓
Tài xế nhận chuyến
        ↓
Tài xế đến đón khách
        ↓
Thực hiện chuyến đi
        ↓
Hoàn thành chuyến
        ↓
Tính cước và thanh toán
        ↓
Khách hàng đánh giá dịch vụ
  
# BƯỚC 2: XÁC ĐỊNH STAKEHOLDERS VÀ STAKEHOLDER MATRIX

## 1. Mục tiêu

Sau khi đã phân tích **Business Context** ở Bước 1, Business Analyst (BA) cần xác định các **Stakeholders** liên quan đến dự án CAB System.

Stakeholder là cá nhân, nhóm người hoặc tổ chức:

- Sử dụng hệ thống.
- Bị ảnh hưởng bởi hệ thống.
- Có quyền ra quyết định đối với hệ thống.
- Cung cấp yêu cầu cho hệ thống.
- Tham gia vận hành hoặc phát triển hệ thống.

Việc xác định Stakeholders giúp BA:

- Hiểu ai liên quan đến hệ thống.
- Xác định ai có quyền ra quyết định.
- Xác định ai cung cấp yêu cầu nghiệp vụ.
- Xác định nhóm người dùng chính.
- Xác định mức độ ảnh hưởng và mức độ quan tâm của từng Stakeholder.
- Xây dựng kế hoạch giao tiếp phù hợp.

---

# PHẦN 1: XÁC ĐỊNH STAKEHOLDERS

## 1.1. Danh sách Stakeholders

Dựa trên yêu cầu của dự án CAB System, các Stakeholders chính được xác định như sau:

| Stakeholder | Vai trò |
|---|---|
| Ban giám đốc / Business Sponsor | Định hướng dự án, phê duyệt ngân sách, phạm vi và các quyết định quan trọng |
| Business Owner | Đại diện cho nhu cầu kinh doanh, xác định mục tiêu và giá trị mong muốn của hệ thống |
| Khách hàng (Customer) | Người sử dụng dịch vụ đặt xe, tạo yêu cầu đặt xe, theo dõi chuyến đi và thanh toán |
| Tài xế (Driver) | Nhận chuyến, thực hiện chuyến đi và cập nhật trạng thái chuyến |
| Nhân viên vận hành (Operation Staff) | Quản lý khách hàng, tài xế, phương tiện, chuyến đi và hỗ trợ xử lý sự cố |
| Quản trị viên hệ thống (System Administrator) | Quản lý tài khoản, quyền truy cập và các hoạt động quản trị hệ thống |
| Business Analyst (BA) | Thu thập, phân tích, làm rõ và quản lý yêu cầu giữa Business và đội ngũ phát triển |
| Project Manager (PM) | Quản lý tiến độ, nguồn lực, phạm vi và việc triển khai dự án trong thời gian 7 tuần |
| Development Team | Phân tích kỹ thuật, thiết kế và phát triển CAB System |
| QA / Tester | Kiểm thử hệ thống, xác nhận các chức năng đáp ứng yêu cầu |
| Payment Provider | Cung cấp dịch vụ xử lý thanh toán điện tử và trả kết quả giao dịch |
| Notification Provider | Cung cấp dịch vụ gửi thông báo như Push Notification, SMS hoặc các kênh khác |
| Bộ phận Tài chính / Kế toán | Theo dõi doanh thu, giao dịch và các thông tin tài chính liên quan |
| Bộ phận Chăm sóc khách hàng | Hỗ trợ khách hàng và xử lý các vấn đề liên quan đến chuyến đi hoặc thanh toán |

---

# PHẦN 2: STAKEHOLDER MATRIX

## 2.1. Mục đích của Stakeholder Matrix

Stakeholder Matrix được sử dụng để đánh giá Stakeholder dựa trên hai yếu tố:

- **Power / Influence:** Mức độ quyền lực hoặc khả năng ảnh hưởng đến dự án và hệ thống.
- **Interest:** Mức độ quan tâm hoặc mức độ bị ảnh hưởng bởi hệ thống.

Từ đó, BA có thể xác định cách thức giao tiếp và quản lý phù hợp với từng nhóm Stakeholder.

---

## 2.2. Các nhóm trong Stakeholder Matrix

| Nhóm | Power / Influence | Interest | Cách quản lý |
|---|---|---|---|
| Manage Closely | Cao | Cao | Tham gia thường xuyên, trao đổi trực tiếp và quản lý chặt chẽ |
| Keep Satisfied | Cao | Thấp | Cập nhật các vấn đề quan trọng và đảm bảo Stakeholder hài lòng |
| Keep Informed | Thấp | Cao | Thường xuyên cung cấp thông tin và tiếp nhận phản hồi |
| Monitor | Thấp | Thấp | Theo dõi và cập nhật khi cần thiết |

---

## 2.3. Stakeholder Matrix của CAB System

```mermaid
quadrantChart
    title Stakeholder Power / Interest Matrix - CAB System

    x-axis Low Interest --> High Interest
    y-axis Low Power / Influence --> High Power / Influence

    quadrant-1 Manage Closely
    quadrant-2 Keep Satisfied
    quadrant-3 Monitor
    quadrant-4 Keep Informed

    "Business Sponsor / Ban giám đốc": [0.85, 0.95]
    "Business Owner": [0.90, 0.90]
    "Project Manager": [0.80, 0.85]

    "Khách hàng": [0.90, 0.55]
    "Tài xế": [0.85, 0.50]
    "Nhân viên vận hành": [0.85, 0.65]
    "BA": [0.85, 0.75]

    "Development Team": [0.75, 0.60]
    "QA / Tester": [0.70, 0.45]
    "Customer Support": [0.70, 0.40]

    "Payment Provider": [0.50, 0.75]
    "Notification Provider": [0.40, 0.55]
    "Finance / Accounting": [0.55, 0.45]
    "System Administrator": [0.55, 0.50]
