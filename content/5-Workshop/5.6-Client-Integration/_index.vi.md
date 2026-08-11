---
title : "Kết nối Unity 2D Client"
date : 2024-01-01 
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Tổng quan về Client Unity 2D

Sau khi đã hoàn thiện toàn bộ hệ thống API Backend (Xác thực, Nhân vật, Túi đồ, Đánh Boss, Dẫn chuyện AI) và triển khai lên AWS thông qua CDK. Bước cuối cùng để có một tựa game hoàn chỉnh là xây dựng Client (Giao diện phía người dùng). 

Trong dự án này, chúng ta sử dụng **Unity Engine (2D)**. Client hoàn toàn không chịu trách nhiệm xử lý logic (ví dụ: không tự trừ máu của Boss, không tự quay random vật phẩm) để tránh hacker dùng công cụ gian lận (cheat). Thay vào đó, Client sẽ vẽ giao diện (UI), gọi các API của AWS để xin phép thao tác và nhận kết quả cập nhật về.

#### Tích hợp HTTP Client trong Unity (sử dụng Task Async/Await)

Trước đây, lập trình viên Unity thường dùng `Coroutine` (thông qua `IEnumerator`) để gọi các hàm mạng. Tuy nhiên, kiến trúc dự án thực tế của chúng ta sử dụng lập trình bất đồng bộ hiện đại (`async/await`) với kiểu trả về `Task<T>`.

Để kết nối đến Amazon API Gateway, Unity sẽ sử dụng module `UnityWebRequest` được bọc bên trong một lớp `ApiClient` dùng chung cho toàn bộ dự án.

Một điểm tối quan trọng: Ngoại trừ API Đăng nhập/Đăng ký, mọi API khác đều yêu cầu Client phải đính kèm **JWT Token (Access Token)** vào Header `Authorization`. 

##### Quản lý JWT Token với ApiClient.cs

Lớp `ApiClient` được xây dựng theo mẫu thiết kế Singleton để duy trì kết nối xuyên suốt các cảnh (Scenes) trong game. Đoạn mã dưới đây là một ví dụ thu gọn mô phỏng cách `ApiClient` của chúng ta tự động đính kèm Token bảo mật:

```csharp
using UnityEngine.Networking;
using System.Threading.Tasks;
using System.Text;
using UnityEngine;

public class ApiClient : MonoBehaviour
{
    public static ApiClient Instance { get; private set; }
    
    private string baseUrl = "https://<api-gateway-id>.execute-api.ap-southeast-1.amazonaws.com/prod/";
    private string jwtToken = ""; // Lưu trữ sau khi Login

    private void Awake()
    {
        if (Instance == null) Instance = this;
        else Destroy(gameObject);
    }

    public void SetToken(string token) => jwtToken = token;

    // Hàm gọi API dùng chung bằng cơ chế Async/Await
    public async Task<T> PostAsync<T>(string endpoint, object bodyData)
    {
        string url = baseUrl + endpoint;
        string json = JsonUtility.ToJson(bodyData);
        
        using (UnityWebRequest request = new UnityWebRequest(url, "POST"))
        {
            byte[] bodyRaw = Encoding.UTF8.GetBytes(json);
            request.uploadHandler = new UploadHandlerRaw(bodyRaw);
            request.downloadHandler = new DownloadHandlerBuffer();
            request.SetRequestHeader("Content-Type", "application/json");
            
            // Tự động đính kèm Token JWT nếu có
            if (!string.IsNullOrEmpty(jwtToken))
            {
                request.SetRequestHeader("Authorization", "Bearer " + jwtToken);
            }

            var operation = request.SendWebRequest();
            while (!operation.isDone) await Task.Yield(); // Chờ đợi bất đồng bộ không khóa luồng UI

            if (request.result == UnityWebRequest.Result.Success)
            {
                return JsonUtility.FromJson<T>(request.downloadHandler.text);
            }
            else
            {
                Debug.LogError($"Lỗi gọi API {endpoint}: " + request.error);
                return default(T);
            }
        }
    }
}
```

#### Quy trình End-to-End Testing

Sau khi ráp toàn bộ mã nguồn Client và Backend lại với nhau, bạn hãy chạy Game trong Unity Editor và tiến hành kiểm thử End-to-End để đảm bảo các luồng hoạt động mượt mà:
1. Đăng ký một tài khoản mới -> Nhận Email chứa OTP -> Nhập mã OTP.
2. Đăng nhập và nhận Token.
3. Tạo nhân vật mới với Class (Ví dụ: Knight).
4. Mở Story Scene và bấm các lựa chọn để AI Bedrock dẫn chuyện.
5. Kiểm tra túi đồ khi nhặt được vật phẩm rơi ra sau màn đánh Boss.

Nếu mọi thứ hoạt động trơn tru mà không có lỗi (Error 401 Unauthorized hoặc 500 Internal Server Error), xin chúc mừng, bạn đã xây dựng thành công một tựa Game AI Serverless chuẩn thực chiến!
