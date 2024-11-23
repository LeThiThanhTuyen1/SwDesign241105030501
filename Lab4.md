# **Thiết kế các ca sử dụng cho hệ thống "Payroll System"**

## **I. Ca sử dụng: Maintain Timecard**

### **1. Mô tả sự tương tác giữa các đối tượng thiết kế**
**Tác nhân liên quan:**
- **Employee (Nhân viên):** Người sử dụng hệ thống để nhập giờ làm việc.
- **Project Management (Quản lý dự án):** Quản lý thông tin liên quan đến các mã chi phí và dự án.

**Các đối tượng chính trong hệ thống:**
- **TimecardUIHandler:** Giao diện xử lý nhập liệu cho nhân viên.
- **TimecardService:** Xử lý nghiệp vụ liên quan đến Timecard.
- **Database (DataStore):** Lưu trữ thông tin Timecard.

### **2. Đơn giản hóa sơ đồ trình tự bằng hệ thống con**

**Sơ đồ trình tự:**

![](https://www.planttext.com/api/plantuml/png/b5FDIWCn4BxFKmmzwQ4lKAWKggXGYz0AWdX8qs5tTPFKRBRGetZm83w122tYpO87GTX5UbZmFV84leBPKhT_5ZI7C4c-RxwPRyXNEgb5XcaJYn0WkWmaQXKHW0bCI5Xg1u8uqrqiOukkOfASS3TWdcQY1C2uKHhtH2zK0oBeg5XscHxCQIU71qnsGz8bP14M9-1A6gt2ER15kXzmci9cyIpxiLONnCqHaymZGT80LAlOz6qoxg4NsFGHmsmeiE_2MuxLAlpKW-MTkMHb8mKAJ4wOYLVmrAPZ1_l0me8jaxq8z9LDtZaQcumK2fi-1Dim8-NyjN8hsB39ym2xJFeOPIFkOzrdsYDing93Ee8r2fON2sbhcpnXtwRNgyH2ThdH0zVMZKJZs_HkbRB1cxh3tijbCFQp8Sh_cTRuV8qBmwQ3sdSs1dCFtNXOQ71XdJLjCedHMyAT0-Hlluiifvm2_-A4yRCtwM4dStDpyT2DW-StGDALMdDx_WU-0G00__y30000)

### **3. Mô tả hành vi lưu trữ**

**Các hành vi lưu trữ liên quan:**
- **Nếu Timecard chưa tồn tại:**
  - **TimecardService** tạo một bản ghi Timecard mới với thông tin nhân viên và ngày làm việc.
- **Nếu Timecard đã tồn tại:**
  - **TimecardService** cập nhật thông tin giờ làm việc vào bản ghi hiện tại.

### **4. Tinh chỉnh mô tả luồng sự kiện**

**Nhập giờ làm việc:**
1. Nhân viên sử dụng **TimecardUIHandler** để nhập mã chi phí và số giờ làm việc.
2. **TimecardService** kiểm tra và xác minh tính hợp lệ của dữ liệu.
3. Nếu hợp lệ, thông tin được lưu vào **Database**.

**Lưu và Gửi Timecard:**
1. Khi nhân viên hoàn tất nhập liệu, họ nhấn nút "Lưu" hoặc "Gửi".
2. **TimecardService** thực hiện lưu thông tin vào **Database**.
3. Nếu là "Gửi," Timecard được đánh dấu là hoàn chỉnh và gửi đến quản lý dự án.

### **5. Hợp nhất các lớp và hệ thống con**

- **TimecardUIHandler** và **TimecardService** có thể được gộp thành một lớp xử lý toàn diện nếu quy trình đơn giản.
- Phân quyền rõ ràng cho các thành phần: UI chỉ tương tác, Service chịu trách nhiệm chính cho logic.

## **II. Ca sử dụng: Run Payroll**

### **1. Mô tả sự tương tác giữa các đối tượng thiết kế**
**Tác nhân liên quan:**
- **SystemClock:** Cung cấp thời gian hiện tại để xác định kỳ trả lương.
- **Printer:** Xuất hóa đơn lương (pay slip) cho nhân viên.
- **BankSystem:** Thực hiện giao dịch chuyển khoản lương.

**Các đối tượng chính trong hệ thống:**
- **PayrollService:** Xử lý nghiệp vụ trả lương.
- **Database (Employee & Timecard):** Lưu trữ thông tin nhân viên và dữ liệu giờ làm việc.

### **2. Đơn giản hóa sơ đồ trình tự bằng hệ thống con**

**Sơ đồ trình tự:**

![](https://www.planttext.com/api/plantuml/png/b5InRjH04EttAqPkGegG_gH3aU-G8W7HGIXeZMzbMxUtUwpNfxX45AcG4b4XcXW9HK94ILglK8eztN_i5_0BpFfix7CK48stc7tlpRnvwr_wxY1LWLJPd16IpX8EKgIK49KeHi5xcUMWfFd1Or3c2hziVRCkU0HxSBmkO7LkzITGcIqlEIYhRpr2zdT8MvedY8cj_XZ0kuUebbP_II0qHGWgDXTOMSIES41G94yLdO-O26S3y6rvhHnnUPbrw1xZlKcGIy7OI73bJYe7i3fBh7wVmIp6ymD7W2cQ1awilW9cVZOzE8gdymKJEQNZG0LlWvJ2qbmql1CfGfgc0cdVDD2frTV0aFiq0nwRhnoMYVdEAzWVsfrz82G8bP3WhSxG4PmtTiRWvnJ7jVgSHnu4QNVI1l3253aal2fFPC8LbKtfi0C77ZbrPzs6oW_uR4D7meqXuFbMVqRhjYtPsaC5RGqaqyO7RtGyVWv7xOZLpR5FACUKv3LttzAwwzetGeR3X_RNYyDmI3fUmDuJw6vLoIIAg7oLyNerZtOhxjSI-KumYDzKjO5-ErihGecMqocC_G4iDhqsj64c9Gw8QQ2xlTkTD7Hb-o7ejr3r-SoMTyhbl0p_Qa5N4IMtti6Xm5NZStEYzqHwm3et_mTg0_GF73cWVEf-7Ry1003__mC0)

### **3. Mô tả hành vi lưu trữ**

**Các hành vi lưu trữ:**
1. **PayrollService** lưu kết quả tính toán lương vào **Database**.
2. Cập nhật trạng thái của nhân viên (đã trả lương hay chưa).

### **4. Tinh chỉnh mô tả luồng sự kiện**

**Tính toán và trả lương:**
1. **PayrollService** lấy danh sách nhân viên và thông tin giờ làm việc.
2. Thực hiện tính toán lương dựa trên số giờ làm việc, mức lương và các khoản phụ cấp.
3. Lưu kết quả vào cơ sở dữ liệu.

**In phiếu lương và chuyển khoản:**
1. **PayrollService** gửi thông tin lương đến **Printer** để in phiếu lương.
2. Đồng thời, gửi dữ liệu đến **BankSystem** để thực hiện chuyển khoản.

### **5. Hợp nhất các lớp và hệ thống con**

- **PayrollService** có thể chịu trách nhiệm chính cho tính toán và tương tác với **Printer** và **BankSystem**.
- Đơn giản hóa giao tiếp giữa **PayrollService** và **SystemClock** bằng cách tích hợp module thời gian.

## **III. Login**

### **1. Biểu đồ ca sử dụng**
![](https://www.planttext.com/api/plantuml/png/X9112i8m44NtESNGbLru0HTI5rqK58MY-o6Trc2Qo2GgHJoP2u_a5Kni4HJ5MGtyzpx3tA-tp7baVsYrS3jbWAqZWT9RXcJjY1D01t4HWabwD8qcI5ROiTKQoivvQXCu2mWJCHYFfp1Qxid0t3QXi32Uk4P9wGUJn-05rPPRzCgQL3ovdt4lRr2h2Zszcr7ixQzvhywa9EU6qrEOG573CU9_pN9hJv0pXzyiGWKsDEZAz0KN8J8oLNpc0m00__y30000)

### **2. Giải thích**
**Tên ca sử dụng**: Login

**Tác nhân**: Nhân viên, Quản lý

**Mô tả**: Tác nhân nhập tên đăng nhập và mật khẩu để truy cập hệ thống.

**Tiền điều kiện**: Tác nhân đã có tài khoản trong hệ thống.

**Luồng sự kiện chính**:
  - Tác nhân mở giao diện đăng nhập.
  - Tác nhân nhập tên đăng nhập và mật khẩu.
  - Hệ thống kiểm tra tính hợp lệ của thông tin đăng nhập.
    - Nếu thông tin hợp lệ, hệ thống cho phép truy cập.
    - Nếu thông tin không hợp lệ, hệ thống thông báo lỗi và yêu cầu nhập lại.

**Hậu điều kiện**: Tác nhân đăng nhập thành công và có quyền sử dụng hệ thống.

**Lý do thiết kế**: Ca sử dụng này là cơ bản và cần thiết cho mọi hệ thống quản lý. Đăng nhập đảm bảo chỉ những người có quyền mới truy cập được hệ thống, đáp ứng yêu cầu về bảo mật và kiểm soát truy cập.
