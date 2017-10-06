---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-identity 요구 사항을 결정 | Microsoft Docs"
description: "밝혀 hello 하이브리드 identity 디자인 toodefine hello 요구 사항을 hello 회사의 비즈니스 요구를 식별 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>하이브리드 ID 솔루션에 대한 ID 요구 사항 확인
하이브리드 id 솔루션을 디자인 hello 첫 번째 단계는이 솔루션 활용 하는 hello 비즈니스 조직에 대 한 toodetermine hello 요구 사항입니다.  하이브리드 id (지원 다른 클라우드 솔루션을 모든 인증을 제공 하 여) 지원 역할을 시작 하 고 계속 해 서 사용자에 대 한 새 워크 로드의 잠금을 해제 하는 tooprovide 새롭고 흥미로운 기능.  이러한 워크 로드 또는 서비스 사용자를 위해 tooadopt 한다고 hello 하이브리드 identity 디자인에 대 한 hello 요구 사항에 따라 결정 됩니다.  이러한 서비스와 작업 tooleverage 하이브리드 id 온-프레미스를 필요 하 고 hello 클라우드에서 합니다.  

필요한 toogo hello 비즈니스 toounderstand의 이러한 주요 측면을 통해 어떤 이제는 요구 사항 및 미래 hello에 대 한 hello 제조업체 계획 합니다. 하이브리드 identity 디자인에 대 한 hello 장기적인 전략의 hello 표시 여부를 설정 하지 않은 가능성 경우 증가 변화 hello 비즈니스 요구에 따라 솔루션 확장 가능한 되지 것입니다.   다음 다이어그램 그는 하이브리드 identity 아키텍처 및 hello 워크 로드의 사용자에 대 한 잠금 해제 하는 예제 T입니다. 이 잠금을 해제 하 고 단색 하이브리드 identity 전략으로 배달 수 있는 모든 hello 새로운 가능성의 예가 있습니다. 

Hello 하이브리드 id 아키텍처의 일부인 일부 구성 요소![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>비즈니스 요구 사항 결정
각 회사는 서로 다른 요구 사항을 갖습니다의 hello 속하는이 회사 들 경우에 동일한 업계 hello 실제 비즈니스 요구 사항이 다를 수 있습니다. Hello 업계의 모범 사례를 활용할 수 있지만 궁극적으로 밝혀 hello 하이브리드 identity 디자인 toodefine hello 요구 사항을 hello 회사의 비즈니스 요구 합니다. 

Tooanswer hello 다음 질문 tooidentify 비즈니스 있는지 확인 해야 합니다.

* 회사는 toocut IT 운영 비용을 찾고 있나요?
* 회사는 toosecure 클라우드 자산 (SaaS 앱, 인프라)를 찾고 있습니까?
* Toomodernize 찾고 회사는 it 부서?
  * 사용자가 더 모바일로 바뀌고 까다로운 IT toocreate 예외는 DMZ tooallow 다른 종류의 트래픽 tooaccess 다른 리소스에 있습니까?
  * 회사에 있습니까 필요한 toobe 게시 하는 레거시 앱 toothese 최근 사용자 하지는 않지만 쉽게 toorewrite?
  * 회사 tooaccomplish 이러한 작업을 모두 필요 않으며 hello에 컨트롤에서 동시?
* 회사는 toosecure 사용자의 id를 찾고 및 Microsoft Azure 보안 전문 지식 온-프레미스 hello 전문 지식을 활용 하는 새로운 도구를 전환 하 여 위험을 줄이려면?
* 회사 tooget hello 제거를 시도 무서운 온-프레미스 "외부" 계정을 사용 하 고 여기서는 더 이상 온-프레미스 환경 내 유휴 위협 toohello 클라우드 이동은?

## <a name="analyze-on-premises-identity-infrastructure"></a>온-프레미스 ID 인프라 분석
회사의 비즈니스 요구 사항에 대 한 아이디어를가지고 온-프레미스 id 인프라 tooevaluate 할 수 있습니다. 이 평가 현재 identity 솔루션 toohello 클라우드 id 관리 시스템과 hello 기술 요구 사항 toointegrate 정의 하기 위한 중요 합니다. 다음 질문 있는지 tooanswer hello를 확인 합니다.

* 회사는 온-프레미스에 어떤 인증 및 권한 부여 솔루션을 사용합니까? 
* 회사에는 현재 온-프레미스 동기화 서비스가 있습니까?
* 회사가 타사 ID 공급자(IdP)를 사용합니까?

또한 해야 toobe 회사 있을 수 있는 hello 클라우드 서비스를 인식 합니다. 와 SaaS 평가 toounderstand hello 현재 통합을 수행 하는 경우, 환경에서 IaaS 또는 PaaS 모델이 매우 중요 합니다. 있는지 tooanswer hello 질문이이 평가 중에 다음을 확인 합니다.

* 귀사가 클라우드 서비스 공급자와 통합된 부분이 있습니까?
* 만약 그렇다면 어떤 서비스를 사용하십니까?
* 이 통합이 현재 운영 중입니까 아니면 파일럿입니까?

> [!NOTE]
> 모든 앱의 정확한 매핑을 사용 하도록 클라우드 서비스 있지 않을 경우 hello Cloud App Discovery 도구를 사용할 수 있습니다. 이 도구는 조직의 모든 비즈니스 및 소비자 클라우드 앱에 가시성이 있는 IT 부서를 제공할 수 있습니다. 통해 사용 패턴 및 클라우드 응용 프로그램을 액세스 하는 모든 사용자에 대 한 세부 정보를 포함 하 여 조직에서 현재까지 toodiscover 그림자 IT 쉬워졌습니다. 시작 tooget 참조 [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md)합니다.
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>ID 통합 요구 사항 평가
다음으로, tooevaluate hello identity 통합 요구 해야 합니다. 이 평가 중요 한 toodefine hello 기술 요구 사항에 사용자를 인증 하는 방법, hello 조직의 존재 hello 클라우드에서 어떻게 보일지, hello 조직 권한 부여는 허용 하는 방법 및 어떤 hello 사용자 환경은 진행 중인 toobe 것입니다. 다음 질문 있는지 tooanswer hello를 확인 합니다.

* 조직이 페더레이션, 표준 인증 또는 둘 모두를 사용합니까?
* 페더레이션 요구 사항입니까?  Hello 다음 때문에:
  * Kerberos 기반 SSO
  * 회사에는 SAML 또는 유사한 페더레이션 기능을 사용하는 온-프레미스 응용 프로그램이 있습니다.(기본 제공 또는 타사 제공 중 하나)
  * 스마트 카드를 통한 MFA. RSA SecurID 등.
  * 아래 hello 질문을 해결 하는 클라이언트 액세스 규칙:
    1. 모든 외부 액세스 tooOffice hello 클라이언트의 hello IP 주소에 따라 365를 차단할 수 있나요?
    2. Exchange ActiveSync를 제외한 모든 외부 액세스 tooOffice 365를 차단할 수 있나요?
    3. 브라우저 기반 앱 (OWA, SPO)를 제외한 모든 외부 액세스 tooOffice 365를 차단할 수 있나요
    4. 지정 된 AD 그룹의 구성원에 대 한 모든 외부 액세스 tooOffice 365를 차단할 수 있나요
* 보안/감사 문제
* 페더레이션된 인증에서 기존 투자
* Hello 클라우드에서 도메인에 대 한 현재 조직에서 사용할는 어떤 이름을?
* Hello 조직 사용자 지정 도메인 있습니까?
  1. 해당 도메인이 공용이고 DNS를 통해 쉽게 확인할 수 있습니까?
  2. 그렇지 않은 경우 다음 있습니까 AD에 사용 되는 tooregister 대체 UPN을 저장할 수 있는 공용 도메인?
* 클라우드 표현에 대 한 일관 된 사용자 식별자 hello? 
* Hello 조직 클라우드 서비스와 통합 되어야 하는 앱이 있나요?
* Hello 조직에서는 여러 도메인 보유 하 고 표준 또는 페더레이션 인증을 모두 사용 됩니다?

## <a name="evaluate-applications-that-run-in-your-environment"></a>사용자 환경에서 실행하는 응용 프로그램 평가
온-프레미스에 대 한 아이디어를 있고 클라우드 인프라를 했으므로 이러한 환경에서 실행 되는 tooevaluate hello 응용 프로그램 해야 합니다. 이 평가 toodefine hello 기술 요구 사항 toointegrate 이러한 응용 프로그램 toohello 클라우드 id 관리 시스템 중요 합니다. 다음 질문 있는지 tooanswer hello를 확인 합니다.

* 응용 프로그램은 어디에 있습니까?
* 사용자는 온-프레미스 응용 프로그램에 액세스합니까?  Hello 클라우드에서? 또는 둘 모두?
* 계획 tootake hello 기존 응용 프로그램 작업 부하 및 사항이 toohello 클라우드 이동?
* 온-프레미스에 상주 하는 hello 클라우드 있는 toodevelop 새 응용 프로그램은 클라우드 인증을 사용 하는 계획 있습니까?

## <a name="evaluate-user-requirements"></a>사용자 요구 사항 평가
또한 tooevaluate hello 사용자 요구 사항이 있습니다. 이 평가 온 보 딩 및 toohello 클라우드를 전환할 때 사용자가 지원 해야 하는 중요 한 toodefine hello 단계. 다음 질문 있는지 tooanswer hello를 확인 합니다.

* 사용자는 응용 프로그램 온-프레미스에 액세스합니까?
* 액세스 하는 사용자가 응용 프로그램 hello 클라우드에서?
* 사용자가 수행 하는 방법은 일반적으로 로그인 tootheir 온-프레미스 환경?
* 사용자가 로그인 toohello는 어떻게 클라우드?

> [!NOTE]
> 각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다. [사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.  질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
[디렉터리 동기화 요구 사항 결정](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>참고 항목
[디자인 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

