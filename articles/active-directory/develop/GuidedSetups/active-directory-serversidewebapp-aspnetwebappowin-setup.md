---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-설치 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="65c9d-103">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="65c9d-103">Set up your project</span></span>

<span data-ttu-id="65c9d-104">이 섹션 hello 단계 tooinstall 보여주며, OpenID Connect를 사용 하 여 ASP.NET 프로젝트에 OWIN 미들웨어를 통해 hello 인증 파이프라인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="65c9d-105">Toodownload이이 샘플의 Visual Studio 프로젝트를 대신 선호?</span><span class="sxs-lookup"><span data-stu-id="65c9d-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="65c9d-106">[프로젝트를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) toohello 건너뛸 [구성 단계](#create-an-application-express) tooconfigure hello 코드 샘플을 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="65c9d-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="65c9d-107">ASP.NET 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="65c9d-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="65c9d-108">Visual Studio에서: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="65c9d-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="65c9d-109">*Visual C#\Web*에서 `ASP.NET Web Application (.NET Framework)`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="65c9d-110">응용 프로그램의 이름을 지정하고 *확인*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="65c9d-111">선택 `Empty` 및 선택 hello 확인란 tooadd `MVC` 참조</span><span class="sxs-lookup"><span data-stu-id="65c9d-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="65c9d-112">인증 구성 요소 추가</span><span class="sxs-lookup"><span data-stu-id="65c9d-112">Add authentication components</span></span>

1. <span data-ttu-id="65c9d-113">Visual Studio에서: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="65c9d-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="65c9d-114">추가 *OWIN 미들웨어 NuGet 패키지* hello 다음 hello 패키지 관리자 콘솔 창에에서 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="65c9d-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="65c9d-115">이러한 라이브러리 정보</span><span class="sxs-lookup"><span data-stu-id="65c9d-115">About these libraries</span></span>

><span data-ttu-id="65c9d-116">single sign on (SSO) 쿠키 기반 인증을 통해 OpenID Connect를 사용 하 여 위의 hello 라이브러리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="65c9d-117">인증이 완료 되 고 hello 사용자를 나타내는 hello 토큰입니다. 전송 tooyour 응용 프로그램, OWIN 미들웨어입니다. 세션 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="65c9d-118">hello 브라우저 다음 사용 하 여이 쿠키 이후 요청에서 hello 사용자 tooretype 필요가 없도록 암호를 며 없는 추가 확인 사항이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="65c9d-119">Hello 인증 파이프라인 구성</span><span class="sxs-lookup"><span data-stu-id="65c9d-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="65c9d-120">hello 단계 아래에 사용 되는 toocreate OWIN 미들웨어 시작 클래스 tooconfigure OpenID Connect 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="65c9d-121">이 클래스는 IIS 프로세스 시작 시 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="65c9d-122">프로젝트에 없는 경우는 `Startup.cs` hello 루트 폴더에 파일:</span><span class="sxs-lookup"><span data-stu-id="65c9d-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="65c9d-123">Hello 프로젝트의 루트 폴더를 마우스 오른쪽 단추로 클릭 합니다. >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="65c9d-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="65c9d-124">이름을 `Startup.cs`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="65c9d-125">선택한 hello 클래스는 OWIN 시작 클래스와 표준 C# 클래스가 아닌 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="65c9d-126">확인 표시 되 면이를 확인할 `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` hello 네임 스페이스 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="65c9d-127">추가 *OWIN* 및 *Microsoft.IdentityModel* 너무 참조`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="65c9d-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="65c9d-128">시작 클래스를 아래 hello 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-128">Replace Startup class with hello code below:</span></span>
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a><span data-ttu-id="65c9d-129">추가 정보</span><span class="sxs-lookup"><span data-stu-id="65c9d-129">More Information</span></span>

> <span data-ttu-id="65c9d-130">매개 변수가 hello *OpenIDConnectAuthenticationOptions* 역할을 Azure AD와 응용 프로그램 toocommunicate hello에 대 한 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="65c9d-131">Hello OpenID Connect 미들웨어 hello 백그라운드에서 쿠키를 사용 하므로 있어야 쿠키 인증을 tooset 위의 hello 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="65c9d-132">hello *ValidateIssuer* 이 값은 OpenIdConnect 지정 toonot tooone 특정 조직 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c9d-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

