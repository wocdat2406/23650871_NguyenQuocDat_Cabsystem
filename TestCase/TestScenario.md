| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC31 | CTX03 | Positive | FR10–FR14 | AC11–AC14 | POST /rides | Customer đã đăng nhập | pickup + destination + vehicleType | 201 | Tạo ride, status SEARCHING_DRIVER và bắt đầu matching |
| TC32 | CTX03 | Negative | FR10–FR14 | AC11–AC12 | POST /rides | Customer đã đăng nhập | Thiếu pickup/destination/vehicleType | 422 | Không tạo ride, trả validation error |
| TC44 | CTX04 | Negative | FR23–FR24 | AC52–AC53 | POST /ride-assignments/{assignmentId}/decision | Offer đã hết hạn | decision=ACCEPT | 409 | Không cho nhận offer hết hạn và tiếp tục tìm tài xế khác |
