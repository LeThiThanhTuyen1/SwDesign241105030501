**Tài liệu hợp nhất phân tích hệ thống Payroll System**

**1. Kiến trúc đề xuất:**
Kiến trúc 3 tầng (Three-tier architecture) là một trong những kiến trúc phổ biến và hiệu quả cho các hệ thống lớn như hệ thống tính lương (Payroll System). Kiến trúc này giúp phân tách rõ ràng giữa các thành phần, đảm bảo tính linh hoạt, bảo trì dễ dàng và khả năng mở rộng cao. Các thành phần chính trong kiến trúc bao gồm:

Các tầng trong hệ thống:
  - Tầng giao diện (Presentation Layer): Đây là tầng người dùng tương tác trực tiếp với hệ thống thông qua các ứng dụng desktop, web hoặc mobile. Chức năng chính của tầng này là hiển thị thông tin, thu thập và xác thực dữ liệu nhập từ người dùng.
  - Tầng xử lý nghiệp vụ (Business Logic Layer): Tầng này chứa các quy tắc và logic nghiệp vụ của hệ thống. Mọi logic liên quan đến tính lương, quản lý thẻ thời gian (timecard), chọn phương thức thanh toán đều được xử lý ở đây. Tầng này cũng đảm bảo tính nhất quán dữ liệu và thực hiện các kiểm tra nghiệp vụ.
  - Tầng dữ liệu (Data Layer): Tầng này chịu trách nhiệm tương tác với cơ sở dữ liệu để lưu trữ và truy vấn thông tin nhân viên, thẻ thời gian, thanh toán và các bảng dữ liệu liên quan.
Dữ liệu được quản lý một cách an toàn và toàn vẹn trong cơ sở dữ liệu.
  - 
Giải thích:
  - Kiến trúc phân lớp cho phép phân tách các mối quan tâm, dễ bảo trì và mở rộng. Kiến trúc này có thể mở rộng thêm các dịch vụ khác (ví dụ: báo cáo, thống kê lương) mà không ảnh hưởng đến các phần còn lại.
  - Kiến trúc 3 tầng cho phép tách biệt rõ ràng giữa giao diện, xử lý nghiệp vụ và lưu trữ dữ liệu. Điều này giúp tăng tính modular, dễ bảo trì và phát triển.
  - Các lớp được tách biệt giúp bảo vệ dữ liệu quan trọng, giảm rủi ro bảo mật bằng cách hạn chế quyền truy cập trực tiếp đến cơ sở dữ liệu.
  - Có thể dễ dàng thay đổi logic nghiệp vụ hoặc giao diện mà không ảnh hưởng đến dữ liệu, và ngược lại.
  - Với kiến trúc phân tầng, các thành viên trong nhóm phát triển có thể tập trung vào các phần riêng biệt mà không ảnh hưởng đến nhau. Ví dụ, một lập trình viên frontend có thể làm việc ở tầng giao diện, trong khi một lập trình viên backend có thể tập trung vào tầng xử lý nghiệp vụ và cơ sở dữ liệu.

Ý nghĩa của từng thành phần trong kiến trúc:
  - Presentation Layer (Tầng giao diện): Cung cấp giao diện người dùng để tương tác với hệ thống. Kiểm tra tính hợp lệ của dữ liệu người dùng nhập. Gửi yêu cầu đến tầng nghiệp vụ và nhận phản hồi để hiển thị.
  - Business Logic Layer (Tầng xử lý nghiệp vụ): Thực hiện các quy tắc tính toán, logic nghiệp vụ liên quan đến quản lý nhân viên, tính lương và thanh toán. Quản lý logic xử lý liên quan đến thẻ thời gian (timecard), thanh toán và bảo mật thông tin nhân viên. Kiểm tra các điều kiện nghiệp vụ trước khi tương tác với dữ liệu.
  - Data Layer (Tầng dữ liệu): Tương tác với cơ sở dữ liệu để lưu trữ thông tin nhân viên, thời gian làm việc, và thanh toán. Đảm bảo tính toàn vẹn và bảo mật cho dữ liệu. Trả về kết quả truy vấn cho tầng nghiệp vụ.

![Package Diagram](https://www.planttext.com/api/plantuml/png/R94nIyGm68Rt_8gNJdV3JQv7kQk1Konou2c2EeGQUk5wQKdIeOYJmys7epYAqw6h3N93nV-HN-1VCDqgDl11-F9-pyD7Vkn-eWrJfbndHA-4XCer9qQOZ2CIpZwK-Dew-uWJuUgzX55DdM248sStC4jdjp95C6ULohCCPvKsV1rWS83CsQTYI4Z1aXLBEOA5grzzTYPO3kh96ndWZi2Vg_4uOnLNOTXznMdw_Uxiim1jFcHwBGTpnJMNXXcHIyJjnF06J6DsVapk_vikdTqXRZuzQDaI2rmu-z8ZxGzwOLHg8RdMYFDK95rb5FSPgRDlY5j4sQDPgBB2eQjtHJVeDPGPreNJQGltMs4KUXE8Bt-ZKn1VVtfjY909bxVj1_u2003__mC0)

**2. Cơ chế phân tích**
Các cơ chế phân tích giúp giải quyết các vấn đề phức tạp trong hệ thống. Một số cơ chế phân tích có thể áp dụng cho Payroll System là:
  - Persistency: Đảm bảo rằng thông tin về nhân viên, thanh toán, và thời gian làm việc được lưu trữ an toàn, giúp hệ thống có thể phục hồi và truy xuất dữ liệu khi cần thiết.
  - Communication (IPC and RPC): Cần thiết để các thành phần trong hệ thống có thể trao đổi dữ liệu một cách hiệu quả và chính xác, đảm bảo tính liên kết giữa các phần của hệ thống.
  - Transaction Management: Quản lý giao dịch để đảm bảo tính nhất quán trong quá trình thanh toán. Đảm bảo tính toàn vẹn của dữ liệu, đặc biệt trong các tình huống giao dịch phức tạp, như khi tính toán lương và ghi nhận thời gian làm việc.
  - Security: Đảm bảo thông tin nhân viên và các thanh toán được lưu trữ an toàn, chỉ có quyền truy cập từ những người có thẩm quyền. Đặc biệt quan trọng trong hệ thống tính lương, nơi chứa nhiều thông tin cá nhân và tài chính của nhân viên.
  - Error Handling: Quản lý các lỗi phát sinh khi giao dịch không thành công. Giúp nâng cao độ tin cậy của hệ thống và cung cấp thông tin cần thiết để sửa chữa lỗi một cách nhanh chóng.
  - Legacy interface: Đảm bảo rằng hệ thống mới có thể làm việc hiệu quả với các hệ thống cũ mà không gặp khó khăn, giúp giảm thiểu chi phí chuyển đổi và thời gian gián đoạn.

**3. Phân tích ca sử dụng Payment**
Lớp phân tích cho ca sử dụng Payment:
  - Employee: Lớp chứa thông tin nhân viên.
  - Payment: Xử lý thanh toán lương cho nhân viên.
  - PayrollManager: Quản lý tính toán lương và xử lý thanh toán.
  - Database: Quản lý truy xuất và lưu trữ thông tin thanh toán.

**Biểu đồ tuần tự (Sequence Diagram) cho "Payment"**

![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T94nJWCn44NxFSMKK7012fG2kY0X58gK9h7MgtZ7mHv7SXbHK72AW11I94GAgdMHmjBUmoVW2imYWHB2DYx6Vk_FZ3_ZTk18MFArBjoiGh36oQ8G4p8MRfoqHNV0oHbSYM2DrfS2HScLKnYdjOT9Rbuzg2h7UmHIEJw2RZVj2ikZu-8FmfABUgvDaF9QpeshE2EmQ9YRby1m-i0IY7j0bPuG5bLQ8rl-OTXqBaZS2YUP7raVOC4It94m-FkaBtXaS_FCP5p2DCTtq3p6W--DFDZ03j_R_U4Ek59Bf8vFRwY0J5hX_jQ-x_U77BOR3xFSR0dkV1TBIlp030qaJhi__0800F__0m00)

**Biểu đồ lớp (Class Diagram) cho "Payment"**

![Class Diagram](https://www.planttext.com/api/plantuml/png/R52z3e903DxlAJhgm0imEU30O6Ba2IeMGYntv5e6Odmo1n_9Lv3pm1XaxDVlhtqzdZjHzDgtREJQMF1Eo9YIKGJsRSTk88AR0G2QfZnBeR4Q88ijfL2eRsmTPa56FwHGiKCrzzddY4DBLgDDYLpsZ4h5XxpP1h3phYIHYJXYlrhlc0zeiIQ_i5ZXpvrFr3bfrFaXQchIUPNRoaN9zy0aMGIPHMuaXB2LpN-cMQan4ZDKFEFuu1tPItZv6m00__y30000)

**4. Phân tích ca sử dụng Maintain Timecard**
Các lớp phân tích:
  - Timecard: Đại diện cho một bản ghi bảng công.
  - Employee: Nhân viên liên quan đến bảng công.
  - TimecardManager: Quản lý bảng công của nhân viên, xác thực giờ công.
  - Database: Lưu trữ thông tin bảng công.

**Biểu đồ tuần tự (Sequence Diagram) cho "Maintain Timecard":**

![Diagram](https://www.planttext.com/api/plantuml/png/T94z2i8m5CVtdEBHtGiuY8FYeejqS4tRq0RRrvAaGaSdpw75HH0Ld9h1eU0zSWAlO3BuWTJflU7z_X_9Gz-6Kb6XoYmbSiaHH2uPeQ7A1Oop8iqhniXhWTu0V9wna8feHf76J40Vl8dHHmw1QMgC8Mol67lazyoIBvKvAtB9hK7bu4Mx3K4bHb_SS30e6mEJTeUmukq1FT91MhqHLJIWaZaLNvGLh4opHuYCFa7AZTwK7ddV_FNtXSrjKRt-ilzdsL7U_sIs9Ue2KklSsVyxx_H-BdzURCWmSh_m1000__y30000)

**Biểu đồ lớp (Class Diagram) cho "Maintain Timecard"**

![Diagram](https://www.planttext.com/api/plantuml/png/R90z3i8m38Ntd28Z3Br0fmvbO60196QtiKhK_5HsYbGXJiR0aRW2YKghYh9OylFxdco_dw-20r3ehH7SQYV9CmfH6s2MEziPFo3Akv1IuhVRbxdKBYJ9WSLSdW9fruZ7X9srnHf8ZTZLzyGNJosgcLCG8bV6kgOEuA116k4R69tCqt2pJIhtbTLXeSMGUTSi-uqIlz4Box_P57N4phCEdWQnbf8n7W0Ln7yLw5Jwu0S00F__0m00)

**5. Hợp nhất kết quả phân tích**
Employee là lớp trung tâm, chịu trách nhiệm quản lý và lưu trữ thông tin nhân viên. Lớp này tương tác trực tiếp với các lớp xử lý bảng chấm công và thanh toán, cụ thể là TimecardManager và PayrollManager. Cả hai thành phần này đều sử dụng chung các lớp liên quan đến lưu trữ dữ liệu như EmployeeRepository và Database.

Các thành phần chính:
  - Employee: Chứa thông tin nhân viên và liên kết với các lớp quản lý bảng chấm công và thanh toán.
  - TimecardManager: Quản lý và cập nhật bảng chấm công cho nhân viên.
  - PayrollManager: Tính toán và xử lý thanh toán lương cho nhân viên.
  - EmployeeRepository: Lớp truy cập dữ liệu cho đối tượng Employee, hỗ trợ thao tác đọc/ghi từ cơ sở dữ liệu.
  - Database: Quản lý lưu trữ dữ liệu cho hệ thống, được dùng chung bởi các repository.

**Class diagram**

![](https://www.planttext.com/api/plantuml/png/T99DJiGm38NtEOMNiEWLq4WC2nP8Y9aBU1AhYiXFITnA4PgJpO8ZSGNQAIb9f-pgFhydVtQ-Br-xo1YujqR4T-qW-4X2i6P3y8efU6FWa2AJXGOU3SO8UurjG2k4l9PFjZC-4S6d081dnw3Lz7NWe5qB3YqLPUUZPksTE6V_KLkI6DGBEcmfp363rmhwJY5Jrk_k5s50erVI4lSxz6sQH2DxCxh63akEYxn8XYJ__J-lsTxeEhSFgGYCE51kcCEMLRJ4XNA3-czSpPghAMuBTO-C9unKGdhdHfI2xQEda6RNCbxJF6oWrVhgBBLOBrciJrZwD_8B_AapOuYDzLJwwhIL9dRarFIAVm000F__0m00)
