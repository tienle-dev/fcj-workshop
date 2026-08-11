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
| 5 | - Tìm hiểu các khái niệm cơ bản về Serverless Architecture (Lambda, API Gateway, DynamoDB). | 25/06/2026 | 25/06/2026 |
| 6 | - Cài đặt AWS CLI, cấu hình profile và làm quen cơ bản với AWS Cloud Development Kit (CDK).<br>- Tạo một ứng dụng Hello World đơn giản để test môi trường. | 26/06/2026 | 27/06/2026 |

### Kết quả đạt được tuần 1:

Trong tuần đầu tiên, tôi đã hoàn thành việc thiết lập nền tảng AWS cơ bản và đảm bảo các tiêu chuẩn bảo mật cho dự án:

* **Bảo mật tài khoản:** Kích hoạt thành công MFA cho tài khoản Root để ngăn ngừa truy cập trái phép. Tạo tài khoản IAM (IAM User) và cấp quyền truy cập Permissions policies vào các dịch vụ cần thiết, giúp an toàn hóa quá trình thao tác trên AWS.
* **Lưu trữ tài nguyên (S3):** Khởi tạo thành công S3 Bucket để lưu trữ tập trung toàn bộ tài nguyên (Asset) của game như ảnh UI, sprite nhân vật/vũ khí. Việc này giúp game Unity dễ dàng lấy dữ liệu thông qua URL mà không cần đóng gói trực tiếp vào game build, làm giảm dung lượng ứng dụng.
  
  ![Cấu trúc S3 Bucket lưu trữ tài nguyên](../../../images/1-Worklog/1.1-Week1/s3-bucket.png)
  *Cấu trúc S3 Bucket lưu trữ tài nguyên*

* **Cài đặt môi trường & Tìm hiểu Serverless:** Đã cài đặt thành công AWS CLI và khởi tạo môi trường lập trình. Dành thời gian nghiên cứu các khái niệm cốt lõi của kiến trúc Serverless (phi máy chủ) và AWS CDK, chuẩn bị nền tảng vững chắc cho việc viết code triển khai hạ tầng ở các tuần sau.
