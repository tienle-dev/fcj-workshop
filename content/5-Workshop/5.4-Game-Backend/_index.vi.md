---
title : "Triển khai, xây dung logic cho game"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Thiết kế Cơ sở dữ liệu NoSQL với Amazon DynamoDB

Trong Game, dữ liệu như thông tin nhân vật, số lượng vật phẩm trong túi đồ, trạng thái máu liên tục thay đổi. Để đảm bảo độ trễ thấp nhất có thể cho số lượng truy cập đồng thời lớn, chúng ta sử dụng **Amazon DynamoDB**.

Cấu trúc các bảng (Tables) cốt lõi của game bao gồm:
- **Bảng `GameUsers`**: 
  - Partition Key: `UserId` (GUID)
  - Chức năng: Lưu trữ thông tin định danh của người chơi.
- **Bảng `Characters`**: 
  - Partition Key: `CharacterId` (GUID)
  - Các trường dữ liệu chính: `Level`, `Experience`, `Stats` (chứa HP, Attack, Defense).
- **Bảng `Inventory`**: 
  - Partition Key: `CharacterId`
  - Sort Key: `ItemId` (Để dễ dàng truy vấn 1 vật phẩm cụ thể của 1 nhân vật).
- **Bảng `Battles`**: 
  - Partition Key: `BattleId`
  - Chức năng: Lưu trạng thái của những cuộc giao tranh với Trùm (Boss) để người chơi không thể gian lận bằng cách đóng ứng dụng.

#### Các luồng xử lý Game Logic (AWS Lambda)

Toàn bộ logic của game được tính toán trên đám mây. Tránh để logic nằm ở Client nhằm phòng chống hack/cheat.

##### 1. Luồng Khởi tạo và Truy xuất Nhân vật
Khi người chơi lần đầu truy cập, họ cần tạo một nhân vật. Hệ thống (Lambda `CharacterHandler`) nhận yêu cầu chọn Class (ví dụ: Chiến binh, Pháp sư) từ Client, sau đó cấp cho nhân vật các chỉ số sức mạnh cơ bản dựa trên Class đó và lưu vào bảng `Characters`.

![Giao diện Tạo nhân vật và Profile](/images/5-Workshop/5.4-Game-Backend/character-ui.png)
*Hình 5.4.1: Giao diện Khởi tạo nhân vật và Màn hình Hồ sơ (Profile)*

##### 2. Luồng Quản lý Túi đồ và Vật phẩm (Inventory)
Cơ chế hòm đồ yêu cầu hệ thống phải luôn kiểm tra (Validate) các điều kiện khắt khe trước khi thay đổi trạng thái trong Cơ sở dữ liệu.

- Khi người chơi chọn **Trang bị (Equip)** một vũ khí mới, Backend sẽ:
  1. Kiểm tra trong bảng `Inventory` xem người chơi có thực sự sở hữu item này không.
  2. Kiểm tra xem Item này có đúng loại "Vũ khí" (Weapon) không (chống việc đội vũ khí lên đầu).
  3. Cập nhật trạng thái `IsEquipped = true` cho Item mới.
  4. Cộng điểm Tấn công/Giáp của Item đó vào bảng `Characters`.

Ngược lại khi **Tháo (Unequip)**, hệ thống sẽ trừ điểm chỉ số tương ứng. Nếu sử dụng (Use) bình máu, Backend sẽ cộng lượng HP hồi phục vào Máu hiện tại của nhân vật.

![Giao diện Túi đồ Inventory](/images/5-Workshop/5.4-Game-Backend/inventory-ui.png)
*Hình 5.4.2: Giao diện Túi đồ (Inventory) và tính năng Quản lý Vật phẩm*

##### 3. Luồng Giao tranh Đánh Boss (Battle System)
Khi đụng độ Boss, luồng chiến đấu được thực thi trên Backend:
- **Khởi tạo (`POST /battle/spawn`)**: Sinh ra thông số máu và sát thương của một quái vật lưu vào bảng `Battles`.
- **Giải quyết Giao tranh (`POST /battle/resolve`)**: Khi người chơi chọn *Tấn công*, Lambda sẽ so sánh và tính toán:
  - `Sát thương gây ra = Tấn công của nhân vật - Phòng thủ của Boss`.
  - Trừ HP của Boss và cập nhật vào bảng `Battles`.
  - Nếu Boss hết HP (Người chơi chiến thắng), Lambda sẽ tự động kích hoạt hàm **LootDrop** để rớt vật phẩm ngẫu nhiên và lưu chúng thẳng vào túi đồ của người chơi, đồng thời cộng điểm kinh nghiệm (EXP).

![Giao diện Đánh Boss](/images/5-Workshop/5.4-Game-Backend/battle-ui.png)
*Hình 5.4.3: Giao diện Màn hình Giao tranh (Battle Scene)*
