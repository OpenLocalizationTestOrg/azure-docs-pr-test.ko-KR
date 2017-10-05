---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SSO 및 토큰 사용자 지정 관리 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="d6f14-102">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SSO 및 토큰 사용자 지정 관리</span><span class="sxs-lookup"><span data-stu-id="d6f14-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="d6f14-103">사용자 지정 정책을 사용하면 토큰, 세션 및 SSO(Single Sign-On) 구성에 대해 기본 정책을 통할 때와 동일한 제어가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="d6f14-104">각 설정에 대해 알아보려면 [여기](#active-directory-b2c-token-session-sso) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f14-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="d6f14-105">토큰 수명 및 클레임 구성</span><span class="sxs-lookup"><span data-stu-id="d6f14-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="d6f14-106">토큰 수명에 대한 설정을 변경하려면 영향을 줄 정책의 신뢰 당사자 파일에 `<ClaimsProviders>` 요소를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="d6f14-107">`<ClaimsProviders>` 요소는 `<TrustFrameworkPolicy>`의 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="d6f14-108">이 안에 토큰 수명에 영향을 주는 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="d6f14-109">XML은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-109">The XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="d6f14-110">**액세스 토큰 수명** `<Item>` 안의 값을 Key="token_lifetime_secs"(초)로 수정하여 액세스 토큰 수명을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="d6f14-111">기본 제공되는 기본값은 3600초(60분)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="d6f14-112">**ID 토큰 수명** `<Item>` 안의 값을 Key="id_token_lifetime_secs"(초)로 수정하여 ID 토큰 수명을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="d6f14-113">기본 제공되는 기본값은 3600초(60분)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="d6f14-114">**새로 고침 토큰 수명** `<Item>` 안의 값을 Key="refresh_token_lifetime_secs"(초)로 수정하여 새로 고침 토큰 수명을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="d6f14-115">기본 제공되는 기본값은 1209600초(14일)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="d6f14-116">**새로 고침 토큰 슬라이딩 윈도우 수명** 새로 고침 토큰에 대한 슬라이딩 윈도우 수명을 설정하려면 `<Item>` 안의 값을 Key="rolling_refresh_token_lifetime_secs"(초)로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="d6f14-117">기본 제공되는 기본값은 7776000초(90일)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="d6f14-118">슬라이딩 윈도우 수명을 적용하지 않으려면 이 줄을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="d6f14-119">**발급자(iss) 클레임** 발급자(iss) 클레임을 변경하려면 `<Item>` 안의 값을 Key="IssuanceClaimPattern"으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="d6f14-120">적용 가능한 값은 `AuthorityAndTenantGuid` 및 `AuthorityWithTfp`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="d6f14-121">**정책 ID를 나타내는 클레임 설정** 이 값을 설정하기 위한 옵션은 TFP(보안 프레임워크 정책) 및 ACR(인증 컨텍스트 참조)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="d6f14-122">TFP로 설정하는 것이 좋으며 이렇게 하려면 Key="AuthenticationContextReferenceClaimPattern"인 `<Item>`이 존재하고 값이 `None`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="d6f14-123">`<OutputClaims>` 항목에서 이 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="d6f14-124">ACR의 경우 Key="AuthenticationContextReferenceClaimPattern"인 `<Item>`을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="d6f14-125">**주체(sub) 클레임** 이 옵션은 기본적으로 ObjectID입니다. 이 값을 `Not Supported`로 전환하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="d6f14-126">다음 줄을</span><span class="sxs-lookup"><span data-stu-id="d6f14-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="d6f14-127">다음 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="d6f14-128">세션 동작 및 SSO</span><span class="sxs-lookup"><span data-stu-id="d6f14-128">Session behavior and SSO</span></span>
<span data-ttu-id="d6f14-129">세션 동작 및 SSO 구성을 변경하려면 `<RelyingParty>` 요소 내에 `<UserJourneyBehaviors>` 요소를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="d6f14-130">`<UserJourneyBehaviors>` 요소 바로 뒤에는 `<DefaultUserJourney>`가 나와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="d6f14-131">`<UserJourneyBehavors>` 요소 내부는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="d6f14-132">**SSO(Single Sign-On) 구성** SSO(Single Sign-On) 구성을 변경하려면 `<SingleSignOn>` 값을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="d6f14-133">적용 가능한 값은 `Tenant`, `Application`, `Policy` 및 `Disabled`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="d6f14-134">**웹앱 세션 수명(분)** 웹앱 세션 수명을 변경하려면 `<SessionExpiryInSeconds>` 요소의 값을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="d6f14-135">기본 제공 정책의 기본값은 86400초(1440분)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="d6f14-136">**웹앱 세션 시간 제한** 웹앱 세션 시간 제한을 변경하려면 `<SessionExpiryType>` 값을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="d6f14-137">적용 가능한 값은 `Absolute` 및 `Rolling`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f14-137">The applicable values are `Absolute` and `Rolling`.</span></span>
