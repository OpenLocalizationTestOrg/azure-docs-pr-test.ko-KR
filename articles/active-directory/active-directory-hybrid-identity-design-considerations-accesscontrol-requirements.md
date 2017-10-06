---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-액세스 제어 요구 사항을 결정 | Microsoft Docs"
description: "덮개 hello 독특하고 id 및 사용자는 하이브리드 환경에 대 한 리소스에 대 한 액세스 요구 사항 확인 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>하이브리드 ID 솔루션에 대한 액세스 제어 요구 사항 확인
이 기회 tooreview 사용할 수도 있습니다는 하이브리드 id 솔루션 toomake를 계획 하는 hello 리소스에 대 한 요구 사항을 확인 조직을 디자인할 때 사용자에 사용할 수 있게 합니다. hello 데이터 액세스는 id의 모든 4 개의 독특하고 간:

* 관리
* 인증
* 권한 부여
* 감사

뒤에 오는 hello 섹션에서는 인증 및 권한 부여 자세히 설명, 관리와 감사 hello 하이브리드 identity lifecycle 포함 되어 있습니다. 이러한 기능에 대한 자세한 내용은 [하이브리드 ID 관리 작업 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)을 읽습니다.

> [!NOTE]
> 읽기 [hello 4 개의 독특하고의 Identity-hello Age의 하이브리드 IT에서에서 Id 관리](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) 이러한 독특하고의 각 노드에 대 한 자세한 내용은 합니다.
> 
> 

## <a name="authentication-and-authorization"></a>인증 및 권한 부여
인증 및 권한 부여에 대 한 다양 한 시나리오는, 이러한 시나리오는 hello 회사는 진행 중인 tooadopt hello 하이브리드 id 솔루션에 의해 충족 해야 하는 특정 요구 사항을 갖습니다. 비즈니스 tooBusiness (B2B)를 포함 하는 시나리오 통신 추가할 수 추가 챌린지 IT 관리자에 대 한 이후 hello 조직에서 사용 되는 hello 인증 및 권한 부여 방법 비즈니스 파트너와 통신할 수 있는 tooensure 필요 합니다. 인증 및 권한 부여 요구 사항에 대 한 프로세스를 디자인 하는 hello, 하는 동안 해당 hello 다음 질문에 대 한 답변은 확인 해야 합니다.

* 조직이 해당 ID 관리 시스템에 있는 사용자만 인증하고 권한을 부여합니까?
  * B2B 시나리오에 대한 계획이 있습니까?
  * 그러한 경우 이미 알 수 있는 프로토콜 (SAML, OAuth, Kerberos, 토큰 또는 인증서)는 두 비즈니스 사용된 tooconnect 수 있습니까?
* Hello 하이브리드 id 솔루션 tooadopt 하려는 이러한 프로토콜을 지원 합니까?

또 다른 중요 한 지점을 tooconsider 이며 사용자 및 파트너에서 사용할 hello 인증 리포지토리 배치 될 위치 hello 관리 모델 toobe 사용 합니다. 다음 두 가지 핵심 옵션 hello를 고려 합니다.

* 중앙 집중형:이 모델 hello에 사용자의 자격 증명, 정책 및 관리 될 수 있습니다 중앙 집중식된 온-프레미스 또는 클라우드에서 hello 합니다.
* 하이브리드:이 모델 hello에 사용자의 자격 증명, 정책 및 관리 됩니다 중앙 집중식된 온-프레미스와 복제 hello 클라우드.

Tooanswer hello를 질문 tooidentify hello id 관리 시스템은 상주 하 고 관리 모드 toouse hello 다음 보겠습니다 조직 채택 하 게 모델 tootheir 비즈니스 요구에 따라 달라 집니다.

* 현재 조직에는 ID 관리 온-프레미스가 있습니까?
  * 그렇다면 이러한 계획이 tookeep 것?
  * 조직 따라야 해당 규정 hello id 관리 시스템 상주해 야 규정 또는 준수 요구 사항이 있나요?
* 조직이 사용 하나요 single sign on 있는 앱 온-프레미스 또는 클라우드에서 hello?
  * 그러한 경우 하이브리드 id 모델의 hello 채택 영향은이 프로세스?

## <a name="access-control"></a>액세스 제어
인증 및 권한 부여는 사용자의 유효성 검사를 통해 핵심 요소 tooenable 액세스 toocorporate 데이터는 것도 중요 한 toocontrol hello 수준의 액세스는 이러한 사용자는 및 hello 보다 hello 수준의 관리자 액세스를 갖습니다. 관리 하 고 있는 리소스입니다. 하이브리드 id 솔루션 수 tooprovide 세부적인 액세스 tooresources, 위임 및 역할 기본 액세스를 제어 해야 합니다. 액세스 제어에 관한 질문 뒤 해당 hello 응답을 확인 합니다.

* 회사에는 높은 권한 toomanage 가진 둘 이상의 사용자 id 시스템과?
  * 예, 각 사용자 하나요 hello 동일한 액세스 수준?
* 회사 요구 toodelegate 액세스 toousers toomanage 특정 리소스는?
  * 그렇다면 얼마나 자주 발생합니까?
* 온-프레미스와 클라우드 간 액세스 제어 기능 toointegrate 해야 회사 리소스?
* 회사는 toolimit 액세스 tooresources toosome 조건에 따라 필요?
* 회사에 사용자 지정 컨트롤 toosome 리소스에 액세스 해야 하는 모든 응용 프로그램에는?
  * 그러한 경우 해당 앱 위치 (온-프레미스 또는 클라우드에서 hello)?
  * 예, 여기서는 해당 대상으로 배치 된 리소스 (온-프레미스 또는 클라우드에서 hello)?

> [!NOTE]
> 각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다. [데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.  질문에 답변하여 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
[사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

