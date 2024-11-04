# Phân tích ca sử dụng Create Administrative Report
1. Mô tả ngắn gọn

Ca sử dụng Create Administrative Report cho phép Payroll Administrator tạo báo cáo quản trị dựa trên các tiêu chí về giờ làm việc hoặc tổng thu nhập năm cho nhân viên.

2. Xác định các lớp

Boundary Classes:
  - PaymentSelectionUI: giao diện cho người dùng chọn hình thức thanh toán.
Control Classes:
  - PaymentController: lớp điều khiển xử lý lựa chọn hình thức thanh toán.
Entity Classes:
  - PaymentMethod: lớp chứa các phương thức thanh toán.
  - Employee: thực thể chứa thông tin về nhân viên (để liên kết thanh toán với nhân viên cụ thể).
  - Payment: thực thể chứa thông tin thanh toán cụ thể (tiền lương, hình thức thanh toán).

3. Biểu đồ tuần tự
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T9DDJeH048NtVOfQQZ9Um8MP2IPcDeP0vW0jNMh7fXkh2mndS-6Hl8B5xxGuie3GttklVWZVdr_xo9guhPsARzO3XOXALnm8SjrJSEvWQkjjPDB3eOwG7zHJQBtHr4E1JI0kyBt5oAVZW4z7LGNFOfrfDhqv7Dr5fj2pvSLR8dMsmX6Llz5ufbH-W9ixYOLRc0i11wW8DIFGg5H2HIFAisOYehECP3LSST_W3eouuWwmRbpe4UDrcfzJwAp1hNUEBpAHbEZD7ovauANm1_H8IMToE20XMTenV5X-XMQgPvAaDQX0Rid3ovndDe7PMRA0R9tZtiR6wNuXIZk6KdThKo3NvRN6ZUh2OhskvNF95boeDDlWjt7B5YyBjxjCAifZB37gafqchOyzDbZPPuj9i0HDKyhabIRppw2Fwu3dEaa_6_CGkfVRy7Fy0000__y30000)

4. Các hành vi cảu từng lớp

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

# Phân tích ca sử dụng Create Employee Report. 
1. Mô tả ngắn gọn
Nhân viên có thể tạo các loại báo cáo như "Tổng giờ làm việc," "Tổng giờ làm việc cho một dự án," "Nghỉ phép/Bệnh," hoặc "Tổng lương đến hiện tại trong năm." Báo cáo này có thể được lưu lại nếu nhân viên yêu cầu.
2. Các Lớp Phân Tích
  - Boundary Class: ReportUI
  - Control Class: ReportController
  - Entity Class: Report
  - Entity Class: Project
3. Biểu đồ tuần tự
![](https://www.planttext.com/api/plantuml/png/Z5JDZjCm4BxxAKOzB-BU0rffGS0540LndjeJhNSTJnXFYl9i77WaNW4xZTjGqf8UglnyFpFVZFFxvw_xf2ZQjy6aPnz1E951gopmfkq23qHcptrqA0Dyfev5lxutbgCAX-d1m_4ka1YAwhK2wzqduIUoQanLX1UlJbfRs9K2OFCWX4edrmcmCHLOIFNbjcYsdKAJwvGH05QyadYyuf891--eedNew0x6ti5btpkWwCOhWq4dteW2ds3pXHK3lEDU4dnZUIOtMcFjRMCW_-QbNaQppK--zvGKy80-u3uGT4SoM7QKPWfdLb6QB8g0YgV34c_2N3FMNk9AjtDYhttg0WuBl2jpf51WS_YAL7ObzpHISwX_aVCRiu9yEV_hNMtXBKMIicOJAGySOOyfMtEybBYPvapWXkCynxfvV3vPoq5-xDJdQZ8muQ6MEgxb2MyVEH_KL37_vBnuK1gVTovYIu0vji0MYy-DYTOpSuEuRkLdVS0Fhu-ZsCi5eUMfxMRqSMAbxOwiRpmjrhDSJRvklBHLgHJbLfo33wo-6SuHSGEfjvPIQlfmZ9z2cdsv7EV9HDR_ZMOIhetvP55SBgdi_Nt-An_bFm000F__0m00)
4. Nhiệm vụ của từng lớp
Employee (Nhân viên)
  - Tương tác với giao diện người dùng để khởi tạo yêu cầu tạo báo cáo, cung cấp các tiêu chí cho báo cáo, và chọn lưu báo cáo nếu cần.
ReportUI (Lớp giao diện người dùng)
  - Thu thập thông tin tiêu chí báo cáo từ nhân viên, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc và mã dự án (nếu cần).
  - Hiển thị báo cáo cho nhân viên và cung cấp tùy chọn lưu báo cáo.
  - Xác nhận tên và vị trí lưu báo cáo khi nhân viên chọn lưu.
ReportController (Lớp xử lý)
  - Xử lý và điều phối quy trình tạo báo cáo.
  - Gửi yêu cầu đến lớp Project để lấy danh sách mã dự án nếu loại báo cáo cần mã dự án.
  - Gửi yêu cầu đến lớp Report để tạo báo cáo dựa trên tiêu chí được cung cấp và lưu trữ báo cáo nếu nhân viên chọn lưu.
Project (Lớp thực thể dự án)
  - Cung cấp danh sách mã dự án từ Cơ sở Dữ liệu Quản lý Dự án, để hỗ trợ việc tạo báo cáo "Total Hours Worked for a Project".
Report (Lớp thực thể báo cáo)
  - Tạo dữ liệu báo cáo dựa trên tiêu chí được cung cấp từ ReportController.
  - Lưu báo cáo đến tên và vị trí được chỉ định khi ReportController yêu cầu lưu.
# Phân tích ca sử dụng Maintain Employee Information 
1. 
