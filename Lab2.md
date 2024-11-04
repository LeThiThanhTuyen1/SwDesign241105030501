##I. Phân tích ca sử dụng Create Administrative Report
#1. Mô tả ngắn gọn

Ca sử dụng Create Administrative Report cho phép Payroll Administrator tạo báo cáo quản trị dựa trên các tiêu chí về giờ làm việc hoặc tổng thu nhập năm cho nhân viên.
#2. Xác định các lớp

Boundary Classes:
  - PaymentSelectionUI: giao diện cho người dùng chọn hình thức thanh toán.
Control Classes:
  - PaymentController: lớp điều khiển xử lý lựa chọn hình thức thanh toán.
Entity Classes:
  - PaymentMethod: lớp chứa các phương thức thanh toán.
  - Employee: thực thể chứa thông tin về nhân viên (để liên kết thanh toán với nhân viên cụ thể).
  - Payment: thực thể chứa thông tin thanh toán cụ thể (tiền lương, hình thức thanh toán).
#3. Biểu đồ tuần tự
[!Sequence Diagram](https://www.planttext.com/api/plantuml/png/T9DDJeH048NtVOfQQZ9Um8MP2IPcDeP0vW0jNMh7fXkh2mndS-6Hl8B5xxGuie3GttklVWZVdr_xo9guhPsARzO3XOXALnm8SjrJSEvWQkjjPDB3eOwG7zHJQBtHr4E1JI0kyBt5oAVZW4z7LGNFOfrfDhqv7Dr5fj2pvSLR8dMsmX6Llz5ufbH-W9ixYOLRc0i11wW8DIFGg5H2HIFAisOYehECP3LSST_W3eouuWwmRbpe4UDrcfzJwAp1hNUEBpAHbEZD7ovauANm1_H8IMToE20XMTenV5X-XMQgPvAaDQX0Rid3ovndDe7PMRA0R9tZtiR6wNuXIZk6KdThKo3NvRN6ZUh2OhskvNF95boeDDlWjt7B5YyBjxjCAifZB37gafqchOyzDbZPPuj9i0HDKyhabIRppw2Fwu3dEaa_6_CGkfVRy7Fy0000__y30000)
#4. Các hành vi cảu từng lớp

PayrollAdministrator (PA)
  - Request to create report: PA yêu cầu hệ thống tạo một báo cáo.
  - Provide report criteria: Cung cấp các thông tin cần thiết để tạo báo cáo, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc, và tên nhân viên.
  - Request to save report (nếu có): Nếu chọn lưu báo cáo, PA yêu cầu hệ thống lưu báo cáo, đồng thời cung cấp tên và vị trí để lưu.
  - No save request (nếu không lưu): PA không thực hiện yêu cầu lưu báo cáo nếu quyết định không lưu.

ReportRequestUI (UI)
  - Request report criteria: Hiển thị biểu mẫu và yêu cầu PA cung cấp các tiêu chí cần thiết để tạo báo cáo.
  - Send report criteria: Gửi các tiêu chí báo cáo đã nhận được từ PA tới ReportController để xử lý việc tạo báo cáo.
  - Display report: Hiển thị báo cáo đã được tạo cho PA xem.
  - Request name and location (khi lưu báo cáo): Yêu cầu PA cung cấp tên và vị trí lưu báo cáo nếu PA chọn lưu.
  - Send save report request: Gửi yêu cầu lưu báo cáo tới ReportController với tên và vị trí mà PA đã cung cấp.
  - Discard report: Nếu PA không chọn lưu báo cáo, UI gửi lệnh hủy báo cáo tới ReportController.

ReportController (RC)
  - Send report criteria to ReportService: Nhận tiêu chí từ UI và gửi tới ReportService để bắt đầu quá trình tạo báo cáo.
  - Return report to UI: Sau khi báo cáo được tạo, nhận báo cáo từ ReportService và gửi lại cho UI để hiển thị cho PA.
  - Save report to ReportService: Khi nhận được yêu cầu lưu báo cáo từ UI, ReportController gửi yêu cầu này tới ReportService để thực hiện lưu báo cáo.
  - Discard report: Nếu không có yêu cầu lưu báo cáo, ReportController thực hiện việc hủy bỏ báo cáo theo yêu cầu từ UI.

ReportService (RS)
  - Generate report: Nhận tiêu chí từ ReportController và thực hiện việc tạo báo cáo, gửi yêu cầu tạo báo cáo tới lớp Report (entity).
  -Save report: Nhận yêu cầu lưu báo cáo từ ReportController và lưu báo cáo vào vị trí và tên được chỉ định bởi PA.
Report (R)
  - Create report: Nhận thông tin từ ReportService và tạo báo cáo theo các tiêu chí đã cung cấp (loại báo cáo, ngày tháng, danh sách nhân viên).
  - Return generated report: Trả báo cáo đã tạo lại cho ReportService.

##II. 
