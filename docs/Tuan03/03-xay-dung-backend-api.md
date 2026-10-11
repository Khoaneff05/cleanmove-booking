# 3. XÂY DỰNG BACKEND VÀ API

## 3.1. Mục tiêu

Xây dựng tầng Backend cho hệ thống CleanMove nhằm tiếp nhận và xử lý các yêu cầu từ giao diện người dùng, thực hiện các nghiệp vụ quản lý đặt lịch dịch vụ vệ sinh và trao đổi dữ liệu với cơ sở dữ liệu MySQL.

Backend đóng vai trò trung gian giữa Frontend và cơ sở dữ liệu, giúp tập trung xử lý nghiệp vụ, kiểm tra dữ liệu đầu vào, xác thực người dùng và kiểm soát quyền truy cập vào các chức năng của hệ thống.

Các mục tiêu chính bao gồm:

- Thiết lập môi trường chạy Backend.
- Tổ chức các API theo nhóm chức năng.
- Kết nối và truy vấn dữ liệu từ MySQL.
- Xử lý các nghiệp vụ đặt lịch và quản lý công việc.
- Kiểm tra kết quả trả về và xử lý lỗi phát sinh trong quá trình thực thi.

## 3.2. Công nghệ sử dụng

| Công nghệ | Vai trò |
|---|---|
| Node.js | Môi trường thực thi JavaScript phía máy chủ |
| Express.js | Xây dựng máy chủ HTTP và định tuyến API |
| MySQL | Lưu trữ dữ liệu nghiệp vụ |
| REST API | Quy ước giao tiếp giữa Frontend và Backend |
| JSON | Định dạng trao đổi dữ liệu |
| Git và GitHub | Quản lý mã nguồn và lịch sử thay đổi |

## 3.3. Tổ chức mã nguồn Backend

Backend được tổ chức theo các nhóm thành phần để thuận tiện cho việc phát triển, kiểm thử và bảo trì.

Các thành phần có thể bao gồm:

- **Routes:** Khai báo đường dẫn API và phương thức HTTP.
- **Controllers:** Tiếp nhận yêu cầu và điều phối xử lý.
- **Models:** Thực hiện các thao tác truy vấn dữ liệu.
- **Middleware:** Xử lý xác thực, phân quyền và các tác vụ dùng chung.
- **Config:** Quản lý cấu hình ứng dụng và kết nối cơ sở dữ liệu.
- **Utils:** Chứa các hàm hỗ trợ được sử dụng chung nếu dự án có nhu cầu.

Cấu trúc cụ thể được xác định theo mã nguồn hiện tại, không yêu cầu bổ sung thư mục nếu dự án đã tổ chức theo cách khác.

## 3.4. Thiết lập và kết nối cơ sở dữ liệu

Backend sử dụng MySQL để lưu trữ và truy xuất dữ liệu phục vụ các nghiệp vụ của hệ thống.

Quá trình thiết lập kết nối bao gồm:

1. Cấu hình thông tin kết nối cơ sở dữ liệu.
2. Khởi tạo kết nối hoặc connection pool theo cấu hình của dự án.
3. Kiểm tra khả năng kết nối đến MySQL.
4. Thực hiện truy vấn thử nghiệm.
5. Xử lý lỗi khi kết nối hoặc truy vấn thất bại.


## 3.5. Các nhóm API nghiệp vụ

### 3.5.1. API xác thực và tài khoản

Phục vụ các chức năng liên quan đến tài khoản người dùng, chẳng hạn đăng ký, đăng nhập, lấy thông tin tài khoản và kiểm tra quyền truy cập.

### 3.5.2. API quản lý dịch vụ

Hỗ trợ truy xuất danh sách dịch vụ vệ sinh và các thông tin cần thiết để khách hàng lựa chọn dịch vụ khi đặt lịch.

### 3.5.3. API quản lý đặt lịch

Tiếp nhận và xử lý các yêu cầu đặt lịch, bao gồm thông tin dịch vụ, thời gian, địa điểm và thông tin liên quan theo thiết kế dữ liệu thực tế.

### 3.5.4. API quản lý công việc của nhân viên

Phục vụ việc xem các công việc được phân công, tiếp nhận công việc và cập nhật trạng thái xử lý theo quy trình nghiệp vụ.

### 3.5.5. API quản trị

Phục vụ các chức năng quản lý dữ liệu và theo dõi hoạt động hệ thống theo quyền hạn của quản trị viên.

Các nhóm API trên mô tả phạm vi nghiệp vụ. Danh sách endpoint cụ thể cần được bổ sung sau khi đối chiếu các routes đang tồn tại trong mã nguồn.

## 3.6. Quy trình xử lý yêu cầu API

Quy trình xử lý yêu cầu thông thường gồm các bước:

1. Frontend gửi yêu cầu HTTP đến endpoint tương ứng.
2. Backend tiếp nhận và kiểm tra dữ liệu đầu vào.
3. Middleware thực hiện xác thực hoặc phân quyền nếu endpoint yêu cầu.
4. Controller điều phối xử lý nghiệp vụ.
5. Backend truy vấn hoặc cập nhật dữ liệu trong MySQL.
6. Backend trả kết quả cùng mã trạng thái HTTP phù hợp.
7. Frontend tiếp nhận phản hồi và hiển thị kết quả cho người dùng.

## 3.7. Kiểm tra và xử lý lỗi

Trong quá trình phát triển Backend, cần kiểm tra các nhóm lỗi sau:

- Lỗi kết nối cơ sở dữ liệu.
- Lỗi truy vấn do tên bảng hoặc tên cột không chính xác.
- Lỗi dữ liệu đầu vào không hợp lệ.
- Lỗi xác thực hoặc phân quyền.
- Lỗi chuyển trạng thái công việc không đúng quy trình.
- Lỗi do dữ liệu giữa Backend và cơ sở dữ liệu không thống nhất.

## 3.8. Kiểm thử API

Việc kiểm thử API tập trung vào các nội dung:

- Endpoint có phản hồi đúng phương thức HTTP hay không.
- Dữ liệu đầu vào có được kiểm tra đầy đủ hay không.
- Kết quả truy vấn có phù hợp với dữ liệu trong MySQL hay không.
- Mã trạng thái HTTP và nội dung phản hồi có phù hợp hay không.
- Người dùng không đủ quyền có bị từ chối truy cập hay không.
- Các trường hợp lỗi có được xử lý mà không làm sai lệch dữ liệu hay không.

## 3.9. Kết quả thực hiện

Mục này được cập nhật theo tình trạng triển khai thực tế của dự án, bao gồm:

- Các API đã xây dựng và chạy thử thành công.
- Khả năng kết nối và truy vấn dữ liệu từ MySQL.
- Các nghiệp vụ đã kiểm thử.
- Những lỗi phát hiện trong quá trình tích hợp.
- Các nội dung còn cần hoàn thiện.