# 2. THIẾT KẾ KIẾN TRÚC HỆ THỐNG

## 2.1. Mục tiêu thiết kế

Thiết kế kiến trúc hệ thống CleanMove nhằm xác định cách tổ chức các thành phần phần mềm, phương thức trao đổi dữ liệu và trách nhiệm xử lý của từng thành phần.

Kiến trúc được xây dựng để hỗ trợ các nghiệp vụ quản lý dịch vụ vệ sinh, tiếp nhận yêu cầu đặt lịch, phân công nhân viên, theo dõi trạng thái công việc và quản lý dữ liệu hệ thống.

Các mục tiêu chính bao gồm:

- Phân tách giao diện người dùng, xử lý nghiệp vụ và lưu trữ dữ liệu.
- Tạo điều kiện thuận lợi cho việc phát triển, kiểm thử và bảo trì.
- Bảo đảm dữ liệu được xử lý nhất quán giữa Frontend, Backend và cơ sở dữ liệu.
- Hỗ trợ phân quyền theo vai trò khách hàng, nhân viên và quản trị viên.

## 2.2. Mô hình kiến trúc tổng thể

Hệ thống sử dụng mô hình Client–Server, trong đó Frontend chịu trách nhiệm hiển thị giao diện và tiếp nhận thao tác của người dùng; Backend xử lý các yêu cầu nghiệp vụ và giao tiếp với cơ sở dữ liệu MySQL.

Các thành phần chính:

**1. Frontend**

Cung cấp giao diện để người dùng thao tác với hệ thống, bao gồm xem dịch vụ, tạo yêu cầu đặt lịch, theo dõi lịch sử đặt lịch và thực hiện các chức năng tương ứng với vai trò được cấp quyền.

**2. Backend**

Tiếp nhận các yêu cầu HTTP từ Frontend, kiểm tra dữ liệu đầu vào, xác thực người dùng, kiểm tra quyền truy cập, thực hiện nghiệp vụ và trả kết quả thông qua API.

**3. Cơ sở dữ liệu MySQL**

Lưu trữ thông tin tài khoản, dịch vụ, yêu cầu đặt lịch, phân công nhân viên và các dữ liệu nghiệp vụ khác theo cấu trúc cơ sở dữ liệu thực tế của dự án.

## 2.3. Công nghệ sử dụng

| Thành phần | Công nghệ | Vai trò |
|---|---|---|
| Frontend | React | Xây dựng giao diện người dùng |
| Ngôn ngữ Frontend | JavaScript hoặc TypeScript, tùy cấu hình thực tế | Xử lý logic phía giao diện |
| Backend | Node.js | Môi trường thực thi phía máy chủ |
| Framework Backend | Express.js | Xây dựng API và xử lý yêu cầu HTTP |
| Cơ sở dữ liệu | MySQL | Lưu trữ và truy vấn dữ liệu |
| Giao tiếp | HTTP/REST API | Trao đổi dữ liệu giữa Frontend và Backend |
| Quản lý mã nguồn | Git và GitHub | Theo dõi lịch sử thay đổi và lưu trữ mã nguồn |

*Lưu ý: Cần đối chiếu `package.json` và cấu hình thực tế trước khi chốt danh sách công nghệ.*

## 2.4. Kiến trúc các thành phần Backend

Backend được tổ chức theo các nhóm chức năng nhằm tách biệt việc tiếp nhận yêu cầu, xử lý nghiệp vụ và truy cập dữ liệu.

Các nhóm thành phần dự kiến gồm:

- **Routes:** Khai báo các endpoint và phương thức HTTP.
- **Controllers:** Tiếp nhận yêu cầu và điều phối xử lý.
- **Models:** Thực hiện các thao tác truy vấn hoặc cập nhật dữ liệu.
- **Middleware:** Xử lý xác thực, phân quyền và các tác vụ dùng chung.
- **Config:** Quản lý cấu hình kết nối cơ sở dữ liệu và các thiết lập cần thiết.

## 2.5. Luồng trao đổi dữ liệu

Quy trình xử lý một yêu cầu từ người dùng được mô tả như sau:

1. Người dùng thực hiện thao tác trên giao diện Frontend.
2. Frontend gửi yêu cầu HTTP đến endpoint tương ứng của Backend.
3. Backend tiếp nhận yêu cầu, kiểm tra dữ liệu đầu vào và xác thực quyền truy cập khi cần thiết.
4. Backend thực hiện xử lý nghiệp vụ và truy vấn hoặc cập nhật dữ liệu trong MySQL.
5. MySQL trả kết quả truy vấn cho Backend.
6. Backend trả phản hồi HTTP, thường ở định dạng JSON.
7. Frontend tiếp nhận phản hồi và hiển thị dữ liệu hoặc thông báo phù hợp.

## 2.6. Các yêu cầu về bảo mật và tính toàn vẹn

Trong quá trình thiết kế và triển khai, hệ thống cần chú trọng các nội dung sau:

- Xác thực người dùng trước khi truy cập các chức năng yêu cầu đăng nhập.
- Kiểm tra quyền hạn theo vai trò đối với các API quản lý và xử lý công việc.
- Kiểm tra dữ liệu đầu vào trước khi thực hiện thao tác với cơ sở dữ liệu.
- Sử dụng truy vấn có tham số để hạn chế nguy cơ SQL Injection.
- Bảo vệ thông tin xác thực và cấu hình kết nối cơ sở dữ liệu.
- Sử dụng ràng buộc cơ sở dữ liệu phù hợp để bảo đảm tính toàn vẹn dữ liệu.
- Xử lý lỗi nhất quán, tránh để lộ thông tin nhạy cảm trong phản hồi API.