# 02. HOÀN THIỆN BACKEND API ĐẶT LỊCH

## 1. Mục tiêu

Trong tuần 5 của kỳ thực tập chuyên ngành, tiến hành rà soát và hoàn thiện các Backend API phục vụ nghiệp vụ đặt lịch dịch vụ của hệ thống CleanMove.

Backend API đóng vai trò tiếp nhận yêu cầu từ Frontend, xác thực người dùng, kiểm tra dữ liệu đầu vào, xử lý quy tắc nghiệp vụ và tương tác với cơ sở dữ liệu MySQL.

Mục tiêu là bảo đảm các thao tác tạo, xem và quản lý lịch đặt dịch vụ hoạt động đúng theo thiết kế, đồng thời duy trì tính toàn vẹn dữ liệu và không làm ảnh hưởng đến những chức năng hiện có của hệ thống.

## 2. Phạm vi thực hiện

Các nội dung được tập trung rà soát và hoàn thiện bao gồm:

- Kiểm tra cơ chế xác thực JWT và phân quyền truy cập API.
- Rà soát API lấy danh sách dịch vụ phục vụ đặt lịch.
- Hoàn thiện hoặc xác minh API tạo yêu cầu đặt lịch.
- Kiểm tra API xem danh sách và chi tiết lịch đặt của khách hàng.
- Kiểm tra các API quản lý trạng thái đặt lịch.
- Kiểm tra nghiệp vụ phân công nhân viên và điều kiện lịch làm việc.
- Chuẩn hóa phản hồi thành công, lỗi xác thực, lỗi dữ liệu và lỗi hệ thống.
- Kiểm thử API và khả năng tương thích với giao diện Frontend.

## 3. Kiến trúc Backend API

Backend của hệ thống được xây dựng bằng Node.js và Express, sử dụng MySQL để lưu trữ dữ liệu và JWT để xác thực người dùng.

Luồng xử lý cơ bản:

1. Frontend gửi HTTP request đến Backend.
2. Middleware xác thực token và kiểm tra quyền truy cập.
3. Route tiếp nhận yêu cầu và chuyển đến Controller.
4. Controller kiểm tra dữ liệu đầu vào và điều phối nghiệp vụ.
5. Các truy vấn cần thiết được thực hiện thông qua kết nối cơ sở dữ liệu.
6. Backend trả về HTTP status và dữ liệu JSON cho Frontend.

Các thành phần liên quan cần được rà soát gồm:

| Thành phần | Trách nhiệm |
|---|---|
| `backend/server.js` | Khởi động máy chủ Backend. |
| `backend/app.js` | Khởi tạo Express và đăng ký middleware, route. |
| `backend/config/db.js` | Quản lý kết nối MySQL. |
| `backend/middlewares/authMiddleware.js` | Xác thực JWT và kiểm tra quyền truy cập. |
| Các file route | Khai báo endpoint và gắn middleware tương ứng. |
| Các file Controller | Xử lý request, nghiệp vụ và phản hồi HTTP. |
| Các tiện ích nghiệp vụ | Hỗ trợ giao dịch cơ sở dữ liệu, kiểm tra lịch và quy trình phân công. |

## 4. Các API phục vụ nghiệp vụ đặt lịch

### 4.1. API lấy danh sách dịch vụ

**Mục đích:** Cung cấp danh sách dịch vụ để khách hàng lựa chọn trước khi đặt lịch.

- Phương thức: `GET`
- Endpoint dự kiến: `/api/services`
- Xác thực: Theo chính sách truy cập hiện hành của hệ thống.

Dữ liệu trả về cần bao gồm những trường cần thiết cho giao diện, chẳng hạn mã dịch vụ, tên dịch vụ, mô tả và giá dịch vụ nếu có.

Backend cần bảo đảm chỉ cung cấp những dịch vụ đáp ứng điều kiện hiển thị và đặt dịch vụ theo quy tắc hiện hành.

### 4.2. API tạo yêu cầu đặt lịch

**Mục đích:** Tiếp nhận thông tin đặt lịch do khách hàng gửi từ Frontend.

- Phương thức: `POST`
- Endpoint: Cần đối chiếu với route đặt lịch hiện có.
- Xác thực: Yêu cầu đăng nhập nếu quy trình hiện hành quy định đặt lịch dành cho người dùng đã xác thực.

Dữ liệu gửi lên có thể bao gồm mã dịch vụ, địa chỉ, thời gian dự kiến và ghi chú. Tên trường và cấu trúc request phải thống nhất với API thực tế.

Backend cần thực hiện các bước:

1. Xác thực người dùng.
2. Kiểm tra dữ liệu đầu vào.
3. Kiểm tra dịch vụ có tồn tại và đáp ứng điều kiện đặt lịch.
4. Xác định thời lượng dịch vụ từ dữ liệu phía máy chủ.
5. Kiểm tra những điều kiện nghiệp vụ liên quan đến ngày giờ.
6. Tạo bản ghi đặt lịch với trạng thái ban đầu hợp lệ.
7. Trả về thông tin lịch đặt vừa được tạo.

### 4.3. API lấy danh sách lịch đặt

**Mục đích:** Cho phép khách hàng xem các yêu cầu đặt lịch thuộc tài khoản của mình.

- Phương thức: `GET`
- Endpoint: Đối chiếu route người dùng hiện có.

Backend cần bảo đảm người dùng chỉ truy cập được những bản ghi thuộc phạm vi quyền của mình. Trường hợp quản trị viên cần xem danh sách tổng thể phải sử dụng quyền quản trị tương ứng.

Thông tin trả về có thể bao gồm mã lịch đặt, dịch vụ, thời gian, địa chỉ, trạng thái và thông tin liên quan đến phân công nếu được phép hiển thị.

### 4.4. API xem chi tiết lịch đặt

**Mục đích:** Cung cấp thông tin chi tiết của một lịch đặt cụ thể.

- Phương thức: `GET`
- Endpoint: Theo route chi tiết lịch đặt hiện có.

Backend phải kiểm tra bản ghi tồn tại và người yêu cầu có quyền xem bản ghi đó. Không được chỉ dựa vào mã lịch đặt do client gửi lên để cho phép truy cập dữ liệu của người khác.

### 4.5. API hủy lịch đặt

**Mục đích:** Hỗ trợ khách hàng gửi yêu cầu hủy lịch theo điều kiện nghiệp vụ.

- Phương thức: `PATCH` hoặc phương thức đang được quy định trong hệ thống.
- Endpoint: Đối chiếu route hiện có.

Backend cần kiểm tra:

- Lịch đặt có tồn tại hay không.
- Người thực hiện có quyền hủy hay không.
- Trạng thái hiện tại có cho phép hủy hay không.
- Có cần cập nhật thông tin phân công và lịch sử trạng thái hay không.

Không nên cho phép chuyển mọi lịch đặt sang trạng thái `cancelled` một cách tùy ý. Điều kiện hủy phải thống nhất với quy trình nghiệp vụ hiện tại.

### 4.6. API quản lý trạng thái và phân công

Nhóm API này phục vụ quản trị viên và nhân viên trong quá trình xử lý lịch đặt.

Các thao tác cần được kiểm tra gồm:

- Xem các yêu cầu cần xử lý.
- Phân công nhân viên.
- Tiếp nhận hoặc từ chối công việc theo quyền được cấp.
- Cập nhật trạng thái thực hiện dịch vụ.
- Ghi nhận lịch sử trạng thái khi cần.

Mỗi thao tác phải kiểm tra vai trò, trạng thái hiện tại và điều kiện chuyển trạng thái trước khi cập nhật dữ liệu.

## 5. Kiểm tra dữ liệu đầu vào

Backend cần thực hiện kiểm tra dữ liệu độc lập với Frontend.

| Dữ liệu | Điều kiện kiểm tra |
|---|---|
| Mã dịch vụ | Phải tồn tại và đáp ứng điều kiện đặt dịch vụ. |
| Địa chỉ | Không được thiếu nếu đây là trường bắt buộc. |
| Ngày giờ | Đúng định dạng và đáp ứng quy tắc thời gian. |
| Thời lượng | Lấy từ dữ liệu đáng tin cậy phía máy chủ. |
| Mã người dùng | Lấy từ thông tin xác thực đã được kiểm tra. |
| Trạng thái | Chỉ chấp nhận các giá trị và chuyển đổi hợp lệ. |
| Mã lịch đặt | Kiểm tra tồn tại và quyền truy cập bản ghi. |
| Thông tin phân công | Kiểm tra nhân viên, trạng thái và lịch làm việc liên quan. |

## 6. Kiểm tra xung đột lịch nhân viên

Một yêu cầu quan trọng của hệ thống là hạn chế việc phân công cùng một nhân viên vào những công việc có thời gian chồng lấn.

Khi phân công nhân viên, Backend cần:

1. Xác định thời gian bắt đầu và thời lượng thực hiện công việc.
2. Tính thời gian kết thúc dự kiến và khoảng đệm di chuyển nếu nghiệp vụ yêu cầu.
3. Khóa các bản ghi lịch liên quan theo thứ tự nhất quán trong giao dịch.
4. Kiểm tra các công việc đã phân công thuộc những module có liên quan.
5. Từ chối phân công nếu phát hiện xung đột.
6. Chỉ lưu phân công sau khi các điều kiện đã được đáp ứng.

Điều kiện kiểm tra khoảng thời gian có thể biểu diễn như sau:

`startA < endB AND startB < endA`

Điều kiện trên xác định hai khoảng thời gian có phần giao nhau khi sử dụng khoảng nửa mở `[start, end)`. Khoảng đệm di chuyển cần được cộng vào khoảng thời gian phù hợp trước khi so sánh.

Việc kiểm tra phải được thực hiện trong giao dịch cơ sở dữ liệu với cơ chế khóa phù hợp. Chỉ truy vấn lịch trước khi ghi dữ liệu mà không bảo vệ trước các yêu cầu đồng thời có thể dẫn đến phân công trùng lịch.

## 7. Xử lý giao dịch cơ sở dữ liệu

Đối với những thao tác cần cập nhật nhiều bản ghi, chẳng hạn tạo lịch kèm lịch sử trạng thái hoặc phân công nhân viên kèm khóa lịch, cần xem xét sử dụng transaction.

Quy trình xử lý:

1. Bắt đầu giao dịch.
2. Thực hiện khóa và kiểm tra dữ liệu cần thiết.
3. Thực hiện các thao tác ghi dữ liệu.
4. Commit khi tất cả thao tác thành công.
5. Rollback khi xảy ra lỗi.

Các lỗi deadlock hoặc lock timeout cần được xử lý theo cơ chế hiện có. Chỉ retry những lỗi được xác định là có thể thử lại an toàn; không tự động thử lại mọi lỗi nghiệp vụ.

Mục tiêu là tránh dữ liệu dở dang và duy trì tính nhất quán giữa lịch đặt, phân công và lịch sử trạng thái.

## 8. Chuẩn hóa phản hồi API

Backend cần sử dụng mã HTTP phù hợp với từng loại kết quả.

| Mã HTTP | Ý nghĩa |
|---|---|
| `200 OK` | Yêu cầu đọc hoặc cập nhật thành công. |
| `201 Created` | Tạo mới lịch đặt thành công. |
| `400 Bad Request` | Dữ liệu gửi lên không hợp lệ. |
| `401 Unauthorized` | Chưa xác thực hoặc token không hợp lệ, hết hạn. |
| `403 Forbidden` | Đã xác thực nhưng không đủ quyền thực hiện thao tác. |
| `404 Not Found` | Không tìm thấy tài nguyên được yêu cầu. |
| `409 Conflict` | Xung đột trạng thái hoặc lịch làm việc. |
| `500 Internal Server Error` | Lỗi hệ thống ngoài dự kiến. |

Cấu trúc JSON cần nhất quán với quy ước hiện tại của dự án. Không thay đổi toàn bộ cấu trúc phản hồi nếu điều đó làm ảnh hưởng đến các giao diện đang sử dụng.

## 9. Kế hoạch kiểm thử API

| Mã | Nội dung kiểm thử | Kết quả mong đợi |
|---|---|---|
| API-01 | Lấy danh sách dịch vụ | Trả về dữ liệu theo cấu trúc quy định. |
| API-02 | Tạo lịch với dữ liệu hợp lệ | Tạo lịch thành công. |
| API-03 | Tạo lịch thiếu trường bắt buộc | Trả về lỗi dữ liệu hợp lệ. |
| API-04 | Tạo lịch với mã dịch vụ không tồn tại | Từ chối yêu cầu. |
| API-05 | Gọi API bằng token không hợp lệ | Trả về `401` nếu endpoint yêu cầu xác thực. |
| API-06 | Truy cập lịch đặt của người dùng khác | Từ chối truy cập theo chính sách phân quyền. |
| API-07 | Hủy lịch không đủ điều kiện | Từ chối chuyển trạng thái. |
| API-08 | Phân công nhân viên bị trùng lịch | Từ chối phân công. |
| API-09 | Hai yêu cầu đồng thời phân công cùng khung giờ | Không tạo phân công xung đột. |
| API-10 | Lỗi giữa giao dịch cập nhật | Rollback những thay đổi thuộc giao dịch. |
| API-11 | Người dùng thường gọi API dành cho quản trị viên | Từ chối theo cơ chế phân quyền. |
| API-12 | Gọi API với mã tài nguyên không tồn tại | Trả về `404` nếu phù hợp với hợp đồng API. |

Kết quả kiểm thử thực tế cần được ghi nhận bằng công cụ hoặc bộ test đang sử dụng trong dự án. Các trường hợp chưa chạy không được đánh dấu là đã đạt.

## 10. Kết quả cần ghi nhận

Sau khi rà soát và hoàn thiện, cần tổng hợp:

- Danh sách API đã được xác minh.
- Những chức năng đã bổ sung hoặc điều chỉnh.
- Kết quả kiểm thử và số lượng test đạt, chưa đạt.
- Các lỗi đã phát hiện và phương án xử lý.
- Những giới hạn hoặc chức năng còn cần hoàn thiện.
- Mức độ tương thích giữa Backend API và Frontend.

Việc xác nhận hoàn thành phải dựa trên mã nguồn, kết quả chạy thử và kiểm thử thực tế.
