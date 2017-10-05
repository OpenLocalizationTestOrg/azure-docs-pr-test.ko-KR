---
title: "Azure Active Directory B2C: 액세스 토큰 요청 | Microsoft Docs"
description: "이 문서에서는 클라이언트 응용 프로그램을 설정하고 액세스 토큰을 획득하는 방법을 보여 줍니다."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 4b361a8e69f885d5b89ac9b2086e2731ee4d8b48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a><span data-ttu-id="466a5-103">Azure AD B2C: 액세스 토큰 요청</span><span class="sxs-lookup"><span data-stu-id="466a5-103">Azure AD B2C: Requesting access tokens</span></span>

<span data-ttu-id="466a5-104">액세스 토큰(Azure AD B2C의 응답에서 **액세스\_토큰**으로 표시됨)은 클라이언트가 웹 API와 같은 [권한 부여 서버](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics)로 보호되는 리소스에 액세스하는 데 사용할 수 있는 보안 토큰의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-104">An access token (denoted as **access\_token** in the responses from Azure AD B2C) is a form of security token that a client can use to access resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API.</span></span> <span data-ttu-id="466a5-105">액세스 토큰은 [JWT](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens)로 표시되고 원하는 리소스 서버에 대한 정보 및 서버에 부여된 사용 권한을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-105">Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about the intended resource server and the granted permissions to the server.</span></span> <span data-ttu-id="466a5-106">리소스 서버를 호출할 때 액세스 토큰은 HTTP 요청에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-106">When calling the resource server, the access token must be present in the HTTP request.</span></span>

<span data-ttu-id="466a5-107">이 문서에서는 **액세스\_토큰**을 얻기 위해 클라이언트 응용 프로그램 및 웹 API를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-107">This article discusses how to configure a client application and web API in order to obtain an **access\_token**.</span></span>

> [!NOTE]
> <span data-ttu-id="466a5-108">**Azure AD B2C에서는 Web API 체인(On-Behalf-Of)을 지원하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="466a5-108">**Web API chains (On-Behalf-Of) is not supported by Azure AD B2C.**</span></span>
>
> <span data-ttu-id="466a5-109">많은 아키텍처에는 다른 다운스트림 웹 API를 호출해야 하는 웹 API가 포함되어 있으며 둘 다 Azure AD B2C로 보안됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-109">Many architectures include a web API that needs to call another downstream web API, both secured by Azure AD B2C.</span></span> <span data-ttu-id="466a5-110">이 시나리오는 웹 API 백 엔드를 포함하는 네이티브 클라이언트에서 일반적이며, Web API 백 엔드가 다시 Azure AD Graph API와 같은 Microsoft 온라인 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-110">This scenario is common in native clients that have a web API back end, which in turn calls a Microsoft online service such as the Azure AD Graph API.</span></span>
>
> <span data-ttu-id="466a5-111">On-Behalf-Of 흐름이라고도 하는 OAuth 2.0 JWT 전달자 자격 증명 권한 부여를 사용하여 이 연결된 웹 API 시나리오를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-111">This chained web API scenario can be supported by using the OAuth 2.0 JWT Bearer Credential grant, otherwise known as the On-Behalf-Of flow.</span></span> <span data-ttu-id="466a5-112">그러나 On-Behalf-Of 흐름은 현재 Azure AD B2C에 구현되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-112">However, the On-Behalf-Of flow is not currently implemented in Azure AD B2C.</span></span>

## <a name="register-a-web-api-and-publish-permissions"></a><span data-ttu-id="466a5-113">웹 API 등록 및 권한 게시</span><span class="sxs-lookup"><span data-stu-id="466a5-113">Register a web API and publish permissions</span></span>

<span data-ttu-id="466a5-114">액세스 토큰을 요청하기 전에 먼저 웹 API를 등록하고 클라이언트 응용 프로그램에 부여할 수 있는 권한(범위)을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-114">Before requesting an access token, you first need to register a web API and publish permissions (scopes) that can be granted to the client application.</span></span>

### <a name="register-a-web-api"></a><span data-ttu-id="466a5-115">웹 API 등록</span><span class="sxs-lookup"><span data-stu-id="466a5-115">Register a web API</span></span>

1. <span data-ttu-id="466a5-116">Azure Portal의 B2C 기능 블레이드에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-116">On the B2C features blade on the Azure portal, click **Applications**.</span></span>
1. <span data-ttu-id="466a5-117">블레이드의 위쪽에서 **+추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-117">Click **+Add** at the top of the blade.</span></span>
1. <span data-ttu-id="466a5-118">소비자에게 응용 프로그램을 설명하는 응용 프로그램의 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-118">Enter a **Name** for the application that will describe your application to consumers.</span></span> <span data-ttu-id="466a5-119">예를 들어 "Contoso API"를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-119">For example, you could enter "Contoso API".</span></span>
1. <span data-ttu-id="466a5-120">**웹앱/ 웹 API 포함** 스위치를 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-120">Toggle the **Include web app / web API** switch to **Yes**.</span></span>
1. <span data-ttu-id="466a5-121">**회신 URL**에 대한 임의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-121">Enter an arbitrary value for the **Reply URLs**.</span></span> <span data-ttu-id="466a5-122">예를 들어 `https://localhost:44316/`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-122">For example, enter `https://localhost:44316/`.</span></span> <span data-ttu-id="466a5-123">API가 Azure AD B2C에서 직접 토큰을 받지 않아야 하므로 값은 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-123">The value does not matter since an API should not be receiving the token directly from Azure AD B2C.</span></span>
1. <span data-ttu-id="466a5-124">**앱 ID URI**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-124">Enter an **App ID URI**.</span></span> <span data-ttu-id="466a5-125">Web API에 사용되는 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-125">This is the identifier used for your web API.</span></span> <span data-ttu-id="466a5-126">예를 들어 상자에 '참고'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-126">For example, enter 'notes' in the box.</span></span> <span data-ttu-id="466a5-127">**앱 ID URI**는 `https://{tenantName}.onmicrosoft.com/notes`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-127">The **App ID URI** would then be `https://{tenantName}.onmicrosoft.com/notes`.</span></span>
1. <span data-ttu-id="466a5-128">**만들기** 를 클릭하여 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-128">Click **Create** to register your application.</span></span>
1. <span data-ttu-id="466a5-129">방금 만든 응용 프로그램을 클릭하고, 나중에 코드에서 사용할 전역적으로 고유한 **응용 프로그램 클라이언트 ID** 를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-129">Click the application that you just created and copy down the globally unique **Application Client ID** that you'll use later in your code.</span></span>

### <a name="publishing-permissions"></a><span data-ttu-id="466a5-130">권한 게시</span><span class="sxs-lookup"><span data-stu-id="466a5-130">Publishing permissions</span></span>

<span data-ttu-id="466a5-131">권한과 유사한 범위는 앱에서 API를 호출하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-131">Scopes, which are analogous to permissions, are necessary when your app is calling an API.</span></span> <span data-ttu-id="466a5-132">범위의 일부 예는 "읽기" 또는 "쓰기"입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-132">Some examples of scopes are "read" or "write".</span></span> <span data-ttu-id="466a5-133">웹 또는 네이티브 앱이 API에서 "읽기"를 원한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-133">Suppose you want your web or native app to "read" from an API.</span></span> <span data-ttu-id="466a5-134">앱은 Azure AD B2C를 호출하고 범위 "읽기"에 대한 액세스를 제공하는 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-134">Your app would call Azure AD B2C and request an access token that gives access to the scope "read".</span></span> <span data-ttu-id="466a5-135">Azure AD B2C가 이러한 액세스 토큰을 내보내기 위해 앱은 특정 API에서 "읽기"에 대한 권한을 부여 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-135">In order for Azure AD B2C to emit such an access token, the app needs to be granted permission to "read" from the specific API.</span></span> <span data-ttu-id="466a5-136">이렇게 하려면 API는 먼저 "읽기" 범위를 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-136">To do this, your API first needs to publish the "read" scope.</span></span>

1. <span data-ttu-id="466a5-137">Azure AD B2C **응용 프로그램** 블레이드 내에서 웹 API 응용 프로그램("Contoso API")을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-137">Within the Azure AD B2C **Applications** blade, open the web API application ("Contoso API").</span></span>
1. <span data-ttu-id="466a5-138">**게시된 범위**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-138">Click on **Published scopes**.</span></span> <span data-ttu-id="466a5-139">다른 응용 프로그램에 부여할 수 있는 사용 권한(범위)을 정의한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-139">This is where you define the permissions (scopes) that can be granted to other applications.</span></span>
1. <span data-ttu-id="466a5-140">필요에 따라 **범위 값**을 추가합니다(예: "읽기").</span><span class="sxs-lookup"><span data-stu-id="466a5-140">Add **Scope Values** as necessary (for example, "read").</span></span> <span data-ttu-id="466a5-141">기본적으로 "user_impersonation" 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-141">By default, the "user_impersonation" scope will be defined.</span></span> <span data-ttu-id="466a5-142">원하는 경우 이를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-142">You can ignore this if you wish.</span></span> <span data-ttu-id="466a5-143">**범위 이름** 열에 범위에 대한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-143">Enter a description of the scope in the **Scope Name** column.</span></span>
1. <span data-ttu-id="466a5-144">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-144">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="466a5-145">**범위 이름**은 **범위 값**에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-145">The **Scope Name** is the description of the **Scope Value**.</span></span> <span data-ttu-id="466a5-146">범위를 사용할 때 **범위 값**을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-146">When using the scope, make sure to use the **Scope Value**.</span></span>

## <a name="grant-a-native-or-web-app-permissions-to-a-web-api"></a><span data-ttu-id="466a5-147">웹 API에 네이티브 또는 웹앱 권한 부여</span><span class="sxs-lookup"><span data-stu-id="466a5-147">Grant a native or web app permissions to a web API</span></span>

<span data-ttu-id="466a5-148">API가 범위를 게시하도록 구성되면 클라이언트 응용 프로그램은 Azure Portal을 통해 해당 범위 권한을 부여 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-148">Once an API is configured to publish scopes, the client application needs to be granted those scopes via the Azure portal.</span></span>

1. <span data-ttu-id="466a5-149">B2C 기능 블레이드의 **응용 프로그램** 메뉴로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-149">Navigate to the **Applications** menu in the B2C features blade.</span></span>
1. <span data-ttu-id="466a5-150">이미 없는 클라이언트 응용 프로그램([웹앱](active-directory-b2c-app-registration.md#register-a-web-app) 또는 [네이티브 클라이언트](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app))을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-150">Register a client application ([web app](active-directory-b2c-app-registration.md#register-a-web-app) or [native client](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) if you don’t have one already.</span></span> <span data-ttu-id="466a5-151">시작 지점부터 이 가이드를 따르는 경우 클라이언트 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-151">If you are following this guide as your starting point, you'll need to register a client application.</span></span>
1. <span data-ttu-id="466a5-152">**API 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-152">Click on **API access**.</span></span>
1. <span data-ttu-id="466a5-153">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-153">Click on **Add**.</span></span>
1. <span data-ttu-id="466a5-154">웹 API 및 부여하려는 범위(권한)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-154">Select your web API and the scopes (permissions) you would like to grant.</span></span>
1. <span data-ttu-id="466a5-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-155">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="466a5-156">Azure AD B2C는 클라이언트 응용 프로그램 사용자의 동의를 묻지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-156">Azure AD B2C does not ask your client application users for their consent.</span></span> <span data-ttu-id="466a5-157">대신 모든 동의는 위에서 설명한 응용 프로그램 간에 구성된 권한에 따라 관리자에 의해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-157">Instead, all consent is provided by the admin, based on the permissions configured between the applications described above.</span></span> <span data-ttu-id="466a5-158">응용 프로그램에 대한 권한 부여가 해지되면 이전에 해당 권한을 획득할 수 있었던 모든 사용자는 더 이상 권한을 획득할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-158">If a permission grant for an application is revoked, all users who were previously able to acquire that permission will no longer be able to do so.</span></span>

## <a name="requesting-a-token"></a><span data-ttu-id="466a5-159">토큰 요청</span><span class="sxs-lookup"><span data-stu-id="466a5-159">Requesting a token</span></span>

<span data-ttu-id="466a5-160">액세스 토큰을 요청할 때 클라이언트 응용 프로그램에서 요청의 **범위** 매개 변수에서 원하는 권한을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-160">When requesting an access token, the client application needs to specify the desired permissions in the **scope** parameter of the request.</span></span> <span data-ttu-id="466a5-161">예를 들어 `https://contoso.onmicrosoft.com/notes`의 **앱 ID URI**가 있는 API에 대한 **범위 값** "읽기"를 지정하기 위해 범위는 `https://contoso.onmicrosoft.com/notes/read`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-161">For example, to specify the **Scope Value** “read” for the API that has the **App ID URI** of `https://contoso.onmicrosoft.com/notes`, the scope would be `https://contoso.onmicrosoft.com/notes/read`.</span></span> <span data-ttu-id="466a5-162">다음은 `/authorize` 끝점에 대한 인증 코드 요청의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-162">Below is an example of an authorization code request to the `/authorize` endpoint.</span></span>

> [!NOTE]
> <span data-ttu-id="466a5-163">현재 사용자 지정 도메인은 액세스 토큰과 함께 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-163">Currently, custom domains are not supported along with access tokens.</span></span> <span data-ttu-id="466a5-164">요청 URL에서 tenantName.onmicrosoft.com 도메인을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-164">You must use your tenantName.onmicrosoft.com domain in the request URL.</span></span>

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

<span data-ttu-id="466a5-165">같은 요청에 여러 권한을 얻기 위해 단일 **범위** 매개 변수에 공백으로 구분된 여러 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-165">To acquire multiple permissions in the same request, you can add multiple entries in the single **scope** parameter, separated by spaces.</span></span> <span data-ttu-id="466a5-166">예:</span><span class="sxs-lookup"><span data-stu-id="466a5-166">For example:</span></span>

<span data-ttu-id="466a5-167">디코딩된 URL:</span><span class="sxs-lookup"><span data-stu-id="466a5-167">URL decoded:</span></span>

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

<span data-ttu-id="466a5-168">인코딩된 URL:</span><span class="sxs-lookup"><span data-stu-id="466a5-168">URL encoded:</span></span>

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

<span data-ttu-id="466a5-169">클라이언트 응용 프로그램에 부여된 것보다 더 많은 범위(권한)를 리소스에 대해 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-169">You may request more scopes (permissions) for a resource than what is granted for your client application.</span></span> <span data-ttu-id="466a5-170">이 경우 하나 이상의 권한이 부여되면 호출이 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-170">When this is the case, the call will succeed if at least one permission is granted.</span></span> <span data-ttu-id="466a5-171">결과 **액세스\_토큰**은 성공적으로 부여된 권한으로 채워진 해당 "scp" 클레임을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-171">The resulting **access\_token** will have its “scp” claim populated with only the permissions that were successfully granted.</span></span>

> [!NOTE] 
> <span data-ttu-id="466a5-172">동일한 요청에 두 개의 다른 웹 리소스에 대한 권한 요청을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-172">We do not support requesting permissions against two different web resources in the same request.</span></span> <span data-ttu-id="466a5-173">이러한 종류의 요청은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-173">This kind of request will fail.</span></span>

### <a name="special-cases"></a><span data-ttu-id="466a5-174">특수 사례</span><span class="sxs-lookup"><span data-stu-id="466a5-174">Special cases</span></span>

<span data-ttu-id="466a5-175">OpenID Connect 표준은 몇 가지 특별한 "범위" 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-175">The OpenID Connect standard specifies several special “scope” values.</span></span> <span data-ttu-id="466a5-176">다음과 같은 특별한 범위는 "사용자의 프로필에 액세스"에 대한 권한을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-176">The following special scopes represent the permission to “access the user’s profile”:</span></span>

* <span data-ttu-id="466a5-177">**openid**: ID 토큰 요청</span><span class="sxs-lookup"><span data-stu-id="466a5-177">**openid**: This requests an ID token</span></span>
* <span data-ttu-id="466a5-178">**오프라인\_액세스**: 새로 고침 토큰을 요청합니다([인증 코드 흐름](active-directory-b2c-reference-oauth-code.md) 사용).</span><span class="sxs-lookup"><span data-stu-id="466a5-178">**offline\_access**: This requests a refresh token (using [Auth Code flows](active-directory-b2c-reference-oauth-code.md)).</span></span>

<span data-ttu-id="466a5-179">`/authorize` 요청의 `response_type` 매개 변수가 `token`을 포함하는 경우 `scope` 매개 변수는 권한이 부여될 하나 이상의 리소스 범위(`openid` 및 `offline_access` 이외)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-179">If the `response_type` parameter in a `/authorize` request includes `token`, the `scope` parameter must include at least one resource scope (other than `openid` and `offline_access`) that will be granted.</span></span> <span data-ttu-id="466a5-180">그렇지 않은 경우 `/authorize` 요청은 실패와 함께 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-180">Otherwise, the `/authorize` request will terminate with a failure.</span></span>

## <a name="the-returned-token"></a><span data-ttu-id="466a5-181">반환된 토큰</span><span class="sxs-lookup"><span data-stu-id="466a5-181">The returned token</span></span>

<span data-ttu-id="466a5-182">성공적으로 생성된 **액세스\_토큰**(`/authorize` 또는 `/token` 끝점에서)에 다음 클레임이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-182">In a successfully minted **access\_token** (from either the `/authorize` or `/token` endpoint), the following claims will be present:</span></span>

| <span data-ttu-id="466a5-183">이름</span><span class="sxs-lookup"><span data-stu-id="466a5-183">Name</span></span> | <span data-ttu-id="466a5-184">클레임</span><span class="sxs-lookup"><span data-stu-id="466a5-184">Claim</span></span> | <span data-ttu-id="466a5-185">설명</span><span class="sxs-lookup"><span data-stu-id="466a5-185">Description</span></span> |
| --- | --- | --- |
|<span data-ttu-id="466a5-186">대상</span><span class="sxs-lookup"><span data-stu-id="466a5-186">Audience</span></span> |`aud` |<span data-ttu-id="466a5-187">토큰에서 액세스를 부여하는 단일 리소스의 **응용 프로그램 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-187">The **application ID** of the single resource that the token grants access to.</span></span> |
|<span data-ttu-id="466a5-188">범위</span><span class="sxs-lookup"><span data-stu-id="466a5-188">Scope</span></span> |`scp` |<span data-ttu-id="466a5-189">리소스에 부여된 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-189">The permissions granted to the resource.</span></span> <span data-ttu-id="466a5-190">여러 부여된 권한은 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-190">Multiple granted permissions will be separated by space.</span></span> |
|<span data-ttu-id="466a5-191">권한 있는 주체</span><span class="sxs-lookup"><span data-stu-id="466a5-191">Authorized Party</span></span> |`azp` |<span data-ttu-id="466a5-192">요청을 시작한 클라이언트 응용 프로그램의 **응용 프로그램 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-192">The **application ID** of the client application that initiated the request.</span></span> |

<span data-ttu-id="466a5-193">API에서 **액세스\_토큰**을 받으면 [토큰의 유효성을 검사](active-directory-b2c-reference-tokens.md)하여 토큰이 인증되었으며 올바른 클레임을 가졌음을 증명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466a5-193">When your API receives the **access\_token**, it must [validate the token](active-directory-b2c-reference-tokens.md) to prove that the token is authentic and has the correct claims.</span></span>

<span data-ttu-id="466a5-194">Microsoft는 사용자 의견 및 제안을 항상 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="466a5-194">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="466a5-195">이 항목에 문제가 있는 경우 태그 ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c)를 사용하여 Stack Overflow에 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="466a5-195">If you have any difficulties with this topic, please post on Stack Overflow using the tag ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c).</span></span> <span data-ttu-id="466a5-196">기능 요청이 있는 경우 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)에 추가해 주세요.</span><span class="sxs-lookup"><span data-stu-id="466a5-196">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

## <a name="next-steps"></a><span data-ttu-id="466a5-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="466a5-197">Next steps</span></span>

* <span data-ttu-id="466a5-198">[.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)를 사용하여 웹 API 빌드</span><span class="sxs-lookup"><span data-stu-id="466a5-198">Build a web API using [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)</span></span>
* <span data-ttu-id="466a5-199">[Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)를 사용하여 웹 API 빌드</span><span class="sxs-lookup"><span data-stu-id="466a5-199">Build a web API using [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)</span></span>
