
# DỰ ÁN: AI DUNGEON RPG ADVENTURE GAME

> ⚠️ **Lưu ý:** Báo cáo proposal dưới đây được tổng hợp dựa trên kiến trúc và mã nguồn thực tế của dự án game 2D **AI Dungeon RPG Adventure Game** (Unity 2D + AWS Serverless + AWS Bedrock).

---

## 1. Executive Summary (Tóm tắt dự án)

Dự án **AI Dungeon RPG Adventure Game** là hệ thống game nhập vai phiêu lưu dungeon kết hợp Trí tuệ Nhân tạo Sáng tạo (Generative AI) được xây dựng trên kiến trúc **AWS Serverless**. Game cho phép người chơi tạo nhân vật, trải nghiệm cốt truyện phiêu lưu tương tác tự do do AI (**AWS Bedrock**) sinh ra theo thời gian thực (real-time narrative generation), quản lý hành trang (inventory), trang bị và tham gia các trận chiến theo lượt (turn-based RPG battles) với Boss.

Hệ thống sử dụng **AWS Lambda (.NET 8)**, **Amazon API Gateway**, **Amazon Cognito** cho xác thực bảo mật và **Amazon DynamoDB** để lưu trữ trạng thái nhân vật cũng như lịch sử phiên chơi. Game Client được phát triển trên nền tảng **Unity 2D**.

---

## 2. Problem Statement (Phát biểu bài toán)

### Vấn đề là gì? (What’s the Problem?)

Các tựa game RPG phiêu lưu truyền thống thường bị giới hạn bởi kịch bản cố định (*hard-coded scripts*) và các nhánh cây lựa chọn đóng khung. Việc phát triển nội dung đa dạng đòi hỏi chi phí sản xuất kịch bản rất lớn nhưng người chơi vẫn nhanh chóng cảm thấy nhàm chán sau khi vượt qua các nhánh chơi. Ngoài ra, việc vận hành máy chủ game truyền thống (*stateful servers*) tốn kém chi phí hạ tầng và khó mở rộng linh hoạt khi lượng người chơi biến động.

### Giải pháp (The Solution)

Dự án đề xuất giải pháp game RPG phiêu lưu tương tác ứng dụng **AWS Bedrock** để tạo câu chuyện linh hoạt và cá nhân hóa cho từng lựa chọn của người chơi:

* **AI Generative Storytelling (AWS Bedrock):** Sinh cốt truyện, tình huống, các lựa chọn và phản hồi hành động của người chơi theo ngữ cảnh thực tế.
* **Serverless Game Backend:** AWS Lambda (.NET 8) kết hợp Amazon API Gateway xử lý toàn bộ logic nghiệp vụ (xác thực, tạo nhân vật, tính toán chỉ số chiến đấu, quản lý kho đồ, phân tích phản hồi AI).
* **Lưu trữ dữ liệu NoSQL (Amazon DynamoDB):** Lưu giữ trạng thái nhân vật, phiên chơi (*story session*), trang bị (*inventory*) và lịch sử lượt chơi với độ trễ cực thấp.
* **Bảo mật & Quản lý người dùng (Amazon Cognito):** Quản lý đăng ký, đăng nhập và phân quyền JWT token an toàn.
* **Game Client (Unity 2D):** Giao diện đồ họa Unity 2D sinh động, giao tiếp mượt mà với RESTful API backend.

### Lợi ích và Tỷ lệ hoàn vốn (Benefits & ROI)

* **Tăng tính chơi lại (Replayability):** Mỗi lượt chơi là một trải nghiệm độc nhất nhờ khả năng sinh kịch bản vô hạn của mô hình LLM.
* **Tối ưu chi phí vận hành:** Nhờ kiến trúc Serverless, chi phí hạ tầng hoàn toàn phụ thuộc vào lưu lượng thực tế (*Pay-as-you-go*), không phát sinh chi phí duy trì server nhàn rỗi.
* **Khả năng mở rộng tự động:** Hệ thống tự động co giãn từ vài người chơi thử nghiệm lên hàng nghìn người chơi đồng thời mà không cần cấu hình lại hạ tầng.
* **Chi phí tối ưu:** Trong giai đoạn phát triển và thử nghiệm, chi phí AWS gần như bằng $0 nhờ gói Free Tier (Cognito, DynamoDB, API Gateway, Lambda) và chi phí sinh token thực tế của AWS Bedrock rất thấp.

---

## 3. Solution Architecture (Kiến trúc giải pháp)

Hệ thống sử dụng mô hình Serverless hoàn toàn trên AWS kết hợp với Unity Game Client.

### Các dịch vụ AWS sử dụng (AWS Services Used)

* **AWS Bedrock:** Cung cấp mô hình ngôn ngữ lớn (LLM) để sinh cốt truyện, các lựa chọn, diễn biến phiêu lưu và cơ chế tương tác NPC/Boss.
* **AWS Lambda (.NET 8):** Thực thi toàn bộ business logic backend (xử lý auth, tạo/lấy nhân vật, quản lý inventory, xử lý tính toán chiến đấu battle, gọi Bedrock API).
* **Amazon API Gateway:** Cung cấp RESTful API làm cầu nối giao tiếp giữa Unity Client và các hàm AWS Lambda.
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL lưu trữ thông tin User, Character, Inventory, StorySession, BossEncounter.
* **Amazon Cognito:** Quản lý tài khoản người dùng, đăng ký/đăng nhập, cấp phát và xác thực Token JWT.
* **AWS CloudWatch:** Ghi log, theo dõi hiệu năng và giám sát lỗi cho các hàm Lambda và API Gateway.
* **AWS CDK (C#):** Định nghĩa toàn bộ Hạ tầng dưới dạng Mã nguồn (*Infrastructure as Code - IaC*).

### Thành phần thiết kế (Component Design)

* **Unity Game Client:** Đảm nhận việc hiển thị giao diện 2D (Menu, Story, Battle, Inventory, Profile, Shop), gửi request và xử lý response JSON từ API Backend.
* **Authentication Layer:** Cognito User Pool cấp phát JWT Token sau khi đăng nhập thành công; API Gateway kiểm tra token cho mỗi request.
* **Logic Processing Layer:** Các hàm Lambda (.NET 8) nhận request, gọi `PromptBuilder` để đóng gói ngữ cảnh game, gửi tới AWS Bedrock, sau đó dùng `StoryAiResponseParser` và `GameRuleValidator` để kiểm tra và cập nhật lại dữ liệu.
* **Data Layer:** DynamoDB lưu trữ dữ liệu nhân vật, lượt chơi và vật phẩm với độ trễ tính bằng millisecond.

---

## 4. Technical Implementation (Triển khai kỹ thuật)

### Các giai đoạn triển khai (Implementation Phases)

1. **Phân tích & Thiết kế Kiến trúc (Giai đoạn 1):** Thiết kế Luồng dữ liệu (Data Flow), định nghĩa DTOs, viết Prompt Templates cho AI và thiết kế database schema cho DynamoDB.
2. **Xây dựng Hạ tầng IaC & Backend (Giai đoạn 2):** Viết mã AWS CDK bằng C# để dựng Cognito, DynamoDB, API Gateway, Lambda. Phát triển các Core Services (.NET 8) xử lý AuthService, StoryService, BattleService, BedrockService.
3. **Phát triển Unity Game Client (Giai đoạn 3):** Xây dựng UI/UX trên Unity 2D (Scenes: Login, Register, Create Character, Story, Battle, Profile, Shop), tích hợp `ApiClient` để gọi REST API backend.
4. **Kiểm thử, Tối ưu & Đóng gói (Giai đoạn 4):** Kiểm thử tích hợp (End-to-End Testing), tối ưu hóa Prompt gửi đến Bedrock để giảm chi phí token và độ trễ, hoàn thiện tài liệu dự án.

### Yêu cầu kỹ thuật (Technical Requirements)

* **Backend:** .NET 8 (C#), AWS SDK for .NET, AWSSDK.BedrockRuntime, Amazon.CDK.
* **Game Engine:** Unity (2D, URP 2D, TextMeshPro, C# scripting, REST Client).
* **AI/LLM:** AWS Bedrock Runtime (Foundation Models).
* **Database & Auth:** DynamoDB (Table Keys, Partition Keys), Amazon Cognito (User Pool, App Client).

---

## 5. Timeline & Milestones (Lộ trình & Cột mốc)

* **Milestone 1:** Hoàn thành thiết kế hệ thống, khởi tạo mô hình CDK và triển khai Cognito Authentication + User/Character Database.
* **Milestone 2:** Tích hợp AWS Bedrock thành công, xây dựng Prompt Builder & Response Parser cho chuỗi phiêu lưu AI.
* **Milestone 3:** Hoàn thiện logic RPG Battle (Turn-based), hệ thống quản lý Inventory, Item, Boss Encounter trên backend.
* **Milestone 4:** Tích hợp hoàn chỉnh Unity Client với Backend API, kiểm thử E2E, hoàn thiện báo cáo tài liệu.

---

## 6. Budget Estimation (Ước tính ngân sách)

### Chi phí hạ tầng AWS (Dự kiến hàng tháng trong giai đoạn thử nghiệm & demo)

* **AWS Cognito:** $0.00 (Miễn phí dưới 50,000 MAU theo Cognito Free Tier).
* **AWS Lambda:** $0.00 (Nằm trong mốc 1 triệu requests/tháng miễn phí).
* **Amazon API Gateway:** ~$0.01 - $0.10 / tháng (Cho các request thử nghiệm).
* **Amazon DynamoDB:** $0.00 (Nằm trong mốc 25GB lưu trữ miễn phí của AWS Free Tier).
* **AWS Bedrock:** Tính theo số lượng Token (Prompt + Completion Token). Ước tính khoảng $1.00 - $5.00 / tháng cho quá trình thử nghiệm & demo.
* **AWS CloudWatch:** ~$0.10 / tháng cho lượng logs cơ bản.
* **Tổng chi phí hạ tầng ước tính:** **~$1.50 - $6.00 / tháng** (Rất tiết kiệm nhờ kiến trúc Serverless & Free Tier).

### Chi phí Phần cứng / Phần mềm

* Thiết bị máy tính cá nhân sẵn có cho phát triển Unity và Backend (.NET 8). Chi phí phần mềm bổ sung: $0 (Sử dụng công cụ mã nguồn mở & Unity Personal License).

---

## 7. Risk Assessment (Đánh giá rủi ro)

### Bảng rủi ro (Risk Matrix)

| Rủi ro | Mức độ ảnh hưởng | Khả năng xảy ra |
| --- | --- | --- |
| **Độ trễ phản hồi từ AI LLM (Bedrock Latency)** | Cao | Trung bình |
| **AI sinh dữ liệu sai định dạng JSON (Malformed Output)** | Cao | Trung bình |
| **Chi phí Bedrock Token vượt hạn mức** | Trung bình | Thấp |
| **Lỗi mất đồng bộ trạng thái game (State Desync)** | Trung bình | Thấp |

### Chiến lược giảm thiểu (Mitigation Strategies)

* **Độ trễ AI:** Hiển thị hiệu ứng loading/narrative typing mượt mà trên Unity Client trong lúc chờ AI phản hồi.
* **Sai định dạng JSON:** Xây dựng module `StoryAiResponseParser` và `GameRuleValidator` ở Backend để validate và tự động fallback/retry nếu AI trả về sai schema.
* **Kiểm soát chi phí:** Cấu hình giới hạn Token tối đa (`max_tokens`) cho mỗi request Bedrock và thiết lập AWS Budget Alerts.
* **Quản lý trạng thái:** Mọi thay đổi về thông số nhân vật và lượt chơi đều được xác thực và cập nhật đồng bộ trực tiếp vào DynamoDB từ Backend (*Server-authoritative*).

### Kế hoạch dự phòng (Contingency Plans)

* Chuẩn bị sẵn bộ kịch bản và dữ liệu cuộc phiêu lưu mẫu (*Fallback Story Template*) trong backend để game vẫn hoạt động bình thường nếu kết nối tới AWS Bedrock gặp sự cố tạm thời.

---

## 8. Expected Outcomes (Kết quả kỳ vọng)

* **Cải tiến kỹ thuật:**
* Xây dựng thành công hệ thống game RPG Serverless 100% linh hoạt, khả năng mở rộng cao.
* Tích hợp thành công Generative AI (AWS Bedrock) vào luồng chơi thực tế (*Dynamic Storytelling*).


* **Giá trị lâu dài:**
* Bộ khung kiến trúc (*Architecture Framework*) có thể tái sử dụng cho các dự án game AI hoặc ứng dụng tương tác cốt truyện khác.
* Cung cấp giải pháp mẫu chuẩn về việc kết hợp Unity Game Engine với Serverless Backend .NET 8 trên hạ tầng AWS.