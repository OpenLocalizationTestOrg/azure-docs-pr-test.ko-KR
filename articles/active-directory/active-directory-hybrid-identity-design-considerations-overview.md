---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-개요 | Microsoft Docs"
description: "하이브리드 ID 설계 고려 사항 가이드의 개요 및 콘텐츠 맵"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Azure Active Directory 하이브리드 ID 설계 고려 사항
소비자 기반 장치 hello 기업 세계 퍼지고는 및 클라우드 기반 소프트웨어-as a service (SaaS) 응용 프로그램은 쉽게 tooadopt 합니다. 결과적으로 내부 데이터 센터 및 클라우드 플랫폼에 걸쳐 사용자의 응용 프로그램 액세스를 제어하도록 유지하는 것은 어렵습니다.  

Microsoft의 id 솔루션에는 온-프레미스 및 클라우드 기반 기능을 위치에 관계 없이 tooall 리소스, 인증 및 권한 부여에 대 한 단일 사용자 id를 만드는 걸쳐 있습니다. 하이브리드 ID라고 합니다. 다양 한 설계 및 Microsoft 솔루션을 사용 하는 하이브리드 id에 대 한 구성 옵션이 있으며 일부 경우에 가장 잘 부합 하는 조합을 조직의 hello 요구 하는 어려운 toodetermine 수 있습니다. 

이 하이브리드 Id 디자인 고려 사항 가이드 toodesign hello 비즈니스 및 기술에 가장 잘 맞는 하이브리드 id 솔루션 조직에 대해 요구 하는 방법을 toounderstand를 수 있습니다.  이 가이드는 일련의 단계와 조직의 고유한 요구 사항을 충족 하는 하이브리드 id 솔루션을 디자인 toohelp를 따를 수 작업을 자세히 설명 합니다. Hello 단계 및 작업의 경우 각 hello 가이드에서는 hello 관련 기술 및 기능 옵션 사용 가능한 tooorganizations toomeet 기능 및 서비스 품질 (예: 가용성, 확장성, 성능, 관리 효율성 및 보안) 있는 수준 요구 사항입니다. 

특히, hello 하이브리드 identity 디자인 고려 사항 가이드 목표는 질문을 따라 tooanswer hello입니다. 

* 질문 수행할 tooask 필요 하 고 답변 toodrive 하이브리드 id 별 디자인 기술 또는 문제 영역에 대 한 내 요구에 가장 적합 합니까?
* 작업의 시퀀스를 어떤 해야 toodesign hello 기술 또는 문제 영역에 대 한 하이브리드 id 솔루션을 완료 합니까? 
* 어떤 하이브리드 id 기술 및 구성 옵션은 사용할 수 있는 toohelp 내 요구 사항을 충족 한? 비즈니스에 대 한 hello 가장 적합 한 옵션을 선택할 수 있나요 hello 척도로 상대적 이러한 옵션은 무엇입니까?

## <a name="who-is-this-guide-intended-for"></a>이 가이드는 누구를 위해 마련되었습니까?
 CIO, CITO, 수석 ID 설계자, 엔터프라이즈 설계자 및 IT 설계자는 중간 규모 또는 대규모 조직에 하이브리드 ID 솔루션의 설계를 담당합니다.

## <a name="how-can-this-guide-help-you"></a>이 가이드가 어떻게 도움이 됩니까?
이 가이드 toounderstand를 사용할 수 있습니다 어떻게 toodesign 수 toointegrate 클라우드에 있는 하이브리드 id 솔루션 기반 id 관리 시스템에 현재 온-프레미스 id 솔루션입니다. 

다음 그래픽 hello toomanage toointegrate IT 관리자의 현재 Windows Server Active Directory에 있는 솔루션 온-프레미스와 Microsoft Azure Active Directory tooenable 사용자 toouse 단일 수 있도록 하는 하이브리드 id 솔루션 예가 나와 Sign-on (SSO) hello 클라우드 및 온-프레미스에 있는 응용 프로그램 간에 합니다.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

위의 그림 hello는 클라우드를 활용 하는 하이브리드 id 솔루션의 예 단일 경험 toohello 최종 사용자 인증 프로세스 및 IT toofacilitate toointegrate 순서 tooprovide에 온-프레미스 기능이 서비스 관리 이러한 리소스입니다. 이 있을 수도 있지만 매우 일반적인 시나리오, 모든 조직의 하이브리드 identity 디자인 toodifferent 요구 사항을 인해 그림 1에 설명 된 hello 예제와 다른 가능성이 toobe입니다. 

이 가이드의 단계와 작업 toodesign 조직의 고유한 요구 사항을 충족 하는 하이브리드 id 솔루션을 따를 수를 제공 합니다. Hello 전체에서 다음 단계 및 작업, hello 가이드 표시 hello 관련 기술 및 기능 사용 가능한 tooyou toomeet 기능 및 서비스 품질 수준 요구 사항을 조직에 대 한 옵션입니다.

**가정**: Windows Server, Active Directory 도메인 서비스 및 Azure Active Directory를 사용한 경험이 있습니다. 이 문서에서는 이러한 솔루션이 자체적으로 또는 통합된 솔루션에서 비즈니스 요구를 충족하는 방법을 찾는다고 가정합니다.

## <a name="design-considerations-overview"></a>설계 고려 사항 개요
이 문서에는 일련을의 단계와 작업 요구 사항에 가장 잘 맞는 하이브리드 id 솔루션 toodesign를 따를 수 있습니다. hello 단계는 순서에 제시 됩니다. 그러나 이후 단계에서 배우는 설계 고려 toochange 결정 한 사항을 이전 단계에서 tooconflicting 설계 선택 사항은 인해 필요할 수 있습니다. 모든 시도 tooalert hello 문서 전체에서 설계 충돌이 toopotential 있습니다. 

가장 적절히 tooincorporate 필요한 횟수 만큼 hello 단계를 반복 하면 요구 사항을 충족 하는 hello 디자인에 도달 하 모든 hello 문서 내에서 hello 고려 사항입니다. 

| 하이브리드 ID 단계 | 항목 목록 |
| --- | --- |
| ID 요구 사항 확인 |[비즈니스 요구 사항 결정](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [디렉터리 동기화 요구 사항 결정](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Multi-Factor Authentication 요구 사항 결정](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [하이브리드 ID 채택 전략 정의](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| 강력한 ID 솔루션을 통해 데이터 보안을 향상하기 위한 계획 |[데이터 보호 요구 사항 결정](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [콘텐츠 관리 요구 사항 결정](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [액세스 제어 요구 사항 확인](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| 하이브리드 ID 수명 주기에 대한 계획 |[하이브리드 ID 관리 작업 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [동기화 관리](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [하이브리드 ID 관리 채택 전략 결정](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>이 가이드 다운로드
Hello에서 pdf 버전의 hello 하이브리드 Id 디자인 고려 사항 가이드를 다운로드할 수 있습니다 [Technet 갤러리](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288)합니다. 

