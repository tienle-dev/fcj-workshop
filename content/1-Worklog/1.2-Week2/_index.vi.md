---
title: "Worklog Tuần 2"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Tích hợp dịch vụ Xác thực người dùng (Amazon Cognito) vào dự án game.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Tìm hiểu dịch vụ Amazon Cognito.<br>- Khởi tạo Cognito User Pool & App Client cấu hình cho game. | 29/06/2026 | 29/06/2026 |
| 3 | - Thiết lập các thuộc tính người dùng cần thiết (Email, Username).<br>- Lập trình API Đăng ký (Register) và Xác thực mã OTP (ConfirmSignUp). | 30/06/2026 | 30/06/2026 |
| 4 | - Lập trình API Đăng nhập (Login) và xử lý cấp lại Token (RefreshToken).<br>- Kiểm thử các API bằng Postman. | 01/07/2026 | 01/07/2026 |
| 5 | - Tích hợp luồng xác thực vào Backend C#.<br>- Lập trình quản lý JWT token (IdToken, AccessToken, RefreshToken). | 02/07/2026 | 02/07/2026 |
| 6 | - Kết nối luồng xác thực giữa Frontend Unity và Backend.<br>- Thiết kế UI Đăng nhập/Đăng ký cơ bản trong Unity. | 03/07/2026 | 03/07/2026 |

### Kết quả đạt được tuần 2:

Tuần này, trọng tâm công việc là xây dựng hệ thống đăng nhập, đăng ký an toàn cho người chơi sử dụng Amazon Cognito. Kết quả cụ thể như sau:

* **Khởi tạo Cognito User Pool:** Đã cấu hình thành công User Pool và App Client chuyên dụng cho game. Cài đặt các chính sách mật khẩu mạnh và yêu cầu xác thực email qua mã OTP khi đăng ký tài khoản mới.
* **Xây dựng API Xác thực:** Hoàn thành việc lập trình và kiểm thử toàn bộ luồng API xác thực cơ bản bao gồm: Register, Login, ConfirmSignUp, và RefreshToken. Các API hoạt động trơn tru và trả về token hợp lệ.
* **Tích hợp Frontend Unity & Backend C#:** Đã kết nối thành công luồng xử lý JWT token giữa server và client. Game Unity giờ đây có thể gửi request đăng nhập, nhận JWT token và lưu trữ an toàn để duy trì phiên đăng nhập cho các thao tác ingame sau này. UI đăng nhập cơ bản cũng đã được dựng xong.

  ![Giao diện đăng nhập trong Unity](/images/week2/unity_login.png)
  *(Ghi chú: Cần bổ sung hình ảnh UI đăng nhập của game Unity tại đây)*

  ```csharp
  // Cấu trúc code xử lý JWT token - Minh họa
  ```
  *(Ghi chú: Cần chèn một đoạn mã C# Login nếu có)*
