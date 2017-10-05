---
title: "Azure Active Directory에서 구성 가능한 토큰 수명 | Microsoft Docs"
description: "Azure AD에서 발급한 토큰의 수명을 설정하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: d23721eba308096a05211eb6e26e1338a69cae0c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="0374d-103">Azure Active Directory에서 구성 가능한 토큰 수명(공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0374d-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="0374d-104">Azure AD(Azure Active Directory)에서 발급한 토큰의 수명을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-104">You can specify the lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0374d-105">조직의 모든 앱, 다중 테넌트(다중 조직) 응용 프로그램 또는 조직의 특정 서비스 주체에 대해 토큰 수명을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="0374d-106">이 기능은 현재 공개 미리 보기로 제공되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="0374d-107">변경 내용을 되돌리거나 제거할 준비를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-107">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="0374d-108">이 기능은 공개 미리 보기 동안 모든 Azure Active Directory 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-108">The feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="0374d-109">그러나 기능이 일반 공급되면 일부 기능에는 [Azure Active Directory Premium](active-directory-get-started-premium.md) 구독이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-109">However, when the feature becomes generally available, some aspects of the feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="0374d-110">Azure AD에서 정책 개체는 개별 응용 프로그램 또는 조직의 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="0374d-111">각 정책 유형에는 할당된 개체에 적용되는 속성 집합이 포함된 고유의 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-111">Each policy type has a unique structure, with a set of properties that are applied to objects to which they are assigned.</span></span>

<span data-ttu-id="0374d-112">조직의 기본 정책이 될 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-112">You can designate a policy as the default policy for your organization.</span></span> <span data-ttu-id="0374d-113">해당 정책은 더 높은 우선 순위의 정책으로 재정의되지 않는 한 조직 내의 모든 응용 프로그램에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-113">The policy is applied to any application in the organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="0374d-114">특정 응용 프로그램에 정책을 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-114">You also can assign a policy to specific applications.</span></span> <span data-ttu-id="0374d-115">우선 순위는 정책 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-115">The order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="0374d-116">토큰 형식</span><span class="sxs-lookup"><span data-stu-id="0374d-116">Token types</span></span>

<span data-ttu-id="0374d-117">새로 고침 토큰, 액세스 토큰, 세션 토큰 및 ID 토큰에 대한 토큰 수명 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="0374d-118">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-118">Access tokens</span></span>
<span data-ttu-id="0374d-119">클라이언트는 액세스 토큰을 사용하여 보호된 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-119">Clients use access tokens to access a protected resource.</span></span> <span data-ttu-id="0374d-120">액세스 토큰은 사용자, 클라이언트 및 리소스의 특정 조합에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="0374d-121">액세스 토큰은 해지될 수 없으며 만료될 때까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="0374d-122">액세스 토큰을 획득한 악의적인 행위자는 수명 범위 동안 이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="0374d-123">액세스 토큰의 수명을 조정하는 것은 시스템 성능을 개선하는 것과 사용자 계정이 비활성화된 후 클라이언트에서 액세스를 유지하는 기간을 늘리는 것 간의 절충 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-123">Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user’s account is disabled.</span></span> <span data-ttu-id="0374d-124">시스템 성능을 개선하려면 클라이언트에서 새 액세스 토큰을 획득해야 하는 횟수를 줄이면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-124">Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="0374d-125">새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-125">Refresh tokens</span></span>
<span data-ttu-id="0374d-126">클라이언트가 보호된 리소스에 액세스하기 위해 액세스 토큰을 획득할 때 새로 고침 토큰과 액세스 토큰을 모두 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-126">When a client acquires an access token to access a protected resource, the client receives both a refresh token and an access token.</span></span> <span data-ttu-id="0374d-127">새로 고침 토큰은 현재 액세스 토큰이 만료된 경우 새 액세스/새로 고침 토큰 쌍을 얻는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-127">The refresh token is used to obtain new access/refresh token pairs when the current access token expires.</span></span> <span data-ttu-id="0374d-128">새로 고침 토큰은 사용자와 클라이언트 조합에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-128">A refresh token is bound to a combination of user and client.</span></span> <span data-ttu-id="0374d-129">새로 고침 토큰은 해지 가능하며 사용될 때마다 토큰의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-129">A refresh token can be revoked, and the token's validity is checked every time the token is used.</span></span>

<span data-ttu-id="0374d-130">비밀 클라이언트와 공용 클라이언트를 구분하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-130">It's important to make a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="0374d-131">다양한 유형의 클라이언트에 대한 자세한 내용은 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0374d-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="0374d-132">비밀 클라이언트 새로 고침 토큰의 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="0374d-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="0374d-133">비밀 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="0374d-134">비밀 클라이언트는 요청이 악의적인 행위자가 아닌 응용 프로그램에서 오는 것을 증명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-134">They can prove that requests are coming from the client application and not from a malicious actor.</span></span> <span data-ttu-id="0374d-135">예를 들어 웹앱은 웹 서버에 클라이언트 비밀을 저장할 수 있으므로 비밀 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-135">For example, a web app is a confidential client because it can store a client secret on the web server.</span></span> <span data-ttu-id="0374d-136">따라서 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-136">It is not exposed.</span></span> <span data-ttu-id="0374d-137">이러한 흐름은 보다 안전하기 때문에 이러한 흐름에 발급된 새로 고침 토큰의 기본 수명은 `until-revoked`이며 정책을 사용하여 변경할 수 없고 자발적인 암호 재설정에서 취소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-137">Because these flows are more secure, the default lifetimes of refresh tokens issued to these flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="0374d-138">공용 클라이언트 새로 고침 토큰의 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="0374d-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="0374d-139">공용 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="0374d-140">예를 들어 iOS/Android 앱은 리소스 소유자의 비밀을 난독 처리할 수 없으므로 공용 클라이언트로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-140">For example, an iOS/Android app cannot obfuscate a secret from the resource owner, so it is considered a public client.</span></span> <span data-ttu-id="0374d-141">리소스에 정책을 설정하여 지정된 기간보다 오래된 공용 클라이언트의 새로 고침 토큰이 새 액세스/새로 고침 토큰 쌍을 얻지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-141">You can set policies on resources to prevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="0374d-142">이렇게 하려면 새로 고침 토큰 최대 비활성 시간 속성을 사용하세요. 특정 기간이 지나면 더 이상 새로 고침 토큰이 허용되지 않도록 정책을 사용하여 기간을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-142">(To do this, use the Refresh Token Max Inactive Time property.) You also can use policies to set a period beyond which the refresh tokens are no longer accepted.</span></span> <span data-ttu-id="0374d-143">이렇게 하려면 새로 고침 토큰 최대 기간 속성을 사용하세요. 새로 고침 토큰의 수명을 조정하여 공용 클라이언트 응용 프로그램을 사용할 때 자동으로 재인증되는 대신 사용자가 자격 증명을 다시 입력해야 하는 시기 및 빈도를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-143">(To do this, use the Refresh Token Max Age property.) You can adjust the lifetime of a refresh token to control when and how often the user is required to reenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="0374d-144">ID 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-144">ID tokens</span></span>
<span data-ttu-id="0374d-145">ID 토큰은 웹 사이트 및 기본 클라이언트에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-145">ID tokens are passed to websites and native clients.</span></span> <span data-ttu-id="0374d-146">ID 토큰은 사용자에 대한 프로필 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="0374d-147">ID 토큰은 사용자와 클라이언트의 특정 조합에 바인딩되며,</span><span class="sxs-lookup"><span data-stu-id="0374d-147">An ID token is bound to a specific combination of user and client.</span></span> <span data-ttu-id="0374d-148">ID 토큰은 만료될 때까지 유효한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="0374d-149">일반적으로 웹 응용 프로그램은 응용 프로그램의 사용자 세션 수명을 해당 사용자에 대해 발급된 ID 토큰의 수명과 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-149">Usually, a web application matches a user’s session lifetime in the application to the lifetime of the ID token issued for the user.</span></span> <span data-ttu-id="0374d-150">ID 토큰의 수명을 조정하여 웹 응용 프로그램이 응용 프로그램 세션을 만료하는 빈도 및 사용자에게 Azure AD에 다시 인증하도록(자동으로 또는 대화형으로) 요구하는 빈도를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-150">You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="0374d-151">Single Sign-On 세션 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-151">Single sign-on session tokens</span></span>
<span data-ttu-id="0374d-152">사용자가 Azure AD에 인증하고 **로그인 유지** 확인란을 선택하면 사용자의 브라우저와 Azure AD에 SSO(Single Sign-On) 세션이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-152">When a user authenticates with Azure AD and selects the **Keep me signed in** check box, a single sign-on session (SSO) is established with the user’s browser and Azure AD.</span></span> <span data-ttu-id="0374d-153">쿠키 형식의 SSO 토큰은 이 세션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-153">The SSO token, in the form of a cookie, represents this session.</span></span> <span data-ttu-id="0374d-154">SSO 세션 토큰은 특정 리소스/클라이언트 응용 프로그램에 바인딩되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-154">Note that the SSO session token is not bound to a specific resource/client application.</span></span> <span data-ttu-id="0374d-155">SSO 세션 토큰은 해지 가능하며 사용될 때마다 토큰의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="0374d-156">Azure AD는 두 종류의 SSO 세션 토큰을 사용합니다. 하나는 영구 세션 토큰이고 다른 하나는 비영구 세션 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="0374d-157">영구 세션 토큰은 브라우저에 영구 쿠키로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-157">Persistent session tokens are stored as persistent cookies by the browser.</span></span> <span data-ttu-id="0374d-158">비영구 세션 토큰은 세션 쿠키로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="0374d-159">브라우저가 닫히면 세션 쿠키는 소멸됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-159">(Session cookies are destroyed when the browser is closed.)</span></span>

<span data-ttu-id="0374d-160">비영구 세션 토큰의 수명은 24시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="0374d-161">영구 토큰의 수명은 180일입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="0374d-162">SSO 세션 토큰은 유효 기간 내에 언제든지 사용할 수 있으며, 토큰 종류에 따라 유효 기간이 24시간 또는 180일 더 연장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-162">Any time an SSO session token is used within its validity period, the validity period is extended another 24 hours or 180 days, depending on the token type.</span></span> <span data-ttu-id="0374d-163">유효 기간 내에 SSO 세션 토큰을 사용하지 않으면 만료된 것으로 간주하여 더 이상 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="0374d-164">첫 번째 세션 토큰이 발급된 후 특정 시간이 지나면 더 이상 세션 토큰이 허용되지 않도록 정책을 사용하여 시간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-164">You can use a policy to set the time after the first session token was issued beyond which the session token is no longer accepted.</span></span> <span data-ttu-id="0374d-165">이렇게 하려면 세션 토큰 최대 기간 속성을 사용하세요. 세션 토큰의 수명을 조정하여 웹 응용 프로그램을 사용할 때 자동으로 인증되는 대신 사용자가 자격 증명을 다시 입력해야 하는 시기 및 빈도를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-165">(To do this, use the Session Token Max Age property.) You can adjust the lifetime of a session token to control when and how often a user is required to reenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="0374d-166">토큰 수명 정책 속성</span><span class="sxs-lookup"><span data-stu-id="0374d-166">Token lifetime policy properties</span></span>
<span data-ttu-id="0374d-167">토큰 수명 정책은 토큰 수명 규칙을 포함하는 정책 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="0374d-168">정책의 속성을 사용하여 지정된 토큰 수명을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-168">Use the properties of the policy to control specified token lifetimes.</span></span> <span data-ttu-id="0374d-169">설정된 정책이 없는 경우 시스템에서 기본 수명값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-169">If no policy is set, the system enforces the default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="0374d-170">구성 가능한 토큰 수명 속성</span><span class="sxs-lookup"><span data-stu-id="0374d-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="0374d-171">속성</span><span class="sxs-lookup"><span data-stu-id="0374d-171">Property</span></span> | <span data-ttu-id="0374d-172">정책 속성 문자열</span><span class="sxs-lookup"><span data-stu-id="0374d-172">Policy property string</span></span> | <span data-ttu-id="0374d-173">영향</span><span class="sxs-lookup"><span data-stu-id="0374d-173">Affects</span></span> | <span data-ttu-id="0374d-174">기본값</span><span class="sxs-lookup"><span data-stu-id="0374d-174">Default</span></span> | <span data-ttu-id="0374d-175">최소</span><span class="sxs-lookup"><span data-stu-id="0374d-175">Minimum</span></span> | <span data-ttu-id="0374d-176">최대</span><span class="sxs-lookup"><span data-stu-id="0374d-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0374d-177">액세스 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="0374d-177">Access Token Lifetime</span></span> |<span data-ttu-id="0374d-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="0374d-178">AccessTokenLifetime</span></span> |<span data-ttu-id="0374d-179">액세스 토큰, ID 토큰, SAML2 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="0374d-180">1시간</span><span class="sxs-lookup"><span data-stu-id="0374d-180">1 hour</span></span> |<span data-ttu-id="0374d-181">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-181">10 minutes</span></span> |<span data-ttu-id="0374d-182">1일</span><span class="sxs-lookup"><span data-stu-id="0374d-182">1 day</span></span> |
| <span data-ttu-id="0374d-183">새로 고침 토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="0374d-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="0374d-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="0374d-184">MaxInactiveTime</span></span> |<span data-ttu-id="0374d-185">새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-185">Refresh tokens</span></span> |<span data-ttu-id="0374d-186">14일</span><span class="sxs-lookup"><span data-stu-id="0374d-186">14 days</span></span> |<span data-ttu-id="0374d-187">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-187">10 minutes</span></span> |<span data-ttu-id="0374d-188">90일</span><span class="sxs-lookup"><span data-stu-id="0374d-188">90 days</span></span> |
| <span data-ttu-id="0374d-189">단일 단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="0374d-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="0374d-191">새로 고침 토큰(모든 사용자)</span><span class="sxs-lookup"><span data-stu-id="0374d-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="0374d-192">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="0374d-192">Until-revoked</span></span> |<span data-ttu-id="0374d-193">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-193">10 minutes</span></span> |<span data-ttu-id="0374d-194">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="0374d-195">다단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="0374d-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="0374d-197">새로 고침 토큰(모든 사용자)</span><span class="sxs-lookup"><span data-stu-id="0374d-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="0374d-198">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="0374d-198">Until-revoked</span></span> |<span data-ttu-id="0374d-199">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-199">10 minutes</span></span> |<span data-ttu-id="0374d-200">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="0374d-201">단일 단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="0374d-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="0374d-203">세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="0374d-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="0374d-204">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="0374d-204">Until-revoked</span></span> |<span data-ttu-id="0374d-205">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-205">10 minutes</span></span> |<span data-ttu-id="0374d-206">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="0374d-207">다단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="0374d-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="0374d-209">세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="0374d-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="0374d-210">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="0374d-210">Until-revoked</span></span> |<span data-ttu-id="0374d-211">10분</span><span class="sxs-lookup"><span data-stu-id="0374d-211">10 minutes</span></span> |<span data-ttu-id="0374d-212">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0374d-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="0374d-213"><sup>1</sup>이러한 특성에 대해 설정할 수 있는 명시적인 최대 기간은 365일입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-213"><sup>1</sup>365 days is the maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="0374d-214"><sup>2</sup>**MaxAgeSessionSingleFactor**가 설정되지 않은 경우 이 값은 **MaxAgeSingleFactor** 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes the **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="0374d-215">두 매개 변수 모두 설정되지 않은 경우에는 이 속성에 기본값(until-revoked)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-215">If neither parameter is set, the property takes the default value (until-revoked).</span></span>
* <span data-ttu-id="0374d-216"><sup>3</sup>**MaxAgeSessionMultiFactor**가 설정되지 않은 경우 이 값은 **MaxAgeMultiFactor** 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes the **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="0374d-217">두 매개 변수 모두 설정되지 않은 경우에는 이 속성에 기본값(until-revoked)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-217">If neither parameter is set, the property takes the default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="0374d-218">예외</span><span class="sxs-lookup"><span data-stu-id="0374d-218">Exceptions</span></span>
| <span data-ttu-id="0374d-219">속성</span><span class="sxs-lookup"><span data-stu-id="0374d-219">Property</span></span> | <span data-ttu-id="0374d-220">영향</span><span class="sxs-lookup"><span data-stu-id="0374d-220">Affects</span></span> | <span data-ttu-id="0374d-221">기본값</span><span class="sxs-lookup"><span data-stu-id="0374d-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0374d-222">새로 고침 토큰 최대 기간(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="0374d-222">Refresh Token Max Age (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="0374d-223">새로 고침 토큰(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="0374d-223">Refresh tokens (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="0374d-224">12시간</span><span class="sxs-lookup"><span data-stu-id="0374d-224">12 hours</span></span> |
| <span data-ttu-id="0374d-225">새로 고침 토큰 최대 비활성 시간(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="0374d-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="0374d-226">새로 고침 토큰(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="0374d-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="0374d-227">90일</span><span class="sxs-lookup"><span data-stu-id="0374d-227">90 days</span></span> |
| <span data-ttu-id="0374d-228">새로 고침 토큰 최대 기간(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="0374d-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="0374d-229">새로 고침 토큰(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="0374d-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="0374d-230">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="0374d-230">Until-revoked</span></span> |

* <span data-ttu-id="0374d-231"><sup>1</sup>해지 정보가 부족한 페더레이션된 사용자에는 "LastPasswordChangeTimestamp" 특성이 동기화되지 않은 모든 사용자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-231"><sup>1</sup>Federated users who have insufficient revocation information include any users who do not have the "LastPasswordChangeTimestamp" attribute synced.</span></span> <span data-ttu-id="0374d-232">이러한 사용자의 경우 AAD가 이전 자격 증명(예: 변경된 암호)에 연결된 토큰을 해지할 시기를 확인할 수 없어 이 짧은 최대 사용 기간이 제공되며, 사용자 및 연결된 토큰이 여전히 양호한 상태인지 자주 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-232">These users are given this short Max Age because AAD is unable to verify when to revoke tokens that are tied to an old credential (such as a password that has been changed) and must check back in more frequently to ensure that the user and associated tokens are still in good standing.</span></span> <span data-ttu-id="0374d-233">이 환경을 개선하기 위해 테넌트 관리자는 "LastPasswordChangeTimestamp" 특성을 동기화해야 합니다. 이 특성은 Powershell을 사용하거나 AADSync를 통해 사용자 개체에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-233">To improve this experience, tenant admins must ensure that they are syncing the “LastPasswordChangeTimestamp” attribute (this can be set on the user object using Powershell or through AADSync).</span></span>

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="0374d-234">정책 평가 및 우선 순위 지정</span><span class="sxs-lookup"><span data-stu-id="0374d-234">Policy evaluation and prioritization</span></span>
<span data-ttu-id="0374d-235">토큰 수명 정책을 만들어서 특정 응용 프로그램, 조직 및 서비스 주체에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-235">You can create and then assign a token lifetime policy to a specific application, to your organization, and to service principals.</span></span> <span data-ttu-id="0374d-236">특정 응용 프로그램에 여러 정책이 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-236">Multiple policies might apply to a specific application.</span></span> <span data-ttu-id="0374d-237">적용되는 토큰 수명 정책은 다음 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-237">The token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="0374d-238">정책이 서비스 주체에 명시적으로 할당된 경우 해당 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-238">If a policy is explicitly assigned to the service principal, it is enforced.</span></span>
* <span data-ttu-id="0374d-239">서비스 주체에 명시적으로 할당된 정책이 없는 경우 서비스 주체의 상위 조직에 명시적으로 할당된 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-239">If no policy is explicitly assigned to the service principal, a policy explicitly assigned to the parent organization of the service principal is enforced.</span></span>
* <span data-ttu-id="0374d-240">서비스 주체 또는 조직에 명시적으로 할당된 정책이 없는 경우 응용 프로그램에 할당된 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-240">If no policy is explicitly assigned to the service principal or to the organization, the policy assigned to the application is enforced.</span></span>
* <span data-ttu-id="0374d-241">서비스 주체, 조직 또는 응용 프로그램 개체에 할당된 정책이 없는 경우 기본값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-241">If no policy has been assigned to the service principal, the organization, or the application object, the default values is enforced.</span></span> <span data-ttu-id="0374d-242">[구성 가능한 토큰 수명 속성](#configurable-token-lifetime-properties)의 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0374d-242">(See the table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="0374d-243">응용 프로그램 개체와 서비스 주체 간의 관계에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 및 서비스 주체 개체](active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0374d-243">For more information about the relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="0374d-244">토큰의 유효성은 토큰이 사용되는 시점에 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-244">A token’s validity is evaluated at the time the token is used.</span></span> <span data-ttu-id="0374d-245">액세스하는 응용 프로그램에 대한 우선 순위가 가장 높은 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-245">The policy with the highest priority on the application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="0374d-246">다음은 예제 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-246">Here's an example scenario.</span></span>
>
> <span data-ttu-id="0374d-247">한 사용자가 두 개의 웹 응용 프로그램에 액세스하려고 하며 하나는 웹 응용 프로그램 A이고 다른 하나는 웹 응용 프로그램 B입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-247">A user wants to access two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="0374d-248">요소:</span><span class="sxs-lookup"><span data-stu-id="0374d-248">Factors:</span></span>
> * <span data-ttu-id="0374d-249">두 웹 응용 프로그램은 모두 동일한 상위 조직에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-249">Both web applications are in the same parent organization.</span></span>
> * <span data-ttu-id="0374d-250">세션 토큰 최대 기간이 8시간인 토큰 수명 정책 1은 상위 조직의 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-250">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as the parent organization’s default.</span></span>
> * <span data-ttu-id="0374d-251">웹 응용 프로그램 A는 어떤 정책에도 연결되지 않은 일반적인 용도의 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-251">Web Application A is a regular-use web application and isn’t linked to any policies.</span></span>
> * <span data-ttu-id="0374d-252">웹 응용 프로그램 B는 매우 중요한 프로세스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-252">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="0374d-253">서비스 주체는 세션 토큰 최대 기간이 30분인 토큰 수명 정책 2에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-253">Its service principal is linked to Token Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="0374d-254">오후 12시에 사용자가 새 브라우저 세션을 시작하고 웹 응용 프로그램 A에 액세스하려고 시도합니다. 이 사용자는 Azure AD로 리디렉션되며 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-254">At 12:00 PM, the user starts a new browser session and tries to access Web Application A. The user is redirected to Azure AD and is asked to sign in.</span></span> <span data-ttu-id="0374d-255">그러면 세션 토큰이 있는 쿠키가 브라우저에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-255">This creates a cookie that has a session token in the browser.</span></span> <span data-ttu-id="0374d-256">사용자는 응용 프로그램에 액세스할 수 있는 ID 토큰으로 웹 응용 프로그램 A로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-256">The user is redirected back to Web Application A with an ID token that allows the user to access the application.</span></span>
>
> <span data-ttu-id="0374d-257">오후 12시 15분에 사용자가 웹 응용 프로그램 B에 액세스하려고 시도합니다. 브라우저는 Azure AD로 리디렉션되고 세션 쿠키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-257">At 12:15 PM, the user tries to access Web Application B. The browser redirects to Azure AD, which detects the session cookie.</span></span> <span data-ttu-id="0374d-258">웹 응용 프로그램 B의 서비스 주체는 토큰 수명 정책 2에 연결되지만 기본 토큰 수명 정책 1이 적용되는 상위 조직의 일부이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-258">Web Application B’s service principal is linked to Token Lifetime Policy 2, but it's also part of the parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="0374d-259">서비스 주체에 연결된 정책이 조직 기본 정책보다 우선 순위가 높기 때문에 토큰 수명 정책 2가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-259">Token Lifetime Policy 2 takes effect because policies linked to service principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="0374d-260">세션 토큰은 지난 30분 이내에 처음 발급되었기 때문에 유효한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-260">The session token was originally issued within the last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="0374d-261">사용자는 액세스 권한을 부여하는 ID 토큰으로 웹 응용 프로그램 B로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-261">The user is redirected back to Web Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="0374d-262">오후 1시에 사용자가 웹 응용 프로그램 A에 액세스하려고 시도합니다. 사용자는 Azure AD로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-262">At 1:00 PM, the user tries to access Web Application A. The user is redirected to Azure AD.</span></span> <span data-ttu-id="0374d-263">웹 응용 프로그램 A는 어떤 정책에도 연결되어 있지 않지만 기본 토큰 수명 정책 1을 사용하는 조직에 있기 때문에 해당 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-263">Web Application A is not linked to any policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="0374d-264">지난 8시간 이내에 발급된 세션 쿠키가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-264">The session cookie that was originally issued within the last eight hours is detected.</span></span> <span data-ttu-id="0374d-265">사용자가 새 ID 토큰을 사용하여 자동으로 웹 응용 프로그램 A로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-265">The user is silently redirected back to Web Application A with a new ID token.</span></span> <span data-ttu-id="0374d-266">사용자가 인증할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-266">The user is not required to authenticate.</span></span>
>
> <span data-ttu-id="0374d-267">그 후 사용자는 웹 응용 프로그램 B에 즉시 액세스하려고 시도합니다. 사용자는 Azure AD로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-267">Immediately afterward, the user tries to access Web Application B. The user is redirected to Azure AD.</span></span> <span data-ttu-id="0374d-268">이전과 마찬가지로 토큰 수명 정책 2가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-268">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="0374d-269">토큰이 발급된 시간이 30분을 넘었기 때문에 사용자에게 로그인 자격 증명을 다시 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-269">Because the token was issued more than 30 minutes ago, the user is prompted to reenter their sign-in credentials.</span></span> <span data-ttu-id="0374d-270">완전히 새로운 세션 토큰 및 ID 토큰이 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-270">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="0374d-271">이제 사용자는 웹 응용 프로그램 B에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-271">The user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="0374d-272">구성 가능한 정책 속성 세부 정보</span><span class="sxs-lookup"><span data-stu-id="0374d-272">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="0374d-273">액세스 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="0374d-273">Access Token Lifetime</span></span>
<span data-ttu-id="0374d-274">**문자열:** AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="0374d-274">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="0374d-275">**영향:** 액세스 토큰, ID 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-275">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="0374d-276">**요약:** 이 정책은 이 리소스에 대한 액세스 및 ID 토큰이 유효한 것으로 간주되는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-276">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="0374d-277">액세스 토큰 수명 속성을 줄이면 악의적인 행위자가 액세스 토큰 또는 ID 토큰을 장시간 사용할 위험을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-277">Reducing the Access Token Lifetime property mitigates the risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="0374d-278">(이러한 토큰은 해지할 수 없습니다.) 그 대신 토큰을 좀 더 자주 교체해야 하기 때문에 성능에 악영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-278">(These tokens cannot be revoked.) The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="0374d-279">새로 고침 토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="0374d-279">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="0374d-280">**문자열:** MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="0374d-280">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="0374d-281">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-281">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="0374d-282">**요약:** 이 정책은 클라이언트에서 이 리소스에 액세스하려고 할 때 새 액세스/새로 고침 토큰을 검색하는 데 새로 고침 토큰을 더 이상 사용할 수 없을 때까지의 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-282">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it to retrieve a new access/refresh token pair when attempting to access this resource.</span></span> <span data-ttu-id="0374d-283">새로 고침 토큰이 사용될 때 일반적으로 새로운 새로 고침 토큰이 반환되기 때문에 클라이언트가 지정된 기간 동안 현재 새로 고침 토큰을 사용하여 리소스에 액세스하려고 시도하면 이 정책에 따라 액세스가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-283">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if the client tries to access any resource by using the current refresh token during the specified period of time.</span></span>

<span data-ttu-id="0374d-284">이 정책은 클라이언트에서 활성화되지 않은 사용자가 새로운 새로 고침 토큰을 검색하려면 다시 인증하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-284">This policy forces users who have not been active on their client to reauthenticate to retrieve a new refresh token.</span></span>

<span data-ttu-id="0374d-285">새로 고침 토큰 최대 비활성 시간 속성은 단일 단계 토큰 최대 기간 및 다단계 새로 고침 토큰 최대 기간 속성보다 낮은 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-285">The Refresh Token Max Inactive Time property must be set to a lower value than the Single-Factor Token Max Age and the Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="0374d-286">단일 단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-286">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="0374d-287">**문자열:** MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-287">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="0374d-288">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-288">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="0374d-289">**요약:** 이 정책은 사용자가 단일 단계만 사용하여 마지막으로 인증에 성공한 후 새로 고침 토큰을 사용하여 새로운 액세스/새로 고침 토큰을 얻을 수 있는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-289">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="0374d-290">사용자는 인증하여 새로운 새로 고침 토큰을 얻은 후 지정된 기간 동안 새로 고침 토큰 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-290">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="0374d-291">(이는 현재 새로 고침 토큰이 해지되지 않고, 비활성 시간보다 오랫동안 사용하지 않은 상태로 남아 있지 않는 한 유효합니다.) 이 시점에서 사용자는 다시 인증하여 새로운 새로 고침 토큰을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-291">(This is true as long as the current refresh token is not revoked, and it is not left unused for longer than the inactive time.) At that point, the user is forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="0374d-292">최대 기간을 줄이면 사용자가 좀 더 자주 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-292">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="0374d-293">단일 단계 인증은 Multi-Factor Authentication보다 안전하지 않으므로 이 속성을 다단계 새로 고침 토큰 최대 기간 속성보다 작거나 같은 값으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-293">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or lesser than the Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="0374d-294">다단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-294">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="0374d-295">**문자열:** MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-295">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="0374d-296">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="0374d-296">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="0374d-297">**요약:** 이 정책은 사용자가 다단계를 사용하여 마지막으로 인증에 성공한 후 새로 고침 토큰을 사용하여 새로운 액세스/새로 고침 토큰을 얻을 수 있는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-297">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="0374d-298">사용자는 인증하여 새로운 새로 고침 토큰을 얻은 후 지정된 기간 동안 새로 고침 토큰 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-298">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="0374d-299">(이는 현재 새로 고침 토큰이 해지되지 않고, 비활성 시간보다 오랫동안 사용하지 않은 상태로 남아 있지 않는 한 유효합니다.) 이 시점에서 사용자는 다시 인증하여 새로운 새로 고침 토큰을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-299">(This is true as long as the current refresh token is not revoked, and it is not unused for longer than the inactive time.) At that point, users are forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="0374d-300">최대 기간을 줄이면 사용자가 좀 더 자주 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-300">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="0374d-301">단일 단계 인증은 Multi-Factor Authentication보다 안전하지 않으므로 이 속성을 단일 단계 새로 고침 토큰 최대 기간 속성보다 크거나 같은 값으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-301">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="0374d-302">단일 단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-302">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="0374d-303">**문자열:** MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-303">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="0374d-304">**영향:** 세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="0374d-304">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="0374d-305">**요약:** 이 정책은 사용자가 단일 단계만 사용하여 마지막으로 인증에 성공한 후 세션 토큰을 사용하여 새로운 ID 및 세션 토큰을 얻을 수 있는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-305">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="0374d-306">사용자는 인증하여 새로운 세션 토큰을 얻은 후 지정된 기간 동안 세션 토큰 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-306">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="0374d-307">(이는 현재 세션 토큰이 해지 및 만료되지 않는 한 유효합니다.) 지정된 시간이 지나면 사용자는 다시 인증하여 새로운 세션 토큰을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-307">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="0374d-308">최대 기간을 줄이면 사용자가 좀 더 자주 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-308">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="0374d-309">단일 단계 인증은 Multi-Factor Authentication보다 안전하지 않으므로 이 속성을 다단계 세션 토큰 최대 기간 속성보다 작거나 같은 값으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-309">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or less than the Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="0374d-310">다단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-310">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="0374d-311">**문자열:** MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="0374d-311">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="0374d-312">**영향:** 세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="0374d-312">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="0374d-313">**요약:** 이 정책은 사용자가 다단계를 사용하여 마지막으로 인증에 성공한 후 세션 토큰을 사용하여 새로운 ID 및 세션 토큰을 얻을 수 있는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-313">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after the last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="0374d-314">사용자는 인증하여 새로운 세션 토큰을 얻은 후 지정된 기간 동안 세션 토큰 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-314">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="0374d-315">(이는 현재 세션 토큰이 해지 및 만료되지 않는 한 유효합니다.) 지정된 시간이 지나면 사용자는 다시 인증하여 새로운 세션 토큰을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-315">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="0374d-316">최대 기간을 줄이면 사용자가 좀 더 자주 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-316">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="0374d-317">단일 단계 인증은 Multi-Factor Authentication보다 안전하지 않으므로 이 속성을 단일 단계 세션 토큰 최대 기간 속성보다 크거나 같은 값으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-317">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="0374d-318">토큰 수명 정책 예제</span><span class="sxs-lookup"><span data-stu-id="0374d-318">Example token lifetime policies</span></span>
<span data-ttu-id="0374d-319">앱, 서비스 주체 및 전체 조직의 토큰 수명을 만들고 관리할 수 있다면 Azure AD에서 다양한 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-319">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="0374d-320">이 섹션에서는 새 규칙을 적용하는 데 도움이 되는 몇 가지 일반적인 정책 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-320">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="0374d-321">토큰 수명</span><span class="sxs-lookup"><span data-stu-id="0374d-321">Token Lifetime</span></span>
* <span data-ttu-id="0374d-322">토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="0374d-322">Token Max Inactive Time</span></span>
* <span data-ttu-id="0374d-323">토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="0374d-323">Token Max Age</span></span>

<span data-ttu-id="0374d-324">이 예제에서는 다음 작업을 수행하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-324">In the examples, you can learn how to:</span></span>

* <span data-ttu-id="0374d-325">조직의 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="0374d-325">Manage an organization's default policy</span></span>
* <span data-ttu-id="0374d-326">웹 로그인에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="0374d-326">Create a policy for web sign-in</span></span>
* <span data-ttu-id="0374d-327">web API를 호출하는 네이티브 앱에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="0374d-327">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="0374d-328">고급 정책 관리</span><span class="sxs-lookup"><span data-stu-id="0374d-328">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0374d-329">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0374d-329">Prerequisites</span></span>
<span data-ttu-id="0374d-330">다음 예제에서는 앱, 서비스 주체 및 조직 전체에 대한 정책을 만들고, 업데이트하고, 연결하고, 삭제해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-330">In the following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="0374d-331">Azure AD을 처음 접하는 분들은 [Azure AD 테넌트를 가져오는 방법](active-directory-howto-tenant.md)을 살펴본 후 예제를 진행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-331">If you are new to Azure AD, we recommend that you learn about [how to get an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="0374d-332">시작하려면 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-332">To get started, do the following steps:</span></span>

1. <span data-ttu-id="0374d-333">최신 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스](https://www.powershellgallery.com/packages/AzureADPreview)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-333">Download the latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="0374d-334">`Connect` 명령을 실행하여 Azure AD 관리자 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-334">Run the `Connect` command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="0374d-335">새 세션을 시작할 때마다 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-335">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="0374d-336">조직에서 만든 모든 정책을 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-336">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="0374d-337">다음 시나리오에서 대부분의 작업 후에 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-337">Run this command after most operations in the following scenarios.</span></span> <span data-ttu-id="0374d-338">이 명령을 실행하면 정책의 ** **을(를) 가져오는 데도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-338">Running the command also helps you get the ** ** of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="0374d-339">예: 조직의 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="0374d-339">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="0374d-340">이 예에서는 사용자가 전체 조직에서 로그인하는 빈도를 줄이는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-340">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="0374d-341">이렇게 하기 위해 전체 조직에 적용되는 단일 단계 새로 고침 토큰에 대한 토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-341">To do this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="0374d-342">이 정책은 조직의 모든 응용 프로그램과 아직 정책이 설정되지 않은 각 서비스 주체에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-342">The policy is applied to every application in your organization, and to each service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="0374d-343">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-343">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="0374d-344">단일 단계 새로 고침 토큰을 "until-revoked"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-344">Set the Single-Factor Refresh Token to "until-revoked."</span></span> <span data-ttu-id="0374d-345">이 토큰은 액세스가 해지될 때까지 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-345">The token doesn't expire until access is revoked.</span></span> <span data-ttu-id="0374d-346">다음 정책 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-346">Create the following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="0374d-347">정책을 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-347">To create the policy, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="0374d-348">새 정책을 보고 정책의 **ObjectId**를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-348">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="0374d-349">정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-349">Update the policy.</span></span>

    <span data-ttu-id="0374d-350">이 예에서 설정한 첫 번째 정책이 서비스에 필요한 만큼 엄격한지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-350">You might decide that the first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="0374d-351">단일 단계 새로 고침 토큰이 이틀 후에 만료되도록 설정하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-351">To set your Single-Factor Refresh Token to expire in two days, run the following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="0374d-352">예: 웹 로그인에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="0374d-352">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="0374d-353">이 예에서는 사용자가 웹앱에 보다 자주 인증하도록 요구하는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-353">In this example, you create a policy that requires users to authenticate more frequently in your web app.</span></span> <span data-ttu-id="0374d-354">이 정책은 액세스/ID 토큰의 수명 및 다단계 세션 토큰의 최대 기간을 웹앱의 서비스 주체로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-354">This policy sets the lifetime of the access/ID tokens and the max age of a multi-factor session token to the service principal of your web app.</span></span>

1. <span data-ttu-id="0374d-355">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-355">Create a token lifetime policy.</span></span>

    <span data-ttu-id="0374d-356">웹 로그인에 대한 이 정책은 액세스/ID 토큰 수명 및 최대 단일 단계 세션 토큰 기간을 2시간으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-356">This policy, for web sign-in, sets the access/ID token lifetime and the max single-factor session token age to two hours.</span></span>

    1.  <span data-ttu-id="0374d-357">정책을 만들려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-357">To create the policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="0374d-358">새 정책을 보고 정책 **ObjectId**를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-358">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="0374d-359">서비스 주체에게 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-359">Assign the policy to your service principal.</span></span> <span data-ttu-id="0374d-360">서비스 주체의 **ObjectId**도 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-360">You also need to get the **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="0374d-361">조직의 모든 서비스 주체를 보려면 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-361">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="0374d-362">또는 [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/)에서 Azure AD 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-362">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in to your Azure AD account.</span></span>

    2.  <span data-ttu-id="0374d-363">서비스 주체의 **ObjectId**가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-363">When you have the **ObjectId** of your service principal, run the following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="0374d-364">예: web API를 호출하는 네이티브 앱에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="0374d-364">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="0374d-365">이 예에서는 사용자가 보다 적게 인증하도록 요구하는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-365">In this example, you create a policy that requires users to authenticate less frequently.</span></span> <span data-ttu-id="0374d-366">또한 이 정책은 사용자가 다시 인증해야 할 때까지 걸리는 비활성 시간을 연장합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-366">The policy also lengthens the amount of time a user can be inactive before the user must reauthenticate.</span></span> <span data-ttu-id="0374d-367">이 정책은 web API에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-367">The policy is applied to the web API.</span></span> <span data-ttu-id="0374d-368">네이티브 앱이 리소스로 web API를 요청하면 이 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-368">When the native app requests the web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="0374d-369">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-369">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="0374d-370">Web API에 대한 엄격한 정책을 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-370">To create a strict policy for a web API, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="0374d-371">새 정책을 보고 정책 **ObjectId**를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-371">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="0374d-372">web API에 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-372">Assign the policy to your web API.</span></span> <span data-ttu-id="0374d-373">응용 프로그램의 **ObjectId**도 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-373">You also need to get the **ObjectId** of your application.</span></span> <span data-ttu-id="0374d-374">앱의 **ObjectId**를 찾는 가장 좋은 방법은 [Azure Portal](https://portal.azure.com/)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-374">The best way to find your app's **ObjectId** is to use the [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="0374d-375">앱의 **ObjectId**가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-375">When you have the **ObjectId** of your app, run the following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of the Application> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="0374d-376">예: 고급 정책 관리</span><span class="sxs-lookup"><span data-stu-id="0374d-376">Example: Manage an advanced policy</span></span>
<span data-ttu-id="0374d-377">이 예에서는 몇 가지 정책을 만들어 보면서 우선 순위 시스템의 작동 방식에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-377">In this example, you create a few policies, to learn how the priority system works.</span></span> <span data-ttu-id="0374d-378">여러 개체에 적용되는 여러 정책을 관리하는 방법도 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-378">You also can learn how to manage multiple policies that are applied to several objects.</span></span>

1. <span data-ttu-id="0374d-379">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-379">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="0374d-380">단일 단계 새로 고침 토큰 수명을 30일로 설정하는 조직 기본 정책을 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-380">To create an organization default policy that sets the Single-Factor Refresh Token lifetime to 30 days, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="0374d-381">새 정책을 보고 정책의 **ObjectId**를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-381">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="0374d-382">서비스 주체에게 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-382">Assign the policy to a service principal.</span></span>

    <span data-ttu-id="0374d-383">이제 조직 전체에 적용되는 정책이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-383">Now, you have a policy that applies to the entire organization.</span></span> <span data-ttu-id="0374d-384">특정 서비스 주체에 대해 이 30일 정책을 유지하지만 조직 기본 정책을 "until-revoked"의 상한으로 변경하고 싶은 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-384">You might want to preserve this 30-day policy for a specific service principal, but change the organization default policy to the upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="0374d-385">조직의 모든 서비스 주체를 보려면 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-385">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="0374d-386">또는 [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/)에서 Azure AD 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-386">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="0374d-387">서비스 주체의 **ObjectId**가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-387">When you have the **ObjectId** of your service principal, run the following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
            ```
        
3. <span data-ttu-id="0374d-388">`IsOrganizationDefault` 플래그를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-388">Set the `IsOrganizationDefault` flag to false:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="0374d-389">새로운 조직 기본 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-389">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="0374d-390">이제 서비스 주체에 연결된 원래 정책과 조직 기본 정책으로 설정된 새 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-390">You now have the original policy linked to your service principal, and the new policy is set as your organization default policy.</span></span> <span data-ttu-id="0374d-391">서비스 주체에 적용되는 정책은 조직 기본 정책보다 우선한다는 점을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-391">It's important to remember that policies applied to service principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="0374d-392">Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="0374d-392">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="0374d-393">정책 관리</span><span class="sxs-lookup"><span data-stu-id="0374d-393">Manage policies</span></span>

<span data-ttu-id="0374d-394">다음 cmdlet을 사용하여 정책을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-394">You can use the following cmdlets to manage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="0374d-395">New-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-395">New-AzureADPolicy</span></span>

<span data-ttu-id="0374d-396">새 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-396">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="0374d-397">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-397">Parameters</span></span> | <span data-ttu-id="0374d-398">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-398">Description</span></span> | <span data-ttu-id="0374d-399">예</span><span class="sxs-lookup"><span data-stu-id="0374d-399">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="0374d-400">정책의 모든 규칙을 포함하는 문자열로 변환된 JSON 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-400">Array of stringified JSON that contains all the policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="0374d-401">정책 이름의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-401">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="0374d-402">true이면 정책을 조직의 기본 정책으로 설정하고</span><span class="sxs-lookup"><span data-stu-id="0374d-402">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="0374d-403">false이면 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-403">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="0374d-404">정책의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-404">Type of policy.</span></span> <span data-ttu-id="0374d-405">토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-405">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="0374d-406"><code>&#8209;AlternativeIdentifier</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-406"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="0374d-407">정책에 대한 대체 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-407">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="0374d-408">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-408">Get-AzureADPolicy</span></span>
<span data-ttu-id="0374d-409">모든 Azure AD 정책 또는 지정된 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-409">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="0374d-410">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-410">Parameters</span></span> | <span data-ttu-id="0374d-411">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-411">Description</span></span> | <span data-ttu-id="0374d-412">예</span><span class="sxs-lookup"><span data-stu-id="0374d-412">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0374d-413"><code>&#8209;Id</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-413"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="0374d-414">원하는 정책의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-414">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="0374d-415">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="0374d-415">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="0374d-416">정책에 연결된 모든 앱 및 서비스 주체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-416">Gets all apps and service principals that are linked to a policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="0374d-417">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-417">Parameters</span></span> | <span data-ttu-id="0374d-418">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-418">Description</span></span> | <span data-ttu-id="0374d-419">예</span><span class="sxs-lookup"><span data-stu-id="0374d-419">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-420">원하는 정책의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-420">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="0374d-421">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-421">Set-AzureADPolicy</span></span>
<span data-ttu-id="0374d-422">기존 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-422">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="0374d-423">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-423">Parameters</span></span> | <span data-ttu-id="0374d-424">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-424">Description</span></span> | <span data-ttu-id="0374d-425">예</span><span class="sxs-lookup"><span data-stu-id="0374d-425">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-426">원하는 정책의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-426">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="0374d-427">정책 이름의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-427">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="0374d-428"><code>&#8209;Definition</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-428"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="0374d-429">정책의 모든 규칙을 포함하는 문자열로 변환된 JSON 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-429">Array of stringified JSON that contains all the policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="0374d-430"><code>&#8209;IsOrganizationDefault</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-430"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="0374d-431">true이면 정책을 조직의 기본 정책으로 설정하고</span><span class="sxs-lookup"><span data-stu-id="0374d-431">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="0374d-432">false이면 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-432">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="0374d-433"><code>&#8209;Type</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-433"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="0374d-434">정책의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-434">Type of policy.</span></span> <span data-ttu-id="0374d-435">토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-435">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="0374d-436"><code>&#8209;AlternativeIdentifier</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="0374d-436"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="0374d-437">정책에 대한 대체 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-437">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="0374d-438">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-438">Remove-AzureADPolicy</span></span>
<span data-ttu-id="0374d-439">지정된 정책을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-439">Deletes the specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="0374d-440">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-440">Parameters</span></span> | <span data-ttu-id="0374d-441">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-441">Description</span></span> | <span data-ttu-id="0374d-442">예</span><span class="sxs-lookup"><span data-stu-id="0374d-442">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-443">원하는 정책의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-443">**ObjectId (Id)** of the policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="0374d-444">응용 프로그램 정책</span><span class="sxs-lookup"><span data-stu-id="0374d-444">Application policies</span></span>
<span data-ttu-id="0374d-445">응용 프로그램 정책에 다음 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-445">You can use the following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="0374d-446">Add-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-446">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="0374d-447">지정된 정책을 응용 프로그램에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-447">Links the specified policy to an application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="0374d-448">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-448">Parameters</span></span> | <span data-ttu-id="0374d-449">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-449">Description</span></span> | <span data-ttu-id="0374d-450">예</span><span class="sxs-lookup"><span data-stu-id="0374d-450">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-451">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-451">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="0374d-452">정책의 **ObjectId**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-452">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="0374d-453">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-453">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="0374d-454">응용 프로그램에 할당된 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-454">Gets the policy that is assigned to an application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="0374d-455">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-455">Parameters</span></span> | <span data-ttu-id="0374d-456">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-456">Description</span></span> | <span data-ttu-id="0374d-457">예</span><span class="sxs-lookup"><span data-stu-id="0374d-457">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-458">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-458">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="0374d-459">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-459">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="0374d-460">응용 프로그램에서 정책을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-460">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="0374d-461">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-461">Parameters</span></span> | <span data-ttu-id="0374d-462">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-462">Description</span></span> | <span data-ttu-id="0374d-463">예</span><span class="sxs-lookup"><span data-stu-id="0374d-463">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-464">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-464">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="0374d-465">정책의 **ObjectId**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-465">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="0374d-466">서비스 사용자 정책</span><span class="sxs-lookup"><span data-stu-id="0374d-466">Service principal policies</span></span>
<span data-ttu-id="0374d-467">서비스 주체 정책에 다음 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-467">You can use the following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="0374d-468">Add-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-468">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="0374d-469">지정된 정책을 서비스 주체에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-469">Links the specified policy to a service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="0374d-470">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-470">Parameters</span></span> | <span data-ttu-id="0374d-471">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-471">Description</span></span> | <span data-ttu-id="0374d-472">예</span><span class="sxs-lookup"><span data-stu-id="0374d-472">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-473">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-473">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="0374d-474">정책의 **ObjectId**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-474">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="0374d-475">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-475">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="0374d-476">지정된 서비스 주체에 연결된 모든 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-476">Gets any policy linked to the specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="0374d-477">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-477">Parameters</span></span> | <span data-ttu-id="0374d-478">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-478">Description</span></span> | <span data-ttu-id="0374d-479">예</span><span class="sxs-lookup"><span data-stu-id="0374d-479">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-480">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-480">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="0374d-481">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="0374d-481">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="0374d-482">지정된 서비스 주체에서 정책을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-482">Removes the policy from the specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="0374d-483">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0374d-483">Parameters</span></span> | <span data-ttu-id="0374d-484">설명</span><span class="sxs-lookup"><span data-stu-id="0374d-484">Description</span></span> | <span data-ttu-id="0374d-485">예</span><span class="sxs-lookup"><span data-stu-id="0374d-485">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="0374d-486">응용 프로그램의 **ObjectId(ID)**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-486">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="0374d-487">정책의 **ObjectId**입니다.</span><span class="sxs-lookup"><span data-stu-id="0374d-487">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
