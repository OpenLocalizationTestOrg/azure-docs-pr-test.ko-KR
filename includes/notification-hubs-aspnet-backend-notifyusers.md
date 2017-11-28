## <a name="create-the-webapi-project"></a><span data-ttu-id="05c5a-101">WebAPI 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="05c5a-101">Create the WebAPI Project</span></span>
<span data-ttu-id="05c5a-102">새 ASP.NET WebAPI 백 엔드는 이후 섹션에서 만들어지며 다음 세 가지 주요 목적이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="05c5a-103">**클라이언트 인증**: 나중에 클라이언트 요청을 인증하고 사용자를 요청과 연결하는 메시지 처리기가 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="05c5a-104">**클라이언트 알림 등록**: 나중에 클라이언트 장치에서 알림을 받을 수 있도록 새 등록을 처리하는 컨트롤러를 추가할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="05c5a-105">인증된 사용자 이름은 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx)로 등록에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="05c5a-106">**클라이언트로 알림 보내기**: 나중에 사용자가 태그와 연결된 장치 및 클라이언트로 보안 푸시를 트리거할 수 있는 방법을 제공하는 컨트롤러를 추가할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="05c5a-107">다음 단계에서는 새 ASP.NET WebAPI 백 엔드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="05c5a-108">Visual Studio 2015 이하를 사용하는 경우 이 자습서를 시작하기 전에 최신 버전의 NuGet 패키지 관리자를 설치했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="05c5a-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="05c5a-109">확인하려면 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-109">To check, start Visual Studio.</span></span> <span data-ttu-id="05c5a-110">**도구** 메뉴에서 **확장 및 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="05c5a-111">사용하는 Visual Studio 버전의 **NuGet 패키지 관리자**를 검색하고, 현재 버전이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="05c5a-112">그렇지 않은 경우 제거한 다음, NuGet 패키지 관리자를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="05c5a-113">웹 사이트 배포를 위해 Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/)를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="05c5a-114">Visual Studio 또는 Visual Studio Express를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="05c5a-115">**서버 탐색기**를 클릭하고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="05c5a-116">계정에 웹 사이트 리소스를 만들려면 Visual Studio에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="05c5a-117">Visual Studio에서 **파일**을 클릭한 후 **새로 만들기**, **프로젝트**를 클릭하고 **템플릿**, **Visual C#**을 확장한 다음 **웹** 및 **ASP.NET 웹 응용프로그램**을 클릭하고 **AppBackend**라는 이름을 입력한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="05c5a-118">**새 ASP.NET 프로젝트** 대화 상자에서 **웹 API**를 클릭한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="05c5a-119">**Microsoft Azure Web App 구성** 대화 상자에서 구독 및 이미 만든 **App Service 계획**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="05c5a-120">**새 앱 서비스 계획 만들기**를 선택하고 대화 상자에서 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="05c5a-121">이 자습서를 위해 데이터베이스는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="05c5a-122">앱 서비스 계획을 선택한 후 **확인**을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="05c5a-123">WebAPI 백 엔드에 클라이언트 인증</span><span class="sxs-lookup"><span data-stu-id="05c5a-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="05c5a-124">이 섹션에서는 새 백 엔드에 대해 **AuthenticationTestHandler** 라는 새 메시지 처리기 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="05c5a-125">이 클래스는 [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx)에서 파생되며 백 엔드로 들어오는 모든 요청을 처리할 수 있도록 메시지 처리기로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="05c5a-126">솔루션 탐색기에서 **AppBackend** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="05c5a-127">새 클래스의 이름을 **AuthenticationTestHandler.cs**로 지정하고 **추가**를 클릭하여 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="05c5a-128">이 클래스는 간단히 하기 위해 *기본 인증*을 사용하여 사용자를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="05c5a-129">앱은 모든 인증 체계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="05c5a-130">AuthenticationTestHandler.cs에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="05c5a-131">AuthenticationTestHandler.cs에서 `AuthenticationTestHandler` 클래스 정의를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="05c5a-132">이 처리기는 다음 세 가지 조건이 모두 충족될 때 요청을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="05c5a-133">요청에 *Authorization* 헤더가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="05c5a-134">요청이 *기본* 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="05c5a-135">사용자 이름 문자열과 암호 문자열은 동일한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="05c5a-136">그렇지 않으면 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="05c5a-137">이는 실제 인증 및 권한 부여 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="05c5a-138">이 자습서를 위한 매우 간단한 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="05c5a-139">요청 메시지가 `AuthenticationTestHandler`에 의해 인증되고 권한이 부여되면 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)의 현재 요청에 기본 인증 사용자가 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="05c5a-140">HttpContext의 사용자 정보는 나중에 다른 컨트롤러(RegisterController)에서 알림 등록 요청에 [태그](https://msdn.microsoft.com/library/azure/dn530749.aspx)를 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="05c5a-141">공용 클래스 AuthenticationTestHandler: DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="05c5a-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach the new principal object to the current HttpContext object
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
       <span data-ttu-id="05c5a-142">}</span><span class="sxs-lookup"><span data-stu-id="05c5a-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="05c5a-143">**보안 정보**: `AuthenticationTestHandler` 클래스는 진정한 의미의 인증을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="05c5a-144">이 클래스는 기본 인증과 비슷한 동작을 하고 보안이 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="05c5a-145">프로덕션 응용프로그램 및 서비스에 보안 인증 메커니즘을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="05c5a-146">**App_Start/WebApiConfig.cs** 클래스의 `Register` 메서드 끝에 다음 코드를 추가하여 메시지 처리기를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="05c5a-147">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="05c5a-148">WebAPI 백 엔드를 사용하여 알림 등록</span><span class="sxs-lookup"><span data-stu-id="05c5a-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="05c5a-149">이 섹션에서는 알림 허브에 클라이언트 라이브러리를 사용하여 알림을 위한 사용자 및 장치 등록 요청을 처리하는 새 컨트롤러를 WebAPI 백 엔드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="05c5a-150">이 컨트롤러는 `AuthenticationTestHandler`에 의해 인증되고 HttpContext에 연결된 사용자에 대한 사용자 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="05c5a-151">태그의 문자열 형식은 `"username:<actual username>"`입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="05c5a-152">솔루션 탐색기에서 **AppBackend**프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="05c5a-153">왼쪽에서 **온라인**을 클릭하고 **Search** 상자에서 **Microsoft.Azure.NotificationHubs**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="05c5a-154">결과 목록에서 **Microsoft Azure Notification Hubs**를 클릭한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="05c5a-155">설치를 완료한 다음, NuGet 패키지 관리자 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="05c5a-156">그러면 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 패키지</a>를 사용하는 Azure Notification Hubs SDK에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="05c5a-157">이제 알림을 보내는 데 사용되는 알림 허브와의 연결을 나타내는 새 클래스 파일을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="05c5a-158">솔루션 탐색기에서 **Models** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="05c5a-159">새 클래스 이름을 **Notifications.cs**로 지정한 후 **추가**를 클릭하여 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="05c5a-160">Notifications.cs에서 파일의 맨 위에 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="05c5a-161">`Notifications` 클래스 정의를 다음으로 바꾸고 두 개의 자리 표시자를 알림 허브에 대한 연결 문자열(모든 권한 사용) 및 허브 이름( [Azure 클래식 포털](http://manage.windowsazure.com)에서 제공)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="05c5a-162">다음으로 **RegisterController**라는 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="05c5a-163">솔루션 탐색기에서 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가**와 **컨트롤러**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="05c5a-164">**웹 API 2 컨트롤러 -- 비어 있음** 항목을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="05c5a-165">새 클래스 이름을 **RegisterController**로 지정한 다음 **추가**를 다시 클릭하여 컨트롤러를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="05c5a-166">RegiterController.cs에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="05c5a-167">다음 코드를 `RegisterController` 클래스 정의 내에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="05c5a-168">이 코드에서 HttpContext에 연결된 사용자에 대한 사용자 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="05c5a-169">이 사용자는 추가한 메시지 필터 `AuthenticationTestHandler`에 의해 인증되고 HttpContext에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="05c5a-170">또한 선택적인 검사를 추가하여 사용자에게 요청된 태그에 등록할 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at the specified id
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
   
            // add check if user is allowed to add these tags
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
10. <span data-ttu-id="05c5a-171">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="05c5a-172">WebAPI 백 엔드에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="05c5a-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="05c5a-173">이 섹션에서는 클라이언트 장치가 ASP.NET WebAPI 백 엔드에서 Azure Notification Hubs 서비스  관리 라이브러리를 사용하여 사용자 이름 태그에 따라 알림을 보낼 수 있는 방법을 제공하는 새 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="05c5a-174">**NotificationsController**라는 다른 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="05c5a-175">이전 섹션에서 **RegisterController**를 만들 때와 동일한 방법으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="05c5a-176">NotificationsController.cs에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="05c5a-177">**NotificationsController** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="05c5a-178">이 코드는 PNS(Platform Notification Service) `pns` 매개 변수를 기반으로 알림 유형을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="05c5a-179">`to_tag` 값은 메시지에서 *사용자 이름* 태그를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="05c5a-180">이 태그는 활성 알림 허브 등록의 사용자 이름 태그와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="05c5a-181">알림 메시지는 POST 요청의 본문에서 가져오고 대상 PNS에 맞게 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="05c5a-182">알림을 수신하기 위해 지원되는 장치가 사용하는 플랫폼 알림 서비스(PNS)에 따라 다른 형식을 사용하여 다양한 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="05c5a-183">예를 들어 Windows 장치에서 다른 PNS에서 직접 지원되지 않는 [WNS로 알림](https://msdn.microsoft.com/library/windows/apps/br230849.aspx)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="05c5a-184">따라서 백 엔드는 알림을 지원하려는 장치의 PNS에 지원되는 알림으로 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="05c5a-185">그런 다음 [NotificationHubClient 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="05c5a-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="05c5a-186">**F5** 키를 눌러 응용프로그램을 실행하고 지금까지 작업의 정확성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="05c5a-187">앱은 웹 브라우저를 시작하고 ASP.NET 홈페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="05c5a-188">새 WebAPI 백엔드 게시</span><span class="sxs-lookup"><span data-stu-id="05c5a-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="05c5a-189">이제 모든 장치에서 액세스할 수 있도록 이 앱을 Azure 웹 사이트에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="05c5a-190">**AppBackend** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="05c5a-191">**Microsoft Azure App Service**를 게시 대상으로 선택하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="05c5a-192">그러면 App Service 만들기 대화 상자가 열리고 Azure에서 ASP.NET 웹앱을 실행하는 데 필요한 모든 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="05c5a-193">**App Service 만들기** 대화 상자에서 Azure 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="05c5a-194">**유형 변경**을 클릭하고 **웹앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="05c5a-195">주어진 **웹앱 이름**을 유지하고 **구독**, **리소스 그룹**, **App Service 계획**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="05c5a-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-196">Click **Create**.</span></span>

4. <span data-ttu-id="05c5a-197">**요약** 섹션의 **사이트 URL** 속성을 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="05c5a-198">이 자습서의 뒷부분에서 이 URL을 *백 엔드 끝점* 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="05c5a-199">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-199">Click **Publish**.</span></span>

5. <span data-ttu-id="05c5a-200">마법사가 완료되면 Azure에 ASP.NET 웹앱을 게시한 다음 기본 브라우저에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="05c5a-201">응용 프로그램을 Azure App Services에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="05c5a-202">URL은 http://<app_name>.azurewebsites.net 형식으로 이전에 지정한 웹앱 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05c5a-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
