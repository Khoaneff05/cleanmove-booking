# 03. Kiểm thử chức năng hệ thống CleanMove

## 1. Mục tiêu kiểm thử

Kiểm thử chức năng nhằm xác minh các chức năng chính của hệ thống CleanMove hoạt động đúng theo yêu cầu nghiệp vụ, dữ liệu được xử lý nhất quán và API có cơ chế xác thực, phân quyền phù hợp.

Các mục tiêu cụ thể:

- Kiểm tra khả năng khởi động backend và kết nối MySQL.
- Kiểm tra API truy xuất danh sách dịch vụ.
- Kiểm tra đăng nhập và xác thực JWT.
- Kiểm tra phân quyền giữa các vai trò `admin`, `user` và `staff`.
- Kiểm tra khả năng truy xuất danh sách công việc của nhân viên.
- Kiểm tra các quy tắc xử lý booking.
- Tổng hợp kết quả kiểm thử tự động.
- Xác định các lỗi hoặc trường hợp chưa được xác minh để tiếp tục xử lý.

## 2. Phạm vi kiểm thử

Các nhóm chức năng trong phạm vi rà soát gồm:

| Nhóm              | Nội dung                                                 |
|-------------------|----------------------------------------------------------|
| Kết nối hệ thống  | Khởi động backend và kết nối database                    |
| Dịch vụ           | Truy xuất danh sách dịch vụ                              |
| Xác thực          | Đăng nhập, JWT, xử lý token không hợp lệ                 |
| Phân quyền        | Kiểm tra quyền truy cập theo vai trò                     |
| Đặt lịch          | Tạo và truy xuất booking                                 |
| Quản lý công việc | Nhân viên xem, tiếp nhận, từ chối và cập nhật trạng thái |
| Quản trị          | Kiểm tra quyền truy cập các API quản trị                 |
| Kiểm thử hồi quy  | Chạy bộ kiểm thử tự động sau thay đổi mã nguồ            |

## 3. Môi trường kiểm thử

| Thành phần                 | Cấu hình                |
|----------------------------|-------------------------|
| Hệ điều hành               | Windows                 |
| Terminal                   | PowerShell              |
| Runtime                    | Node.js                 |
| Backend framework          | Express.js 5            |
| Database                   | MySQL                   |
| Thư viện truy cập database | mysql2                  |
| Xác thực                   | JWT                     |
| Kiểm thử tự động           | Node.js Test Runner     |
| Địa chỉ backend            | `http://localhost:5000` |

Các yêu cầu HTTP được gửi trực tiếp từ PowerShell. Các bài kiểm thử tự động được thực thi trong thư mục backend bằng lệnh `npm test`.

## 4. Phương pháp kiểm thử

### 4.1. Kiểm thử thủ công API

Sử dụng HTTP request để kiểm tra:

- Mã trạng thái HTTP.
- Nội dung JSON phản hồi.
- Hành vi khi thiếu token.
- Hành vi khi token không hợp lệ.
- Hành vi khi tài khoản không đủ quyền.
- Hành vi khi tài khoản có quyền truy cập hợp lệ.

### 4.2. Kiểm thử tự động

Sử dụng Node.js Test Runner để thực thi các bài kiểm thử có sẵn trong thư mục `tests/`.

Lệnh chạy:

```powershell
npm test
```

Sau khi thay đổi middleware, controller hoặc logic nghiệp vụ, cần chạy lại bộ test để phát hiện lỗi hồi quy.

### 4.3. Quy ước đánh giá

- **Đạt:** Đã thực hiện kiểm thử và kết quả thực tế phù hợp với kỳ vọng.
- **Chưa kiểm thử:** Chưa có kết quả thực tế được ghi nhận.
- **Cần xác minh:** Đã phát hiện dữ liệu hoặc hành vi cần đối chiếu thêm với yêu cầu nghiệp vụ.

## 5. Danh sách ca kiểm thử

### 5.1. Khởi động hệ thống và truy xuất dịch vụ

| Mã   | Trường hợp kiểm thử                 | Kết quả mong đợi            | Kết quả thực tế                                    | Đánh giá     |
|------|-------------------------------------|-----------------------------|----------------------------------------------------|--------------|
| TC01 | Khởi động backend                   | Server khởi động thành công | Server chạy tại cổng 5000                          | Đạt          |
| TC02 | Kết nối MySQL                       | Kết nối thành công          | Đã ghi nhận thông báo kết nối thành công           | Đạt          |
| TC03 | `GET /api/services`                 | Trả về danh sách dịch vụ    | HTTP 200, JSON có 5 bản ghi tại thời điểm kiểm thử | Đạt          |
| TC04 | Kiểm tra nội dung danh sách dịch vụ | Dữ liệu có cấu trúc phù hợp | Có tên dịch vụ và thời lượng                       | Đạt một phần |

### 5.2. Kiểm thử xác thực và JWT

| Mã   | Trường hợp kiểm thử                          | Kết quả mong đợi | Kết quả thực tế                                     | Đánh giá |
|------|----------------------------------------------|------------------|-----------------------------------------------------|----------|
| TC05 | Truy cập API admin không có token            | HTTP 401         | HTTP 401                                            | Đạt      |
| TC06 | Truy cập API user không có token             | HTTP 401         | HTTP 401                                            | Đạt      |
| TC07 | Truy cập API staff không có token            | HTTP 401         | HTTP 401                                            | Đạt      |
| TC08 | Truy cập API staff bằng token giả            | HTTP 401         | HTTP 401, thông báo token không hợp lệ hoặc hết hạn | Đạt      |
| TC09 | Tài khoản user gọi API staff với JWT hợp lệ  | HTTP 403         | HTTP 403, `Staff permission required.`              | Đạt      |
| TC10 | Tài khoản staff gọi API staff với JWT hợp lệ | HTTP 200         | HTTP 200, trả về danh sách công việc                | Đạt      |

## 6. Kết quả kiểm thử tự động

Lệnh được sử dụng:

```powershell
npm test
```

Kết quả lần chạy gần nhất đã ghi nhận:

| Chỉ tiêu         | Kết quả          |
|------------------|------------------|
| Tổng số bài test | 32               |
| Thành công       | 32               |
| Thất bại         | 0                |
| Thời gian chạy   | Khoảng 2,11 giây |

Các nhóm kiểm thử hiện có bao gồm:

- Xử lý đổi mật khẩu.
- Xác thực JWT.
- Quy trình booking.
- Quyền sở hữu phân công.
- Chuyển đổi trạng thái công việc.
- Truy xuất danh sách booking cho nhân viên và quản trị viên.

## 7. Đánh giá tổng thể

Các hạng mục đã có kết quả thực tế:

- Backend khởi động và kết nối MySQL thành công.
- API dịch vụ trả về HTTP 200.
- API được bảo vệ từ chối request không có token.
- Token không hợp lệ bị từ chối.
- Tài khoản `user` không thể truy cập API yêu cầu quyền `staff`.
- Tài khoản `staff` hợp lệ truy cập API danh sách công việc thành công.
- Bộ kiểm thử tự động hiện có đạt 32/32 test trong lần chạy gần nhất.

Các hạng mục cần tiếp tục:

- Kiểm thử HTTP các thao tác tiếp nhận, từ chối và cập nhật trạng thái booking.
- Kiểm tra các tình huống booking quá hạn.
- Kiểm thử giao diện frontend với dữ liệu thực.
- Xác minh dữ liệu dịch vụ và dữ liệu kiểm thử.
- Đối chiếu schema database với truy vấn backend.