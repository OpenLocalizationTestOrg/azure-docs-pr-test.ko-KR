---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-인시던트 rResponse 요구 사항을 결정 | Microsoft Docs"
description: "IT tootake 작업 tooidentify로 이용 될 수 있습니다 및 잠재적인 위협을 완화 하는 hello 하이브리드 id 솔루션에 대 한 모니터링 및 보고 기능을 결정"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>하이브리드 ID 솔루션에 대한 인시던트 대응 요구 사항 확인
대규모 또는 중간 규모 조직 있을 가능성이 가장 높습니다 됩니다는 [보안 사고 대응](https://technet.microsoft.com/library/cc700825.aspx) 위치 toohelp IT에서에서 작업을 적절 하 게 수행할 인시던트의 toohello 수준입니다. hello identity 관리 시스템은 hello 목표에 대해 특정 작업을 수행한 사용자를 식별 하는 사용 되는 toohelp 수 있기 때문에 hello 사고 대응 프로세스에서 중요 한 요소입니다. hello 하이브리드 id 솔루션 수 tooprovide 모니터링 및 IT tootake 작업 tooidentify로 이용 될 수 하 고 잠재적인 위협을 완화 하는 기능을 보고 해야 합니다. 일반적인 사고 대응 계획에 hello hello 계획의 일환으로 단계를 수행 해야 합니다.

1. 초기 평가.
2. 인시던트 통신.
3. 피해 제어 및 위험 감소.
4. 손상 및 심각도의 식별.
5. 증거 보존.
6. 알림 tooappropriate 당사자입니다.
7. 시스템 복구.
8. 설명서.
9. 피해 및 비용 평가.
10. 프로세스 및 계획 수정.

어떤 it의 hello 식별 하는 동안 손상 및 심각도 단계를 필요한 tooidentify hello 시스템을 손상 된 파일 액세스 되 고 해당 파일의 hello 중요도 결정 하는 것입니다. 하이브리드 id 시스템과 이러한 요구 사항을 tooassist toofulfill 수 있어야 하면 해당 변경 작업을 수행 하는 hello 사용자 식별 합니다. 

## <a name="monitoring-and-reporting"></a>모니터링 및 보고
여러 번 hello id 시스템 hello 시스템의 기본 제공 감사 및 보고 기능을 제공 하는 경우에 주로 초기 평가 단계에서 유용할 수 있습니다. Hello 초기 평가 하는 동안 IT 관리자가 의심 스러운 활동 수 tooidentify 이거나 hello 시스템 미리 구성 된 작업에 따라 자동으로 수 tootrigger 수 있어야 합니다. 다른 경우 시스템이 잘못 구성된 침입 감지 시스템 tooa 수의 거짓 긍정 이어질 수 있지만 많은 활동 공격의 가능성을 나타낼 수 있습니다. 

hello id 관리 시스템 IT 관리자 tooidentify 지원 하 고 의심 스러운 활동을 보고 해야 합니다. 일반적으로 이러한 기술 요구 사항은 모든 시스템을 모니터링하고 잠재적인 위협 요소를 강조 표시할 수 있는 보고 기능에 의해 수행될 수 있습니다. Hello 질문을 사용 하면서 고려 사고 대응 요구 사항으로 하이브리드 id 솔루션을 디자인할 toohelp 아래:

* 회사는 보안 인시던트 대응에 대비하고 있습니까?
  * 예, hello 현재 id 관리 시스템으로 사용 됩니다 hello 프로세스의 일부로?
* 회사 다양 한 장치의 tooidentify 의심 스러운 로그온 시도 사용자 로부터 필요 합니까?
* 회사에 toodetect 잠재적인 공격에 노출 된 사용자의 자격 증명이 필요 합니까?
* 회사는 tooaudit 사용자의 액세스 및 작업에 필요 합니까?
* 사용자 암호를 다시 설정 하는 경우 회사 tooknow에 필요 합니까?

## <a name="policy-enforcement"></a>정책 적용
이 손상 제어 및 위험 감소 단계 동안 tooquickly 공격 hello 실제 및 잠재적 효과가 저하 중요 합니다. 이 시점에서 수행할 해당 동작 사소한와 심각한 hello 차이 만들 수 있습니다. hello 정확한 대응 조직과 hello 공격의의 hello 특성에 따라 달라 집니다. Hello 초기 평가 계정을 보안이 손상 된 데이터를 완료 하는 경우이 계정이 tooenforce 정책 tooblock 필요 합니다. Hello id 관리 시스템을 활용 하는 예 중 하나일 뿐입니다. Tooreact tooan 진행 중인 인시던트 적용 정책 되는 방식을 점을 고려 하는 동안 하이브리드 id 솔루션을 디자인할 toohelp 아래 hello 질문을 사용 합니다.

* 회사에에서 한 정책이 있습니까 액세스 hello 네트워크 위치 tooblock 사용자가 필요한 경우?
  * 그렇다면에 hello 현재 솔루션 통합 hello 하이브리드 id 관리 시스템 하락 tooadopt는?
* 회사 격리에 있는 사용자에 대 한 조건부 액세스 tooenforce에 필요 합니까? 

> [!NOTE]
> 각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다. [데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.  질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

