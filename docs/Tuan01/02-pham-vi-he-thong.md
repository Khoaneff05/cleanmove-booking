# 2. Phạm vi hệ thống

## 2.1. Phạm vi tổng quát

Hệ thống Web được xây dựng nhằm hỗ trợ việc đặt lịch và quản lý các dịch vụ vệ sinh, vận chuyển theo yêu cầu.

Hệ thống phục vụ ba nhóm người dùng chính:

* Khách hàng.
* Nhân viên.
* Quản lý/Quản trị viên.

Phạm vi hệ thống tập trung vào quy trình từ khi khách hàng gửi yêu cầu sử dụng dịch vụ, quản lý tiếp nhận và báo giá, phân công nhân viên, nhân viên thực hiện dịch vụ, cập nhật trạng thái cho đến khi dịch vụ hoàn thành và được lưu vào lịch sử.

## 2.2. Phạm vi đối với khách hàng

Khách hàng có thể thực hiện các chức năng:

* Đăng ký tài khoản.
* Đăng nhập và đăng xuất.
* Quản lý thông tin cá nhân.
* Đổi mật khẩu.
* Xem danh sách dịch vụ.
* Tìm kiếm dịch vụ.
* Lọc dịch vụ theo loại.
* Xem thông tin chi tiết dịch vụ.
* Gửi yêu cầu sử dụng dịch vụ.
* Chọn ngày và thời gian thực hiện.
* Nhập địa điểm thực hiện.
* Nhập thông tin hoặc yêu cầu bổ sung.
* Xem trạng thái xử lý yêu cầu.
* Xem báo giá.
* Xác nhận hoặc từ chối báo giá.
* Hủy yêu cầu khi đáp ứng điều kiện.
* Xem lịch sử sử dụng dịch vụ.

## 2.3. Phạm vi đối với nhân viên

Nhân viên có thể thực hiện các chức năng:

* Đăng nhập và đăng xuất.
* Xem và cập nhật thông tin cá nhân.
* Xem danh sách công việc được phân công.
* Xem chi tiết công việc.
* Xem thông tin cần thiết của khách hàng.
* Xem thời gian và địa điểm thực hiện.
* Xác nhận tiếp nhận công việc.
* Cập nhật trạng thái thực hiện dịch vụ.
* Cập nhật kết quả thực hiện.
* Xem lịch sử các công việc đã thực hiện.

Nhân viên không có quyền quản lý toàn bộ dữ liệu hệ thống và chỉ được truy cập các chức năng phù hợp với quyền được cấp.

## 2.4. Phạm vi đối với quản lý/quản trị viên

Quản lý/Quản trị viên có quyền quản lý và theo dõi hoạt động của hệ thống, bao gồm:

### Quản lý tài khoản

* Xem danh sách tài khoản.
* Tìm kiếm tài khoản.
* Thêm tài khoản nhân viên.
* Cập nhật thông tin tài khoản.
* Khóa hoặc mở khóa tài khoản khi cần.
* Phân quyền tài khoản.

### Quản lý khách hàng

* Xem danh sách khách hàng.
* Tìm kiếm khách hàng.
* Xem thông tin khách hàng.
* Cập nhật thông tin cần thiết.

### Quản lý nhân viên

* Thêm nhân viên.
* Xem danh sách nhân viên.
* Cập nhật thông tin nhân viên.
* Quản lý trạng thái hoạt động của nhân viên.

### Quản lý loại dịch vụ

* Thêm loại dịch vụ.
* Xem loại dịch vụ.
* Cập nhật loại dịch vụ.
* Xóa loại dịch vụ khi đáp ứng điều kiện.

### Quản lý dịch vụ

* Thêm dịch vụ.
* Xem danh sách dịch vụ.
* Tìm kiếm và lọc dịch vụ.
* Xem chi tiết dịch vụ.
* Cập nhật dịch vụ.
* Xóa hoặc ngừng cung cấp dịch vụ.

### Quản lý yêu cầu dịch vụ

* Xem danh sách yêu cầu.
* Tìm kiếm và lọc yêu cầu.
* Xem chi tiết yêu cầu.
* Tiếp nhận yêu cầu.
* Từ chối yêu cầu.
* Nhập và cập nhật báo giá.
* Xác nhận xử lý yêu cầu.
* Phân công nhân viên.
* Cập nhật trạng thái đơn dịch vụ.

### Dashboard và thống kê

* Xem tổng số yêu cầu dịch vụ.
* Xem số lượng yêu cầu theo trạng thái.
* Xem số lượng dịch vụ đã hoàn thành.
* Xem doanh thu cơ bản.
* Xem thống kê theo khoảng thời gian.
* Xem thống kê theo loại dịch vụ.

## 2.5. Các nhóm dịch vụ trong phạm vi

Hệ thống gồm hai nhóm dịch vụ chính.

### 2.5.1. Dịch vụ vệ sinh

Một số dịch vụ mẫu:

* Vệ sinh nhà ở.
* Vệ sinh phòng trọ.
* Vệ sinh văn phòng.
* Vệ sinh theo giờ.
* Vệ sinh sau xây dựng.

### 2.5.2. Dịch vụ vận chuyển

Một số dịch vụ mẫu:

* Chuyển nhà.
* Chuyển phòng trọ.
* Chuyển văn phòng.
* Vận chuyển hàng hóa.

Các dịch vụ trên được lưu trữ và quản lý trong cơ sở dữ liệu. Quản trị viên có thể thêm hoặc điều chỉnh dịch vụ tùy theo nhu cầu của hệ thống.


## 2.6. Phạm vi quy trình đặt dịch vụ

Quy trình đặt dịch vụ của hệ thống được giới hạn trong các bước chính:

Khách hàng
    ↓
Chọn dịch vụ
    ↓
Nhập thông tin yêu cầu
    ↓
Chọn thời gian và địa điểm
    ↓
Gửi yêu cầu
    ↓
Chờ quản lý tiếp nhận
    ↓
Quản lý kiểm tra yêu cầu
    ↓
Nhập báo giá
    ↓
Khách hàng xem và xác nhận
    ↓
Quản lý phân công nhân viên
    ↓
Nhân viên thực hiện
    ↓
Cập nhật trạng thái
    ↓
Hoàn thành

Các trường hợp ngoại lệ bao gồm:

* Quản lý từ chối yêu cầu.
* Khách hàng từ chối báo giá.
* Khách hàng hủy yêu cầu theo điều kiện cho phép.
* Nhân viên không thể tiếp nhận công việc và cần được phân công lại.

## 2.7. Trạng thái yêu cầu dịch vụ

Hệ thống dự kiến sử dụng các trạng thái chính sau:

| Trạng thái         | Ý nghĩa                                             |
| ------------------ | --------------------------------------------------- |
| **Chờ tiếp nhận**  | Khách hàng đã gửi yêu cầu và đang chờ quản lý xử lý |
| **Đã tiếp nhận**   | Quản lý đã tiếp nhận yêu cầu                        |
| **Đã báo giá**     | Yêu cầu đã được xác định mức giá                    |
| **Chờ xác nhận**   | Khách hàng đang chờ xem và xác nhận báo giá         |
| **Đã xác nhận**    | Khách hàng đã đồng ý sử dụng dịch vụ                |
| **Đã phân công**   | Yêu cầu đã được phân công cho nhân viên             |
| **Đang thực hiện** | Nhân viên đang thực hiện dịch vụ                    |
| **Hoàn thành**     | Dịch vụ đã được thực hiện hoàn tất                  |
| **Từ chối**        | Yêu cầu không được chấp nhận                        |
| **Đã hủy**         | Yêu cầu đã bị hủy theo điều kiện của hệ thống       |

Các trạng thái có thể được điều chỉnh trong quá trình phân tích chi tiết nếu phát sinh yêu cầu nghiệp vụ phù hợp.

## 2.8. Phạm vi dữ liệu

Hệ thống dự kiến quản lý các nhóm dữ liệu chính:

* Tài khoản người dùng.
* Khách hàng.
* Nhân viên.
* Loại dịch vụ.
* Dịch vụ.
* Yêu cầu đặt dịch vụ.
* Thông tin thời gian và địa điểm thực hiện.
* Báo giá.
* Phân công nhân viên.
* Trạng thái yêu cầu.
* Lịch sử dịch vụ.