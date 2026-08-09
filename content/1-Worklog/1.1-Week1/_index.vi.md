---
title: "Worklog Tuần 1"
date: 2026-06-22
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Khởi tạo môi trường AWS & Bảo mật hạ tầng cơ bản cho dự án game.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Bật xác thực đa yếu tố (MFA) cho tài khoản Root AWS.<br>- Thiết lập người dùng và phân quyền IAM theo chuẩn Least Privilege cho Developer. | 22/06/2026 | 22/06/2026 |
| 3 | - Tìm hiểu và khởi tạo Amazon S3 Bucket.<br>- Cấu hình quyền truy cập và chính sách CORS cho S3. | 23/06/2026 | 23/06/2026 |
| 4 | - Tải lên S3 các tài nguyên Game ban đầu: hình ảnh UI, sprite nhân vật, vũ khí và file cấu hình (JSON). | 24/06/2026 | 24/06/2026 |
| 5 | - Thiết kế kiến trúc mạng cơ bản: Tạo VPC, thiết lập Public/Private Subnet. | 25/06/2026 | 25/06/2026 |
| 6 | - Cấu hình Security Group bảo mật các luồng truy cập.<br>- Khởi tạo máy chủ ảo EC2 và kiểm tra kết nối SSH/RDP an toàn. | 26/06/2026 | 27/06/2026 |

### Kết quả đạt được tuần 1:

Trong tuần đầu tiên, tôi đã hoàn thành việc thiết lập nền tảng AWS cơ bản và đảm bảo các tiêu chuẩn bảo mật cho dự án:

* **Bảo mật tài khoản:** Kích hoạt thành công MFA cho tài khoản Root để ngăn ngừa truy cập trái phép. Đã tạo nhóm người dùng (IAM Group) và cấp quyền tối thiểu (Least Privilege) cho các vai trò phát triển (Developer), giúp an toàn hóa quá trình thao tác trên AWS.
* **Lưu trữ tài nguyên (S3):** Khởi tạo thành công S3 Bucket để lưu trữ tập trung toàn bộ tài nguyên (Asset) của game như ảnh UI, sprite nhân vật/vũ khí. Việc này giúp game Unity dễ dàng lấy dữ liệu thông qua URL mà không cần đóng gói trực tiếp vào game build, làm giảm dung lượng ứng dụng.
  
  ![Cấu trúc S3 Bucket lưu trữ tài nguyên](/images/week1/s3_bucket.png)
  *(Ghi chú: Cần bổ sung hình ảnh S3 Bucket tại đây)*

* **Hạ tầng mạng (VPC & EC2):** Đã thiết lập xong VPC dành riêng cho môi trường game, bao gồm các Subnet và Security Group quản lý cổng truy cập chặt chẽ. Khởi tạo một máy chủ EC2 thử nghiệm và thực hiện kết nối SSH an toàn thành công, chuẩn bị sẵn sàng cho các thiết lập backend phức tạp ở các tuần sau.
