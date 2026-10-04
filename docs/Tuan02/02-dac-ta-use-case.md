# 2. ĐẶC TẢ USE CASE

## 2.1. Mục đích

Mô tả chi tiết cách hệ thống xử lý các chức năng chính, bao gồm điều kiện thực hiện, luồng xử lý chính, luồng thay thế và kết quả.

---

## 2.2. UC01 – Đăng ký tài khoản

**Actor:** Khách hàng

**Mục tiêu:** Tạo tài khoản để sử dụng các chức năng dành cho khách hàng.

**Điều kiện:**

* Khách hàng chưa có tài khoản.
* Hệ thống đang hoạt động.

**Luồng chính:**

1. Khách hàng chọn chức năng **Đăng ký**.
2. Hệ thống hiển thị biểu mẫu đăng ký.
3. Khách hàng nhập thông tin cần thiết.
4. Hệ thống kiểm tra tính hợp lệ của thông tin.
5. Hệ thống tạo tài khoản.
6. Hệ thống thông báo đăng ký thành công.

**Luồng thay thế:**

* Thông tin không hợp lệ → Hệ thống yêu cầu nhập lại.
* Email hoặc số điện thoại đã tồn tại → Hệ thống thông báo và yêu cầu sử dụng thông tin khác.

---

## 2.3. UC02 – Đăng nhập

**Actor:** Khách hàng / Nhân viên / Admin

**Mục tiêu:** Xác thực người dùng để truy cập hệ thống theo quyền hạn.

**Điều kiện:** Người dùng đã có tài khoản.

**Luồng chính:**

1. Người dùng chọn **Đăng nhập**.
2. Hệ thống hiển thị biểu mẫu đăng nhập.
3. Người dùng nhập thông tin đăng nhập.
4. Hệ thống kiểm tra thông tin.
5. Hệ thống xác thực tài khoản.
6. Hệ thống chuyển người dùng đến giao diện phù hợp với quyền hạn.

**Luồng thay thế:**

* Sai thông tin đăng nhập → Thông báo lỗi.
* Tài khoản bị khóa → Từ chối đăng nhập.

---

## 2.4. UC03 – Quản lý thông tin cá nhân

**Actor:** Khách hàng

**Mục tiêu:** Xem và cập nhật thông tin cá nhân.

**Điều kiện:** Khách hàng đã đăng nhập.

**Luồng chính:**

1. Khách hàng mở trang **Thông tin cá nhân**.
2. Hệ thống hiển thị thông tin hiện tại.
3. Khách hàng chỉnh sửa thông tin.
4. Khách hàng chọn **Lưu**.
5. Hệ thống kiểm tra dữ liệu.
6. Hệ thống cập nhật thông tin.
7. Hệ thống thông báo thành công.

**Luồng thay thế:**

* Dữ liệu không hợp lệ → Hệ thống yêu cầu chỉnh sửa.

---

## 2.5. UC04 – Xem danh sách dịch vụ

**Actor:** Khách hàng

**Mục tiêu:** Xem các dịch vụ đang được cung cấp.

**Điều kiện:** Không yêu cầu.

**Luồng chính:**

1. Khách hàng truy cập danh sách dịch vụ.
2. Hệ thống tải dữ liệu dịch vụ.
3. Hệ thống hiển thị danh sách.
4. Khách hàng có thể tìm kiếm hoặc lọc dịch vụ.

**Luồng thay thế:**

* Không có dịch vụ phù hợp → Hệ thống hiển thị thông báo.

---

## 2.6. UC05 – Xem chi tiết dịch vụ

**Actor:** Khách hàng

**Mục tiêu:** Xem đầy đủ thông tin của một dịch vụ.

**Điều kiện:** Dịch vụ tồn tại và đang được hiển thị.

**Luồng chính:**

1. Khách hàng chọn một dịch vụ.
2. Hệ thống kiểm tra thông tin dịch vụ.
3. Hệ thống hiển thị tên, mô tả, giá, thời lượng và thông tin liên quan.
4. Khách hàng có thể chọn **Đặt lịch**.

**Luồng thay thế:**

* Dịch vụ không tồn tại hoặc đã ngừng cung cấp → Hệ thống thông báo.

---

## 2.7. UC06 – Đặt lịch dịch vụ

**Actor:** Khách hàng

**Mục tiêu:** Tạo lịch đặt cho một dịch vụ.

**Điều kiện:**

* Khách hàng đã đăng nhập.
* Dịch vụ đang được cung cấp.

**Luồng chính:**

1. Khách hàng chọn dịch vụ.
2. Hệ thống hiển thị thông tin dịch vụ và thời gian có thể đặt.
3. Khách hàng chọn ngày và giờ.
4. Khách hàng nhập thông tin bổ sung nếu cần.
5. Khách hàng xác nhận đặt lịch.
6. Hệ thống kiểm tra thời gian đã chọn.
7. Hệ thống tạo lịch đặt.
8. Hệ thống thông báo đặt lịch thành công.

**Luồng thay thế:**

* Khung giờ đã có người đặt → Hệ thống yêu cầu chọn thời gian khác.
* Dịch vụ không còn khả dụng → Hệ thống thông báo.
* Thông tin đặt lịch không hợp lệ → Hệ thống yêu cầu nhập lại.

---

## 2.8. UC07 – Xem lịch đã đặt

**Actor:** Khách hàng

**Mục tiêu:** Theo dõi các lịch đã đặt và trạng thái xử lý.

**Điều kiện:** Khách hàng đã đăng nhập.

**Luồng chính:**

1. Khách hàng mở **Lịch đã đặt**.
2. Hệ thống truy vấn các lịch của khách hàng.
3. Hệ thống hiển thị danh sách lịch.
4. Khách hàng chọn một lịch để xem chi tiết.

**Luồng thay thế:**

* Không có lịch đặt → Hệ thống thông báo chưa có lịch.

---

## 2.9. UC08 – Hủy lịch

**Actor:** Khách hàng

**Mục tiêu:** Hủy một lịch đặt đã tạo.

**Điều kiện:**

* Khách hàng đã đăng nhập.
* Lịch đặt thuộc tài khoản khách hàng.
* Lịch đang ở trạng thái cho phép hủy.

**Luồng chính:**

1. Khách hàng mở danh sách lịch đã đặt.
2. Khách hàng chọn lịch cần hủy.
3. Hệ thống kiểm tra điều kiện hủy.
4. Hệ thống yêu cầu xác nhận.
5. Khách hàng xác nhận hủy.
6. Hệ thống cập nhật trạng thái lịch.
7. Hệ thống thông báo hủy thành công.

**Luồng thay thế:**

* Lịch không được phép hủy → Hệ thống thông báo lý do.
* Khách hàng không xác nhận → Giữ nguyên lịch.

---

## 2.10. UC09 – Đánh giá dịch vụ

**Actor:** Khách hàng

**Mục tiêu:** Đánh giá chất lượng dịch vụ đã sử dụng.

**Điều kiện:**

* Khách hàng đã đăng nhập.
* Lịch đã hoàn thành.
* Lịch chưa được đánh giá.

**Luồng chính:**

1. Khách hàng chọn lịch đã hoàn thành.
2. Khách hàng chọn chức năng **Đánh giá**.
3. Khách hàng nhập số sao và nhận xét.
4. Hệ thống kiểm tra dữ liệu.
5. Hệ thống lưu đánh giá.
6. Hệ thống thông báo thành công.

**Luồng thay thế:**

* Dữ liệu đánh giá không hợp lệ → Yêu cầu nhập lại.
* Lịch đã được đánh giá → Không cho phép đánh giá lại.

---

## 2.11. UC11 – Quản lý lịch đặt

**Actor:** Nhân viên

**Mục tiêu:** Theo dõi và xử lý các lịch đặt của khách hàng.

**Điều kiện:** Nhân viên đã đăng nhập và có quyền xử lý lịch.

**Luồng chính:**

1. Nhân viên mở chức năng **Quản lý lịch đặt**.
2. Hệ thống hiển thị danh sách lịch.
3. Nhân viên tìm kiếm hoặc lọc lịch.
4. Nhân viên chọn một lịch.
5. Hệ thống hiển thị thông tin chi tiết.
6. Nhân viên thực hiện thao tác phù hợp.
7. Hệ thống cập nhật dữ liệu.

**Luồng thay thế:**

* Không tìm thấy lịch → Hệ thống thông báo.
* Nhân viên không có quyền thao tác → Hệ thống từ chối.

---

## 2.12. UC12 – Xác nhận lịch đặt

**Actor:** Nhân viên

**Mục tiêu:** Xác nhận hoặc từ chối lịch đặt của khách hàng.

**Điều kiện:**

* Nhân viên đã đăng nhập.
* Lịch đang ở trạng thái chờ xác nhận.

**Luồng chính:**

1. Nhân viên mở lịch cần xử lý.
2. Hệ thống hiển thị thông tin lịch.
3. Nhân viên kiểm tra dịch vụ và thời gian.
4. Nhân viên chọn **Xác nhận**.
5. Hệ thống cập nhật trạng thái lịch.
6. Hệ thống lưu thông tin xử lý.

**Luồng thay thế:**

* Thời gian không còn phù hợp → Nhân viên từ chối lịch.
* Thông tin lịch không hợp lệ → Hệ thống yêu cầu kiểm tra lại.

---

## 2.13. UC13 – Cập nhật trạng thái lịch

**Actor:** Nhân viên

**Mục tiêu:** Cập nhật tiến trình cung cấp dịch vụ.

**Điều kiện:** Lịch đã được xác nhận.

**Luồng chính:**

1. Nhân viên chọn lịch cần cập nhật.
2. Hệ thống hiển thị trạng thái hiện tại.
3. Nhân viên chọn trạng thái mới.
4. Hệ thống kiểm tra tính hợp lệ.
5. Hệ thống cập nhật trạng thái.
6. Hệ thống lưu thay đổi.

---

## 2.14. UC16 – Quản lý tài khoản

**Actor:** Admin

**Mục tiêu:** Quản lý tài khoản và quyền truy cập hệ thống.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở chức năng **Quản lý tài khoản**.
2. Hệ thống hiển thị danh sách tài khoản.
3. Admin tìm kiếm hoặc chọn tài khoản.
4. Admin thực hiện thêm, sửa, khóa hoặc phân quyền.
5. Hệ thống kiểm tra dữ liệu.
6. Hệ thống lưu thay đổi.

**Luồng thay thế:**

* Dữ liệu không hợp lệ → Hệ thống yêu cầu chỉnh sửa.
* Tài khoản không tồn tại → Hệ thống thông báo.

---

## 2.15. UC17 – Quản lý dịch vụ

**Actor:** Admin

**Mục tiêu:** Quản lý danh sách và thông tin dịch vụ.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở chức năng **Quản lý dịch vụ**.
2. Hệ thống hiển thị danh sách dịch vụ.
3. Admin chọn thêm mới hoặc chỉnh sửa dịch vụ.
4. Admin nhập thông tin dịch vụ.
5. Hệ thống kiểm tra dữ liệu.
6. Hệ thống lưu thông tin.
7. Hệ thống cập nhật danh sách dịch vụ.

**Luồng thay thế:**

* Dữ liệu không hợp lệ → Yêu cầu nhập lại.
* Dịch vụ đang được sử dụng → Hệ thống hạn chế hoặc từ chối xóa.

---

## 2.16. UC18 – Quản lý lịch đặt

**Actor:** Admin

**Mục tiêu:** Quản lý toàn bộ lịch đặt trong hệ thống.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở chức năng quản lý lịch.
2. Hệ thống hiển thị toàn bộ lịch đặt.
3. Admin tìm kiếm hoặc lọc lịch.
4. Admin xem chi tiết.
5. Admin thực hiện thao tác cần thiết.
6. Hệ thống cập nhật dữ liệu.

---

## 2.17. UC19 – Quản lý nhân viên

**Actor:** Admin

**Mục tiêu:** Quản lý thông tin và quyền hạn của nhân viên.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở danh sách nhân viên.
2. Hệ thống hiển thị thông tin nhân viên.
3. Admin thêm, sửa, khóa hoặc cập nhật quyền.
4. Hệ thống kiểm tra dữ liệu.
5. Hệ thống lưu thay đổi.

---

## 2.18. UC20 – Quản lý đánh giá

**Actor:** Admin

**Mục tiêu:** Theo dõi và xử lý đánh giá của khách hàng.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở chức năng quản lý đánh giá.
2. Hệ thống hiển thị danh sách đánh giá.
3. Admin xem nội dung đánh giá.
4. Admin thực hiện thao tác xử lý nếu cần.
5. Hệ thống lưu thay đổi.

---

## 2.19. UC21 – Xem báo cáo và thống kê

**Actor:** Admin

**Mục tiêu:** Theo dõi tình hình hoạt động của hệ thống.

**Điều kiện:** Admin đã đăng nhập.

**Luồng chính:**

1. Admin mở chức năng báo cáo và thống kê.
2. Hệ thống tổng hợp dữ liệu.
3. Hệ thống hiển thị các chỉ số thống kê.
4. Admin lựa chọn khoảng thời gian hoặc tiêu chí cần xem.