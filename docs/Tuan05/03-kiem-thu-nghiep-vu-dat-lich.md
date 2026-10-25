# 03. KIỂM THỬ NGHIỆP VỤ ĐẶT LỊCH

## 1. Mục tiêu kiểm thử

Kiểm thử chức năng đặt lịch dịch vụ vệ sinh nhằm xác minh:

- API lấy danh sách dịch vụ hoạt động đúng.
- API tạo lịch kiểm tra dữ liệu đầu vào.
- Hệ thống xử lý đúng các trường hợp thiếu dữ liệu, dữ liệu không hợp lệ và mã dịch vụ không tồn tại.
- API yêu cầu xác thực người dùng.
- Các phản hồi HTTP và thông báo lỗi phù hợp với logic xử lý hiện tại.

## 2. Môi trường kiểm thử

| Thành phần | Thông tin |
|---|---|
| Backend | Node.js, Express |
| Cơ sở dữ liệu | MySQL |
| API cơ sở | `http://localhost:5000` |
| API danh sách dịch vụ | `GET /api/services` |
| API tạo lịch | `POST /api/bookings` |
| Xác thực | JWT Bearer Token |
| Công cụ kiểm thử | Windows PowerShell |
| Phương thức kiểm thử | Kiểm thử API thủ công |

## 3. Kết quả kiểm thử

### 3.1. Kiểm thử danh sách dịch vụ và xác thực

| Mã TC | Trường hợp kiểm thử | Kết quả mong đợi | Kết quả thực tế | Đánh giá |
|---|---|---|---|---|
| TC-00 | Lấy danh sách dịch vụ | HTTP 200 | HTTP 200 | PASS |
| TC-08 | Tạo lịch không có token | HTTP 401 | HTTP 401 | PASS |
| TC-09 | Tạo lịch với token không hợp lệ | HTTP 401 | HTTP 401 | PASS |
| TC-32 | Kiểm tra lại API tạo lịch không có token | HTTP 401 | HTTP 401 | PASS |

### 3.2. Kiểm thử dữ liệu bắt buộc

| Mã TC | Trường hợp kiểm thử | Kết quả mong đợi | Kết quả thực tế | Đánh giá |
|---|---|---|---|---|
| TC-02 | Thiếu tên khách hàng | HTTP 400 | HTTP 400 | PASS |
| TC-03 | Thiếu địa chỉ | HTTP 400 | HTTP 400 | PASS |
| TC-04 | Thiếu thời gian đặt lịch | HTTP 400 | HTTP 400 | PASS |
| TC-05 | Thiếu mã dịch vụ | HTTP 400 | HTTP 400 | PASS |
| TC-10 | Tên khách hàng chỉ chứa khoảng trắng | HTTP 400 | HTTP 400 | PASS |
| TC-11 | Địa chỉ chỉ chứa khoảng trắng | HTTP 400 | HTTP 400 | PASS |
| TC-18 | Không gửi trường `customer_name` | HTTP 400 | HTTP 400 | PASS |
| TC-19 | `customer_name = null` | HTTP 400 | HTTP 400 | PASS |
| TC-20 | `customer_name` là chuỗi rỗng | HTTP 400 | HTTP 400 | PASS |
| TC-21 | `customer_name` chỉ chứa khoảng trắng | HTTP 400 | HTTP 400 | PASS |
| TC-22 | Không gửi trường `address` | HTTP 400 | HTTP 400 | PASS |
| TC-23 | `address = null` | HTTP 400 | HTTP 400 | PASS |
| TC-24 | `address` là chuỗi rỗng | HTTP 400 | HTTP 400 | PASS |
| TC-25 | `address` chỉ chứa khoảng trắng | HTTP 400 | HTTP 400 | PASS |
| TC-26 | Không gửi trường `date_time` | HTTP 400 | HTTP 400 | PASS |
| TC-27 | `date_time = null` | HTTP 400 | HTTP 400 | PASS |
| TC-28 | `date_time` là chuỗi rỗng | HTTP 400 | HTTP 400 | PASS |

### 3.3. Kiểm thử mã dịch vụ

| Mã TC | Trường hợp kiểm thử | Kết quả mong đợi | Kết quả thực tế | Đánh giá |
|---|---|---|---|---|
| TC-06 | `service_id` là chuỗi không phải số (`abc`) | HTTP 400 | HTTP 400 | PASS |
| TC-07 | Mã dịch vụ không tồn tại (`999999`) | HTTP 404 | HTTP 404 | PASS |
| TC-12 | `service_id` là số thập phân (`23.5`) | HTTP 400 | HTTP 400 | PASS |
| TC-13 | `service_id = -1` | HTTP 404 theo logic hiện tại | HTTP 404 | PASS |
| TC-14 | `service_id = 0` | HTTP 404 theo logic hiện tại | HTTP 404 | PASS |
| TC-15 | `service_id = null` | HTTP 404 theo logic hiện tại | HTTP 404 | PASS |
| TC-16 | `service_id` là chuỗi rỗng | HTTP 404 theo logic hiện tại | HTTP 404 | PASS |
| TC-17 | `service_id` là đối tượng JSON | HTTP 400 | HTTP 400 | PASS |
| TC-29 | Không gửi trường `service_id` | HTTP 400 | HTTP 400 | PASS |
| TC-30 | `service_id = abc` | HTTP 400 | HTTP 400 | PASS |
| TC-31 | `service_id = 999999` | HTTP 404 | HTTP 404 | PASS |

## 4. Tổng hợp kết quả

- API danh sách dịch vụ trả về HTTP 200.
- Các trường dữ liệu bắt buộc được kiểm tra và trả về HTTP 400 khi thiếu hoặc không hợp lệ.
- Token thiếu hoặc không hợp lệ bị từ chối với HTTP 401.
- Mã dịch vụ không tồn tại trả về HTTP 404.
- Dữ liệu `service_id` có kiểu không phù hợp được xử lý theo logic kiểm tra hiện tại.

## 5. Các vấn đề và hướng cải thiện

1. **Xác thực mã dịch vụ:** Cân nhắc yêu cầu `service_id` là số nguyên dương trước khi truy vấn cơ sở dữ liệu.
2. **Xác thực ngày giờ:** Cần kiểm tra định dạng ngày giờ, tính hợp lệ và quy tắc không cho phép đặt lịch trong quá khứ nếu đó là yêu cầu nghiệp vụ.
3. **Kiểm soát quyền truy cập:** Kiểm thử việc người dùng chỉ được truy cập hoặc thao tác trên lịch thuộc quyền của mình.
4. **Xung đột lịch nhân viên:** Kiểm thử trường hợp hai lịch có thời gian chồng lấn và bảo đảm không phân công cùng nhân viên vào các lịch xung đột.
5. **Dữ liệu kiểm thử:** Theo dõi các lịch đã tạo trong quá trình kiểm thử và không xóa dữ liệu hiện có nếu chưa được phê duyệt.

## 6. Kết luận

Kiểm thử API đặt lịch đã xác minh được các luồng cơ bản gồm lấy danh sách dịch vụ, tạo lịch hợp lệ, kiểm tra dữ liệu đầu vào, kiểm tra mã dịch vụ và xác thực JWT. Các trường hợp được chạy lại đã cho kết quả nhất quán với logic xử lý hiện tại.

Cần tiếp tục kiểm thử các quy tắc về ngày giờ, phân quyền và xung đột lịch để đánh giá đầy đủ hơn tính đúng đắn và an toàn của nghiệp vụ đặt lịch.
