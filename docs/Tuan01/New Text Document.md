# 3. Yêu cầu chức năng

## 3.1. Tổng quan

Hệ thống Web đặt lịch và quản lý dịch vụ vệ sinh, vận chuyển theo yêu cầu cung cấp các chức năng phục vụ ba nhóm người dùng chính:

* **Khách hàng:** tìm hiểu dịch vụ, gửi yêu cầu đặt dịch vụ, theo dõi báo giá và trạng thái xử lý.
* **Nhân viên:** tiếp nhận công việc được phân công, cập nhật trạng thái và kết quả thực hiện dịch vụ.
* **Quản trị viên:** quản lý người dùng, nhân viên, dịch vụ, yêu cầu dịch vụ, báo giá, phân công công việc và theo dõi thống kê.

Các yêu cầu chức năng được phân loại theo từng nhóm nghiệp vụ như sau.

---

## 3.2. Quản lý tài khoản và xác thực

### FR01 – Đăng ký tài khoản

Hệ thống cho phép khách hàng tạo tài khoản bằng các thông tin cơ bản:

* Họ và tên
* Số điện thoại
* Email
* Mật khẩu

Hệ thống phải kiểm tra dữ liệu đầu vào và không cho phép đăng ký khi email hoặc số điện thoại đã tồn tại.

### FR02 – Đăng nhập

Người dùng có thể đăng nhập bằng email/số điện thoại và mật khẩu.

Sau khi đăng nhập, hệ thống xác định quyền của người dùng và điều hướng đến giao diện phù hợp.

### FR03 – Đăng xuất

Người dùng có thể đăng xuất khỏi hệ thống.

Sau khi đăng xuất, phiên đăng nhập hoặc token xác thực phải được vô hiệu hóa theo cơ chế được triển khai.

### FR04 – Quản lý thông tin cá nhân

Khách hàng có thể:

* Xem thông tin tài khoản.
* Cập nhật họ tên.
* Cập nhật số điện thoại.
* Cập nhật địa chỉ.
* Thay đổi mật khẩu.

### FR05 – Phân quyền người dùng

Hệ thống phải phân quyền dựa trên vai trò:

| Vai trò       | Quyền chính                                      |
| ------------- | ------------------------------------------------ |
| Khách hàng    | Đặt dịch vụ, xem và quản lý yêu cầu của bản thân |
| Nhân viên     | Xem và xử lý công việc được phân công            |
| Quản trị viên | Quản lý toàn bộ dữ liệu và nghiệp vụ hệ thống    |

Người dùng không được phép truy cập các chức năng không thuộc quyền của mình.

---

## 3.3. Xem và tìm kiếm dịch vụ

### FR06 – Xem danh sách dịch vụ

Khách hàng có thể xem danh sách các dịch vụ đang được cung cấp.

Dịch vụ được chia thành hai nhóm chính:

* Dịch vụ vệ sinh.
* Dịch vụ vận chuyển.

### FR07 – Xem chi tiết dịch vụ

Khách hàng có thể xem thông tin chi tiết của một dịch vụ, bao gồm:

* Tên dịch vụ.
* Nhóm dịch vụ.
* Mô tả.
* Điều kiện hoặc phạm vi cung cấp.
* Thông tin cần chuẩn bị.
* Trạng thái cung cấp dịch vụ.

### FR08 – Tìm kiếm dịch vụ

Khách hàng có thể tìm kiếm dịch vụ theo từ khóa.

Ví dụ:

* Vệ sinh nhà.
* Vệ sinh văn phòng.
* Chuyển phòng trọ.
* Chuyển nhà.
* Vận chuyển hàng hóa.

### FR09 – Lọc dịch vụ

Khách hàng có thể lọc dịch vụ theo nhóm:

* Vệ sinh.
* Vận chuyển.

Hệ thống có thể hỗ trợ kết hợp tìm kiếm và lọc để giúp khách hàng nhanh chóng tìm được dịch vụ phù hợp.

---

## 3.4. Đặt dịch vụ

### FR10 – Tạo yêu cầu sử dụng dịch vụ

Khách hàng có thể tạo yêu cầu sử dụng một dịch vụ.

Thông tin yêu cầu tối thiểu gồm:

* Dịch vụ cần sử dụng.
* Ngày thực hiện.
* Thời gian dự kiến.
* Địa điểm thực hiện.
* Thông tin liên hệ.
* Ghi chú/yêu cầu bổ sung.

### FR11 – Kiểm tra dữ liệu đặt dịch vụ

Trước khi tạo yêu cầu, hệ thống phải kiểm tra:

* Người dùng đã đăng nhập.
* Dịch vụ còn đang được cung cấp.
* Ngày và thời gian được nhập hợp lệ.
* Các thông tin bắt buộc không được để trống.
* Địa điểm thực hiện hợp lệ theo quy tắc của hệ thống.

Nếu dữ liệu không hợp lệ, hệ thống thông báo lỗi và yêu cầu khách hàng chỉnh sửa.

### FR12 – Tạo mã yêu cầu dịch vụ

Sau khi tạo yêu cầu thành công, hệ thống sinh một mã yêu cầu duy nhất.

Mã này được sử dụng để tra cứu và quản lý yêu cầu trong hệ thống.

### FR13 – Xem yêu cầu đã đặt

Khách hàng có thể xem danh sách các yêu cầu dịch vụ của mình.

Danh sách hiển thị tối thiểu:

* Mã yêu cầu.
* Tên dịch vụ.
* Ngày thực hiện.
* Địa điểm.
* Báo giá.
* Trạng thái.
* Thời gian tạo yêu cầu.

### FR14 – Xem chi tiết yêu cầu

Khách hàng có thể xem toàn bộ thông tin của một yêu cầu dịch vụ.

Thông tin bao gồm:

* Thông tin khách hàng.
* Thông tin dịch vụ.
* Thời gian thực hiện.
* Địa điểm.
* Ghi chú.
* Báo giá.
* Nhân viên được phân công.
* Trạng thái xử lý.
* Lịch sử cập nhật.

---

## 3.5. Báo giá và xác nhận dịch vụ

### FR15 – Tiếp nhận yêu cầu

Quản trị viên có thể xem các yêu cầu mới được gửi từ khách hàng.

Quản trị viên kiểm tra thông tin và quyết định tiếp nhận hoặc từ chối yêu cầu.

### FR16 – Nhập báo giá

Quản trị viên có thể nhập báo giá cho từng yêu cầu dịch vụ.

Báo giá được nhập thủ công dựa trên thông tin thực tế của yêu cầu.

Thông tin báo giá có thể bao gồm:

* Số tiền.
* Ghi chú báo giá.
* Thời gian báo giá.

Hệ thống không yêu cầu tính giá tự động trong phạm vi phiên bản cơ bản.

### FR17 – Khách hàng xem báo giá

Sau khi quản trị viên nhập báo giá, khách hàng có thể xem mức giá được đề xuất.

### FR18 – Xác nhận báo giá

Khách hàng có thể xác nhận sử dụng dịch vụ theo báo giá.

Sau khi xác nhận, yêu cầu chuyển sang trạng thái phù hợp để quản trị viên tiến hành phân công nhân viên.

### FR19 – Từ chối báo giá

Khách hàng có thể từ chối báo giá.

Khi đó yêu cầu được cập nhật trạng thái tương ứng và không tiếp tục quy trình thực hiện dịch vụ.

---

## 3.6. Phân công và xử lý công việc

### FR20 – Phân công nhân viên

Quản trị viên có thể phân công một nhân viên cho yêu cầu dịch vụ đã được xác nhận.

Thông tin phân công gồm:

* Mã yêu cầu.
* Nhân viên thực hiện.
* Thời gian thực hiện.
* Ghi chú phân công.

### FR21 – Nhân viên xem công việc được phân công

Nhân viên có thể xem danh sách các yêu cầu được phân công cho mình.

Thông tin gồm:

* Mã yêu cầu.
* Dịch vụ.
* Khách hàng.
* Địa điểm.
* Thời gian thực hiện.
* Trạng thái.

### FR22 – Nhân viên xem chi tiết công việc

Nhân viên có thể xem thông tin chi tiết của công việc được giao để chuẩn bị thực hiện dịch vụ.

### FR23 – Cập nhật trạng thái công việc

Nhân viên có thể cập nhật trạng thái trong quá trình thực hiện theo quyền được cấp.

Các trạng thái chính gồm:

* Đã phân công.
* Đang thực hiện.
* Hoàn thành.

### FR24 – Cập nhật kết quả thực hiện

Sau khi hoàn thành dịch vụ, nhân viên có thể cập nhật thông tin kết quả thực hiện và ghi chú nếu cần.

Quản trị viên có thể xem thông tin này để kiểm tra và hoàn tất yêu cầu.

---

## 3.7. Quản lý trạng thái yêu cầu

### FR25 – Quản lý trạng thái yêu cầu

Hệ thống quản lý vòng đời của một yêu cầu dịch vụ thông qua các trạng thái:

1. Chờ tiếp nhận
2. Đã tiếp nhận
3. Đã báo giá
4. Chờ xác nhận
5. Đã xác nhận
6. Đã phân công
7. Đang thực hiện
8. Hoàn thành
9. Từ chối
10. Đã hủy

Việc chuyển trạng thái phải tuân theo quy trình nghiệp vụ đã được định nghĩa.

### FR26 – Hủy yêu cầu

Khách hàng có thể hủy yêu cầu trong những trạng thái được hệ thống cho phép.

Hệ thống phải kiểm tra trạng thái hiện tại trước khi cho phép hủy.

---

## 3.8. Quản lý dữ liệu bởi quản trị viên

### FR27 – Quản lý khách hàng

Quản trị viên có thể:

* Xem danh sách khách hàng.
* Tìm kiếm khách hàng.
* Xem thông tin khách hàng.
* Cập nhật thông tin khách hàng.
* Khóa/mở khóa tài khoản khi cần thiết.

### FR28 – Quản lý nhân viên

Quản trị viên có thể:

* Thêm nhân viên.
* Xem danh sách nhân viên.
* Tìm kiếm nhân viên.
* Cập nhật thông tin nhân viên.
* Khóa/mở khóa tài khoản nhân viên.

### FR29 – Quản lý nhóm dịch vụ

Quản trị viên có thể quản lý các nhóm dịch vụ:

* Vệ sinh.
* Vận chuyển.

Chức năng gồm:

* Thêm.
* Sửa.
* Xóa hoặc ngừng sử dụng.
* Xem danh sách.

### FR30 – Quản lý dịch vụ

Quản trị viên có thể:

* Thêm dịch vụ.
* Chỉnh sửa dịch vụ.
* Xem chi tiết dịch vụ.
* Tìm kiếm dịch vụ.
* Lọc dịch vụ theo nhóm.
* Kích hoạt/ngừng cung cấp dịch vụ.

---

## 3.9. Quản lý yêu cầu dịch vụ

### FR31 – Xem danh sách yêu cầu

Quản trị viên có thể xem toàn bộ yêu cầu dịch vụ trong hệ thống.

Danh sách hỗ trợ:

* Tìm kiếm.
* Lọc theo trạng thái.
* Lọc theo nhóm dịch vụ.
* Lọc theo thời gian.
* Phân trang khi số lượng dữ liệu lớn.

### FR32 – Xử lý yêu cầu

Quản trị viên có thể:

* Tiếp nhận yêu cầu.
* Từ chối yêu cầu.
* Nhập báo giá.
* Xác nhận thông tin.
* Phân công nhân viên.
* Cập nhật trạng thái.
* Theo dõi kết quả thực hiện.

### FR33 – Theo dõi lịch sử yêu cầu

Hệ thống lưu lại lịch sử thay đổi của yêu cầu, bao gồm các thông tin phù hợp như:

* Trạng thái trước.
* Trạng thái sau.
* Người thực hiện thay đổi.
* Thời gian thay đổi.
* Ghi chú.

---

## 3.10. Dashboard và thống kê

### FR34 – Dashboard quản trị

Quản trị viên có thể xem dashboard tổng quan về hoạt động của hệ thống.

Các chỉ số cơ bản gồm:

* Tổng số khách hàng.
* Tổng số nhân viên.
* Tổng số dịch vụ.
* Tổng số yêu cầu.
* Số yêu cầu đang xử lý.
* Số yêu cầu hoàn thành.
* Số yêu cầu bị từ chối/hủy.

### FR35 – Thống kê số lượng yêu cầu

Hệ thống cung cấp thống kê số lượng yêu cầu theo:

* Khoảng thời gian.
* Nhóm dịch vụ.
* Trạng thái.

### FR36 – Thống kê doanh thu

Hệ thống cung cấp thống kê doanh thu dựa trên các yêu cầu đã hoàn thành và có báo giá hợp lệ.

Có thể lọc theo khoảng thời gian để hỗ trợ quản trị viên theo dõi hoạt động kinh doanh.

---

## 3.11. Bảng tổng hợp yêu cầu chức năng

| Mã   | Chức năng                     | Đối tượng sử dụng      |
| ---- | ----------------------------- | ---------------------- |
| FR01 | Đăng ký                       | Khách hàng             |
| FR02 | Đăng nhập                     | Tất cả                 |
| FR03 | Đăng xuất                     | Tất cả                 |
| FR04 | Quản lý thông tin cá nhân     | Khách hàng             |
| FR05 | Phân quyền                    | Tất cả                 |
| FR06 | Xem danh sách dịch vụ         | Khách hàng             |
| FR07 | Xem chi tiết dịch vụ          | Khách hàng             |
| FR08 | Tìm kiếm dịch vụ              | Khách hàng             |
| FR09 | Lọc dịch vụ                   | Khách hàng             |
| FR10 | Tạo yêu cầu dịch vụ           | Khách hàng             |
| FR11 | Kiểm tra dữ liệu đặt dịch vụ  | Khách hàng/Hệ thống    |
| FR12 | Sinh mã yêu cầu               | Hệ thống               |
| FR13 | Xem danh sách yêu cầu         | Khách hàng             |
| FR14 | Xem chi tiết yêu cầu          | Khách hàng             |
| FR15 | Tiếp nhận yêu cầu             | Quản trị viên          |
| FR16 | Nhập báo giá                  | Quản trị viên          |
| FR17 | Xem báo giá                   | Khách hàng             |
| FR18 | Xác nhận báo giá              | Khách hàng             |
| FR19 | Từ chối báo giá               | Khách hàng             |
| FR20 | Phân công nhân viên           | Quản trị viên          |
| FR21 | Xem công việc được giao       | Nhân viên              |
| FR22 | Xem chi tiết công việc        | Nhân viên              |
| FR23 | Cập nhật trạng thái công việc | Nhân viên              |
| FR24 | Cập nhật kết quả thực hiện    | Nhân viên              |
| FR25 | Quản lý trạng thái yêu cầu    | Hệ thống/Quản trị viên |
| FR26 | Hủy yêu cầu                   | Khách hàng             |
| FR27 | Quản lý khách hàng            | Quản trị viên          |
| FR28 | Quản lý nhân viên             | Quản trị viên          |
| FR29 | Quản lý nhóm dịch vụ          | Quản trị viên          |
| FR30 | Quản lý dịch vụ               | Quản trị viên          |
| FR31 | Tìm kiếm/lọc yêu cầu          | Quản trị viên          |
| FR32 | Xử lý yêu cầu                 | Quản trị viên          |
| FR33 | Theo dõi lịch sử yêu cầu      | Quản trị viên          |
| FR34 | Dashboard                     | Quản trị viên          |
| FR35 | Thống kê yêu cầu              | Quản trị viên          |
| FR36 | Thống kê doanh thu            | Quản trị viên          |

---

## 3.12. Nguyên tắc xử lý chức năng

Các chức năng của hệ thống phải tuân thủ những nguyên tắc sau:

* Người dùng phải đăng nhập trước khi thực hiện các chức năng yêu cầu xác thực.
* Người dùng chỉ được truy cập chức năng phù hợp với vai trò.
* Dữ liệu đầu vào phải được kiểm tra trước khi lưu vào cơ sở dữ liệu.
* Các thao tác không hợp lệ phải trả về thông báo rõ ràng.
* Không cho phép thực hiện các bước nghiệp vụ trái với trạng thái hiện tại của yêu cầu.
* Các thay đổi quan trọng đối với yêu cầu dịch vụ cần được lưu lại để phục vụ việc theo dõi lịch sử.
* Các chức năng quản trị phải được bảo vệ bằng cơ chế phân quyền.
