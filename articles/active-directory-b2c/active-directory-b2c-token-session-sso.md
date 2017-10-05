---
title: "Azure Active Directory B2C: 토큰, 세션 및 Single Sign-On 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에서 토큰, 세션 및 Single Sign-On 구성"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 4442174a857681adff33001e660809ec7d47ad7d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a><span data-ttu-id="326de-103">Azure Active Directory B2C: 토큰, 세션 및 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="326de-103">Azure Active Directory B2C: Token, session and single sign-on configuration</span></span>
<span data-ttu-id="326de-104">이 기능은 다음의 [정책별](active-directory-b2c-reference-policies.md)세분화된 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-104">This feature gives you fine-grained control, on a [per-policy basis](active-directory-b2c-reference-policies.md), of:</span></span>

1. <span data-ttu-id="326de-105">Azure AD(Azure Active Directory) B2C에서 내보낸 보안 토큰의 수명.</span><span class="sxs-lookup"><span data-stu-id="326de-105">Lifetimes of security tokens emitted by Azure Active Directory (Azure AD) B2C.</span></span>
2. <span data-ttu-id="326de-106">Azure AD B2C에서 관리하는 웹 응용 프로그램 세션의 수명.</span><span class="sxs-lookup"><span data-stu-id="326de-106">Lifetimes of web application sessions managed by Azure AD B2C.</span></span>
3. <span data-ttu-id="326de-107">Azure AD B2C에서 내보낸 보안 토큰의 중요한 클레임 형식</span><span class="sxs-lookup"><span data-stu-id="326de-107">Formats of important claims in the security tokens emitted by Azure AD B2C.</span></span>
4. <span data-ttu-id="326de-108">B2C 테넌트에 있는 여러 앱 및 정책의 SSO(Single Sign-On) 동작.</span><span class="sxs-lookup"><span data-stu-id="326de-108">Single sign-on (SSO) behavior across multiple apps and policies in your B2C tenant.</span></span>

<span data-ttu-id="326de-109">다음과 같이 B2C 테넌트에서 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-109">You can use this feature in your B2C tenant as follows:</span></span>

1. <span data-ttu-id="326de-110">다음 단계에 따라 [Azure Portal의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) .</span><span class="sxs-lookup"><span data-stu-id="326de-110">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="326de-111">**로그인 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-111">Click **Sign-in policies**.</span></span> <span data-ttu-id="326de-112">*참고: **로그인 정책**뿐만 아니라 모든 정책 유형에서 이 기능을 사용할 수 있습니다*.</span><span class="sxs-lookup"><span data-stu-id="326de-112">*Note: You can use this feature on any policy type, not just on **Sign-in policies***.</span></span>
3. <span data-ttu-id="326de-113">클릭하여 정책을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="326de-113">Open a policy by clicking it.</span></span> <span data-ttu-id="326de-114">예를 들어 **B2C_1_SiIn**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-114">For example, click on **B2C_1_SiIn**.</span></span>
4. <span data-ttu-id="326de-115">블레이드 위쪽에서 **편집** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-115">Click **Edit** at the top of the blade.</span></span>
5. <span data-ttu-id="326de-116">**토큰, 세션 및 Single Sign-On 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-116">Click **Token, session & single sign-on config**.</span></span>
6. <span data-ttu-id="326de-117">원하는 변경 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-117">Make your desired changes.</span></span> <span data-ttu-id="326de-118">이후 섹션에서 사용할 수 있는 속성에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="326de-118">Learn about available properties in subsequent sections.</span></span>
7. <span data-ttu-id="326de-119">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-119">Click **OK**.</span></span>
8. <span data-ttu-id="326de-120">블레이드 맨 위의 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-120">Click **Save** on the top of the blade.</span></span>

## <a name="token-lifetimes-configuration"></a><span data-ttu-id="326de-121">토큰 수명 구성</span><span class="sxs-lookup"><span data-stu-id="326de-121">Token lifetimes configuration</span></span>
<span data-ttu-id="326de-122">Azure AD B2C는 보호된 리소스에 대한 보안 액세스를 활성화하도록 [OAuth 2.0 권한 부여 프로토콜](active-directory-b2c-reference-protocols.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-122">Azure AD B2C supports the [OAuth 2.0 authorization protocol](active-directory-b2c-reference-protocols.md) for enabling secure access to protected resources.</span></span> <span data-ttu-id="326de-123">이 지원을 구현하기 위해 Azure AD B2C는 다양한 [보안 토큰](active-directory-b2c-reference-tokens.md)을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="326de-123">To implement this support, Azure AD B2C emits various [security tokens](active-directory-b2c-reference-tokens.md).</span></span> <span data-ttu-id="326de-124">다음은 Azure AD B2C에서 내보낸 보안 토큰의 수명을 관리하는 데 사용할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-124">These are the properties you can use to manage lifetimes of security tokens emitted by Azure AD B2C:</span></span>

* <span data-ttu-id="326de-125">**액세스 및 ID 토큰 수명(분)**: OAuth 2.0 전달자 토큰의 수명은 보호된 리소스에 대한 액세스를 얻는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="326de-125">**Access & ID token lifetimes (minutes)**: The lifetime of the OAuth 2.0 bearer token used to gain access to a protected resource.</span></span> <span data-ttu-id="326de-126">Azure AD B2C는 이때 ID 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-126">Azure AD B2C issues only ID tokens at this time.</span></span> <span data-ttu-id="326de-127">이 값은 해당 지원을 추가하는 경우 액세스 토큰에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="326de-127">This value would apply to access tokens as well, when we add support for them.</span></span>
  * <span data-ttu-id="326de-128">기본값: 60분.</span><span class="sxs-lookup"><span data-stu-id="326de-128">Default = 60 minutes.</span></span>
  * <span data-ttu-id="326de-129">최소(포함) = 5분.</span><span class="sxs-lookup"><span data-stu-id="326de-129">Minimum (inclusive) = 5 minutes.</span></span>
  * <span data-ttu-id="326de-130">최대(포함) = 1440분.</span><span class="sxs-lookup"><span data-stu-id="326de-130">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="326de-131">**새로 고침 토큰 수명(일)**: 새로 고침 토큰을 새 액세스 또는 ID 토큰(필요에 따라 응용 프로그램에 `offline_access` 범위가 부여된 경우 새로운 새로 고침 토큰)을 획득하는 데 사용할 수 있기 전까지의 최대 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-131">**Refresh token lifetime (days)**: The maximum time period before which a refresh token can be used to acquire a new access or ID token (and optionally, a new refresh token, if your application had been granted the `offline_access` scope).</span></span>
  * <span data-ttu-id="326de-132">기본값 = 14일.</span><span class="sxs-lookup"><span data-stu-id="326de-132">Default = 14 days.</span></span>
  * <span data-ttu-id="326de-133">최소(포함) = 1일.</span><span class="sxs-lookup"><span data-stu-id="326de-133">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="326de-134">최대(포함) = 90일.</span><span class="sxs-lookup"><span data-stu-id="326de-134">Maximum (inclusive) = 90 days.</span></span>
* <span data-ttu-id="326de-135">**새로 고침 토큰 슬라이딩 창 수명(일)**: 이 기간이 경과한 후 사용자는 응용 프로그램에서 가져온 가장 최근 새로 고침 토큰의 유효 기간과 관계 없이 강제로 다시 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-135">**Refresh token sliding window lifetime (days)**: After this time period elapses the user is forced to re-authenticate, irrespective of the validity period of the most recent refresh token acquired by the application.</span></span> <span data-ttu-id="326de-136">스위치가 **제한된**으로 설정된 경우 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-136">It can only be provided if the switch is set to **Bounded**.</span></span> <span data-ttu-id="326de-137">**새로 고침 토큰 수명(일)** 값보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-137">It needs to be greater than or equal to the **Refresh token lifetime (days)** value.</span></span> <span data-ttu-id="326de-138">스위치가 **제한 없는**으로 설정된 경우 특정 값을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-138">If the switch is set to **Unbounded**, you cannot provide a specific value.</span></span>
  * <span data-ttu-id="326de-139">기본값 = 90일.</span><span class="sxs-lookup"><span data-stu-id="326de-139">Default = 90 days.</span></span>
  * <span data-ttu-id="326de-140">최소(포함) = 1일.</span><span class="sxs-lookup"><span data-stu-id="326de-140">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="326de-141">최대(포함) = 365일.</span><span class="sxs-lookup"><span data-stu-id="326de-141">Maximum (inclusive) = 365 days.</span></span>

<span data-ttu-id="326de-142">다음은 이러한 속성을 사용하여 활성화할 수 있는 몇 가지 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-142">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="326de-143">응용 프로그램에서 지속적으로 활성 상태인 한 사용자가 모바일 응용 프로그램에 무기한으로 로그인 상태를 유지하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-143">Allow a user to stay signed into a mobile application indefinitely, as long as he or she is continually active on the application.</span></span> <span data-ttu-id="326de-144">로그인 정책에서 **새로 고침 토큰 슬라이딩 창 수명(일)** 스위치를 **제한 없는**으로 설정하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-144">You can do this by setting the **Refresh token sliding window lifetime (days)** switch to **Unbounded** in your sign-in policy.</span></span>
* <span data-ttu-id="326de-145">적절한 액세스 토큰 수명을 설정하여 업계의 보안 및 규정 준수 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-145">Meet your industry's security and compliance requirements by setting the appropriate access token lifetimes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="326de-146">이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-146">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="token-compatibility-settings"></a><span data-ttu-id="326de-147">토큰 호환성 설정</span><span class="sxs-lookup"><span data-stu-id="326de-147">Token compatibility settings</span></span>
<span data-ttu-id="326de-148">Azure AD B2C에서 내보낸 보안 토큰에서 중요한 클레임에 대한 형식을 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-148">We made formatting changes to important claims in security tokens emitted by Azure AD B2C.</span></span> <span data-ttu-id="326de-149">이는 표준 프로토콜 지원을 개선하고 타사 ID 라이브러리와의 상호 운용성을 향상시키기 위해 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-149">This was done to improve our standard protocol support and for better interoperability with third-party identity libraries.</span></span> <span data-ttu-id="326de-150">그러나 기존 앱을 손상시키지 않기 위해 고객이 필요에 따라 옵트인할 수 있도록 다음과 같은 속성을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-150">However, to avoid breaking existing apps, we created the following properties to allow customers to opt-in as needed:</span></span>

* <span data-ttu-id="326de-151">**발급자(iss) 클레임**: 토큰을 발급한 Azure AD B2C 테넌트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-151">**Issuer (iss) claim**: This identifies the Azure AD B2C tenant that issued the token.</span></span>
  * <span data-ttu-id="326de-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: This is the default value.</span></span>
  * <span data-ttu-id="326de-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: 이 값에는 B2C 테넌트 및 토큰 요청에 사용된 정책에 대한 ID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="326de-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: This value includes IDs for both the B2C tenant and the policy used in the token request.</span></span> <span data-ttu-id="326de-154">앱이나 라이브러리에 [OpenID Connect 검색 1.0 사양](http://openid.net/specs/openid-connect-discovery-1_0.html)과 호환되도록 Azure AD B2C가 필요한 경우 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-154">If your app or library needs Azure AD B2C to be compliant with the [OpenID Connect Discovery 1.0 spec](http://openid.net/specs/openid-connect-discovery-1_0.html), use this value.</span></span>
* <span data-ttu-id="326de-155">**주체(sub) 클레임**: 토큰에서 정보를 어설션하는 엔터티, 즉 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-155">**Subject (sub) claim**: This identifies the entity, i.e., the user, for which the token asserts information.</span></span>
  * <span data-ttu-id="326de-156">**ObjectID**: 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-156">**ObjectID**: This is the default value.</span></span> <span data-ttu-id="326de-157">디렉터리에 있는 사용자의 개체 ID를 토큰의 `sub` 클레임에 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="326de-157">It populates the object ID of the user in the directory into the `sub` claim in the token.</span></span>
  * <span data-ttu-id="326de-158">**지원되지 않음**: 이전 버전과의 호환성을 위해서만 제공되므로 가능한 한 빨리 **ObjectID**로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-158">**Not supported**: This is only provided for backward-compatibility, and we recommend that you switch to **ObjectID** as soon as you are able to.</span></span>
* <span data-ttu-id="326de-159">**정책 ID를 나타내는 클레임**: 토큰 요청에 사용된 정책 ID가 채워지는 클레임 유형을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-159">**Claim representing policy ID**: This identifies the claim type into which the policy ID used in the token request is populated.</span></span>
  * <span data-ttu-id="326de-160">**tfp**: 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-160">**tfp**: This is the default value.</span></span>
  * <span data-ttu-id="326de-161">**acr**: 이전 버전과의 호환성을 위해서만 제공되므로 가능한 한 빨리 `tfp`로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-161">**acr**: This is only provided for backward-compatibility, and we recommend that you switch to `tfp` as soon as you are able to.</span></span>

## <a name="session-behavior"></a><span data-ttu-id="326de-162">세션 동작</span><span class="sxs-lookup"><span data-stu-id="326de-162">Session behavior</span></span>
<span data-ttu-id="326de-163">Azure AD B2C는 웹 응용 프로그램에 대한 보안 로그인을 활성화하도록 [OpenID Connect 인증 프로토콜](active-directory-b2c-reference-oidc.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-163">Azure AD B2C supports the [OpenID Connect authentication protocol](active-directory-b2c-reference-oidc.md) for enabling secure sign-in to web applications.</span></span> <span data-ttu-id="326de-164">다음은 웹 응용 프로그램 세션을 관리하는 데 사용할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-164">These are the properties you can use to manage web application sessions:</span></span>

* <span data-ttu-id="326de-165">**웹앱 세션 수명(분)**: 인증 성공 시 사용자의 브라우저에 저장된 Azure AD B2C 세션 쿠키의 수명입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-165">**Web app session lifetime (minutes)**: The lifetime of Azure AD B2C's session cookie stored on the user's browser upon successful authentication.</span></span>
  * <span data-ttu-id="326de-166">기본값: 1440분.</span><span class="sxs-lookup"><span data-stu-id="326de-166">Default = 1440 minutes.</span></span>
  * <span data-ttu-id="326de-167">최소(포함) = 15분.</span><span class="sxs-lookup"><span data-stu-id="326de-167">Minimum (inclusive) = 15 minutes.</span></span>
  * <span data-ttu-id="326de-168">최대(포함) = 1440분.</span><span class="sxs-lookup"><span data-stu-id="326de-168">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="326de-169">**웹앱 세션 제한 시간**: 이 스위치가 **절대**로 설정된 경우 사용자는 **웹앱 세션 수명(분)**에서 지정한 기간이 경과된 후 강제로 다시 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-169">**Web app session timeout**: If this switch is set to **Absolute**, the user is forced to re-authenticate after the time period specified by **Web app session lifetime (minutes)** elapses.</span></span> <span data-ttu-id="326de-170">이 스위치가 **롤링** (기본 설정)으로 설정된 경우 사용자는 웹 응용 프로그램에서 지속적으로 활성 상태인 한 로그인 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="326de-170">If this switch is set to **Rolling** (the default setting), the user remains signed in as long as the user is continually active in your web application.</span></span>

<span data-ttu-id="326de-171">다음은 이러한 속성을 사용하여 활성화할 수 있는 몇 가지 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-171">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="326de-172">적절한 웹 응용 프로그램 세션 수명을 설정하여 업계의 보안 및 규정 준수 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-172">Meet your industry's security and compliance requirements by setting the appropriate web application session lifetimes.</span></span>
* <span data-ttu-id="326de-173">사용자가 웹 응용 프로그램의 높은 수준의 보안 일부와 상호 작용하는 동안 설정 기간 후 강제로 다시 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-173">Force re-authentication after a set time period during a user's interaction with a high-security part of your web application.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="326de-174">이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-174">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a><span data-ttu-id="326de-175">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="326de-175">Single sign-on (SSO) configuration</span></span>
<span data-ttu-id="326de-176">B2C 테넌트에 여러 응용 프로그램 및 정책이 있는 경우 **Single Sign-On 구성** 속성을 사용하여 이들 간에 사용자 상호 작용을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-176">If you have multiple applications and policies in your B2C tenant, you can manage user interactions across them using the **Single sign-on configuration** property.</span></span> <span data-ttu-id="326de-177">다음 설정 중 하나에 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-177">You can set the property to one of the following settings:</span></span>

* <span data-ttu-id="326de-178">**테넌트**: 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="326de-178">**Tenant**: This is the default setting.</span></span> <span data-ttu-id="326de-179">이 설정을 사용하여 B2C 테넌트의 여러 응용 프로그램 및 정책이 동일한 사용자 세션을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-179">Using this setting allows multiple applications and policies in your B2C tenant to share the same user session.</span></span> <span data-ttu-id="326de-180">예를 들어 사용자가 응용 프로그램, Contoso Shopping에 로그인하면 액세스의 관점에서 볼 때 다른 앱인 Contoso Pharmacy에도 원활하게 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-180">For example, once a user signs into an application, Contoso Shopping, he or she can also seamlessly sign into another one, Contoso Pharmacy, upon accessing it.</span></span>
* <span data-ttu-id="326de-181">**응용 프로그램**: 다른 응용 프로그램과 독립적으로 응용 프로그램에 대한 독점적인 사용자 세션을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-181">**Application**: This allows you to maintain a user session exclusively for an application, independent of other applications.</span></span> <span data-ttu-id="326de-182">예를 들어 동일한 B2C 테넌트에 있는 다른 응용 프로그램인 Contoso Shopping에 이미 로그인한 경우라하더라도 (동일한 자격 증명을 사용하여) 사용자가 Contoso Pharmacy에 로그인하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-182">For example, if you want the user to sign in to Contoso Pharmacy (with the same credentials), even if he or she is already signed into Contoso Shopping, another application on the same B2C tenant.</span></span> 
* <span data-ttu-id="326de-183">**정책**: 이를 사용하는 응용 프로그램과 독립적으로 정책에 대한 독점적인 사용자 세션을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-183">**Policy**: This allows you to maintain a user session exclusively for a policy, independent of the applications using it.</span></span> <span data-ttu-id="326de-184">예를 들어 사용자가 이미 로그인하고 MFA(다단계 인증) 단계를 완료한 경우 정책에 연결된 세션이 만료되지 않는 한 여러 응용 프로그램의 높은 수준의 보안 부분에 대한 액세스를 부여 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-184">For example, if the user has already signed in and completed a multi factor authentication (MFA) step, he or she can be given access to higher-security parts of multiple applications as long as the session tied to the policy doesn't expire.</span></span>
* <span data-ttu-id="326de-185">**비활성화**: 사용자가 모든 정책 실행에서 전체 사용자 과정을 통해 강제로 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="326de-185">**Disabled**: This forces the user to run through the entire user journey on every execution of the policy.</span></span> <span data-ttu-id="326de-186">예를 들어 전체 시간 동안 단일 사용자가 로그인 상태로 남아 있더라도 여러 사용자가 응용 프로그램(공유 데스크톱 시나리오에서)에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-186">For example, this will allow multiple users to sign up to your application (in a shared desktop scenario), even while a single user remains signed in during the whole time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="326de-187">이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="326de-187">These settings are not available for password reset policies.</span></span>
    > 
    > 

