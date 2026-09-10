# 04 – Trip Tracking Test Cases

**API Specification:** `04-trip-tracking-api.yaml`

## Ngữ cảnh kiểm thử

### CTX06 – Theo dõi và thực hiện chuyến

Sau khi tài xế được phân công, khách hàng theo dõi ETA/trạng thái; tài xế cập nhật ARRIVED → PICKED_UP → IN_PROGRESS → COMPLETED. Có thể truy cập sai người, sai rideId hoặc cập nhật trạng thái sai thứ tự nghiệp vụ.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC47 | CTX06 | Positive | FR26–FR28, FR33 | AC24–AC27 | GET /rides/{rideId}/tracking | Customer sở hữu ride đang SEARCHING_DRIVER | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 200 | Trả trạng thái SEARCHING_DRIVER; driver/ETA có thể chưa có. |
| TC48 | CTX06 | Positive | FR26–FR28, FR33 | AC25–AC27 | GET /rides/{rideId}/tracking | Ride đã có driver | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 200 | Trả driver info, ETA và trạng thái mới nhất. |
| TC49 | CTX06 | Negative | FR33 | AC24–AC27 | GET /rides/{rideId}/tracking | Người dùng không thuộc ride | Bearer `<valid_token>` của user khác; rideId=550e8400-e29b-41d4-a716-446655440000 | 403 | Không cho xem tracking chuyến người khác. |
| TC50 | CTX06 | Positive | FR29–FR32 | AC54–AC58 | PATCH /rides/{rideId}/status | Driver được assign; trạng thái hiện tại cho phép chuyển tiếp | Bearer `<valid_token>`; body {"status":"ARRIVED_PICKUP"} | 200 | Status cập nhật thành ARRIVED_PICKUP và được lưu. |
| TC51 | CTX06 | Positive | FR29–FR32 | AC55–AC58 | PATCH /rides/{rideId}/status | Ride theo đúng thứ tự | Lần lượt ARRIVED_PICKUP → PASSENGER_PICKED_UP → IN_PROGRESS → COMPLETED | 200 mỗi bước | Mỗi trạng thái được lưu; cuối cùng ride COMPLETED. |
| TC52 | CTX06 | Negative | FR29–FR32 | AC56–AC57 | PATCH /rides/{rideId}/status | Ride vừa DRIVER_ASSIGNED | Gửi trực tiếp {"status":"COMPLETED"} | 409 | Từ chối chuyển trạng thái sai thứ tự; trạng thái cũ giữ nguyên. |
| TC53 | CTX06 | Negative | FR29–FR32 | AC54 | PATCH /rides/{rideId}/status | Driver khác không được assign | Bearer `<valid_token>` của driver khác; body status hợp lệ | 403 | Không cho driver khác cập nhật chuyến. |
| TC54 | CTX06 | Negative | FR29–FR32 | AC55–AC57 | PATCH /rides/{rideId}/status | Driver được assign | body {"status":"UNKNOWN"} | 422 | Validation error; không đổi trạng thái. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
