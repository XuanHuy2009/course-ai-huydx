# SOFTWARE REQUIREMENTS SPECIFICATION (SRS)
123
## Module Login - Perfex CRM | Anh Tester Demo

| Thuộc tính | Giá trị |
|---|---|
| Tài liệu | Đặc tả yêu cầu phần mềm cho module Login |
| Hệ thống | Perfex CRM \| Anh Tester Demo |
| URL khảo sát | `https://crm.anhtester.com/admin/authentication` |
| Phiên bản tài liệu | 1.0 |
| Ngày khảo sát | 26/11/2026 |
| Trạng thái | Bản cơ sở từ khảo sát hệ thống đang chạy |

## 1. Mục đích

Tài liệu mô tả yêu cầu chức năng, giao diện, dữ liệu, bảo mật và tiêu chí nghiệm thu của module đăng nhập khu vực quản trị. Tài liệu được xây dựng bằng phương pháp black-box dựa trên hành vi quan sát trực tiếp trên môi trường demo.

Các yêu cầu được phân loại như sau:

- **Đã quan sát:** hành vi đã được xác nhận trên hệ thống tại ngày khảo sát.
- **Yêu cầu chuẩn hóa:** yêu cầu cần có để đặc tả đầy đủ sản phẩm; cần Product Owner xác nhận nếu chưa thể kiểm chứng bằng black-box.
- **Khuyến nghị:** yêu cầu bảo mật hoặc vận hành nên áp dụng nhưng chưa được xác nhận trên giao diện.

## 2. Phạm vi

### 2.1. Trong phạm vi

- Hiển thị màn hình đăng nhập quản trị.
- Nhập email và mật khẩu.
- Kiểm tra dữ liệu bắt buộc và định dạng email.
- Xác thực thông tin đăng nhập.
- Ghi nhớ phiên đăng nhập theo lựa chọn **Remember me**.
- Điều hướng sau khi đăng nhập thành công.
- Xử lý đăng nhập thất bại.
- Truy cập và kiểm tra đầu vào của màn hình **Forgot Password**.
- Kiểm soát truy cập màn hình đăng nhập khi người dùng đã có phiên hợp lệ.

### 2.2. Ngoài phạm vi

- Đăng ký tài khoản mới.
- Quản trị người dùng, vai trò và phân quyền sau đăng nhập.
- Quy trình đặt lại mật khẩu sau khi người dùng nhận email.
- Đổi mật khẩu khi đang đăng nhập.
- Xác thực đa yếu tố, SSO hoặc đăng nhập mạng xã hội.

## 3. Tác nhân và hệ thống liên quan

| Mã | Tác nhân/hệ thống | Mô tả |
|---|---|---|
| ACT-01 | Người dùng quản trị | Người có tài khoản hợp lệ, truy cập khu vực `/admin`. |
| ACT-02 | Người dùng chưa xác thực | Người chưa có phiên đăng nhập hợp lệ. |
| SYS-01 | Dịch vụ xác thực | Kiểm tra email, mật khẩu, trạng thái tài khoản và tạo phiên. |
| SYS-02 | Dịch vụ email | Gửi hướng dẫn đặt lại mật khẩu; chưa kiểm chứng trong đợt khảo sát. |
| SYS-03 | Khu vực quản trị | Trang đích sau khi xác thực thành công. |

## 4. Giả định và phụ thuộc

- Người dùng có kết nối mạng và trình duyệt hỗ trợ HTML5, cookie và HTTPS.
- Tài khoản đăng nhập đã được tạo và đang hoạt động.
- Dịch vụ xác thực và cơ sở dữ liệu người dùng sẵn sàng.
- Tính năng **Remember me** phụ thuộc vào cookie hoặc token lưu trên trình duyệt.
- Luồng quên mật khẩu phụ thuộc vào cấu hình gửi email của hệ thống.

## 5. Tổng quan giao diện

### 5.1. Màn hình Login

| Thành phần | Loại | Bắt buộc | Trạng thái ban đầu | Mô tả |
|---|---|---:|---|---|
| Logo/tên hệ thống | Liên kết | Không | Hiển thị | Liên kết về trang gốc của hệ thống. |
| Tiêu đề `Login` | Tiêu đề | - | Hiển thị | Xác định chức năng của màn hình. |
| `Email Address` | Trường email | Có | Rỗng, được focus | Nhập địa chỉ email đăng nhập. |
| `Password` | Trường mật khẩu | Có | Rỗng, ký tự được che | Nhập mật khẩu. |
| `Remember me` | Checkbox | Không | Không chọn | Yêu cầu duy trì phiên đăng nhập. |
| `Login` | Nút | - | Cho phép bấm | Gửi yêu cầu đăng nhập. |
| `Forgot Password?` | Liên kết | - | Hiển thị | Mở màn hình khôi phục mật khẩu. |

### 5.2. Màn hình Forgot Password

| Thành phần | Loại | Bắt buộc | Mô tả |
|---|---|---:|---|
| Tiêu đề `Forgot Password` | Tiêu đề | - | Xác định màn hình khôi phục mật khẩu. |
| `Email Address` | Trường email | Có theo nghiệp vụ | Nhập email của tài khoản cần khôi phục. |
| `Confirm` | Nút | - | Gửi yêu cầu khôi phục mật khẩu. |

## 6. Quy tắc nghiệp vụ

| Mã | Quy tắc |
|---|---|
| BR-01 | Email và mật khẩu là dữ liệu bắt buộc khi đăng nhập. |
| BR-02 | Email phải tuân thủ định dạng email được trình duyệt chấp nhận. |
| BR-03 | Chỉ cặp email/mật khẩu hợp lệ mới được tạo phiên đăng nhập. |
| BR-04 | Hệ thống không tiết lộ email hay mật khẩu sai; thông báo chung là `Invalid email or password`. |
| BR-05 | Sau khi đăng nhập thành công, người dùng được chuyển đến khu vực quản trị `/admin/`. |
| BR-06 | Nếu đã có phiên hợp lệ, truy cập URL đăng nhập phải chuyển người dùng về khu vực quản trị. |
| BR-07 | Mật khẩu phải được hiển thị dưới dạng che ký tự. |
| BR-08 | Khi chọn **Remember me**, thời hạn phiên phải dài hơn phiên thông thường theo chính sách được cấu hình. |
| BR-09 | Chức năng quên mật khẩu chỉ xử lý email gắn với tài khoản hợp lệ và đủ điều kiện khôi phục. |
| BR-10 | Thông tin xác thực không được ghi vào URL, log phía trình duyệt hoặc nội dung thông báo lỗi. |

## 7. Yêu cầu chức năng

### 7.1. Hiển thị màn hình đăng nhập

**FR-LOGIN-01 - Tải màn hình Login**  
Hệ thống phải hiển thị màn hình đăng nhập tại `/admin/authentication` cho người dùng chưa có phiên hợp lệ.

**Tiêu chí nghiệm thu**

1. Trang tải qua HTTPS.
2. Tiêu đề trang là `Perfex CRM | Anh Tester Demo - Login`.
3. Các thành phần tại mục 5.1 được hiển thị.
4. Trường Email Address được focus khi màn hình sẵn sàng.

### 7.2. Nhập thông tin xác thực

**FR-LOGIN-02 - Nhập email**  
Hệ thống phải cho phép người dùng nhập địa chỉ email vào trường `Email Address`.

**FR-LOGIN-03 - Nhập mật khẩu**  
Hệ thống phải cho phép người dùng nhập mật khẩu và che nội dung đã nhập.

**FR-LOGIN-04 - Chọn Remember me**  
Hệ thống phải cho phép người dùng bật hoặc tắt tùy chọn `Remember me`; mặc định tùy chọn không được chọn.

### 7.3. Kiểm tra dữ liệu đầu vào

**FR-LOGIN-05 - Kiểm tra trường bắt buộc**  
Khi người dùng bấm `Login` mà chưa nhập dữ liệu, hệ thống phải giữ nguyên màn hình và hiển thị:

- `The Password field is required.`
- `The Email Address field is required.`

**FR-LOGIN-06 - Kiểm tra định dạng email**  
Nếu giá trị email không đúng định dạng, trình duyệt/hệ thống phải ngăn gửi biểu mẫu và hiển thị thông báo kiểm tra định dạng phù hợp. Với giá trị thiếu ký tự `@`, hành vi quan sát được là thông báo dạng `Please include an '@' in the email address.`

**FR-LOGIN-07 - Bảo toàn an toàn dữ liệu khi lỗi**  
Sau lần đăng nhập thất bại, hệ thống phải xóa mật khẩu khỏi biểu mẫu. Việc giữ hay xóa email cần được Product Owner xác nhận; hệ thống khảo sát trả biểu mẫu về trạng thái rỗng.

### 7.4. Xác thực đăng nhập

**FR-LOGIN-08 - Gửi yêu cầu đăng nhập**  
Khi dữ liệu vượt qua kiểm tra phía giao diện, hệ thống phải gửi email và mật khẩu đến dịch vụ xác thực qua HTTPS.

**FR-LOGIN-09 - Đăng nhập thành công**  
Nếu thông tin xác thực hợp lệ và tài khoản được phép đăng nhập, hệ thống phải:

1. Tạo phiên xác thực.
2. Điều hướng đến `https://crm.anhtester.com/admin/`.
3. Hiển thị trang có tiêu đề `Bảng tin`.
4. Hiển thị danh tính người dùng đang đăng nhập tại khu vực đầu trang.

**FR-LOGIN-10 - Đăng nhập thất bại**  
Nếu email hoặc mật khẩu không hợp lệ, hệ thống phải:

1. Không tạo phiên xác thực.
2. Giữ người dùng tại `/admin/authentication`.
3. Hiển thị thông báo `Invalid email or password`.
4. Không cho biết email có tồn tại hay không.

**FR-LOGIN-11 - Gửi bằng bàn phím**  
Khi focus nằm trong biểu mẫu, nhấn `Enter` phải có hành vi tương đương bấm nút `Login`. Đây là yêu cầu chuẩn hóa, chưa được xác nhận trong đợt khảo sát.

### 7.5. Ghi nhớ đăng nhập

**FR-LOGIN-12 - Phiên thông thường**  
Khi `Remember me` không được chọn, phiên phải kết thúc theo thời hạn phiên thông thường hoặc khi người dùng đăng xuất.

**FR-LOGIN-13 - Phiên được ghi nhớ**  
Khi `Remember me` được chọn và đăng nhập thành công, hệ thống phải duy trì trạng thái đăng nhập qua lần đóng/mở trình duyệt trong thời hạn do chính sách hệ thống quy định.

**FR-LOGIN-14 - Thu hồi phiên**  
Đăng xuất, đổi mật khẩu, khóa tài khoản hoặc thu hồi phiên phải làm mất hiệu lực cả phiên thông thường và phiên được ghi nhớ tương ứng.

> FR-LOGIN-12 đến FR-LOGIN-14 là yêu cầu chuẩn hóa; thời hạn cookie/token chưa thể xác định bằng khảo sát giao diện.

### 7.6. Người dùng đã đăng nhập

**FR-LOGIN-15 - Ngăn hiển thị lại Login**  
Khi người dùng có phiên hợp lệ truy cập `/admin/authentication`, hệ thống phải chuyển hướng đến `/admin/` thay vì hiển thị lại biểu mẫu đăng nhập.

### 7.7. Quên mật khẩu

**FR-LOGIN-16 - Mở màn hình Forgot Password**  
Khi bấm `Forgot Password?`, hệ thống phải điều hướng đến `/admin/authentication/forgot_password` và hiển thị các thành phần tại mục 5.2.

**FR-LOGIN-17 - Kiểm tra định dạng email khôi phục**  
Hệ thống phải ngăn gửi yêu cầu nếu email không đúng định dạng.

**FR-LOGIN-18 - Email khôi phục không hợp lệ**  
Hành vi quan sát hiện tại hiển thị `Email not found` khi không tìm thấy email. Vì thông báo này có thể giúp dò tài khoản, yêu cầu mục tiêu nên dùng thông báo trung tính, ví dụ: `Nếu email tồn tại, hướng dẫn khôi phục sẽ được gửi.`

**FR-LOGIN-19 - Gửi yêu cầu khôi phục**  
Với email hợp lệ, hệ thống phải tạo mã khôi phục dùng một lần, có thời hạn và gửi hướng dẫn đến email tương ứng. Chức năng gửi email không được kích hoạt trong đợt khảo sát để tránh tạo tác động ngoài ý muốn.

## 8. Luồng nghiệp vụ

### UC-LOGIN-01 - Đăng nhập thành công

**Tiền điều kiện**

- Người dùng chưa đăng nhập.
- Tài khoản tồn tại, đang hoạt động và có quyền truy cập khu vực quản trị.

**Luồng chính**

1. Người dùng mở `/admin/authentication`.
2. Hệ thống hiển thị màn hình Login.
3. Người dùng nhập email hợp lệ.
4. Người dùng nhập mật khẩu hợp lệ.
5. Người dùng tùy chọn `Remember me`.
6. Người dùng bấm `Login`.
7. Hệ thống kiểm tra đầu vào.
8. Hệ thống xác thực tài khoản.
9. Hệ thống tạo phiên.
10. Hệ thống điều hướng đến `/admin/` và hiển thị `Bảng tin`.

**Hậu điều kiện**

- Phiên đăng nhập hợp lệ tồn tại.
- Người dùng có thể truy cập các chức năng theo quyền được cấp.

### UC-LOGIN-02 - Đăng nhập thất bại

1. Thực hiện bước 1-7 của UC-LOGIN-01.
2. Dịch vụ xác thực từ chối thông tin đăng nhập.
3. Hệ thống không tạo phiên.
4. Hệ thống hiển thị `Invalid email or password`.
5. Người dùng có thể nhập lại thông tin.

### UC-LOGIN-03 - Thiếu dữ liệu

1. Người dùng mở màn hình Login.
2. Người dùng để trống một hoặc cả hai trường bắt buộc.
3. Người dùng bấm `Login`.
4. Hệ thống không gửi yêu cầu xác thực.
5. Hệ thống hiển thị thông báo tương ứng với từng trường thiếu.

### UC-LOGIN-04 - Truy cập Forgot Password

1. Người dùng bấm `Forgot Password?`.
2. Hệ thống mở `/admin/authentication/forgot_password`.
3. Người dùng nhập email.
4. Hệ thống kiểm tra định dạng email.
5. Nếu email đủ điều kiện, hệ thống xử lý yêu cầu khôi phục theo FR-LOGIN-19.

## 9. Ma trận thông báo

| Mã | Điều kiện | Thông báo/hành vi quan sát | Vị trí |
|---|---|---|---|
| MSG-01 | Email trống khi Login | `The Email Address field is required.` | Phía trên biểu mẫu |
| MSG-02 | Password trống khi Login | `The Password field is required.` | Phía trên biểu mẫu |
| MSG-03 | Email thiếu `@` | Thông báo kiểm tra email chuẩn của trình duyệt | Gắn với trường Email |
| MSG-04 | Email hoặc mật khẩu sai | `Invalid email or password` | Phía trên biểu mẫu |
| MSG-05 | Email khôi phục không tìm thấy/để trống | `Email not found` | Phía trên biểu mẫu Forgot Password |

## 10. Yêu cầu phi chức năng

### 10.1. Bảo mật

| Mã | Yêu cầu | Mức độ |
|---|---|---|
| NFR-SEC-01 | Toàn bộ trang và request xác thực phải sử dụng HTTPS; không cho phép gửi thông tin xác thực qua HTTP. | Bắt buộc |
| NFR-SEC-02 | Mật khẩu phải được băm bằng thuật toán thích hợp có salt; không lưu hoặc ghi log mật khẩu dạng rõ. | Bắt buộc |
| NFR-SEC-03 | Cookie phiên phải có `Secure`, `HttpOnly` và `SameSite` phù hợp. | Bắt buộc |
| NFR-SEC-04 | Biểu mẫu đăng nhập và quên mật khẩu phải chống CSRF nếu kiến trúc xác thực sử dụng cookie. | Bắt buộc |
| NFR-SEC-05 | Hệ thống phải giới hạn tần suất đăng nhập và khôi phục mật khẩu theo tài khoản/IP/thiết bị, có cơ chế chống brute force. | Bắt buộc |
| NFR-SEC-06 | Thông báo lỗi đăng nhập không được phân biệt email tồn tại với mật khẩu sai. | Bắt buộc |
| NFR-SEC-07 | Thông báo quên mật khẩu nên trung tính để tránh dò email tồn tại. | Khuyến nghị cao |
| NFR-SEC-08 | Session ID phải được tái tạo sau khi đăng nhập để chống session fixation. | Bắt buộc |
| NFR-SEC-09 | Không lưu mật khẩu trong localStorage/sessionStorage hoặc giá trị tự động điền không an toàn. | Bắt buộc |
| NFR-SEC-10 | Mọi lần đăng nhập thành công, thất bại, khóa tài khoản và yêu cầu khôi phục phải được ghi nhật ký bảo mật mà không chứa mật khẩu. | Bắt buộc |

### 10.2. Hiệu năng và sẵn sàng

| Mã | Yêu cầu |
|---|---|
| NFR-PERF-01 | 95% request tải màn hình Login hoàn tất trong tối đa 2 giây trong điều kiện tải bình thường. |
| NFR-PERF-02 | 95% request xác thực trả kết quả trong tối đa 3 giây, không tính độ trễ mạng của người dùng. |
| NFR-AVL-01 | Module Login phải có mức sẵn sàng phù hợp với SLA chung của hệ thống. |
| NFR-AVL-02 | Khi dịch vụ xác thực gặp lỗi, hiển thị thông báo chung, không lộ stack trace, truy vấn hoặc thông tin hạ tầng. |

### 10.3. Khả dụng và tương thích

| Mã | Yêu cầu |
|---|---|
| NFR-USA-01 | Giao diện phải sử dụng được bằng bàn phím; thứ tự focus hợp lý: Email → Password → Remember me → Login → Forgot Password. |
| NFR-USA-02 | Trường nhập phải có label liên kết đúng để công nghệ hỗ trợ nhận biết. |
| NFR-USA-03 | Thông báo lỗi phải được công nghệ hỗ trợ thông báo và không chỉ dựa vào màu sắc. |
| NFR-USA-04 | Màu chữ/nền và trạng thái focus phải đáp ứng WCAG 2.1 AA. |
| NFR-COM-01 | Hỗ trợ hai phiên bản ổn định gần nhất của Chrome, Edge, Firefox và Safari. |
| NFR-COM-02 | Giao diện phải sử dụng được ở màn hình desktop và thiết bị di động phổ biến, không xuất hiện cuộn ngang ngoài ý muốn. |

## 11. Dữ liệu và quyền riêng tư

| Dữ liệu | Phân loại | Xử lý yêu cầu |
|---|---|---|
| Email | Dữ liệu định danh | Chỉ sử dụng cho xác thực/khôi phục; không hiển thị trong log công khai. |
| Mật khẩu | Dữ liệu xác thực bí mật | Che khi nhập; truyền qua HTTPS; không lưu dạng rõ; không đưa vào log. |
| Session ID/token | Dữ liệu xác thực bí mật | Sinh ngẫu nhiên đủ mạnh; lưu trong cookie bảo mật; thu hồi khi hết hiệu lực. |
| IP/thiết bị/thời điểm | Dữ liệu nhật ký bảo mật | Chỉ lưu theo chính sách bảo mật và thời hạn lưu trữ được phê duyệt. |

Tài khoản và mật khẩu dùng trong khảo sát không được ghi vào tài liệu này.

## 12. Ma trận nghiệm thu tối thiểu

| TC | Kịch bản | Kết quả mong đợi | Liên kết yêu cầu |
|---|---|---|---|
| TC-01 | Mở URL Login khi chưa có phiên | Hiển thị đầy đủ biểu mẫu Login | FR-LOGIN-01 |
| TC-02 | Bấm Login khi cả hai trường trống | Hiển thị hai thông báo bắt buộc; không đăng nhập | FR-LOGIN-05 |
| TC-03 | Chỉ để trống Email | Hiển thị lỗi bắt buộc của Email | FR-LOGIN-05 |
| TC-04 | Chỉ để trống Password | Hiển thị lỗi bắt buộc của Password | FR-LOGIN-05 |
| TC-05 | Nhập email `abc` | Ngăn gửi và báo sai định dạng | FR-LOGIN-06 |
| TC-06 | Nhập email hợp lệ nhưng sai tài khoản/mật khẩu | Hiển thị `Invalid email or password`; không tạo phiên | FR-LOGIN-10 |
| TC-07 | Nhập tài khoản và mật khẩu hợp lệ | Chuyển đến `/admin/`, hiển thị `Bảng tin` | FR-LOGIN-09 |
| TC-08 | Đăng nhập bằng phím Enter | Kết quả tương đương bấm Login | FR-LOGIN-11 |
| TC-09 | Login không chọn Remember me, đóng/mở lại trình duyệt sau khi phiên hết hạn | Yêu cầu đăng nhập lại | FR-LOGIN-12 |
| TC-10 | Login có chọn Remember me, đóng/mở lại trình duyệt trong thời hạn | Phiên vẫn hợp lệ | FR-LOGIN-13 |
| TC-11 | Người dùng đã đăng nhập mở URL Login | Chuyển đến `/admin/` | FR-LOGIN-15 |
| TC-12 | Bấm Forgot Password? | Mở đúng URL và biểu mẫu khôi phục | FR-LOGIN-16 |
| TC-13 | Nhập email khôi phục sai định dạng | Ngăn gửi và báo sai định dạng | FR-LOGIN-17 |
| TC-14 | Gửi yêu cầu khôi phục với email không tồn tại | Không lộ trạng thái tồn tại của tài khoản theo yêu cầu mục tiêu | FR-LOGIN-18, NFR-SEC-07 |
| TC-15 | Gửi yêu cầu khôi phục hợp lệ | Tạo token một lần, có hạn; gửi email; không lộ token | FR-LOGIN-19 |
| TC-16 | Thử đăng nhập sai liên tục vượt ngưỡng | Rate limit/biện pháp bảo vệ được kích hoạt | NFR-SEC-05 |
| TC-17 | Kiểm tra cookie phiên | Có Secure, HttpOnly, SameSite phù hợp | NFR-SEC-03 |
| TC-18 | Đăng xuất rồi dùng lại URL bảo vệ | Phiên bị vô hiệu và chuyển về Login | FR-LOGIN-14 |

## 13. Kết quả khảo sát và điểm cần xác nhận

### 13.1. Hành vi đã xác nhận

- Màn hình Login và các thành phần được mô tả tại mục 5.1 tồn tại.
- Bấm Login khi để trống hiển thị hai thông báo trường bắt buộc.
- Email sai định dạng bị kiểm tra bởi trình duyệt.
- Sai email hoặc mật khẩu hiển thị thông báo chung `Invalid email or password`.
- Đăng nhập hợp lệ chuyển đến `/admin/` và hiển thị trang `Bảng tin`.
- Trang Forgot Password tồn tại tại `/admin/authentication/forgot_password`.
- Trường email của Forgot Password có kiểm tra định dạng email.
- Gửi Forgot Password khi để trống hiển thị `Email not found` trên phiên bản khảo sát.

### 13.2. Cần Product Owner/đội kỹ thuật xác nhận

1. Thời hạn phiên thường và phiên `Remember me`.
2. Chính sách khóa/rate limit sau nhiều lần đăng nhập sai.
3. Điều kiện tài khoản bị khóa, chưa kích hoạt, bị xóa hoặc hết hạn.
4. Nội dung, thời hạn và số lần sử dụng token khôi phục mật khẩu.
5. SLA hiệu năng và mức sẵn sàng chính thức.
6. Danh sách trình duyệt, thiết bị và độ phân giải được hỗ trợ.
7. Chính sách lưu giữ nhật ký xác thực.
8. Ngôn ngữ chính thức của màn hình Login và thông báo lỗi.
9. Có yêu cầu CAPTCHA hoặc MFA theo mức rủi ro hay không.

## 14. Rủi ro đã nhận diện

| Mã | Rủi ro | Mức độ | Đề xuất |
|---|---|---|---|
| RSK-01 | Forgot Password trả `Email not found`, có thể hỗ trợ dò tài khoản. | Cao | Dùng thông báo trung tính và thời gian phản hồi đồng đều. |
| RSK-02 | Chưa xác nhận rate limit/khóa tạm thời. | Cao | Áp dụng giới hạn tần suất và giám sát bất thường. |
| RSK-03 | Chính sách Remember me chưa rõ. | Trung bình | Quy định thời hạn, xoay vòng và thu hồi token. |
| RSK-04 | Thông báo giao diện Login dùng tiếng Anh trong khi trang đích dùng tiếng Việt. | Thấp | Xác nhận yêu cầu đa ngôn ngữ và chuẩn hóa locale. |

## 15. Truy vết phạm vi khảo sát

| Hạng mục | Trạng thái |
|---|---|
| Hiển thị Login | Đã kiểm chứng |
| Bắt buộc Email/Password | Đã kiểm chứng |
| Định dạng Email | Đã kiểm chứng |
| Sai thông tin đăng nhập | Đã kiểm chứng |
| Đăng nhập thành công và URL đích | Đã kiểm chứng |
| Forgot Password - giao diện và kiểm tra định dạng | Đã kiểm chứng |
| Gửi email khôi phục thực tế | Không thực hiện để tránh phát sinh email |
| Remember me qua lần đóng/mở trình duyệt | Chưa kiểm chứng |
| Cookie, session timeout, rate limit, CSRF | Chưa kiểm chứng bằng giao diện |

