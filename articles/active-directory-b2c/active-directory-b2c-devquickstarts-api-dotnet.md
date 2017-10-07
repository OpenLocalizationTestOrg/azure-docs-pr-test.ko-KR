---
title: AD B2C aaaAzure | Microsoft Docs
description: "Toobuild Azure Active Directory B2C를 사용 하 여.NET 웹 API 인증에 대 한 OAuth 2.0 액세스 토큰을 사용 하 여 보호 하는 방법"
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
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="50f06-103">Azure Active Directory B2C: .NET Web API 빌드</span><span class="sxs-lookup"><span data-stu-id="50f06-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="50f06-104">Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="50f06-105">이러한 토큰을 사용 하 여 클라이언트 앱 tooauthenticate toohello API 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="50f06-106">이 문서에서는 어떻게 toocreate.NET MVC "할 일 목록" API를 허용 하 여 클라이언트의 사용자가 응용 프로그램 tooCRUD 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="50f06-107">hello 웹 API는 Azure AD B2C를 사용 하 여 보안 처리 되며 toomanage 인증 된 사용자의 할 일 목록을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="50f06-108">Azure AD B2C 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="50f06-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="50f06-109">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="50f06-110">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="50f06-111">아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="50f06-112">hello 클라이언트 응용 프로그램 및 web API hello 동일한 Azure AD B2C 디렉터리를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="50f06-113">Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="50f06-113">Create a web API</span></span>

<span data-ttu-id="50f06-114">다음으로, 웹 API 앱 toocreate B2C 디렉터리에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="50f06-115">Azure AD 정보가 필요한 toosecurely 통신할 수 있는지 응용 프로그램에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="50f06-116">응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="50f06-117">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-117">Be sure to:</span></span>

* <span data-ttu-id="50f06-118">포함 된 **웹 앱** 또는 **웹 API** hello 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="50f06-119">사용 하 여 hello **리디렉션 URI** `https://localhost:44332/` hello 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="50f06-120">이 코드 샘플에 대 한 웹 앱 클라이언트 hello의 hello 기본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="50f06-121">복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="50f06-122">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-122">You'll need it later.</span></span>
* <span data-ttu-id="50f06-123">앱 식별자를 **앱 ID URI**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="50f06-124">Hello 통해 사용 권한을 추가 **범위 게시** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="50f06-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="50f06-125">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="50f06-125">Create your policies</span></span>

<span data-ttu-id="50f06-126">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="50f06-127">Azure AD B2C와 정책 toocommunicate toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="50f06-128">권장 로그-up/로그인 정책 결합 hello를 사용 하 여 hello에 설명 된 대로 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="50f06-129">정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="50f06-130">정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="50f06-131">모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="50f06-132">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="50f06-133">복사 hello **이름** 를 만든 후 각 정책의 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="50f06-134">Hello 정책 이름을 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="50f06-135">준비 toobuild 하는 hello 정책을 성공적으로 만든 후 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="50f06-136">Hello 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="50f06-136">Download hello code</span></span>

<span data-ttu-id="50f06-137">이 자습서에 대 한 hello 코드에서 유지 관리 됩니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="50f06-138">실행 하 여 hello 샘플을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="50f06-139">Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="50f06-140">hello 솔루션 파일에는 두 개의 프로젝트가 포함 되어: `TaskWebApp` 및 `TaskService`합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="50f06-141">`TaskWebApp`와 상호 작용 사용자 hello MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="50f06-142">`TaskService`각 사용자의 할 일 목록에 저장 하는 hello 앱 백 엔드 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="50f06-143">이 문서에서는 hello 설명만 `TaskService` 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="50f06-144">toolearn 어떻게 toobuild `TaskWebApp` Azure AD B2C를 사용 하 여 참조 [이.NET 웹 응용 프로그램 자습서](active-directory-b2c-devquickstarts-web-dotnet-susi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="50f06-145">Azure AD B2C hello 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="50f06-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="50f06-146">이 샘플은 구성 된 toouse hello 정책 및 클라이언트 ID 우리의 데모 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="50f06-147">Toouse 원하는 경우 고유한 테 넌 트 다음 toodo hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="50f06-148">열기 `web.config` hello에 `TaskService` 프로젝트 및에 대 한 hello 값 바꾸기</span><span class="sxs-lookup"><span data-stu-id="50f06-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="50f06-149">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="50f06-150">`ida:ClientId`을 Web API 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="50f06-151">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="50f06-152">열기 `web.config` hello에 `TaskWebApp` 프로젝트 및에 대 한 hello 값 바꾸기</span><span class="sxs-lookup"><span data-stu-id="50f06-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="50f06-153">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="50f06-154">`ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="50f06-155">`ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="50f06-156">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="50f06-157">`ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="50f06-158">`ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="50f06-159">Hello API 보호</span><span class="sxs-lookup"><span data-stu-id="50f06-159">Secure hello API</span></span>

<span data-ttu-id="50f06-160">API를 호출하는 클라이언트가 있는 경우 OAuth 2.0 전달자 토큰을 사용하여 API(예: `TaskService`)를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="50f06-161">이렇게 하면 각 요청 tooyour API만 되도록 hello 요청은 전달자 토큰을 하는 경우에 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="50f06-162">API는 Microsoft OWIN(Open Web Interface for .NET)을 사용하여 전달자 토큰을 허용하고 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="50f06-163">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="50f06-163">Install OWIN</span></span>

<span data-ttu-id="50f06-164">Hello OWIN OAuth 인증 파이프라인 hello Visual Studio 패키지 관리자 콘솔을 사용 하 여 설치 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="50f06-165">그러면 hello OWIN 미들웨어 있고 전달자 토큰의 유효성을 검사 되도록 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="50f06-166">OWIN 시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="50f06-166">Add an OWIN startup class</span></span>

<span data-ttu-id="50f06-167">OWIN 시작 클래스 toohello API 호출 추가 `Startup.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="50f06-168">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 **추가** 및 **새 항목**, 한 다음 OWIN에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="50f06-169">hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="50f06-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="50f06-170">이 예제에서는 변경 했습니다 hello 클래스 선언 너무`public partial class Startup` 구현에서 hello 클래스의 다른 부분을 hello `App_Start\Startup.Auth.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="50f06-171">내부 hello `Configuration` 메서드를 호출 너무 추가`ConfigureAuth`에 정의 된 `Startup.Auth.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="50f06-172">Hello 수정한 다음 `Startup.cs` hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="50f06-173">OAuth 2.0 인증 구성</span><span class="sxs-lookup"><span data-stu-id="50f06-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="50f06-174">파일 열기 hello `App_Start\Startup.Auth.cs`, 고 hello 구현 `ConfigureAuth(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="50f06-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="50f06-175">예를 들어 것 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-175">For example, it could look like hello following:</span></span>

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
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="50f06-176">보안 hello 작업 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="50f06-176">Secure hello task controller</span></span>

<span data-ttu-id="50f06-177">Hello 앱 구성된 toouse OAuth 2.0 인증을 추가 하 여 web API를 보호할 수 있습니다는 `[Authorize]` 태그 toohello 작업 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="50f06-178">모든 할 일 목록 조작 발생, hello 전체 컨트롤러 hello 클래스 수준에서 보안을 설정 해야 하므로 hello 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="50f06-179">Hello를 추가할 수도 있습니다 `[Authorize]` 보다 세부적으로 제어에 대 한 tooindividual 작업 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="50f06-180">사용자 정보 hello에서 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="50f06-180">Get user information from hello token</span></span>

<span data-ttu-id="50f06-181">`TasksController`각 작업에 "소유" hello 작업 하 고 연결된 된 사용자 데이터베이스에서 작업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="50f06-182">hello 소유자 hello 사용자로 식별 되 **개체 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="50f06-183">(이 때문에 응용 프로그램으로 tooadd hello 개체 ID를 필요한 모든 정책에서 클레임입니다.)</span><span class="sxs-lookup"><span data-stu-id="50f06-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="50f06-184">Hello 권한을 hello 토큰의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="50f06-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="50f06-185">웹 Api에 대 한 일반적인 요구 사항은 toovalidate hello "범위" hello 토큰에 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="50f06-186">이렇게 하면 해당 hello 사용자가 동의 toohello 권한이 필요한 tooaccess hello 할 일 목록 서비스.</span><span class="sxs-lookup"><span data-stu-id="50f06-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="50f06-187">Hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="50f06-187">Run hello sample app</span></span>

<span data-ttu-id="50f06-188">마지막으로 `TaskWebApp`과 `TaskService`를 모두 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="50f06-189">Hello 사용자의 할 일 목록에서 몇 가지 작업을 만들고 어떻게 유지 하기 hello API에서에서 중지 하 고 hello 클라이언트를 다시 시작 후에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="50f06-190">청책 편집</span><span class="sxs-lookup"><span data-stu-id="50f06-190">Edit your policies</span></span>

<span data-ttu-id="50f06-191">Azure AD B2C를 사용 하 여 API을 확보 한 후 사용자 로그인-에/등록 정책 및 hello 효과 보기 (또는 결핍) hello API에를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="50f06-192">Hello 정책에서 응용 프로그램 클레임 hello를 조작 하 고 hello web API에서에서 제공 하는 hello 사용자 정보를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="50f06-193">추가 하는 모든 클레임을 사용할 수 있는 tooyour.NET MVC 웹 API hello 수 `ClaimsPrincipal` 이 문서의 앞부분에 설명 된 대로 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="50f06-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
