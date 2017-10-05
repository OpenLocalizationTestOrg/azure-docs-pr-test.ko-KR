---
title: Azure Active Directory B2C | Microsoft Docs
description: "Azure Active Directory B2C 및 OAuth 2.0 액세스 토큰을 사용하여 .NET 웹앱을 빌드하고 웹 API를 호출하는 방법입니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="b7387-103">Azure AD B2C: .NET 웹앱에서 .NET 웹 API 호출</span><span class="sxs-lookup"><span data-stu-id="b7387-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="b7387-104">Azure AD B2C를 사용하여 강력한 ID 관리 기능을 웹앱 및 웹 API에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="b7387-105">이 문서에서는 액세스 토큰을 요청하고 .NET "할 일 모음" 웹앱에서 .NET 웹 API로 호출하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="b7387-106">이 문서는 Azure AD B2C를 사용하여 등록, 로그인 및 프로필 관리를 구현하는 방법을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="b7387-107">사용자를 인증한 후에 Web API를 호출하는 데 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="b7387-108">아직 하지 않은 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="b7387-109">[.NET 웹앱](active-directory-b2c-devquickstarts-web-dotnet-susi.md) 시작</span><span class="sxs-lookup"><span data-stu-id="b7387-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="b7387-110">[.NET 웹 API](active-directory-b2c-devquickstarts-api-dotnet.md) 시작</span><span class="sxs-lookup"><span data-stu-id="b7387-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="b7387-111">필수 요소</span><span class="sxs-lookup"><span data-stu-id="b7387-111">Prerequisite</span></span>

<span data-ttu-id="b7387-112">웹 API를 호출하는 웹 응용 프로그램을 빌드하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="b7387-113">[Azure AD B2C 테넌트를 만듭니다](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b7387-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="b7387-114">[웹 API를 등록합니다](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="b7387-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="b7387-115">[웹앱을 등록합니다](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="b7387-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="b7387-116">[정책을 설정합니다](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b7387-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="b7387-117">[웹 API를 사용하도록 웹앱 권한을 부여합니다](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="b7387-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7387-118">클라이언트 응용 프로그램 및 웹 API는 동일한 Azure AD B2C 디렉터리를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="b7387-119">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="b7387-119">Download the code</span></span>

<span data-ttu-id="b7387-120">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="b7387-121">다음을 실행하여 샘플을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="b7387-122">샘플 코드를 다운로드한 후 Visual Studio .sln 파일을 열어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="b7387-123">이제 솔루션에는 `TaskWebApp`과 `TaskService`, 2개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="b7387-124">`TaskWebApp`은 사용자와 상호 작용하는 MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="b7387-125">`TaskService` 는 각 사용자의 할 일 모음을 저장하는 앱의 백 엔드 Web API입니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="b7387-126">이 문서에서는 `TaskWebApp` 웹앱 또는 `TaskService` 웹 API를 구축하는 방법을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="b7387-127">Azure AD B2C를 사용하여 .NET 웹앱을 구축하는 방법을 알아보려면 [.NET 웹앱 자습서](active-directory-b2c-devquickstarts-web-dotnet-susi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7387-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="b7387-128">Azure AD B2C를 사용하여 보안된 .NET 웹 API를 구축하는 방법을 알아보려면 [.NET 웹 API 자습서](active-directory-b2c-devquickstarts-api-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7387-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="b7387-129">Azure AD B2C 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="b7387-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="b7387-130">샘플은 데모 테넌트의 정책 및 클라이언트 ID를 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="b7387-131">자신의 테넌트를 사용하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="b7387-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="b7387-132">`TaskService` 프로젝트에서 `web.config`을 열고 다음 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="b7387-133">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b7387-134">`ida:ClientId`를 웹 API 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="b7387-135">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="b7387-136">`TaskWebApp` 프로젝트에서 `web.config`를 열고 다음 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="b7387-137">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b7387-138">`ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="b7387-139">`ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="b7387-140">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="b7387-141">`ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="b7387-142">`ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="b7387-143">액세스 토큰 요청 및 저장</span><span class="sxs-lookup"><span data-stu-id="b7387-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="b7387-144">사용 권한 지정</span><span class="sxs-lookup"><span data-stu-id="b7387-144">Specify the permissions</span></span>

<span data-ttu-id="b7387-145">웹 API에 대한 호출을 만들려면 사용자를 인증하고(등록/로그인 정책 사용) Azure AD B2C에서 [액세스 토큰을 받아야](active-directory-b2c-access-tokens.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="b7387-146">액세스 토큰을 받으려면 먼저 액세스 토큰을 부여하려는 권한을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="b7387-147">`/authorize` 끝점에 대한 요청을 만들 때 `scope` 매개 변수에서 권한이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="b7387-148">예를 들어 `https://contoso.onmicrosoft.com/tasks`의 앱 ID URI를 가진 리소스 응용 프로그램에 대한 "읽기" 권한으로 액세스 토큰을 얻으려면 범위는 `https://contoso.onmicrosoft.com/tasks/read`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="b7387-149">이 샘플의 범위를 지정하려면 `App_Start\Startup.Auth.cs` 파일을 열고 OpenIdConnectAuthenticationOptions에서 `Scope` 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="b7387-150">액세스 토큰에 대한 인증 코드 교환</span><span class="sxs-lookup"><span data-stu-id="b7387-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="b7387-151">사용자가 등록 또는 로그인 환경을 완료한 후 앱은 Azure AD B2C에서 인증 코드를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="b7387-152">OWIN OpenID Connect 미들웨어는 코드를 저장하지만 액세스 토큰에 대해 교환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="b7387-153">[MSAL 라이브러리](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)를 사용하여 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="b7387-154">샘플에서는 권한 부여 코드를 받을 때마다 OpenID Connect 미들웨어로 알림 콜백을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="b7387-155">콜백에서 MSAL을 사용하여 토큰에 대한 코드를 교환하고 토큰을 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="b7387-156">웹 API 호출</span><span class="sxs-lookup"><span data-stu-id="b7387-156">Calling the web API</span></span>

<span data-ttu-id="b7387-157">이 섹션에서는 웹 API에 액세스하기 위해 Azure AD B2C를 사용하여 등록/로그인 중에 받은 토큰을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="b7387-158">컨트롤러에서 저장된 토큰 검색</span><span class="sxs-lookup"><span data-stu-id="b7387-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="b7387-159">`TasksController`은 HTTP 요청을 API로 보내 작업을 읽고 만들고 삭제하도록 웹 API와 통신을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="b7387-160">API는 Azure AD B2C에 의해 보안되므로, 먼저 위의 단계에서 저장한 토큰을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="b7387-161">Web API로부터 작업 읽기</span><span class="sxs-lookup"><span data-stu-id="b7387-161">Read tasks from the web API</span></span>

<span data-ttu-id="b7387-162">이제 토큰이 있으므로 `Authorization` 헤더에서 HTTP `GET` 요청에 토큰을 연결하여 `TaskService`를 안전하게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="b7387-163">Web API에서 작업 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="b7387-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="b7387-164">캐시에서 액세스 토큰을 검색하기 위해 `POST` 및 `DELETE` 요청을 MSAL을 사용하여 웹 API에 보낼 때 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="b7387-165">샘플 앱 실행</span><span class="sxs-lookup"><span data-stu-id="b7387-165">Run the sample app</span></span>

<span data-ttu-id="b7387-166">마지막으로 두 앱을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="b7387-167">등록하고 로그인하여, 로그인된 사용자에 대한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="b7387-168">로그아웃했다가 다른 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="b7387-169">해당 사용자에 대한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-169">Create tasks for that user.</span></span> <span data-ttu-id="b7387-170">API 가 받는 토큰에서 사용자의 ID를 추출하므로 API에 사용자별 작업이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="b7387-171">또한 범위 다루기를 시도해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-171">Also try playing with the scopes.</span></span> <span data-ttu-id="b7387-172">"쓰기"에 대한 권한을 제거한 다음 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="b7387-173">범위를 변경할 때마다 로그아웃해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7387-173">Just make sure to sign out each time you change the scope.</span></span>

