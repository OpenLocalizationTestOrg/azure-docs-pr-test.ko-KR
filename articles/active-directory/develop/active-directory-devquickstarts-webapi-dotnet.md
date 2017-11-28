---
title: "aaaAzure AD.NET 웹 API 시작 | Microsoft Docs"
description: "어떻게 toobuild.NET MVC 웹 API는 Azure AD와 통합 인증 및 권한 부여에 대 한 합니다."
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
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="d722a-103">Azure AD에서 전달자 토큰을 사용하여 Web API 보호</span><span class="sxs-lookup"><span data-stu-id="d722a-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d722a-104">Tooknow 필요한 tooprotected 리소스 액세스를 제공 하는 응용 프로그램을 빌드하는 경우 어떻게 tooprevent 초래 toothose 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="d722a-105">Azure Active Directory (Azure AD)을 사용 하면 간단 하 고 간단 하 게 toohelp 단 몇 줄의 코드 함께 OAuth 2.0 전달자 액세스 토큰을 사용 하 여 web API를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="d722a-106">ASP.NET 웹 응용 프로그램에서 hello 커뮤니티 기반 OWIN 미들웨어의.NET Framework 4.5에 포함 된 Microsoft 구현 hello를 사용 하 여이 보호를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="d722a-107">여기에서는 "tooDo 목록" web API OWIN toobuild입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="d722a-108">보호되는 API를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="d722a-109">Hello 웹 API 호출에 유효한 액세스 토큰이 포함 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="d722a-110">toobuild hello tooDo 목록 API를 먼저 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="d722a-111">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="d722a-112">Hello 앱 toouse hello OWIN 인증 파이프라인을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="d722a-113">클라이언트 응용 프로그램 toocall hello 웹 API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="d722a-114">시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d722a-115">각 샘플은 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="d722a-116">또한 해야 어떤 tooregister에 Azure AD 테 넌 트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="d722a-117">없는 경우 하나 이미 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="d722a-118">1단계: Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="d722a-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="d722a-119">toohelp secure 응용 프로그램에 먼저 테 넌 트에 응용 프로그램 toocreate 필요 하 고 Azure AD 몇 가지 중요 한 내용을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="d722a-120">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d722a-121">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-121">On hello top bar, click your account.</span></span> <span data-ttu-id="d722a-122">Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="d722a-123">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="d722a-124">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="d722a-125">Hello 화면에 따라 수행 하 고 새 **웹 응용 프로그램 및/또는 Web API**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="d722a-126">**이름** 응용 프로그램 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="d722a-127">입력 **tooDo 목록 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="d722a-128">**리디렉션 Uri** 는 구성표 및 문자열 조합 tooreturn 응용 프로그램을 요청 했습니다 모든 토큰을 사용 하 여 Azure AD입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="d722a-129">이 값으로 `https://localhost:44321/` 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="d722a-130">Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="d722a-131">테넌트별 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="d722a-132">예를 들어 `https://contoso.onmicrosoft.com/TodoListService`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="d722a-133">Hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-133">Save hello configuration.</span></span> <span data-ttu-id="d722a-134">또한 필요 하므로 tooregister 클라이언트 응용 프로그램이 곧 hello 포털을 열어를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="d722a-135">2 단계: hello 앱 toouse hello OWIN 인증 파이프라인 설정</span><span class="sxs-lookup"><span data-stu-id="d722a-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="d722a-136">toovalidate 들어오는 요청 및 토큰을 Azure AD와 응용 프로그램 toocommunicate 프로그램 tooset이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="d722a-137">toobegin, hello 솔루션을 열고 hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello TodoListService 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="d722a-138">OWIN 시작 클래스 toohello TodoListService 프로젝트 라는 추가 `Startup.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d722a-139">마우스 오른쪽 단추로 클릭 hello 프로젝트를 선택 **추가** > **새 항목**, 검색할 **OWIN**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="d722a-140">hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="d722a-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="d722a-141">Hello 클래스 선언에도 변경`public partial class Startup`합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="d722a-142">다른 파일에서 이 클래스의 일부를 이미 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="d722a-143">Hello에 `Configuration(…)` 메서드를 너무 호출할`ConfgureAuth(…)` tooset 웹 앱에 대 한 인증을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="d722a-144">파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(…)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d722a-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="d722a-145">매개 변수에서 제공 하는 hello `WindowsAzureActiveDirectoryBearerAuthenticationOptions` 좌표 Azure AD와 앱 toocommunicate 프로그램에 대 한 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

5. <span data-ttu-id="d722a-146">에서는 이제 `[Authorize]` 특성 toohelp 컨트롤러와 JSON 웹 토큰 (JWT) 전달자 인증을 사용 하 여 작업을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="d722a-147">Hello 데코레이팅 `Controllers\TodoListController.cs` authorize 태그를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="d722a-148">이렇게 하면 해당 페이지에 액세스 하기 전에 hello 사용자 toosign에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="d722a-149">하면 권한 있는 발신자를 성공적으로 중 하나를 호출 hello `TodoListController` Api hello 작업 해야에 액세스할 수 tooinformation hello 호출자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="d722a-150">OWIN hello 통해 hello 전달자 토큰에 대 한 액세스 toohello 클레임을 제공 `ClaimsPrincpal` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="d722a-151">웹 Api에 대 한 일반적인 요구 사항은 toovalidate hello "범위" hello 토큰에 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="d722a-152">이렇게 하면 해당 hello 사용자가 동의 toohello 권한이 필요한 tooaccess hello tooDo 목록 서비스.</span><span class="sxs-lookup"><span data-stu-id="d722a-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="d722a-153">열기 hello `web.config` hello TodoListService 프로젝트의 hello 루트에서 파일을 hello에 구성 값을 입력 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="d722a-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="d722a-154">`ida:Tenant`Azure AD 테 넌 트-예를 들어 contoso.onmicrosoft.com hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d722a-155">`ida:Audience`hello hello Azure 포털에에서 입력 된 hello 응용 프로그램의 앱 ID URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="d722a-156">3 단계: 클라이언트 응용 프로그램을 구성 하 고 hello 서비스 실행</span><span class="sxs-lookup"><span data-stu-id="d722a-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="d722a-157">Hello tooDo 목록 서비스 실행에서 하기 전에 Azure AD에서 토큰을 가져오기 고 toohello 서비스 호출을 높일 수 있도록 tooconfigure hello tooDo 목록 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="d722a-158">Toohello 돌아가서 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d722a-159">Azure AD 테 넌 트에 새 응용 프로그램을 만들고 선택 **네이티브 클라이언트 응용 프로그램** hello 프롬프트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="d722a-160">**이름** 응용 프로그램 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="d722a-161">입력 `http://TodoListClient/` hello에 대 한 **리디렉션 Uri** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="d722a-162">등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="d722a-163">이 값이 필요 합니다 hello 다음 단계에서 하므로에서 복사 hello 응용 프로그램 페이지.</span><span class="sxs-lookup"><span data-stu-id="d722a-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="d722a-164">Hello에서 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="d722a-165">찾기 및 hello tooDo 목록 서비스를 선택, 추가 hello **액세스 TodoListService** 에 따른 권한 **위임 된 권한**, 클릭 하 고 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="d722a-166">Visual Studio에서 열고 `App.config` 에 hello TodoListClient 프로젝트를 선택한 다음 hello에 구성 값을 입력 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="d722a-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="d722a-167">`ida:Tenant`Azure AD 테 넌 트-예를 들어 contoso.onmicrosoft.com hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d722a-168">`ida:ClientId`hello Azure 포털에서에서 복사한 hello 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="d722a-169">`todo:TodoListResourceId`hello hello tooDo hello Azure 포털에에서 입력 된 목록 서비스 응용 프로그램의 앱 ID URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d722a-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d722a-170">Next steps</span></span>
<span data-ttu-id="d722a-171">마지막으로, 각 프로젝트를 정리하고 빌드한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="d722a-172">아직 하지 않는 경우 이제는 hello 시간 toocreate와 테 넌 트에 새 사용자는 *. onmicrosoft.com 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="d722a-173">해당 사용자와 toohello tooDo 목록 클라이언트에 로그인 하 고 일부 작업 toohello 사용자의 할 일 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="d722a-174">구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d722a-175">이제 toomore id 시나리오에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d722a-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
