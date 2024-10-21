**Tài liệu hợp nhất phân tích hệ thống Payroll System**

**1. Kiến trúc đề xuất:**
Hệ thống phù hợp với kiến trúc phân lớp (Layered Architecture) vì tính chất rõ ràng giữa các tầng xử lý.

Các tầng trong hệ thống:
- Tầng trình bày (Presentation Layer): Xử lý tương tác người dùng (ví dụ: nhập bảng công, xem lương).
- Tầng logic nghiệp vụ (Business Logic Layer): Tính toán lương, quản lý bảng công, xử lý thanh toán.
- Tầng truy cập dữ liệu (Data Access Layer): Quản lý việc truy xuất dữ liệu từ cơ sở dữ liệu (ví dụ: thông tin nhân viên, lịch sử thanh toán).
- Tầng cơ sở dữ liệu (Database Layer): Lưu trữ và truy xuất dữ liệu.

Giải thích:
- Kiến trúc phân lớp cho phép phân tách các mối quan tâm, dễ bảo trì và mở rộng.
- Mỗi tầng có thể được chỉnh sửa độc lập (ví dụ: thay đổi UI không ảnh hưởng đến logic tính lương).

**Biểu đồ gói (Package Diagram)**

![Package Diagram](https://www.planttext.com/api/plantuml/png/Z9CzJiD044PxdsAK2efSW0851898GGee762o7imgwrrhVr0ib8g2WbD4Y38Y1LLSK4JAFNm2hi0wi8co2XBkFFlDU-En_LLzTen5RLqkaYGn8ov1AqD9OhaL10Mo4MO4ASTCO-uZeTBNP4XQj5p97fQauJ41O0ADWTlk-iPVAJU5mBAFfLP271p-L8qRvjmEU4uCTRgkJfB9bdtg39TaJ4zbdCNmNzOLIX_LGSHGC2VGaZ_E_Ln1LMZ5F2bo1LOeHx0753prh9skVynzXXPFMEEBXpxF2w5AeXigbE5MwJAuChBXi2llr4RbC-5P6kn-sH0DnQfG3m8Q4tEMhXtfSalnhwZTFewNUGIjIrvNJnBiVLszW5ZDLrEPjK8ytfVFNzJLZCEmNhpA3DZoeqb7rAPppm9yys0va_TWrN8gjwvOydTxRpLtVj962jP_kRjJxEbfK9lzD7xjIXYxUl5c8QshTn3-wPzTA-cGJ9jVuXi00F__0m00)

**2. Cơ chế phân tích**
Các cơ chế phân tích giúp giải quyết các vấn đề phức tạp trong hệ thống. Một số cơ chế phân tích có thể áp dụng cho Payroll System là:
- Persistency: Cơ chế lưu trữ dữ liệu như thông tin nhân viên, bảng chấm công, và thanh toán.
- Transaction Management: Quản lý giao dịch để đảm bảo tính nhất quán trong quá trình thanh toán.
- Security: Bảo mật dữ liệu liên quan đến lương và chấm công
- Error Handling: Quản lý các lỗi phát sinh khi giao dịch không thành công.
- Authentication and Authorization: Xác thực và phân quyền cho các thao tác khác nhau, ví dụ: chỉ quản lý có thể duyệt và sửa đổi phương thức thanh toán.

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
