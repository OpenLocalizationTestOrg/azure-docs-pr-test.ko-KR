---
title: Azure AD B2C | Microsoft Docs
description: "Azure Active Directory B2C를 사용하여 .NET Web API를 빌드하는 방법이며 인증을 위해 OAuth 2.0 액세스 토큰을 사용하여 보호됩니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="f198e-103">Azure Active Directory B2C: .NET Web API 빌드</span><span class="sxs-lookup"><span data-stu-id="f198e-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="f198e-104">Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="f198e-105">이러한 토큰을 통해 클라이언트 앱이 API에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="f198e-106">이 문서에서는 클라이언트 응용 프로그램의 사용자에게 CRUD 태스크를 허용하는 .NET MVC "할 일 모음" API를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="f198e-107">Web API는 Azure AD B2C를 사용하여 보호되며 사용자가 해당 할 일 목록을 관리하도록 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="f198e-108">Azure AD B2C 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="f198e-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="f198e-109">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f198e-110">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="f198e-111">아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="f198e-112">클라이언트 응용 프로그램 및 웹 API는 동일한 Azure AD B2C 디렉터리를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="f198e-113">Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="f198e-113">Create a web API</span></span>

<span data-ttu-id="f198e-114">다음으로 B2C 디렉터리에서 Web API 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="f198e-115">앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="f198e-116">앱을 만들려면 [다음 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f198e-117">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-117">Be sure to:</span></span>

* <span data-ttu-id="f198e-118">응용 프로그램에서 **웹앱** 또는 **Web API**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="f198e-119">웹앱의 **리디렉션 URI** `https://localhost:44332/`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="f198e-120">이 코드 샘플에 대한 웹앱 클라이언트의 기본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="f198e-121">앱에 할당된 **응용 프로그램 ID** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="f198e-122">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-122">You'll need it later.</span></span>
* <span data-ttu-id="f198e-123">앱 식별자를 **앱 ID URI**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="f198e-124">**게시된 범위** 메뉴를 통해 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f198e-125">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="f198e-125">Create your policies</span></span>

<span data-ttu-id="f198e-126">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f198e-127">Azure AD B2C와 통신하는 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="f198e-128">[정책 참조 문서](active-directory-b2c-reference-policies.md)에 설명된 대로 결합된 등록/로그인 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f198e-129">정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="f198e-130">정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="f198e-131">모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="f198e-132">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="f198e-133">각 정책을 만든 후에 **이름**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="f198e-134">정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f198e-135">정책을 성공적으로 만들면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="f198e-136">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="f198e-136">Download the code</span></span>

<span data-ttu-id="f198e-137">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="f198e-138">다음을 실행하여 샘플을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="f198e-139">샘플 코드를 다운로드한 후 Visual Studio .sln 파일을 열어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="f198e-140">이제 솔루션에는 `TaskWebApp`과 `TaskService`, 2개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="f198e-141">`TaskWebApp` 은 사용자와 상호 작용하는 MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="f198e-142">`TaskService` 는 각 사용자의 할 일 모음을 저장하는 앱의 백 엔드 Web API입니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="f198e-143">이 문서에서는 `TaskService` 응용 프로그램만을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="f198e-144">Azure AD B2C를 사용하여 `TaskWebApp`을 구축하는 방법을 알아보려면 [.NET 웹앱 자습서](active-directory-b2c-devquickstarts-web-dotnet-susi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f198e-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="f198e-145">Azure AD B2C 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="f198e-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="f198e-146">샘플은 데모 테넌트의 정책 및 클라이언트 ID를 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="f198e-147">고유한 테넌트를 사용하려는 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="f198e-148">`TaskService` 프로젝트에서 `web.config`을 열고 다음 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="f198e-149">`ida:Tenant`을 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="f198e-150">`ida:ClientId`을 Web API 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="f198e-151">`ida:SignUpSignInPolicyId`을 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="f198e-152">`TaskWebApp` 프로젝트에서 `web.config`를 열고 다음 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="f198e-153">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="f198e-154">`ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="f198e-155">`ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="f198e-156">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="f198e-157">`ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="f198e-158">`ida:ResetPasswordPolicyId`을 "암호 재설정" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="f198e-159">API 보호</span><span class="sxs-lookup"><span data-stu-id="f198e-159">Secure the API</span></span>

<span data-ttu-id="f198e-160">API를 호출하는 클라이언트가 있는 경우 OAuth 2.0 전달자 토큰을 사용하여 API(예: `TaskService`)를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="f198e-161">이렇게 하면 요청에 전달자 토큰이 있는 경우 API에 대한 각 요청이 유효해 집니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="f198e-162">API는 Microsoft OWIN(Open Web Interface for .NET)을 사용하여 전달자 토큰을 허용하고 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="f198e-163">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="f198e-163">Install OWIN</span></span>

<span data-ttu-id="f198e-164">OAuth OWIN 인증 파이프라인을 설치하거나 Visual Studio 패키지 관리자 콘솔을 사용하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="f198e-165">전달자 토큰을 허용하고 유효성을 검사하는 OWIN 미들웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="f198e-166">OWIN 시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="f198e-166">Add an OWIN startup class</span></span>

<span data-ttu-id="f198e-167">`Startup.cs`라는 API에 OWIN 시작 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="f198e-168">프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** 및 **새 항목**을 선택한 다음 OWIN을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="f198e-169">OWIN 미들웨어는 앱이 시작되면 `Configuration(…)` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="f198e-170">이 샘플에서는 `public partial class Startup`에 대한 클래스 선언을 변경하고 `App_Start\Startup.Auth.cs`에서 클래스의 다른 부분을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="f198e-171">`Configuration` 메서드 내에서 `ConfigureAuth`에 호출을 추가했습니다. 이는 `Startup.Auth.cs`에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="f198e-172">수정 후에 `Startup.cs`는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="f198e-173">OAuth 2.0 인증 구성</span><span class="sxs-lookup"><span data-stu-id="f198e-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="f198e-174">`App_Start\Startup.Auth.cs` 파일을 열고 `ConfigureAuth(...)` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="f198e-175">예를 들어 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="f198e-176">작업 컨트롤러 보호</span><span class="sxs-lookup"><span data-stu-id="f198e-176">Secure the task controller</span></span>

<span data-ttu-id="f198e-177">앱을 OAuth 2.0 인증을 사용하도록 구성한 후 작업 컨트롤러에 `[Authorize]` 태그를 추가하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="f198e-178">할 일 모음 조작이 발생하는 컨트롤러이므로 클래스 수준에서 전체 컨트롤러를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="f198e-179">보다 세분화한 제어를 위해 개별 작업에 `[Authorize]` 태그를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="f198e-180">토큰에서 사용자 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="f198e-180">Get user information from the token</span></span>

<span data-ttu-id="f198e-181">`TasksController` 는 데이터베이스에 작업을 저장하며, 여기서 각 작업에는 작업을 "소유"하는 연결된 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="f198e-182">소유자는 사용자의 **개체 ID**로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="f198e-183">(따라서 모든 정책에 응용 프로그램 클레임으로 개체 ID를 추가해야 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="f198e-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="f198e-184">토큰에서 사용 권한 확인</span><span class="sxs-lookup"><span data-stu-id="f198e-184">Validate the permissions in the token</span></span>

<span data-ttu-id="f198e-185">웹 API에 대한 일반적인 요구 사항은 토큰에 있는 "범위"를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="f198e-186">이렇게 하여 사용자가 할 일 목록 서비스에 액세스하는 데 필요한 권한에 동의했음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="f198e-187">샘플 앱 실행</span><span class="sxs-lookup"><span data-stu-id="f198e-187">Run the sample app</span></span>

<span data-ttu-id="f198e-188">마지막으로 `TaskWebApp`과 `TaskService`를 모두 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="f198e-189">사용자의 할 일 모음에 일부 작업을 만들고 클라이언트를 중지하고 다시 시작한 후에 API에서 어떻게 유지할지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="f198e-190">청책 편집</span><span class="sxs-lookup"><span data-stu-id="f198e-190">Edit your policies</span></span>

<span data-ttu-id="f198e-191">Azure AD B2C를 사용하여 API를 보호한 후에 로그인/등록 정책을 시험해 보고 API에서 효과(또는 부족)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="f198e-192">정책에서 응용 프로그램 클레임을 조작하고 Web API에서 사용할 수 있는 사용자 정보를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="f198e-193">이 문서의 앞에서 설명한 것처럼 추가한 모든 클레임은 `ClaimsPrincipal` 개체의 .NET MVC Web API에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f198e-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
