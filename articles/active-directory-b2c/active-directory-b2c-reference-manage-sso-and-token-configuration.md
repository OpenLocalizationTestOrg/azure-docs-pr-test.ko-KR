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
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="1e577-102">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SSO 및 토큰 사용자 지정 관리</span><span class="sxs-lookup"><span data-stu-id="1e577-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="1e577-103">사용자 지정 정책을 사용 하 여 기본 제공 정책을 통해 같은 제어할 토큰, 세션 및 (SSO) 구성 로그온 단일 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="1e577-104">각 설정, toolearn hello 설명서를 참조 하십시오 [여기](#active-directory-b2c-token-session-sso)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="1e577-105">토큰 수명 및 클레임 구성</span><span class="sxs-lookup"><span data-stu-id="1e577-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="1e577-106">사용자 토큰 수명에 toochange hello 설정 해야 tooadd는 `<ClaimsProviders>` 요소 tooimpact hello 정책 hello 신뢰 당사자 파일에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="1e577-107">hello `<ClaimsProviders>` hello의 자식 이며 `<TrustFrameworkPolicy>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="1e577-108">내부 사용자 토큰 수명에 영향을 주는 tooput hello 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="1e577-109">hello XML은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="1e577-110">**액세스 토큰 수명** hello 액세스 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "token_lifetime_secs" 시간 (초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1e577-111">기본 제공 hello 기본값은 3600 초 (60 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1e577-112">**ID 토큰 수명** hello ID 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "id_token_lifetime_secs" 시간 (초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1e577-113">기본 제공 hello 기본값은 3600 초 (60 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1e577-114">**토큰 수명 새로 고침** hello 새로 고침 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "refresh_token_lifetime_secs" 시간 (초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1e577-115">기본 제공 hello 기본값은 1209600 초 (14 일)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="1e577-116">**슬라이딩 창 수명 토큰 새로 고침** tooset 슬라이딩 창 수명 tooyour 새로 고침 토큰을 원하는 경우 내부 hello 값 수정 `<Item>` hello 키로 = "rolling_refresh_token_lifetime_secs" 시간 (초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1e577-117">hello에 기본 제공 기본값이 7776000 (90 일)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="1e577-118">Tooenfore 않으려면는와이 줄을 바꿉니다 슬라이딩 창 수명:</span><span class="sxs-lookup"><span data-stu-id="1e577-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="1e577-119">**(Iss) 발급자 클레임** toochange hello (iss) 발급자 클레임 hello 내 hello 값을 수정, `<Item>` hello 키로 = "IssuanceClaimPattern"입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="1e577-120">hello 적용 가능한 값은 `AuthorityAndTenantGuid` 및 `AuthorityWithTfp`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="1e577-121">**설정 정책 ID를 나타내는 클레임** 이 값을 설정 하기 위한 hello 옵션은 TFP (신뢰 프레임 워크 정책) 및 ACR (인증 컨텍스트 참조).</span><span class="sxs-lookup"><span data-stu-id="1e577-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="1e577-122">에서는이이 tooTFP toodo를 설정 하는 것, hello 확인 `<Item>` hello 키로 = "AuthenticationContextReferenceClaimPattern" 있으며 hello 값이 `None`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="1e577-123">`<OutputClaims>` 항목에서 이 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="1e577-124">ACR를 hello 제거 `<Item>` hello 키로 = "AuthenticationContextReferenceClaimPattern"입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="1e577-125">**제목 (sub) 클레임** 이 옵션은 기본적으로, tooObjectID tooswitch 원하는 경우이 너무`Not Supported`, 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="1e577-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="1e577-126">다음 줄을</span><span class="sxs-lookup"><span data-stu-id="1e577-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="1e577-127">다음 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="1e577-128">세션 동작 및 SSO</span><span class="sxs-lookup"><span data-stu-id="1e577-128">Session behavior and SSO</span></span>
<span data-ttu-id="1e577-129">toochange 세션 동작 및 SSO 구성 tooadd 해야는 `<UserJourneyBehaviors>` 요소 hello 내의 요소 `<RelyingParty>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="1e577-130">hello `<UserJourneyBehaviors>` 요소 바로 뒤에 붙여야 hello `<DefaultUserJourney>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="1e577-131">내부에 hello 프로그램 `<UserJourneyBehavors>` 요소는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="1e577-132">**Single sign-on (SSO) 구성** 의 toomodify hello 값이 필요한 toochange hello single sign on 구성, `<SingleSignOn>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="1e577-133">hello 적용 가능한 값은 `Tenant`, `Application`, `Policy` 및 `Disabled`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="1e577-134">**웹 응용 프로그램 세션 수명 (분)** toochange hello hello 웹 응용 프로그램의 hello toomodify 값이 필요한 세션 수명 `<SessionExpiryInSeconds>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="1e577-135">기본 제공 정책에서 hello 기본값은 86, 400 초 (1440 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="1e577-136">**웹 앱에 대 한 세션 제한 시간** 의 toomodify hello 값이 필요한 toochange hello 웹 응용 프로그램 세션 제한 시간 `<SessionExpiryType>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="1e577-137">hello 적용 가능한 값은 `Absolute` 및 `Rolling`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e577-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
