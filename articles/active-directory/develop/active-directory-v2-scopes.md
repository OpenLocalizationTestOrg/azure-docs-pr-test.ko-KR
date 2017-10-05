---
title: "Azure Active Directory v2.0 범위, 사용 권한 및 동의 | Microsoft Docs"
description: "범위, 사용 권한 및 동의를 포함하여 Azure AD v2.0 끝점의 권한 부여에 대한 설명입니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 04869a7627ecb3e6a0d11733fae7da2ecb04ed51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scopes-permissions-and-consent-in-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="d4046-103">Azure Active Directory v2.0 끝점의 범위, 사용 권한 및 동의</span><span class="sxs-lookup"><span data-stu-id="d4046-103">Scopes, permissions, and consent in the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="d4046-104">Azure AD(Azure Active Directory)와 통합된 앱은 사용자가 앱이 데이터에 액세스하는 방법을 제어할 수 있는 권한 부여 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-104">Apps that integrate with Azure Active Directory (Azure AD) follow an authorization model that gives users control over how an app can access their data.</span></span> <span data-ttu-id="d4046-105">이 권한 부여 모델의 v2.0 구현이 업데이트되어 앱이 Azure AD와 상호 작용하는 방법이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-105">The v2.0 implementation of the authorization model has been updated, and it changes how an app must interact with Azure AD.</span></span> <span data-ttu-id="d4046-106">이 문서에서는 범위, 사용 권한 및 동의를 포함하여 이 권한 부여 모델의 기본 개념에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-106">This article covers the basic concepts of this authorization model, including scopes, permissions, and consent.</span></span>

> [!NOTE]
> <span data-ttu-id="d4046-107">v2.0 끝점에서는 일부 Azure Active Directory 시나리오 및 기능만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-107">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="d4046-108">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4046-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

## <a name="scopes-and-permissions"></a><span data-ttu-id="d4046-109">범위 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="d4046-109">Scopes and permissions</span></span>
<span data-ttu-id="d4046-110">Azure AD는 [OAuth 2.0](active-directory-v2-protocols.md) 권한 부여 프로토콜을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-110">Azure AD implements the [OAuth 2.0](active-directory-v2-protocols.md) authorization protocol.</span></span> <span data-ttu-id="d4046-111">OAuth 2.0은 사용자 대신 타사 앱에서 웹에 호스트된 리소스에 액세스할 수 있도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-111">OAuth 2.0 is a method through which a third-party app can access web-hosted resources on behalf of a user.</span></span> <span data-ttu-id="d4046-112">Azure AD와 통합된 웹에 호스트된 리소스에는 리소스 식별자 또는 *응용 프로그램 ID URI*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-112">Any web-hosted resource that integrates with Azure AD has a resource identifier, or *Application ID URI*.</span></span> <span data-ttu-id="d4046-113">예를 들어 웹에 호스트된 몇 가지 Microsoft 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-113">For example, some of Microsoft's web-hosted resources include:</span></span>

* <span data-ttu-id="d4046-114">Office 365 통합 메일 API: `https://outlook.office.com`</span><span class="sxs-lookup"><span data-stu-id="d4046-114">The Office 365 Unified Mail API: `https://outlook.office.com`</span></span>
* <span data-ttu-id="d4046-115">Azure AD Graph API: `https://graph.windows.net`</span><span class="sxs-lookup"><span data-stu-id="d4046-115">The Azure AD Graph API: `https://graph.windows.net`</span></span>
* <span data-ttu-id="d4046-116">Microsoft Graph: `https://graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="d4046-116">Microsoft Graph: `https://graph.microsoft.com`</span></span>

<span data-ttu-id="d4046-117">Azure AD와 통합된 타사 리소스의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-117">The same is true for any third-party resources that have integrated with Azure AD.</span></span> <span data-ttu-id="d4046-118">이러한 리소스는 해당 리소스의 기능을 더 작은 청크로 나누는 데 사용할 수 있는 사용 권한 집합을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-118">Any of these resources also can define a set of permissions that can be used to divide the functionality of that resource into smaller chunks.</span></span> <span data-ttu-id="d4046-119">예를 들어 [Microsoft Graph](https://graph.microsoft.io)는 특히 다음 작업을 수행할 수 있는 사용 권한을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-119">As an example, [Microsoft Graph](https://graph.microsoft.io) has defined permissions to do the following tasks, among others:</span></span>

* <span data-ttu-id="d4046-120">사용자의 일정 읽기</span><span class="sxs-lookup"><span data-stu-id="d4046-120">Read a user's calendar</span></span>
* <span data-ttu-id="d4046-121">사용자의 일정에 쓰기</span><span class="sxs-lookup"><span data-stu-id="d4046-121">Write to a user's calendar</span></span>
* <span data-ttu-id="d4046-122">사용자로 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="d4046-122">Send mail as a user</span></span>

<span data-ttu-id="d4046-123">이러한 유형의 사용 권한을 정의하면 리소스가 해당 데이터 및 데이터가 노출되는 방식을 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-123">By defining these types of permissions, the resource has fine-grained control over its data and how the data is exposed.</span></span> <span data-ttu-id="d4046-124">타사 앱은 앱 사용자로부터 이러한 사용 권한을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-124">A third-party app can request these permissions from an app user.</span></span> <span data-ttu-id="d4046-125">앱 사용자가 사용 권한을 승인해야 앱이 사용자 대신 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-125">The app user must approve the permissions before the app can act on the user's behalf.</span></span> <span data-ttu-id="d4046-126">리소스 기능을 더 작은 사용 권한 집합으로 나누면 기능을 수행하는 데 필요한 특정 권한만 요청하도록 타사 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-126">By chunking the resource's functionality into smaller permission sets, third-party apps can be built to request only the specific permissions that they need to perform their function.</span></span> <span data-ttu-id="d4046-127">앱 사용자는 앱에서 데이터가 사용되는 방식을 정확하게 알 수 있으며 앱이 악의적인 의도로 동작하지 않는다는 것을 더 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-127">App users can know exactly how an app will use their data, and they can be more confident that the app is not behaving with malicious intent.</span></span>

<span data-ttu-id="d4046-128">Azure AD 및 OAuth에서는 이러한 유형의 사용 권한을 *범위*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-128">In Azure AD and OAuth, these types of permissions are called *scopes*.</span></span> <span data-ttu-id="d4046-129">*oAuth2Permissions*라고 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-129">They also sometimes are referred to as *oAuth2Permissions*.</span></span> <span data-ttu-id="d4046-130">범위는 Azure AD에서 문자열 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-130">A scope is represented in Azure AD as a string value.</span></span> <span data-ttu-id="d4046-131">Microsoft Graph 예제를 계속하는 경우 각 사용 권한에 대한 범위 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-131">Continuing with the Microsoft Graph example, the scope value for each permission is:</span></span>

* <span data-ttu-id="d4046-132">`Calendar.Read`를 사용하여 사용자의 일정 읽기</span><span class="sxs-lookup"><span data-stu-id="d4046-132">Read a user's calendar by using `Calendar.Read`</span></span>
* <span data-ttu-id="d4046-133">`Mail.ReadWrite`를 사용하여 사용자의 일정 쓰기</span><span class="sxs-lookup"><span data-stu-id="d4046-133">Write to a user's calendar by using `Mail.ReadWrite`</span></span>
* <span data-ttu-id="d4046-134">`Mail.Send`을 사용하여 사용자로 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="d4046-134">Send mail as a user using by `Mail.Send`</span></span>

<span data-ttu-id="d4046-135">앱은 v2.0 끝점에 대한 요청에 범위를 지정하여 이러한 사용 권한을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-135">An app can request these permissions by specifying the scopes in requests to the v2.0 endpoint.</span></span>

## <a name="openid-connect-scopes"></a><span data-ttu-id="d4046-136">OpenID Connect 범위</span><span class="sxs-lookup"><span data-stu-id="d4046-136">OpenID Connect scopes</span></span>
<span data-ttu-id="d4046-137">OpenID Connect의 v2.0 구현에는 특정 리소스에 적용되지 않는 몇 가지의 잘 정의된 범위 `openid`, `email`, `profile` 및 `offline_access`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-137">The v2.0 implementation of OpenID Connect has a few well-defined scopes that do not apply to a specific resource: `openid`, `email`, `profile`, and `offline_access`.</span></span>

### <a name="openid"></a><span data-ttu-id="d4046-138">openid</span><span class="sxs-lookup"><span data-stu-id="d4046-138">openid</span></span>
<span data-ttu-id="d4046-139">앱이 [OpenID Connect](active-directory-v2-protocols.md)를 사용하여 로그인을 수행하는 경우 `openid` 범위를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-139">If an app performs sign-in by using [OpenID Connect](active-directory-v2-protocols.md), it must request the `openid` scope.</span></span> <span data-ttu-id="d4046-140">`openid` 범위는 작업 계정 동의 페이지에 "로그인" 권한으로 표시되고 Microsoft 계정 동의 페이지에 "Microsoft 계정을 사용하여 프로필 보기 및 앱과 서비스에 연결" 권한으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-140">The `openid` scope shows on the work account consent page as the "Sign you in" permission, and on the personal Microsoft account consent page as the "View your profile and connect to apps and services using your Microsoft account" permission.</span></span> <span data-ttu-id="d4046-141">이 사용 권한을 통해 앱은 `sub` 클레임 형식으로 사용자에 대한 고유 식별자를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-141">With this permission, an app can receive a unique identifier for the user in the form of the `sub` claim.</span></span> <span data-ttu-id="d4046-142">또한 앱이 UserInfo 끝점에 액세스할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-142">It also gives the app access to the UserInfo endpoint.</span></span> <span data-ttu-id="d4046-143">v2.0 토큰 끝점에서 `openid` 범위를 사용하여 ID 토큰을 획득할 수도 있습니다. 이 토큰을 사용하면 앱의 다양한 구성 요소 간 HTTP 호출의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-143">The `openid` scope can be used at the v2.0 token endpoint to acquire ID tokens, which can be used to secure HTTP calls between different components of an app.</span></span>

### <a name="email"></a><span data-ttu-id="d4046-144">email</span><span class="sxs-lookup"><span data-stu-id="d4046-144">email</span></span>
<span data-ttu-id="d4046-145">`email` 범위는 `openid` 범위 및 다른 모든 범위와 함께 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-145">The `email` scope can be used with the `openid` scope and any others.</span></span> <span data-ttu-id="d4046-146">이는 앱이 `email` 클레임의 형식으로 사용자의 기본 전자 메일 주소에 액세스할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-146">It gives the app access to the user's primary email address in the form of the `email` claim.</span></span> <span data-ttu-id="d4046-147">전자 메일 주소가 사용자 계정과 연결된 경우 `email` 클레임은 오직 토큰에만 포함되지만, 항상 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-147">The `email` claim is included in a token only if an email address is associated with the user account, which is not always the case.</span></span> <span data-ttu-id="d4046-148">`email` 범위를 사용하는 경우 앱에서 `email` 클레임이 토큰에 존재하지 않는 경우를 처리할 수 있도록 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-148">If it uses the `email` scope, your app should be prepared to handle a case in which the `email` claim does not exist in the token.</span></span>

### <a name="profile"></a><span data-ttu-id="d4046-149">프로필</span><span class="sxs-lookup"><span data-stu-id="d4046-149">profile</span></span>
<span data-ttu-id="d4046-150">`profile` 범위는 `openid` 범위 및 다른 모든 범위와 함께 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-150">The `profile` scope can be used with the `openid` scope and any others.</span></span> <span data-ttu-id="d4046-151">이는 앱이 사용자에 대한 상당한 양의 정보에 액세스할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-151">It gives the app access to a substantial amount of information about the user.</span></span> <span data-ttu-id="d4046-152">액세스할 수 있는 정보에는 사용자 이름, 성, 기본 설정된 사용자 이름, 개체 ID 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-152">The information it can access includes, but is not limited to, the user's given name, surname, preferred username, and object ID.</span></span> <span data-ttu-id="d4046-153">특정 사용자에 대한 id_token 매개 변수에서 사용할 수 있는 프로필 클레임의 전체 목록은 [v2.0 토큰 참조](active-directory-v2-tokens.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4046-153">For a complete list of the profile claims available in the id_tokens parameter for a specific user, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

### <a name="offlineaccess"></a><span data-ttu-id="d4046-154">offline_access</span><span class="sxs-lookup"><span data-stu-id="d4046-154">offline_access</span></span>
<span data-ttu-id="d4046-155">[`offline_access` 범위](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess)를 사용하면 앱이 연장된 기간 동안 사용자 대신 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-155">The [`offline_access` scope](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) gives your app access to resources on behalf of the user for an extended time.</span></span> <span data-ttu-id="d4046-156">작업 계정 동의 페이지에서는 이 범위가 "언제든지 데이터 액세스" 권한으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-156">On the work account consent page, this scope appears as the "Access your data anytime" permission.</span></span> <span data-ttu-id="d4046-157">개인 Microsoft 계정 동의 페이지에서는 이 범위가 "언제든지 정보 액세스" 권한으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-157">On the personal Microsoft account consent page, it appears as the "Access your info anytime" permission.</span></span> <span data-ttu-id="d4046-158">사용자가 `offline_access` 범위를 승인하면 앱이 v2.0 토큰 끝점에서 새로 고침 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-158">When a user approves the `offline_access` scope, your app can receive refresh tokens from the v2.0 token endpoint.</span></span> <span data-ttu-id="d4046-159">새로 고침 토큰은 장기적으로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-159">Refresh tokens are long-lived.</span></span> <span data-ttu-id="d4046-160">오래된 액세스 토큰이 만료되면 앱에서 새 액세스 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-160">Your app can get new access tokens as older ones expire.</span></span>

<span data-ttu-id="d4046-161">앱이 `offline_access` 범위를 요청하지 않으면 새로 고침 토큰을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-161">If your app does not request the `offline_access` scope, it won't receive refresh tokens.</span></span> <span data-ttu-id="d4046-162">즉, [OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols.md)에서 권한 부여 코드를 교환하는 경우 `/token` 끝점에서 액세스 토큰만 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-162">This means that when you redeem an authorization code in the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md), you'll receive only an access token from the `/token` endpoint.</span></span> <span data-ttu-id="d4046-163">액세스 토큰은 짧은 시간 동안 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-163">The access token is valid for a short time.</span></span> <span data-ttu-id="d4046-164">액세스 토큰은 일반적으로 1시간 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-164">The access token usually expires in one hour.</span></span> <span data-ttu-id="d4046-165">이 시점에 앱은 사용자를 `/authorize` 끝점으로 다시 리디렉션하여 새 권한 부여 코드를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-165">At that point, your app needs to redirect the user back to the `/authorize` endpoint to get a new authorization code.</span></span> <span data-ttu-id="d4046-166">이 리디렉션 중에 앱 형식에 따라 사용자가 자격 증명을 다시 입력하거나 권한에 다시 동의해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-166">During this redirect, depending on the type of app, the user might need to enter their credentials again or consent again to permissions.</span></span>

<span data-ttu-id="d4046-167">새로 고침 토큰을 가져오고 사용하는 방법에 대한 자세한 내용은 [v2.0 프로토콜 참조](active-directory-v2-protocols.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4046-167">For more information about how to get and use refresh tokens, see the [v2.0 protocol reference](active-directory-v2-protocols.md).</span></span>

## <a name="requesting-individual-user-consent"></a><span data-ttu-id="d4046-168">개별 사용자의 동의 요청</span><span class="sxs-lookup"><span data-stu-id="d4046-168">Requesting individual user consent</span></span>
<span data-ttu-id="d4046-169">[OpenID Connect 또는 OAuth 2.0](active-directory-v2-protocols.md) 권한 부여 요청에서 앱은 `scope` 쿼리 매개 변수를 사용하여 필요한 사용 권한을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-169">In an [OpenID Connect or OAuth 2.0](active-directory-v2-protocols.md) authorization request, an app can request the permissions it needs by using the `scope` query parameter.</span></span> <span data-ttu-id="d4046-170">예를 들어 사용자가 앱에 로그인하면 앱이 다음 예제와 같은 요청을 보냅니다(읽기 쉽도록 줄 바꿈 추가).</span><span class="sxs-lookup"><span data-stu-id="d4046-170">For example, when a user signs in to an app, the app sends a request like the following example (with line breaks added for legibility):</span></span>

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

<span data-ttu-id="d4046-171">`scope` 매개 변수는 앱이 요청하는 공백으로 구분된 범위 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-171">The `scope` parameter is a space-separated list of scopes that the app is requesting.</span></span> <span data-ttu-id="d4046-172">각 범위는 리소스 식별자(응용 프로그램 ID URI)에 범위 값을 추가하여 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-172">Each scope is indicated by appending the scope value to the resource's identifier (the Application ID URI).</span></span> <span data-ttu-id="d4046-173">요청 예제에서 앱에는 사용자의 일정을 읽고 사용자로 메일을 보낼 수 있는 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-173">In the request example, the app needs permission to read the user's calendar and send mail as the user.</span></span>

<span data-ttu-id="d4046-174">사용자가 자격 증명을 입력하면 v2.0 끝점이 *사용자 동의*와 일치하는 레코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-174">After the user enters their credentials, the v2.0 endpoint checks for a matching record of *user consent*.</span></span> <span data-ttu-id="d4046-175">사용자가 이전에 요청된 사용 권한 중 하나에 동의하지 않은 경우 v2.0 끝점이 사용자에게 요청된 사용 권한을 부여하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-175">If the user has not consented to any of the requested permissions in the past, the v2.0 endpoint asks the user to grant the requested permissions.</span></span>

![작업 계정 동의](../../media/active-directory-v2-flows/work_account_consent.png)

<span data-ttu-id="d4046-177">사용자가 사용 권한을 승인하면 후속 계정 로그인 시 다시 동의할 필요가 없도록 동의가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-177">When the user approves the permission, the consent is recorded so that the user doesn't have to consent again on subsequent account sign-ins.</span></span>

## <a name="requesting-consent-for-an-entire-tenant"></a><span data-ttu-id="d4046-178">전체 테넌트에 대한 동의 요청</span><span class="sxs-lookup"><span data-stu-id="d4046-178">Requesting consent for an entire tenant</span></span>
<span data-ttu-id="d4046-179">조직이 응용 프로그램에 대한 라이선스 또는 구독을 구입하는 경우 직원들을 위해 응용 프로그램을 완전히 프로비전하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-179">Often, when an organization purchases a license or subscription for an application, the organization wants to fully provision the application for its employees.</span></span> <span data-ttu-id="d4046-180">이 프로세스의 일부로 관리자는 모든 직원을 대신하여 해당 응용 프로그램에 대한 동의를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-180">As part of this process, an administrator can grant consent for the application to act on behalf of any employee.</span></span> <span data-ttu-id="d4046-181">관리자가 전체 테넌트에 대한 동의를 부여하면 해당 조직의 직원에게는 응용 프로그램에 대한 동의 화면이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-181">If the admin grants consent for the entire tenant, the organization's employees won't see a consent page for the application.</span></span>

<span data-ttu-id="d4046-182">테넌트에서 모든 사용자에 대한 동의를 요청하기 위해 앱은 관리 동의 끝점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-182">To request consent for all users in a tenant, your app can use the admin consent endpoint.</span></span>

## <a name="admin-restricted-scopes"></a><span data-ttu-id="d4046-183">관리 제한 범위</span><span class="sxs-lookup"><span data-stu-id="d4046-183">Admin-restricted scopes</span></span>
<span data-ttu-id="d4046-184">Microsoft 에코시스템에서 일부 높은 수준 사용 권한을 *관리 제한*으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-184">Some high-privilege permissions in the Microsoft ecosystem can be set to *admin-restricted*.</span></span> <span data-ttu-id="d4046-185">이러한 종류의 범위에는 다음과 같은 사용 권한이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-185">Examples of these kinds of scopes include the following permissions:</span></span>

* <span data-ttu-id="d4046-186">`Directory.Read`를 사용하여 조직의 디렉터리 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="d4046-186">Read an organization's directory data by using `Directory.Read`</span></span>
* <span data-ttu-id="d4046-187">`Directory.ReadWrite`를 사용하여 조직의 디렉터리에 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="d4046-187">Write data to an organization's directory by using `Directory.ReadWrite`</span></span>
* <span data-ttu-id="d4046-188">`Groups.Read.All`을 사용하여 조직의 디렉터리에서 보안 그룹 읽기</span><span class="sxs-lookup"><span data-stu-id="d4046-188">Read security groups in an organization's directory by using `Groups.Read.All`</span></span>

<span data-ttu-id="d4046-189">소비자 사용자는 이러한 데이터에 대한 응용 프로그램 액세스 권한을 부여할 수 있는 반면 조직 사용자는 동일한 집합인 회사의 중요한 데이터에 대한 액세스 권한을 부여하지 않도록 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-189">Although a consumer user might grant an application access to this kind of data, organizational users are restricted from granting access to the same set of sensitive company data.</span></span> <span data-ttu-id="d4046-190">응용 프로그램이 조직 사용자에게 이러한 사용 권한 중 하나에 대한 액세스를 요청하는 경우 사용자에게는 앱의 사용 권한에 동의할 권한이 부여되지 않음을 나타내는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-190">If your application requests access to one of these permissions from an organizational user, the user receives an error message that says they are not authorized to consent to your app's permissions.</span></span>

<span data-ttu-id="d4046-191">또한 앱이 조직의 이러한 관리 제한 범위에 대한 액세스 권한을 필요로 하는 경우 아래에 설명한 관리 동의 끝점을 사용하여 회사 관리자에게 직접 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-191">If your app requires access to admin-restricted scopes for organizations, you should request them directly from a company administrator, also by using the admin consent endpoint, described next.</span></span>

<span data-ttu-id="d4046-192">관리자가 관리 동의 끝점을 통해 이러한 사용 권한을 부여할 경우 테넌트에서 모든 사용자에 대한 동의가 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-192">When an administrator grants these permissions via the admin consent endpoint, consent is granted for all users in the tenant.</span></span>

## <a name="using-the-admin-consent-endpoint"></a><span data-ttu-id="d4046-193">관리 동의 끝점 사용</span><span class="sxs-lookup"><span data-stu-id="d4046-193">Using the admin consent endpoint</span></span>
<span data-ttu-id="d4046-194">다음 단계를 따를 경우 앱은 관리 제한 범위를 포함하여 테넌트의 모든 사용자에 대한 사용 권한을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-194">If you follow these steps, your app can gather permissions for all users in a tenant, including admin-restricted scopes.</span></span> <span data-ttu-id="d4046-195">단계를 구현하는 코드 샘플을 보려면 [관리 제한 범위 샘플](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4046-195">To see a code sample that implements the steps, see the [admin-restricted scopes sample](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).</span></span>

### <a name="request-the-permissions-in-the-app-registration-portal"></a><span data-ttu-id="d4046-196">앱 등록 포털에서 사용 권한 요청</span><span class="sxs-lookup"><span data-stu-id="d4046-196">Request the permissions in the app registration portal</span></span>
1. <span data-ttu-id="d4046-197">[응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 응용 프로그램으로 이동하거나 응용 프로그램이 없는 경우 [응용 프로그램을 만듭니다](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d4046-197">Go to your application in the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or [create an app](active-directory-v2-app-registration.md) if you haven't already.</span></span>
2. <span data-ttu-id="d4046-198">**Microsoft Graph 사용 권한** 섹션으로 이동하여 앱에 필요한 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-198">Locate the **Microsoft Graph Permissions** section, and then add the permissions that your app requires.</span></span>
3. <span data-ttu-id="d4046-199">앱 등록을 **저장**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-199">Make sure you **Save** the app registration.</span></span>

### <a name="recommended-sign-the-user-in-to-your-app"></a><span data-ttu-id="d4046-200">사용자가 앱에 로그인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-200">Recommended: Sign the user in to your app</span></span>
<span data-ttu-id="d4046-201">일반적으로 관리 동의 끝점을 사용하는 응용 프로그램을 빌드할 때 앱에는 관리자가 앱의 사용 권한을 승인할 수 있는 페이지 또는 보기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-201">Typically, when you build an application that uses the admin consent endpoint, the app needs a page or view in which the admin can approve the app's permissions.</span></span> <span data-ttu-id="d4046-202">이 페이지는 앱 로그인 흐름의 일부, 앱 설정의 일부 또는 전용 "연결" 흐름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-202">This page can be part of the app's sign-up flow, part of the app's settings, or it can be a dedicated "connect" flow.</span></span> <span data-ttu-id="d4046-203">대부분의 경우에 사용자가 회사 또는 학교 Microsoft 계정으로 로그인한 후에 앱은 이 "연결" 보기만을 표시하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-203">In many cases, it makes sense for the app to show this "connect" view only after a user has signed in with a work or school Microsoft account.</span></span>

<span data-ttu-id="d4046-204">사용자로 앱에 로그인하면 사용자에게 필요한 사용 권한을 승인하도록 요청하기 전에 관리자가 속해 있는 조직을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-204">When you sign the user in to your app, you can identify the organization to which the admin belongs before asking them to approve the necessary permissions.</span></span> <span data-ttu-id="d4046-205">반드시 필요하지는 않지만 조직 사용자를 위한 직관적인 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-205">Although not strictly necessary, it can help you create a more intuitive experience for your organizational users.</span></span> <span data-ttu-id="d4046-206">사용자가 로그인하려면 [v2.0 프로토콜 자습서](active-directory-v2-protocols.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-206">To sign the user in, follow our [v2.0 protocol tutorials](active-directory-v2-protocols.md).</span></span>

### <a name="request-the-permissions-from-a-directory-admin"></a><span data-ttu-id="d4046-207">디렉터리 관리에서 사용 권한 요청</span><span class="sxs-lookup"><span data-stu-id="d4046-207">Request the permissions from a directory admin</span></span>
<span data-ttu-id="d4046-208">조직의 관리자에게 사용 권한을 요청할 준비가 되면 v 2.0 *관리 동의 끝점*에 사용자를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-208">When you're ready to request permissions from your organization's admin, you can redirect the user to the v2.0 *admin consent endpoint*.</span></span>

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting the below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| <span data-ttu-id="d4046-209">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d4046-209">Parameter</span></span> | <span data-ttu-id="d4046-210">조건</span><span class="sxs-lookup"><span data-stu-id="d4046-210">Condition</span></span> | <span data-ttu-id="d4046-211">설명</span><span class="sxs-lookup"><span data-stu-id="d4046-211">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4046-212">tenant</span><span class="sxs-lookup"><span data-stu-id="d4046-212">tenant</span></span> |<span data-ttu-id="d4046-213">필수</span><span class="sxs-lookup"><span data-stu-id="d4046-213">Required</span></span> |<span data-ttu-id="d4046-214">사용 권한을 요청하려는 디렉터리 테넌트입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-214">The directory tenant that you want to request permission from.</span></span> <span data-ttu-id="d4046-215">GUID 또는 친숙한 이름 형식으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-215">Can be provided in GUID or friendly name format.</span></span> |
| <span data-ttu-id="d4046-216">client_id</span><span class="sxs-lookup"><span data-stu-id="d4046-216">client_id</span></span> |<span data-ttu-id="d4046-217">필수</span><span class="sxs-lookup"><span data-stu-id="d4046-217">Required</span></span> |<span data-ttu-id="d4046-218">[응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 앱에 할당한 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-218">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span></span> |
| <span data-ttu-id="d4046-219">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="d4046-219">redirect_uri</span></span> |<span data-ttu-id="d4046-220">필수</span><span class="sxs-lookup"><span data-stu-id="d4046-220">Required</span></span> |<span data-ttu-id="d4046-221">리디렉션 URI는 처리할 앱에 응답을 전송하려는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-221">The redirect URI where you want the response to be sent for your app to handle.</span></span> <span data-ttu-id="d4046-222">앱 등록 포털에 등록한 리디렉션 URI 중 하나와 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-222">It must exactly match one of the redirect URIs that you registered in the app registration portal.</span></span> |
| <span data-ttu-id="d4046-223">state</span><span class="sxs-lookup"><span data-stu-id="d4046-223">state</span></span> |<span data-ttu-id="d4046-224">권장</span><span class="sxs-lookup"><span data-stu-id="d4046-224">Recommended</span></span> |<span data-ttu-id="d4046-225">토큰 응답에도 반환되는 요청에 포함된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-225">A value included in the request that will also be returned in the token response.</span></span> <span data-ttu-id="d4046-226">원하는 모든 콘텐츠의 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-226">It can be a string of any content you want.</span></span> <span data-ttu-id="d4046-227">상태를 사용하여 인증 요청이 발생하기 전에 앱에서 사용자 상태에 대한 정보(예: 사용한 페이지 또는 보기)를 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-227">Use the state to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |

<span data-ttu-id="d4046-228">이 시점에서 Azure AD는 테넌트 관리자에게 요청을 완료하기 위해 로그인하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-228">At this point, Azure AD requires a tenant administrator to sign in to complete the request.</span></span> <span data-ttu-id="d4046-229">관리자에게는 앱 등록 포털에서 앱에 요청한 사용 권한을 모두 승인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-229">The administrator is asked to approve all the permissions that you have requested for your app in the app registration portal.</span></span>

#### <a name="successful-response"></a><span data-ttu-id="d4046-230">성공적인 응답</span><span class="sxs-lookup"><span data-stu-id="d4046-230">Successful response</span></span>
<span data-ttu-id="d4046-231">관리자가 앱에 대한 사용 권한을 승인하는 경우 성공적인 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-231">If the admin approves the permissions for your app, the successful response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| <span data-ttu-id="d4046-232">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d4046-232">Parameter</span></span> | <span data-ttu-id="d4046-233">설명</span><span class="sxs-lookup"><span data-stu-id="d4046-233">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4046-234">tenant</span><span class="sxs-lookup"><span data-stu-id="d4046-234">tenant</span></span> |<span data-ttu-id="d4046-235">디렉터리 테넌트는 GUID 형식으로 요청한 권한을 응용 프로그램에 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-235">The directory tenant that granted your application the permissions it requested, in GUID format.</span></span> |
| <span data-ttu-id="d4046-236">state</span><span class="sxs-lookup"><span data-stu-id="d4046-236">state</span></span> |<span data-ttu-id="d4046-237">토큰 응답에도 반환되는 요청에 포함된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-237">A value included in the request that also will be returned in the token response.</span></span> <span data-ttu-id="d4046-238">원하는 모든 콘텐츠의 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-238">It can be a string of any content you want.</span></span> <span data-ttu-id="d4046-239">상태는 인증 요청이 발생하기 전에 앱에서 사용자 상태에 대한 정보(예: 사용한 페이지 또는 보기)를 인코딩하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-239">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |
| <span data-ttu-id="d4046-240">admin_consent</span><span class="sxs-lookup"><span data-stu-id="d4046-240">admin_consent</span></span> |<span data-ttu-id="d4046-241">**true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-241">Will be set to **true**.</span></span> |

#### <a name="error-response"></a><span data-ttu-id="d4046-242">오류 응답</span><span class="sxs-lookup"><span data-stu-id="d4046-242">Error response</span></span>
<span data-ttu-id="d4046-243">관리자가 앱에 대한 사용 권한을 승인하지 않는 경우 실패한 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-243">If the admin does not approve the permissions for your app, the failed response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| <span data-ttu-id="d4046-244">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d4046-244">Parameter</span></span> | <span data-ttu-id="d4046-245">설명</span><span class="sxs-lookup"><span data-stu-id="d4046-245">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4046-246">error</span><span class="sxs-lookup"><span data-stu-id="d4046-246">error</span></span> |<span data-ttu-id="d4046-247">발생하는 오류 유형을 분류하는 데 사용할 수 있고 오류에 대응하는 데 사용할 수 있는 오류 코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-247">An error code string that can be used to classify types of errors that occur, and can be used to react to errors.</span></span> |
| <span data-ttu-id="d4046-248">error_description</span><span class="sxs-lookup"><span data-stu-id="d4046-248">error_description</span></span> |<span data-ttu-id="d4046-249">개발자가 오류의 근본 원인을 식별하도록 도울 수 있는 특정 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-249">A specific error message that can help a developer identify the root cause of an error.</span></span> |

<span data-ttu-id="d4046-250">관리 동의 끝점에서 성공적인 응답을 받은 후 앱은 요청한 사용 권한을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-250">After you've received a successful response from the admin consent endpoint, your app has gained the permissions it requested.</span></span> <span data-ttu-id="d4046-251">이제 원하는 리소스에 대한 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-251">Next, you can request a token for the resource you want.</span></span>

## <a name="using-permissions"></a><span data-ttu-id="d4046-252">사용 권한 사용</span><span class="sxs-lookup"><span data-stu-id="d4046-252">Using permissions</span></span>
<span data-ttu-id="d4046-253">사용자가 앱에 대한 사용 권한에 동의하면 앱이 일부 용량으로 리소스에 액세스할 수 있는 앱의 권한을 나타내는 액세스 토큰을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-253">After the user consents to permissions for your app, your app can acquire access tokens that represent your app's permission to access a resource in some capacity.</span></span> <span data-ttu-id="d4046-254">액세스 토큰은 단일 리소스에만 사용할 수 있지만 해당 리소스에 대해 앱에 부여된 모든 사용 권한이 액세스 토큰 안에 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-254">An access token can be used only for a single resource, but encoded inside the access token is every permission that your app has been granted for that resource.</span></span> <span data-ttu-id="d4046-255">액세스 토큰을 획득하기 위해 앱은 다음과 같이 v2.0 토큰 끝점을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-255">To acquire an access token, your app can make a request to the v2.0 token endpoint, like this:</span></span>

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

<span data-ttu-id="d4046-256">리소스에 대한 HTTP 요청에 결과 액세스 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-256">You can use the resulting access token in HTTP requests to the resource.</span></span> <span data-ttu-id="d4046-257">이는 앱에 특정 작업을 수행할 수 있는 적절한 권한이 있음을 리소스에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4046-257">It reliably indicates to the resource that your app has the proper permission to perform a specific task.</span></span>  

<span data-ttu-id="d4046-258">OAuth 2.0 프로토콜 및 액세스 토큰을 가져오는 방법에 대한 자세한 내용은 [v2.0 끝점 프로토콜 참조](active-directory-v2-protocols.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4046-258">For more information about the OAuth 2.0 protocol and how to get access tokens, see the [v2.0 endpoint protocol reference](active-directory-v2-protocols.md).</span></span>
