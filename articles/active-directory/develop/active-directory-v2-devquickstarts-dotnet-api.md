---
title: "Azure AD v2.0 끝점 hello aaaAdd 로그인 tooa.NET MVC 웹 API를 사용 하 여 | Microsoft Docs"
description: "어떻게 toobuild 회사 또는 학교 계정 및 두 개인 Microsoft 계정에서 보낸 토큰을 허용 하는.NET MVC 웹 Api입니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="02784-103">MVC 웹 API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="02784-103">Secure an MVC web API</span></span>
<span data-ttu-id="02784-104">사용 하 여 웹 API 보호 하려면 Azure Active Directory hello v2.0 끝점과 [OAuth 2.0](active-directory-v2-protocols.md) 액세스 토큰을 두 개인 Microsoft 계정 가진 사용자 및 toosecurely 웹 API에 액세스 하는 회사 또는 학교 계정을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="02784-105">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="02784-106">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="02784-107">ASP.NET Web API에서는 .NET Framework 4.5에 포함된 Microsoft OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="02784-108">여기에서는 OWIN toobuild toocreate 이며 읽기 작업을 사용자의 할 일 목록 클라이언트를 허용 하는 "tooDo 목록" MVC 웹 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="02784-109">hello web API는 들어오는 요청을 유효한 액세스 토큰을 포함 하 고 보호 된 경로에 유효성 검사를 통과 하지 못한 모든 요청을 거부 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="02784-110">이 샘플은 Visual Studio 2015를 사용하여 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="02784-111">다운로드</span><span class="sxs-lookup"><span data-stu-id="02784-111">Download</span></span>
<span data-ttu-id="02784-112">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="02784-113">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="02784-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="02784-114">hello 뼈대 앱 간단한 API에 대 한 모든 hello 상용구 코드를 포함 하지만 모든 hello id 관련 조각을 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="02784-115">대신 복제할 수 toofollow와 함께 사용 하지 않으려는 경우 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="02784-116">앱 등록</span><span class="sxs-lookup"><span data-stu-id="02784-116">Register an app</span></span>
<span data-ttu-id="02784-117">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="02784-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="02784-118">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-118">Make sure to:</span></span>

* <span data-ttu-id="02784-119">Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="02784-120">또한 이 visual studio 솔루션에는 간단한 WPF 앱인 "TodoListClient"가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="02784-121">hello TodoListClient 방법을 사용자가 로그인에 사용 되는 toodemonstrate 이며 tooyour 웹 API 요청 방법을 클라이언트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="02784-122">이 경우 둘 다 TodoListClient hello와 hello TodoListService 표현 된 hello 동일한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="02784-123">tooconfigure TodoListClient hello, 또한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="02784-124">Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="02784-125">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="02784-125">Install OWIN</span></span>
<span data-ttu-id="02784-126">응용 프로그램을 등록 한 사용자 앱 toocommunicate 순서 toovalidate 들어오는 요청 및 토큰에 대 한 hello v2.0 끝점과 tooset이 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="02784-127">toobegin, hello 솔루션을 열고 hello OWIN 미들웨어 NuGet 패키지 toohello TodoListService 프로젝트 hello 패키지 관리자 콘솔을 사용 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="02784-128">OAuth 인증 구성</span><span class="sxs-lookup"><span data-stu-id="02784-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="02784-129">OWIN 시작 클래스 toohello TodoListService 프로젝트 라는 추가 `Startup.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="02784-130">Hello 프로젝트에서 마우스 오른쪽 단추로 클릭--> **추가** --> **새 항목** "OWIN"에 대 한 검색--> 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="02784-131">hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="02784-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="02784-132">Hello 클래스 선언에도 변경`public partial class Startup` -이미 구현 했습니다이 클래스의 일부를 다른 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="02784-133">Hello에 `Configuration(…)` 메서드는 호출 tooConfgureAuth(...) tooset 웹 앱에 대 한 인증을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="02784-134">파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(…)` 메서드 hello v2.0 끝점에서 hello 웹 API tooaccept 토큰을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="02784-135">에서는 이제 `[Authorize]` tooprotect 특성을 컨트롤러 및 OAuth 2.0 전달자 인증을 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="02784-136">Hello 데코레이팅 `Controllers\TodoListController.cs` authorize 태그를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="02784-137">이렇게 하면 해당 페이지에 액세스 하기 전에 hello 사용자 toosign에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="02784-138">하면 권한 있는 발신자를 성공적으로 중 하나를 호출 hello `TodoListController` Api hello 작업 해야에 액세스할 수 tooinformation hello 호출자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="02784-139">OWIN hello 통해 hello 전달자 토큰에 대 한 액세스 toohello 클레임을 제공 `ClaimsPrincpal` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="02784-140">마지막으로 hello를 열고 `web.config` hello TodoListService 프로젝트의 hello 루트에서 파일을 hello에 구성 값을 입력 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="02784-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="02784-141">프로그램 `ida:Audience` 는 hello **응용 프로그램 Id** hello 포털에 입력 한 hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="02784-142">Hello 클라이언트 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="02784-142">Configure hello client app</span></span>
<span data-ttu-id="02784-143">작업에 할 일 목록 서비스 hello 볼 수 있듯이 먼저 tooconfigure hello 할 일 목록 클라이언트 hello v2.0 끝점에서 토큰을 가져올 고 toohello 서비스 호출을 높일 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="02784-144">Hello TodoListClient 프로젝트를 열고 `App.config` hello에 구성 값을 입력 하 고 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="02784-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="02784-145">프로그램 `ida:ClientId` hello 포털에서 복사 하는 응용 프로그램 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="02784-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="02784-146">마지막으로, 각 프로젝트를 정리하고 빌드한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="02784-147">이제 개인 Microsoft 계정과 회사 또는 학교 계정 둘 다의 토큰을 허용하는 .NET MVC Web API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="02784-148">Hello TodoListClient에 로그인 하 고 웹 api tooadd 작업 toohello 사용자의 할 일 목록을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="02784-149">참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="02784-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02784-150">Next steps</span></span>
<span data-ttu-id="02784-151">이제 추가 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="02784-152">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02784-152">You may want tootry:</span></span>

[<span data-ttu-id="02784-153">웹앱에서 웹 API 호출 >></span><span class="sxs-lookup"><span data-stu-id="02784-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="02784-154">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="02784-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="02784-155">hello v2.0 개발자 가이드 >></span><span class="sxs-lookup"><span data-stu-id="02784-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="02784-156">StackOverflow "azure-active-directory" 태그 >></span><span class="sxs-lookup"><span data-stu-id="02784-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="02784-157">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="02784-157">Get security updates for our products</span></span>
<span data-ttu-id="02784-158">보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="02784-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
