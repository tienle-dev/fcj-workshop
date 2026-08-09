---
title: "AWS First Cloud Journey AI Meetup"
date: 2026-06-13
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch: "AWS First Cloud Journey AI Meetup"

### Mục Đích Của Sự Kiện

- Trang bị cho sinh viên và lập trình viên trẻ các kiến thức thực tế về thiết kế kiến trúc đám mây có khả năng mở rộng (như dịch vụ rút gọn liên kết URL Shortener).
- Chia sẻ góc nhìn thực tế về công việc phân tích dữ liệu (Data Analytics), quy trình tuyển dụng và văn hóa làm việc tại các tập đoàn đa quốc gia (MNC).
- Cung cấp cái nhìn chân thực về công việc DevOps thực tế hàng ngày, phạm vi trách nhiệm và các kỹ năng nền tảng cốt lõi cần chuẩn bị.
- Đề xuất lộ trình 8 bước phát triển sự nghiệp toàn diện từ một sinh viên tò mò đến đối tác của AWS và người dẫn dắt cộng đồng công nghệ.

### Danh Sách Diễn Giả

- **Đinh Trung Kiên** – Lead Developer tại một Startup
- **Nguyễn Minh Thọ** – Sinh viên
- **Đạt Phạm** – Data Analytics Engineer (Kamereo & Colgate-Palmolive)
- **Cường Nguyễn** – Process Engineer (Colgate-Palmolive)
- **Hoàng Trọng** – DevOps Engineer @ Endava Vietnam
- **Danh Hoàng Hiếu Nghị** – AI Engineer, AWS Community Builder, và AWS Student Builder Group Leader

---

### Nội Dung Nổi Bật

#### 1. Thiết kế dịch vụ rút gọn liên kết có thể mở rộng trên AWS (Kiên & Thọ)
- **Đặt vấn đề:** Dịch vụ rút gọn liên kết (URL Shortener) chuyển đổi một URL dài phức tạp thành mã ngắn. Mô hình cơ bản ban đầu (User → Frontend → Backend → Database) dễ triển khai và chi phí rẻ, nhưng dễ gặp lỗi bảo mật, độ trễ khi đọc cao (Read Latency), có điểm lỗi đơn lẻ (SPOF), và rất khó để mở rộng quy mô khi lưu lượng truy cập tăng vọt.
- **Kiến trúc đề xuất:**
  - **Bảo mật & Điều hướng biên:** Quản lý bởi **Amazon Route 53** (DNS), **Amazon CloudFront** (CDN) để phân phối và caching nhanh, kết hợp với **AWS WAF** (Tường lửa ứng dụng web) để lọc lưu lượng xấu. Việc quản lý khóa bảo mật, phân quyền và chứng chỉ sử dụng **AWS Secrets Manager**, **AWS KMS**, **AWS IAM** và **AWS Certificate Manager**.
  - **Lớp Frontend:** Quản lý và deploy tự động qua **AWS Amplify**.
  - **Lớp Backend (Tính toán):** Triển khai các container SpringBoot chạy trên **AWS Fargate** (Amazon ECS) kết hợp bộ cân bằng tải **Application Load Balancer (ALB)** trên nhiều Availability Zones (AZs) để đảm bảo tính sẵn sàng cao.
  - **Lớp Lưu trữ & Caching:** Cơ sở dữ liệu chính là **Amazon DynamoDB** (NoSQL) và cụm **Amazon ElastiCache for Redis** (trong Database Subnet riêng biệt) để tối ưu hóa tốc độ đọc/ghi.
- **Đi sâu vào kiến trúc xử lý:**
  - **Dịch vụ tạo khóa trước - Key Generation Service (KGS):** Để tránh việc sinh mã ngẫu nhiên khi người dùng gửi yêu cầu (dễ bị trùng lặp và tốn thời gian tính toán), một service độc lập chạy trên ECS container sẽ tạo sẵn các mã ngắn (ví dụ: `GpFHUcn`, `aB3xZ9q`) và đẩy vào hàng đợi trong Redis bằng lệnh `LPUSH key_queue`.
  - **Luồng Tạo liên kết (Create Flow):** Khi người dùng tạo link ngắn, backend chỉ cần rút một mã có sẵn từ Redis qua lệnh `RPOP` và ghi cặp `{mã ngắn: URL dài}` vào DynamoDB. Quá trình này diễn ra tức thì và hoàn toàn không lo trùng lặp (collision-free).
  - **Luồng Chuyển hướng (Forward Flow):** Khi người dùng click vào link ngắn, hệ thống kiểm tra trong Redis trước. Nếu tìm thấy (Cache Hit), trả về ngay URL dài để chuyển hướng. Nếu không (Cache Miss), hệ thống mới truy vấn DynamoDB và lưu lại vào Redis để phục vụ cho các lần sau (Cache-aside pattern).

#### 2. Phân tích dữ liệu & Văn hóa doanh nghiệp tại các tập đoàn đa quốc gia (MNC) (Đạt Phạm & Cường Nguyễn)
- **Thực tế công việc dữ liệu:**
  - **Tại Kamereo (Nền tảng B2B thực phẩm):** Xây dựng báo cáo hàng ngày/tuần/tháng/quý để theo dõi hiệu suất vận hành, thiết kế dashboard phát hiện bất thường và phối hợp liên phòng ban hỗ trợ ra quyết định kinh doanh.
  - **Tại Colgate-Palmolive (Tập đoàn FMCG):** Phân tích dữ liệu thiết bị sản xuất và IoT trong nhà máy, tìm cơ hội tối ưu chi phí sản xuất và thúc đẩy các dự án chuyển đổi số dài hạn.
- **Bốn kỹ năng cốt lõi:** Tư duy phản biện, kỹ năng giao tiếp, kể chuyện với dữ liệu (Data Storytelling - biến số liệu khô khan thành gợi ý hành động cụ thể cho sếp, ví dụ: tìm hiểu nguyên nhân biến động GMV thay vì chỉ liệt kê doanh thu), và giải quyết vấn đề.
- **Dashboard phân tích thực tế (Kamereo Hanoi):** Minh họa hoạt động thực tế bao gồm GMV (+0.5%), giá trị đơn hàng trung bình (AOV đạt 913K), số đơn hàng/ngày (78 đơn), chi phí xử lý (FFM% 11.7%-13.2%), chi phí giao hàng chặng cuối (LMC% 7.8%), chi phí nhà cung cấp dự phòng (11.1%), và tỷ lệ đủ hàng (99.1%).
- **Mô hình 5 giai đoạn tư duy phát triển sự nghiệp:**
  1. *Follower:* Làm việc theo hướng dẫn chi tiết, làm quen môi trường (Thực tập sinh/Junior).
  2. *Learner:* Hiểu cách giải quyết bài toán nhưng cần mentor định hướng; biết hỏi các câu hỏi sâu.
  3. *Problem Solver:* Chủ động phân tích sâu, đề xuất giải pháp tối ưu và chịu trách nhiệm cho chất lượng đầu ra.
  4. *System Thinker:* Nhìn nhận bài toán ở bức tranh toàn cảnh, hiểu mối liên kết chéo giữa các bộ phận, quản trị rủi ro vận hành và tài chính.
  5. *Super Star:* Thiết lập tầm nhìn, định hướng chiến lược dữ liệu và phát triển thế hệ kế cận.
- **Quy trình tuyển dụng chuẩn tại MNCs:** Trải qua 4 vòng khắt khe: Sàng lọc CV & phỏng vấn tiếng Anh với HR, Test Năng lực (Logic/Tech/Supply Chain), Phỏng vấn Chuyên môn (sử dụng mô hình **STAR** để hỏi sâu các dự án thực tế), và Phỏng vấn Văn hóa (Culture Fit) với ban lãnh đạo.
- **Giải mã văn hóa MNC:**
  - *Văn hóa No-Blame Post-Mortem (Môi trường công nghệ):* Khi xảy ra sự cố hệ thống nghiêm trọng, tập trung tìm nguyên nhân gốc rễ để cải tiến quy trình chứ không đổ lỗi cá nhân.
  - *Văn hóa Caring & Inclusive (Môi trường FMCG):* Đặt con người làm trung tâm, tôn trọng sự đa dạng và không ngừng cải tiến.

#### 3. Trăn trở quốc gia & Tiêu chuẩn toàn cầu (Đạt Phạm & Cường Nguyễn)
- **Lịch sử chuỗi cung ứng và Internet tại Việt Nam (1975 - 1997):**
  - *1975 - 1986:* Giai đoạn bao vây cô lập kinh tế, phân phối hàng hóa thủ công.
  - *1986 - 1995:* Đổi mới kinh tế và bình thường hóa ngoại giao mở đường cho logistics phát triển. Ngoại giao là "logistics" đi đầu.
  - *1997:* Việt Nam chính thức kết nối Internet toàn cầu (19/11/1997), khai thông dòng chảy thông tin số.
- **Kỷ nguyên FDI & Công xưởng số:** Chuyển dịch kép qua hai hiệu ứng domino: Chuỗi vật lý (FDI → Sản xuất → Logistics) và Chuỗi số (4G → Điện thoại thông minh → Khởi nghiệp → Đám mây).
- **Nâng cấp tiêu chuẩn cuộc chơi:** Chuyển từ "làm được" sang "làm đúng chuẩn quốc tế":
  - *Chuỗi cung ứng vật lý:* Tuân thủ **GMP**, **GSP**, **GDP** để đảm bảo an toàn hàng hóa.
  - *Chuỗi cung ứng số:* Tuân thủ **ISO 27001**, **SOC 2**, **GDPR** để bảo vệ dữ liệu và chủ quyền số quốc gia.
  - *Mô hình triết lý "Đúng việc" của thế hệ trẻ:* Gồm 3 vùng cốt lõi: **Làm người** (thấu hiểu, tử tế, tự quản trị nội tâm), **Làm nghề** (phụng sự, giải quyết bài toán thực tế xuất sắc), và **Làm dân** (trách nhiệm quốc gia, gánh vác huyết mạch số).

#### 4. Thực tế công việc & Hành trang DevOps (Hoàng Trọng)
- **Xu hướng thị trường:** Các vị trí hạ tầng và dữ liệu (AI/ML, Data, Cloud, Security, DevOps) có nhu cầu tuyển dụng và mức thu nhập tăng trưởng nhanh. Lương DevOps dao động từ Junior (16-28 triệu) đến Lead/Expert (65-100 triệu).
- **Góc nhìn thực tế:** DevOps không chỉ đơn thuần là CI/CD hay Docker/Kubernetes mà bao hàm khối lượng kiến thức khổng lồ (IaC, Cloud, Sec, Monitoring, Serverless). Công việc đi liền với trách nhiệm và áp lực giải quyết yêu cầu từ nhiều bên:
  - *Developer:* Hỗ trợ debug khi code chạy local nhưng lỗi ở staging.
  - *QA/Tester:* Khôi phục môi trường test và cấp quyền hệ thống.
  - *Client/User:* Trực chiến (On-call) xử lý sự cố khi hệ thống chậm hoặc sập.
  - *Project Manager:* Quản lý quy trình và làm rõ quyền sở hữu (Ownership) khi chuẩn bị release.
  - *Security:* Rà soát và vá các lỗ hổng bảo mật của thư viện.
  - *Finance:* Điều tra hóa đơn Cloud tăng cao và tối ưu hóa chi phí tài nguyên.
- **Hành trang cho người mới:** Tập trung vào các **Nền tảng cốt lõi (Fundamentals)**: Hệ điều hành Linux, mạng máy tính cơ bản, ngôn ngữ scripting (Python, Go), Git & CI/CD, containerization (Docker), và kiến thức vận hành ứng dụng thực tế theo phương châm "Break it, fix it" (tự làm hỏng để tự sửa).
- **Bài học xương máu:** Copy lệnh không có nghĩa là bạn hiểu nó; tìm đúng người chịu trách nhiệm cho vấn đề; luôn hỏi "Tại sao" trước khi hỏi "Làm như thế nào"; giao tiếp là chìa khóa; và tránh biến mình thành anh hùng đơn độc gánh team. Tư duy hệ thống, tự động hóa tác vụ lặp đi lặp lại và sử dụng AI thông minh mà "không tắt não".

##### 5. Lộ trình phát triển từ sinh viên đến AWS Partner (Hiếu Nghị)
- **Lộ trình 8 bước sự nghiệp:** Student Curiosity → First Cloud Journey → Workshop & Community → Hands-on Labs → School Projects → Portfolio → AWS Partner → Share Back.
- **Các dấu mốc phát triển:**
  - *First Cloud AI Journey Program:* Hệ thống LMS học tập bài bản các dịch vụ AWS cốt lõi (VPC, IAM, EC2, storage, databases, monitoring).
  - *AWS Student Builder Group:* Dẫn dắt câu lạc bộ sinh viên, tổ chức training trực tuyến (như workshop Amazon Bedrock AI) và nhận Badge/AWS Credits tài tài trợ.
  - *AWS Community Builder:* Trở thành Community Builder toàn cầu, chia sẻ kiến thức tại các hội nghị lớn như AWS Community Day Vietnam (Bitexco) và nhận quà tặng độc quyền từ AWS.
  - *AWS Partners:* Làm việc tại đối tác chiến lược của AWS, tiêu biểu là RENOVA CLOUD với giải thưởng "AWS Partner of the Year - Vietnam 2026".
- **Thông điệp:** "Nhận được một công việc mới chỉ là sự khởi đầu." Hãy liên tục kết nối và chia sẻ lại cho cộng đồng (Share Back) để tạo bệ phóng phát triển dài lâu.

---

### Những Gì Học Được

#### Tư duy thiết kế
- **Phân tách mối quan tâm (Separation of Concerns):** Phân chia luồng đọc và ghi độc lập giúp tối ưu hiệu năng và tránh tắc nghẽn hệ thống.
- **Phòng thủ tại vùng biên:** Sử dụng CloudFront/WAF để xử lý bảo mật và caching ngay từ biên mạng, giảm tải cho hệ thống lõi.
- **Tư duy hướng nghiệp và chuẩn hóa:** Công nghệ phải đi liền với bài toán kinh doanh thực tế và tuân thủ các quy chuẩn bảo mật quốc tế (ISO 27001, SOC 2, GDPR).

#### Kiến trúc kỹ thuật
- **Tính toán trước (Pre-computation):** Sinh sẵn tài nguyên (như mã rút gọn) bất đồng bộ giúp giảm thời gian phản hồi ở các luồng tạo trực tiếp của người dùng.
- **Cache-aside Pattern:** Sử dụng bộ nhớ đệm in-memory (Redis) làm chốt chặn bảo vệ Database và giảm độ trễ đọc xuống tối đa.
- **Nền tảng quan trọng hơn công cụ:** Các công cụ có thể thay đổi liên tục, nhưng kiến thức nền tảng về HĐH, mạng, scripting và container là bất biến.

#### Phát triển sự nghiệp & Văn hóa
- **Tư duy hệ thống:** Nhìn nhận bài toán một cách tổng thể, thấu hiểu mối liên kết tài chính, vận hành và con người.
- **Văn hóa không đổ lỗi:** Tập trung khắc phục hệ thống và quy trình hơn là tìm cá nhân chịu tội khi xảy ra sự cố.
- **Chia sẻ cộng đồng:** Việc chia sẻ kiến thức (Share Back) không chỉ giúp đỡ đàn em mà còn củng cố vững chắc kiến thức của bản thân.

---

### Ứng Dụng Vào Công Việc

- **Áp dụng bộ nhớ đệm:** Triển khai mô hình Cache-aside bằng Redis để giảm tải cho DB trong các đồ án và dự án thực tế.
- **Tối ưu bảo mật biên:** Sử dụng CDN (CloudFront) và WAF để tăng cường an ninh mạng cho các ứng dụng web.
- **Nắm vững DevOps cơ bản:** Tự động hóa quá trình build/deploy bằng Docker và CI/CD, viết script tự động hóa hạ tầng.
- **Phân tích Dashboard thực tế:** Thiết kế dashboard chú trọng kể chuyện bằng dữ liệu (GMV, AOV, FFM%) thay vì chỉ hiển thị bảng biểu đơn thuần.
- **Định hình lộ trình học tập:** Bắt đầu xây dựng portfolio chuyên nghiệp, thi chứng chỉ đám mây (AWS) và tích cực tham gia, chia sẻ kiến thức trong các câu lạc bộ công nghệ.

---

### Trải nghiệm trong event

Tham gia buổi **AWS First Cloud Journey AI Meetup** đã mang lại cho tôi những kiến thức chuyên môn và định hướng sự nghiệp vô cùng đắt giá.

- **Bài học từ các chuyên gia thực thụ:** Được nghe chia sẻ từ các kỹ sư DevOps, Data và AI tại Colgate, Endava, Renova Cloud giúp tôi hiểu rõ yêu cầu tuyển dụng thực tế của doanh nghiệp.
- **Nâng cao tư duy thiết kế hệ thống:** Phân tích kỹ lưỡng về KGS (Key Generation Service) và cấu hình AWS thực tế giúp tôi hình dung rõ nét cách vận hành hệ thống ở quy mô lớn.
- **Truyền cảm hứng mạnh mẽ:** Lộ trình 8 bước đi từ sinh viên tò mò đến Community Builder và đối tác AWS của anh Hiếu Nghị đã tiếp thêm động lực lớn để tôi học tập và cống hiến cho cộng đồng.
- **Môi trường giao lưu cởi mở:** Workshop tạo không gian tuyệt vời để tôi kết nối với các đàn anh đi trước và nhận những phần quà ý nghĩa từ ban tổ chức.

#### Một số hình ảnh khi tham gia sự kiện
![Event photo 1](hinh-anh-sk-1/IMG_20260613_093319.webp)

> Tổng thể, sự kiện không chỉ trang bị cho tôi kiến thức kỹ thuật về AWS mà còn giúp tôi định hình lại tư duy làm nghề, sự phối hợp giữa kinh doanh - công nghệ, và trách nhiệm phát triển cộng đồng công nghệ số Việt Nam.
