---
title : "Chuẩn bị môi trường"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Các công cụ cần thiết

Để bắt đầu tham gia workshop, bạn cần chuẩn bị môi trường phát triển trên máy tính cá nhân. Do dự án sử dụng C# .NET 8 cho Backend và Unity cho Client, hãy đảm bảo bạn cài đặt đầy đủ các thành phần sau:

1. **Tài khoản AWS**: Bạn cần một tài khoản AWS để có thể cấp quyền và khởi tạo tài nguyên. Nếu chưa có, hãy tạo một tài khoản AWS miễn phí (Free Tier). Đảm bảo tạo User IAM có quyền AdministratorAccess để chạy AWS CDK.

2. **AWS CLI & Cấu hình Profile**:
   - Tải và cài đặt [AWS CLI](https://aws.amazon.com/cli/).
   - Mở Terminal/Command Prompt và chạy lệnh `aws configure` để thiết lập Access Key, Secret Key và Default Region (ví dụ: `ap-southeast-1`).

3. **Node.js và AWS CDK Toolkit**:
   - Cài đặt [Node.js](https://nodejs.org/) (phiên bản LTS).
   - Mở Terminal và cài đặt AWS CDK Toolkit toàn cục bằng lệnh:
     ```bash
     npm install -g aws-cdk
     ```

4. **.NET 8 SDK**:
   - Tải và cài đặt [.NET 8.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0). Đây là nền tảng cốt lõi để viết mã nguồn Lambda Serverless.
   - Kiểm tra cài đặt bằng lệnh: `dotnet --version`.

5. **Unity Hub và Unity Editor** (Dành cho phần Client):
   - Cài đặt [Unity Hub](https://unity.com/download) và cài một phiên bản Unity Editor (Khuyến nghị bản 2022.3 LTS hoặc mới hơn).
   - Môi trường lập trình C# cho Unity (Visual Studio, Rider hoặc VS Code).

6. **Postman (Tùy chọn)**:
   - Cài đặt [Postman](https://www.postman.com/) để hỗ trợ gọi và kiểm thử các API RESTful độc lập với giao diện Client.