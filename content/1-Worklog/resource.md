

| TRƯỜNG ĐẠI HỌC SÀI GÒN KHOA CÔNG NGHỆ THÔNG TIN   | CỘNG HÒA XÃ HỘI CHỦ NGHĨA VIỆT NAM Độc lập – Tự do – Hạnh phúc  *Tp. Hồ Chí Minh, ngày …  tháng ….  năm 20…* |
| :---: | :---: |

**BẢNG GHI NHẬN KẾT QUẢ THỰC TẬP HÀNG TUẦN**

| Một số thông tin liên hệ |  |  |
| ----- | :---- | ----- |
| Họ và tên: Tiến |  |  |
| Ngày sinh:  |  |  |
| Mã số sinh viên:  |  |  |
| Lớp:  |  |  |
| Ngành học: Công nghệ thông tin |  |  |
| Email:  |  |  |
| Điện thoại:  |  |  |
|  |  |  |
| Chuyên gia doanh nghiệp: Nguyễn Gia Hưng |  |  |
| Email: [hunggia@amazon.com](mailto:hunggia@amazon.com) |  |  |
| Điện thoại: 0817870645 |  |  |
|  |  |  |
| Giảng viên hướng dẫn: Nguyễn Thanh Sang |  |  |
| Email: thanhsang@sgu.edu.vn |  |  |
| Điện thoại: 0366686557 |  |  |

| Tuần | Nội dung thực tập (do chuyên gia của doanh nghiệp giao) | Kết quả thực tập (do chuyên gia của doanh nghiệp đánh giá) |
| :---: | ----- | ----- |
| 1 Từ ngày 22/6/ 2026 đến ngày 27/6/ 2026 | **Khởi tạo môi trường AWS & Bảo mật hạ tầng cơ bản:** \- Bật MFA cho tài khoản Root; phân quyền IAM chuẩn Least Privilege cho Dev. \- Cài đặt và cấu hình AWS CLI, chuẩn bị môi trường lập trình. \- Tìm hiểu các khái niệm cơ bản về kiến trúc Serverless và thực hành tạo thử nghiệm S3 Bucket chứa file tĩnh. |  |
| 2 Từ ngày 29/6/ 2026 đến ngày 03/ 07/ 2026 | **Tích hợp dịch vụ Xác thực người dùng (Amazon Cognito):** \- Khởi tạo Cognito User Pool & App Client cho game. \- Lập trình và kiểm thử các API: Đăng ký (Register), Đăng nhập (Login), Xác thực OTP (ConfirmSignUp) và Cấp lại Token (RefreshToken). \- Kết nối luồng xác thực JWT token giữa Backend C\# và Frontend Unity. |  |
| 3 Từ ngày 06/07/ 2026 đến ngày 11/07/ 2026 | **Thiết kế & Thao tác Cơ sở dữ liệu Game (DynamoDB / RDS):** \- Thiết kế cấu trúc cơ sở dữ liệu lưu trữ: Tài khoản (User), Nhân vật (Character), Vật phẩm (Inventory), Tiến trình câu chuyện (StorySession) và Trận đấu (Battle). \- Khởi tạo bảng DynamoDB / RDS, thiết lập Primary Key, Partition Key và Index (GSI). \- Viết lớp Repository C\# thao tác đọc/ghi dữ liệu trạng thái game thời gian thực. |  |
| 4 Từ ngày 13/07/ 2026 đến ngày 18/07/ 2026 | **Tích hợp Trí tuệ nhân tạo sinh cốt truyện (Amazon Bedrock AI):** \- Tích hợp API Amazon Bedrock (mô hình Amazon Nova Pro) phục vụ tính năng AI Storyteller. \- Viết module PromptBuilder để ghép nối ngữ cảnh (thông tin nhân vật, vật phẩm, lịch sử lượt chơi) cho AI hiểu. \- Viết hàm xử lý JSON đầu ra từ Bedrock để phát sinh diễn biến câu chuyện, danh sách lựa chọn (Choices) và bối cảnh Boss.  |  |
| 5 Từ ngày 20/07/ 2026 đến ngày 25/07/ 2026 | **Xây dựng kiến trúc Backend Serverless (AWS Lambda & API Gateway):** \- Chuyển logic code .NET 8 thành các hàm AWS Lambda (Auth, Character, Inventory, Story, Battle). \- Nối API Gateway làm cổng kết nối cho game Unity gọi tới. \- Dùng lệnh `dotnet publish` để build code và chỉnh sửa mức RAM/Timeout khác nhau cho từng Lambda để tối ưu (ví dụ nâng RAM cho hàm gọi AI).  |  |
| 6 Từ ngày 27/07/ 2026 đến ngày 01/08/ 2026 | **Tự động hóa hạ tầng đám mây (Infrastructure as Code \- AWS CDK):** \- Tập dùng AWS CDK bằng C# để tạo hạ tầng đám mây (Cognito, Database, Lambda, API) thay vì bấm bằng tay trên web. \- Thử nghiệm việc chia nhỏ code hạ tầng thành các file riêng biệt (Stack) để code đỡ rối. \- Thực hành gõ lệnh `cdk deploy` và `cdk destroy` để tạo và xóa tài nguyên trên AWS. |  |
| 7 Từ ngày 03/08/ 2026 đến ngày 08/08/ 2026 | **Bảo mật, Giám sát & Tối ưu chi phí vận hành:** \- Bảo mật code: Dùng Biến môi trường (Environment Variables) cho Lambda và thiết lập quyền IAM Role để kết nối DynamoDB, Bedrock thay vì hardcode thông tin. \- Cấu hình CloudWatch Dashboard để theo dõi hệ thống và cài đặt Alarm báo lỗi Lambda. \- Dùng Cost Explorer kiểm tra và dọn dẹp các tài nguyên không dùng để tránh phát sinh chi phí. |  |
| 8 Từ ngày 09/08/ 2026 đến ngày 15/08/ 2026 | **Kiểm thử End-to-End toàn bộ Game, Tối ưu & Bàn giao đồ án:** \- Kiểm thử toàn diện luồng chơi: Đăng ký/Đăng nhập \-\> Tạo nhân vật \-\> Sinh cốt truyện AI \-\> Nhận/trang bị vật phẩm \-\> Đánh Boss \-\> Lưu lịch sử. \- Đánh giá hệ thống theo Khung kiến trúc AWS Well-Architected Framework. \- Tổng hợp báo cáo thực tập tốt nghiệp và đóng gói mã nguồn/tài liệu hướng dẫn triển khai. |  |

**Chuyên gia doanh nghiệp hướng dẫn thực tập**  
(Ký tên và ghi họ tên)

**Ghi chú:**   
\-**Chuyên gia doanh nghiệp** ghi nhận kết quả thực tập của **sinh viên** theo tuần và gởi qua email cho **giảng viên hướng dẫn** khi kết thúc các tuần 3,6 của đợt thực tập. BẢNG GHI NHẬN KẾT QUẢ THỰC TẬP TỐT NGHIỆP HÀNG TUẦN này là một trong những hồ sơ kèm theo quyển báo cáo thực tập tốt nghiệp.  
\-Cột **Kết quả thực tập**, chuyên gia doanh nghiệp có thể ghi *Hoàn thành tốt*, *Hoàn thành*, *Không đạt* hoặc có thể ghi nhận chi tiết hơn.