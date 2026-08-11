---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01 
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Dọn dẹp tài nguyên (Cleanup)

Sau khi đã hoàn thành bài thực hành và kiểm thử thành công trò chơi, điều quan trọng nhất là bạn cần phải dọn dẹp các tài nguyên đã tạo trên đám mây AWS. 

Mặc dù kiến trúc Serverless (Lambda, API Gateway, DynamoDB) chỉ tính phí khi có truy cập, tuy nhiên việc giữ lại các tài nguyên không sử dụng vẫn có thể phát sinh những khoản phí nhỏ lẻ ngoài ý muốn (ví dụ phí lưu trữ dữ liệu của DynamoDB hoặc S3).

#### Hướng dẫn xóa tự động bằng AWS CDK

Vì toàn bộ hạ tầng Backend của chúng ta (từ Cognito, API Gateway, đến DynamoDB) đều được định nghĩa dưới dạng mã nguồn (Infrastructure as Code) và triển khai thông qua AWS CDK, việc xóa bỏ chúng cực kỳ đơn giản và nhanh chóng.

1. Mở Terminal / Command Prompt của bạn.
2. Điều hướng tới thư mục gốc chứa mã nguồn CDK của Backend C#.
3. Chạy lệnh sau để xóa toàn bộ các CloudFormation Stacks đã được tạo ra:

   ```bash
   cdk destroy --all
   ```

4. Hệ thống sẽ liệt kê các Stack chuẩn bị bị xóa và yêu cầu bạn xác nhận (`y/n`). Hãy gõ `y` và nhấn Enter.
5. Chờ vài phút để AWS CloudFormation tiến hành tháo dỡ tuần tự các tài nguyên.

#### Kiểm tra lại trên giao diện AWS Console

Để chắc chắn 100% mọi thứ đã được dọn sạch:
- Đăng nhập vào giao diện [AWS Management Console](https://console.aws.amazon.com/).
- Vào dịch vụ **CloudFormation**, kiểm tra xem các Stack của bạn (như `CognitoStack`, `LambdaStack`, `ApiStack`, `DatabaseStack`) đã ở trạng thái `DELETE_COMPLETE` hoặc biến mất khỏi danh sách hay chưa.
- Một số tài nguyên lưu trữ như **S3 Bucket** (nếu có chứa file) hoặc **DynamoDB Table** có thể được cấu hình mặc định là `Retain` (giữ lại) để tránh mất dữ liệu quan trọng. Nếu chúng chưa bị xóa, hãy vào trực tiếp dịch vụ đó trên Console và xóa bằng tay (Manual delete).

Chúc mừng bạn đã hoàn tất toàn bộ quy trình xây dựng, triển khai và quản lý một tựa game nhập vai AI Serverless! Hẹn gặp lại bạn ở các Workshop tiếp theo.
