## <a name="create-hello-webapi-project"></a><span data-ttu-id="a29b0-101">Hello WebAPI 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a29b0-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="a29b0-102">새 ASP.NET WebAPI 백 엔드 hello 섹션에 만들고 3 가지 기본 목적을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="a29b0-103">**클라이언트 인증**: 이후 tooauthenticate 클라이언트 요청 및 연결 hello 사용자에 게 hello 요청이 메시지 처리기 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="a29b0-104">**클라이언트 알림 등록**: 나중 클라이언트 장치 tooreceive 알림을 컨트롤러 toohandle 새 등록 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="a29b0-105">hello 인증 된 사용자 이름이 자동으로 추가 됩니다 toohello로 등록 하는 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="a29b0-106">**알림 tooClients 보내기**: 나중에 추가 합니다 컨트롤러 tooprovide 사용자 tootrigger 보안 밀어넣기 toodevices 하는 방법 및 hello 태그와 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="a29b0-107">단계를 수행 하는 hello toocreate 새 ASP.NET WebAPI 백 엔드 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a29b0-108">이 자습서를 시작 하기 전에 이전, 또는 Visual Studio 2015를 사용 하는 경우 hello 최신 버전의 hello NuGet 패키지 관리자를 설치 했는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a29b0-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="a29b0-109">toocheck, Visual Studio 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="a29b0-110">Hello에서 **도구** 메뉴를 클릭 하 여 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="a29b0-111">검색할 **NuGet 패키지 관리자** hello 최신 버전의 경우 할 버전의 Visual Studio 및 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a29b0-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="a29b0-112">그렇지 않은 경우에, 제거한 다음 hello NuGet 패키지 관리자를 다시 설치 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a29b0-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="a29b0-113">Hello Visual Studio를 설치 했는지 확인 [Azure SDK](https://azure.microsoft.com/downloads/) 웹 사이트 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="a29b0-114">Visual Studio 또는 Visual Studio Express를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="a29b0-115">클릭 **서버 탐색기** tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="a29b0-116">Visual Studio toocreate hello 웹 사이트 리소스 계정에 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="a29b0-117">Visual Studio에서 클릭 **파일**, 클릭 **새로**, 다음 **프로젝트**, 확장 **템플릿**, **Visual C#**, 클릭 **웹** 및 **ASP.NET 웹 응용 프로그램**, 형식 hello 이름 **AppBackend**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="a29b0-118">Hello에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **웹 API**, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="a29b0-119">Hello에 **Microsoft Azure 웹 앱 구성** 대화 상자에서 구독을 선택 및 **앱 서비스 계획** 이미 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="a29b0-120">선택할 수도 있습니다 **새 앱 서비스 계획 만들기** hello 대화 상자에서 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="a29b0-121">이 자습서를 위해 데이터베이스는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="a29b0-122">앱 서비스 계획을 선택 하면 클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a29b0-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="a29b0-123">인증 클라이언트 toohello WebAPI 백 엔드</span><span class="sxs-lookup"><span data-stu-id="a29b0-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="a29b0-124">이 섹션에서는 라는 새 메시지 처리기 클래스가 만들어집니다 **AuthenticationTestHandler** hello 새 백 엔드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="a29b0-125">이 클래스에서 파생 된 [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) hello 백 엔드에 들어오는 모든 요청을 처리할 수 있도록 메시지 처리기로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="a29b0-126">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **AppBackend** 프로젝트를 클릭 하 여 **추가**, 클릭 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="a29b0-127">Hello 새 클래스 이름을 **AuthenticationTestHandler.cs**를 클릭 하 고 **추가** toogenerate hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="a29b0-128">이 클래스를 사용 하 여 사용 되는 tooauthenticate 사용자 됩니다 *기본 인증* 을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="a29b0-129">앱은 모든 인증 체계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="a29b0-130">Hello 다음 추가 AuthenticationTestHandler.cs에서 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="a29b0-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="a29b0-131">AuthenticationTestHandler.cs, 대체 hello에에서 `AuthenticationTestHandler` 클래스 코드 다음 hello로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="a29b0-132">이 처리기는 hello 다음 세 가지 조건이 모두 참인 경우 hello 요청 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="a29b0-133">포함 하는 hello 요청은 *권한 부여* 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="a29b0-134">사용 하 여 hello 요청 *기본* 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="a29b0-135">사용자 이름 문자열로 hello 및 hello 암호 문자열 hello는 동일한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="a29b0-136">그렇지 않으면 hello 요청은 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="a29b0-137">이는 실제 인증 및 권한 부여 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="a29b0-138">이 자습서를 위한 매우 간단한 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="a29b0-139">Hello 요청 메시지 인증 되 고 hello에 권한을 부여 하는 경우 `AuthenticationTestHandler`, hello 기본 인증 사용자는 hello에 연결 된 toohello 현재 요청을 경우가 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="a29b0-140">HttpContext hello에서 사용자 정보 (RegisterController) 다른 컨트롤러에서 사용할 이후 tooadd는 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello 알림 등록 요청이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="a29b0-141">공용 클래스 AuthenticationTestHandler: DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="a29b0-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="a29b0-142">}</span><span class="sxs-lookup"><span data-stu-id="a29b0-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="a29b0-143">**보안 정보**: hello `AuthenticationTestHandler` 클래스 true 인증을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="a29b0-144">기본 인증을 사용 하는 유일한 toomimic 이며 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="a29b0-145">프로덕션 응용프로그램 및 서비스에 보안 인증 메커니즘을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="a29b0-146">Hello 코드 hello의 hello 끝에 다음 추가 `Register` hello에 대 한 메서드 **App_Start/WebApiConfig.cs** 클래스 tooregister hello 메시지 처리기:</span><span class="sxs-lookup"><span data-stu-id="a29b0-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="a29b0-147">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="a29b0-148">Hello WebAPI 백 엔드를 사용 하 여 알림 등록</span><span class="sxs-lookup"><span data-stu-id="a29b0-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="a29b0-149">이 섹션에서는 새 컨트롤러 toohello WebAPI 백 엔드 toohandle tooregister 사용자 및 장치에 대 한 hello 클라이언트 라이브러리를 사용 하 여 알림 허브에 대 한 알림 요청을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="a29b0-150">hello 컨트롤러 hello 사용자가 인증 되 고 toohello HttpContext hello 하 여 연결 된에 대 한 사용자 태그를 추가 합니다 `AuthenticationTestHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="a29b0-151">hello 태그 hello 문자열 형식 갖습니다 `"username:<actual username>"`합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="a29b0-152">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **AppBackend** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a29b0-153">Hello 왼쪽에 클릭 **온라인**, 검색 및 **Microsoft.Azure.NotificationHubs** hello에 **검색** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="a29b0-154">Hello 결과 목록에서 클릭 **Microsoft Azure 알림 허브**, 클릭 하 고 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="a29b0-155">Hello 설치를 완료 한 후 hello NuGet 패키지 관리자 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="a29b0-156">이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="a29b0-157">이제 알림 허브 사용 toosend 알림 hello 연결을 나타내는 새 클래스 파일을 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="a29b0-158">솔루션 탐색기 hello hello 마우스 오른쪽 단추로 클릭 **모델** 폴더를 클릭 하 여 **추가**, 클릭 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="a29b0-159">Hello 새 클래스 이름을 **Notifications.cs**, 클릭 **추가** toogenerate hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="a29b0-160">Hello 다음 추가 Notifications.cs에서 `using` hello 파일의 맨 위에 hello에 문:</span><span class="sxs-lookup"><span data-stu-id="a29b0-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="a29b0-161">Hello 대체 `Notifications` 클래스 hello 다음과 같이 정의 하 고 알림 허브에 대 한 (모든 권한)으로 hello 연결 문자열을 사용 하는지 tooreplace hello 두 자리 표시자 확인 허브 이름 hello (//go.microsoft.com/fwlink/ [Azure 클래식 포털 ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="a29b0-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="a29b0-162">다음으로 **RegisterController**라는 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="a29b0-163">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **컨트롤러** 폴더를 클릭 한 다음 **추가**, 클릭 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="a29b0-164">Hello 클릭 **Web API 2 컨트롤러-비어 있지** 항목을 선택한 다음 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="a29b0-165">Hello 새 클래스 이름을 **RegisterController**, 클릭 하 고 **추가** 다시 toogenerate hello 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="a29b0-166">Hello 다음 추가 RegisterController.cs에서 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="a29b0-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="a29b0-167">Hello hello 내부에서 코드를 다음 추가 `RegisterController` 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="a29b0-168">이 코드를이 hello 사용자에 대 한 사용자 태그 toohello HttpContext 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="a29b0-169">hello 사용자가 인증 되 고 추가 된 hello 메시지 필터가 HttpContext toohello 연결 `AuthenticationTestHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="a29b0-170">사용자 hello 선택적 검사 tooverify 권한이 추가할 수도 있습니다 tooregister hello에 대 한 태그를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="a29b0-171">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="a29b0-172">WebAPI 백 엔드 hello에서 보내는 알림</span><span class="sxs-lookup"><span data-stu-id="a29b0-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="a29b0-173">이 섹션에서는 클라이언트 장치 toosend hello ASP.NET WebAPI 백 엔드에에서 Azure 알림 허브 서비스 관리 라이브러리를 사용 하 여 hello username 태그에 따라 알림 방법을 노출 하는 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="a29b0-174">**NotificationsController**라는 다른 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="a29b0-175">Hello 만들기 hello를 만든 동일한 방식으로 **RegisterController** hello 이전 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="a29b0-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="a29b0-176">Hello 다음 추가 NotificationsController.cs에서 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="a29b0-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="a29b0-177">다음 메서드 toohello hello 추가 **NotificationsController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="a29b0-178">이 코드는 hello 서비스 PNS (플랫폼 알림)에 따라 알림 유형을 전송 `pns` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="a29b0-179">값의 hello `to_tag` 는 사용 되는 tooset hello *username* hello 메시지에 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="a29b0-180">이 태그는 활성 알림 허브 등록의 사용자 이름 태그와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="a29b0-181">hello 알림 메시지는 hello hello POST 요청 본문에서 가져오고 hello 대상 PNS에 대 한 서식이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="a29b0-182">서비스 PNS (플랫폼 알림)에 지원 되는 장치 tooreceive 알림을 사용 하 여는 hello에 따라 다른 형식을 사용 하 여 다른 알림은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="a29b0-183">예를 들어 Windows 장치에서 다른 PNS에서 직접 지원되지 않는 [WNS로 알림](https://msdn.microsoft.com/library/windows/apps/br230849.aspx)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="a29b0-184">백 엔드는 hello 장치 PNS에 지원 되는 알림 tooformat hello 알림이 필요 toosupport를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="a29b0-185">다음 hello 적절 한 송신 API를 사용 하 여 hello에 [NotificationHubClient 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="a29b0-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="a29b0-186">키를 눌러 **F5** 지금까지 작업 toorun hello 응용 프로그램 및 tooensure hello 정확도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="a29b0-187">hello 앱에서는 웹 브라우저를 시작 하 고 hello ASP.NET 홈 페이지를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="a29b0-188">게시할 새 WebAPI 백 엔드 hello</span><span class="sxs-lookup"><span data-stu-id="a29b0-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="a29b0-189">순서 toomake이 응용 프로그램 tooan Azure 웹 사이트 배포에서는 이제는 모든 장치에서 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="a29b0-190">Hello를 마우스 오른쪽 단추로 클릭 **AppBackend** 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="a29b0-191">**Microsoft Azure App Service**를 게시 대상으로 선택하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="a29b0-192">Hello 응용 프로그램 서비스 만들기 대화 상자를 사용 하면 Azure에서 모든 hello 필요한 Azure 리소스 toorun hello ASP.NET 웹 앱을 만들어 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="a29b0-193">Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 Azure 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="a29b0-194">**유형 변경**을 클릭하고 **웹앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="a29b0-195">Hello 유지 **웹 앱 이름은** 지정 및 선택 hello **구독**, **리소스 그룹**, 및 **앱 서비스 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="a29b0-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-196">Click **Create**.</span></span>

4. <span data-ttu-id="a29b0-197">Hello 메모 **사이트 URL** hello에 대 한 속성 **요약** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a29b0-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="a29b0-198">다음 URL로 toothis 이라고 합니다 프로그램 *백 엔드 끝점* 이 자습서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="a29b0-199">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-199">Click **Publish**.</span></span>

5. <span data-ttu-id="a29b0-200">Hello 마법사가 완료 되 면 hello ASP.NET 웹 응용 프로그램 tooAzure 게시 하 고 실행 하는 경우 hello hello 기본 브라우저에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="a29b0-201">응용 프로그램을 Azure App Services에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="a29b0-202">hello URL 형식 http://<app_name>.azurewebsites.net hello 사용 하 여 이전에 지정한는 hello 웹 응용 프로그램 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29b0-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
