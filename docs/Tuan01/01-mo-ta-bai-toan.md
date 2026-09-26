# 1. Mô tả bài toán

## 1.1. Giới thiệu đề tài

**Tên đề tài:** Phân tích, thiết kế, xây dựng và triển khai hệ thống Web đặt lịch và quản lý dịch vụ vệ sinh, vận chuyển theo yêu cầu.

Đề tài được thực hiện trong khuôn khổ học phần **Thực tập công nghiệp**, nhằm xây dựng một hệ thống Web hỗ trợ việc cung cấp và quản lý các dịch vụ vệ sinh, vận chuyển theo yêu cầu.

Hệ thống cho phép khách hàng tìm hiểu các dịch vụ, gửi yêu cầu sử dụng dịch vụ trực tuyến và theo dõi quá trình xử lý. Đồng thời, hệ thống hỗ trợ nhân viên và quản lý trong việc tiếp nhận yêu cầu, báo giá, phân công nhân viên, cập nhật trạng thái và quản lý lịch sử thực hiện dịch vụ.

## 1.2. Bối cảnh và vấn đề

Trong thực tế, các dịch vụ vệ sinh và vận chuyển theo yêu cầu thường tiếp nhận khách hàng thông qua điện thoại, tin nhắn hoặc các nền tảng mạng xã hội. Phương thức này có thể gây khó khăn trong việc quản lý thông tin khách hàng, thời gian thực hiện, địa điểm, nhân viên được phân công và trạng thái của từng yêu cầu.

Đối với khách hàng, việc đăng ký dịch vụ theo phương thức thủ công có thể mất nhiều thời gian để trao đổi thông tin về loại dịch vụ, thời gian, địa điểm và mức giá.

Đối với đơn vị cung cấp dịch vụ, việc quản lý bằng các phương thức thủ công có thể dẫn đến khó khăn trong việc theo dõi số lượng yêu cầu, phân công nhân viên, kiểm soát lịch thực hiện và tổng hợp doanh thu.

Vì vậy, cần xây dựng một hệ thống Web tập trung nhằm hỗ trợ số hóa quy trình tiếp nhận và quản lý dịch vụ.

## 1.3. Giải pháp đề xuất

Hệ thống Web được đề xuất nhằm quản lý tập trung các thông tin liên quan đến khách hàng, nhân viên, dịch vụ và yêu cầu sử dụng dịch vụ.

Khách hàng có thể đăng ký tài khoản, đăng nhập, xem và tìm kiếm dịch vụ, gửi yêu cầu với thời gian và địa điểm mong muốn, theo dõi trạng thái xử lý và xem lịch sử sử dụng dịch vụ.

Quản lý có thể tiếp nhận yêu cầu, kiểm tra thông tin, nhập báo giá, xác nhận hoặc từ chối yêu cầu và phân công nhân viên thực hiện.

Nhân viên có thể xem các công việc được phân công, xem thông tin cần thiết và cập nhật trạng thái thực hiện dịch vụ.

Hệ thống cũng cung cấp dashboard và các thống kê cơ bản về số lượng đơn dịch vụ và doanh thu nhằm hỗ trợ quản lý theo dõi hoạt động của đơn vị.

## 1.4. Các nhóm dịch vụ

Hệ thống tập trung vào hai nhóm dịch vụ chính:

### 1.4.1. Dịch vụ vệ sinh

Bao gồm các dịch vụ vệ sinh theo nhu cầu của khách hàng, chẳng hạn:

* Vệ sinh nhà ở.
* Vệ sinh phòng trọ.
* Vệ sinh văn phòng.
* Vệ sinh theo giờ.
* Vệ sinh sau xây dựng.

Danh sách dịch vụ cụ thể có thể được quản lý và điều chỉnh bởi quản trị viên.

### 1.4.2. Dịch vụ vận chuyển

Bao gồm các dịch vụ vận chuyển theo yêu cầu, chẳng hạn:

* Chuyển nhà.
* Chuyển phòng trọ.
* Chuyển văn phòng.
* Vận chuyển hàng hóa.

Danh sách dịch vụ cụ thể có thể được quản lý và điều chỉnh bởi quản trị viên.

## 1.5. Đối tượng sử dụng

Hệ thống gồm ba nhóm người dùng chính:

### Khách hàng

Khách hàng là người có nhu cầu sử dụng dịch vụ. Khách hàng có thể xem thông tin dịch vụ, gửi yêu cầu, xem báo giá, theo dõi trạng thái và xem lịch sử sử dụng dịch vụ.

### Nhân viên

Nhân viên là người trực tiếp thực hiện dịch vụ. Nhân viên có thể xem các yêu cầu được phân công, xem thông tin công việc và cập nhật trạng thái thực hiện.

### Quản lý/Quản trị viên

Quản lý/Quản trị viên chịu trách nhiệm quản lý hoạt động của hệ thống, bao gồm quản lý tài khoản, dịch vụ, nhân viên, yêu cầu dịch vụ, báo giá, phân công và thống kê.

## 1.6. Quy trình nghiệp vụ tổng quát

Quy trình nghiệp vụ chính của hệ thống được thực hiện theo các bước:

```text
Khách hàng
    |
    | Gửi yêu cầu dịch vụ
    v
Hệ thống
    |
    v
Quản lý tiếp nhận yêu cầu
    |
    v
Kiểm tra thông tin và báo giá
    |
    v
Khách hàng xác nhận báo giá
    |
    v
Quản lý phân công nhân viên
    |
    v
Nhân viên tiếp nhận công việc
    |
    v
Nhân viên thực hiện dịch vụ
    |
    v
Cập nhật trạng thái
    |
    v
Hoàn thành dịch vụ
    |
    v
Lưu lịch sử dịch vụ
```

Trong trường hợp yêu cầu không hợp lệ hoặc không thể đáp ứng, quản lý có thể từ chối yêu cầu. Khách hàng cũng có thể hủy yêu cầu trong trường hợp đáp ứng các điều kiện hủy theo quy định của hệ thống.

## 1.7. Phương thức báo giá

Trong phạm vi đề tài, hệ thống không xây dựng thuật toán tự động tính giá phức tạp.

Mức giá của từng yêu cầu dịch vụ được quản lý hoặc nhân viên xác định dựa trên thông tin do khách hàng cung cấp và nhập vào hệ thống.

Khách hàng có thể xem mức báo giá và xác nhận hoặc từ chối sử dụng dịch vụ theo quy trình nghiệp vụ được thiết kế.

Cách tiếp cận này giúp giảm độ phức tạp của hệ thống và phù hợp với phạm vi triển khai trong thời gian 08 tuần.

## 1.8. Mục tiêu của hệ thống

Hệ thống được xây dựng nhằm đạt các mục tiêu chính:

* Số hóa quy trình tiếp nhận và quản lý yêu cầu dịch vụ.
* Hỗ trợ khách hàng gửi yêu cầu sử dụng dịch vụ trực tuyến.
* Hỗ trợ quản lý tập trung thông tin khách hàng, nhân viên và dịch vụ.
* Hỗ trợ quản lý tiếp nhận, báo giá và phân công nhân viên.
* Hỗ trợ nhân viên theo dõi và cập nhật công việc được phân công.
* Theo dõi trạng thái của các yêu cầu dịch vụ trong suốt quá trình xử lý.
* Lưu trữ lịch sử sử dụng dịch vụ.
* Cung cấp dashboard và thống kê cơ bản phục vụ quản lý.
* Xây dựng hệ thống Web có giao diện responsive và có khả năng triển khai trên Internet.

## 1.9. Phạm vi định hướng

Trong giai đoạn đầu, hệ thống tập trung vào các chức năng cốt lõi gồm quản lý tài khoản, quản lý dịch vụ, đặt dịch vụ, tiếp nhận yêu cầu, báo giá, xác nhận, phân công nhân viên, cập nhật trạng thái, quản lý lịch sử và thống kê cơ bản.

Các chức năng nâng cao như thanh toán trực tuyến, định vị GPS, tối ưu tuyến đường và tự động tính giá vận chuyển không thuộc phạm vi bắt buộc của phiên bản cơ bản và chỉ được xem xét bổ sung khi các chức năng cốt lõi đã hoàn thiện.
