## <a name="create-hello-webapi-project"></a>Hello WebAPI 프로젝트 만들기
새 ASP.NET WebAPI 백 엔드 hello 섹션에 만들고 3 가지 기본 목적을 갖습니다.

1. **클라이언트 인증**: 이후 tooauthenticate 클라이언트 요청 및 연결 hello 사용자에 게 hello 요청이 메시지 처리기 추가 됩니다.
2. **클라이언트 알림 등록**: 나중 클라이언트 장치 tooreceive 알림을 컨트롤러 toohandle 새 등록 추가 됩니다. hello 인증 된 사용자 이름이 자동으로 추가 됩니다 toohello로 등록 하는 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx)합니다.
3. **알림 tooClients 보내기**: 나중에 추가 합니다 컨트롤러 tooprovide 사용자 tootrigger 보안 밀어넣기 toodevices 하는 방법 및 hello 태그와 연결 된 클라이언트입니다. 

단계를 수행 하는 hello toocreate 새 ASP.NET WebAPI 백 엔드 hello 하는 방법을 보여 줍니다. 

> [!IMPORTANT]
> 이 자습서를 시작 하기 전에 이전, 또는 Visual Studio 2015를 사용 하는 경우 hello 최신 버전의 hello NuGet 패키지 관리자를 설치 했는지 확인 하십시오. toocheck, Visual Studio 시작 합니다. Hello에서 **도구** 메뉴를 클릭 하 여 **확장명 및 업데이트**합니다. 검색할 **NuGet 패키지 관리자** hello 최신 버전의 경우 할 버전의 Visual Studio 및 있는지 확인 하십시오. 그렇지 않은 경우에, 제거한 다음 hello NuGet 패키지 관리자를 다시 설치 하십시오.
> 
> ![][B4]
> 
> [!NOTE]
> Hello Visual Studio를 설치 했는지 확인 [Azure SDK](https://azure.microsoft.com/downloads/) 웹 사이트 배포에 대 한 합니다.
> 
> 

1. Visual Studio 또는 Visual Studio Express를 시작합니다. 클릭 **서버 탐색기** tooyour Azure 계정에에서 로그인 합니다. Visual Studio toocreate hello 웹 사이트 리소스 계정에 로그인 할 수 있습니다.
2. Visual Studio에서 클릭 **파일**, 클릭 **새로**, 다음 **프로젝트**, 확장 **템플릿**, **Visual C#**, 클릭 **웹** 및 **ASP.NET 웹 응용 프로그램**, 형식 hello 이름 **AppBackend**, 클릭 하 고 **확인**합니다. 
   
    ![][B1]
3. Hello에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **웹 API**, 클릭 **확인**합니다.
   
    ![][B2]
4. Hello에 **Microsoft Azure 웹 앱 구성** 대화 상자에서 구독을 선택 및 **앱 서비스 계획** 이미 만들었습니다. 선택할 수도 있습니다 **새 앱 서비스 계획 만들기** hello 대화 상자에서 하나를 만듭니다. 이 자습서를 위해 데이터베이스는 필요하지 않습니다. 앱 서비스 계획을 선택 하면 클릭 **확인** toocreate hello 프로젝트.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>인증 클라이언트 toohello WebAPI 백 엔드
이 섹션에서는 라는 새 메시지 처리기 클래스가 만들어집니다 **AuthenticationTestHandler** hello 새 백 엔드에 대 한 합니다. 이 클래스에서 파생 된 [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) hello 백 엔드에 들어오는 모든 요청을 처리할 수 있도록 메시지 처리기로 추가 합니다. 

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **AppBackend** 프로젝트를 클릭 하 여 **추가**, 클릭 **클래스**합니다. Hello 새 클래스 이름을 **AuthenticationTestHandler.cs**를 클릭 하 고 **추가** toogenerate hello 클래스입니다. 이 클래스를 사용 하 여 사용 되는 tooauthenticate 사용자 됩니다 *기본 인증* 을 간소화 합니다. 앱은 모든 인증 체계를 사용할 수 있습니다.
2. Hello 다음 추가 AuthenticationTestHandler.cs에서 `using` 문:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. AuthenticationTestHandler.cs, 대체 hello에에서 `AuthenticationTestHandler` 클래스 코드 다음 hello로 정의 합니다. 
   
    이 처리기는 hello 다음 세 가지 조건이 모두 참인 경우 hello 요청 권한이 부여 됩니다.
   
   * 포함 하는 hello 요청은 *권한 부여* 헤더입니다. 
   * 사용 하 여 hello 요청 *기본* 인증 합니다. 
   * 사용자 이름 문자열로 hello 및 hello 암호 문자열 hello는 동일한 문자열입니다.
     
     그렇지 않으면 hello 요청은 거부 됩니다. 이는 실제 인증 및 권한 부여 방법이 아닙니다. 이 자습서를 위한 매우 간단한 예제일 뿐입니다.
     
     Hello 요청 메시지 인증 되 고 hello에 권한을 부여 하는 경우 `AuthenticationTestHandler`, hello 기본 인증 사용자는 hello에 연결 된 toohello 현재 요청을 경우가 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)합니다. HttpContext hello에서 사용자 정보 (RegisterController) 다른 컨트롤러에서 사용할 이후 tooadd는 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello 알림 등록 요청이 있습니다.
     
       공용 클래스 AuthenticationTestHandler: DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **보안 정보**: hello `AuthenticationTestHandler` 클래스 true 인증을 제공 하지 않습니다. 기본 인증을 사용 하는 유일한 toomimic 이며 안전 하지 않습니다. 프로덕션 응용프로그램 및 서비스에 보안 인증 메커니즘을 구현해야 합니다.                
     > 
     > 
4. Hello 코드 hello의 hello 끝에 다음 추가 `Register` hello에 대 한 메서드 **App_Start/WebApiConfig.cs** 클래스 tooregister hello 메시지 처리기:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. 변경 내용을 저장합니다.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Hello WebAPI 백 엔드를 사용 하 여 알림 등록
이 섹션에서는 새 컨트롤러 toohello WebAPI 백 엔드 toohandle tooregister 사용자 및 장치에 대 한 hello 클라이언트 라이브러리를 사용 하 여 알림 허브에 대 한 알림 요청을 추가 합니다. hello 컨트롤러 hello 사용자가 인증 되 고 toohello HttpContext hello 하 여 연결 된에 대 한 사용자 태그를 추가 합니다 `AuthenticationTestHandler`합니다. hello 태그 hello 문자열 형식 갖습니다 `"username:<actual username>"`합니다.

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **AppBackend** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
2. Hello 왼쪽에 클릭 **온라인**, 검색 및 **Microsoft.Azure.NotificationHubs** hello에 **검색** 상자입니다.
3. Hello 결과 목록에서 클릭 **Microsoft Azure 알림 허브**, 클릭 하 고 **설치**합니다. Hello 설치를 완료 한 후 hello NuGet 패키지 관리자 창을 닫습니다.
   
    이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
4. 이제 알림 허브 사용 toosend 알림 hello 연결을 나타내는 새 클래스 파일을 사항을 만듭니다. 솔루션 탐색기 hello hello 마우스 오른쪽 단추로 클릭 **모델** 폴더를 클릭 하 여 **추가**, 클릭 **클래스**합니다. Hello 새 클래스 이름을 **Notifications.cs**, 클릭 **추가** toogenerate hello 클래스입니다. 
   
    ![][B6]
5. Hello 다음 추가 Notifications.cs에서 `using` hello 파일의 맨 위에 hello에 문:
   
        using Microsoft.Azure.NotificationHubs;
6. Hello 대체 `Notifications` 클래스 hello 다음과 같이 정의 하 고 알림 허브에 대 한 (모든 권한)으로 hello 연결 문자열을 사용 하는지 tooreplace hello 두 자리 표시자 확인 허브 이름 hello (//go.microsoft.com/fwlink/ [Azure 클래식 포털 ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. 다음으로 **RegisterController**라는 새 컨트롤러를 만듭니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **컨트롤러** 폴더를 클릭 한 다음 **추가**, 클릭 **컨트롤러**합니다. Hello 클릭 **Web API 2 컨트롤러-비어 있지** 항목을 선택한 다음 클릭 **추가**합니다. Hello 새 클래스 이름을 **RegisterController**, 클릭 하 고 **추가** 다시 toogenerate hello 컨트롤러입니다.
   
    ![][B7]
   
    ![][B8]
8. Hello 다음 추가 RegisterController.cs에서 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Hello hello 내부에서 코드를 다음 추가 `RegisterController` 클래스 정의 합니다. 이 코드를이 hello 사용자에 대 한 사용자 태그 toohello HttpContext 연결을 추가 합니다. hello 사용자가 인증 되 고 추가 된 hello 메시지 필터가 HttpContext toohello 연결 `AuthenticationTestHandler`합니다. 사용자 hello 선택적 검사 tooverify 권한이 추가할 수도 있습니다 tooregister hello에 대 한 태그를 요청 합니다.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. 변경 내용을 저장합니다.

## <a name="sending-notifications-from-hello-webapi-backend"></a>WebAPI 백 엔드 hello에서 보내는 알림
이 섹션에서는 클라이언트 장치 toosend hello ASP.NET WebAPI 백 엔드에에서 Azure 알림 허브 서비스 관리 라이브러리를 사용 하 여 hello username 태그에 따라 알림 방법을 노출 하는 새 컨트롤러를 추가 합니다.

1. **NotificationsController**라는 다른 새 컨트롤러를 만듭니다. Hello 만들기 hello를 만든 동일한 방식으로 **RegisterController** hello 이전 섹션에서.
2. Hello 다음 추가 NotificationsController.cs에서 `using` 문:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. 다음 메서드 toohello hello 추가 **NotificationsController** 클래스입니다.
   
    이 코드는 hello 서비스 PNS (플랫폼 알림)에 따라 알림 유형을 전송 `pns` 매개 변수입니다. 값의 hello `to_tag` 는 사용 되는 tooset hello *username* hello 메시지에 태그를 지정 합니다. 이 태그는 활성 알림 허브 등록의 사용자 이름 태그와 일치해야 합니다. hello 알림 메시지는 hello hello POST 요청 본문에서 가져오고 hello 대상 PNS에 대 한 서식이 지정 합니다. 
   
    서비스 PNS (플랫폼 알림)에 지원 되는 장치 tooreceive 알림을 사용 하 여는 hello에 따라 다른 형식을 사용 하 여 다른 알림은 지원 됩니다. 예를 들어 Windows 장치에서 다른 PNS에서 직접 지원되지 않는 [WNS로 알림](https://msdn.microsoft.com/library/windows/apps/br230849.aspx)을 사용할 수 있습니다. 백 엔드는 hello 장치 PNS에 지원 되는 알림 tooformat hello 알림이 필요 toosupport를 계획 합니다. 다음 hello 적절 한 송신 API를 사용 하 여 hello에 [NotificationHubClient 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. 키를 눌러 **F5** 지금까지 작업 toorun hello 응용 프로그램 및 tooensure hello 정확도 합니다. hello 앱에서는 웹 브라우저를 시작 하 고 hello ASP.NET 홈 페이지를 표시 해야 합니다. 

## <a name="publish-hello-new-webapi-backend"></a>게시할 새 WebAPI 백 엔드 hello
1. 순서 toomake이 응용 프로그램 tooan Azure 웹 사이트 배포에서는 이제는 모든 장치에서 액세스할 수 있게 합니다. Hello를 마우스 오른쪽 단추로 클릭 **AppBackend** 프로젝트를 마우스 선택 **게시**합니다.
2. **Microsoft Azure App Service**를 게시 대상으로 선택하고 **게시**를 클릭합니다. Hello 응용 프로그램 서비스 만들기 대화 상자를 사용 하면 Azure에서 모든 hello 필요한 Azure 리소스 toorun hello ASP.NET 웹 앱을 만들어 열립니다.

    ![][B15]
3. Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 Azure 계정을 선택 합니다. **유형 변경**을 클릭하고 **웹앱**을 선택합니다. Hello 유지 **웹 앱 이름은** 지정 및 선택 hello **구독**, **리소스 그룹**, 및 **앱 서비스 계획**합니다.  **만들기**를 클릭합니다.

4. Hello 메모 **사이트 URL** hello에 대 한 속성 **요약** 섹션. 다음 URL로 toothis 이라고 합니다 프로그램 *백 엔드 끝점* 이 자습서의 뒷부분에 나오는 합니다. **게시**를 클릭합니다.

5. Hello 마법사가 완료 되 면 hello ASP.NET 웹 응용 프로그램 tooAzure 게시 하 고 실행 하는 경우 hello hello 기본 브라우저에서 응용 프로그램입니다.  응용 프로그램을 Azure App Services에서 볼 수 있습니다.

hello URL 형식 http://<app_name>.azurewebsites.net hello 사용 하 여 이전에 지정한는 hello 웹 응용 프로그램 이름을 사용 합니다.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
