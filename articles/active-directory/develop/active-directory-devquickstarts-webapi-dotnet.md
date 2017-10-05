---
title: "Azure AD .NET Web API 시작 | Microsoft Docs"
description: "인증 및 권한 부여를 위해 Azure AD와 통합되는 .NET MVC Web API를 빌드하는 방법입니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="9368f-103">Azure AD에서 전달자 토큰을 사용하여 Web API 보호</span><span class="sxs-lookup"><span data-stu-id="9368f-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="9368f-104">보호된 리소스에 액세스할 수 있는 응용 프로그램을 빌드하는 경우 허가되지 않은 액세스로부터 해당 리소스를 보호하는 방법을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="9368f-105">Azure Active Directory(Azure AD)를 사용하면 몇 개의 코드 줄만으로 단순하고 간편하게 OAuth 2.0 Bearer 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="9368f-106">ASP.NET 웹앱에서는 .NET Framework 4.5에 포함된 Microsoft에서 구현한 커뮤니티 기반 OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="9368f-107">여기서는 "할 일 목록" 웹 API를 작성하는 데 OWIN을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="9368f-108">보호되는 API를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="9368f-109">웹 API 호출에 유효한 액세스 토큰이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="9368f-110">To Do List API를 빌드하려면 다음을 먼저 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="9368f-111">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="9368f-112">OWIN 인증 파이프라인을 사용하도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="9368f-113">Web API를 호출하도록 클라이언트 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="9368f-114">시작하려면 [앱 기본 사항을 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="9368f-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="9368f-115">각 샘플은 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="9368f-116">응용 프로그램을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="9368f-117">테넌트가 아직 없는 경우 [가져오는 방법을 알아봅니다](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9368f-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="9368f-118">1단계: Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="9368f-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="9368f-119">응용 프로그램 보안을 유지하려면 먼저 테넌트에서 응용 프로그램을 만들고 몇 가지 중요 정보로 Azure AD를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="9368f-120">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9368f-121">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-121">On the top bar, click your account.</span></span> <span data-ttu-id="9368f-122">**디렉터리** 목록에서 응용 프로그램을 등록할 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="9368f-123">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="9368f-124">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="9368f-125">프롬프트에 따라 새 **웹 응용 프로그램 및/또는 Web API**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="9368f-126">**이름**은 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-126">**Name** describes your application to users.</span></span> <span data-ttu-id="9368f-127">**To Do List Service**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="9368f-128">**리디렉션 Uri**는 Azure AD가 앱이 요청한 토큰을 반환하는 데 사용하는 구성표 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="9368f-129">이 값으로 `https://localhost:44321/` 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="9368f-130">응용 프로그램에 대한 **설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="9368f-131">테넌트별 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="9368f-132">예를 들어 `https://contoso.onmicrosoft.com/TodoListService`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="9368f-133">구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-133">Save the configuration.</span></span> <span data-ttu-id="9368f-134">잠시 후에 클라이언트 응용 프로그램을 등록해야 하므로 포털을 열어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="9368f-135">2단계: OWIN 인증 파이프라인을 사용하도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="9368f-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="9368f-136">들어오는 요청 및 토큰 유효성을 검사하려면 Azure AD와 통신하도록 응용 프로그램을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="9368f-137">시작하려면 솔루션을 열고 패키지 관리자 콘솔을 사용하여 OWIN 미들웨어 NuGet 패키지를 TodoListService 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="9368f-138">OWIN Startup 클래스를 `Startup.cs`라는 TodoListService 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="9368f-139">프로젝트를 마우스 오른쪽 단추로 클릭하고 **새 항목** **추가** > 를 선택한 다음 **OWIN**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="9368f-140">OWIN 미들웨어는 앱이 시작되면 `Configuration(…)` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="9368f-141">클래스 선언을 `public partial class Startup`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="9368f-142">다른 파일에서 이 클래스의 일부를 이미 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="9368f-143">`Configuration(…)` 메서드에서 `ConfgureAuth(…)`를 호출하여 웹앱에 대한 인증을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="9368f-144">`App_Start\Startup.Auth.cs` 파일을 열고 `ConfigureAuth(…)` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="9368f-145">`WindowsAzureActiveDirectoryBearerAuthenticationOptions`에 제공하는 매개 변수는 앱이 Azure AD와 통신하기 위한 좌표로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="9368f-146">이제 `[Authorize]` 특성을 사용하여 JSON Web Token(JWT) 전달자 인증으로 컨트롤러 및 작업을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="9368f-147">authorize 태그를 사용하여 `Controllers\TodoListController.cs` 클래스를 데코레이팅합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="9368f-148">이렇게 하면 사용자는 해당 페이지에 액세스하기 전에 강제로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="9368f-149">권한 있는 호출자가 `TodoListController` API 중 하나를 호출하면 작업은 호출자에 대한 정보에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="9368f-150">OWIN은 `ClaimsPrincpal` 개체를 통해 전달자 토큰 내의 클레임에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="9368f-151">웹 API에 대한 일반적인 요구 사항은 토큰에 있는 "범위"를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="9368f-152">이렇게 하여 사용자가 To Do List Service에 액세스하는 데 필요한 권한에 동의했음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="9368f-153">TodoListService 프로젝트의 루트에서 `web.config` 파일을 열고 `<appSettings>` 섹션에 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="9368f-154">`ida:Tenant`는 Azure AD 테넌트의 이름(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="9368f-155">`ida:Audience`는 Azure 포털에 입력한 응용 프로그램의 앱 ID URI입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="9368f-156">3단계: 클라이언트 응용 프로그램 구성 및 서비스 실행</span><span class="sxs-lookup"><span data-stu-id="9368f-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="9368f-157">To Do List Service가 작동하는 것을 보려면 먼저 Azure AD에서 토큰을 가져오고 서비스를 호출할 수 있도록 To Do List Client를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="9368f-158">[Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9368f-159">Azure AD 테넌트에 새 응용 프로그램을 만들고 결과 프롬프트에서 **네이티브 클라이언트 응용 프로그램** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="9368f-160">**이름**은 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="9368f-161">**리디렉션 URI** 값으로 `http://TodoListClient/`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="9368f-162">등록을 완료한 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="9368f-163">이 값은 다음 단계에서 필요하므로 응용 프로그램 페이지에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="9368f-164">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="9368f-165">To Do List Service를 찾은 후 선택하고 **위임된 사용 권한**에서 **TodoListService 액세스** 사용 권한을 추가한 다음 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="9368f-166">Visual Studio의 TodoListClient 프로젝트에서 `App.config`를 열고 `<appSettings>` 섹션에 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="9368f-167">`ida:Tenant`는 Azure AD 테넌트의 이름(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="9368f-168">`ida:ClientId`는 Azure Portal에서 복사한 앱 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="9368f-169">`todo:TodoListResourceId`는 Azure Portal에 입력한 To Do List Service 응용 프로그램의 앱 ID URI입니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9368f-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9368f-170">Next steps</span></span>
<span data-ttu-id="9368f-171">마지막으로, 각 프로젝트를 정리하고 빌드한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="9368f-172">새 사용자를 아직 만들지 않았으면 *.onmicrosoft.com 도메인을 사용하여 테넌트에 새 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="9368f-173">해당 사용자로 To Do List 클라이언트에 로그인하고 사용자의 To Do List에 일부 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="9368f-174">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="9368f-175">이제 더 많은 ID 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9368f-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
