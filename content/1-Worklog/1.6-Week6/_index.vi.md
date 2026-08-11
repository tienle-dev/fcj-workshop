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
| 5 | - Bổ sung thêm code C# định nghĩa phần Storage (S3) và Monitoring (CloudWatch).<br>- Thử nghiệm việc chia nhỏ code hạ tầng ra nhiều file (Stack) để code gọn gàng hơn. | 30/07/2026 | 30/07/2026 |
| 6 | - Thực hành chạy các lệnh CDK CLI (`cdk synth`, `cdk deploy`, `cdk destroy`).<br>- Đánh giá tính linh hoạt trong việc quản lý tài nguyên. | 31/07/2026 | 01/08/2026 |

### Kết quả đạt được tuần 6:

Tuần này tôi bắt đầu làm quen với khái niệm "Hạ tầng như một mã nguồn" (Infrastructure as Code - IaC) thông qua công cụ AWS CDK. Thay vì phải lên web AWS tạo thủ công từng tài nguyên, tôi dùng code để tự động hóa việc này:

* **Dùng code C# để tạo hạ tầng AWS:** Thay vì phải lên web click chuột tạo từng cái bảng DynamoDB hay hàm Lambda, tôi đã học cách dùng chính code C# (ngôn ngữ quen thuộc khi làm Unity) để khai báo hạ tầng. Việc dùng code thế này giúp tôi đỡ bị nhầm lẫn hay quên các bước cấu hình nếu lỡ bấm sai trên web.
* **Tập chia nhỏ file code hạ tầng:** Lúc đầu tôi định viết tất cả vào chung một file, nhưng thấy code quá dài và rối. Vì vậy, tôi đã học cách chia nó ra thành nhiều cụm nhỏ (gọi là các Stack) như Database, API, Lambda. Dù ban đầu hơi khó hiểu về cách lấy dữ liệu qua lại giữa các file này, nhưng sau khi làm quen thì tôi thấy code gọn gàng và dễ tìm lỗi hơn hẳn.
* **Quản lý tài nguyên linh hoạt:** Nắm vững việc sử dụng các lệnh CDK CLI. Nhờ vậy, tôi có thể tạo ra một bản sao toàn bộ hệ thống (deploy) chỉ trong vài phút, và gỡ bỏ hoàn toàn (destroy) một cách an toàn khi không còn sử dụng, giúp tối ưu hóa chi phí.

  ![Giao diện terminal chạy lệnh cdk deploy](../../../images/1-Worklog/1.6-Week6/cdk-deploy.png)
  *Giao diện terminal chạy lệnh cdk deploy*

  ```csharp
  // Code khai báo User Pool trong CognitoStack.cs
  public CognitoStack(Construct scope, string id, IStackProps? props = null) : base(scope, id, props)
  {
      UserPool = new UserPool(this, "GameUserPool", new UserPoolProps
      {
          UserPoolName = "RPG-Game-User-Pool",
          SelfSignUpEnabled = true,
          AutoVerify = new AutoVerifiedAttrs { Email = true },
          PasswordPolicy = new PasswordPolicy { MinLength = 8, RequireDigits = true }
      });
  }
  ```
