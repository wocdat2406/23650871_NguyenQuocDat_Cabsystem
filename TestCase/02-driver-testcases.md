# 02 – Driver Test Cases

**API Specification:** `02-driver-api.yaml`

## Ngữ cảnh kiểm thử

### CTX05 – Tài xế quản lý trạng thái và vị trí

Tài xế đã đăng nhập cập nhật hồ sơ, phương tiện, trạng thái sẵn sàng và vị trí. Có thể sai loại xe, trùng biển số, trạng thái không hợp lệ hoặc tọa độ ngoài phạm vi.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC16 | CTX05 | Positive | FR05 | AC62–AC64 | POST /drivers | Operation Staff có quyền tạo driver | Bearer `<valid_token>`; body {"fullName":"Tran Tai Xe","phone":"0909999999","email":"driver@example.com"} | 201 | Trả `id` của driver mới. |
| TC17 | CTX05 | Negative | FR05 | AC65 | POST /drivers | Người dùng không có quyền | Bearer `<valid_token>` của customer/driver | 403 | Không tạo driver. |
| TC18 | CTX05 | Negative | FR05 | AC64 | POST /drivers | Operation Staff có quyền | Email sai định dạng | 422 | Validation error; không tạo driver. |
| TC19 | CTX05 | Positive | FR06 | AC41–AC42 | GET /drivers/me | Driver đã đăng nhập | Bearer `<valid_token>` | 200 | Trả đúng hồ sơ driver hiện tại. |
| TC20 | CTX05 | Positive | FR06 | AC41, AC43–AC44 | PATCH /drivers/me | Driver đã đăng nhập | Bearer `<valid_token>`; body {"fullName":"Tran Driver New"} | 200 | Thông tin mới được lưu và trả về. |
| TC21 | CTX05 | Negative | FR06 | AC41 | PATCH /drivers/me | Token không hợp lệ | Bearer `<invalid_or_expired_token>`; body hợp lệ | 401 | Không cập nhật hồ sơ. |
| TC22 | CTX05 | Positive | FR07 | AC42 | GET /drivers/me/vehicle | Driver có vehicle | Bearer `<valid_token>` | 200 | Trả vehicle liên kết đúng driver. |
| TC23 | CTX05 | Negative | FR07 | AC42 | GET /drivers/me/vehicle | Driver chưa có vehicle | Bearer `<valid_token>` | 404 | Trả not found. |
| TC24 | CTX05 | Positive | FR07 | AC41, AC43–AC44, AC68 | PUT /drivers/me/vehicle | Driver đã đăng nhập | Bearer `<valid_token>`; body {"vehicleType":"CAR","licensePlate":"51A-12345","model":"Vios"} | 200 | Vehicle được tạo/cập nhật và gắn đúng driver. |
| TC25 | CTX05 | Negative | FR07 | AC43 | PUT /drivers/me/vehicle | Driver đã đăng nhập | Bearer `<valid_token>`; `vehicleType:"TRUCK"` | 422 | Từ chối loại xe ngoài enum. |
| TC26 | CTX05 | Negative | FR07 | AC43 | PUT /drivers/me/vehicle | Biển số đã thuộc vehicle khác | Bearer `<valid_token>`; body dùng biển số trùng | 409 | Không tạo/cập nhật biển số trùng. |
| TC27 | CTX05 | Positive | FR08 | AC45–AC47 | PUT /drivers/me/activity-status | Driver đã đăng nhập | Bearer `<valid_token>`; body {"status":"AVAILABLE"} | 204 | Không body; trạng thái driver thành AVAILABLE. |
| TC28 | CTX05 | Negative | FR08 | AC45–AC47 | PUT /drivers/me/activity-status | Driver đã đăng nhập | Bearer `<valid_token>`; body {"status":"ON_TRIP"} | 422 | Từ chối trạng thái không cho phép từ API này. |
| TC29 | CTX05 | Positive | FR09 | AC17–AC18 | PUT /drivers/me/location | Driver đã đăng nhập | Bearer `<valid_token>`; body {"latitude":10.8231,"longitude":106.6297} | 204 | Vị trí mới được ghi nhận để matching. |
| TC30 | CTX05 | Negative | FR09 | AC17–AC18 | PUT /drivers/me/location | Driver đã đăng nhập | Bearer `<valid_token>`; latitude=100 hoặc longitude=200 | 422 | Từ chối tọa độ ngoài phạm vi; không cập nhật vị trí. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
