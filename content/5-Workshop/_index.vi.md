---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai hệ thống Game RPG tương tác cốt truyện bằng AI (Serverless AWS)

#### Tổng quan

Trong workshop này, chúng ta sẽ xây dựng hệ thống Backend Serverless toàn diện trên đám mây **AWS** cho một tựa game nhập vai phiêu lưu (RPG) 2D. Điểm đặc biệt của dự án là việc ứng dụng Trí tuệ nhân tạo (Generative AI) từ **Amazon Bedrock** làm hệ thống dẫn chuyện (AI Dungeon Master), giúp tạo ra những tình huống và cốt truyện hoàn toàn độc nhất theo từng quyết định của người chơi.

Thay vì quản lý máy chủ truyền thống, toàn bộ kiến trúc (Backend) sẽ sử dụng mô hình **Serverless** (Không máy chủ) giúp hệ thống tự động mở rộng theo lưu lượng thực tế và tối ưu hóa chi phí.

#### Mục tiêu của Workshop

Sau khi hoàn thành workshop này, bạn sẽ nắm vững cách:
- Triển khai và quản lý luồng định danh người dùng an toàn với **Amazon Cognito**.
- Thiết kế cơ sở dữ liệu tốc độ cao (NoSQL) quản lý thông tin nhân vật và túi đồ bằng **Amazon DynamoDB**.
- Xây dựng các hàm tính toán logic game (Giao tranh, Rơi đồ) bằng **AWS Lambda** và phơi bày qua **Amazon API Gateway**.
- Viết kịch bản Prompt Engineering và gọi mô hình ngôn ngữ lớn (LLM) qua **Amazon Bedrock** để tự động sinh cốt truyện.
- Dùng **AWS CDK** để tự động hóa hạ tầng bằng mã nguồn (IaC).

#### Nội dung

1. [Tổng quan về workshop và Kiến trúc](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường](5.2-Prerequisites/)
3. [Triển khai hệ thống Xác thực (Cognito)](5.3-Authentication/)
4. [Xây dựng Game Logic (DynamoDB & Lambda)](5.4-Game-Backend/)
5. [Tích hợp AI Dẫn chuyện (Bedrock)](5.5-AI-Story-Engine/)
6. [Kết nối với Unity 2D Client](5.6-Client-Integration/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)