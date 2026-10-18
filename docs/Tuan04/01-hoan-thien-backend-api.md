# 01. Hoàn thiện Backend API

## 1. Mục tiêu

Hoàn thiện và rà soát Backend API của hệ thống CleanMove nhằm bảo đảm các chức năng phía máy chủ hoạt động ổn định, dữ liệu được truy xuất từ cơ sở dữ liệu chính xác và các API được bảo vệ bằng cơ chế xác thực, phân quyền phù hợp.

Các mục tiêu chính:

- Rà soát cấu trúc và cách tổ chức mã nguồn backend.
- Kiểm tra kết nối giữa backend và cơ sở dữ liệu MySQL.
- Kiểm tra cơ chế đăng nhập và xác thực bằng JSON Web Token (JWT).
- Kiểm tra phân quyền truy cập API theo vai trò người dùng.
- Kiểm thử các API dịch vụ và danh sách công việc của nhân viên.
- Chạy bộ kiểm thử tự động để phát hiện lỗi hồi quy.
- Ghi nhận kết quả kiểm thử và xác định các hạng mục cần tiếp tục hoàn thiện.

## 2. Công nghệ sử dụng

| Công nghệ            | Vai trò                                    |
|----------------------|--------------------------------------------|
| Node.js              | Môi trường thực thi backend                |
| Express.js 5         | Xây dựng máy chủ và định tuyến API         |
| MySQL                | Hệ quản trị cơ sở dữ liệu                  |
| mysql2               | Kết nối và truy vấn MySQL                  |
| JSON Web Token (JWT) | Xác thực người dùng thông qua access token |
| bcryptjs             | Băm và so sánh mật khẩu                    |
| Node.js Test Runner  | Thực thi các bài kiểm thử tự động          |
| PowerShell           | Gửi HTTP request và kiểm thử API thủ công  |

## 3. Cấu trúc backend

Backend được tổ chức theo các thành phần có trách nhiệm riêng biệt, hỗ trợ việc phát triển, kiểm thử và bảo trì.

Các thành phần chính đã được rà soát gồm:

- `app.js`: Khởi tạo ứng dụng Express và đăng ký các nhóm route.
- `server.js`: Khởi động máy chủ backend.
- `routes/`: Định nghĩa các endpoint API.
- `controllers/`: Xử lý yêu cầu và trả về phản hồi HTTP.
- `middlewares/`: Xác thực JWT và kiểm tra quyền truy cập.
- `config/`: Cấu hình kết nối và các thành phần hệ thống.

Các nhóm API được đăng ký trong ứng dụng:

| Prefix          | Chức năng                          |
|-----------------|------------------------------------|
| `/api/auth`     | Đăng nhập, đăng ký và đổi mật khẩu |
| `/api/admin`    | Chức năng dành cho quản trị viên   |
| `/api/user`     | Chức năng dành cho khách hàng      |
| `/api/bookings` | Các thao tác đặt lịch              |
| `/api/staff`    | Chức năng dành cho nhân viên       |
| `/api/services` | Truy xuất danh sách dịch vụ        |

## 4. Hoàn thiện xác thực và phân quyền

### 4.1. Xác thực bằng JWT

Hệ thống sử dụng JWT để xác thực các yêu cầu đến những API cần đăng nhập.

Sau khi đăng nhập thành công, backend trả về access token cùng thông tin người dùng. Token chứa các thông tin cần thiết như mã người dùng và vai trò; thời hạn token được cấu hình là một giờ.

Các yêu cầu đến API được bảo vệ cần gửi token trong header:

`Authorization: Bearer <access_token>`

Middleware kiểm tra sự hiện diện và tính hợp lệ của token trước khi cho phép yêu cầu đi tiếp.

### 4.2. Chuẩn hóa phản hồi lỗi xác thực

Các trường hợp thiếu token, token sai định dạng, token không hợp lệ hoặc token hết hạn được xử lý theo hướng trả về mã HTTP `401 Unauthorized`.

Ví dụ phản hồi khi không gửi token:

```json
{
  "message": "Access token is required."
}
```

Ví dụ phản hồi khi token không hợp lệ hoặc hết hạn:

```json
{
  "message": "Invalid or expired access token."
}
```

Việc chuẩn hóa phản hồi giúp frontend nhận biết tình trạng xác thực và xử lý phù hợp.

### 4.3. Phân quyền theo vai trò

Hệ thống có ba vai trò chính:

- `admin`: Quản trị viên.
- `user`: Khách hàng.
- `staff`: Nhân viên thực hiện dịch vụ.

Middleware phân quyền kiểm tra vai trò trong thông tin người dùng đã được xác thực trước khi cho phép truy cập API tương ứng.

Đối với API nhân viên, tài khoản không có vai trò `staff` bị từ chối với mã HTTP `403 Forbidden`.

Ví dụ phản hồi khi tài khoản không đủ quyền nhân viên:

```json
{
  "message": "Staff permission required."
}
```

## 5. Kiểm thử API thực tế

Các kiểm thử HTTP được thực hiện với backend chạy tại `http://localhost:5000`.

### 5.1. Kiểm tra API dịch vụ

**Endpoint:** `GET /api/services`

Kết quả thực tế:

- Mã HTTP: `200 OK`.
- API trả về danh sách dịch vụ dạng JSON.
- Dữ liệu nhận được tại thời điểm kiểm thử gồm 5 bản ghi.

Một số dịch vụ trong kết quả:

- Carpet Cleaning.
- Window Cleaning.
- Deep Cleaning.
- Sofa Cleaning.

**Đánh giá:** API trả về dữ liệu thành công tại thời điểm kiểm thử.

### 5.2. Kiểm tra API khi thiếu token

Các endpoint được kiểm tra:

| Endpoint                  | Mã HTTP thực tế |
|---------------------------|-----------------|
| `GET /api/admin/bookings` | `401`           |
| `GET /api/user/bookings` -| `401`           |
| `GET /api/staff/bookings` | `401`           |

Các yêu cầu không có access token đều bị từ chối.

**Đánh giá:** Đạt đối với các trường hợp kiểm thử thiếu token đã thực hiện.

### 5.3. Kiểm tra token không hợp lệ

**Endpoint:** `GET /api/staff/bookings`

Sử dụng token giả để kiểm tra phản ứng của middleware.

Kết quả thực tế sau khi cập nhật middleware:

- Mã HTTP: `401 Unauthorized`.
- Phản hồi JSON thông báo token không hợp lệ hoặc đã hết hạn.

**Đánh giá:** Đạt đối với trường hợp token không hợp lệ.

### 5.4. Kiểm tra tài khoản không đủ quyền

**Endpoint:** `GET /api/staff/bookings`

Sử dụng JWT hợp lệ của tài khoản có vai trò `user`.

Kết quả thực tế:

- Mã HTTP: `403 Forbidden`.
- Nội dung: `Staff permission required.`

**Đánh giá:** Đạt. Người dùng đã đăng nhập nhưng không có quyền nhân viên nên không được phép truy cập API.

### 5.5. Kiểm tra tài khoản nhân viên hợp lệ

**Endpoint:** `GET /api/staff/bookings`

Sử dụng JWT hợp lệ của tài khoản nhân viên có mã người dùng `13`.

Kết quả thực tế:

- Mã HTTP: `200 OK`.
- API trả về 3 bản ghi công việc được gán cho nhân viên này tại thời điểm kiểm thử.
- Dữ liệu bao gồm thông tin lịch hẹn, dịch vụ, trạng thái booking, trạng thái phân công và thời lượng dịch vụ.

Một số trường dữ liệu quan trọng:

- `assigned_staff_id`: Mã nhân viên được phân công.
- `assignment_status`: Trạng thái phân công.
- `effective_duration_minutes`: Thời lượng dịch vụ được áp dụng.
- `scheduled_start`: Thời gian bắt đầu dự kiến.
- `scheduled_end`: Thời gian kết thúc dự kiến.
- `service_name`: Tên dịch vụ.

**Đánh giá:** Đạt đối với việc xác thực và truy cập danh sách công việc bằng tài khoản nhân viên hợp lệ.

## 6. Kiểm thử tự động

Lệnh kiểm thử được sử dụng:

```powershell
npm test
```

Lệnh này thực thi script:

```json
{
  "scripts": {
    "test": "node --test tests/"
  }
}
```

Kết quả lần chạy gần nhất:

| Chỉ tiêu           | Kết quả          |
|--------------------|------------------|
| Tổng số test       | 32               |
| Test thành công    | 32               |
| Test thất bại      | 0                |
| Thời gian thực thi | Khoảng 2,11 giây |

Các nhóm kiểm thử được bao gồm trong bộ test hiện có:

- Xử lý đổi mật khẩu.
- Xác thực và kiểm tra JWT.
- Quy trình xử lý booking.
- Kiểm tra quyền sở hữu phân công công việc.
- Kiểm tra chuyển đổi trạng thái.
- Truy xuất danh sách booking dành cho nhân viên và quản trị viên.

**Đánh giá:** Bộ kiểm thử tự động hiện có đạt 32/32 test trong lần chạy gần nhất. Kết quả này không đồng nghĩa toàn bộ API hoặc mọi tình huống tích hợp đã được kiểm thử đầy đủ.

## 7. Tổng hợp kết quả

| Hạng mục                                    | Kết quả                |
|---------------------------------------------|------------------------|
| Khởi động backend và kết nối MySQL ---------| Thành công             |
| Truy xuất danh sách dịch vụ ----------------| Đạt                    |
| Từ chối yêu cầu thiếu token ----------------| Đạt                    |
| Từ chối token không hợp lệ -----------------| Đạt                    |
| Từ chối tài khoản sai vai trò --------------| Đạt                    |
| Cho phép tài khoản staff truy cập API staff | Đạt                    |
| Bộ kiểm thử tự động hiện có ----------------| 32/32 test pass        |
| Kiểm thử toàn bộ API với frontend ----------| Chưa xác nhận hoàn tất |
| Rà soát toàn bộ quy tắc nghiệp vụ booking --| Cần tiếp tục           |

## 8. Những vấn đề cần tiếp tục rà soát

### 8.1. Dữ liệu kiểm thử

API dịch vụ đang trả về bản ghi `Test1`. Cần xác minh bản ghi này có được sử dụng bởi booking hiện có hay không trước khi xóa hoặc chỉnh sửa.

### 8.2. Trạng thái booking và phân công

Kết quả kiểm thử cho thấy có booking ở trạng thái `in_progress` nhưng lịch dự kiến đã qua ngày kiểm thử. Cần đối chiếu với quy tắc nghiệp vụ để xác định đây là dữ liệu kiểm thử, công việc chưa hoàn tất hay trường hợp cần xử lý riêng.

### 8.3. Tính nhất quán giữa schema và mã nguồn

Cần tiếp tục đối chiếu các truy vấn SQL, cấu trúc bảng và migration để bảo đảm những cột được sử dụng trong backend tồn tại trong database và có kiểu dữ liệu phù hợp.

### 8.4. Kiểm thử tích hợp

Cần kiểm tra thêm các luồng:

- Đăng nhập từ frontend và lưu trữ token.
- Tạo booking và truy xuất booking của khách hàng.
- Tiếp nhận hoặc từ chối công việc của nhân viên.
- Cập nhật trạng thái công việc theo đúng thứ tự nghiệp vụ.
- Hoàn tất công việc và giải phóng phân công nếu quy tắc nghiệp vụ yêu cầu.
- Kiểm tra quyền truy cập API admin, user và staff bằng các tài khoản có vai trò tương ứng.
