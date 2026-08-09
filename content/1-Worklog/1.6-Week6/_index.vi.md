---
title: "Worklog Tuần 6"
date: 2026-07-27
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tự động hóa hạ tầng đám mây (Infrastructure as Code - AWS CDK).

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Tìm hiểu về khái niệm Infrastructure as Code (IaC) và công cụ AWS CDK.<br>- Khởi tạo project CDK bằng ngôn ngữ C#. | 27/07/2026 | 27/07/2026 |
| 3 | - Viết mã nguồn định nghĩa CognitoStack (User Pool, App Client) và DatabaseStack (DynamoDB). | 28/07/2026 | 28/07/2026 |
| 4 | - Viết mã nguồn định nghĩa LambdaStack (các hàm xử lý) và ApiStack (API Gateway). | 29/07/2026 | 29/07/2026 |
| 5 | - Cấu hình quy trình CI/CD sử dụng GitHub Actions.<br>- Tự động hóa việc Build Docker Image và Deploy hạ tầng trực tiếp từ kho mã nguồn GitHub. | 30/07/2026 | 30/07/2026 |
| 6 | - Thực hành chạy các lệnh CDK CLI (`cdk synth`, `cdk deploy`, `cdk destroy`).<br>- Đánh giá tính linh hoạt trong việc quản lý tài nguyên. | 31/07/2026 | 01/08/2026 |

### Kết quả đạt được tuần 6:

Thay vì cấu hình thủ công từng dịch vụ trên giao diện web AWS (Console), tuần này tôi đã áp dụng phương pháp Infrastructure as Code (IaC) bằng AWS Cloud Development Kit (CDK) để tự động hóa hoàn toàn quy trình triển khai:

* **Viết hạ tầng bằng Code C#:** Tôi đã sử dụng chính ngôn ngữ C# quen thuộc để lập trình ra các lớp (Stack) định nghĩa toàn bộ hệ thống, bao gồm: CognitoStack, DatabaseStack, LambdaStack và ApiStack. Việc code hóa hạ tầng giúp tôi quản lý phiên bản (version control) dễ dàng và tránh các sai sót khi cấu hình bằng tay.
* **Tích hợp CI/CD với GitHub Actions:** Đã thiết lập thành công đường ống CI/CD. Giờ đây, mỗi khi có thay đổi code được đẩy lên nhánh chính của kho mã nguồn GitHub, hệ thống tự động build Docker image và kích hoạt lệnh deploy AWS CDK để cập nhật hạ tầng mà không cần can thiệp thủ công.
* **Quản lý tài nguyên linh hoạt:** Nắm vững việc sử dụng các lệnh CDK CLI. Nhờ vậy, tôi có thể tạo ra một bản sao toàn bộ hệ thống (deploy) chỉ trong vài phút, và gỡ bỏ hoàn toàn (destroy) một cách an toàn khi không còn sử dụng, giúp tối ưu hóa chi phí.

  ![Giao diện GitHub Actions CI/CD](/images/week6/github_actions.png)
  *(Ghi chú: Cần bổ sung ảnh chụp màn hình luồng chạy GitHub Actions thành công tại đây)*

  ```csharp
  // Ví dụ đoạn code định nghĩa LambdaStack bằng AWS CDK C#
  ```
  *(Ghi chú: Cần chèn một đoạn code CDK C# minh họa)*
