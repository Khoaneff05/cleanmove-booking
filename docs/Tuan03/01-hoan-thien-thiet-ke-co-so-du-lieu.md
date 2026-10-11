# 1. HOÀN THIỆN THIẾT KẾ CƠ SỞ DỮ LIỆU

## 1.1. Mục tiêu

Trong tuần 3, tiến hành khảo sát và rà soát cơ sở dữ liệu của hệ thống CleanMove nhằm đánh giá mức độ phù hợp giữa thiết kế dữ liệu và các chức năng quản lý đặt lịch, cung cấp dịch vụ vệ sinh, phân công nhân viên và theo dõi trạng thái công việc.

Nội dung thực hiện bao gồm kiểm tra danh sách bảng, cấu trúc trường dữ liệu, kiểu dữ liệu, khóa chính, khóa ngoại, các ràng buộc và mối quan hệ giữa các bảng. Đồng thời, rà soát những điểm có khả năng gây mất đồng bộ dữ liệu hoặc ảnh hưởng đến hoạt động của Backend.

## 1.2. Công nghệ sử dụng

- Hệ quản trị cơ sở dữ liệu: MySQL.
- Ngôn ngữ truy vấn: SQL.
- Phương pháp khảo sát: truy vấn thông tin từ `INFORMATION_SCHEMA`, kiểm tra cấu trúc bảng và các quan hệ khóa ngoại.

## 1.3. Tổng quan cơ sở dữ liệu

Qua quá trình kiểm tra, cơ sở dữ liệu hiện tại gồm 6 bảng:

| STT | Tên bảng | Chức năng |
|---|---|---|
| 1 | `users` | Lưu tài khoản người dùng và vai trò. |
| 2 | `services` | Lưu danh sách dịch vụ và thời lượng thực hiện. |
| 3 | `bookings` | Quản lý thông tin yêu cầu đặt lịch. |
| 4 | `booking_assignments` | Theo dõi việc phân công nhân viên và phản hồi nhận công việc. |
| 5 | `booking_status_history` | Lưu lịch sử thay đổi trạng thái đặt lịch. |
| 6 | `staff_schedule_locks` | Hỗ trợ khóa lịch nhân viên trong quá trình xử lý. |

## 1.4. Chi tiết thiết kế các bảng

### 1.4.1. Bảng `users`

Bảng `users` lưu thông tin tài khoản và vai trò của người sử dụng hệ thống.

| Trường | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | INT | PK, AUTO_INCREMENT | Mã người dùng. |
| `username` | VARCHAR(50) | NOT NULL, UNIQUE | Tên đăng nhập. |
| `password_hash` | VARCHAR(255) | NOT NULL | Mật khẩu đã được băm. |
| `role` | ENUM | DEFAULT 'user', NULL | Vai trò: user, admin hoặc staff. |

Trường `password_hash` được sử dụng để lưu giá trị mật khẩu đã băm thay vì lưu mật khẩu dạng văn bản thuần. Trường `role` hỗ trợ xác định nhóm quyền của tài khoản khi truy cập các chức năng hệ thống.

### 1.4.2. Bảng `services`

Bảng `services` lưu thông tin các dịch vụ mà hệ thống cung cấp.

| Trường | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | INT | PK, AUTO_INCREMENT | Mã dịch vụ. |
| `name` | VARCHAR(100) | NOT NULL | Tên dịch vụ. |
| `duration_minutes` | INT UNSIGNED | NOT NULL, DEFAULT 120 | Thời lượng dịch vụ tính bằng phút. |

### 1.4.3. Bảng `bookings`

Bảng `bookings` lưu thông tin chính của mỗi yêu cầu đặt lịch.

| Trường | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | INT | PK, AUTO_INCREMENT | Mã đặt lịch. |
| `customer_name` | VARCHAR(100) | NOT NULL | Tên khách hàng. |
| `address` | VARCHAR(255) | NOT NULL | Địa chỉ thực hiện dịch vụ. |
| `date_time` | DATETIME | NOT NULL | Ngày và giờ đặt lịch. |
| `service_id` | INT | FK, NULL | Mã dịch vụ được chọn. |
| `user_id` | INT | FK, NULL | Tài khoản tạo yêu cầu. |
| `status` | ENUM | NOT NULL, DEFAULT 'pending' | Trạng thái đặt lịch. |
| `assigned_staff_id` | INT | FK, NULL | Nhân viên được gán trực tiếp trên yêu cầu. |
| `assignment_status` | ENUM | NOT NULL, DEFAULT 'unassigned' | Trạng thái phân công. |
| `duration_minutes` | INT UNSIGNED | NULL | Thời lượng dự kiến của công việc. |

Trường `status` có các giá trị:

- `pending`: yêu cầu đang chờ xử lý.
- `in_progress`: công việc đang được thực hiện.
- `completed`: công việc đã hoàn thành.
- `cancelled`: yêu cầu đã bị hủy.

Trường `assignment_status` có các giá trị:

- `unassigned`: chưa phân công.
- `assigned`: đã phân công.
- `accepted`: nhân viên đã chấp nhận công việc.
- `rejected_pending_review`: nhân viên từ chối và đang chờ xem xét.
- `released`: công việc đã được giải phóng khỏi phân công hiện tại.

Bảng `bookings` đóng vai trò trung tâm trong quy trình đặt lịch. Thông tin dịch vụ, khách hàng và nhân viên được liên kết thông qua các trường mã tương ứng.

### 1.4.4. Bảng `booking_assignments`

Bảng `booking_assignments` quản lý thông tin phân công công việc cho nhân viên, bao gồm kết quả phản hồi và quá trình xem xét việc từ chối.

| Trường | Kiểu dữ liệu | Mô tả |
|---|---|---|
| `id` | INT | Mã bản ghi phân công, khóa chính tự tăng. |
| `booking_id` | INT | Mã yêu cầu đặt lịch được phân công. |
| `staff_id` | INT | Mã nhân viên được phân công. |
| `status` | ENUM | Trạng thái phân công: assigned, accepted, rejected hoặc released. |
| `is_active` | TINYINT(1) | Đánh dấu phân công đang có hiệu lực. |
| `assigned_by` | INT | Người thực hiện phân công. |
| `assigned_at` | TIMESTAMP | Thời điểm phân công. |
| `responded_at` | TIMESTAMP | Thời điểm nhân viên phản hồi. |
| `rejection_reason` | VARCHAR(500) | Lý do từ chối công việc. |
| `rejected_at` | TIMESTAMP | Thời điểm từ chối. |
| `rejection_status` | ENUM | Trạng thái xem xét việc từ chối. |
| `reviewed_by` | INT | Người thực hiện xem xét. |
| `reviewed_at` | TIMESTAMP | Thời điểm xem xét. |
| `review_note` | VARCHAR(500) | Ghi chú xem xét. |
| `released_at` | TIMESTAMP | Thời điểm giải phóng phân công. |
| `released_by` | INT | Người thực hiện giải phóng. |
| `created_at` | TIMESTAMP | Thời điểm tạo bản ghi. |
| `updated_at` | TIMESTAMP | Thời điểm cập nhật gần nhất. |

Trạng thái xem xét việc từ chối gồm `pending_review`, `approved` và `dismissed`.

### 1.4.5. Bảng `booking_status_history`

Bảng `booking_status_history` lưu lịch sử thay đổi trạng thái của yêu cầu đặt lịch.

| Trường | Kiểu dữ liệu | Mô tả |
|---|---|---|
| `id` | INT | Mã bản ghi lịch sử, khóa chính tự tăng. |
| `booking_id` | INT | Mã yêu cầu đặt lịch liên quan. |
| `old_status` | VARCHAR(32) | Trạng thái trước khi thay đổi. |
| `new_status` | VARCHAR(32) | Trạng thái sau khi thay đổi. |
| `actor_id` | INT | Mã người thực hiện thay đổi. |
| `actor_role` | VARCHAR(16) | Vai trò của người thực hiện. |
| `reason` | VARCHAR(255) | Lý do thay đổi trạng thái. |
| `changed_at` | TIMESTAMP | Thời điểm ghi nhận thay đổi. |

Mỗi bản ghi lịch sử được liên kết với một yêu cầu đặt lịch thông qua trường `booking_id`.

### 1.4.6. Bảng `staff_schedule_locks`

Bảng `staff_schedule_locks` hỗ trợ kiểm soát việc truy cập hoặc cập nhật lịch của nhân viên trong quá trình xử lý công việc.

| Trường | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `staff_id` | INT | PK, FK | Mã nhân viên. |
| `locked_at` | TIMESTAMP | NOT NULL | Thời điểm khóa được tạo hoặc cập nhật. |

Trường `staff_id` vừa là khóa chính vừa là khóa ngoại tham chiếu đến bảng `users`. Thiết kế này cho phép mỗi nhân viên có tối đa một bản ghi khóa lịch tại một thời điểm.

## 1.5. Các mối quan hệ giữa các bảng

Qua kết quả kiểm tra khóa ngoại, hệ thống hiện có các quan hệ sau:

| Bảng nguồn | Trường khóa ngoại | Bảng đích | Trường tham chiếu |
|---|---|---|---|
| `bookings` | `user_id` | `users` | `id` |
| `bookings` | `service_id` | `services` | `id` |
| `bookings` | `assigned_staff_id` | `users` | `id` |
| `booking_assignments` | `booking_id` | `bookings` | `id` |
| `booking_assignments` | `staff_id` | `users` | `id` |
| `booking_assignments` | `assigned_by` | `users` | `id` |
| `booking_assignments` | `reviewed_by` | `users` | `id` |
| `booking_assignments` | `released_by` | `users` | `id` |
| `booking_status_history` | `booking_id` | `bookings` | `id` |
| `staff_schedule_locks` | `staff_id` | `users` | `id` |

## 1.6. Đánh giá và các vấn đề cần rà soát

### 1.6.1. Điểm đã đạt được

- Đã xác định được 6 bảng đang tồn tại trong cơ sở dữ liệu.
- Các bảng chính có khóa chính để định danh bản ghi.
- Đã khai báo các quan hệ khóa ngoại giữa đặt lịch, dịch vụ, người dùng, phân công và lịch sử trạng thái.
- Đã tách riêng thông tin đặt lịch, thông tin phân công và lịch sử thay đổi trạng thái.
- Đã có các trường phục vụ theo dõi thời điểm tạo, cập nhật, phản hồi và giải phóng phân công.

### 1.6.2. Các vấn đề cần kiểm tra thêm

**Thứ nhất, tính nhất quán của trạng thái phân công.**

Bảng `bookings` có trường `assignment_status`, trong khi bảng `booking_assignments` có trường `status` và `is_active`. Cần rà soát các API để bảo đảm trạng thái trên yêu cầu đặt lịch và bản ghi phân công được cập nhật đúng quy tắc nghiệp vụ.

**Thứ hai, thông tin nhân viên được phân công.**

Trường `bookings.assigned_staff_id` cùng tồn tại với `booking_assignments.staff_id`. Cần xác định cách đồng bộ hai trường và quy định rõ nguồn dữ liệu chính khi phân công, tiếp nhận, từ chối hoặc giải phóng công việc.

**Thứ ba, lịch sử thao tác.**

Trường `actor_id` trong bảng `booking_status_history` chưa có khóa ngoại đến `users` theo kết quả khảo sát. Cần xem xét yêu cầu lưu vết thao tác, khả năng giữ lịch sử khi tài khoản bị xóa và chính sách toàn vẹn dữ liệu trước khi quyết định bổ sung ràng buộc.

**Thứ tư, cơ chế khóa lịch nhân viên.**

Cần kiểm tra quy trình tạo và giải phóng khóa trong Backend, đặc biệt khi xảy ra lỗi giữa quá trình xử lý hoặc có nhiều yêu cầu phân công cùng lúc.

**Thứ năm, các trường thông tin tài khoản và nghiệp vụ.**

Cần đối chiếu với yêu cầu chức năng để xác định liệu hệ thống có cần bổ sung email, số điện thoại, thông tin liên hệ, giá dịch vụ hoặc các trường khác hay không. Không bổ sung trường chỉ vì chúng thường xuất hiện trong các hệ thống tương tự.