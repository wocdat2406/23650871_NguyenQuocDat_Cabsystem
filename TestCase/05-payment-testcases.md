# 05 – Payment Test Cases

**API Specification:** `05-payment-api.yaml`

## Ngữ cảnh kiểm thử

### CTX07 – Tính cước và thanh toán

Chỉ sau khi chuyến COMPLETED, hệ thống trả cước và khách hàng chọn CASH hoặc ELECTRONIC. Có thể yêu cầu cước quá sớm, payment token thiếu, provider thất bại hoặc retry sai trạng thái.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC55 | CTX07 | Positive | FR34–FR35 | AC31–AC32 | GET /rides/{rideId}/fare | Ride COMPLETED và user có quyền | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 200 | Trả fare của ride, số tiền >= 0. |
| TC56 | CTX07 | Negative | FR34–FR35 | AC31 | GET /rides/{rideId}/fare | Ride chưa COMPLETED | Bearer `<valid_token>`; rideId=550e8400-e29b-41d4-a716-446655440000 | 409 | Không tính/trả cước cuối cùng trước khi hoàn thành. |
| TC57 | CTX07 | Negative | FR34–FR35 | AC31–AC32 | GET /rides/{rideId}/fare | Ride không thuộc user | Bearer `<valid_token>` của user khác | 403 | Không trả thông tin cước. |
| TC58 | CTX07 | Positive | FR36–FR37, FR39 | AC33, AC36 | POST /rides/{rideId}/payments | Ride COMPLETED, fare đã có | Authorization; body {"method":"CASH"} | 201 | Tạo payment CASH; amount đúng fare; lưu trạng thái thanh toán. |
| TC59 | CTX07 | Positive | FR36, FR38–FR39 | AC33–AC36 | POST /rides/{rideId}/payments | Ride COMPLETED; payment token hợp lệ | Authorization; body {"method":"ELECTRONIC","paymentToken":"tok_test_123"} | 201 | Tạo payment; gửi provider; không lưu dữ liệu thẻ nhạy cảm; ghi kết quả. |
| TC60 | CTX07 | Negative | FR38–FR39 | AC34–AC35 | POST /rides/{rideId}/payments | Ride COMPLETED | body ELECTRONIC nhưng thiếu paymentToken | 422 | Validation error; không gọi provider với dữ liệu thiếu. |
| TC61 | CTX07 | Negative | FR36–FR39 | AC31–AC33 | POST /rides/{rideId}/payments | Ride chưa COMPLETED | body CASH/ELECTRONIC hợp lệ | 409 | Không tạo payment trước khi chuyến hoàn thành. |
| TC62 | CTX07 | Positive | FR39 | AC36 | GET /payments/{paymentId} | Payment tồn tại và user có quyền | Bearer `<valid_token>`; paymentId=550e8400-e29b-41d4-a716-446655440001 | 200 | Trả paymentId, rideId, method, amount, status. |
| TC63 | CTX07 | Negative | FR39 | AC36 | GET /payments/{paymentId} | Payment không tồn tại | Bearer `<valid_token>`; paymentId UUID không tồn tại | 404 | Trả not found. |
| TC64 | CTX07 | Positive | FR40 | AC37 | POST /payments/{paymentId}/retry | Payment ELECTRONIC ở FAILED | Authorization; body {"paymentToken":"tok_retry_123"} | 200 | Thực hiện retry và trả trạng thái payment mới. |
| TC65 | CTX07 | Negative | FR40 | AC37 | POST /payments/{paymentId}/retry | Payment SUCCESS hoặc CASH | Authorization; body paymentToken hợp lệ | 409 | Không retry payment không ở trạng thái/loại cho phép. |
| TC66 | CTX07 | Negative | FR40 | AC37 | POST /payments/{paymentId}/retry | Payment FAILED | body thiếu paymentToken | 422 | Validation error; payment vẫn FAILED. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
