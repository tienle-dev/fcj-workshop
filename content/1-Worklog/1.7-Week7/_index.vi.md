---
title: "Worklog Tuần 7"
date: 2026-08-03
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Bảo mật, Giám sát & Tối ưu chi phí vận hành hệ thống AWS.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Rà soát lại toàn bộ mã nguồn Backend để loại bỏ các chuỗi kết nối (connection string) bị hardcode.<br>- Cấu hình lưu trữ khóa bí mật trên AWS Secrets Manager. | 03/08/2026 | 03/08/2026 |
| 3 | - Tích hợp Backend để gọi và giải mã chuỗi kết nối từ Secrets Manager khi runtime. | 04/08/2026 | 04/08/2026 |
| 4 | - Thiết lập Amazon CloudWatch, tạo Dashboard giám sát hệ thống.<br>- Đưa các metric quan trọng lên Dashboard: Độ trễ API Gateway, số lượng Lambda invocation. | 05/08/2026 | 05/08/2026 |
| 5 | - Theo dõi và thiết lập cảnh báo (Alarm) cho chi phí sử dụng API Amazon Bedrock. | 06/08/2026 | 06/08/2026 |
| 6 | - Dùng AWS Cost Explorer rà soát lại tài nguyên toàn hệ thống.<br>- Tiến hành dọn dẹp tài nguyên rác (Orphaned EBS, Elastic IP không dùng) giúp tối ưu chi phí sử dụng AWS. | 07/08/2026 | 08/08/2026 |

### Kết quả đạt được tuần 7:

Sau khi hệ thống cơ bản hoàn thiện, tôi dành riêng tuần này để đảm bảo game vận hành không chỉ trơn tru mà còn an toàn và tiết kiệm:

* **Bảo mật với AWS Secrets Manager:** Đã loại bỏ hoàn toàn rủi ro lộ lọt thông tin nhạy cảm. Toàn bộ chuỗi kết nối Database và khóa API Bedrock được chuyển sang lưu trữ mã hóa an toàn trên AWS Secrets Manager. Các hàm Lambda chỉ gọi lấy khóa khi đang chạy, đảm bảo mã nguồn (đẩy lên GitHub) hoàn toàn sạch.
* **Giám sát trực quan với CloudWatch:** Đã xây dựng thành công một Dashboard tổng quan trên Amazon CloudWatch. Từ đây, tôi có thể theo dõi "sức khỏe" hệ thống theo thời gian thực như: tốc độ phản hồi (latency) của API Gateway, tần suất gọi hàm Lambda (invocation) hay phát hiện các lỗi (error rate) một cách nhanh chóng.
* **Tối ưu hóa chi phí vận hành:** Sử dụng AWS Cost Explorer để phân tích biểu đồ chi phí. Thông qua đó, tôi đã phát hiện và dọn dẹp các tài nguyên bị "bỏ quên" (như EBS snapshot cũ, các Elastic IP không đính kèm) cũng như giới hạn lại ngân sách (budget) để ngăn ngừa hóa đơn phát sinh đột biến từ API AI.

  ![CloudWatch Dashboard Giám sát Hệ thống](/images/week7/cloudwatch_dashboard.png)
  *(Ghi chú: Cần bổ sung ảnh chụp màn hình CloudWatch Dashboard tại đây)*
