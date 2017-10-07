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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SSO 및 토큰 사용자 지정 관리
사용자 지정 정책을 사용 하 여 기본 제공 정책을 통해 같은 제어할 토큰, 세션 및 (SSO) 구성 로그온 단일 hello를 제공 합니다.  각 설정, toolearn hello 설명서를 참조 하십시오 [여기](#active-directory-b2c-token-session-sso)합니다.

## <a name="token-lifetimes-and-claims-configuration"></a>토큰 수명 및 클레임 구성
사용자 토큰 수명에 toochange hello 설정 해야 tooadd는 `<ClaimsProviders>` 요소 tooimpact hello 정책 hello 신뢰 당사자 파일에서 원하는 합니다.  hello `<ClaimsProviders>` hello의 자식 이며 `<TrustFrameworkPolicy>`합니다.  내부 사용자 토큰 수명에 영향을 주는 tooput hello 정보가 필요 합니다.  hello XML은 다음과 같습니다.

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

**액세스 토큰 수명** hello 액세스 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "token_lifetime_secs" 시간 (초)에 있습니다.  기본 제공 hello 기본값은 3600 초 (60 분)입니다.

**ID 토큰 수명** hello ID 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "id_token_lifetime_secs" 시간 (초)에 있습니다.  기본 제공 hello 기본값은 3600 초 (60 분)입니다.

**토큰 수명 새로 고침** hello 새로 고침 토큰 수명 hello 내 hello 값을 수정 하 여 변경할 수 있습니다 `<Item>` hello 키로 = "refresh_token_lifetime_secs" 시간 (초)에 있습니다.  기본 제공 hello 기본값은 1209600 초 (14 일)입니다.

**슬라이딩 창 수명 토큰 새로 고침** tooset 슬라이딩 창 수명 tooyour 새로 고침 토큰을 원하는 경우 내부 hello 값 수정 `<Item>` hello 키로 = "rolling_refresh_token_lifetime_secs" 시간 (초)에 있습니다.  hello에 기본 제공 기본값이 7776000 (90 일)입니다.  Tooenfore 않으려면는와이 줄을 바꿉니다 슬라이딩 창 수명:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**(Iss) 발급자 클레임** toochange hello (iss) 발급자 클레임 hello 내 hello 값을 수정, `<Item>` hello 키로 = "IssuanceClaimPattern"입니다.  hello 적용 가능한 값은 `AuthorityAndTenantGuid` 및 `AuthorityWithTfp`합니다.

**설정 정책 ID를 나타내는 클레임** 이 값을 설정 하기 위한 hello 옵션은 TFP (신뢰 프레임 워크 정책) 및 ACR (인증 컨텍스트 참조).  
에서는이이 tooTFP toodo를 설정 하는 것, hello 확인 `<Item>` hello 키로 = "AuthenticationContextReferenceClaimPattern" 있으며 hello 값이 `None`합니다.
`<OutputClaims>` 항목에서 이 요소를 추가합니다.
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
ACR를 hello 제거 `<Item>` hello 키로 = "AuthenticationContextReferenceClaimPattern"입니다.

**제목 (sub) 클레임** 이 옵션은 기본적으로, tooObjectID tooswitch 원하는 경우이 너무`Not Supported`, 다음 hello지 않습니다:

다음 줄을 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
다음 줄로 바꿉니다.
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>세션 동작 및 SSO
toochange 세션 동작 및 SSO 구성 tooadd 해야는 `<UserJourneyBehaviors>` 요소 hello 내의 요소 `<RelyingParty>` 요소입니다.  hello `<UserJourneyBehaviors>` 요소 바로 뒤에 붙여야 hello `<DefaultUserJourney>`합니다.  내부에 hello 프로그램 `<UserJourneyBehavors>` 요소는 다음과 같이 표시 됩니다.

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Single sign-on (SSO) 구성** 의 toomodify hello 값이 필요한 toochange hello single sign on 구성, `<SingleSignOn>`합니다.  hello 적용 가능한 값은 `Tenant`, `Application`, `Policy` 및 `Disabled`합니다. 

**웹 응용 프로그램 세션 수명 (분)** toochange hello hello 웹 응용 프로그램의 hello toomodify 값이 필요한 세션 수명 `<SessionExpiryInSeconds>` 요소입니다.  기본 제공 정책에서 hello 기본값은 86, 400 초 (1440 분)입니다.

**웹 앱에 대 한 세션 제한 시간** 의 toomodify hello 값이 필요한 toochange hello 웹 응용 프로그램 세션 제한 시간 `<SessionExpiryType>`합니다.  hello 적용 가능한 값은 `Absolute` 및 `Rolling`합니다.
