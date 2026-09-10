# 09 – Reporting Test Cases

**API Specification:** `09-reporting-api.yaml`

## Ngữ cảnh kiểm thử

### CTX11 – Báo cáo quản lý

Management/nhân sự có quyền báo cáo truy vấn số chuyến, doanh thu, tỷ lệ và hiệu quả tài xế theo khoảng ngày. Có thể thiếu quyền, thiếu ngày, from > to hoặc khoảng ngày không có dữ liệu.

## Test Cases

| TC | Context | Type | FR | AC | API | Preconditions | Input | Expected HTTP | Expected Output |
|---|---|---|---|---|---|---|---|---:|---|
| TC90 | CTX11 | Positive | FR57 | AC82–AC83 | GET /reports/trips/count | User có REPORT_READ | Authorization; from=2026-09-01&to=2026-09-10 | 200 | Trả `from`, `to`, `tripCount >= 0`. |
| TC91 | CTX11 | Positive | FR58 | AC82, AC84 | GET /reports/revenue | User có REPORT_READ | Authorization; from=2026-09-01&to=2026-09-10 | 200 | Trả revenue >= 0 và currency. |
| TC92 | CTX11 | Positive | FR59 | AC82, AC85 | GET /reports/rides/rates | User có REPORT_READ | Authorization; from=2026-09-01&to=2026-09-10 | 200 | completionRate và cancellationRate nằm trong 0..1. |
| TC93 | CTX11 | Positive | FR60 | AC82, AC86 | GET /reports/drivers/performance | User có REPORT_READ | Authorization; from=2026-09-01&to=2026-09-10 | 200 | Trả danh sách performance; completedTrips >=0; rating nếu có nằm 1..5. |
| TC94 | CTX11 | Positive | FR57–FR60 | AC87 | Các GET /reports/* | Khoảng thời gian hợp lệ nhưng không có dữ liệu | Authorization; from/to không có dữ liệu | 200 | Trả 0 hoặc danh sách rỗng phù hợp; không sinh dữ liệu giả. |
| TC95 | CTX11 | Negative | FR57–FR60 | AC82 | Các GET /reports/* | User không có REPORT_READ | Bearer `<valid_token>` không đủ quyền | 403 | Không trả dữ liệu báo cáo. |
| TC96 | CTX11 | Negative | FR57–FR60 | AC82–AC87 | Các GET /reports/* | User có quyền | Thiếu `from` hoặc `to` | 422 | Validation error. |
| TC97 | CTX11 | Negative | FR57–FR60 | AC82–AC87 | Các GET /reports/* | User có quyền | from=2026-09-10&to=2026-09-01 | 422 | Từ chối khoảng ngày ngược; không trả báo cáo sai. |

## Điều kiện Pass/Fail

- **PASS:** HTTP status, cấu trúc response và quy tắc nghiệp vụ khớp Expected Output.
- **FAIL:** trả sai status, sai dữ liệu, cho phép thao tác trái quy trình, hoặc thay đổi dữ liệu khi request phải bị từ chối.
