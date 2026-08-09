---
title: "Worklog Tuần 5"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Xây dựng kiến trúc Backend Serverless (AWS Lambda & API Gateway) cho game.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Tái cấu trúc (Refactor) mã nguồn Backend .NET 8 để phù hợp với kiến trúc Serverless.<br>- Tạo các AWS Lambda Handlers độc lập. | 20/07/2026 | 20/07/2026 |
| 3 | - Tách logic xử lý thành các cụm chức năng riêng biệt: Auth, Character, Inventory, Story, Battle. | 21/07/2026 | 21/07/2026 |
| 4 | - Cấu hình Amazon API Gateway để tạo các Endpoint RESTful API.<br>- Liên kết API Gateway với các hàm AWS Lambda tương ứng. | 22/07/2026 | 22/07/2026 |
| 5 | - Đóng gói Backend thành Docker Image để đảm bảo tính nhất quán của môi trường chạy.<br>- Đẩy (Push) Docker Image lên Amazon ECR. | 23/07/2026 | 23/07/2026 |
| 6 | - Triển khai và chạy thử nghiệm hệ thống Serverless hoàn chỉnh.<br>- Cập nhật URL endpoint mới vào mã nguồn Unity và test luồng game. | 24/07/2026 | 25/07/2026 |

### Kết quả đạt được tuần 5:

Tuần này đánh dấu một bước chuyển mình lớn của hệ thống khi tôi tiến hành chuyển đổi hoàn toàn kiến trúc Backend truyền thống sang mô hình Serverless hiện đại trên AWS:

* **Hoàn thiện các AWS Lambda Handlers:** Toàn bộ logic nghiệp vụ (Auth, Character, Inventory, Story, Battle) được chia nhỏ thành các hàm Lambda riêng biệt chạy trên nền .NET 8. Việc chia nhỏ này giúp ứng dụng dễ dàng bảo trì và mỗi chức năng có thể tự động mở rộng (scale) độc lập tùy theo lượng người chơi.
* **Tích hợp API Gateway:** Đã thiết lập thành công cổng giao tiếp API Gateway kết nối trực tiếp đến các hàm Lambda. Cổng này đóng vai trò như một "lễ tân", tiếp nhận mọi yêu cầu RESTful API từ client (game Unity), kiểm tra tính hợp lệ và chuyển tiếp đến đúng hàm xử lý.
* **Triển khai bằng Docker & ECR:** Thay vì deploy file zip thông thường, tôi đã đóng gói code thành Docker Image và lưu trữ trên kho Amazon Elastic Container Registry (ECR). Giải pháp này khắc phục được giới hạn về dung lượng của Lambda và đồng bộ tuyệt đối môi trường chạy, tạo nên một hệ thống backend cực kỳ ổn định, không cần phải quản lý và bảo trì máy chủ ảo (EC2) truyền thống.

  ![Sơ đồ kiến trúc Serverless với API Gateway và Lambda](/images/week5/serverless_architecture.png)
  *(Ghi chú: Cần bổ sung hình ảnh kiến trúc API Gateway -> Lambda hoặc giao diện ECR tại đây)*
