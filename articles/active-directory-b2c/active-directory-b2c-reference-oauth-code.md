---
title: "인증 코드 흐름 - Azure AD B2C | Microsoft Docs"
description: "Azure AD B2C 및 OpenID Connect 인증 프로토콜을 사용하여 웹앱 빌드 방법을 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: dfc4f2e84704307ccbea6141c0dbc8d089733b22
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a><span data-ttu-id="de7f5-103">Azure Active Directory B2C: OAuth 2.0 인증 코드 흐름</span><span class="sxs-lookup"><span data-stu-id="de7f5-103">Azure Active Directory B2C: OAuth 2.0 authorization code flow</span></span>
<span data-ttu-id="de7f5-104">장치에 설치된 앱에서 OAuth 2.0 인증 코드 권한 부여를 사용하여 Web API와 같은 보호된 리소스에 대한 액세스 권한을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-104">You can use the OAuth 2.0 authorization code grant in apps installed on a device to gain access to protected resources, such as web APIs.</span></span> <span data-ttu-id="de7f5-105">OAuth 2.0의 Azure AD B2C(Azure Active Directory B2C) 구현을 사용하면 모바일 및 데스크톱 앱에 등록, 로그인 및 기타 ID 관리 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-105">By using the Azure Active Directory B2C (Azure AD B2C) implementation of OAuth 2.0, you can add sign-up, sign-in, and other identity management tasks to your mobile and desktop apps.</span></span> <span data-ttu-id="de7f5-106">이 문서는 언어 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-106">This article is language-independent.</span></span> <span data-ttu-id="de7f5-107">이 문서에서는 오픈 소스 라이브러리를 사용하지 않고 HTTP 메시지를 보내고 받는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-107">In the article, we describe how to send and receive HTTP messages without using any open-source libraries.</span></span>

<!-- TODO: Need link to libraries -->

<span data-ttu-id="de7f5-108">OAuth 2.0 인증 코드 흐름은 [OAuth 2.0 사양의 섹션 4.1](http://tools.ietf.org/html/rfc6749)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-108">The OAuth 2.0 authorization code flow is described in [section 4.1 of the OAuth 2.0 specification](http://tools.ietf.org/html/rfc6749).</span></span> <span data-ttu-id="de7f5-109">[웹앱](active-directory-b2c-apps.md#web-apps) 및 [기본적으로 설치된 앱](active-directory-b2c-apps.md#mobile-and-native-apps)을 포함하여 대부분의 앱 형식에서 인증 및 권한 부여에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-109">You can use it for authentication and authorization in most app types, including [web apps](active-directory-b2c-apps.md#web-apps) and [natively installed apps](active-directory-b2c-apps.md#mobile-and-native-apps).</span></span> <span data-ttu-id="de7f5-110">OAuth 2.0 인증 코드 흐름을 사용하여 [권한 부여 서버](active-directory-b2c-reference-protocols.md#the-basics)를 통해 보안된 리소스에 액세스하는 데 사용할 수 있는 *액세스 토큰*을 앱이 안전하게 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-110">You can use the OAuth 2.0 authorization code flow to securely acquire *access tokens* for your apps, which can be used to access resources that are secured by an [authorization server](active-directory-b2c-reference-protocols.md#the-basics).</span></span>

<span data-ttu-id="de7f5-111">이 문서에서는 **공용 클라이언트** OAuth 2.0 인증 코드 흐름을 중점적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-111">This article focuses on the **public clients** OAuth 2.0 authorization code flow.</span></span> <span data-ttu-id="de7f5-112">공용 클라이언트는 보안 암호의 무결성을 안전하게 유지하기 위해 신뢰할 수 없는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-112">A public client is any client application that cannot be trusted to securely maintain the integrity of a secret password.</span></span> <span data-ttu-id="de7f5-113">모바일 앱, 데스크톱 앱 및 기본적으로 장치에서 실행되고 액세스 토큰이 필요한 모든 응용 프로그램이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-113">This includes mobile apps, desktop apps, and essentially any application that runs on a device and needs to get access tokens.</span></span> 

> [!NOTE]
> <span data-ttu-id="de7f5-114">Azure AD B2C를 사용하여 ID 관리를 웹앱에 추가하려면 OAuth 2.0 대신 [OpenID Connect](active-directory-b2c-reference-oidc.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-114">To add identity management to a web app by using Azure AD B2C, use [OpenID Connect](active-directory-b2c-reference-oidc.md) instead of OAuth 2.0.</span></span>

<span data-ttu-id="de7f5-115">Azure AD B2C는 단순한 인증 및 권한 부여 보다 더 많은 작업으로 표준 OAuth 2.0의 흐름을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-115">Azure AD B2C extends the standard OAuth 2.0 flows to do more than simple authentication and authorization.</span></span> <span data-ttu-id="de7f5-116">Azure AD B2C는 [정책 매개 변수](active-directory-b2c-reference-policies.md)를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-116">It introduces the [policy parameter](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="de7f5-117">기본 제공 정책을 사용하면 OAuth 2.0을 통해 등록, 로그인 및 프로필 관리와 같은 사용자 환경을 앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-117">With built-in policies, you can use OAuth 2.0 to add user experiences to your app, such as sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="de7f5-118">이 문서에서는 OAuth 2.0 및 정책을 사용하여 네이티브 응용 프로그램에서 이러한 환경을 각각 구현하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-118">In this article, we show you how to use OAuth 2.0 and policies to implement each of these experiences in your native applications.</span></span> <span data-ttu-id="de7f5-119">또한 Web API에 액세스하기 위한 액세스 토큰을 얻는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-119">We also show you how to get access tokens for accessing web APIs.</span></span>

<span data-ttu-id="de7f5-120">이 문서의 예제 HTTP 요청에서는 샘플 Azure AD B2C 디렉터리인 **fabrikamb2c.onmicrosoft.com**을 사용합니다. 또한 응용 프로그램 예제 및 정책도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-120">In the example HTTP requests in this article, we use our sample Azure AD B2C directory, **fabrikamb2c.onmicrosoft.com**. We also use our sample application and policies.</span></span> <span data-ttu-id="de7f5-121">이러한 값을 사용하여 직접 요청을 시도하거나 사용자 고유의 값으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-121">You can try the requests yourself by using these values, or you can replace them with your own values.</span></span>
<span data-ttu-id="de7f5-122">[사용자 고유의 Azure AD B2C 디렉터리, 응용 프로그램 및 정책을 가져오는](#use-your-own-azure-ad-b2c-directory) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-122">Learn how to [get your own Azure AD B2C directory, application, and policies](#use-your-own-azure-ad-b2c-directory).</span></span>

## <a name="1-get-an-authorization-code"></a><span data-ttu-id="de7f5-123">1. 권한 부여 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="de7f5-123">1. Get an authorization code</span></span>
<span data-ttu-id="de7f5-124">인증 코드 흐름은 클라이언트가 사용자를 `/authorize` 끝점으로 보내는 것으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-124">The authorization code flow begins with the client directing the user to the `/authorize` endpoint.</span></span> <span data-ttu-id="de7f5-125">사용자가 조치를 취하는 흐름의 대화형 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-125">This is the interactive part of the flow, where the user takes action.</span></span> <span data-ttu-id="de7f5-126">이 요청에서 클라이언트는 사용자로부터 얻어야 하는 사용 권한을 `scope` 매개 변수에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-126">In this request, the client indicates in the `scope` parameter the permissions that it needs to acquire from the user.</span></span> <span data-ttu-id="de7f5-127">`p` 매개 변수에서 실행할 정책을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-127">In the `p` parameter, it indicates the policy to execute.</span></span> <span data-ttu-id="de7f5-128">다음 세 가지 예제(쉽게 읽을 수 있도록 줄 바꿈 적용)에서는 각각 다른 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-128">The following three examples (with line breaks for readability) each use a different policy.</span></span>

### <a name="use-a-sign-in-policy"></a><span data-ttu-id="de7f5-129">로그인 정책 사용</span><span class="sxs-lookup"><span data-stu-id="de7f5-129">Use a sign-in policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a><span data-ttu-id="de7f5-130">등록 정책 사용</span><span class="sxs-lookup"><span data-stu-id="de7f5-130">Use a sign-up policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a><span data-ttu-id="de7f5-131">편집 프로필 정책 사용</span><span class="sxs-lookup"><span data-stu-id="de7f5-131">Use an edit-profile policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| <span data-ttu-id="de7f5-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-132">Parameter</span></span> | <span data-ttu-id="de7f5-133">Required?</span><span class="sxs-lookup"><span data-stu-id="de7f5-133">Required?</span></span> | <span data-ttu-id="de7f5-134">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de7f5-135">client_id</span><span class="sxs-lookup"><span data-stu-id="de7f5-135">client_id</span></span> |<span data-ttu-id="de7f5-136">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-136">Required</span></span> |<span data-ttu-id="de7f5-137">[Azure Portal](https://portal.azure.com)에서 앱에 할당된 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-137">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="de7f5-138">response_type</span><span class="sxs-lookup"><span data-stu-id="de7f5-138">response_type</span></span> |<span data-ttu-id="de7f5-139">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-139">Required</span></span> |<span data-ttu-id="de7f5-140">응답 유형입니다. 인증 코드 흐름의 경우 `code`를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-140">The response type, which must include `code` for the authorization code flow.</span></span> |
| <span data-ttu-id="de7f5-141">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="de7f5-141">redirect_uri</span></span> |<span data-ttu-id="de7f5-142">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-142">Required</span></span> |<span data-ttu-id="de7f5-143">앱이 인증 응답을 보내고 받는 앱의 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-143">The redirect URI of your app, where authentication responses are sent and received by your app.</span></span> <span data-ttu-id="de7f5-144">URL로 인코드되어야 한다는 점을 제외하고 포털에서 등록한 리디렉션 URI 중 하나와 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-144">It must exactly match one of the redirect URIs that you registered in the portal, except that it must be URL-encoded.</span></span> |
| <span data-ttu-id="de7f5-145">scope</span><span class="sxs-lookup"><span data-stu-id="de7f5-145">scope</span></span> |<span data-ttu-id="de7f5-146">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-146">Required</span></span> |<span data-ttu-id="de7f5-147">공백으로 구분된 범위 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-147">A space-separated list of scopes.</span></span> <span data-ttu-id="de7f5-148">단일 범위 값은 요청되는 사용 권한을 Azure AD(Azure Active Directory)에 둘 다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-148">A single scope value indicates to Azure Active Directory (Azure AD) both of the permissions that are being requested.</span></span> <span data-ttu-id="de7f5-149">클라이언트 ID를 범위로 사용할 경우 동일한 클라이언트 ID가 나타내는 사용자 고유의 서비스 또는 Web API에 대해 사용할 수 있는 액세스 토큰이 앱에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-149">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="de7f5-150">`offline_access` 범위는 리소스에 대한 장기 액세스를 위해 앱에 새로 고침 토큰이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-150">The `offline_access` scope indicates that your app needs a refresh token for long-lived access to resources.</span></span> <span data-ttu-id="de7f5-151">`openid` 범위를 사용하여 Azure AD B2C에서 ID 토큰을 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-151">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="de7f5-152">response_mode</span><span class="sxs-lookup"><span data-stu-id="de7f5-152">response_mode</span></span> |<span data-ttu-id="de7f5-153">권장</span><span class="sxs-lookup"><span data-stu-id="de7f5-153">Recommended</span></span> |<span data-ttu-id="de7f5-154">결과로 생성된 인증 코드를 앱에 다시 보내는 데 사용하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-154">The method that you use to send the resulting authorization code back to your app.</span></span> <span data-ttu-id="de7f5-155">`query`, `form_post` 또는 `fragment`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-155">It can be `query`, `form_post`, or `fragment`.</span></span> |
| <span data-ttu-id="de7f5-156">state</span><span class="sxs-lookup"><span data-stu-id="de7f5-156">state</span></span> |<span data-ttu-id="de7f5-157">권장</span><span class="sxs-lookup"><span data-stu-id="de7f5-157">Recommended</span></span> |<span data-ttu-id="de7f5-158">토큰 응답에 반환되는 요청에 포함된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-158">A value included in the request that is returned in the token response.</span></span> <span data-ttu-id="de7f5-159">사용하려는 임의 콘텐츠의 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-159">It can be a string of any content that you want to use.</span></span> <span data-ttu-id="de7f5-160">일반적으로 교차 사이트 요청 위조 공격을 방지하기 위해 임의로 생성된 고유 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-160">Usually, a randomly generated unique value is  used, to prevent cross-site request forgery attacks.</span></span> <span data-ttu-id="de7f5-161">또한 상태는 인증 요청이 발생하기 전에 앱에서 사용자 상태에 대한 정보를 인코드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-161">The state also is used to encode information about the user's state in the app before the authentication request occurred.</span></span> <span data-ttu-id="de7f5-162">예를 들어 사용자가 보고 있던 페이지 또는 실행 중이었던 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-162">For example, the page the user was on, or the policy that was being executed.</span></span> |
| <span data-ttu-id="de7f5-163">p</span><span class="sxs-lookup"><span data-stu-id="de7f5-163">p</span></span> |<span data-ttu-id="de7f5-164">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-164">Required</span></span> |<span data-ttu-id="de7f5-165">실행되는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-165">The policy that is executed.</span></span> <span data-ttu-id="de7f5-166">Azure AD B2C 디렉터리에 생성된 정책의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-166">It's the name of a policy that is created in your Azure AD B2C directory.</span></span> <span data-ttu-id="de7f5-167">정책 이름 값은 **b2c\_1\_**로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-167">The policy name value should begin with **b2c\_1\_**.</span></span> <span data-ttu-id="de7f5-168">정책에 대한 자세한 내용은 [Azure AD B2C 기본 제공 정책](active-directory-b2c-reference-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de7f5-168">To learn more about policies, see [Azure AD B2C built-in policies](active-directory-b2c-reference-policies.md).</span></span> |
| <span data-ttu-id="de7f5-169">prompt</span><span class="sxs-lookup"><span data-stu-id="de7f5-169">prompt</span></span> |<span data-ttu-id="de7f5-170">옵션</span><span class="sxs-lookup"><span data-stu-id="de7f5-170">Optional</span></span> |<span data-ttu-id="de7f5-171">필요한 사용자 상호 작용 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-171">The type of user interaction that is required.</span></span> <span data-ttu-id="de7f5-172">현재 유효한 값은 `login`뿐이며, 강제로 사용자가 해당 요청에 자격 증명을 입력하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-172">Currently, the only valid value is `login`, which forces the user to enter their credentials on that request.</span></span> <span data-ttu-id="de7f5-173">Single Sign-On은 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-173">Single sign-on will not take effect.</span></span> |

<span data-ttu-id="de7f5-174">이 시점에서 정책의 워크플로를 완료하도록 사용자에게 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-174">At this point, the user is asked to complete the policy's workflow.</span></span> <span data-ttu-id="de7f5-175">이 경우 사용자 이름과 암호를 입력하거나, 소셜 ID로 로그인하거나, 디렉터리를 등록하거나, 다른 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-175">This might involve the user entering their username and password, signing in with a social identity, signing up for the directory, or any other number of steps.</span></span> <span data-ttu-id="de7f5-176">사용자 작업은 정책을 정의한 방식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-176">User actions depend on how the policy is defined.</span></span>

<span data-ttu-id="de7f5-177">사용자가 정책을 완료하면 Azure AD에서 앱에 대한 응답을 `redirect_uri`에 사용한 값으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-177">After the user completes the policy, Azure AD returns a response to your app at the value you used for `redirect_uri`.</span></span> <span data-ttu-id="de7f5-178">`response_mode` 매개 변수에 지정된 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-178">It uses the method specified in the `response_mode` parameter.</span></span> <span data-ttu-id="de7f5-179">응답은 실행된 정책과 별개로, 각 사용자 작업 시나리오에서 정확히 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-179">The response is exactly the same for each of the user action scenarios, independent of the policy that was executed.</span></span>

<span data-ttu-id="de7f5-180">`response_mode=query`를 사용하는 성공적인 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-180">A successful response that uses `response_mode=query` looks like this:</span></span>

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // the authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // the value provided in the request
```

| <span data-ttu-id="de7f5-181">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-181">Parameter</span></span> | <span data-ttu-id="de7f5-182">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-183">코드</span><span class="sxs-lookup"><span data-stu-id="de7f5-183">code</span></span> |<span data-ttu-id="de7f5-184">앱이 요청한 권한 부여 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-184">The authorization code that the app requested.</span></span> <span data-ttu-id="de7f5-185">앱은 인증 코드를 사용하여 대상 리소스에 대한 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-185">The app can use the authorization code to request an access token for a target resource.</span></span> <span data-ttu-id="de7f5-186">인증 코드는 수명이 매우 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-186">Authorization codes are very short-lived.</span></span> <span data-ttu-id="de7f5-187">일반적으로 약 10분 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-187">Typically, they expire after about 10 minutes.</span></span> |
| <span data-ttu-id="de7f5-188">state</span><span class="sxs-lookup"><span data-stu-id="de7f5-188">state</span></span> |<span data-ttu-id="de7f5-189">전체 설명은 이전 섹션의 첫 번째 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de7f5-189">See the full description in the table in the preceding section.</span></span> <span data-ttu-id="de7f5-190">요청에 `state` 매개 변수가 포함되어 있으면 동일한 값이 응답에도 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-190">If a `state` parameter is included in the request, the same value should appear in the response.</span></span> <span data-ttu-id="de7f5-191">앱은 요청 및 응답의 `state` 값이 동일한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-191">The app should verify that the `state` values in the request and response are identical.</span></span> |

<span data-ttu-id="de7f5-192">앱이 적절하게 처리할 수 있도록 오류 응답을 리디렉션 URI로 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-192">Error responses also can be sent to the redirect URI so that the app can handle them appropriately:</span></span>

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| <span data-ttu-id="de7f5-193">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-193">Parameter</span></span> | <span data-ttu-id="de7f5-194">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-195">error</span><span class="sxs-lookup"><span data-stu-id="de7f5-195">error</span></span> |<span data-ttu-id="de7f5-196">발생한 오류 유형을 분류하는 데 사용할 수 있는 오류 코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-196">An error code string that you can use to classify the types of errors that occur.</span></span> <span data-ttu-id="de7f5-197">문자열을 사용하여 오류에 대응할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-197">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="de7f5-198">error_description</span><span class="sxs-lookup"><span data-stu-id="de7f5-198">error_description</span></span> |<span data-ttu-id="de7f5-199">인증 오류의 근본 원인을 식별하도록 도울 수 있는 특정 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-199">A specific error message that can help you identify the root cause of an authentication error.</span></span> |
| <span data-ttu-id="de7f5-200">state</span><span class="sxs-lookup"><span data-stu-id="de7f5-200">state</span></span> |<span data-ttu-id="de7f5-201">잎의 표에 나와 있는 전체 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de7f5-201">See the full description in the preceding table.</span></span> <span data-ttu-id="de7f5-202">요청에 `state` 매개 변수가 포함되어 있으면 동일한 값이 응답에도 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-202">If a `state` parameter is included in the request, the same value should appear in the response.</span></span> <span data-ttu-id="de7f5-203">앱은 요청 및 응답의 `state` 값이 동일한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-203">The app should verify that the `state` values in the request and response are identical.</span></span> |

## <a name="2-get-a-token"></a><span data-ttu-id="de7f5-204">2. 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="de7f5-204">2. Get a token</span></span>
<span data-ttu-id="de7f5-205">인증 코드를 받았으므로 이제 POST 요청을 `/token` 끝점으로 전송하여 `code`를 의도한 리소스에 대한 토큰으로 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-205">Now that you've acquired an authorization code, you can redeem the `code` for a token to the intended resource by sending a POST request to the `/token` endpoint.</span></span> <span data-ttu-id="de7f5-206">Azure AD B2C에서 토큰을 요청할 수 있는 리소스는 앱 자체의 백 엔드 Web API뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-206">In Azure AD B2C, the only resource that you can request a token for is your app's own back-end web API.</span></span> <span data-ttu-id="de7f5-207">자체 토큰을 요청하는 데 사용되는 규칙은 앱의 클라이언트 ID를 범위로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-207">The convention that's used for requesting a token to yourself is to use your app's client ID as the scope:</span></span>

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| <span data-ttu-id="de7f5-208">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-208">Parameter</span></span> | <span data-ttu-id="de7f5-209">Required?</span><span class="sxs-lookup"><span data-stu-id="de7f5-209">Required?</span></span> | <span data-ttu-id="de7f5-210">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-210">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de7f5-211">p</span><span class="sxs-lookup"><span data-stu-id="de7f5-211">p</span></span> |<span data-ttu-id="de7f5-212">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-212">Required</span></span> |<span data-ttu-id="de7f5-213">권한 부여 코드를 획득하는 데 사용된 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-213">The policy that was used to acquire the authorization code.</span></span> <span data-ttu-id="de7f5-214">이 요청에 다른 정책을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-214">You cannot use a different policy in this request.</span></span> <span data-ttu-id="de7f5-215">이 매개 변수는 POST 본문이 아니라 *쿼리 문자열*에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-215">Note that you add this parameter to the *query string*, not in the POST body.</span></span> |
| <span data-ttu-id="de7f5-216">client_id</span><span class="sxs-lookup"><span data-stu-id="de7f5-216">client_id</span></span> |<span data-ttu-id="de7f5-217">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-217">Required</span></span> |<span data-ttu-id="de7f5-218">[Azure Portal](https://portal.azure.com)에서 앱에 할당된 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-218">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="de7f5-219">grant_type</span><span class="sxs-lookup"><span data-stu-id="de7f5-219">grant_type</span></span> |<span data-ttu-id="de7f5-220">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-220">Required</span></span> |<span data-ttu-id="de7f5-221">권한 부여 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-221">The type of grant.</span></span> <span data-ttu-id="de7f5-222">인증 코드 흐름에서 권한 부여 유형은 `authorization_code`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-222">For the authorization code flow, the grant type must be `authorization_code`.</span></span> |
| <span data-ttu-id="de7f5-223">scope</span><span class="sxs-lookup"><span data-stu-id="de7f5-223">scope</span></span> |<span data-ttu-id="de7f5-224">권장</span><span class="sxs-lookup"><span data-stu-id="de7f5-224">Recommended</span></span> |<span data-ttu-id="de7f5-225">공백으로 구분된 범위 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-225">A space-separated list of scopes.</span></span> <span data-ttu-id="de7f5-226">단일 범위 값은 요청된 사용 권한을 모두 Azure AD에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-226">A single scope value indicates to Azure AD both of the permissions that are being requested.</span></span> <span data-ttu-id="de7f5-227">클라이언트 ID를 범위로 사용할 경우 동일한 클라이언트 ID가 나타내는 사용자 고유의 서비스 또는 Web API에 대해 사용할 수 있는 액세스 토큰이 앱에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-227">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="de7f5-228">`offline_access` 범위는 리소스에 대한 장기 액세스를 위해 앱에 새로 고침 토큰이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-228">The `offline_access` scope indicates that your app needs a refresh token for long-lived access to resources.</span></span>  <span data-ttu-id="de7f5-229">`openid` 범위를 사용하여 Azure AD B2C에서 ID 토큰을 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-229">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="de7f5-230">코드</span><span class="sxs-lookup"><span data-stu-id="de7f5-230">code</span></span> |<span data-ttu-id="de7f5-231">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-231">Required</span></span> |<span data-ttu-id="de7f5-232">흐름의 첫 번째 단계에서 얻은 권한 부여 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-232">The authorization code that you acquired in the first leg of the flow.</span></span> |
| <span data-ttu-id="de7f5-233">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="de7f5-233">redirect_uri</span></span> |<span data-ttu-id="de7f5-234">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-234">Required</span></span> |<span data-ttu-id="de7f5-235">인증 코드를 받은 응용 프로그램의 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-235">The redirect URI of the application where you received the authorization code.</span></span> |

<span data-ttu-id="de7f5-236">성공적인 토큰 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-236">A successful token response looks like this:</span></span>

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| <span data-ttu-id="de7f5-237">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-237">Parameter</span></span> | <span data-ttu-id="de7f5-238">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-238">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-239">not_before</span><span class="sxs-lookup"><span data-stu-id="de7f5-239">not_before</span></span> |<span data-ttu-id="de7f5-240">epoch 시간에서 토큰은 유효한 것으로 간주되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-240">The time at which the token is considered valid, in epoch time.</span></span> |
| <span data-ttu-id="de7f5-241">token_type</span><span class="sxs-lookup"><span data-stu-id="de7f5-241">token_type</span></span> |<span data-ttu-id="de7f5-242">토큰 형식 값입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-242">The token type value.</span></span> <span data-ttu-id="de7f5-243">Azure AD는 전달자 유형만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-243">The only type that Azure AD supports is Bearer.</span></span> |
| <span data-ttu-id="de7f5-244">access_token</span><span class="sxs-lookup"><span data-stu-id="de7f5-244">access_token</span></span> |<span data-ttu-id="de7f5-245">사용자가 요청한 서명된 JWT(JSON Web Token)입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-245">The signed JSON Web Token (JWT) that you requested.</span></span> |
| <span data-ttu-id="de7f5-246">scope</span><span class="sxs-lookup"><span data-stu-id="de7f5-246">scope</span></span> |<span data-ttu-id="de7f5-247">토큰이 유효한 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-247">The scopes that the token is valid for.</span></span> <span data-ttu-id="de7f5-248">또한 나중에 사용할 수 있도록 범위를 사용하여 토큰을 캐시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-248">You also can use scopes to cache tokens for later use.</span></span> |
| <span data-ttu-id="de7f5-249">expires_in</span><span class="sxs-lookup"><span data-stu-id="de7f5-249">expires_in</span></span> |<span data-ttu-id="de7f5-250">토큰이 유효한 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-250">The length of time that the token is valid (in seconds).</span></span> |
| <span data-ttu-id="de7f5-251">refresh_token</span><span class="sxs-lookup"><span data-stu-id="de7f5-251">refresh_token</span></span> |<span data-ttu-id="de7f5-252">OAuth 2.0 새로 고침 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-252">An OAuth 2.0 refresh token.</span></span> <span data-ttu-id="de7f5-253">앱은 현재 토큰이 만료된 후 이 토큰을 사용하여 추가 토큰을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-253">The app can use this token to acquire additional tokens after the current token expires.</span></span> <span data-ttu-id="de7f5-254">새로 고침 토큰은 장기적으로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-254">Refresh tokens are long-lived.</span></span> <span data-ttu-id="de7f5-255">토큰을 사용하여 오랜 시간 동안 리소스에 대한 액세스를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-255">You can use them to retain access to resources for extended periods of time.</span></span> <span data-ttu-id="de7f5-256">자세한 내용은 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de7f5-256">For more information, see the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span> |

<span data-ttu-id="de7f5-257">오류 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-257">Error responses look like this:</span></span>

```
{
    "error": "access_denied",
    "error_description": "The user revoked access to the app.",
}
```

| <span data-ttu-id="de7f5-258">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-258">Parameter</span></span> | <span data-ttu-id="de7f5-259">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-259">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-260">error</span><span class="sxs-lookup"><span data-stu-id="de7f5-260">error</span></span> |<span data-ttu-id="de7f5-261">발생한 오류 유형을 분류하는 데 사용할 수 있는 오류 코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-261">An error code string that you can use to classify the types of errors that occur.</span></span> <span data-ttu-id="de7f5-262">문자열을 사용하여 오류에 대응할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-262">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="de7f5-263">error_description</span><span class="sxs-lookup"><span data-stu-id="de7f5-263">error_description</span></span> |<span data-ttu-id="de7f5-264">인증 오류의 근본 원인을 식별하도록 도울 수 있는 특정 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-264">A specific error message that can help you identify the root cause of an authentication error.</span></span> |

## <a name="3-use-the-token"></a><span data-ttu-id="de7f5-265">3. 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="de7f5-265">3. Use the token</span></span>
<span data-ttu-id="de7f5-266">액세스 토큰을 성공적으로 얻었으므로 이제 `Authorization` 헤더에 포함하여 백 엔드 Web API에 대한 요청에 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-266">Now that you've successfully acquired an access token, you can use the token in requests to your back-end web APIs by including it in the `Authorization` header:</span></span>

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-the-token"></a><span data-ttu-id="de7f5-267">4. 토큰 새로 고침</span><span class="sxs-lookup"><span data-stu-id="de7f5-267">4. Refresh the token</span></span>
<span data-ttu-id="de7f5-268">액세스 토큰 및 ID 토큰은 수명이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-268">Access tokens and ID tokens are short-lived.</span></span> <span data-ttu-id="de7f5-269">만료되면 새로 고쳐야 리소스에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-269">After they expire, you must refresh them to continue to access resources.</span></span> <span data-ttu-id="de7f5-270">이렇게 하려면 다른 POST 요청을 `/token` 끝점에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-270">To do this, submit another POST request to the `/token` endpoint.</span></span> <span data-ttu-id="de7f5-271">여기에서는 `code` 대신 `refresh_token`을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-271">This time, provide the `refresh_token` instead of the `code`:</span></span>

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| <span data-ttu-id="de7f5-272">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-272">Parameter</span></span> | <span data-ttu-id="de7f5-273">Required?</span><span class="sxs-lookup"><span data-stu-id="de7f5-273">Required?</span></span> | <span data-ttu-id="de7f5-274">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-274">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de7f5-275">p</span><span class="sxs-lookup"><span data-stu-id="de7f5-275">p</span></span> |<span data-ttu-id="de7f5-276">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-276">Required</span></span> |<span data-ttu-id="de7f5-277">원래의 새로 고침 토큰을 얻는 데 사용된 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-277">The policy that was used to acquire the original refresh token.</span></span> <span data-ttu-id="de7f5-278">이 요청에 다른 정책을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-278">You cannot use a different policy in this request.</span></span> <span data-ttu-id="de7f5-279">이 매개 변수는 POST 본문이 아니라 *쿼리 문자열*에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-279">Note that you add this parameter to the *query string*, not in the POST body.</span></span> |
| <span data-ttu-id="de7f5-280">client_id</span><span class="sxs-lookup"><span data-stu-id="de7f5-280">client_id</span></span> |<span data-ttu-id="de7f5-281">권장</span><span class="sxs-lookup"><span data-stu-id="de7f5-281">Recommended</span></span> |<span data-ttu-id="de7f5-282">[Azure Portal](https://portal.azure.com)에서 앱에 할당된 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-282">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="de7f5-283">grant_type</span><span class="sxs-lookup"><span data-stu-id="de7f5-283">grant_type</span></span> |<span data-ttu-id="de7f5-284">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-284">Required</span></span> |<span data-ttu-id="de7f5-285">권한 부여 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-285">The type of grant.</span></span> <span data-ttu-id="de7f5-286">이 인증 코드 흐름 레그에서 권한 부여 유형은 `refresh_token`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-286">For this leg of the authorization code flow, the grant type must be `refresh_token`.</span></span> |
| <span data-ttu-id="de7f5-287">scope</span><span class="sxs-lookup"><span data-stu-id="de7f5-287">scope</span></span> |<span data-ttu-id="de7f5-288">권장</span><span class="sxs-lookup"><span data-stu-id="de7f5-288">Recommended</span></span> |<span data-ttu-id="de7f5-289">공백으로 구분된 범위 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-289">A space-separated list of scopes.</span></span> <span data-ttu-id="de7f5-290">단일 범위 값은 요청된 사용 권한을 모두 Azure AD에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-290">A single scope value indicates to Azure AD both of the permissions that are being requested.</span></span> <span data-ttu-id="de7f5-291">클라이언트 ID를 범위로 사용할 경우 동일한 클라이언트 ID가 나타내는 사용자 고유의 서비스 또는 Web API에 대해 사용할 수 있는 액세스 토큰이 앱에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-291">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="de7f5-292">`offline_access` 범위는 리소스에 대한 장기 액세스를 위해 앱에 새로 고침 토큰이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-292">The `offline_access` scope indicates that your app will need a refresh token for long-lived access to resources.</span></span>  <span data-ttu-id="de7f5-293">`openid` 범위를 사용하여 Azure AD B2C에서 ID 토큰을 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-293">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="de7f5-294">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="de7f5-294">redirect_uri</span></span> |<span data-ttu-id="de7f5-295">옵션</span><span class="sxs-lookup"><span data-stu-id="de7f5-295">Optional</span></span> |<span data-ttu-id="de7f5-296">인증 코드를 받은 응용 프로그램의 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-296">The redirect URI of the application where you received the authorization code.</span></span> |
| <span data-ttu-id="de7f5-297">refresh_token</span><span class="sxs-lookup"><span data-stu-id="de7f5-297">refresh_token</span></span> |<span data-ttu-id="de7f5-298">필수</span><span class="sxs-lookup"><span data-stu-id="de7f5-298">Required</span></span> |<span data-ttu-id="de7f5-299">흐름의 두 번째 레그에서 얻은 원본 새로 고침 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-299">The original refresh token that you acquired in the second leg of the flow.</span></span> |

<span data-ttu-id="de7f5-300">성공적인 토큰 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-300">A successful token response looks like this:</span></span>

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| <span data-ttu-id="de7f5-301">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-301">Parameter</span></span> | <span data-ttu-id="de7f5-302">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-302">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-303">not_before</span><span class="sxs-lookup"><span data-stu-id="de7f5-303">not_before</span></span> |<span data-ttu-id="de7f5-304">epoch 시간에서 토큰은 유효한 것으로 간주되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-304">The time at which the token is considered valid, in epoch time.</span></span> |
| <span data-ttu-id="de7f5-305">token_type</span><span class="sxs-lookup"><span data-stu-id="de7f5-305">token_type</span></span> |<span data-ttu-id="de7f5-306">토큰 형식 값입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-306">The token type value.</span></span> <span data-ttu-id="de7f5-307">Azure AD는 전달자 유형만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-307">The only type that Azure AD supports is Bearer.</span></span> |
| <span data-ttu-id="de7f5-308">access_token</span><span class="sxs-lookup"><span data-stu-id="de7f5-308">access_token</span></span> |<span data-ttu-id="de7f5-309">사용자가 요청한 서명된 JWT입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-309">The signed JWT that you requested.</span></span> |
| <span data-ttu-id="de7f5-310">scope</span><span class="sxs-lookup"><span data-stu-id="de7f5-310">scope</span></span> |<span data-ttu-id="de7f5-311">토큰이 유효한 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-311">The scopes that the token is valid for.</span></span> <span data-ttu-id="de7f5-312">또한 나중에 사용할 수 있도록 범위를 사용하여 토큰을 캐시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-312">You also can use the scopes to cache tokens for later use.</span></span> |
| <span data-ttu-id="de7f5-313">expires_in</span><span class="sxs-lookup"><span data-stu-id="de7f5-313">expires_in</span></span> |<span data-ttu-id="de7f5-314">토큰이 유효한 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-314">The length of time that the token is valid (in seconds).</span></span> |
| <span data-ttu-id="de7f5-315">refresh_token</span><span class="sxs-lookup"><span data-stu-id="de7f5-315">refresh_token</span></span> |<span data-ttu-id="de7f5-316">OAuth 2.0 새로 고침 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-316">An OAuth 2.0 refresh token.</span></span> <span data-ttu-id="de7f5-317">앱은 현재 토큰이 만료된 후 이 토큰을 사용하여 추가 토큰을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-317">The app can use this token to acquire additional tokens after the current token expires.</span></span> <span data-ttu-id="de7f5-318">새로 고침 토큰은 수명이 길며, 오랜 시간 동안 리소스에 대한 액세스를 유지하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-318">Refresh tokens are long-lived, and can be used to retain access to resources for extended periods of time.</span></span> <span data-ttu-id="de7f5-319">자세한 내용은 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de7f5-319">For more information, see the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span> |

<span data-ttu-id="de7f5-320">오류 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-320">Error responses look like this:</span></span>

```
{
    "error": "access_denied",
    "error_description": "The user revoked access to the app.",
}
```

| <span data-ttu-id="de7f5-321">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de7f5-321">Parameter</span></span> | <span data-ttu-id="de7f5-322">설명</span><span class="sxs-lookup"><span data-stu-id="de7f5-322">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7f5-323">error</span><span class="sxs-lookup"><span data-stu-id="de7f5-323">error</span></span> |<span data-ttu-id="de7f5-324">발생한 오류 유형을 분류하는 데 사용할 수 있는 오류 코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-324">An error code string that you can use to classify types of errors that occur.</span></span> <span data-ttu-id="de7f5-325">문자열을 사용하여 오류에 대응할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-325">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="de7f5-326">error_description</span><span class="sxs-lookup"><span data-stu-id="de7f5-326">error_description</span></span> |<span data-ttu-id="de7f5-327">인증 오류의 근본 원인을 식별하도록 도울 수 있는 특정 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-327">A specific error message that can help you identify the root cause of an authentication error.</span></span> |

## <a name="use-your-own-azure-ad-b2c-directory"></a><span data-ttu-id="de7f5-328">사용자 고유의 Azure AD B2C 디렉터리 사용</span><span class="sxs-lookup"><span data-stu-id="de7f5-328">Use your own Azure AD B2C directory</span></span>
<span data-ttu-id="de7f5-329">이러한 요청을 직접 시도하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-329">To try these requests yourself, complete the following steps.</span></span> <span data-ttu-id="de7f5-330">이 문서에서 사용한 예제 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-330">Replace the example values we used in this article with your own values.</span></span>

1. <span data-ttu-id="de7f5-331">[Azure AD B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="de7f5-331">[Create an Azure AD B2C directory](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="de7f5-332">요청에 디렉터리의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-332">Use the name of your directory in the requests.</span></span>
2. <span data-ttu-id="de7f5-333">[응용 프로그램을 만들어](active-directory-b2c-app-registration.md) 응용 프로그램 ID 및 리디렉션 URI를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-333">[Create an application](active-directory-b2c-app-registration.md) to obtain an application ID and a redirect URI.</span></span> <span data-ttu-id="de7f5-334">앱에 네이티브 클라이언트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-334">Include a native client in your app.</span></span>
3. <span data-ttu-id="de7f5-335">[정책을 만들어](active-directory-b2c-reference-policies.md) 정책 이름을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="de7f5-335">[Create your policies](active-directory-b2c-reference-policies.md) to obtain your policy names.</span></span>

