---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Kiểm thử End-to-End toàn bộ Game, Đánh giá tối ưu hệ thống & Bàn giao đồ án.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 2 | - Xây dựng kịch bản kiểm thử End-to-End (E2E).<br>- Test luồng: Đăng ký/Đăng nhập -> Tạo nhân vật. | 09/08/2026 | 09/08/2026 |
| 3 | - Test luồng tương tác AI: Sinh cốt truyện AI -> Đưa ra lựa chọn -> Cập nhật trạng thái game. | 10/08/2026 | 10/08/2026 |
| 4 | - Test luồng Gameplay: Nhận/trang bị vật phẩm -> Đánh Boss -> Lưu lịch sử (StorySession).<br>- Fix các bug phát sinh trong quá trình ghép nối. | 11/08/2026 | 12/08/2026 |
| 5 | - Đánh giá hệ thống theo Khung kiến trúc AWS Well-Architected Framework (tập trung vào Security, Reliability, Performance Efficiency). | 13/08/2026 | 13/08/2026 |
| 6 | - Tổng hợp và hoàn thiện báo cáo thực tập tốt nghiệp.<br>- Đóng gói toàn bộ mã nguồn (Backend CDK, Frontend Unity) và tài liệu hướng dẫn triển khai. | 14/08/2026 | 15/08/2026 |

### Kết quả đạt được tuần 8:

Tuần cuối cùng là lúc để hoàn thiện, đánh giá lại toàn bộ thành quả công việc trong suốt 2 tháng qua. Các kết quả cụ thể bao gồm:

* **Kiểm thử thành công toàn bộ luồng chơi:** Game đã vận hành trơn tru từ đầu đến cuối mà không gặp lỗi nghiêm trọng. Người chơi có thể đăng nhập, trải nghiệm hành trình độc nhất vô nhị do AI Storyteller tạo ra, chiến đấu với Boss và mọi trạng thái (vật phẩm, điểm số) đều được sao lưu thời gian thực về DynamoDB một cách chính xác.
* **Đánh giá AWS Well-Architected:** Đối chiếu hệ thống với các tiêu chuẩn tốt nhất của AWS. Hệ thống đạt mức tốt về Bảo mật (nhờ IAM, Cognito, Secrets Manager), Ổn định (nhờ kiến trúc Serverless Lambda không lo sập server) và Hiệu suất (nhờ API Gateway và DynamoDB).
* **Hoàn thiện Bàn giao:** Đã hoàn thành đóng gói mã nguồn và hoàn tất bài Báo cáo thực tập. Toàn bộ repo được viết kèm tài liệu README hướng dẫn các bước deploy lại hạ tầng CDK từ đầu, giúp dự án có thể dễ dàng chuyển giao hoặc mở rộng trong tương lai.

  ![Trải nghiệm Game Hoàn thiện](/images/week8/gameplay_final.png)
  *(Ghi chú: Cần bổ sung ảnh chụp màn hình gameplay hoàn thiện tại đây)*
