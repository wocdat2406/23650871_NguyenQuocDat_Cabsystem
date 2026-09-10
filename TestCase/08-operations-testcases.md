# 08 – Operations Test Cases

**API Specification:** `08-operations-api.yaml`

## Ngữ cảnh kiểm thử

### CTX10 – Vận hành và phân quyền

Operation Staff tìm kiếm khách hàng/tài xế/xe/chuyến/giao dịch, hỗ trợ chuyến và phân quyền theo quyền được cấp. Người không có quyền phải bị từ chối; dữ liệu/ride/staff không tồn tại phải trả lỗi phù hợp.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC76 | CTX10 | Positive | FR49 | AC59–AC61 | GET /operations/customers | Operation Staff có CUSTOMER_READ | Bearer `<valid_token>`; q=Nguyen | 200 | Trả danh sách customer phù hợp. |
| TC77 | CTX10 | Negative | FR49 | AC59–AC61 | GET /operations/customers | User không có quyền | Bearer `<valid_token>` không có CUSTOMER_READ | 403 | Không trả dữ liệu customer. |
| TC78 | CTX10 | Positive | FR50, FR53 | AC62, AC69–AC70 | GET /operations/drivers | Operation Staff có DRIVER_READ | Bearer `<valid_token>`; q=Tran | 200 | Trả driver và trạng thái hoạt động. |
| TC79 | CTX10 | Positive | FR51 | AC66–AC68 | GET /operations/vehicles | Operation Staff có quyền phù hợp | Bearer `<valid_token>`; q=51A | 200 | Trả vehicle phù hợp và liên kết driver. |
| TC80 | CTX10 | Positive | FR52–FR53 | AC69–AC70 | GET /operations/rides | Operation Staff được phép xem | Bearer `<valid_token>`; status=IN_PROGRESS | 200 | Trả các ride phù hợp trạng thái để theo dõi. |
| TC81 | CTX10 | Positive | FR54 | AC71–AC72 | POST /operations/rides/{rideId}/support-actions | Staff có RIDE_SUPPORT; ride tồn tại | Bearer `<valid_token>`; body {"action":"MARK_FOR_REVIEW","reason":"Driver lost connection"} | 202 | Support action được tiếp nhận và thao tác quan trọng được audit. |
| TC82 | CTX10 | Negative | FR54 | AC71–AC72 | POST /operations/rides/{rideId}/support-actions | Staff không có RIDE_SUPPORT | Bearer `<valid_token>`; body hợp lệ | 403 | Không thực hiện support action; không thay đổi ride. |
| TC83 | CTX10 | Negative | FR54 | AC71–AC72 | POST /operations/rides/{rideId}/support-actions | Staff có quyền | body thiếu reason hoặc action sai enum | 422 | Validation error; không tạo action. |
| TC84 | CTX10 | Positive | FR55 | AC73–AC75 | GET /operations/transactions | Staff có TRANSACTION_READ | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000&status=SUCCESS | 200 | Trả giao dịch phù hợp điều kiện. |
| TC85 | CTX10 | Positive | FR55 | AC76 | GET /operations/transactions | Không có giao dịch phù hợp | Bearer `<valid_token>`; filter không khớp | 200 | Trả danh sách rỗng, không báo lỗi hệ thống. |
| TC86 | CTX10 | Positive | FR56 | AC77–AC80 | PUT /operations/staff/{staffId}/permissions | Người thực hiện có PERMISSION_MANAGE | Bearer `<valid_token>`; body {"permissions":["CUSTOMER_READ","RIDE_SUPPORT"]} | 204 | Quyền mới được lưu/applied và audit. |
| TC87 | CTX10 | Negative | FR56 | AC77, AC81 | PUT /operations/staff/{staffId}/permissions | Người thực hiện không có PERMISSION_MANAGE | Bearer `<valid_token>`; body hợp lệ | 403 | Không thay đổi quyền. |
| TC88 | CTX10 | Negative | FR56 | AC78–AC80 | PUT /operations/staff/{staffId}/permissions | Staff target không tồn tại | Bearer `<valid_token>`; staffId không tồn tại | 404 | Không tạo permission cho staff không tồn tại. |
| TC89 | CTX10 | Negative | FR56 | AC79 | PUT /operations/staff/{staffId}/permissions | Có quyền quản trị | Bearer `<valid_token>`; body permissions=[] hoặc giá trị ngoài enum | 422 | Từ chối danh sách quyền không hợp lệ. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
