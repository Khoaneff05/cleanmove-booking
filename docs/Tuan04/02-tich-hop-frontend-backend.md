# 02. Tích hợp Frontend và Backend

## 1. Mục tiêu

Mục tiêu của công việc là kết nối giao diện người dùng với Backend API, giúp các chức năng trên giao diện sử dụng dữ liệu thực từ cơ sở dữ liệu thay vì chỉ sử dụng dữ liệu mẫu.

Các mục tiêu cụ thể:

- Kết nối frontend với Backend API.
- Xây dựng hoặc rà soát cơ chế gửi HTTP request.
- Tích hợp chức năng đăng nhập và xác thực JWT.
- Hiển thị danh sách dịch vụ từ backend.
- Tích hợp các chức năng đặt lịch và quản lý booking.
- Phân biệt giao diện và chức năng theo vai trò `user`, `staff`, `admin`.
- Xử lý trạng thái tải dữ liệu, phản hồi thành công và lỗi API.
- Kiểm tra tính nhất quán dữ liệu giữa frontend, backend và MySQL.

## 2. Phạm vi tích hợp

Các nhóm chức năng dự kiến tích hợp gồm:

| Nhóm chức năng | API liên quan   | Nội dung tích hợp                            |
|----------------|-----------------|----------------------------------------------|
| Xác thực       | `/api/auth`     | Đăng nhập, đăng ký, đổi mật khẩu             |
| Dịch vụ        | `/api/services` | Hiển thị danh sách dịch vụ                   |
| Đặt lịch       | `/api/bookings` | Gửi thông tin đặt lịch và nhận kết quả       |
| Khách hàng     | `/api/user`     | Truy xuất dữ liệu thuộc tài khoản khách hàng |
| Nhân viên      | `/api/staff`    | Xem và xử lý công việc được phân công        |
| Quản trị viên  | `/api/admin`    | Tích hợp các chức năng quản trị              |

## 3. Kiến trúc giao tiếp

Frontend gửi HTTP request đến backend. Backend tiếp nhận yêu cầu, xác thực và phân quyền khi cần, thực hiện xử lý nghiệp vụ và truy vấn MySQL, sau đó trả về phản hồi JSON.

Quy trình tổng quát:

1. Người dùng thao tác trên giao diện.
2. Frontend kiểm tra dữ liệu đầu vào cơ bản.
3. Frontend gửi request đến endpoint tương ứng.
4. Backend xác thực token và kiểm tra quyền truy cập.
5. Backend xử lý nghiệp vụ và truy vấn cơ sở dữ liệu.
6. Backend trả về dữ liệu hoặc thông báo lỗi.
7. Frontend cập nhật giao diện dựa trên kết quả nhận được.

## 4. Cấu hình kết nối API

Frontend cần sử dụng địa chỉ backend phù hợp với môi trường chạy.

Trong môi trường phát triển cục bộ, backend hiện được kiểm thử tại:

`http://localhost:5000`

Nếu frontend sử dụng Vite, có thể cấu hình biến môi trường trong file `.env` của frontend:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Ví dụ sử dụng `fetch` để lấy danh sách dịch vụ:

```javascript
const API_BASE_URL = import.meta.env.VITE_API_BASE_URL;

export async function getServices() {
  const response = await fetch(`${API_BASE_URL}/services`);

  if (!response.ok) {
    throw new Error(`Không thể lấy danh sách dịch vụ: ${response.status}`);
  }

  return response.json();
}
```

Đoạn mã trên là ví dụ tham khảo. Cần điều chỉnh theo cấu trúc thực tế của frontend và tránh tạo thêm hàm trùng lặp nếu dự án đã có API client.

## 5. Tích hợp xác thực và phân quyền

### 5.1. Đăng nhập

Frontend gửi thông tin đăng nhập đến:

`POST /api/auth/login`

Khi đăng nhập thành công, backend trả về access token và thông tin người dùng.

Frontend cần:

- Kiểm tra phản hồi đăng nhập.
- Lưu trữ token theo cơ chế phù hợp với kiến trúc bảo mật của ứng dụng.
- Cập nhật trạng thái đăng nhập.
- Điều hướng người dùng đến giao diện tương ứng với vai trò.
- Hiển thị thông báo phù hợp khi thông tin đăng nhập không chính xác.

### 5.2. Gửi token

Đối với API yêu cầu xác thực, frontend gửi token trong header:

```http
Authorization: Bearer <access_token>
```

Ví dụ:

```javascript
const response = await fetch(`${API_BASE_URL}/staff/bookings`, {
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```

Token cần được xử lý khi hết hạn hoặc không hợp lệ. Frontend không nên tiếp tục sử dụng token đã hết hạn.

### 5.3. Xử lý lỗi phân quyền

Backend đã được kiểm thử với các kết quả:

- `401 Unauthorized`: yêu cầu thiếu token hoặc token không hợp lệ.
- `403 Forbidden`: tài khoản đã xác thực nhưng không có quyền phù hợp.

Frontend cần hiển thị thông báo dễ hiểu, đồng thời không cho phép người dùng chỉ dựa vào việc ẩn nút hoặc ẩn trang để vượt qua kiểm tra phân quyền phía backend.

## 6. Tích hợp danh sách dịch vụ

Endpoint:

`GET /api/services`

Kết quả kiểm thử backend

- Mã HTTP: `200 OK`.
- Dữ liệu trả về ở định dạng JSON.
- Có 5 bản ghi dịch vụ tại thời điểm kiểm thử.

Frontend cần sử dụng dữ liệu API để hiển thị tên dịch vụ, thời lượng và các thông tin cần thiết cho quy trình đặt lịch.

Các nội dung cần kiểm tra:

- Danh sách dịch vụ hiển thị chính xác.
- Giao diện xử lý trường hợp danh sách rỗng.
- Có trạng thái tải dữ liệu.
- Có thông báo khi API lỗi.
- Thông tin dịch vụ được sử dụng nhất quán trong form đặt lịch.

## 7. Tích hợp quy trình đặt lịch

Quy trình đặt lịch cần được kiểm tra từ đầu đến cuối:

1. Người dùng chọn dịch vụ.
2. Người dùng nhập thông tin khách hàng và địa chỉ.
3. Người dùng chọn ngày, giờ thực hiện.
4. Frontend kiểm tra các trường bắt buộc.
5. Frontend gửi yêu cầu tạo booking đến endpoint phù hợp trong `/api/bookings`.
6. Backend kiểm tra dữ liệu và thực hiện nghiệp vụ.
7. Frontend hiển thị kết quả và cập nhật danh sách booking nếu thành công.

Các nội dung cần xác minh:

- Tên và kiểu dữ liệu của các trường request.
- Quy tắc kiểm tra ngày giờ.
- Xử lý thời lượng dịch vụ.
- Phản hồi khi dữ liệu không hợp lệ.
- Tránh gửi yêu cầu tạo booking nhiều lần do người dùng nhấn nút liên tục.
- Hiển thị đúng thông tin booking sau khi tạo.

Endpoint và cấu trúc request cụ thể phải được đối chiếu với route và controller thực tế trước khi triển khai.

## 8. Tích hợp giao diện nhân viên

Endpoint đã kiểm thử:

`GET /api/staff/bookings`

Kết quả thực tế khi sử dụng tài khoản nhân viên hợp lệ:

- Mã HTTP: `200 OK`.
- API trả về danh sách công việc được phân công cho nhân viên.
- Dữ liệu bao gồm thông tin dịch vụ, lịch hẹn và trạng thái công việc.

Frontend cần hiển thị các thông tin phù hợp, chẳng hạn:

- Mã booking.
- Tên khách hàng.
- Địa chỉ thực hiện.
- Dịch vụ.
- Ngày và giờ dự kiến.
- Trạng thái booking.
- Trạng thái phân công.

## 9. Xử lý lỗi và trạng thái giao diện

Frontend cần có cơ chế xử lý tối thiểu cho các tình huống:

| Tình huống       | Cách xử lý đề xuất                             |
|------------------|------------------------------------------------| 
| Đang tải dữ liệu | Hiển thị trạng thái loading                    |
| API trả về `200` | Cập nhật dữ liệu                               |
| API trả về `400` | Hiển thị lỗi dữ liệu đầu vào                   |
| API trả về `401` | Thông báo phiên đăng nhập không hợp lệ         |
| API trả về `403` | Thông báo không đủ quyền                       |
| API trả về `404` | Thông báo không tìm thấy dữ liệu               |
| API trả về `409` | Hiển thị xung đột nghiệp vụ phù hợp            |
| API trả về `500` | Thông báo lỗi hệ thống và ghi nhận để kiểm tra |

## 10. Kiểm thử tích hợp

Các bước kiểm thử cần thực hiện:

| STT | Nội dung                                     | Kết quả cần xác nhận                       |
|-----|----------------------------------------------|--------------------------------------------|
| 1   | Frontend kết nối backend                     | Request đến đúng địa chỉ                   |
| 2   | Tải danh sách dịch vụ                        | Hiển thị dữ liệu API                       |
| 3   | Đăng nhập thành công                         | Nhận và sử dụng token                      |
| 4   | Truy cập API không có token                  | Backend từ chối với `401`                  |
| 5   | Tài khoản sai vai trò truy cập API staff     | Backend từ chối với `403`                  |
| 6   | Tài khoản staff truy cập danh sách công việc | Backend trả về `200`                       |
| 7   | Tạo booking từ giao diện                     | Dữ liệu được backend xử lý chính xác       |
| 8   | Cập nhật trạng thái booking                  | Giao diện phản ánh kết quả backend         |
| 9   | API gặp lỗi                                  | Giao diện hiển thị thông báo phù hợp       |
| 10  | Tải lại trang                                | Trạng thái và dữ liệu được xử lý nhất quán |

Các trường hợp 1–6 đã có kết quả kiểm thử backend hoặc HTTP tương ứng.

## 11. Kết luận

Backend đã được kiểm thử thành công đối với API dịch vụ và API danh sách công việc nhân viên. Cơ chế từ chối yêu cầu thiếu token, token không hợp lệ và tài khoản sai vai trò cũng đã được xác nhận.

Tuy nhiên, kết quả kiểm thử backend chưa đủ để kết luận toàn bộ frontend và backend đã tích hợp hoàn chỉnh.