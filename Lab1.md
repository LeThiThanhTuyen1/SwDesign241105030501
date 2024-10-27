# Tài liệu hợp nhất phân tích hệ thống Payroll System

## 1. Kiến trúc đề xuất:

Kiến trúc 3 tầng (Three-tier architecture) là một trong những kiến trúc phổ biến và hiệu quả cho các hệ thống lớn như hệ thống tính lương (Payroll System). Kiến trúc này giúp phân tách rõ ràng giữa các thành phần, đảm bảo tính linh hoạt, bảo trì dễ dàng và khả năng mở rộng cao. Các thành phần chính trong kiến trúc bao gồm:

Các tầng trong hệ thống:
  - Tầng giao diện (Presentation Layer): Đây là tầng người dùng tương tác trực tiếp với hệ thống thông qua các ứng dụng desktop, web hoặc mobile. Chức năng chính của tầng này là hiển thị thông tin, thu thập và xác thực dữ liệu nhập từ người dùng.
  - Tầng xử lý nghiệp vụ (Business Logic Layer): Tầng này chứa các quy tắc và logic nghiệp vụ của hệ thống. Mọi logic liên quan đến tính lương, quản lý thẻ thời gian (timecard), chọn phương thức thanh toán đều được xử lý ở đây. Tầng này cũng đảm bảo tính nhất quán dữ liệu và thực hiện các kiểm tra nghiệp vụ.
  - Tầng dữ liệu (Data Layer): Tầng này chịu trách nhiệm tương tác với cơ sở dữ liệu để lưu trữ và truy vấn thông tin nhân viên, thẻ thời gian, thanh toán và các bảng dữ liệu liên quan.
Dữ liệu được quản lý một cách an toàn và toàn vẹn trong cơ sở dữ liệu.
    
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

## 2. Cơ chế phân tích

Các cơ chế phân tích giúp giải quyết các vấn đề phức tạp trong hệ thống. Một số cơ chế phân tích có thể áp dụng cho Payroll System là:
  - Persistency: Đảm bảo rằng thông tin về nhân viên, thanh toán, và thời gian làm việc được lưu trữ an toàn, giúp hệ thống có thể phục hồi và truy xuất dữ liệu khi cần thiết.
  - Communication (IPC and RPC): Cần thiết để các thành phần trong hệ thống có thể trao đổi dữ liệu một cách hiệu quả và chính xác, đảm bảo tính liên kết giữa các phần của hệ thống.
  - Transaction Management: Quản lý giao dịch để đảm bảo tính nhất quán trong quá trình thanh toán. Đảm bảo tính toàn vẹn của dữ liệu, đặc biệt trong các tình huống giao dịch phức tạp, như khi tính toán lương và ghi nhận thời gian làm việc.
  - Security: Đảm bảo thông tin nhân viên và các thanh toán được lưu trữ an toàn, chỉ có quyền truy cập từ những người có thẩm quyền. Đặc biệt quan trọng trong hệ thống tính lương, nơi chứa nhiều thông tin cá nhân và tài chính của nhân viên.
  - Error Handling: Quản lý các lỗi phát sinh khi giao dịch không thành công. Giúp nâng cao độ tin cậy của hệ thống và cung cấp thông tin cần thiết để sửa chữa lỗi một cách nhanh chóng.
  - Legacy interface: Đảm bảo rằng hệ thống mới có thể làm việc hiệu quả với các hệ thống cũ mà không gặp khó khăn, giúp giảm thiểu chi phí chuyển đổi và thời gian gián đoạn.

## 3. Phân tích ca sử dụng Payment
1. Mô Tả Ca Sử Dụng "Payment"
  - Tên ca sử dụng: Payment
  - Diễn giả chính: Khách hàng
  - Mô tả: Khách hàng thực hiện thanh toán cho đơn hàng của họ thông qua hệ thống. Hệ thống xử lý thanh toán và gửi thông báo cho khách hàng về trạng thái thanh toán.

2. Các Lớp Phân Tích

Boundary Class: PaymentUI
  - Mô tả: Lớp này quản lý giao diện người dùng cho việc thực hiện thanh toán.
  - Nhiệm vụ: Thu thập thông tin thanh toán từ khách hàng và hiển thị kết quả thanh toán.

Control Class: PaymentController
  - Mô tả: Lớp này xử lý logic thanh toán.
  - Nhiệm vụ: Điều phối các bước thực hiện thanh toán và tương tác giữa các lớp khác.

Entity Class: Payment
  - Mô tả: Lớp này đại diện cho thông tin thanh toán.
  - Nhiệm vụ: Lưu trữ thông tin thanh toán, chẳng hạn như số tiền, phương thức thanh toán và trạng thái thanh toán.

Entity Class: Order
  - Mô tả: Lớp này đại diện cho đơn hàng mà khách hàng đang thanh toán.
  - Nhiệm vụ: Lưu trữ thông tin chi tiết của đơn hàng.

3. Biểu Đồ Sequence
   
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/Z98nJiD044NxFSMKK7012XGf1I0Xe029rh6js8ez2-inaaj4IPKRO4MKaIYel4KAeznZJi0LcCLnx28cAMTttf__P_V7haOPUORoD57PB4OmEWkLvvCsCCupqcber4Jd67YcW5klI4Ea-qlbQoIZa_Pat9I9D4iLqxQrBMzC87UgbOIJiquCJk4wuchv21JLNpW54XyKUHW1wRh4esFLzNPWDrC4pjakuxry3n6TFq_2Nd7rKVJPx_cwH8ZgTvmAsxGDpBqpN2tWcUtBiC3EuPj39y5LgGLXEvS4wq-s2oUpo_-GYuUwz07T3WyAtj_yHSpsrL5its36rOhWANUP_dc0xIkA-IRqf9O8m_GenC3zi5y0003__mC0)

4. Nhiệm Vụ của Từng Lớp Phân Tích

PaymentUI:
  - Thu thập thông tin thanh toán từ khách hàng (số thẻ, ngày hết hạn, v.v.).
  - Hiển thị thông báo kết quả thanh toán cho khách hàng.

PaymentController:
  - Nhận thông tin thanh toán từ PaymentUI.
  - Tương tác với lớp Order để lấy thông tin đơn hàng liên quan.
  - Tạo đối tượng Payment để lưu trữ thông tin thanh toán.
  - Xác nhận thanh toán và gửi kết quả về PaymentUI.

Payment:
  - Chứa các thuộc tính như amount, paymentMethod, paymentStatus.
  - Cung cấp các phương thức để xác nhận thanh toán.

Order:
  - Chứa các thuộc tính như orderId, customerId, totalAmount.
  - Cung cấp thông tin cần thiết cho việc thanh toán.

5. Biểu đồ lớp 

![Class Diagram](https://www.planttext.com/api/plantuml/png/T94zJiGm48NxdC8b5Bb02hG8cYqG2CG1BDiRBEoPo3CkLeZ3fA14eYO51TBU8oVW2ZZ48Sh-kFDyC-yzZt-whnMn31ozA-ZPWWX8fb1E4eaxkVK6-74jNWen70jDv5ozDYojexFp4MbBZPFR3EyDHSU9lHPBhIi43kYS2PDc4r0PeimdkThmRT0cp2xxIdc-b1uZS2Ks3YMFfMRik37yXBeInC52lK0FB3dI0Wc5iB71pq7-7V-IJ7uuNDP9raAsKv4O_LwHaQMxFCXs_67peilouiYgKj2-UnUwxzvIsaC-J8qXAy6xZrqBjU3lLfredJQOcllF5ekL0Jty_oy0003__mC0)

Giải Thích Biểu Đồ Lớp

  - PaymentUI: Chịu trách nhiệm giao tiếp với người dùng để thu thập thông tin thanh toán và hiển thị kết quả.
  - PaymentController: Chịu trách nhiệm xử lý logic thanh toán. Nó tương tác với Order để lấy thông tin cần thiết và với Payment để lưu trữ thông tin thanh toán.
  - Payment: Lưu trữ các thông tin liên quan đến thanh toán, bao gồm số tiền, phương thức thanh toán và trạng thái thanh toán. Nó cung cấp phương thức để xác nhận thanh toán.
  - Order: Chứa thông tin về đơn hàng mà khách hàng đang thanh toán. Nó cung cấp phương thức để lấy thông tin chi tiết về đơn hàng.

## 4. Phân tích ca sử dụng Maintain Timecard
1. Mô Tả Ca Sử Dụng "Maintain Timecard"
  - Tên ca sử dụng: Maintain Timecard
  - Diễn giả chính: Nhân viên (Employee)
  - Mô tả: Nhân viên có thể xem, thêm, sửa đổi và xóa thông tin thời gian làm việc của họ thông qua hệ thống. Hệ thống lưu trữ và quản lý thông tin thời gian làm việc cho các nhân viên.

2. Các Lớp Phân Tích

Boundary Class: TimecardUI
  - Mô tả: Lớp này quản lý giao diện người dùng cho việc quản lý thời gian làm việc.
  - Nhiệm vụ: Hiển thị thông tin thời gian làm việc cho nhân viên và cho phép họ thêm, sửa đổi hoặc xóa thông tin.

Control Class: TimecardController
  - Mô tả: Lớp này xử lý logic quản lý thời gian làm việc.
  - Nhiệm vụ: Điều phối các bước thực hiện thao tác với thông tin thời gian làm việc và tương tác giữa các lớp khác.

Entity Class: Timecard
  - Mô tả: Lớp này đại diện cho thông tin thời gian làm việc của nhân viên.
  - Nhiệm vụ: Lưu trữ thông tin thời gian vào và ra của nhân viên, cùng với ngày tháng và trạng thái.

Entity Class: Employee
  - Mô tả: Lớp này đại diện cho thông tin nhân viên.
  - Nhiệm vụ: Lưu trữ thông tin chi tiết của nhân viên, như ID, tên, và các thông tin liên quan khác.
    
3. Biểu Đồ Sequence

![Diagram](https://www.planttext.com/api/plantuml/png/f9DFIWCn5CRtESLRseKNS2658YguZ52Nqqpe1FEdP3A5MHONBZo222qYGg4xLvE5Yvma9_0APWoTPZDsq5qItlVxllSU-RAVuz9asbI2e_AUIT2gf2WZHccu40kkQahHJ5KoptGDc0bACftVNYEYfD6ATq-JUETK8oeDCuVY_Rt3eVq9JiyJ99p1b0emXRSl3EOiay3TMi2IUVj8JaOeAKs41-C0k7FR2eXltgl0SHzo3YRqb20JJ29CS05ouvkt-hY-DmJMldc5fRUhluRu6SPLwFiXwfwEW-9GkiaEbVVl0XTk-yzjN7gxOptU8BnzPaFMWNspKKCflLccRaD05hxPjO3Gsh0bu6WxSp72MXP0sfVV9Zy99elePPBSGJAcCcz_sZS0003__mC0)

4. Nhiệm Vụ của Từng Lớp Phân Tích

TimecardUI:
  - Hiển thị thông tin thời gian làm việc cho nhân viên.
  - Cung cấp giao diện để thêm, sửa đổi hoặc xóa thông tin thời gian làm việc.

TimecardController:
  - Nhận yêu cầu từ TimecardUI và điều phối các thao tác cần thiết.
  - Tương tác với lớp Timecard để lấy, thêm, sửa đổi hoặc xóa thông tin thời gian làm việc.

Timecard:
  - Chứa các thuộc tính như employeeId, date, timeIn, timeOut, status.
  - Cung cấp các phương thức để thêm, sửa đổi và lấy thông tin thời gian làm việc.

Employee:
  - Chứa các thuộc tính như employeeId, name, position.
  - Cung cấp thông tin liên quan đến nhân viên để hỗ trợ việc quản lý thời gian làm việc.

5. Biểu Đồ Lớp
   
![Diagram](https://www.planttext.com/api/plantuml/png/j98nJiGm44Nxd69AA7A156Wbe4X50mUmub7MmXb7zWIqGXncaRP1GgAW8WL5fBr7Ji0Li9KrEAjb9GfSsFBJpFm_zdps7ml7mdBNwCpTAW9h76QL5ix1jMgm4bRUbF2GGLXt2kyZTIUd4nHIHXPHrqh1k4ybQfpHnsnFwTmGMwCrsgXO8_-du4ucnwRLPeLOoW8KyGH3oGB2FjtP9vLKG3X_o5N7AVAloPqhmB5LLF_HSD9jwlPov-weMn8DpcJprZZ5oj3SZDU8zIwGXT9kaaf-Ey_F3ds9hpFsBo37VkEB7GX8ytmqRr-tQwg1XtNrM_XtQmNeyNsp0buERo77Zo8jXoVoCpSyKxP0ac56lm000F__0m00)

6. Giải Thích Biểu Đồ Lớp
  - TimecardUI: Chịu trách nhiệm giao tiếp với nhân viên để quản lý thông tin thời gian làm việc.
  - TimecardController:Chịu trách nhiệm xử lý logic quản lý thời gian làm việc, bao gồm việc lấy, thêm, sửa đổi và xóa thông tin thời gian làm việc.
  - Timecard: Lưu trữ các thông tin liên quan đến thời gian làm việc, bao gồm ID nhân viên, ngày, giờ vào, giờ ra và trạng thái. Cung cấp phương thức để quản lý thông tin thời gian.
  - Employee: Lưu trữ thông tin chi tiết của nhân viên. Cung cấp phương thức để lấy thông tin liên quan đến nhân viên.

## 5. Hợp nhất kết quả phân tích
  - Lớp Employee: Được sử dụng trong cả hai ca sử dụng "Maintain Timecard" và "Payment", do đó, chỉ có một lớp Employee duy nhất.
  - Lớp TimecardUI và PaymentUI: Các lớp này quản lý giao diện cho các chức năng khác nhau của hai ca sử dụng.
  - Lớp TimecardController và PaymentController: Các lớp điều khiển riêng biệt để xử lý logic cho hai ca sử dụng khác nhau.
  - Lớp Timecard: Lưu trữ thông tin thời gian làm việc cho nhân viên.
  - Lớp Payment: Lưu trữ thông tin về thanh toán cho nhân viên.

Class diagram

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIeN5rT1Od9sOdggWf9lOcPU2H0hX6JcfYOd5gKeALHpAG11SavYSJ5SDDHJmSOcARyqBoMngDBE3ge61C2CMYuiUfppyqgAydDoKek0UfCX72Ijk3K2bQVcbMIM4BB8DRSW9xyoDHMl-beapmOaLkO2LQ9w4If8YW-XMWXu48_E4amdWrsA5DowkdROGj9AeVZXxhKAAGztByrBvqAu7QGSqrcegh4OXsmBK7N9iGt75kQbAvGSNfZCXMaSaYKbwAfn60wF8ok5d8UxbbOgb6GStWBI0qnoUHc75-Kfb6KUNfM7mp9YTNCvfEQbWD8u0000__y30000)
