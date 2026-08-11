---
title : "Tích hợp AI Dẫn chuyện (Bedrock)"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Tổng quan về AI Story Engine

Trong các tựa game RPG truyền thống, kịch bản được viết sẵn (hard-coded) bởi đội ngũ biên kịch. Nhưng với sự trợ giúp của **Amazon Bedrock**, chúng ta sẽ biến mô hình ngôn ngữ lớn (LLM) thành một Người dẫn chuyện (AI Dungeon Master) đầy sáng tạo.

AI sẽ ghi nhớ các thao tác trước đó của bạn, đánh giá chỉ số nhân vật hiện tại và tự động vạch ra diễn biến câu chuyện cũng như đưa ra 3 phương án lựa chọn (hành động) để bạn quyết định hướng đi tiếp theo.

#### Luồng hoạt động của Hệ thống Dẫn chuyện

1. **Gửi yêu cầu Hành động (`POST /story/action`)**:
   - Khi người chơi click chọn 1 trong 3 hành động hiển thị trên màn hình, Unity Client sẽ gọi API đẩy quyết định đó lên Backend Lambda.

2. **Xây dựng Ngữ cảnh (Prompt Builder)**:
   - Một vấn đề thực tế khi làm việc với LLM: AI không tự động nhớ được toàn bộ quá khứ nếu ta không cung cấp. Nếu ta gửi toàn bộ lịch sử chơi game từ level 1, chi phí Token sẽ khổng lồ và AI xử lý rất chậm.
   - Giải pháp: Hàm Lambda của chúng ta sẽ quét DynamoDB và chỉ trích xuất **5 lượt chơi gần nhất** từ bảng `StorySessions`.
   - Kết hợp 5 lượt này với chỉ số nhân vật (Class, Level, Vũ khí đang cầm), hệ thống đúc kết thành một `Prompt Template` chuẩn chỉ trước khi đưa cho AI. 

3. **Giao tiếp với Amazon Bedrock**:
   - Lambda gửi khối Prompt này tới Amazon Bedrock thông qua AWS SDK.
   - Mô hình LLM (như `anthropic.claude-v2`) sẽ suy luận và sinh ra kết quả dưới định dạng JSON bao gồm: `Nội dung cốt truyện mới` và `3 Lựa chọn hành động mới`.

4. **Hiển thị trên Client**:
   - Khi nhận được JSON phản hồi, Unity sẽ cập nhật lại giao diện Story Scene, chạy chữ cốt truyện từ từ lên màn hình và hiện 3 nút bấm tương ứng.

![Giao diện Story Scene](/images/5-Workshop/5.5-AI-Story-Engine/story-ui.png)
*Hình 5.5.1: Giao diện màn hình Dẫn chuyện AI (Story Scene)*

#### Mã nguồn tương tác Story trên Unity (Client)

Dưới đây là một phần mã nguồn (class `StoryApiService`) được dùng trên Unity Client để gọi Backend, truyền hành động của người chơi và nhận về cốt truyện tiếp theo:

```csharp
using System.Threading.Tasks;
using UnityEngine;
using GameShared.DTOs.Story;

/// <summary>
/// API service cho Story feature.
/// Giao tiếp với endpoints POST story/start và POST story/action
/// </summary>
public class StoryApiService
{
    // Bắt đầu một màn chơi cốt truyện mới
    public async Task<StoryActionResponse> StartStoryAsync(string characterId, string storyFileId = "prologue")
    {
        var body = new StoryStartBody { characterId = characterId, storyFileId = storyFileId };
        // ApiClient tự động đính kèm JWT Token vào Header và gửi POST request
        return await ApiClient.Instance.PostAsync<StoryActionResponse>("story/start", body);
    }

    // Gửi hành động/lựa chọn của người chơi lên AI Server
    public async Task<StoryActionResponse> SendActionAsync(string characterId, string sessionId, int choiceIndex, string playerInput)
    {
        var body = new StoryActionBody
        {
            characterId = characterId,
            sessionId = sessionId,
            choiceIndex = choiceIndex,
            playerInput = playerInput
        };
        // Nhận lại JSON chứa: Nội dung câu chuyện tiếp theo & 3 Lựa chọn mới
        return await ApiClient.Instance.PostAsync<StoryActionResponse>("story/action", body);
    }

    [System.Serializable]
    private class StoryStartBody { public string characterId; public string storyFileId; }

    [System.Serializable]
    private class StoryActionBody { public string characterId; public string sessionId; public int choiceIndex; public string playerInput; }
}
```

Việc tích hợp này minh chứng cho sức mạnh kết hợp giữa Game Client truyền thống và Generative AI thông qua kiến trúc Serverless, mở ra một chân trời mới về trải nghiệm nhập vai không giới hạn.
