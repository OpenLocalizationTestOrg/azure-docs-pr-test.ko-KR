---
title: "Azure Active Directory B2B 공동 작업 사용자에 대 한 aaaConditional 액세스 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 대 한 선택적 액세스 tooyour 회사 응용 프로그램에 대 한 multi-factor authentication (MFA)를 지원"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>B2B 공동 작업 사용자에 대한 조건부 액세스

## <a name="multi-factor-authentication-for-b2b-users"></a>B2B 사용자에 대한 다단계 인증
Azure AD B2B 공동 작업을 통해 조직에서는 B2B 사용자에 대한 MFA(Multi-Factor Authentication) 정책을 적용할 수 있습니다. 이러한 정책이 적용 hello 테 넌 트, 앱 또는 개별 사용자 수준에서 hello 정규직 직원 및 hello 조직의 멤버에 대해 설정 된 동일한 방식으로 합니다. Hello 리소스 조직에서 MFA 정책은 적용 합니다.

예제:
1. 관리자 또는 정보 근로자 회사 A에서에서 B 사는 tooan 응용 프로그램에서 사용자를 초대 *Foo* 회사 A에서
2. 응용 프로그램 *Foo* 회사 A는 구성 된 toorequire MFA 액세스 합니다.
3. B 사는에서 hello 사용자 tooaccess 응용 프로그램을 시도 하는 경우 *Foo* hello 회사는 테 넌 트에 toocomplete MFA 챌린지를 요청 합니다.
4. hello 사용자 회사 A가 MFA를 설정할 수 및가 자신의 MFA 옵션을 선택 합니다.
5. 이러한 시나리오는 어떤 ID에도 잘 맞습니다(Azure AD 또는 회사 B의 사용자가 소셜 ID를 사용하여 인증을 받는 경우 MSA).
6. 회사 A는 MFA를 지원하는 충분한 Azure AD 프리미엄 라이선스가 있어야 합니다. B 사는에서 hello 사용자가 회사 A에서에서이 라이선스 사용

hello 초대 테 넌 시는 hello 파트너 조직에는 MFA 기능이 하는 경우에 항상 hello 파트너 조직에서 사용자에 대 한 MFA 담당 합니다.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>B2B 공동 작업 사용자에 대한 MFA 설정
B2B 공동 작업 사용자가 MFA tooset 것이 얼마나 쉬운지 toodiscover 방법은 참조 비디오 다음 hello:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>B2B 사용자는 제안 상환을 위해 MFA 환경을 사용합니다.
다음 애니메이션 toosee hello 상환 경험 hello 확인해 보세요.

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>B2B 공동 작업 사용자에 대해 다시 설정된 MFA
현재 admin 님 안녕하세요 요구할 수 B2B 공동 작업 사용자 tooproof를 다시 hello 다음 PowerShell cmdlet을 사용 하 여:

1. TooAzure AD 연결

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. 증명 방법이 있는 모든 사용자 가져오기

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  다음은 예제입니다.

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. 특정 사용자 toorequire hello B2B 공동 작업 사용자 tooset 증명 방법에 대 한 hello MFA 메서드를 다시 설정 합니다. 예제:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Hello 리소스 테 넌 트에 MFA를 수행 하려면 이유 म?

Hello 현재 릴리스에서 MFA는 hello 리소스 테 넌 트, 예측 가능성의 이유로 항상 있습니다. 예를 들어 Contoso 사용자 (Sally)가 초대 된 tooFabrikam 고 Fabrikam B2B 사용자에 대 한 MFA를 활성화 가정해 봅니다.

Contoso에는 MFA 정책 App1 있지만 하지 App2 사용 다음 hello Contoso MFA 클레임 hello 토큰에 표시 될 수 있습니다 보면 hello 문제 다음:

* 1일: Contoso의 한 사용자에게 MFA가 있고 이 사용자가 App1에 액세스하는 경우 Fabrikam에 추가 MFA 프롬프트가 표시되지 않습니다.

* 2 일: hello 사용자가 액세스 Contoso에서 응용 프로그램 2 이제 Fabrikam에 액세스할 때, 있습니다 MFA에 대 한 등록 해야 합니다.

이 프로세스 혼동 될 수 있으며 toodrop 완료가 로그인에 발생할 수 있습니다.

또한도 Contoso에 MFA 기능이 없는 경우 항상 hello 사례 hello Fabrikam에서 Contoso MFA 정책 hello를 신뢰 합니다.

마지막으로 리소스 테넌트 MFA는 MSA 및 소셜 ID에도 적용되고 MFA가 설정되지 않은 파트너 조직에도 적용됩니다.

따라서 B2B 사용자에 대 한 MFA에 대 한 hello 권장 tooalways hello 초대 테 넌 트에에서 MFA를 요구 사항은입니다. 이 요구 사항은 경우에 따라 MFA toodouble 될 수 있지만 hello 최종 사용자에 게 체험은 예측 가능한 hello 초대 테 넌 트에 액세스 하 때마다: Sally hello 초대 테 넌 트와 MFA를 등록 해야 합니다.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>B2B 사용자에 대한 장치 기반, 위치 기반 및 위험 기반 조건부 액세스

Contoso 회사 데이터에 대 한 장치 기반 조건부 액세스 정책을 사용 하면 때 Contoso 및 hello Contoso 장치 정책을 준수 하지 않으면 관리 되지 않는 장치에서 액세스할 수 없게 됩니다.

Hello B2B 사용자의 장치는 Contoso에 의해 관리 되지, 이러한 정책이 적용 된 모든 컨텍스트에서 hello 파트너 조직에서 B2B 사용자의 액세스 차단 됩니다. 그러나 Contoso 장치 기반 조건부 액세스 정책에서 hello 특정 파트너 사용자 tooexclude를 포함 하는 목록을 제외를 만들 수 있습니다.

#### <a name="location-based-conditional-access-for-b2b"></a>B2B에 대한 위치 기반 조건부 액세스

위치 기반 조건부 액세스 정책은 수 toocreate 파트너 조직을 정의 하는 신뢰할 수 있는 IP 주소 범위는 하는 hello 초대 조직 B2B 사용자에 대 한 적용 될 수 있습니다.

#### <a name="risk-based-conditional-access-for-b2b"></a>B2B에 대한 위험 기반 조건부 액세스

현재 로그인 위험 기반 정책 hello 위험 평가 hello B2B 사용자의 홈 조직에서 수행 되기 때문에 적용 된 tooB2B 사용자 일 수 없습니다.

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [hello B2B 공동 작업 초대 메일의 hello 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 공동 작업 API 및 사용자 지정](active-directory-b2b-api.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
