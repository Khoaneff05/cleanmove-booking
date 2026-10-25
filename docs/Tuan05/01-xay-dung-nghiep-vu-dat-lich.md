# 01. XÂY DỰNG NGHIỆP VỤ ĐẶT LỊCH

## 1. Mục tiêu

Trong tuần 5 của kỳ thực tập chuyên ngành, tiến hành xây dựng và hoàn thiện nghiệp vụ đặt lịch dịch vụ cho hệ thống web CleanMove. Nghiệp vụ này cho phép khách hàng lựa chọn dịch vụ vệ sinh, nhập thông tin cần thiết, lựa chọn thời gian thực hiện và gửi yêu cầu đặt lịch thông qua giao diện web.

Bên cạnh đó, hệ thống cần bảo đảm dữ liệu đầu vào hợp lệ, lưu trữ thông tin đặt lịch chính xác, quản lý trạng thái xử lý và hỗ trợ kiểm tra lịch làm việc của nhân viên nhằm hạn chế tình trạng phân công công việc trùng thời gian.

## 2. Phạm vi thực hiện

Nội dung xây dựng nghiệp vụ đặt lịch tập trung vào các chức năng sau:

- Lựa chọn dịch vụ vệ sinh từ danh sách dịch vụ hiện có.
- Nhập thông tin liên quan đến địa điểm và thời gian thực hiện dịch vụ.
- Kiểm tra tính hợp lệ của thông tin đặt lịch trước khi lưu.
- Tạo yêu cầu đặt lịch thông qua Backend API.
- Lưu thông tin đặt lịch vào cơ sở dữ liệu.
- Theo dõi trạng thái xử lý của yêu cầu đặt lịch.
- Hỗ trợ quản lý và phân công nhân viên theo lịch làm việc.
- Xử lý các trường hợp đặt lịch không hợp lệ hoặc phát sinh lỗi trong quá trình thực hiện.

## 3. Phân tích nghiệp vụ đặt lịch

### 3.1. Đối tượng tham gia

| Đối tượng | Vai trò |
|---|---|
| Khách hàng | Lựa chọn dịch vụ, nhập thông tin và gửi yêu cầu đặt lịch. |
| Hệ thống | Kiểm tra dữ liệu, tiếp nhận yêu cầu và lưu thông tin đặt lịch. |
| Quản trị viên | Quản lý các yêu cầu đặt lịch và hỗ trợ điều phối công việc. |
| Nhân viên | Tiếp nhận và thực hiện công việc theo phân công. |

### 3.2. Thông tin đầu vào

Một yêu cầu đặt lịch cần có các thông tin phù hợp với cấu trúc dữ liệu của hệ thống, bao gồm:

- Người đặt lịch.
- Dịch vụ được lựa chọn.
- Địa chỉ thực hiện dịch vụ.
- Ngày và giờ dự kiến.
- Thời lượng thực hiện dự kiến.
- Ghi chú hoặc yêu cầu bổ sung nếu có.

Thông tin người đặt lịch cần được xác định từ tài khoản đã đăng nhập thay vì tin tưởng trực tiếp mã người dùng do trình duyệt gửi lên. Thời lượng dịch vụ cần được xác định từ dữ liệu dịch vụ phía máy chủ, không cho phép khách hàng tự ý thay đổi để bỏ qua kiểm tra lịch.

## 4. Quy trình xử lý đặt lịch

### Bước 1. Lựa chọn dịch vụ

Khách hàng truy cập giao diện đặt lịch và xem danh sách dịch vụ hiện có. Sau khi lựa chọn dịch vụ phù hợp, hệ thống hiển thị thông tin cần thiết để khách hàng tiếp tục nhập thông tin đặt lịch.

### Bước 2. Nhập thông tin đặt lịch

Khách hàng cung cấp địa chỉ, thời gian dự kiến thực hiện và các thông tin bổ sung theo yêu cầu của biểu mẫu.

Giao diện cần kiểm tra những trường bắt buộc trước khi gửi dữ liệu đến máy chủ. Các trường hợp bỏ trống thông tin quan trọng hoặc nhập sai định dạng phải được thông báo rõ ràng.

### Bước 3. Kiểm tra dữ liệu tại Backend

Khi nhận yêu cầu, Backend thực hiện các bước kiểm tra:

1. Xác thực người dùng và quyền thực hiện thao tác.
2. Kiểm tra dịch vụ có tồn tại và được phép đặt hay không.
3. Kiểm tra địa chỉ, thời gian và các trường bắt buộc.
4. Xác định thời lượng thực hiện dựa trên dữ liệu dịch vụ.
5. Kiểm tra các điều kiện nghiệp vụ liên quan đến thời gian và lịch làm việc.
6. Trả về lỗi phù hợp nếu dữ liệu không hợp lệ.

### Bước 4. Tạo yêu cầu đặt lịch

Sau khi dữ liệu hợp lệ, hệ thống lưu thông tin đặt lịch vào cơ sở dữ liệu. Trạng thái ban đầu phải tuân theo quy trình nghiệp vụ và các giá trị trạng thái được định nghĩa trong hệ thống.

Nếu hệ thống cần ghi nhận lịch sử trạng thái, thao tác tạo yêu cầu và ghi nhận lịch sử liên quan cần được thực hiện nhất quán trong cùng một giao dịch cơ sở dữ liệu khi phù hợp.

Sau khi lưu thành công, Backend trả về thông tin yêu cầu để giao diện thông báo kết quả cho khách hàng.

### Bước 5. Quản lý và phân công lịch

Quản trị viên theo dõi các yêu cầu đặt lịch và thực hiện điều phối nhân viên theo quy trình được hỗ trợ.

Trước khi phân công, hệ thống cần kiểm tra thời gian làm việc, thời lượng dịch vụ và các công việc đang được phân công cho nhân viên. Việc kiểm tra phải tính đến các dịch vụ khác nhau mà cùng một nhân viên có thể được giao thực hiện.

Để tránh hai yêu cầu đồng thời cùng chiếm một khung giờ, việc kiểm tra xung đột lịch và lưu phân công cần được bảo vệ bằng giao dịch và cơ chế khóa phù hợp. Chỉ kiểm tra lịch ở giao diện là chưa đủ.

### Bước 6. Theo dõi và cập nhật trạng thái

Khách hàng theo dõi tình trạng yêu cầu đặt lịch. Quản trị viên và nhân viên cập nhật trạng thái theo quyền được cấp và theo quy trình nghiệp vụ.

Các trạng thái phải được chuyển đổi theo những điều kiện hợp lệ. Hệ thống không được cho phép người dùng thông thường tự ý chuyển trạng thái sang hoàn thành hoặc sửa thông tin phân công trái phép.

## 5. Quy tắc nghiệp vụ

| Mã | Quy tắc |
|---|---|
| BR-01 | Người dùng phải được xác thực trước khi thực hiện thao tác đặt lịch yêu cầu đăng nhập. |
| BR-02 | Dịch vụ được chọn phải tồn tại và đáp ứng điều kiện đặt dịch vụ. |
| BR-03 | Thông tin bắt buộc phải được kiểm tra trước khi tạo yêu cầu. |
| BR-04 | Thời gian đặt lịch phải đáp ứng các điều kiện hợp lệ của hệ thống. |
| BR-05 | Thời lượng thực hiện phải được xác định từ dữ liệu đáng tin cậy phía máy chủ. |
| BR-06 | Việc phân công phải kiểm tra xung đột lịch của nhân viên. |
| BR-07 | Các thao tác thay đổi trạng thái phải tuân thủ phân quyền và quy trình nghiệp vụ. |
| BR-08 | Những thay đổi dữ liệu liên quan cần được thực hiện nhất quán để tránh trạng thái không đồng bộ. |
| BR-09 | Thông báo lỗi cần đủ rõ ràng để người dùng biết nguyên nhân và cách xử lý. |
| BR-10 | Việc mở rộng nghiệp vụ phải bảo toàn dữ liệu và không làm ảnh hưởng chức năng hiện có. |

## 6. Xử lý các tình huống ngoại lệ

| Tình huống | Cách xử lý mong muốn |
|---|---|
| Chưa đăng nhập | Yêu cầu người dùng đăng nhập trước khi đặt lịch. |
| Không chọn dịch vụ | Thông báo yêu cầu lựa chọn dịch vụ hợp lệ. |
| Dịch vụ không tồn tại hoặc không còn khả dụng | Từ chối yêu cầu và trả về thông báo phù hợp. |
| Thiếu địa chỉ hoặc thông tin bắt buộc | Yêu cầu bổ sung dữ liệu. |
| Ngày giờ không hợp lệ | Từ chối yêu cầu và hướng dẫn chọn thời gian khác. |
| Không tìm được nhân viên phù hợp | Thông báo hoặc giữ yêu cầu ở trạng thái phù hợp với quy trình hiện hành. |
| Nhân viên bị trùng lịch | Từ chối phân công hoặc yêu cầu chọn nhân viên, thời gian khác. |
| Người dùng không đủ quyền | Từ chối thao tác và trả về lỗi xác thực hoặc phân quyền phù hợp. |
| Lỗi cơ sở dữ liệu | Trả về thông báo lỗi an toàn, không để lại dữ liệu dở dang. |
| Gửi yêu cầu nhiều lần | Hạn chế tạo bản ghi trùng ngoài ý muốn bằng cơ chế phù hợp với thiết kế hệ thống. |

## 7. Yêu cầu kỹ thuật

### 7.1. Backend

Backend chịu trách nhiệm xác thực, phân quyền, kiểm tra dữ liệu, thực hiện quy tắc nghiệp vụ và lưu trữ thông tin đặt lịch.

Các API cần tuân thủ hợp đồng dữ liệu thống nhất với Frontend. Các thao tác ghi dữ liệu quan trọng cần sử dụng giao dịch phù hợp và xử lý lỗi theo quy ước của hệ thống.

### 7.2. Frontend

Frontend cung cấp biểu mẫu đặt lịch dễ sử dụng, hỗ trợ kiểm tra dữ liệu cơ bản, hiển thị trạng thái xử lý và thông báo lỗi từ Backend.

Giao diện cần hạn chế gửi yêu cầu lặp do người dùng nhấn nút nhiều lần, đồng thời không tự giả định thao tác đã thành công khi chưa nhận được phản hồi hợp lệ.

### 7.3. Cơ sở dữ liệu

Nghiệp vụ đặt lịch sử dụng cấu trúc cơ sở dữ liệu hiện có. Các bảng liên quan có thể bao gồm `users`, `services`, `bookings`, `booking_assignments`, `booking_status_history` và `staff_schedule_locks`.

Mọi thay đổi cấu trúc cơ sở dữ liệu phải được đánh giá riêng, có phương án bảo vệ dữ liệu và được phê duyệt trước khi triển khai. Không tự ý xóa dữ liệu hoặc tạo lại cơ sở dữ liệu để xử lý lỗi nghiệp vụ.

## 8. Kế hoạch kiểm thử

Các trường hợp kiểm thử trọng tâm gồm:

| Mã | Trường hợp kiểm thử | Kết quả mong đợi |
|---|---|---|
| TC-01 | Đặt lịch với dữ liệu hợp lệ | Tạo yêu cầu thành công. |
| TC-02 | Đặt lịch khi chưa đăng nhập | Yêu cầu đăng nhập hoặc từ chối theo chính sách xác thực. |
| TC-03 | Thiếu trường thông tin bắt buộc | Từ chối và thông báo lỗi. |
| TC-04 | Gửi mã dịch vụ không tồn tại | Từ chối yêu cầu. |
| TC-05 | Nhập ngày giờ không hợp lệ | Từ chối yêu cầu. |
| TC-06 | Phân công nhân viên đang có lịch trùng | Không tạo phân công xung đột. |
| TC-07 | Hai yêu cầu đồng thời cùng chiếm một khung giờ | Cơ chế đồng bộ phải ngăn phân công xung đột. |
| TC-08 | Người dùng không có quyền cập nhật trạng thái | Từ chối thao tác. |
| TC-09 | Xảy ra lỗi trong quá trình lưu dữ liệu | Không để lại dữ liệu dở dang ngoài dự kiến. |
| TC-10 | Đặt lịch sau khi có thay đổi giao diện | Frontend và Backend vẫn trao đổi dữ liệu đúng hợp đồng. |

## 9. Kết quả cần đạt

Sau khi hoàn thành nội dung này, hệ thống cần đáp ứng các mục tiêu:

- Có quy trình đặt lịch được mô tả rõ ràng.
- Xác định được trách nhiệm xử lý giữa khách hàng, Backend, quản trị viên và nhân viên.
- Có các quy tắc kiểm tra dữ liệu và điều kiện đặt lịch.
- Có phương án kiểm tra xung đột lịch trong quá trình phân công.
- Có danh sách tình huống ngoại lệ và kế hoạch kiểm thử.