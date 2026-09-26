Hệ thống Web đặt lịch và quản lý dịch vụ vệ sinh, vận chuyển theo yêu cầu

## 1. Giới thiệu

Nhu cầu sử dụng các dịch vụ tiện ích như vệ sinh nhà cửa, văn phòng và vận chuyển hàng hóa/chuyển nhà ngày càng tăng cao. Tuy nhiên, quy trình kết nối giữa khách hàng và đơn vị cung cấp dịch vụ truyền thống thường gặp khó khăn trong việc báo giá minh bạch, theo dõi tiến độ và quản lý lịch làm việc của nhân viên.

Hệ thống được xây dựng nhằm hỗ trợ khách hàng đặt lịch sử dụng các dịch vụ vệ sinh và vận chuyển theo yêu cầu thông qua nền tảng Web.

Đồng thời, hệ thống hỗ trợ nhân viên và quản lý trong việc tiếp nhận, báo giá, phân công, thực hiện và theo dõi trạng thái các đơn dịch vụ.

## 2. Phạm vi hệ thống

Hệ thống tập trung vào hai nhóm dịch vụ chính:

* Dịch vụ vệ sinh
* Dịch vụ vận chuyển

Các nhóm người dùng chính:

1. *Khách hàng (Customer):* Người tìm kiếm và đăng ký sử dụng dịch vụ.
2. *Nhân viên (Staff):* Người trực tiếp thực hiện các ca dịch vụ vệ sinh/vận chuyển.
3. *Quản trị viên / Quản lý (Admin/Manager):* Người điều hành, phân công, quản lý dữ liệu và doanh thu.

## 3. Quy trình nghiệp vụ chính

[Khách hàng] Gửi yêu cầu đặt dịch vụ
       │
       ▼
[Quản lý] Tiếp nhận & Kiểm tra thông tin
       │
       ▼
[Quản lý] Nhập báo giá & Xác nhận yêu cầu
       │
       ▼
[Quản lý] Phân công Nhân viên thực hiện
       │
       ▼
[Nhân viên] Tiếp nhận ca & Thực hiện dịch vụ
       │
       ▼
[Nhân viên/Quản lý] Cập nhật trạng thái ➔ Hoàn thành đơn

## 4. Chức năng chính
## 4.1. Yêu cầu chức năng (Functional Requirements)
### Khách hàng

* Xác thực: Đăng ký, đăng nhập, đăng xuất, cập nhật thông tin cá nhân.

* Tra cứu: Xem danh mục dịch vụ (Vệ sinh, Vận chuyển), tìm kiếm, lọc và xem chi tiết từng dịch vụ.

* Đặt lịch: Gửi yêu cầu đặt dịch vụ, chọn mốc thời gian, địa điểm và chi tiết ghi chú.

* Theo dõi & Quản lý: Xem báo giá từ quản lý, theo dõi trạng thái đơn (Mới tạo ➔ Đã báo giá ➔ Đã phân công ➔ Đang thực hiện ➔ Hoàn thành ➔ Hủy), xem lịch sử đặt lịch và hủy yêu cầu khi thỏa điều kiện.

### Nhân viên

* Xác thực: Đăng nhập hệ thống.

* Quản lý ca làm: Xem danh sách công việc được phân công, chi tiết địa điểm, thời gian và yêu cầu dịch vụ.

* Cập nhật tiến độ: Cập nhật trạng thái thực hiện công việc (Đã tiếp nhận ➔ Đang thực hiện ➔ Hoàn thành) và xem lịch sử ca làm.

### Quản lý / Quản trị viên

* Quản lý danh mục: CRUD Tài khoản, Loại dịch vụ, Dịch vụ.

* Xử lý đơn: Tiếp nhận yêu cầu, nhập báo giá, duyệt/từ chối đơn, phân công nhân viên phụ trách.

* Giám sát & Báo cáo: Đổi trạng thái xử lý đơn hàng, xem Dashboard thống kê số lượng đơn và doanh thu cơ bản (theo ngày/tháng/dịch vụ).

## 4.2. Yêu cầu phi chức năng (Non-Functional Requirements)
* Giao diện: Hiển thị chuẩn, tương thích mượt mà trên cả Laptop/Desktop và thiết bị di động.

*Bảo mật & Xác thực: Phân quyền người dùng chặt chẽ.

* Lưu trữ & Dữ liệu: Sử dụng CSDL quan hệ đảm bảo tính toàn vẹn dữ liệu.

## 5. Tiến độ thực hiện

| Tuần | Nội dung                              | Trạng thái     |
| ---- | ------------------------------------- | -------------- |
| 1    | Khảo sát bài toán và xác định yêu cầu | Đang thực hiện |
| 2    | Phân tích và thiết kế hệ thống        | Chưa thực hiện |
| 3    | Xây dựng nền tảng hệ thống            | Chưa thực hiện |
| 4    | Xây dựng chức năng quản lý dữ liệu    | Chưa thực hiện |
| 5    | Xây dựng nghiệp vụ đặt lịch           | Chưa thực hiện |
| 6    | Hoàn thiện nghiệp vụ và thống kê      | Chưa thực hiện |
| 7    | Kiểm thử và triển khai                | Chưa thực hiện |
| 8    | Hoàn thiện và bàn giao                | Chưa thực hiện |

## 7. Cấu trúc thư mục dự án
├── docs/                     # Tài liệu phân tích, thiết kế, Test Case, Sổ nhật ký
│   └── images/               # Hình ảnh sơ đồ, wireframe
└── README.md                 # Tài liệu giới thiệu dự án
