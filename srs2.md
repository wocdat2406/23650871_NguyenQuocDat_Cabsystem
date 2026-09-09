# Bước 1: Phân tích yêu cầu sơ khởi của khách hàng

## 1.1. Business Context

### Thông tin dự án

- **Khách hàng:** Công ty ABC.
- **Lĩnh vực:** Cung cấp dịch vụ đặt xe trực tuyến.
- **Dự án:** CAB System – Nền tảng đặt xe.
- **Thời gian xây dựng và triển khai:** 7 tuần.
- **Mục tiêu tổng quát:** Xây dựng nền tảng đặt xe có khả năng phục vụ số lượng lớn khách hàng và tài xế, đồng thời dễ mở rộng trong tương lai.

### Hệ thống hiện tại

Khách hàng hiện có thể đặt xe bằng:
- Liên hệ tổng đài.
- Sử dụng một ứng dụng đặt xe đơn giản.

Việc phân công tài xế hiện vẫn chủ yếu được thực hiện thủ công và các thông tin về chuyến đi, thanh toán, vận hành chưa được quản lý hiệu quả trên một hệ thống tập trung.

### Nhóm người dùng chính

Hệ thống có 3 nhóm người dùng chính:

| Nhóm người dùng | Nhu cầu chính |
|---|---|
| Khách hàng | Đặt xe, theo dõi chuyến đi, thanh toán, xem lịch sử và đánh giá tài xế |
| Tài xế | Nhận/từ chối chuyến, cập nhật vị trí và trạng thái chuyến đi |
| Nhân viên vận hành | Quản lý khách hàng, tài xế, phương tiện, chuyến đi và hỗ trợ xử lý sự cố |

### Quy trình nghiệp vụ chính

Quy trình chính của CAB System được xác định sơ bộ:

**Đặt xe → Tìm tài xế → Phân công tài xế → Thực hiện chuyến → Hoàn thành chuyến → Tính cước → Thanh toán → Đánh giá**

Ngoài ra, hệ thống cần hỗ trợ:
- Theo dõi trạng thái chuyến đi.
- Thông báo cho khách hàng và tài xế.
- Quản lý hoạt động vận hành.
- Báo cáo hoạt động kinh doanh.

---

## 1.2. Business Problem

Từ yêu cầu của khách hàng, các vấn đề nghiệp vụ chính được xác định:

### BP01 – Phân công tài xế còn thủ công
Việc phân công tài xế chủ yếu được thực hiện thủ công, gây khó khăn khi số lượng yêu cầu đặt xe tăng.

### BP02 – Khó theo dõi trạng thái chuyến đi
Khách hàng khó biết trạng thái yêu cầu đặt xe, tài xế đã nhận chuyến, thời gian tài xế đến và trạng thái hiện tại của chuyến.

### BP03 – Quản lý thanh toán chưa tập trung
Thông tin thanh toán chưa được quản lý tập trung, gây khó khăn cho việc theo dõi giao dịch và doanh thu.

### BP04 – Khó khăn trong công tác vận hành
Nhân viên vận hành gặp khó khăn trong việc theo dõi tài xế, chuyến đi, xử lý sự cố và tra cứu lịch sử giao dịch.

### BP05 – Khả năng mở rộng còn hạn chế
Hệ thống hiện tại khó đáp ứng khi số lượng khách hàng, tài xế và yêu cầu đặt xe tăng cao.

### BP06 – Khả năng phát triển hệ thống còn hạn chế
Doanh nghiệp cần bổ sung dịch vụ, phương thức thanh toán và kênh thông báo mới trong tương lai mà không phải xây dựng lại toàn bộ hệ thống.

---

## 1.3. Các vấn đề BA cần làm rõ

Một số vấn đề nghiệp vụ khách hàng chưa xác định cụ thể:

- Cách tính cước chuyến đi.
- Tiêu chí ưu tiên và lựa chọn tài xế.
- Thời gian tài xế phải phản hồi yêu cầu chuyến.
- Chính sách hủy chuyến.
- Cách xử lý khi mất kết nối mạng.
- Cách xử lý thanh toán thất bại.
- Thời gian lưu trữ dữ liệu.

Các vấn đề này cần được BA xác nhận với stakeholder trước khi chuyển thành yêu cầu chi tiết.

---

## 1.4. Kết luận

**Business Context:** Công ty ABC cần xây dựng CAB System để quản lý toàn bộ quy trình đặt xe từ khi khách hàng tạo yêu cầu đến khi chuyến đi hoàn thành, thanh toán và đánh giá.

**Business Problem:** Hệ thống hiện tại còn phụ thuộc vào phân công tài xế thủ công, khó theo dõi chuyến đi, quản lý thanh toán chưa tập trung, vận hành khó khăn và khả năng mở rộng còn hạn chế.

# Bước 2: Xác định Stakeholders

## 2.1. Danh sách Stakeholders

Dựa trên Business Context và Business Problem, các stakeholder chính của CAB System được xác định như sau:

| Stakeholder | Vai trò |
|---|---|
| **Khách hàng (Customer)** | Đặt xe, theo dõi chuyến đi, thanh toán, xem lịch sử chuyến và đánh giá tài xế. |
| **Tài xế (Driver)** | Nhận hoặc từ chối chuyến, cập nhật vị trí, trạng thái hoạt động và thực hiện chuyến đi. |
| **Nhân viên vận hành (Operation Staff)** | Quản lý khách hàng, tài xế, phương tiện, chuyến đi và hỗ trợ xử lý các trường hợp gặp sự cố. |
| **Ban lãnh đạo (Management)** | Đưa ra yêu cầu, theo dõi báo cáo và đánh giá hiệu quả hoạt động của hệ thống. |
| **Nhà cung cấp thanh toán (Payment Provider)** | Xử lý các giao dịch thanh toán điện tử của khách hàng. |
| **Nhà cung cấp thông báo (Notification Provider)** | Hỗ trợ gửi thông báo đến khách hàng và tài xế qua các kênh thông báo. |

---

## 2.2. Stakeholder Matrix

Stakeholder Matrix giúp xác định **mức độ ảnh hưởng (Power)** và **mức độ quan tâm (Interest)** của các stakeholder đối với CAB System.

```mermaid
quadrantChart
    title Stakeholder Matrix - CAB System
    x-axis Low Interest --> High Interest
    y-axis Low Power --> High Power

    quadrant-1 Manage Closely
    quadrant-2 Keep Satisfied
    quadrant-3 Monitor
    quadrant-4 Keep Informed

    Management: [0.90, 0.95]
    Operation Staff: [0.85, 0.80]
    Customer: [0.90, 0.65]
    Driver: [0.85, 0.60]
    Payment Provider: [0.55, 0.50]
    Notification Provider: [0.40, 0.35]
```

### Phân nhóm Stakeholders

- **Manage Closely:** Ban lãnh đạo, Nhân viên vận hành.
- **Keep Informed:** Khách hàng, Tài xế.
- **Monitor / Keep Satisfied:** Nhà cung cấp thanh toán và Nhà cung cấp thông báo tùy theo mức độ tích hợp và phụ thuộc của hệ thống.

# Bước 3: Xác định Business Goal

Business Goal được xác định dựa trên các vấn đề nghiệp vụ của hệ thống hiện tại và kỳ vọng của Công ty ABC.

### BG01 – Tự động tìm và phân công tài xế
- **Mục tiêu:** Giảm thời gian tìm tài xế và hạn chế việc phân công tài xế thủ công.
- **Kết quả mong muốn:** Hệ thống có thể tự động tìm tài xế phù hợp và gần khách hàng.

### BG02 – Hỗ trợ thanh toán
- **Mục tiêu:** Tạo sự thuận tiện cho khách hàng khi thanh toán và quản lý giao dịch tập trung.
- **Kết quả mong muốn:** Cho phép thanh toán bằng tiền mặt và thanh toán điện tử.

### BG03 – Theo dõi trạng thái chuyến đi
- **Mục tiêu:** Giúp khách hàng dễ dàng theo dõi quá trình thực hiện chuyến đi.
- **Kết quả mong muốn:** Khách hàng biết được trạng thái tìm tài xế, tài xế nhận chuyến, thời gian dự kiến đến và trạng thái chuyến đi.

### BG04 – Nâng cao hiệu quả vận hành
- **Mục tiêu:** Giúp nhân viên vận hành quản lý và theo dõi hoạt động tập trung.
- **Kết quả mong muốn:** Nhân viên có thể theo dõi tài xế, chuyến đi và hỗ trợ xử lý các trường hợp gặp sự cố.

### BG05 – Mở rộng khả năng phục vụ
- **Mục tiêu:** Đáp ứng số lượng khách hàng, tài xế và yêu cầu đặt xe tăng cao.
- **Kết quả mong muốn:** Hệ thống có khả năng mở rộng các thành phần khi nhu cầu sử dụng tăng.

### BG06 – Hỗ trợ quản lý và ra quyết định
- **Mục tiêu:** Giúp ban lãnh đạo theo dõi hiệu quả hoạt động kinh doanh.
- **Kết quả mong muốn:** Cung cấp các báo cáo về số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả tài xế.

### BG07 – Đảm bảo an toàn thông tin
- **Mục tiêu:** Bảo vệ dữ liệu người dùng và các hoạt động quan trọng của hệ thống.
- **Kết quả mong muốn:** Kiểm soát quyền truy cập, bảo vệ dữ liệu và lưu vết các thao tác quan trọng.

### BG08 – Hỗ trợ phát triển hệ thống trong tương lai
- **Mục tiêu:** Giảm ảnh hưởng khi doanh nghiệp bổ sung hoặc thay đổi chức năng.
- **Kết quả mong muốn:** Có thể bổ sung loại dịch vụ, phương thức thanh toán và kênh thông báo mới mà không phải xây dựng lại toàn bộ hệ thống.

# Bước 4: Xác định phạm vi yêu cầu

## 4.1. In Scope – Phạm vi cần thực hiện

Dưới góc độ MVB, CAB System cần tập trung vào các module cơ bản để hỗ trợ đầy đủ quy trình đặt xe.

| Module | Phạm vi chính |
|---|---|
| **Quản lý khách hàng** | Đăng ký, đăng nhập, cập nhật thông tin cá nhân, xem lịch sử chuyến đi. |
| **Quản lý tài xế** | Quản lý hồ sơ tài xế, trạng thái hoạt động, thông tin phương tiện. |
| **Quản lý đặt xe** | Nhập điểm đón, điểm đến, chọn loại xe và tạo yêu cầu đặt xe. |
| **Tìm và phân công tài xế** | Tự động tìm tài xế phù hợp, xử lý trường hợp tài xế từ chối hoặc không phản hồi. |
| **Quản lý chuyến đi** | Theo dõi và cập nhật trạng thái chuyến đi từ lúc nhận chuyến đến khi hoàn thành. |
| **Tính cước và thanh toán** | Tính số tiền chuyến đi, hỗ trợ thanh toán tiền mặt và thanh toán điện tử. |
| **Thông báo** | Thông báo các trạng thái quan trọng của chuyến đi cho khách hàng và tài xế. |
| **Đánh giá tài xế** | Cho phép khách hàng đánh giá tài xế sau khi chuyến đi hoàn thành. |
| **Quản lý vận hành** | Quản lý khách hàng, tài xế, phương tiện, chuyến đi và hỗ trợ xử lý sự cố cơ bản. |
| **Báo cáo cơ bản** | Thống kê số lượng chuyến, doanh thu, tỷ lệ hoàn thành và tỷ lệ hủy chuyến. |

---

## 4.2. Out of Scope – Ngoài phạm vi MVB

Trong phiên bản MVB, chưa thực hiện các chức năng sau:

- Nhiều loại dịch vụ xe nâng cao ngoài các loại xe cơ bản.
- Chương trình khuyến mãi, voucher và loyalty.
- Ví điện tử riêng của CAB System.
- Nhiều nhà cung cấp thanh toán cùng lúc.
- Nhiều kênh thông báo nâng cao.
- Thuật toán AI/ML để dự đoán nhu cầu hoặc tối ưu phân công tài xế.
- Hệ thống định giá động theo thời gian thực.
- Báo cáo và phân tích nâng cao.
- Hệ thống quản lý khiếu nại, chăm sóc khách hàng chuyên sâu.
- Các chức năng mở rộng chưa cần thiết cho quy trình đặt xe cơ bản.

---

## 4.3. Phạm vi MVB cốt lõi

MVB tập trung vào quy trình chính:

**Khách hàng đặt xe → Hệ thống tìm tài xế → Tài xế nhận chuyến → Thực hiện chuyến → Hoàn thành → Tính cước → Thanh toán → Đánh giá**

# Bước 5: Xác định Business Requirement

Sau khi xác định phạm vi hệ thống và xác nhận lại với khách hàng, các yêu cầu trong phạm vi MVB được chuyển thành **Business Requirement (BR)**.

## 5.1. Danh sách Business Requirement

| Mã BR | Tên Business Requirement | Diễn giải |
|---|---|---|
| **BR01** | Quản lý khách hàng | Hệ thống cho phép khách hàng đăng ký tài khoản, đăng nhập, cập nhật thông tin cá nhân và xem lịch sử chuyến đi. |
| **BR02** | Quản lý tài xế | Hệ thống cho phép tạo tài khoản tài xế, cập nhật hồ sơ, thông tin phương tiện và trạng thái hoạt động. |
| **BR03** | Đặt chuyến | Khách hàng có thể nhập điểm đón, điểm đến, lựa chọn loại xe và gửi yêu cầu đặt chuyến. |
| **BR04** | Tìm và phân công tài xế | Hệ thống tự động tìm tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và các tiêu chí vận hành để phân công chuyến. |
| **BR05** | Xử lý yêu cầu nhận chuyến | Tài xế có thể chấp nhận hoặc từ chối chuyến. Nếu tài xế từ chối hoặc không phản hồi, hệ thống tiếp tục tìm tài xế khác mà khách hàng không cần tạo lại yêu cầu. |
| **BR06** | Quản lý chuyến đi | Hệ thống quản lý quá trình thực hiện chuyến và cho phép tài xế cập nhật các trạng thái: đã đến điểm đón, đã đón khách, đang di chuyển và hoàn thành chuyến. |
| **BR07** | Theo dõi chuyến đi | Khách hàng có thể theo dõi trạng thái tìm tài xế, thông tin tài xế nhận chuyến, thời gian dự kiến tài xế đến và trạng thái hiện tại của chuyến. |
| **BR08** | Tính cước | Sau khi chuyến hoàn thành, hệ thống xác định số tiền khách hàng phải trả dựa trên loại dịch vụ và thông tin chuyến đi. |
| **BR09** | Thanh toán | Hệ thống hỗ trợ thanh toán bằng tiền mặt và thanh toán điện tử, đồng thời ghi nhận kết quả thanh toán của chuyến đi. |
| **BR10** | Thông báo | Hệ thống gửi thông báo cho khách hàng và tài xế về các sự kiện quan trọng liên quan đến yêu cầu đặt xe, chuyến đi và thanh toán. |
| **BR11** | Quản lý lịch sử chuyến đi | Hệ thống lưu trữ và cho phép tra cứu lịch sử chuyến đi và các thông tin giao dịch liên quan. |
| **BR12** | Đánh giá tài xế | Khách hàng có thể đánh giá tài xế sau khi chuyến đi hoàn thành. |
| **BR13** | Quản lý vận hành | Nhân viên vận hành có thể quản lý khách hàng, tài xế, phương tiện, theo dõi chuyến đi và hỗ trợ xử lý các chuyến gặp sự cố. |
| **BR14** | Phân quyền quản trị | Hệ thống kiểm soát quyền truy cập đối với các chức năng quản trị để hạn chế nhân viên thực hiện các thao tác nhạy cảm không được phép. |
| **BR15** | Báo cáo hoạt động | Hệ thống cung cấp báo cáo về số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả hoạt động của tài xế. |

---

## 5.2. Mối quan hệ giữa Business Goal và Business Requirement

| Business Goal | Business Requirement liên quan |
|---|---|
| **BG01 – Tự động tìm và phân công tài xế** | BR03, BR04, BR05 |
| **BG02 – Hỗ trợ thanh toán** | BR08, BR09 |
| **BG03 – Theo dõi trạng thái chuyến đi** | BR06, BR07, BR10 |
| **BG04 – Nâng cao hiệu quả vận hành** | BR02, BR11, BR13, BR14 |
| **BG05 – Mở rộng khả năng phục vụ** | Các BR của hệ thống cần được thiết kế để hỗ trợ khả năng mở rộng |
| **BG06 – Hỗ trợ quản lý và ra quyết định** | BR11, BR15 |
| **BG07 – Đảm bảo an toàn thông tin** | BR01, BR02, BR14 |
| **BG08 – Hỗ trợ phát triển hệ thống trong tương lai** | Các BR cần được thiết kế theo hướng dễ mở rộng và thay đổi |

---

## 5.3. Quy trình nghiệp vụ chính

Các Business Requirement trên hỗ trợ quy trình nghiệp vụ cốt lõi của CAB System:

```mermaid
flowchart LR
    A[Khách hàng đặt chuyến] --> B[Hệ thống tìm tài xế]
    B --> C[Tài xế nhận chuyến]
    C --> D[Thực hiện chuyến]
    D --> E[Hoàn thành chuyến]
    E --> F[Tính cước]
    F --> G[Thanh toán]
    G --> H[Đánh giá tài xế]
```

---

## 5.4. Kết luận

Các Business Requirement trên xác định những yêu cầu nghiệp vụ chính mà **CAB System phiên bản MVB** cần đáp ứng.

Các yêu cầu tập trung vào quy trình chính:

**Quản lý khách hàng → Đặt chuyến → Tìm và phân công tài xế → Thực hiện chuyến → Theo dõi chuyến → Tính cước → Thanh toán → Đánh giá**

Ngoài ra, hệ thống hỗ trợ các hoạt động cần thiết như **quản lý tài xế, thông báo, quản lý vận hành, phân quyền và báo cáo**.

Các yêu cầu chi tiết hơn về chức năng, quy tắc nghiệp vụ, yêu cầu phi chức năng và các trường hợp ngoại lệ sẽ được phân tích ở các bước tiếp theo.

# Bước 6: Xây dựng Business Process

Business Process mô tả luồng nghiệp vụ chính của CAB System từ khi khách hàng đặt chuyến cho đến khi chuyến đi hoàn thành.

## 6.1. BP01 – Quy trình đặt chuyến và tìm tài xế

### Mô tả

1. Khách hàng nhập điểm đón.
2. Khách hàng nhập điểm đến.
3. Khách hàng chọn loại xe.
4. Khách hàng gửi yêu cầu đặt chuyến.
5. Hệ thống tiếp nhận và xác nhận yêu cầu.
6. Hệ thống tìm tài xế phù hợp dựa trên vị trí và trạng thái sẵn sàng.
7. Hệ thống gửi yêu cầu chuyến cho tài xế.
8. Tài xế chấp nhận hoặc từ chối chuyến.
9. Nếu tài xế chấp nhận, hệ thống phân công tài xế và thông báo cho khách hàng.
10. Nếu tài xế từ chối hoặc không phản hồi, hệ thống tiếp tục tìm và gửi yêu cầu cho tài xế khác.
11. Nếu không tìm được tài xế phù hợp, hệ thống thông báo cho khách hàng.

```mermaid
flowchart TD
    A[Khách hàng nhập điểm đón] --> B[Nhập điểm đến]
    B --> C[Chọn loại xe]
    C --> D[Gửi yêu cầu đặt chuyến]
    D --> E[Hệ thống xác nhận yêu cầu]
    E --> F[Hệ thống tìm tài xế phù hợp]
    F --> G{Tìm thấy tài xế?}

    G -->|Không| H[Thông báo không tìm được tài xế]
    G -->|Có| I[Gửi yêu cầu cho tài xế]

    I --> J{Tài xế chấp nhận?}
    J -->|Có| K[Phân công tài xế]
    K --> L[Thông báo cho khách hàng]

    J -->|Không / Không phản hồi| M[Tiếp tục tìm tài xế khác]
    M --> F
```

---

## 6.2. BP02 – Quy trình thực hiện chuyến đi

### Mô tả

1. Tài xế chấp nhận chuyến.
2. Hệ thống thông báo thông tin tài xế cho khách hàng.
3. Tài xế di chuyển đến điểm đón.
4. Tài xế cập nhật trạng thái đã đến điểm đón.
5. Hệ thống thông báo cho khách hàng.
6. Tài xế đón khách và cập nhật trạng thái đã đón khách.
7. Tài xế bắt đầu thực hiện chuyến đi.
8. Tài xế cập nhật trạng thái đang di chuyển.
9. Tài xế đến điểm đến.
10. Tài xế cập nhật trạng thái hoàn thành chuyến.
11. Hệ thống ghi nhận chuyến đi đã hoàn thành.

```mermaid
flowchart TD
    A[Tài xế chấp nhận chuyến] --> B[Thông báo cho khách hàng]
    B --> C[Tài xế di chuyển đến điểm đón]
    C --> D[Cập nhật: Đã đến điểm đón]
    D --> E[Thông báo khách hàng]
    E --> F[Đón khách]
    F --> G[Cập nhật: Đã đón khách]
    G --> H[Bắt đầu chuyến đi]
    H --> I[Cập nhật: Đang di chuyển]
    I --> J[Đến điểm đến]
    J --> K[Cập nhật: Hoàn thành]
    K --> L[Hệ thống ghi nhận chuyến hoàn thành]
```

---

## 6.3. BP03 – Quy trình tính cước và thanh toán

### Mô tả

1. Chuyến đi được hoàn thành.
2. Hệ thống tính số tiền khách hàng phải trả.
3. Hệ thống hiển thị số tiền cho khách hàng.
4. Khách hàng lựa chọn phương thức thanh toán.
5. Nếu thanh toán bằng tiền mặt, hệ thống ghi nhận phương thức thanh toán.
6. Nếu thanh toán điện tử, hệ thống gửi yêu cầu đến nhà cung cấp thanh toán.
7. Nhà cung cấp thanh toán xử lý giao dịch.
8. Nếu thanh toán thành công, hệ thống ghi nhận kết quả.
9. Nếu thanh toán thất bại, hệ thống thông báo cho khách hàng và cho phép xử lý lại theo chính sách của doanh nghiệp.

```mermaid
flowchart TD
    A[Chuyến đi hoàn thành] --> B[Hệ thống tính cước]
    B --> C[Hiển thị số tiền]
    C --> D{Phương thức thanh toán}

    D -->|Tiền mặt| E[Ghi nhận thanh toán tiền mặt]
    E --> J[Hoàn tất thanh toán]

    D -->|Điện tử| F[Gửi yêu cầu thanh toán]
    F --> G[Nhà cung cấp xử lý]
    G --> H{Thanh toán thành công?}

    H -->|Có| I[Ghi nhận thanh toán thành công]
    I --> J

    H -->|Không| K[Thông báo thanh toán thất bại]
    K --> L[Cho phép xử lý lại]
```

---

## 6.4. BP04 – Quy trình đánh giá sau chuyến đi

### Mô tả

1. Chuyến đi đã hoàn thành.
2. Hệ thống cho phép khách hàng đánh giá tài xế.
3. Khách hàng nhập đánh giá.
4. Khách hàng gửi đánh giá.
5. Hệ thống lưu đánh giá của chuyến đi.

```mermaid
flowchart TD
    A[Chuyến đi hoàn thành] --> B[Cho phép đánh giá tài xế]
    B --> C[Khách hàng nhập đánh giá]
    C --> D[Gửi đánh giá]
    D --> E[Hệ thống lưu đánh giá]
```

---

## 6.5. BP05 – Quy trình quản lý và theo dõi vận hành

### Mô tả

1. Nhân viên vận hành đăng nhập hệ thống quản trị.
2. Nhân viên xem danh sách các chuyến đi.
3. Nhân viên theo dõi trạng thái chuyến và tài xế.
4. Nếu chuyến hoạt động bình thường, hệ thống tiếp tục ghi nhận trạng thái.
5. Nếu chuyến gặp sự cố, nhân viên kiểm tra thông tin.
6. Nhân viên thực hiện xử lý theo quyền được cấp.
7. Hệ thống lưu lại thao tác quan trọng.

```mermaid
flowchart TD
    A[Nhân viên vận hành đăng nhập] --> B[Xem danh sách chuyến đi]
    B --> C[Theo dõi trạng thái chuyến và tài xế]
    C --> D{Có sự cố?}

    D -->|Không| E[Tiếp tục theo dõi]
    E --> C

    D -->|Có| F[Kiểm tra thông tin sự cố]
    F --> G[Xử lý theo quyền được cấp]
    G --> H[Hệ thống lưu thao tác]
```

---

## 6.6. Business Process tổng quát

Quy trình nghiệp vụ chính của CAB System:

```mermaid
flowchart LR
    A[Khách hàng đặt chuyến] --> B[Tìm tài xế]
    B --> C{Tài xế nhận?}

    C -->|Không| B
    C -->|Có| D[Phân công tài xế]

    D --> E[Đón khách]
    E --> F[Thực hiện chuyến]
    F --> G[Hoàn thành chuyến]
    G --> H[Tính cước]
    H --> I[Thanh toán]
    I --> J[Đánh giá tài xế]
```

## 6.7. Kết luận

Các Business Process chính của CAB System gồm:

- **BP01:** Đặt chuyến và tìm tài xế.
- **BP02:** Thực hiện chuyến đi.
- **BP03:** Tính cước và thanh toán.
- **BP04:** Đánh giá sau chuyến đi.
- **BP05:** Quản lý và theo dõi vận hành.

Các quy trình trên bao phủ luồng nghiệp vụ cốt lõi của phiên bản MVB từ khi khách hàng tạo yêu cầu đặt xe đến khi chuyến đi được hoàn thành, thanh toán và đánh giá.
