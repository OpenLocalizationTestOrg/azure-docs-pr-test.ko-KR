---
title: "라이선스 지침 aaaAzure Active Directory B2B 공동 작업 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에는 유료 Azure AD 라이선스가 필요하지 않지만 B2B 게스트 사용자를 위한 유료 기능도 얻을 수 있습니다."
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Azure Active Directory B2B 공동 작업 라이선스 지침

사용할 수 있습니다 tooinvite 게스트 사용자가 Azure AD B2B 공동 작업 기능으로 Azure AD 테 넌 트 tooallow tooaccess Azure AD 서비스 및 기타 리소스 조직에서. Tooprovide 액세스 toopaid Azure AD 기능을 사용 하도록 하려는 경우 B2B 공동 작업 게스트 사용자에 게 사용 허가 받아야와 적절 한 Azure AD 라이선스입니다. 

구체적으로 살펴보면 다음과 같습니다.
* Azure AD Free 기능은 추가 라이선싱 없이 게스트 사용자에게 제공됩니다.
* Tooprovide 액세스 toopaid Azure AD 기능 tooB2B 사용자가 하려는 경우 이러한 B2B 게스트 사용자에 게 충분 한 라이선스 toosupport 있어야 합니다.
* 라이선스를 지불 하는 Azure AD와 테 넌 트 초대 B2B 공동 작업 사용 권한 tooan 추가 5 B2B 게스트 초대 사용자 toohello 테 넌 트를 있습니다.
* hello 고객 테 넌 트를 초대 hello를 소유 하 고 hello 하나의 toodetermine B2B 공동 작업 하는 사용자 수 있어야 Azure AD 기능을 지불 해야 합니다. Azure AD 유료 hello에 따라 충분 한 Azure AD 있어야 게스트 사용자가 원하는 기능에에서 지급 된 라이선스 toocover B2B 공동 작업 사용자 hello 5:1 비율 동일 합니다.

B2B 공동 작업 게스트 사용자는 조직의 직원 또는 대기업에서 다른 비즈니스 직원이 아닌, 파트너 회사의 사용자로 추가됩니다. B2B 게스트 사용자는 이 문서에 설명된 것처럼 외부 자격 증명 또는 조직이 소유한 자격 증명으로 로그인할 수 있습니다. 

즉, B2B 라이선스는 설정 hello 사용자가 인증 하는 방법을가 아니라 하지만 hello 사용자 tooyour 조직의 hello 관계 여 있습니다. 이러한 사용자가 파트너가 아닌 경우 라이선스 조건에서 다르게 처리됩니다. 해당 UserType "게스트"로 표시 된 경우에 라이선싱 용 toobe B2B 공동 작업 사용자 고려 되지 않습니다. 이들은 사용자당 하나의 라이선스로 정상적인 사용 허가를 받아야 합니다. 이러한 사용자는 다음과 같습니다.
* 직원
* 외부 ID를 사용하여 로그인하는 직원
* 대기업에서 다른 비즈니스의 직원


## <a name="licensing-examples"></a>라이선스 예제
- 고객이 tooinvite 100 B2B 공동 작업 사용자 tooits Azure AD 테 넌 트입니다. 액세스 관리 및 모든 사용자에 대 한 프로비저닝 hello 고객 할당 하지만 사용자 50 명 MFA 및 조건부 액세스도 필요 합니다. 이 고객 구매 해야 10 Azure AD Basic 라이선스 및 10 Azure AD Premium P1 라이선스 toocover 이러한 B2B 사용자 올바르게 합니다. Hello 고객 B2B 사용자와 toouse Id 보호 기능을 계획 하는 경우 라이선스 toocover hello 초대 된 사용자가 Azure AD Premium P2 hello에 있어야 5:1 비율 동일 합니다.
- 한 명의 고객에게 Azure AD Premium P1으로 사용이 허가된 10명의 직원이 있습니다. 이제 tooinvite 60 B2B 필요한 사용자에 게 모든 multi-factor authentication (MFA) 원합니다. Hello 5:1 라이선스 규칙에서 모든 60 B2B 공동 작업 사용자 hello 고객 12 Azure AD Premium P1 라이선스 toocover 있어야 합니다. 10 직원에 게 10 프리미엄 P1 라이선스 이미 있는 MFA 같은 프리미엄 P1 기능 권한이 tooinvite 50 B2B 사용자가지고 있습니다. 이 예제에서는 그런 다음 이러한 해야 2 추가 라이선스를 구입 프리미엄 P1 toocover hello 나머지 10 B2B 공동 작업 사용자입니다.

> [!NOTE]
> Tooassign 라이선스 직접 toohello B2B 사용자 tooenable 이러한 B2B 공동 작업 사용자 권한을 아직 방법은 없습니다.

hello 고객 테 넌 트를 초대 hello를 소유 하 고 hello 하나의 toodetermine B2B 공동 작업 하는 사용자 수 있어야 Azure AD 기능을 지불 해야 합니다. 게스트 사용자에 대해 원하는 Azure AD 기능을 지불 하에 따라 충분 한 Azure AD hello 5:1 비율로 라이선스 toocover B2B 공동 작업 사용자가 유료 있어야 합니다. 

## <a name="additional-licensing-details"></a>추가 라이선스 정보
- Tooactually 할당 라이선스 tooB2B 사용자 계정이 필요 하지 않습니다. Hello 5:1 비율에 따라, 라이선스 자동으로 계산 되며 보고 합니다.
- Azure AD 라이선스 hello 테 넌 트와 Azure AD Free hello 모든 초대한 사용자 가져옵니다 hello 권한에에서 있는 경우 아니요 유료 버전 제공 합니다.
- 조직에서 공동 작업 사용자가 이미 유료 Azure AD B2B 라이선스, 경우 hello 초대 테 넌 트의 hello B2B 공동 작업 라이선스 중 하나가 사용 하지 않습니다.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>토론 고급: Api를 사용 하 여 "멤버로" conglomerate 조직에서 사용자가 추가할 때 hello 라이선스 고려 사항이 무엇 인가요?
B2B 게스트 사용자는 hello 호스트의 조직과 파트너 조직 toowork에서 초대입니다. 일반적으로 다른 모든 경우는 B2B 기능을 사용하더라도 B2B로 인정되지 않습니다. 특히 다음 두 가지 경우를 살펴보겠습니다.

1. 호스트가 소비자 주소를 사용하는 직원을 초대하는 경우
  * 이 시나리오는 라이선싱 정책을 준수하지 않으며 권장되지 않습니다.

2. 호스트 조직이 다른 대기업 조직의 사용자를 추가하는 경우
  1. 이 경우 B2B Api를 사용 하 여 hello 사용자는 초대 있지만이 경우는 전통적으로 B2B 되지 않습니다. 이상적으로 이러한 조직 해야 초대 (API를 통해) 구성원으로 다른 조직 사용자가 hello 합니다. 이 경우 라이선스가 toobe toothese 멤버 hello 조직 초대의 tooaccess 리소스를 할당 합니다.

  2. 일부 조직에서는 정책으로 "게스트"로 추가 하는 다른 조직 사용자가 toobe tooadd hello를 할 수 있습니다. 다음 두 가지 경우가 있습니다.
      * hello conglomerate 조직 이미 사용 하는 Azure AD 및 hello 초대 된 사용자 라이선스를 취득 hello에는 다른 조직의:이 경우이 문서의 앞부분에서 1:5 수식을 배치 하는 초대 된 사용자 tooneed toofollow hello 않을 것입니다. 

      * hello conglomerate 조직 Azure AD를 사용 하지 않는 또는 적절 한 라이선스가 없는 경우:이 경우이 문서의 앞부분에서 1:5 수식을 배치 하는 hello를 수행 합니다.

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [hello B2B 공동 작업 초대 메일의 hello 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 공동 작업 API 및 사용자 지정](active-directory-b2b-api.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
