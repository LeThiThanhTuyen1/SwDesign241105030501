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

5. Biểu đồ lớp

a) Các lớp phân tích và nhiệm vụ của từng lớp

AdminReportUI:
  - Nhiệm vụ: Đây là lớp giao diện, tương tác trực tiếp với người dùng để yêu cầu nhập tiêu chí báo cáo và khởi tạo yêu cầu tạo báo cáo từ AdminReportController. Lớp này cũng cho phép người dùng lưu báo cáo.
  - Phương thức:
    + generateReport(): Yêu cầu tạo báo cáo từ AdminReportController.
    + saveReport(location: String): Lưu báo cáo vào vị trí do người dùng chỉ định.

AdminReportController:
  - Nhiệm vụ: Đây là lớp điều khiển, chịu trách nhiệm quản lý quá trình tạo báo cáo, yêu cầu và lấy dữ liệu từ các lớp liên quan (như Employee và Project). Nó cũng xử lý logic lưu báo cáo.
  - Phương thức:
      + requestReport(criteria: ReportCriteria): Nhận yêu cầu từ AdminReportUI và tạo báo cáo dựa trên tiêu chí từ ReportCriteria.
      + saveReport(report: Report, location: String): Lưu báo cáo được tạo vào vị trí chỉ định.

Report:
  - Nhiệm vụ: Lớp này đại diện cho báo cáo thực tế, bao gồm các loại báo cáo khác nhau (như giờ làm, nghỉ phép, lương, v.v.) cùng các phương thức để tạo và lấy dữ liệu báo cáo.
  - Phương thức:
    + generate(): Tạo báo cáo dựa trên dữ liệu có sẵn và tiêu chí nhận được từ ReportCriteria.
    + getData(): Trả về dữ liệu báo cáo để hiển thị hoặc lưu.

ReportCriteria:
  - Nhiệm vụ: Lớp này lưu trữ tiêu chí báo cáo, chẳng hạn như loại báo cáo, ngày bắt đầu và kết thúc. Nó giúp AdminReportController có thể xác định rõ ràng thông tin cần để tạo báo cáo.
  - Thuộc tính: reportType, startDate, endDate.

Project:
  - Nhiệm vụ: Lớp này đại diện cho một dự án, bao gồm các thuộc tính liên quan đến mã số dự án và cung cấp danh sách các số mã (charge numbers) liên quan đến dự án để báo cáo về dự án.
  - Phương thức:
    + getChargeNumbers(): Cung cấp danh sách mã chi phí liên quan đến dự án nếu báo cáo yêu cầu dữ liệu về dự án.

Employee:
  - Nhiệm vụ: Đại diện cho nhân viên, bao gồm thông tin về thời gian làm việc, ngày nghỉ phép, tiền lương, và phương thức để tạo báo cáo dựa trên yêu cầu của AdminReportController.
  - Phương thức:
    + generateReport(reportType: String, startDate: Date, endDate: Date): Tạo báo cáo cho nhân viên dựa trên loại báo cáo và khoảng thời gian.
   
b) Quan hệ giữa các lớp
  - AdminReportUI — AdminReportController: AdminReportUI là giao diện người dùng sẽ gửi yêu cầu tạo báo cáo đến AdminReportController.
  - AdminReportController — Report: AdminReportController quản lý quá trình tạo báo cáo bằng cách lấy và cung cấp dữ liệu từ các lớp khác (như Employee và Project) dựa trên tiêu chí của ReportCriteria.
  - ReportCriteria — Report: ReportCriteria chứa thông tin về loại báo cáo và khoảng thời gian, được sử dụng trong lớp Report để tạo báo cáo chính xác.
  - AdminReportController — Project và Employee: AdminReportController truy vấn dữ liệu từ Project và Employee dựa trên loại báo cáo yêu cầu để tổng hợp thông tin cho báo cáo.

c) Biểu đồ lớp phân tích
![](https://www.planttext.com/api/plantuml/png/h5HBJiCm4Dtd55usgBr0XAgY5aIbgggW2B4SaY6O9dOOEvKYnCbOS2IkW5t7WJYqAx98DCypRtxF-Vhud2aDfEkoYDIE2qPIOPGMe1Ixo4ekRh2IfE-Mx2rYzibH8856XuzYXohOUwIGAMWkHS9kDN6Hnz5xD2ISIw595WMI9oPyhL7fbYKbhf4u9AprR-rXFZfylD-OdSZlN7uIMclRLEXTMsuxZuLfCM7sxK0KMGXbe4rvAwxqkGkVzYVaPvEZPOFHe13VqpyKr35lIBvWslLOENEPzHbRU0rbaChKEdy6od5Tbuz8QXG77NQ9Bikga0sYpuIj7QRIKaDnBMjIzv9sQ4wl2WdQ7Ux1xMe1ZKhOKhImukbkXMR50NxWsa3pW41RwTh_nHP8SpZESJZASN-CiLUHRREl_ibaUaI-YLUkYlvsiA6jyX9MWe0SJxdw3LfUKpNkKHsaTYAasyKW9X1QhnH_nTYJfD3nR38vscwjJFtHp4pE_ZI-0G00__y30000)
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
5. Biểu đồ lớp

a) Các lớp phân tích và nhiệm vụ của từng lớp
Employee
  - Nhiệm vụ: Lớp này đại diện cho nhân viên, cho phép truy xuất và quản lý thông tin về nhân viên.
  - Thuộc tính:
    + employeeID
    + name
    + position
Phương thức:
  - getEmployeeInfo(): Lấy thông tin nhân viên cho báo cáo.

ReportGenerator
  - Nhiệm vụ: Xử lý yêu cầu từ người dùng để tạo các loại báo cáo khác nhau.
  - Thuộc tính:
    + reportType
    + startDate
    + endDate
  - Phương thức:
    + generateReport(): Tạo báo cáo dựa trên tiêu chí được cung cấp.
    + selectChargeNumber(): Lựa chọn mã phí cho báo cáo dự án cụ thể.

EmployeeReportUI
  - Nhiệm vụ: Giao diện cho phép người dùng chọn loại báo cáo, nhập tiêu chí, và yêu cầu lưu báo cáo.
  - Thuộc tính:
    + selectedReportType
    + inputCriteria
  - Phương thức:
    + displayReportOptions(): Hiển thị các lựa chọn loại báo cáo.
    + enterCriteria(): Yêu cầu người dùng nhập tiêu chí báo cáo.
    + displayReport(): Hiển thị báo cáo đã tạo cho người dùng.

FileManager
  - Nhiệm vụ: Xử lý lưu trữ và xóa các báo cáo đã tạo.
  - Thuộc tính:
    + fileName
    + filePath
  - Phương thức:
    + saveReport(): Lưu báo cáo vào hệ thống.
    + discardReport(): Xóa báo cáo không lưu.

b) Quan hệ giữa các lớp
  - EmployeeReportUI tương tác với ReportGenerator để yêu cầu tạo báo cáo và lấy thông tin liên quan từ Employee.
  - ReportGenerator có thể yêu cầu Employee cung cấp thông tin nhân viên nếu cần thiết cho báo cáo.
  - ReportGenerator sau khi tạo báo cáo sẽ gửi kết quả tới EmployeeReportUI để hiển thị.
  - FileManager được EmployeeReportUI sử dụng để lưu hoặc xóa báo cáo sau khi người dùng xác nhận.

c) Biểu đồ lớp
![](https://www.planttext.com/api/plantuml/png/T5BBJiCm4BpxAto4GyGz1rIf1PG31HNuW2NP9XQ9RRoReWZnPHpu97u1Eo-eKtA8el7EpcGytvzVAs9mt3Qre1UbfJE48g-1I5urjZOTedmNqZ-9n178DgbKcaTKGuEfV62dT3b2rf1YPVGHB6M9FEtCzDwSdQVoO5GXFiIek4Dh7D-WHWTit2piUlonix5Gxtq3xF7mddpg8iA2ThyK1ubPUZWah37dTGMkn6tRFADRUfkS3mkUijdSGCPYzvz9fMtBQwSOdO8eaaAHhQ4Rk7SsX4QHETIUED6ZioFwqlErgl4MD9Juc-NUOzlbbGNu7hYA_14SJaVcbNDmnL9vaLEIN2ukjk-F_ywPv9lYIiG3WJJtB_K5U6sH_70132U7__vgsjkcYz4ZZVqHOkMR4Ph-0m00__y30000)

# Phân tích ca sử dụng Maintain Employee Information 
1. Mô tả ngắn gọn

Ca sử dụng "Maintain Employee Information" cho phép Payroll Administrator (Quản trị viên Lương) thực hiện các thao tác duy trì thông tin nhân viên như: thêm mới, cập nhật, và xóa. Payroll Administrator sẽ chọn hành động muốn thực hiện (thêm, cập nhật, hoặc xóa). Hệ thống sẽ hướng dẫn để nhập thông tin cần thiết, xác nhận và lưu lại thông tin.

2. Các lớp phân tích
  - Actor: PayrollAdministrator
  - Boundary class: EmployeeUI 
  - Control Class: EmployeeController 
  - Entity Class: Employee 

3. Biều đồ tuần tự
![](https://www.planttext.com/api/plantuml/png/x5N1Ji904BtlLqmyIQ9-00S34MCua1W97x1qXxXnkrkdKqc_pOEVv2yu2uM2hL28YHT9QCgoxysRzwRTp_UFGSwQk4YTob-i1mevAfrm87ZK9GNdXYQrtkPCMXRLF1JUQ2hXFirSA15dOvK4px9pktIt_ksG57gsN6zMgeqKhcztwFemZOhWOgAjP_bk_uEnNmHADTlWBrIDYFWstZuyKaWp1a61z2Gmk1mQSmMpp6Z6AnYXGyPUDrMoD-6AHodj68GBTArFWNnEb8MRtWnAhovVSNIHS-yPct2uz3gLnhZCv8gStFHQL3M3YkrvqwwckNkNemztX68cU5pMUC8aaDc3_rJu0JrI9DY2nwCETQC78vjdJfVxfR-X3-KmVGxB1bYXox6Qa5zBjn9rHh2jxRJv-8Il1UPS8wqyBJ0lkzaPyKmMtt2Ve5E40Yt87m0UZx29xU9LbTB1iJqoyiMAuipH_rx_XB6N-uMbjAfVJTtwVVG_TNyoTIlladKigpEcitcRB4sCRmCyxjqUh7QWasyJJI-r_AXyMrmENQFKGAxnLFy2003__mC0)
4. Nhiệm Vụ của Từng Lớp

PayrollAdministrator (Quản trị viên Lương)
  - Tương tác với giao diện người dùng để thêm, cập nhật, hoặc xóa thông tin nhân viên.
  - Nhập thông tin nhân viên mới, xác nhận việc xóa nhân viên, và thực hiện các chỉnh sửa cần thiết.

EmployeeUI (Lớp giao diện người dùng)
  - Hiển thị các lựa chọn thao tác (Thêm, Cập nhật, Xóa) cho Payroll Administrator.
  -Nhận thông tin nhân viên từ Payroll Administrator để thêm mới hoặc cập nhật.
  - Xác nhận thao tác xóa nhân viên với Payroll Administrator.
  - Hiển thị ID nhân viên mới hoặc thông tin cập nhật cho Payroll Administrator.

EmployeeController (Lớp điều khiển)
  - Xử lý và điều phối yêu cầu thêm, cập nhật, hoặc xóa thông tin nhân viên từ EmployeeUI.
  - Gửi yêu cầu tới lớp Employee để tạo, truy xuất, cập nhật, hoặc đánh dấu nhân viên cần xóa.
  - Truyền thông tin hoặc xác nhận về trạng thái nhân viên đến EmployeeUI.

Employee (Lớp thực thể nhân viên)
  - Tạo và lưu trữ thông tin nhân viên mới, bao gồm việc sinh mã ID độc nhất.
  - Truy xuất thông tin nhân viên để hiển thị cho Payroll Administrator trong quá trình cập nhật hoặc xóa.
  - Cập nhật các chi tiết nhân viên khi cần.
  - Đánh dấu nhân viên cần xóa để hệ thống trả lương cuối cùng trước khi xóa khỏi hệ thống.
5. Biểu đồ lớp
a)  Các lớp phân tích và nhiệm vụ của từng lớp

PayrollAdministrator
  - Nhiệm vụ: Đại diện cho người sử dụng chính, người thực hiện các thao tác duy trì thông tin nhân viên.
  - Thuộc tính:
    + administratorID
    + name
  - Phương thức:
    + selectFunction(): Chọn chức năng (thêm, cập nhật, hoặc xóa).

EmployeeManager
  - Nhiệm vụ: Xử lý các thao tác thêm, cập nhật và xóa thông tin nhân viên.
  - Thuộc tính:
    + employeeList
  - Phương thức:
    + addEmployee(): Thêm nhân viên mới.
    + updateEmployee(): Cập nhật thông tin nhân viên.
    + deleteEmployee(): Xóa thông tin nhân viên.

Employee
  - Nhiệm vụ: Đại diện cho thông tin nhân viên trong hệ thống.
  - Thuộc tính:
    + employeeID
    + name
    + employeeType (giờ, lương, hoặc hoa hồng)
    + address
    + socialSecurityNumber
    + phoneNumber
    + salary
    + hourlyRate
  - Phương thức:
    + getEmployeeInfo(): Truy xuất thông tin nhân viên.
    + setEmployeeInfo(): Cập nhật thông tin nhân viên.

EmployeeUI
  - Nhiệm vụ: Giao diện cho Payroll Administrator để nhập và xem thông tin nhân viên.
  - Thuộc tính:
    + selectedFunction
    + inputData
  - Phương thức:
    + displayEmployeeInfo(): Hiển thị thông tin nhân viên.
    + enterEmployeeData(): Yêu cầu người dùng nhập thông tin nhân viên.
    + confirmDeletion(): Xác nhận thao tác xóa.
b) Quan hệ giữa các lớp
  - PayrollAdministrator sử dụng EmployeeUI để chọn chức năng (thêm, cập nhật, hoặc xóa).
  - EmployeeUI tương tác với EmployeeManager để thực hiện chức năng đã chọn và yêu cầu thêm thông tin   - từ lớp Employee khi cần.
  - EmployeeManager trực tiếp quản lý dữ liệu trong Employee, thực hiện các thao tác thêm, cập nhật hoặc xóa.

c) Biểu đồ lớp phân tích
![](https://www.planttext.com/api/plantuml/png/X5D1JiCm4Bpx5Nk4GpyGeQf81QaI84JX0TjusreuTl2kGH7YPHnu4b_0QPCsk2taaCFCP7TsT_Bz-JLXmI2niegVZOFWcLHfaHdkiGdUsajT6MTO0eeFyAuWFIF08JgR5c2ST9J3YWgOIp1kjO40c2oLSXrTASQxi_C2NhtHwaDrhQwgslg6w1OThcZVXJhy9dKge7rVzD9nLngrxg5TtIqJQur29qYT71qX3nmTMFbdrhtmiQbpAdaDn9oXx4k3Tavb34QQkrWjA6IIUkqT7MKOBOQc0EtZmb87hdqCjdb8q_yY05Oa_M0pj_JPJlW4Ux2KfzbkBTlBakvlczapheuoHS4i4DfmRR7vmmmveT3pROMCBxrRcb1DspjccJeQtD5eFFI_EI85B8NXpSXQ3RYXj4za0O5U8d6IusPGLhba-5dILnkO8OKGbPgGq-rFzWC00F__0m00)

# Phân tích ca sử dụng Run Payroll
1. Mô tả ngắn gọn

Ca sử dụng "Run Payroll" mô tả quá trình hệ thống tự động xử lý bảng lương cho nhân viên vào mỗi thứ Sáu và ngày làm việc cuối cùng của tháng. Hệ thống sẽ tính toán tiền lương dựa trên các thông tin liên quan như thời gian làm việc, đơn hàng, thông tin nhân viên và các khoản khấu trừ hợp pháp. Hệ thống sẽ in phiếu lương nếu phương thức thanh toán là thư hoặc nhận trực tiếp, hoặc tạo giao dịch ngân hàng nếu là chuyển khoản trực tiếp.

2. Các lớp phân tích
  - Boundary: PayrollUI: Đại diện cho giao diện hệ thống để hiển thị kết quả và trạng thái quá trình tính lương.
  - Entity:
    + Employee: Chứa thông tin về nhân viên, bao gồm mức lương, giờ làm, các khoản khấu trừ, và phương thức thanh toán.
    + Timecard: Lưu trữ thời gian làm việc của từng nhân viên, được sử dụng để tính lương.
    + Payroll: Thực hiện tính toán lương cho nhân viên dựa trên thông tin từ Employee và  Timecard.
    + BankTransaction: Đại diện cho giao dịch ngân hàng để xử lý các khoản lương qua phương thức chuyển khoản.

Controller: PayrollController: Điều khiển toàn bộ quá trình chạy bảng lương, từ việc lấy danh sách nhân viên, tính toán lương, đến việc in phiếu lương hoặc tạo giao dịch ngân hàng.

3. Biểu đồ tuần tự
![](https://www.planttext.com/api/plantuml/png/T5D1ReCm4Bpx5IjEYTHyW4CLGLALGwD89UhPDKknC3QobqFUraEVr2zqJKAIbfG3icTdTeR5_lxyMWUIdeREYD1g2zu555AHyx2NH--CEHGW0nmAePmb1YOyFsqD-bY_xWHQqdI4RTSRTqICLLvFSAaxLD9N4Ixp2JttZ20l9pIJjYszj843QMTZDIk5u4Ihnnl75FnWpnqMIt4JZ6bidS87qjRe3_rkS8eLcCbhMFrfPNGWS3NWcGyu2OHnheUQ9uDIDHTS03-_FSjyj7nsWm-BYLTKov5QvZFF9XBVd6-nkjEDlom59OqQZ2JS8J4GknQsTW-tsbD_hiuCx2WQoz9Gf7GyOkYG6bU13f1ij4T5iC7U1Kt9I9r7oSeKUkyKXd3pNwvXJZxBYpehPr7egdibIKCOoMW2telr8hL9W4UUxBLgLqF_Nx934PDf6_rLWwgz7mhjlGcFPwIJldroVeC6OxYYtY5MMF4nYQ8rl-8b-G400F__0m00)
4. Nhiệm vụ của từng lớp

  - PayrollUI: Khởi tạo quá trình xử lý bảng lương và hiển thị trạng thái hoặc kết quả cho người dùng.
  - PayrollController: Điều phối toàn bộ quy trình chạy bảng lương, lấy danh sách nhân viên, tính toán và thực hiện thanh toán dựa trên phương thức đã chọn.
  - Employee:Đại diện cho từng nhân viên và lưu trữ các thông tin chi tiết như mức lương, phương thức thanh toán và trạng thái xóa.
  - Timecard: Quản lý giờ làm việc của từng nhân viên để cung cấp dữ liệu tính lương.
  - Payroll: Thực hiện các phép tính cho lương ròng và áp dụng các khoản khấu trừ hợp pháp.
  - BankTransaction: Xử lý giao dịch ngân hàng cho các khoản thanh toán qua chuyển khoản.

5.Biểu đồ lớp

a) Các lớp phân tích và nhiệm vụ của từng lớp

PayrollUI
  - Nhiệm vụ: Giao diện người dùng để khởi tạo quá trình chạy bảng lương và hiển thị trạng thái hoặc kết quả.
  - Phương thức:
    + runPayroll(): Gửi yêu cầu chạy bảng lương tới PayrollController.
    + printPaycheck(empInfo: Employee, netPay: Float): In phiếu lương cho nhân viên.
    + displayPayrollStatus(status: String): Hiển thị trạng thái quá trình chạy bảng lương.

PayrollController
  - Nhiệm vụ: Điều phối toàn bộ quá trình chạy bảng lương, bao gồm lấy danh sách nhân viên, tính toán lương, và xử lý thanh toán.
  - Phương thức:
    + runPayroll(): Quản lý toàn bộ quá trình chạy bảng lương.
    + getEligibleEmployees(): List<Employee>: Lấy danh sách nhân viên đủ điều kiện nhận lương.
    + processEmployeePay(employee: Employee): Tính toán và xử lý thanh toán cho từng nhân viên.
    + markForDeletionIfNeeded(employee: Employee): Đánh dấu xóa nhân viên nếu cần.

Employee
  - Nhiệm vụ: Lưu trữ thông tin chi tiết của từng nhân viên và cung cấp các phương thức liên quan đến nhân viên.
  - Thuộc tính:
    + employeeId: String
    + salary: Float
    + paymentMethod: String
    + markedForDeletion: Boolean
  - Phương thức:
    + isEligibleForPayroll(currentDate: Date): Boolean: Kiểm tra điều kiện nhận lương.
    + getPaymentDetails(): Payment: Lấy thông tin thanh toán của nhân viên.

Timecard
  - Nhiệm vụ: Quản lý và cung cấp dữ liệu về giờ làm việc của nhân viên.
  - Thuộc tính:
    + employeeId: String
    + hoursWorked: Float
    + date: Date
  - Phương thức:
    + getHours(employeeId: String): Float: Lấy số giờ làm việc của nhân viên.

Payroll
  - Nhiệm vụ: Thực hiện các phép tính chi tiết cho quá trình chạy bảng lương.
  - Phương thức:
    + calculateNetPay(empInfo: Employee, hoursWorked: Float): Float: Tính lương ròng.
    + applyDeductions(empInfo: Employee): Float: Áp dụng các khoản khấu trừ hợp pháp.

BankTransaction 
  - Nhiệm vụ: Xử lý giao dịch ngân hàng cho các khoản thanh toán qua chuyển khoản.
  - Thuộc tính:
    + transactionId: String
    + amount: Float
  - Phương thức:
    + processTransaction(empInfo: Employee, netPay: Float): Boolean: Thực hiện giao dịch ngân hàng.

b) Quan hệ giữa các lớp
  - PayrollUI giao tiếp với PayrollController để khởi tạo quá trình chạy bảng lương và nhận trạng thái từ quá trình.
  - PayrollController tương tác với Employee để lấy danh sách nhân viên đủ điều kiện nhận lương.
  - PayrollController sử dụng Timecard để lấy dữ liệu giờ làm việc của từng nhân viên.
  - PayrollController gọi Payroll để tính toán lương ròng cho từng nhân viên.
  - PayrollController tương tác với BankTransaction nếu phương thức thanh toán của nhân viên là chuyển khoản trực tiếp.
  - PayrollController tương tác lại với Employee để đánh dấu xóa nhân viên nếu cần thiết sau khi xử lý lương.

c) Biểu đồ lớp phân tích
![](https://www.planttext.com/api/plantuml/png/X9JFYjim4CRlUWeTRMXUG9HbsMQN1jgbi5jwdbgpYOWi6OsqO4gVh8S-Kb-XactPZXsJ76BpUURJR_xO__xylISFpeTQCpehmvqbP9K68luDMcUr_dxWlnXFFnVCe1LbhpHE6H-rweJLkS2wEPWtA_XZtMZR8dxW1jDZmP-q1JyaIKMDXdQmUl7W0nNKNGH_yT7oMBBVx9BYapK-NT5jqnpHFsfrL3yrPW8gIi6_AF8VitANoMs5H5cDJWc_kv_u1zyQtFd9kZrgzCgQmzipeaHvDM7apjA0kyl11vcBx7K23Ivtg9SQQ6iq_Ylwarr49nIKCnZ17wpL2AP7LPGx46DoUwhWNFJRWu-ewRzSP1sxAQKpz-X1wQvhWp9LzAfghC39MnMTR73qmoRGYxBaUFvuwkSKMgoDofouN8Cy_0fq5NIqUkxGhwtU6gESut1e6jtkKOOgzP7M5ck81p3dLmU6eCl9ZV2JjEm5r3OOVt7ki7apdzilpZIlo3AzbxlTtPNtGt1bb5UnESJMJrFEk9k2Euoq-BuPEWvTy42RKNaw8bUt6RbiuHoMZLnRXKNtToMHUDmbO2FRpV3PBcIkpQJOaU0C3HDWI-1RQRDbw3zjx1wDJD_N_m000F__0m00)

# Phân tích biểu đồ Select Payment Method
1. Mô tả ngắn gọn

Ca sử dụng này cho phép Nhân viên chọn một phương thức thanh toán. Phương thức thanh toán sẽ quyết định cách Nhân viên nhận lương. Nhân viên có thể chọn một trong ba phương thức: nhận séc trực tiếp, nhận séc qua đường bưu điện, hoặc nhận lương qua chuyển khoản trực tiếp vào tài khoản ngân hàng đã đăng ký.

2. Các lớp phân tích
  - Boundary Class: PaymentUI
  - Controller Class: PaymentController
  - Entity Class: Employee, EmployeePayment
3. Biểu đồ tuần tự
![](https://www.planttext.com/api/plantuml/png/b5JBQjmm5DthAowppmy4N492eQLfo2A5TkdnY94OMpAs7EfbwQAKKEZGHRVZXb8QMff2L_PY5XhcF_G5_OLUoKxzcCaaySB6L-UUSy-nvB_LyY1LVgAoA2JfZ0j8P4g97oYPmECe3cLEAVWfK4B6CXCJFydXrCyZAjIBftOXuoIGGYKolAaVrQyXJUnwe9AGO9Mhl4yOnSDoq-zMOpydXCBU8nI0VJWqvIy5gxaflsKGC5Dz412pzVMw45DG-Fuzm8Sl62Yf2q6m2LkjDZQ_qbVOTDzMueSAJWU0aM2c_2b09QRwZNXkocKy8e2N4q4nEpAA7I4k1WTN4DUEdbF5v0IyssXecD9DoV7wEaFBt5JlH5_AHT9nvLXZ6qzruJkFxns-Je4Y-6GJ0Lr-1s_ZNdtSXUk5UvPakQdUY3ku7vHIppcSwmM4TQNZRtjc0RFJl1KmOzAKb_VBJJ7zntBWxXTJ_KK0qmintPwWqbSzb9ikDTKSLnRyHdOGvzbT0iCiTqpqe20tucZ3l4M2YWaX0urZYzzrP1okjV5I5m4qEtqrrvSsxVz3ajx7Q98PwqBQYHP86TWAQOD_mfq3Ati1hrjgGZmFZZDJVN93uGG8APVxyAnnfdz4hlGrxvbbrkmvjz_HyznXF-cKPWtIqkAzBFZc3kfD59hgCuVH5j6EqgZEzG3lzaVx3m00__y30000)
4. Nhiệm vụ của từng lớp phân tích
PaymentUI
  - Hiển thị các tùy chọn phương thức thanh toán cho nhân viên (nhận trực tiếp, bưu điện, chuyển khoản).
  - Nhận thông tin đầu vào từ nhân viên, như địa chỉ bưu điện (khi chọn phương thức bưu điện) hoặc thông tin ngân hàng (khi chọn phương thức chuyển khoản).
  - Hiển thị thông báo xác nhận hoặc lỗi cho nhân viên sau khi xử lý.
PaymentController
  - Nhận yêu cầu chọn phương thức thanh toán từ PaymentUI.
  - Kiểm tra và yêu cầu thông tin bổ sung nếu cần, dựa trên phương thức thanh toán được chọn (ví dụ, yêu cầu địa chỉ bưu điện hoặc thông tin ngân hàng).
  - Tương tác với lớp EmployeePayment để lưu thông tin phương thức thanh toán đã chọn.Truyền kết quả cập nhật thành công hoặc thông báo lỗi về PaymentUI.
Employee
  - Lưu trữ thông tin cơ bản của nhân viên, cần thiết để xác định danh tính khi chọn phương thức thanh toán.
  - Cung cấp các phương thức cần thiết để lấy thông tin nhân viên và kiểm tra tính hợp lệ của nhân viên.
EmployeePayment
  - Lưu trữ thông tin về phương thức thanh toán mà nhân viên đã chọn.
  - Lưu các thông tin bổ sung, như địa chỉ (với phương thức bưu điện) hoặc tên ngân hàng và số tài khoản (với phương thức chuyển khoản).
  - Cung cấp các phương thức để cập nhật và xác nhận thông tin thanh toán đã chọn.
5. Phân tích các lớp
a) Thuộc tính của từng lớp
PaymentUI (Boundary Class):
  - selectedMethod: Chuỗi biểu thị phương thức thanh toán đã chọn ("pick up", "mail", hoặc "direct deposit").
  - address: Chuỗi chứa địa chỉ, nếu phương thức thanh toán là "mail".
  - bankName: Chuỗi tên ngân hàng, nếu phương thức thanh toán là "direct deposit".
  - accountNumber: Chuỗi chứa số tài khoản, nếu phương thức thanh toán là "direct deposit".
PaymentController (Control Class):
  - employee: Đối tượng Employee đại diện cho nhân viên thực hiện lựa chọn.
  - payment: Đối tượng EmployeePayment đại diện cho thông tin thanh toán của nhân viên.
Employee (Entity Class):
  - employeeId: ID duy nhất của nhân viên.
  - name: Tên nhân viên.
  - position: Chức vụ của nhân viên.
EmployeePayment (Entity Class):
  - paymentMethod: Chuỗi phương thức thanh toán ("pick up", "mail", hoặc "direct deposit").
  - mailingAddress: Chuỗi địa chỉ nhận qua thư, nếu phương thức là "mail".
  - bankName: Tên ngân hàng, nếu phương thức là "direct deposit".
  - accountNumber: Số tài khoản ngân hàng, nếu phương thức là "direct deposit".
  - status: Trạng thái thanh toán (có thể là "active", "pending", v.v.).
b) Quan hệ giữa các lớp
  - PaymentUI ↔ PaymentController: PaymentUI tương tác với PaymentController để gửi phương thức thanh toán được chọn và nhận lại kết quả xác nhận hoặc lỗi.
  - PaymentController ↔ Employee: PaymentController có quan hệ với Employee để truy cập và xác minh thông tin nhân viên thực hiện lựa chọn phương thức thanh toán.
  - PaymentController ↔ EmployeePayment: PaymentController cũng liên kết với EmployeePayment để cập nhật thông tin thanh toán mới và xác nhận phương thức thanh toán.

c) Biểu đồ lớp
![](https://www.planttext.com/api/plantuml/png/h9DDJiCm48NtEONLLI8r5-W22G6BB2X84GTmusbhrN_oE48HucGiE19Nm4cSD7P0RCWgyOpdVVDcylNnYHUkYDK8MICe8dccdGJbNYhobX7_b0H1GEE0FO8xQxOZjRDSdKAGCcO1CJazK7NPKmbfSjFeLhbzAmzWenWXZACHj0loJyPnhJ0lGlG4hWuO8MEaoOka39xrwvrMHsubxKlawAXhPxuYUy_YHdsoire8i7F388tG7NZwX_0M0cQySZqFDIRjWJ3cav5fKplDI1XIymNLL7a5KwNEgxM_HYFlcquyyUPDPU_1KIvmOTjAEK3D06RPJo8eVJ7_TVi_I-1NBHfMm6yDesx2gjHH9wPkqoNS3jAByAZuon3gGJDsvFeJbEND3vko8viM0JVPEjHVc8VeyxouH_ixTxAzBpqqx6zy0m00__y30000)
d) Giải thích biểu đồ lớp
  - PaymentUI: Đây là lớp giao diện, chứa các thuộc tính về phương thức thanh toán đã chọn và thông tin bổ sung như địa chỉ hoặc thông tin ngân hàng. PaymentUI chịu trách nhiệm thu thập đầu vào từ nhân viên và hiển thị kết quả sau khi PaymentController xử lý.
  - PaymentController: Lớp điều khiển này quản lý quá trình xử lý chọn phương thức thanh toán. Nó chứa tham chiếu tới Employee (để truy xuất thông tin nhân viên) và EmployeePayment (để lưu thông tin thanh toán của nhân viên).
  - Employee: Lớp này đại diện cho nhân viên đang thực hiện lựa chọn phương thức thanh toán, chứa các thuộc tính cơ bản của nhân viên như ID, tên, và chức vụ.
  - EmployeePayment: Lớp lưu trữ thông tin thanh toán của nhân viên, bao gồm phương thức thanh toán và các thuộc tính liên quan. Lớp này kết nối với PaymentController để lưu trữ và quản lý thông tin thanh toán.

# Code java mô phỏng ca sử dụng Maintain Timecard.
import java.util.ArrayList;
import java.util.Date;
import java.util.Scanner;

// Lớp đại diện cho thông tin của một nhân viên
class Employee {
    private String employeeId;
    private String name;

    public Employee(String employeeId, String name) {
        this.employeeId = employeeId;
        this.name = name;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public String getName() {
        return name;
    }
}

// Lớp đại diện cho thông tin thẻ chấm công (timecard)
class Timecard {
    private String employeeId;
    private Date date;
    private float hoursWorked;

    public Timecard(String employeeId, Date date, float hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public Date getDate() {
        return date;
    }

    public float getHoursWorked() {
        return hoursWorked;
    }

    @Override
    public String toString() {
        return "Timecard{" +
                "employeeId='" + employeeId + '\'' +
                ", date=" + date +
                ", hoursWorked=" + hoursWorked +
                '}';
    }
}

// Lớp đại diện cho bộ điều khiển quản lý thẻ chấm công
class TimecardController {
    private ArrayList<Timecard> timecards = new ArrayList<>();

    // Phương thức để ghi lại thông tin thẻ chấm công
    public void addTimecard(String employeeId, Date date, float hoursWorked) {
        Timecard timecard = new Timecard(employeeId, date, hoursWorked);
        timecards.add(timecard);
        System.out.println("Timecard đã được ghi nhận: " + timecard);
    }

    // Phương thức để xem thẻ chấm công của nhân viên
    public void viewTimecards(String employeeId) {
        System.out.println("Danh sách thẻ chấm công của nhân viên ID: " + employeeId);
        for (Timecard tc : timecards) {
            if (tc.getEmployeeId().equals(employeeId)) {
                System.out.println(tc);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TimecardController timecardController = new TimecardController();

        // Danh sách nhân viên mẫu
        Employee employee1 = new Employee("E001", "John Doe");
        Employee employee2 = new Employee("E002", "Jane Smith");

        // Ghi thẻ chấm công cho nhân viên
        System.out.println("Nhập số giờ làm việc của nhân viên " + employee1.getName() + ":");
        float hoursWorked1 = scanner.nextFloat();
        timecardController.addTimecard(employee1.getEmployeeId(), new Date(), hoursWorked1);

        System.out.println("Nhập số giờ làm việc của nhân viên " + employee2.getName() + ":");
        float hoursWorked2 = scanner.nextFloat();
        timecardController.addTimecard(employee2.getEmployeeId(), new Date(), hoursWorked2);

        // Xem thẻ chấm công
        System.out.println("\nDanh sách thẻ chấm công của " + employee1.getName() + ":");
        timecardController.viewTimecards(employee1.getEmployeeId());

        System.out.println("\nDanh sách thẻ chấm công của " + employee2.getName() + ":");
        timecardController.viewTimecards(employee2.getEmployeeId());

        scanner.close();
    }
}
