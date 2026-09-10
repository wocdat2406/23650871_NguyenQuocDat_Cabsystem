# 07 – Rating Test Cases

**API Specification:** `07-rating-api.yaml`

## Ngữ cảnh kiểm thử

### CTX09 – Đánh giá tài xế

Khách hàng chỉ đánh giá tài xế của chuyến đã hoàn thành. Có thể đánh giá trước khi hoàn thành, score ngoài 1–5, đánh giá trùng hoặc truy cập chuyến người khác.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC71 | CTX09 | Positive | FR47–FR48 | AC38–AC40 | POST /rides/{rideId}/rating | Ride COMPLETED, customer là chủ chuyến và chưa đánh giá | Bearer `<valid_token>`; body {"score":5,"comment":"Good driver"} | 201 | Rating được tạo, gắn đúng ride/customer/driver. |
| TC72 | CTX09 | Negative | FR47–FR48 | AC38 | POST /rides/{rideId}/rating | Ride chưa COMPLETED | Bearer `<valid_token>`; body {"score":5} | 409 | Không cho đánh giá trước khi chuyến hoàn thành. |
| TC73 | CTX09 | Negative | FR47–FR48 | AC39 | POST /rides/{rideId}/rating | Customer không sở hữu ride | Bearer `<valid_token>` user khác; score hợp lệ | 403 | Không tạo rating. |
| TC74 | CTX09 | Negative | FR47–FR48 | AC40 | POST /rides/{rideId}/rating | Ride COMPLETED | body {"score":0} hoặc {"score":6} | 422 | Từ chối score ngoài 1–5. |
| TC75 | CTX09 | Negative | FR47–FR48 | AC38–AC40 | POST /rides/{rideId}/rating | Ride đã có rating của customer | body score hợp lệ lần thứ hai | 409 | Không tạo đánh giá trùng cho cùng chuyến. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
