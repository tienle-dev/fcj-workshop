---
title : "Hệ thống Xác thực (Cognito)"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Luồng Quản lý Tài khoản & Định danh

Bước đầu tiên trong bất kỳ tựa game online nào là xây dựng hệ thống đăng ký và đăng nhập. Trong kiến trúc Serverless trên AWS, **Amazon Cognito** là dịch vụ hoàn hảo để đảm nhận trọng trách này. Nó giúp quản lý danh sách người dùng (User Pool), mã hóa mật khẩu an toàn và cung cấp cơ chế xác thực mạnh mẽ (bao gồm cả mã OTP qua Email và chuẩn JWT).

Thay vì tự xây dựng máy chủ riêng biệt để lưu trữ tài khoản, chúng ta sẽ giao phó toàn bộ quy trình này cho AWS. 

#### 1. Định nghĩa hạ tầng Cognito bằng mã nguồn (AWS CDK)

Trong dự án thực tế, hạ tầng không được tạo bằng tay trên giao diện web mà được tự động hóa hoàn toàn bằng mã nguồn (Infrastructure as Code - IaC) thông qua **AWS CDK**. 

Dưới đây là trích đoạn mã nguồn thực tế từ file `CognitoStack.cs` trong dự án Backend:

```csharp
using Amazon.CDK;
using Amazon.CDK.AWS.Cognito;
using Constructs;

namespace Infrastructure.Stacks
{
    public class CognitoStack : Stack
    {
        public UserPool UserPool { get; }
        public UserPoolClient UserPoolClient { get; }

        public CognitoStack(Construct scope, string id, IStackProps? props = null) : base(scope, id, props)
        {
            // Khởi tạo Cognito User Pool với các chính sách bảo mật
            UserPool = new UserPool(this, "GameUserPool", new UserPoolProps
            {
                UserPoolName = "RPG-Game-User-Pool",
                SelfSignUpEnabled = true, // Cho phép người dùng tự đăng ký
                AutoVerify = new AutoVerifiedAttrs { Email = true }, // Tự động gửi OTP qua Email
                PasswordPolicy = new PasswordPolicy
                {
                    MinLength = 8,
                    RequireDigits = true,
                    RequireLowercase = true,
                    RequireUppercase = false,
                    RequireSymbols = false
                },
                AccountRecovery = AccountRecovery.EMAIL_ONLY
            });

            // Khởi tạo Client truy cập cho Unity Game
            UserPoolClient = UserPool.AddClient("GameMobileClient", new UserPoolClientOptions
            {
                UserPoolClientName = "GameMobileClient",
                AuthFlows = new AuthFlow { UserPassword = true },
                GenerateSecret = false // Mobile/Unity client không giữ client secret vì rủi ro bảo mật
            });
        }
    }
}
```

Đoạn code trên quy định rõ: mật khẩu người chơi cần ít nhất 8 ký tự, có số và chữ thường, đồng thời tự động kích hoạt tính năng gửi mã xác thực (OTP) qua Email để kích hoạt tài khoản.

#### 2. Viết API Đăng nhập với AWS Lambda (C#)

Sau khi có User Pool, bước tiếp theo là xây dựng các hàm Serverless bằng AWS Lambda để hứng yêu cầu từ Client (Unity). Các hàm này đóng vai trò trung gian, tiếp nhận thông tin người dùng và gọi thư viện AWS SDK của Cognito.

Hãy cùng xem chi tiết file `LoginHandler.cs` (nhiệm vụ xử lý Đăng nhập) trong dự án của chúng ta:

```csharp
using Amazon.Lambda.APIGatewayEvents;
using Amazon.Lambda.Core;
using GameBackend.Core.Services.Interfaces;
using GameBackend.Core.Utils;
using GameShared.DTOs.Auth;
using Microsoft.Extensions.DependencyInjection;

[assembly: LambdaSerializer(typeof(Amazon.Lambda.Serialization.SystemTextJson.DefaultLambdaJsonSerializer))]

namespace GameBackend.Handlers.Auth
{
    /// <summary>
    /// Lambda entrypoint cho POST /auth/login.
    /// </summary>
    public class LoginHandler
    {
        private readonly IAuthService _authService;

        public LoginHandler()
        {
            // Khởi tạo Dependency Injection
            var sp = ServiceProviderBuilder.Build();
            _authService = sp.GetRequiredService<IAuthService>();
        }

        public async Task<APIGatewayProxyResponse> Handler(APIGatewayProxyRequest request, ILambdaContext context)
        {
            // Xử lý CORS cho các yêu cầu pre-flight
            if (request.HttpMethod.Equals("OPTIONS", StringComparison.OrdinalIgnoreCase))
                return ResponseBuilder.Options();

            try
            {
                // Parse dữ liệu từ Client gửi lên
                var loginRequest = JsonUtils.Deserialize<LoginRequest>(request.Body);
                if (loginRequest == null || string.IsNullOrWhiteSpace(loginRequest.username))
                    return ResponseBuilder.Error(400, "Invalid request payload", "INVALID_REQUEST");

                // Gọi lớp dịch vụ xử lý Đăng nhập với Cognito
                var result = await _authService.LoginAsync(loginRequest);
                
                // Trả về Token (JWT) nếu đăng nhập thành công
                return ResponseBuilder.Success(result, "Login successful");
            }
            catch (GameNotFoundException ex)
            {
                return ResponseBuilder.Error(404, ex.Message, "USER_NOT_FOUND");
            }
            catch (GameUnauthorizedException ex)
            {
                return ResponseBuilder.Error(401, ex.Message, "INVALID_CREDENTIALS");
            }
            catch (Exception ex)
            {
                context.Logger.LogLine($"Error: {ex.Message} {ex.StackTrace}");
                return ResponseBuilder.Error(500, "Internal server error", "SERVER_ERROR");
            }
        }
    }
}
```

Đoạn mã trên xử lý việc hứng Http Request từ API Gateway, chuyển đổi sang chuỗi JSON và xử lý các kịch bản lỗi (ví dụ: Sai mật khẩu - trả về HTTP 401, Không tìm thấy người dùng - trả về HTTP 404). Nếu thành công, mã **Access Token (chuẩn JWT)** sẽ được trả về và Unity Client phải lưu giữ cẩn thận để tiếp tục trò chơi.

![Giao diện Đăng ký và Đăng nhập Unity](/images/5-Workshop/5.3-Authentication/login-ui.png)
*Hình 5.3.1: Giao diện Đăng nhập và Đăng ký tài khoản trên Unity Client*
