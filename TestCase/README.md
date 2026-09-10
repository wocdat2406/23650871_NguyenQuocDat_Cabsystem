# Test Case – CAB System

Bộ Test Case được xây dựng từ **Business Process → FR → UC → AC → API Specification**. Mỗi Test Case đều chỉ rõ ngữ cảnh, loại kiểm thử, API, input và output kỳ vọng.

## Quy ước

- `CTXxx`: Test Context – Ngữ cảnh kiểm thử.
- `TCxx`: Test Case.
- **Positive**: Luồng hợp lệ, mong đợi chức năng thành công.
- **Negative**: Luồng không hợp lệ hoặc sai quy trình nghiệp vụ, hệ thống phải từ chối/xử lý đúng.
- HTTP status và response được lấy theo OpenAPI Specification hiện tại.
- Các giá trị UUID/token bên dưới là dữ liệu mẫu để mô tả test, khi chạy thực tế phải thay bằng dữ liệu test hợp lệ.

## Ngữ cảnh kiểm thử

| Mã | Ngữ cảnh | Luồng chính | Tình huống âm cần kiểm thử |
|---|---|---|---|
| CTX01 | Đăng ký và đăng nhập khách hàng | Khách hàng mới tạo tài khoản; sau đó đăng nhập để sử dụng các chức năng cần xác thực. | Có thể xảy ra dữ liệu thiếu/sai định dạng, tài khoản trùng, mật khẩu sai hoặc thiếu token. |
| CTX02 | Quản lý hồ sơ và lịch sử khách hàng | Khách hàng đã đăng nhập xem/cập nhật hồ sơ và xem lịch sử chuyến của chính mình. | Có thể xảy ra token không hợp lệ, dữ liệu cập nhật sai hoặc phân trang không hợp lệ. |
| CTX03 | Khởi tạo chuyến đi | Khách hàng đã đăng nhập nhập điểm đón, điểm đến, loại xe và gửi yêu cầu đặt chuyến. | Có thể thiếu tọa độ/địa chỉ, tọa độ ngoài phạm vi, loại xe không hỗ trợ hoặc không xác thực. |
| CTX04 | Tìm và phân công tài xế | Sau khi chuyến được tạo, hệ thống tìm tài xế gần, AVAILABLE và có loại xe phù hợp; gửi offer cho tài xế. | Tài xế có thể từ chối, không phản hồi, offer hết hạn hoặc không còn tài xế phù hợp. |
| CTX05 | Tài xế quản lý trạng thái và vị trí | Tài xế đã đăng nhập cập nhật hồ sơ, phương tiện, trạng thái sẵn sàng và vị trí. | Có thể sai loại xe, trùng biển số, trạng thái không hợp lệ hoặc tọa độ ngoài phạm vi. |
| CTX06 | Theo dõi và thực hiện chuyến | Sau khi tài xế được phân công, khách hàng theo dõi ETA/trạng thái; tài xế cập nhật ARRIVED → PICKED_UP → IN_PROGRESS → COMPLETED. | Có thể truy cập sai người, sai rideId hoặc cập nhật trạng thái sai thứ tự nghiệp vụ. |
| CTX07 | Tính cước và thanh toán | Chỉ sau khi chuyến COMPLETED, hệ thống trả cước và khách hàng chọn CASH hoặc ELECTRONIC. | Có thể yêu cầu cước quá sớm, payment token thiếu, provider thất bại hoặc retry sai trạng thái. |
| CTX08 | Thông báo sự kiện | Hệ thống gửi thông báo khi booking nhận, driver nhận, driver đến, trip hoàn thành, payment result hoặc ride offer. | Notification Provider có thể thất bại; lỗi thông báo không được làm gián đoạn luồng chuyến. |
| CTX09 | Đánh giá tài xế | Khách hàng chỉ đánh giá tài xế của chuyến đã hoàn thành. | Có thể đánh giá trước khi hoàn thành, score ngoài 1–5, đánh giá trùng hoặc truy cập chuyến người khác. |
| CTX10 | Vận hành và phân quyền | Operation Staff tìm kiếm khách hàng/tài xế/xe/chuyến/giao dịch, hỗ trợ chuyến và phân quyền theo quyền được cấp. | Người không có quyền phải bị từ chối; dữ liệu/ride/staff không tồn tại phải trả lỗi phù hợp. |
| CTX11 | Báo cáo quản lý | Management/nhân sự có quyền báo cáo truy vấn số chuyến, doanh thu, tỷ lệ và hiệu quả tài xế theo khoảng ngày. | Có thể thiếu quyền, thiếu ngày, from > to hoặc khoảng ngày không có dữ liệu. |

## Cấu trúc thư mục

| File | Phạm vi |
|---|---|
| `01-auth-customer-testcases.md` | FR01–FR04 |
| `02-driver-testcases.md` | FR05–FR09 |
| `03-ride-booking-matching-testcases.md` | FR10–FR25 |
| `04-trip-tracking-testcases.md` | FR26–FR33 |
| `05-payment-testcases.md` | FR34–FR40 |
| `06-notification-testcases.md` | FR41–FR46 |
| `07-rating-testcases.md` | FR47–FR48 |
| `08-operations-testcases.md` | FR49–FR56 |
| `09-reporting-testcases.md` | FR57–FR60 |

## Nguyên tắc nghiệm thu

Một FR được xem là đã được kiểm thử khi có ít nhất một Test Case liên kết tới FR/AC tương ứng và kết quả thực tế khớp **HTTP Status + Expected Output + Business Rule**. Không chỉ chạy happy path; các nhánh từ chối, timeout, thiếu quyền, sai trạng thái và dữ liệu không hợp lệ phải được kiểm thử.
