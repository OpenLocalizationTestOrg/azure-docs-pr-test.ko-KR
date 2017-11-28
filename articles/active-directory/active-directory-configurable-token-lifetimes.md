---
title: "Azure Active Directory에서 토큰 수명 aaaConfigurable | Microsoft Docs"
description: "Tooset 수명 토큰에 대 한 Azure AD에서 발급 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="abc80-103">Azure Active Directory에서 구성 가능한 토큰 수명(공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="abc80-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="abc80-104">Azure Active Directory (Azure AD)에서 발급 한 토큰의 hello 수명을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-104">You can specify hello lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="abc80-105">조직의 모든 앱, 다중 테넌트(다중 조직) 응용 프로그램 또는 조직의 특정 서비스 주체에 대해 토큰 수명을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="abc80-106">이 기능은 현재 공개 미리 보기로 제공되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="abc80-107">Toorevert 준비 하거나 변경 내용을 모두 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-107">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="abc80-108">hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-108">hello feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="abc80-109">그러나 hello 기능이 일반 공급 되 면 일부의 hello 기능이 필요할 수 있습니다는 [Azure Active Directory Premium](active-directory-get-started-premium.md) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-109">However, when hello feature becomes generally available, some aspects of hello feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="abc80-110">Azure AD에서 정책 개체는 개별 응용 프로그램 또는 조직의 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="abc80-111">각 정책 형식에 적용 된 tooobjects toowhich가 할당 되는 속성 집합으로는 고유한 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-111">Each policy type has a unique structure, with a set of properties that are applied tooobjects toowhich they are assigned.</span></span>

<span data-ttu-id="abc80-112">조직에 대 한 정책을 hello 기본 정책으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-112">You can designate a policy as hello default policy for your organization.</span></span> <span data-ttu-id="abc80-113">hello 정책은 더 높은 우선 순위를 가진 정책에 의해 재정의 되지 않은 상태로 hello 조직에 적용 된 tooany 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-113">hello policy is applied tooany application in hello organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="abc80-114">또한 할당할 수 있습니다 정책 toospecific 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="abc80-114">You also can assign a policy toospecific applications.</span></span> <span data-ttu-id="abc80-115">우선 순위에 따라 hello 정책 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-115">hello order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="abc80-116">토큰 형식</span><span class="sxs-lookup"><span data-stu-id="abc80-116">Token types</span></span>

<span data-ttu-id="abc80-117">새로 고침 토큰, 액세스 토큰, 세션 토큰 및 ID 토큰에 대한 토큰 수명 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="abc80-118">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-118">Access tokens</span></span>
<span data-ttu-id="abc80-119">액세스를 사용 하는 클라이언트 tooaccess 보호 된 리소스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-119">Clients use access tokens tooaccess a protected resource.</span></span> <span data-ttu-id="abc80-120">액세스 토큰은 사용자, 클라이언트 및 리소스의 특정 조합에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="abc80-121">액세스 토큰은 해지될 수 없으며 만료될 때까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="abc80-122">액세스 토큰을 획득한 악의적인 행위자는 수명 범위 동안 이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="abc80-123">Hello 수명을 조정 하는 액세스 토큰은 시스템 성능 향상 사이의 절충 하며 증가 hello 클라이언트 hello는 시간의 양을 보유 액세스 hello 사용자 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-123">Adjusting hello lifetime of an access token is a trade-off between improving system performance and increasing hello amount of time that hello client retains access after hello user’s account is disabled.</span></span> <span data-ttu-id="abc80-124">향상 된 시스템 성능을 낼 수 클라이언트 tooacquire 새 액세스 토큰을 필요한 시간이 hello 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-124">Improved system performance is achieved by reducing hello number of times a client needs tooacquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="abc80-125">새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-125">Refresh tokens</span></span>
<span data-ttu-id="abc80-126">클라이언트가 보호 된 리소스는 액세스 토큰 tooaccess 가져오면 hello 클라이언트가 모두 새로 고침 토큰 및 액세스 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-126">When a client acquires an access token tooaccess a protected resource, hello client receives both a refresh token and an access token.</span></span> <span data-ttu-id="abc80-127">hello 새로 고침 토큰 hello 현재 액세스 토큰이 만료 될 때 사용 되는 tooobtain 새로운 액세스/새로 고침 토큰 쌍은입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-127">hello refresh token is used tooobtain new access/refresh token pairs when hello current access token expires.</span></span> <span data-ttu-id="abc80-128">새로 고침 토큰은 사용자와 클라이언트의 바인딩된 tooa 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-128">A refresh token is bound tooa combination of user and client.</span></span> <span data-ttu-id="abc80-129">새로 고침 토큰 이며 해지할 수 및 hello 토큰을 사용할 때마다 hello 토큰의 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-129">A refresh token can be revoked, and hello token's validity is checked every time hello token is used.</span></span>

<span data-ttu-id="abc80-130">것이 중요 한 toomake 기밀 클라이언트 및 클라이언트에 공용 구별 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-130">It's important toomake a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="abc80-131">다양한 유형의 클라이언트에 대한 자세한 내용은 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abc80-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="abc80-132">비밀 클라이언트 새로 고침 토큰의 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="abc80-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="abc80-133">비밀 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="abc80-134">악의적인 행위자 아닌 hello 클라이언트 응용 프로그램에서 요청이 들어오는지를 증명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-134">They can prove that requests are coming from hello client application and not from a malicious actor.</span></span> <span data-ttu-id="abc80-135">예를 들어 웹 응용 프로그램은 기밀 클라이언트 hello 웹 서버에서 클라이언트 암호를 저장할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-135">For example, a web app is a confidential client because it can store a client secret on hello web server.</span></span> <span data-ttu-id="abc80-136">따라서 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-136">It is not exposed.</span></span> <span data-ttu-id="abc80-137">이러한 흐름에서 보다 안전한 되므로 hello 발급된 toothese 흐름은 새로 고침 토큰의 기본 수명 `until-revoked`, 정책을 사용 하 여 변경할 수 없습니다 및 자발적 암호 재설정에 취소 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-137">Because these flows are more secure, hello default lifetimes of refresh tokens issued toothese flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="abc80-138">공용 클라이언트 새로 고침 토큰의 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="abc80-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="abc80-139">공용 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="abc80-140">예를 들어 iOS/Android 앱 수 없는 난독 처리 hello 리소스 소유자 로부터 암호 공용 클라이언트의 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-140">For example, an iOS/Android app cannot obfuscate a secret from hello resource owner, so it is considered a public client.</span></span> <span data-ttu-id="abc80-141">정책을 설정할 수 있습니다 리소스에 tooprevent 새로 고침 토큰은 새 액세스/새로 고침 토큰 쌍 하지 못하도록 지정 된 기간 보다 오래 된 공용 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="abc80-141">You can set policies on resources tooprevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="abc80-142">(toodo이를 사용 하 여 hello 토큰 최대 비활성 시간이 새로 고침 속성입니다.) 정책 tooset hello 새로 고침 토큰을 벗어나는 기간 증명이 더 이상 사용할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-142">(toodo this, use hello Refresh Token Max Inactive Time property.) You also can use policies tooset a period beyond which hello refresh tokens are no longer accepted.</span></span> <span data-ttu-id="abc80-143">(toodo이를 사용 하 여 hello 속성 새로 고침 토큰 최대 처리 기간입니다.) Hello 수명의 시기와 빈도 hello 사용자가 자동으로 검색, 공용 클라이언트 응용 프로그램을 사용 하는 경우 대신 필요한 tooreenter 자격 증명, 새로 고침 토큰 toocontrol 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-143">(toodo this, use hello Refresh Token Max Age property.) You can adjust hello lifetime of a refresh token toocontrol when and how often hello user is required tooreenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="abc80-144">ID 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-144">ID tokens</span></span>
<span data-ttu-id="abc80-145">ID 토큰 toowebsites 및 네이티브 클라이언트에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-145">ID tokens are passed toowebsites and native clients.</span></span> <span data-ttu-id="abc80-146">ID 토큰은 사용자에 대한 프로필 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="abc80-147">ID 토큰은 사용자와 클라이언트의 바인딩된 tooa 특정 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-147">An ID token is bound tooa specific combination of user and client.</span></span> <span data-ttu-id="abc80-148">ID 토큰은 만료될 때까지 유효한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="abc80-149">웹 응용 프로그램에서 사용자를 일치 하는 일반적으로 hello ID 토큰의 hello 응용 프로그램 toohello 수명에서 세션 수명의 hello 사용자에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-149">Usually, a web application matches a user’s session lifetime in hello application toohello lifetime of hello ID token issued for hello user.</span></span> <span data-ttu-id="abc80-150">ID 토큰 toocontrol 얼마나 자주 hello 응용 프로그램 세션 및 (자동으로 또는 대화형)을 Azure AD와 다시 인증할 hello 사용자 toobe 필요 얼마나 자주 hello 웹 응용 프로그램 만료 됨의 hello 수명을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-150">You can adjust hello lifetime of an ID token toocontrol how often hello web application expires hello application session, and how often it requires hello user toobe reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="abc80-151">Single Sign-On 세션 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-151">Single sign-on session tokens</span></span>
<span data-ttu-id="abc80-152">사용자를 Azure AD를 인증 하 고 선택 하는 hello **로그인 상태 유지** 확인란을 hello 사용자의 브라우저와 Azure AD는 single sign-on (SSO) 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-152">When a user authenticates with Azure AD and selects hello **Keep me signed in** check box, a single sign-on session (SSO) is established with hello user’s browser and Azure AD.</span></span> <span data-ttu-id="abc80-153">쿠키의 hello 형태로 hello SSO 토큰이이 세션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-153">hello SSO token, in hello form of a cookie, represents this session.</span></span> <span data-ttu-id="abc80-154">Note hello SSO 세션 토큰 바인딩된 tooa 특정 리소스/클라이언트 응용 프로그램이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-154">Note that hello SSO session token is not bound tooa specific resource/client application.</span></span> <span data-ttu-id="abc80-155">SSO 세션 토큰은 해지 가능하며 사용될 때마다 토큰의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="abc80-156">Azure AD는 두 종류의 SSO 세션 토큰을 사용합니다. 하나는 영구 세션 토큰이고 다른 하나는 비영구 세션 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="abc80-157">영구 세션 토큰 hello 브라우저에서 영구 쿠키로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-157">Persistent session tokens are stored as persistent cookies by hello browser.</span></span> <span data-ttu-id="abc80-158">비영구 세션 토큰은 세션 쿠키로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="abc80-159">(Hello 브라우저를 닫을 때 세션 쿠키 제거 됨 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="abc80-159">(Session cookies are destroyed when hello browser is closed.)</span></span>

<span data-ttu-id="abc80-160">비영구 세션 토큰의 수명은 24시간입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="abc80-161">영구 토큰의 수명은 180일입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="abc80-162">SSO 세션 토큰의 유효 기간이 내에서 사용 되는 언제 든 지 다른 24 시간 또는 hello 토큰 유형에 따라 180 일 hello 유효 기간 연장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-162">Any time an SSO session token is used within its validity period, hello validity period is extended another 24 hours or 180 days, depending on hello token type.</span></span> <span data-ttu-id="abc80-163">유효 기간 내에 SSO 세션 토큰을 사용하지 않으면 만료된 것으로 간주하여 더 이상 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="abc80-164">정책 tooset hello 시간 초과 hello 세션 토큰은 더 이상 받지 않습니다 hello 첫 번째 세션 토큰 발급 된 후 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-164">You can use a policy tooset hello time after hello first session token was issued beyond which hello session token is no longer accepted.</span></span> <span data-ttu-id="abc80-165">(toodo이를 사용 하 여 hello 세션 토큰의 최대 처리 기간 속성입니다.) 사용자가 필요한 tooreenter 자격 증명을 자동으로 인증을 받은 웹 응용 프로그램을 사용 하는 경우 대신 시기와 빈도 세션 토큰 toocontrol의 hello 수명을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-165">(toodo this, use hello Session Token Max Age property.) You can adjust hello lifetime of a session token toocontrol when and how often a user is required tooreenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="abc80-166">토큰 수명 정책 속성</span><span class="sxs-lookup"><span data-stu-id="abc80-166">Token lifetime policy properties</span></span>
<span data-ttu-id="abc80-167">토큰 수명 정책은 토큰 수명 규칙을 포함하는 정책 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="abc80-168">Hello 정책 toocontrol의 hello 속성을 사용 하 여 토큰 수명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-168">Use hello properties of hello policy toocontrol specified token lifetimes.</span></span> <span data-ttu-id="abc80-169">설정 된 정책이 hello 시스템 hello 기본 수명 값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-169">If no policy is set, hello system enforces hello default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="abc80-170">구성 가능한 토큰 수명 속성</span><span class="sxs-lookup"><span data-stu-id="abc80-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="abc80-171">속성</span><span class="sxs-lookup"><span data-stu-id="abc80-171">Property</span></span> | <span data-ttu-id="abc80-172">정책 속성 문자열</span><span class="sxs-lookup"><span data-stu-id="abc80-172">Policy property string</span></span> | <span data-ttu-id="abc80-173">영향</span><span class="sxs-lookup"><span data-stu-id="abc80-173">Affects</span></span> | <span data-ttu-id="abc80-174">기본값</span><span class="sxs-lookup"><span data-stu-id="abc80-174">Default</span></span> | <span data-ttu-id="abc80-175">최소</span><span class="sxs-lookup"><span data-stu-id="abc80-175">Minimum</span></span> | <span data-ttu-id="abc80-176">최대</span><span class="sxs-lookup"><span data-stu-id="abc80-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="abc80-177">액세스 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="abc80-177">Access Token Lifetime</span></span> |<span data-ttu-id="abc80-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="abc80-178">AccessTokenLifetime</span></span> |<span data-ttu-id="abc80-179">액세스 토큰, ID 토큰, SAML2 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="abc80-180">1시간</span><span class="sxs-lookup"><span data-stu-id="abc80-180">1 hour</span></span> |<span data-ttu-id="abc80-181">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-181">10 minutes</span></span> |<span data-ttu-id="abc80-182">1일</span><span class="sxs-lookup"><span data-stu-id="abc80-182">1 day</span></span> |
| <span data-ttu-id="abc80-183">새로 고침 토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="abc80-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="abc80-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="abc80-184">MaxInactiveTime</span></span> |<span data-ttu-id="abc80-185">새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-185">Refresh tokens</span></span> |<span data-ttu-id="abc80-186">14일</span><span class="sxs-lookup"><span data-stu-id="abc80-186">14 days</span></span> |<span data-ttu-id="abc80-187">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-187">10 minutes</span></span> |<span data-ttu-id="abc80-188">90일</span><span class="sxs-lookup"><span data-stu-id="abc80-188">90 days</span></span> |
| <span data-ttu-id="abc80-189">단일 단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="abc80-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="abc80-191">새로 고침 토큰(모든 사용자)</span><span class="sxs-lookup"><span data-stu-id="abc80-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="abc80-192">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="abc80-192">Until-revoked</span></span> |<span data-ttu-id="abc80-193">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-193">10 minutes</span></span> |<span data-ttu-id="abc80-194">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="abc80-195">다단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="abc80-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="abc80-197">새로 고침 토큰(모든 사용자)</span><span class="sxs-lookup"><span data-stu-id="abc80-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="abc80-198">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="abc80-198">Until-revoked</span></span> |<span data-ttu-id="abc80-199">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-199">10 minutes</span></span> |<span data-ttu-id="abc80-200">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="abc80-201">단일 단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="abc80-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="abc80-203">세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="abc80-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="abc80-204">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="abc80-204">Until-revoked</span></span> |<span data-ttu-id="abc80-205">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-205">10 minutes</span></span> |<span data-ttu-id="abc80-206">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="abc80-207">다단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="abc80-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="abc80-209">세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="abc80-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="abc80-210">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="abc80-210">Until-revoked</span></span> |<span data-ttu-id="abc80-211">10분</span><span class="sxs-lookup"><span data-stu-id="abc80-211">10 minutes</span></span> |<span data-ttu-id="abc80-212">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="abc80-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="abc80-213"><sup>1</sup>365 일 hello 길이 제한이 명시적이 특성에 대해 설정할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-213"><sup>1</sup>365 days is hello maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="abc80-214"><sup>2</sup>경우 **MaxAgeSessionSingleFactor** hello를 사용 하는이 값을 설정 하지 않으면 **MaxAgeSingleFactor** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes hello **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="abc80-215">두 매개 변수가 설정 된 hello 속성 (까지 해지 된) hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-215">If neither parameter is set, hello property takes hello default value (until-revoked).</span></span>
* <span data-ttu-id="abc80-216"><sup>3</sup>경우 **MaxAgeSessionMultiFactor** hello를 사용 하는이 값을 설정 하지 않으면 **MaxAgeMultiFactor** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes hello **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="abc80-217">두 매개 변수가 설정 된 hello 속성 (까지 해지 된) hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-217">If neither parameter is set, hello property takes hello default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="abc80-218">예외</span><span class="sxs-lookup"><span data-stu-id="abc80-218">Exceptions</span></span>
| <span data-ttu-id="abc80-219">속성</span><span class="sxs-lookup"><span data-stu-id="abc80-219">Property</span></span> | <span data-ttu-id="abc80-220">영향</span><span class="sxs-lookup"><span data-stu-id="abc80-220">Affects</span></span> | <span data-ttu-id="abc80-221">기본값</span><span class="sxs-lookup"><span data-stu-id="abc80-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abc80-222">새로 고침 토큰 최대 기간(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="abc80-222">Refresh Token Max Age (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="abc80-223">새로 고침 토큰(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="abc80-223">Refresh tokens (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="abc80-224">12시간</span><span class="sxs-lookup"><span data-stu-id="abc80-224">12 hours</span></span> |
| <span data-ttu-id="abc80-225">새로 고침 토큰 최대 비활성 시간(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="abc80-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="abc80-226">새로 고침 토큰(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="abc80-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="abc80-227">90일</span><span class="sxs-lookup"><span data-stu-id="abc80-227">90 days</span></span> |
| <span data-ttu-id="abc80-228">새로 고침 토큰 최대 기간(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="abc80-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="abc80-229">새로 고침 토큰(비밀 클라이언트에 대해 발급됨)</span><span class="sxs-lookup"><span data-stu-id="abc80-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="abc80-230">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="abc80-230">Until-revoked</span></span> |

* <span data-ttu-id="abc80-231"><sup>1</sup>없는 경우에 모든 사용자 포함 부족 하 여 해지 정보를 가진 페더레이션 사용자 hello "LastPasswordChangeTimestamp" 특성을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-231"><sup>1</sup>Federated users who have insufficient revocation information include any users who do not have hello "LastPasswordChangeTimestamp" attribute synced.</span></span> <span data-ttu-id="abc80-232">이러한 증명이 사용자가 짧은 최대 처리 기간 AAD toorevoke 토큰을 연결 이전 (예: 변경 된 암호) 자격 증명 길이 해당 hello 사용자 더 자주 tooensure에 다시 확인 해야 tooan 없습니다 tooverify 되어 있기 때문에 계속 해 서 연결 된 토큰 에 좋은 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-232">These users are given this short Max Age because AAD is unable tooverify when toorevoke tokens that are tied tooan old credential (such as a password that has been changed) and must check back in more frequently tooensure that hello user and associated tokens are still in good standing.</span></span> <span data-ttu-id="abc80-233">tooimprove admins 동기화는 확인 해야 하는 테 넌 트가이 환경을 hello "LastPasswordChangeTimestamp" 특성 (설정할 수 있습니다 AADSync 또는 Powershell을 사용 하 여 hello 사용자 개체에).</span><span class="sxs-lookup"><span data-stu-id="abc80-233">tooimprove this experience, tenant admins must ensure that they are syncing hello “LastPasswordChangeTimestamp” attribute (this can be set on hello user object using Powershell or through AADSync).</span></span>

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="abc80-234">정책 평가 및 우선 순위 지정</span><span class="sxs-lookup"><span data-stu-id="abc80-234">Policy evaluation and prioritization</span></span>
<span data-ttu-id="abc80-235">수 만들고 토큰 수명 정책 tooa 특정 응용 프로그램, tooyour 조직 및 tooservice 보안 주체를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-235">You can create and then assign a token lifetime policy tooa specific application, tooyour organization, and tooservice principals.</span></span> <span data-ttu-id="abc80-236">여러 정책을 tooa 특정 응용 프로그램을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-236">Multiple policies might apply tooa specific application.</span></span> <span data-ttu-id="abc80-237">hello 토큰 수명 정책을 적용 하는 이러한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-237">hello token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="abc80-238">정책을 명시적으로 toohello 서비스 사용자를 할당 하 고, 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-238">If a policy is explicitly assigned toohello service principal, it is enforced.</span></span>
* <span data-ttu-id="abc80-239">정책이 명시적으로 할당 된 toohello 서비스 사용자 인 경우 hello 서비스 사용자의 toohello 모 조직을 명시적으로 할당 하는 정책이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-239">If no policy is explicitly assigned toohello service principal, a policy explicitly assigned toohello parent organization of hello service principal is enforced.</span></span>
* <span data-ttu-id="abc80-240">할당 된 정책이 명시적으로 toohello 서비스 사용자 또는 toohello 조직, toohello 응용 프로그램을 할당 하는 hello 정책 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-240">If no policy is explicitly assigned toohello service principal or toohello organization, hello policy assigned toohello application is enforced.</span></span>
* <span data-ttu-id="abc80-241">정책이 없는 toohello 서비스 보안 주체, hello 조직 또는 hello application 개체 hello 기본 값에 할당 된 경우 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-241">If no policy has been assigned toohello service principal, hello organization, or hello application object, hello default values is enforced.</span></span> <span data-ttu-id="abc80-242">(Hello 표를 참조 [구성 가능한 토큰 수명 속성](#configurable-token-lifetime-properties).)</span><span class="sxs-lookup"><span data-stu-id="abc80-242">(See hello table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="abc80-243">응용 프로그램 개체 및 서비스 사용자 개체 간의 관계 hello에 대 한 자세한 내용은 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-243">For more information about hello relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="abc80-244">토큰의 유효성은 hello 토큰을 사용 하는 hello 시 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-244">A token’s validity is evaluated at hello time hello token is used.</span></span> <span data-ttu-id="abc80-245">hello 정책 hello 우선 순위가 가장 높은 액세스 하는 hello 응용 프로그램에 적용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-245">hello policy with hello highest priority on hello application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="abc80-246">다음은 예제 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-246">Here's an example scenario.</span></span>
>
> <span data-ttu-id="abc80-247">사용자가 두 tooaccess 웹 응용 프로그램: 웹 응용 프로그램 A와 웹 응용 프로그램 B</span><span class="sxs-lookup"><span data-stu-id="abc80-247">A user wants tooaccess two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="abc80-248">요소:</span><span class="sxs-lookup"><span data-stu-id="abc80-248">Factors:</span></span>
> * <span data-ttu-id="abc80-249">웹 응용 프로그램은 모두 hello에 조직 부모 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-249">Both web applications are in hello same parent organization.</span></span>
> * <span data-ttu-id="abc80-250">세션 토큰 최대 기간이 8 시간이 토큰 수명 정책 1 hello 모 조직 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-250">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as hello parent organization’s default.</span></span>
> * <span data-ttu-id="abc80-251">웹 응용 프로그램 A 일반을 사용 하 여 웹 응용 프로그램 이며 연결 된 tooany 정책을 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-251">Web Application A is a regular-use web application and isn’t linked tooany policies.</span></span>
> * <span data-ttu-id="abc80-252">웹 응용 프로그램 B는 매우 중요한 프로세스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-252">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="abc80-253">서비스 사용자는 세션 토큰 최대 처리 기간을 30 분에 연결 된 tooToken 수명 정책 2 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-253">Its service principal is linked tooToken Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="abc80-254">오후 12시 hello 사용자가 새 브라우저 세션을 시작할 시도 tooaccess 웹 응용 프로그램 1. hello 사용자 한 리디렉션된 tooAzure AD가 toosign에서 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-254">At 12:00 PM, hello user starts a new browser session and tries tooaccess Web Application A. hello user is redirected tooAzure AD and is asked toosign in.</span></span> <span data-ttu-id="abc80-255">Hello 브라우저에서 세션 토큰에 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-255">This creates a cookie that has a session token in hello browser.</span></span> <span data-ttu-id="abc80-256">hello 사용자 수 있도록 하는 hello 사용자 tooaccess hello ID 토큰으로 리디렉션된 백 tooWeb 응용 프로그램 A가입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-256">hello user is redirected back tooWeb Application A with an ID token that allows hello user tooaccess hello application.</span></span>
>
> <span data-ttu-id="abc80-257">오후 12 시 15 분 hello 사용자 tooaccess 웹 응용 프로그램 B. hello 브라우저 리디렉션 tooAzure hello 세션 쿠키를 검색 하는 광고를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-257">At 12:15 PM, hello user tries tooaccess Web Application B. hello browser redirects tooAzure AD, which detects hello session cookie.</span></span> <span data-ttu-id="abc80-258">웹 응용 프로그램 B의 서비스 사용자가 연결 된 tooToken 수명 정책 2 하지만 hello 모 조직, 기본값은 토큰 수명 정책 1의 일부 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-258">Web Application B’s service principal is linked tooToken Lifetime Policy 2, but it's also part of hello parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="abc80-259">토큰 수명 정책 2 정책 tooservice 연결 된 보안 주체 보다 우선 순위가 더 높은 조직 기본 정책 때문에 적용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-259">Token Lifetime Policy 2 takes effect because policies linked tooservice principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="abc80-260">hello 세션 토큰이 원래 발급 된 hello 내에서 마지막 30 분 때문에 유효한 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-260">hello session token was originally issued within hello last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="abc80-261">hello 사용자 액세스 권한을 부여 하는 ID 토큰으로 리디렉션된 백 tooWeb 응용 프로그램 B는입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-261">hello user is redirected back tooWeb Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="abc80-262">오후 1 시에 hello 사용자 시도 tooaccess 웹 응용 프로그램 1. hello 사용자는 리디렉션된 tooAzure AD는입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-262">At 1:00 PM, hello user tries tooaccess Web Application A. hello user is redirected tooAzure AD.</span></span> <span data-ttu-id="abc80-263">웹 응용 프로그램 A는 연결 된 tooany 정책 없지만 기본 토큰 수명은 정책 1 있는 조직에서 이기 때문에 해당 정책에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-263">Web Application A is not linked tooany policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="abc80-264">원래 실행 된 hello 내에서 마지막 8 시간 hello 세션 쿠키를 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-264">hello session cookie that was originally issued within hello last eight hours is detected.</span></span> <span data-ttu-id="abc80-265">hello 사용자가 자동으로 리디렉션된 백 tooWeb 응용 프로그램 A를 새 ID 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-265">hello user is silently redirected back tooWeb Application A with a new ID token.</span></span> <span data-ttu-id="abc80-266">hello 사용자가 필요한 tooauthenticate 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-266">hello user is not required tooauthenticate.</span></span>
>
> <span data-ttu-id="abc80-267">Hello 사용자가 나중에 즉시 tooaccess 웹 응용 프로그램 B. hello 사용자는 리디렉션된 tooAzure AD입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-267">Immediately afterward, hello user tries tooaccess Web Application B. hello user is redirected tooAzure AD.</span></span> <span data-ttu-id="abc80-268">이전과 마찬가지로 토큰 수명 정책 2가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-268">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="abc80-269">Hello 사용자 프롬프트 tooreenter가 30 분 넘게, hello 토큰이 발급 된 때문에 해당 로그인 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-269">Because hello token was issued more than 30 minutes ago, hello user is prompted tooreenter their sign-in credentials.</span></span> <span data-ttu-id="abc80-270">완전히 새로운 세션 토큰 및 ID 토큰이 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-270">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="abc80-271">hello 사용자 웹 응용 프로그램 2. 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-271">hello user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="abc80-272">구성 가능한 정책 속성 세부 정보</span><span class="sxs-lookup"><span data-stu-id="abc80-272">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="abc80-273">액세스 토큰 수명</span><span class="sxs-lookup"><span data-stu-id="abc80-273">Access Token Lifetime</span></span>
<span data-ttu-id="abc80-274">**문자열:** AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="abc80-274">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="abc80-275">**영향:** 액세스 토큰, ID 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-275">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="abc80-276">**요약:** 이 정책은 이 리소스에 대한 액세스 및 ID 토큰이 유효한 것으로 간주되는 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-276">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="abc80-277">액세스 토큰 또는 오랜 시간에 대 한 악의적인 행위자에서 사용 하 고 ID 토큰의 hello 위험을 완화 시키는 hello 액세스 토큰 수명 속성 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-277">Reducing hello Access Token Lifetime property mitigates hello risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="abc80-278">(이러한 토큰을 취소할 수 없습니다.) hello 대신 hello 토큰 교체를 더 자주 toobe 때문에 성능이 나쁜 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-278">(These tokens cannot be revoked.) hello trade-off is that performance is adversely affected, because hello tokens have toobe replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="abc80-279">새로 고침 토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="abc80-279">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="abc80-280">**문자열:** MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="abc80-280">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="abc80-281">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-281">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="abc80-282">**요약:** 오래 된 새로 고침 토큰 일 수 없습니다 클라이언트가 사용할 수는 더 이상 새 액세스/새로 고침 토큰 쌍 tooretrieve tooaccess이이 리소스를 시도할 때이 정책을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-282">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it tooretrieve a new access/refresh token pair when attempting tooaccess this resource.</span></span> <span data-ttu-id="abc80-283">새로 고침 토큰이 사용 될 때 새로운 새로 고침 토큰 반환은 일반적으로, 때문에이 정책을 hello 클라이언트 tooaccess 지정 된 기간 동안 hello 동안 hello 현재 새로 고침 토큰을 사용 하 여 모든 리소스를 시도 하는 경우 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-283">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if hello client tries tooaccess any resource by using hello current refresh token during hello specified period of time.</span></span>

<span data-ttu-id="abc80-284">이 정책이 사용자에 게 해당 클라이언트 tooreauthenticate tooretrieve 새로운 새로 고침 토큰에서 활성화 되지 않은 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-284">This policy forces users who have not been active on their client tooreauthenticate tooretrieve a new refresh token.</span></span>

<span data-ttu-id="abc80-285">hello 단일 요소 토큰 최대 처리 기간 보다 더 낮은 값 tooa 및 hello Multi-factor 새로 고침 토큰 최대 처리 기간 속성 hello 토큰 최대 비활성 시간이 새로 고침 속성을 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-285">hello Refresh Token Max Inactive Time property must be set tooa lower value than hello Single-Factor Token Max Age and hello Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="abc80-286">단일 단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-286">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="abc80-287">**문자열:** MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-287">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="abc80-288">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-288">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="abc80-289">**요약:** 이 정책 제어 방법 장기 사용자를 새 새로 고침 토큰 tooget 사용 액세스/새로 고침 토큰 쌍은 마지막 성공적으로 인증 되는 단일 요소에만 사용 하 여 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-289">**Summary:** This policy controls how long a user can use a refresh token tooget a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="abc80-290">사용자를 인증 하 고 새로운 새로 고침 토큰도 수신, 후 hello 사용자 지정 하는 hello에 대 한 hello 새로 고침 토큰 흐름을 사용할 수는 시간 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-290">After a user authenticates and receives a new refresh token, hello user can use hello refresh token flow for hello specified period of time.</span></span> <span data-ttu-id="abc80-291">(그렇습니다으로 hello 현재 새로 고침 토큰이 해지 되지 않으며 hello 비활성 시간 보다 오래 사용 하지 않는 상태로 있습니다.) 해당 시점에 hello 사용자는 강제 tooreauthenticate tooreceive 새로운 새로 고침 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-291">(This is true as long as hello current refresh token is not revoked, and it is not left unused for longer than hello inactive time.) At that point, hello user is forced tooreauthenticate tooreceive a new refresh token.</span></span>

<span data-ttu-id="abc80-292">Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-292">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="abc80-293">단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값을 설정 하는 것이 좋습니다 같은 tooor 즉 hello Multi-factor 새로 고침 토큰 최대 처리 기간 속성 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-293">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor lesser than hello Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="abc80-294">다단계 새로 고침 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-294">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="abc80-295">**문자열:** MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-295">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="abc80-296">**영향:** 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="abc80-296">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="abc80-297">**요약:** 이 정책 제어 방법 장기 사용자를 새 새로 고침 토큰 tooget 사용 액세스/새로 고침 토큰 쌍은 마지막 인증 된 후 성공적으로 여러 요소를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-297">**Summary:** This policy controls how long a user can use a refresh token tooget a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="abc80-298">사용자를 인증 하 고 새로운 새로 고침 토큰도 수신, 후 hello 사용자 지정 하는 hello에 대 한 hello 새로 고침 토큰 흐름을 사용할 수는 시간 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-298">After a user authenticates and receives a new refresh token, hello user can use hello refresh token flow for hello specified period of time.</span></span> <span data-ttu-id="abc80-299">(그렇습니다 hello 현재 새로 고침 토큰 해지 되지 않은 고 hello 비활성 시간 보다 오래 사용 되지 않습니다.) 이 시점에서 사용자가 tooreauthenticate tooreceive 새 새로 고침 토큰을 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-299">(This is true as long as hello current refresh token is not revoked, and it is not unused for longer than hello inactive time.) At that point, users are forced tooreauthenticate tooreceive a new refresh token.</span></span>

<span data-ttu-id="abc80-300">Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-300">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="abc80-301">단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 tooor hello 단일 요소 새로 고침 토큰 최대 처리 기간 속성 보다 큼을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-301">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor greater than hello Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="abc80-302">단일 단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-302">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="abc80-303">**문자열:** MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-303">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="abc80-304">**영향:** 세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="abc80-304">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="abc80-305">**요약:** 이 정책 기간을 제어 사용자가 새 ID와 세션 토큰은 마지막 성공적으로 인증 되는 단일 요소에만 사용 하 여 후 세션 토큰 tooget를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-305">**Summary:** This policy controls how long a user can use a session token tooget a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="abc80-306">인증 하 고 새 세션 토큰을 수신 하는 사용자, 후 hello 사용자 지정 하는 hello에 대 한 세션 토큰 흐름 hello를 사용할 수는 시간 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-306">After a user authenticates and receives a new session token, hello user can use hello session token flow for hello specified period of time.</span></span> <span data-ttu-id="abc80-307">(그렇습니다 hello 현재 세션 토큰 해지 되지 않은 하 고 만료 되지 않았습니다.) Hello 기간 동안 지정 후 hello 사용자는 강제 tooreauthenticate tooreceive 새 세션 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-307">(This is true as long as hello current session token is not revoked and has not expired.) After hello specified period of time, hello user is forced tooreauthenticate tooreceive a new session token.</span></span>

<span data-ttu-id="abc80-308">Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-308">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="abc80-309">단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 hello 보다 작은 tooor Multi-factor 세션 토큰 최대 처리 기간 속성을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-309">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor less than hello Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="abc80-310">다단계 세션 토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-310">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="abc80-311">**문자열:** MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="abc80-311">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="abc80-312">**영향:** 세션 토큰(영구 및 비영구)</span><span class="sxs-lookup"><span data-stu-id="abc80-312">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="abc80-313">**요약:** 이 정책 기간을 제어 사용자가 새 ID와 세션 후 토큰 세션 토큰 tooget צ ְ ײ hello 마지막으로 여러 요소를 사용 하 여 성공적으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-313">**Summary:** This policy controls how long a user can use a session token tooget a new ID and session token after hello last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="abc80-314">인증 하 고 새 세션 토큰을 수신 하는 사용자, 후 hello 사용자 지정 하는 hello에 대 한 세션 토큰 흐름 hello를 사용할 수는 시간 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-314">After a user authenticates and receives a new session token, hello user can use hello session token flow for hello specified period of time.</span></span> <span data-ttu-id="abc80-315">(그렇습니다 hello 현재 세션 토큰 해지 되지 않은 하 고 만료 되지 않았습니다.) Hello 기간 동안 지정 후 hello 사용자는 강제 tooreauthenticate tooreceive 새 세션 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-315">(This is true as long as hello current session token is not revoked and has not expired.) After hello specified period of time, hello user is forced tooreauthenticate tooreceive a new session token.</span></span>

<span data-ttu-id="abc80-316">Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-316">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="abc80-317">단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 tooor hello 단일 요소 세션 토큰 최대 처리 기간 속성 보다 큼을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-317">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor greater than hello Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="abc80-318">토큰 수명 정책 예제</span><span class="sxs-lookup"><span data-stu-id="abc80-318">Example token lifetime policies</span></span>
<span data-ttu-id="abc80-319">앱, 서비스 주체 및 전체 조직의 토큰 수명을 만들고 관리할 수 있다면 Azure AD에서 다양한 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-319">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="abc80-320">이 섹션에서는 새 규칙을 적용하는 데 도움이 되는 몇 가지 일반적인 정책 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-320">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="abc80-321">토큰 수명</span><span class="sxs-lookup"><span data-stu-id="abc80-321">Token Lifetime</span></span>
* <span data-ttu-id="abc80-322">토큰 최대 비활성 시간</span><span class="sxs-lookup"><span data-stu-id="abc80-322">Token Max Inactive Time</span></span>
* <span data-ttu-id="abc80-323">토큰 최대 기간</span><span class="sxs-lookup"><span data-stu-id="abc80-323">Token Max Age</span></span>

<span data-ttu-id="abc80-324">Hello 예제에서 배울 방법:</span><span class="sxs-lookup"><span data-stu-id="abc80-324">In hello examples, you can learn how to:</span></span>

* <span data-ttu-id="abc80-325">조직의 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="abc80-325">Manage an organization's default policy</span></span>
* <span data-ttu-id="abc80-326">웹 로그인에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="abc80-326">Create a policy for web sign-in</span></span>
* <span data-ttu-id="abc80-327">web API를 호출하는 네이티브 앱에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="abc80-327">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="abc80-328">고급 정책 관리</span><span class="sxs-lookup"><span data-stu-id="abc80-328">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="abc80-329">필수 조건</span><span class="sxs-lookup"><span data-stu-id="abc80-329">Prerequisites</span></span>
<span data-ttu-id="abc80-330">다음 예제는 hello, 업데이트, 링크를 만들고 응용 프로그램, 서비스 사용자 및 조직 전체에 대 한 정책을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-330">In hello following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="abc80-331">새 tooAzure AD 인 경우에 대 한 자세히 배울 것이 좋습니다 [tooget는 Azure AD 테 넌 트](active-directory-howto-tenant.md) 이러한 예제를 진행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="abc80-331">If you are new tooAzure AD, we recommend that you learn about [how tooget an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="abc80-332">시작 tooget 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-332">tooget started, do hello following steps:</span></span>

1. <span data-ttu-id="abc80-333">Hello를 최신 버전 다운로드 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스에서](https://www.powershellgallery.com/packages/AzureADPreview)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-333">Download hello latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="abc80-334">Hello 실행 `Connect` tooyour Azure AD 관리자 계정에에서 toosign 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-334">Run hello `Connect` command toosign in tooyour Azure AD admin account.</span></span> <span data-ttu-id="abc80-335">새 세션을 시작할 때마다 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-335">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="abc80-336">toosee 다음 실행된 hello 조직에서 생성 된 모든 정책을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-336">toosee all policies that have been created in your organization, run hello following command.</span></span> <span data-ttu-id="abc80-337">Hello 다음 시나리오에서에서 대부분의 작업 후이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-337">Run this command after most operations in hello following scenarios.</span></span> <span data-ttu-id="abc80-338">Hello 가져오기는 데 도움이 됩니다. 또한 hello 명령을 실행 * * * * 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-338">Running hello command also helps you get hello ** ** of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="abc80-339">예: 조직의 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="abc80-339">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="abc80-340">이 예에서는 사용자가 전체 조직에서 로그인하는 빈도를 줄이는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-340">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="abc80-341">toodo이 토큰에 대 한 단일 요소 새로 고침을 조직 전체에 적용 되는 토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-341">toodo this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="abc80-342">hello 정책은 조직 및 설정 정책 지문이 아직 없으면 tooeach 서비스 사용자에 적용 된 tooevery 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-342">hello policy is applied tooevery application in your organization, and tooeach service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="abc80-343">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-343">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="abc80-344">너무 "까지-해지." hello 단일 요소 새로 고침 토큰 설정</span><span class="sxs-lookup"><span data-stu-id="abc80-344">Set hello Single-Factor Refresh Token too"until-revoked."</span></span> <span data-ttu-id="abc80-345">액세스가 취소 될 때까지 hello 토큰 만료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-345">hello token doesn't expire until access is revoked.</span></span> <span data-ttu-id="abc80-346">정책 정의 다음 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-346">Create hello following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="abc80-347">다음 명령을 hello 실행 toocreate hello 정책:</span><span class="sxs-lookup"><span data-stu-id="abc80-347">toocreate hello policy, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="abc80-348">toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="abc80-348">toosee your new policy, and tooget hello policy's **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="abc80-349">Hello 정책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-349">Update hello policy.</span></span>

    <span data-ttu-id="abc80-350">이 예제에 설정 된 hello 첫 번째 정책을 서비스에 필요한 만큼 엄격 인지를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-350">You might decide that hello first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="abc80-351">tooset 프로그램 단일 요소 새로 고침 토큰 tooexpire 2 일 동안에서 실행 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="abc80-351">tooset your Single-Factor Refresh Token tooexpire in two days, run hello following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="abc80-352">예: 웹 로그인에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="abc80-352">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="abc80-353">이 예제에서는 웹 앱에 더 자주 tooauthenticate 사용자가 요구 하는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-353">In this example, you create a policy that requires users tooauthenticate more frequently in your web app.</span></span> <span data-ttu-id="abc80-354">이 정책은 hello 수명 hello 액세스/ID 토큰 및 웹 응용 프로그램의 다단계 세션 토큰 toohello 서비스 사용자의 hello 최대 보존 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-354">This policy sets hello lifetime of hello access/ID tokens and hello max age of a multi-factor session token toohello service principal of your web app.</span></span>

1. <span data-ttu-id="abc80-355">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-355">Create a token lifetime policy.</span></span>

    <span data-ttu-id="abc80-356">웹 로그인에 대 한이 정책을 hello 액세스/ID 토큰 수명 및 hello 최대 단일 요소 세션 토큰 age tootwo 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-356">This policy, for web sign-in, sets hello access/ID token lifetime and hello max single-factor session token age tootwo hours.</span></span>

    1.  <span data-ttu-id="abc80-357">이 명령을 실행 toocreate hello 정책:</span><span class="sxs-lookup"><span data-stu-id="abc80-357">toocreate hello policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="abc80-358">toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="abc80-358">toosee your new policy, and tooget hello policy **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="abc80-359">Hello 정책 tooyour 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-359">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="abc80-360">또한 tooget hello 해야 **ObjectId** 서비스 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-360">You also need tooget hello **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="abc80-361">toosee 조직의 모든 서비스 사용자를 쿼리할 수 있습니다 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-361">toosee all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="abc80-362">또는 [Azure AD 그래프 탐색기](https://graphexplorer.cloudapp.net/), tooyour Azure AD 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-362">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in tooyour Azure AD account.</span></span>

    2.  <span data-ttu-id="abc80-363">Hello를 보유 하는 경우 **ObjectId** 의 서비스 사용자를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-363">When you have hello **ObjectId** of your service principal, run hello following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="abc80-364">예: web API를 호출하는 네이티브 앱에 대한 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="abc80-364">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="abc80-365">이 예제에서는 사용자가 tooauthenticate 덜 자주 요구 하는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-365">In this example, you create a policy that requires users tooauthenticate less frequently.</span></span> <span data-ttu-id="abc80-366">hello 정책에는 또한 hello 사용자 수 전에 비활성 상태로 유지 hello 사용자 다시 인증 해야 하는 시간의 양을 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-366">hello policy also lengthens hello amount of time a user can be inactive before hello user must reauthenticate.</span></span> <span data-ttu-id="abc80-367">hello 정책에 적용 된 toohello 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-367">hello policy is applied toohello web API.</span></span> <span data-ttu-id="abc80-368">Hello 네이티브 응용 프로그램 리소스로 hello 웹 API를 요청 하면이 정책이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-368">When hello native app requests hello web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="abc80-369">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-369">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="abc80-370">웹 API hello 다음 명령을 실행에 대 한 엄격한 정책 toocreate:</span><span class="sxs-lookup"><span data-stu-id="abc80-370">toocreate a strict policy for a web API, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="abc80-371">toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="abc80-371">toosee your new policy, and tooget hello policy **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="abc80-372">Hello 정책 tooyour 웹 API를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-372">Assign hello policy tooyour web API.</span></span> <span data-ttu-id="abc80-373">또한 tooget hello 해야 **ObjectId** 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-373">You also need tooget hello **ObjectId** of your application.</span></span> <span data-ttu-id="abc80-374">앱의 가장 좋은 방법은 toofind hello **ObjectId** 는 toouse hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-374">hello best way toofind your app's **ObjectId** is toouse hello [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="abc80-375">Hello를 보유 하는 경우 **ObjectId** hello 다음 명령을 실행 하면 앱의:</span><span class="sxs-lookup"><span data-stu-id="abc80-375">When you have hello **ObjectId** of your app, run hello following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="abc80-376">예: 고급 정책 관리</span><span class="sxs-lookup"><span data-stu-id="abc80-376">Example: Manage an advanced policy</span></span>
<span data-ttu-id="abc80-377">이 예제에서는 몇 가지 정책, toolearn hello 우선 순위 시스템 작동 하는 방법을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-377">In this example, you create a few policies, toolearn how hello priority system works.</span></span> <span data-ttu-id="abc80-378">또한 학습할 수 있는 방법을 toomanage는 적용 된 tooseveral 개체는 여러 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-378">You also can learn how toomanage multiple policies that are applied tooseveral objects.</span></span>

1. <span data-ttu-id="abc80-379">토큰 수명 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-379">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="abc80-380">toocreate 설정 하는 단일 요소 새로 고침 토큰 수명 too30 hello 일 전 부터는 hello 다음 명령을 실행 하는 조직 기본 정책:</span><span class="sxs-lookup"><span data-stu-id="abc80-380">toocreate an organization default policy that sets hello Single-Factor Refresh Token lifetime too30 days, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="abc80-381">toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="abc80-381">toosee your new policy, and tooget hello policy's **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="abc80-382">Hello 정책 tooa 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-382">Assign hello policy tooa service principal.</span></span>

    <span data-ttu-id="abc80-383">이제 toohello 전체 조직에 적용 되는 정책을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-383">Now, you have a policy that applies toohello entire organization.</span></span> <span data-ttu-id="abc80-384">Toopreserve이 30 일 정책을 특정 서비스 주체에 대 한 원하는 수 있지만 hello 조직 기본 정책 toohello 상한값 "까지-해지."의 변경</span><span class="sxs-lookup"><span data-stu-id="abc80-384">You might want toopreserve this 30-day policy for a specific service principal, but change hello organization default policy toohello upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="abc80-385">toosee 조직의 모든 서비스 사용자를 쿼리할 수 있습니다 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-385">toosee all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="abc80-386">또는 [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/)에서 Azure AD 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-386">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="abc80-387">Hello를 보유 하는 경우 **ObjectId** 의 서비스 사용자를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-387">When you have hello **ObjectId** of your service principal, run hello following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. <span data-ttu-id="abc80-388">집합 hello `IsOrganizationDefault` toofalse 플래그:</span><span class="sxs-lookup"><span data-stu-id="abc80-388">Set hello `IsOrganizationDefault` flag toofalse:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="abc80-389">새로운 조직 기본 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-389">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="abc80-390">Hello 원래 정책 tooyour 연결 된 서비스 사용자, 있으며 hello 새 정책이 조직의 기본 정책으로 설정 된 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-390">You now have hello original policy linked tooyour service principal, and hello new policy is set as your organization default policy.</span></span> <span data-ttu-id="abc80-391">것이 중요 한 tooremember 정책이 적용 tooservice 주체 조직 기본 정책 보다 우선 순위가 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-391">It's important tooremember that policies applied tooservice principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="abc80-392">Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="abc80-392">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="abc80-393">정책 관리</span><span class="sxs-lookup"><span data-stu-id="abc80-393">Manage policies</span></span>

<span data-ttu-id="abc80-394">다음 cmdlet toomanage 정책 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-394">You can use hello following cmdlets toomanage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="abc80-395">New-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-395">New-AzureADPolicy</span></span>

<span data-ttu-id="abc80-396">새 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-396">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="abc80-397">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-397">Parameters</span></span> | <span data-ttu-id="abc80-398">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-398">Description</span></span> | <span data-ttu-id="abc80-399">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-399">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="abc80-400">모든 hello 정책 규칙이 포함 된 화 JSON의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-400">Array of stringified JSON that contains all hello policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="abc80-401">문자열 hello 정책 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-401">String of hello policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="abc80-402">True 이면 hello 정책을 hello 조직의 기본 정책으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-402">If true, sets hello policy as hello organization's default policy.</span></span> <span data-ttu-id="abc80-403">false이면 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-403">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="abc80-404">정책의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-404">Type of policy.</span></span> <span data-ttu-id="abc80-405">토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-405">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="abc80-406"><code>&#8209;AlternativeIdentifier</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-406"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="abc80-407">Hello 정책에 대 한 대체 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-407">Sets an alternative ID for hello policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="abc80-408">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-408">Get-AzureADPolicy</span></span>
<span data-ttu-id="abc80-409">모든 Azure AD 정책 또는 지정된 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-409">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="abc80-410">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-410">Parameters</span></span> | <span data-ttu-id="abc80-411">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-411">Description</span></span> | <span data-ttu-id="abc80-412">예</span><span class="sxs-lookup"><span data-stu-id="abc80-412">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abc80-413"><code>&#8209;Id</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-413"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="abc80-414">**ObjectId (Id)** 원하는 hello 정책.</span><span class="sxs-lookup"><span data-stu-id="abc80-414">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="abc80-415">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="abc80-415">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="abc80-416">모든 앱과 연결 된 tooa 정책 인 서비스 사용자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-416">Gets all apps and service principals that are linked tooa policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="abc80-417">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-417">Parameters</span></span> | <span data-ttu-id="abc80-418">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-418">Description</span></span> | <span data-ttu-id="abc80-419">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-419">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-420">**ObjectId (Id)** 원하는 hello 정책.</span><span class="sxs-lookup"><span data-stu-id="abc80-420">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="abc80-421">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-421">Set-AzureADPolicy</span></span>
<span data-ttu-id="abc80-422">기존 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-422">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="abc80-423">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-423">Parameters</span></span> | <span data-ttu-id="abc80-424">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-424">Description</span></span> | <span data-ttu-id="abc80-425">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-425">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-426">**ObjectId (Id)** 원하는 hello 정책.</span><span class="sxs-lookup"><span data-stu-id="abc80-426">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="abc80-427">문자열 hello 정책 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-427">String of hello policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="abc80-428"><code>&#8209;Definition</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-428"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="abc80-429">모든 hello 정책 규칙이 포함 된 화 JSON의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-429">Array of stringified JSON that contains all hello policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="abc80-430"><code>&#8209;IsOrganizationDefault</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-430"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="abc80-431">True 이면 hello 정책을 hello 조직의 기본 정책으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-431">If true, sets hello policy as hello organization's default policy.</span></span> <span data-ttu-id="abc80-432">false이면 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-432">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="abc80-433"><code>&#8209;Type</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-433"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="abc80-434">정책의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-434">Type of policy.</span></span> <span data-ttu-id="abc80-435">토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-435">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="abc80-436"><code>&#8209;AlternativeIdentifier</code>[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="abc80-436"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="abc80-437">Hello 정책에 대 한 대체 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-437">Sets an alternative ID for hello policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="abc80-438">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-438">Remove-AzureADPolicy</span></span>
<span data-ttu-id="abc80-439">삭제 hello 정책을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-439">Deletes hello specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="abc80-440">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-440">Parameters</span></span> | <span data-ttu-id="abc80-441">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-441">Description</span></span> | <span data-ttu-id="abc80-442">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-442">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-443">**ObjectId (Id)** 원하는 hello 정책.</span><span class="sxs-lookup"><span data-stu-id="abc80-443">**ObjectId (Id)** of hello policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="abc80-444">응용 프로그램 정책</span><span class="sxs-lookup"><span data-stu-id="abc80-444">Application policies</span></span>
<span data-ttu-id="abc80-445">Hello 다음 응용 프로그램 정책에 대 한 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-445">You can use hello following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="abc80-446">Add-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-446">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="abc80-447">링크 hello 정책 tooan 응용 프로그램을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-447">Links hello specified policy tooan application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="abc80-448">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-448">Parameters</span></span> | <span data-ttu-id="abc80-449">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-449">Description</span></span> | <span data-ttu-id="abc80-450">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-450">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-451">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-451">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="abc80-452">**ObjectId** hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-452">**ObjectId** of hello policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="abc80-453">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-453">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="abc80-454">Tooan 응용 프로그램에 할당 된 hello 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-454">Gets hello policy that is assigned tooan application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="abc80-455">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-455">Parameters</span></span> | <span data-ttu-id="abc80-456">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-456">Description</span></span> | <span data-ttu-id="abc80-457">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-457">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-458">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-458">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="abc80-459">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-459">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="abc80-460">응용 프로그램에서 정책을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-460">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="abc80-461">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-461">Parameters</span></span> | <span data-ttu-id="abc80-462">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-462">Description</span></span> | <span data-ttu-id="abc80-463">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-463">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-464">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-464">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="abc80-465">**ObjectId** hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-465">**ObjectId** of hello policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="abc80-466">서비스 사용자 정책</span><span class="sxs-lookup"><span data-stu-id="abc80-466">Service principal policies</span></span>
<span data-ttu-id="abc80-467">서비스 주체 정책에 대 한 cmdlet을 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-467">You can use hello following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="abc80-468">Add-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-468">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="abc80-469">링크 hello 지정한 정책 tooa 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-469">Links hello specified policy tooa service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="abc80-470">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-470">Parameters</span></span> | <span data-ttu-id="abc80-471">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-471">Description</span></span> | <span data-ttu-id="abc80-472">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-472">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-473">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-473">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="abc80-474">**ObjectId** hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-474">**ObjectId** of hello policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="abc80-475">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-475">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="abc80-476">모든 정책 연결 된 toohello 지정된 서비스 보안 주체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-476">Gets any policy linked toohello specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="abc80-477">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-477">Parameters</span></span> | <span data-ttu-id="abc80-478">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-478">Description</span></span> | <span data-ttu-id="abc80-479">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-479">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-480">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-480">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="abc80-481">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="abc80-481">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="abc80-482">Hello 정책을 hello 지정된 서비스 보안 주체에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-482">Removes hello policy from hello specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="abc80-483">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abc80-483">Parameters</span></span> | <span data-ttu-id="abc80-484">설명</span><span class="sxs-lookup"><span data-stu-id="abc80-484">Description</span></span> | <span data-ttu-id="abc80-485">예제</span><span class="sxs-lookup"><span data-stu-id="abc80-485">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="abc80-486">**ObjectId (Id)** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-486">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="abc80-487">**ObjectId** hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="abc80-487">**ObjectId** of hello policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
