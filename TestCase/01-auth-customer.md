# 01 – Auth & Customer Test Cases

**API Specification:** `01-auth-customer-api.yaml`

## Ngữ cảnh kiểm thử

### CTX01 – Đăng ký và đăng nhập khách hàng

Khách hàng mới tạo tài khoản; sau đó đăng nhập để sử dụng các chức năng cần xác thực. Có thể xảy ra dữ liệu thiếu/sai định dạng, tài khoản trùng, mật khẩu sai hoặc thiếu token.

### CTX02 – Quản lý hồ sơ và lịch sử khách hàng

Khách hàng đã đăng nhập xem/cập nhật hồ sơ và xem lịch sử chuyến của chính mình. Có thể xảy ra token không hợp lệ, dữ liệu cập nhật sai hoặc phân trang không hợp lệ.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC01 | CTX01 | Positive | FR01 | AC01–AC04 | POST /auth/register | Email/phone chưa tồn tại | {"fullName":"Nguyen Van A","phone":"+84901234567","email":"a@example.com","password":"StrongPwd1"} | 201 | Trả object có `id` UUID; tài khoản được tạo. |
| TC02 | CTX01 | Negative | FR01 | AC01, AC02 | POST /auth/register | Không có | Thiếu `email` hoặc `password` | 422 | `Error` với code/message validation; không tạo tài khoản. |
| TC03 | CTX01 | Negative | FR01 | AC02 | POST /auth/register | Không có | `email:"abc"` hoặc `phone:"123"` hoặc password < 8 ký tự | 422 | Từ chối dữ liệu sai schema; không tạo tài khoản. |
| TC04 | CTX01 | Negative | FR01 | AC03 | POST /auth/register | Email/phone đã tồn tại | Đăng ký lại thông tin đã dùng | 409 | Trả conflict; không tạo tài khoản trùng. |
| TC05 | CTX01 | Positive | FR02 | AC05–AC07 | POST /auth/login | Tài khoản ACTIVE tồn tại | {"identifier":"a@example.com","password":"StrongPwd1"} | 200 | Trả `accessToken`, `tokenType: Bearer`, `role` đúng. |
| TC06 | CTX01 | Negative | FR02 | AC06 | POST /auth/login | Tài khoản tồn tại | Mật khẩu sai | 401 | Không cấp accessToken; trả lỗi xác thực. |
| TC07 | CTX01 | Negative | FR02 | AC05–AC06 | POST /auth/login | Không có | Thiếu identifier/password | 422 | Validation error. |
| TC08 | CTX02 | Positive | FR03 | AC08, AC10 | GET /customers/me | Customer đã đăng nhập | Bearer `<valid_token>` | 200 | Trả đúng profile của customer hiện tại. |
| TC09 | CTX02 | Negative | FR03 | AC08 | GET /customers/me | Không có token hợp lệ | Bearer `<invalid_or_expired_token>` | 401 | Không trả dữ liệu hồ sơ. |
| TC10 | CTX02 | Positive | FR03 | AC08–AC10 | PATCH /customers/me | Customer đã đăng nhập | Bearer `<valid_token>`; body {"fullName":"Nguyen Van B"} | 200 | Profile trả về có `fullName` mới. |
| TC11 | CTX02 | Negative | FR03 | AC09 | PATCH /customers/me | Customer đã đăng nhập | Bearer `<valid_token>`; body {"email":"invalid-email"} | 422 | Không cập nhật dữ liệu sai định dạng. |
| TC12 | CTX02 | Negative | FR03 | AC09 | PATCH /customers/me | Customer đã đăng nhập | Bearer `<valid_token>`; body email/phone đã thuộc customer khác | 409 | Không ghi đè thông tin trùng. |
| TC13 | CTX02 | Positive | FR04 | AC28–AC30 | GET /customers/me/rides | Customer có lịch sử chuyến | Bearer `<valid_token>`; query `page=1&size=20` | 200 | Chỉ trả danh sách chuyến của customer đang đăng nhập. |
| TC14 | CTX02 | Positive | FR04 | AC29 | GET /customers/me/rides | Customer chưa có chuyến | Bearer `<valid_token>` | 200 | Trả danh sách rỗng, không báo lỗi. |
| TC15 | CTX02 | Negative | FR04 | AC28 | GET /customers/me/rides | Không có token hợp lệ | Bearer `<invalid_or_expired_token>` | 401 | Không cho xem lịch sử. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
