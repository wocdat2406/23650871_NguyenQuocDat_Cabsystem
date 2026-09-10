# 06 – Notification Test Cases

**API Specification:** `06-notification-api.yaml`

## Ngữ cảnh kiểm thử

### CTX08 – Thông báo sự kiện

Hệ thống gửi thông báo khi booking nhận, driver nhận, driver đến, trip hoàn thành, payment result hoặc ride offer. Notification Provider có thể thất bại; lỗi thông báo không được làm gián đoạn luồng chuyến.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC67 | CTX08 | Positive | FR41 | AC88 | POST /notifications | Booking vừa được tiếp nhận | {"receiverType":"CUSTOMER","receiverId":"550e8400-e29b-41d4-a716-446655440000","rideId":"550e8400-e29b-41d4-a716-446655440001","eventType":"BOOKING_RECEIVED","message":"Booking received"} | 202 | Trả notification result; status SENT hoặc trạng thái xử lý phù hợp. |
| TC68 | CTX08 | Positive | FR42–FR46 | AC89–AC93 | POST /notifications | Có sự kiện hợp lệ | eventType tương ứng DRIVER_ACCEPTED / DRIVER_ARRIVED / TRIP_COMPLETED / PAYMENT_RESULT / NEW_RIDE_OFFER | 202 | Notification được tiếp nhận và gắn đúng receiver/event. |
| TC69 | CTX08 | Negative | FR41–FR46 | AC88–AC93 | POST /notifications | Không có | Thiếu receiverId/eventType/message hoặc receiverType ngoài enum | 422 | Validation error; không tạo notification hợp lệ. |
| TC70 | CTX08 | Negative | FR41–FR46 | AC94 | POST /notifications | Notification Provider mô phỏng lỗi | Request hợp lệ nhưng provider thất bại | 202 | Hệ thống ghi nhận notification `FAILED`/errorCode; luồng ride/payment không bị rollback hoặc gián đoạn. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
