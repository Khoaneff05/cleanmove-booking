# 1. USE CASE CHI TIẾT

## 1.1. Mục đích

Phân rã các chức năng chính của hệ thống thành các Use Case chi tiết, làm cơ sở cho việc đặc tả chức năng, thiết kế cơ sở dữ liệu và thiết kế giao diện.

## 1.2. Danh sách Actor

| Actor         | Mô tả                                                                 | 
| ------------- | --------------------------------------------------------------------- | 
| Khách hàng	| Người sử dụng hệ thống để tìm kiếm, đặt lịch và sử dụng dịch vụ.      | 
| Nhân viên	    | Người tiếp nhận, xử lý lịch đặt và quản lý dịch vụ được phân quyền.   | 
| Admin	        | Người quản trị toàn bộ hệ thống, tài khoản, dịch vụ và dữ liệu.       | 

## 1.3. Use Case của Khách hàng

### UC01. Đăng ký tài khoản

Khách hàng tạo tài khoản mới bằng cách cung cấp thông tin cần thiết.

### UC02. Đăng nhập

Khách hàng đăng nhập vào hệ thống để sử dụng các chức năng dành cho tài khoản.

### UC03. Quản lý thông tin cá nhân

Khách hàng xem và cập nhật thông tin cá nhân.

### UC04. Xem danh sách dịch vụ

Khách hàng xem các dịch vụ đang được cung cấp.

### UC05. Xem chi tiết dịch vụ

Khách hàng xem thông tin chi tiết, giá và thời lượng của dịch vụ.

### UC06. Đặt lịch dịch vụ

Khách hàng lựa chọn dịch vụ, thời gian và thông tin cần thiết để tạo lịch đặt.

### UC07. Xem lịch đã đặt

Khách hàng xem danh sách và trạng thái các lịch đã đặt.

### UC08. Hủy lịch

Khách hàng hủy lịch đặt theo các điều kiện được hệ thống quy định.

### UC09. Đánh giá dịch vụ

Khách hàng đánh giá dịch vụ sau khi hoàn thành.

## 1.4. Use Case của Nhân viên

### UC10. Đăng nhập

Nhân viên đăng nhập vào hệ thống bằng tài khoản được cấp.

### UC11. Quản lý lịch đặt

Nhân viên xem và xử lý các lịch đặt của khách hàng.

### UC12. Xác nhận lịch đặt

Nhân viên xác nhận hoặc từ chối lịch đặt dựa trên tình trạng thực tế.

### UC13. Cập nhật trạng thái lịch

Nhân viên cập nhật trạng thái lịch trong quá trình cung cấp dịch vụ.

### UC14. Quản lý thông tin dịch vụ

Nhân viên xem và cập nhật thông tin dịch vụ theo quyền được cấp.

### UC15. Xem thông tin khách hàng

Nhân viên xem các thông tin cần thiết của khách hàng phục vụ quá trình cung cấp dịch vụ.

## 1.5. Use Case của Admin

### UC16. Quản lý tài khoản

Admin xem, thêm, sửa, khóa hoặc phân quyền tài khoản người dùng.

### UC17. Quản lý dịch vụ

Admin thêm, sửa, xóa và cập nhật thông tin dịch vụ.

### UC18. Quản lý lịch đặt

Admin xem và xử lý toàn bộ lịch đặt trong hệ thống.

### UC19. Quản lý nhân viên

Admin quản lý thông tin và quyền hạn của nhân viên.

### UC20. Quản lý đánh giá

Admin xem và xử lý các đánh giá của khách hàng.

### UC21. Xem báo cáo và thống kê

Admin xem các thông tin thống kê liên quan đến lịch đặt, dịch vụ và hoạt động của hệ thống.
