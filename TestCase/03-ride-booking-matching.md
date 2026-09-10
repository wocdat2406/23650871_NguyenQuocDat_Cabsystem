# 03 – Ride Booking & Matching Test Cases

**API Specification:** `03-ride-booking-matching-api.yaml`

## Ngữ cảnh kiểm thử

### CTX03 – Khởi tạo chuyến đi

Khách hàng đã đăng nhập nhập điểm đón, điểm đến, loại xe và gửi yêu cầu đặt chuyến. Có thể thiếu tọa độ/địa chỉ, tọa độ ngoài phạm vi, loại xe không hỗ trợ hoặc không xác thực.

### CTX04 – Tìm và phân công tài xế

Sau khi chuyến được tạo, hệ thống tìm tài xế gần, AVAILABLE và có loại xe phù hợp; gửi offer cho tài xế. Tài xế có thể từ chối, không phản hồi, offer hết hạn hoặc không còn tài xế phù hợp.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC31 | CTX03 | Positive | FR10–FR14 | AC11–AC14 | POST /rides | Customer đã đăng nhập | Authorization; pickup {10.77,106.69,"IUH"}; destination {10.78,106.70,"Destination"}; vehicleType="CAR" | 201 | Tạo ride; trả trạng thái ban đầu `SEARCHING_DRIVER`; bắt đầu matching. |
| TC32 | CTX03 | Negative | FR10–FR14 | AC11–AC12 | POST /rides | Customer đã đăng nhập | Thiếu pickup hoặc destination hoặc vehicleType | 422 | Không tạo ride; validation error. |
| TC33 | CTX03 | Negative | FR10–FR14 | AC11–AC12 | POST /rides | Customer đã đăng nhập | pickup.latitude=95 hoặc address rỗng | 422 | Không tạo ride vì vị trí không hợp lệ. |
| TC34 | CTX03 | Negative | FR13–FR14 | AC12–AC14 | POST /rides | Không xác thực | Bearer `<invalid_or_expired_token>`; body hợp lệ | 401 | Không tạo ride. |
| TC35 | CTX04 | Positive | FR14, FR25 | AC13, AC23 | GET /rides/{rideId} | Ride đang matching | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 200 | Trả ride/status hiện tại. |
| TC36 | CTX04 | Positive | FR25 | AC23 | GET /rides/{rideId} | Matching kết thúc không có driver | Bearer `<valid_token>`; rideId của ride no-driver | 200 | Status `NO_DRIVER_FOUND` để customer biết không tìm được driver. |
| TC37 | CTX04 | Negative | FR14, FR25 | AC13, AC23 | GET /rides/{rideId} | Ride không tồn tại | Bearer `<valid_token>`; rideId UUID không tồn tại | 404 | Trả not found. |
| TC38 | CTX04 | Positive | FR16–FR19, FR24 | AC15–AC18, AC21–AC22 | POST /rides/{rideId}/matching/retry | Ride ở trạng thái cho phép retry | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 202 | Chấp nhận retry và tiếp tục tìm driver mà không tạo ride mới. |
| TC39 | CTX04 | Negative | FR24 | AC21–AC22 | POST /rides/{rideId}/matching/retry | Ride đã có driver hoặc đã hoàn tất/cancel | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 409 | Không chạy matching lại khi trạng thái nghiệp vụ không cho phép. |
| TC40 | CTX04 | Positive | FR20 | AC48 | GET /drivers/me/ride-offers | Driver AVAILABLE có offer hợp lệ | Bearer `<valid_token>` | 200 | Trả danh sách offer gồm assignmentId, rideId, expiresAt và thông tin chuyến. |
| TC41 | CTX04 | Positive | FR20 | AC48 | GET /drivers/me/ride-offers | Driver không có offer | Bearer `<valid_token>` | 200 | Trả danh sách rỗng. |
| TC42 | CTX04 | Positive | FR21 | AC19–AC20, AC49–AC50 | POST /ride-assignments/{assignmentId}/decision | Offer còn hiệu lực; driver đúng người nhận | Bearer `<valid_token>`; body {"decision":"ACCEPT"} | 200 | Offer được chấp nhận; ride được phân công cho driver; chỉ một driver được assign. |
| TC43 | CTX04 | Positive | FR22, FR24 | AC21–AC22, AC49, AC51 | POST /ride-assignments/{assignmentId}/decision | Offer còn hiệu lực | Bearer `<valid_token>`; body {"decision":"REJECT"} | 200 | Ghi nhận reject; ride tiếp tục matching driver khác. |
| TC44 | CTX04 | Negative | FR23–FR24 | AC52–AC53 | POST /ride-assignments/{assignmentId}/decision | Offer đã quá expiresAt | Bearer `<valid_token>`; body {"decision":"ACCEPT"} | 409 | Không cho accept offer hết hạn; ride tiếp tục matching. |
| TC45 | CTX04 | Negative | FR21–FR22 | AC49 | POST /ride-assignments/{assignmentId}/decision | Offer hợp lệ | Bearer `<valid_token>`; body {"decision":"MAYBE"} | 422 | Validation error; không thay đổi assignment. |
| TC46 | CTX04 | Negative | FR21–FR24 | AC20, AC50 | POST /ride-assignments/{assignmentId}/decision | Ride đã được driver khác nhận | Bearer `<valid_token>`; ACCEPT trên offer cũ | 409 | Không cho hai driver cùng được phân công cho một ride. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
