---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-데이터 보호 요구 사항을 확인 | Microsoft Docs"
description: "하이브리드 id 솔루션을 계획을 식별 하는 경우 귀하 비즈니스에 대 한 hello 데이터 보호 요구 사항 및 옵션을 사용할 수 있는 toobest 이러한 요구에 부합 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>강력한 ID 솔루션을 통해 데이터 보안을 향상하기 위한 계획
hello 첫 번째 단계 tooprotect hello 데이터가 해당 데이터에 액세스할 수 있는 사용자 식별 되며 toohave 수 있는 id 솔루션 시스템 tooprovide 인증 및 권한 부여 기능 통합이 프로세스의 일부로 필요 합니다. 인증 및 권한 부여는 종종 서로 혼동되고 역할은 오해됩니다. 실제로 매우 다릅니다, 아래 hello 그림에 나와 있는 것 처럼:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**모바일 장치 관리 수명 주기 단계**

하이브리드 id 솔루션을 계획할 때 이러한 요구에 부합 조직 및 옵션을 사용할 수 있는 toobest hello 데이터 보호 요구 사항을 이해 해야 합니다.

> [!NOTE]
> 데이터 보안 계획을 완료 한 후 검토 [다단계 인증 요구 사항을 결정](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure는 다단계 인증 요구 사항에 대 한 선택 항목에 영향을 받지 않은 hello 결정 이 섹션에 있습니다.
> 
> 

## <a name="determine-data-protection-requirements"></a>데이터 보호 요구 사항 결정
이동성 hello 시대의 대부분의 기업 들은 공통의 목표를: 해당 사용자가 toobe에서 생산성을 유지 하는 동안 온-프레미스 또는 원격으로 모바일 장치에 순서 tooincrease 생산성 곳에 나 사용 하도록 설정 합니다. 이 수는 공통의 목표를 하는 동안 회사 그러한 요구 사항에 안전 하 게 순서 tookeep 회사의 데이터에 완화 해야 하 고 사용자의 개인 정보를 유지 관리 하는 위협 양 hello에 관한 수도 있습니다. 각 회사는 이런 점에서; 서로 다른 요구 사항을 있을 수 있습니다. 다양 한 규정 준수 규칙을 따라 toowhich 업계 hello 회사 달라 집니다가 작동 하는 발생할 toodifferent 디자인 관련 결정 합니다. 

그러나 보안 측면이 있습니다 탐색 하 고 hello 업계에 관계 없이 유효성 검사 해야 하는 hello 다음 섹션에 설명 된 합니다.

## <a name="data-protection-paths"></a>데이터 보호 경로
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**데이터 보호 경로**

위의 다이어그램 hello, hello id 구성 요소를 데이터에 액세스 하기 전에 확인 하는 첫 번째 toobe hello 됩니다. 그러나이 데이터는 서로 다른 상태에 액세스 하는 hello 시간 동안 수 있습니다. 이 다이어그램의 각 숫자는 데이터가 특정 시점에 위치할 수 있는 경로를 나타냅니다. 이러한 숫자는 아래에 설명됩니다.

1. Hello 장치 수준의 데이터 보호 합니다.
2. 전송 중에 데이터 보호.
3. 휴지 상태의 온-프레미스에서 데이터 보호.
4. hello 클라우드의 데이터 보호 합니다.

Hello 하이브리드 id 솔루션은 온-프레미스를 활용할 수 있는 필요는 없지만 hello 기술적 컨트롤 단계 중 하나에 각 IT tooprotect hello 데이터 자체 수 있게 하는 hello 하이브리드 id 솔루션으로 직접 제공 되지 않습니다. 및 id 관리 리소스 tooidentify hello 사용자 권한 부여 toohello 데이터에 액세스 하기 전에 클라우드입니다. 다음 해당 hello 확인 하이브리드 id 솔루션을 계획 하는 경우 게시 된 질문은 tooyour 조직의 요구 사항에 따라:

## <a name="data-protection-at-rest"></a>휴지 상태의 데이터 보호
Hello 데이터 (장치, 클라우드 또는 온-프레미스) 미사용 위치에 관계 없이 반드시 tooperform 평가 toounderstand hello 조직 이런 점에서 필요 합니다. 이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.

* 미사용 데이터 tooprotect 회사에 필요 합니까?
  * 그렇다면 현재 온-프레미스 인프라와 hello 하이브리드 identity 솔루션 수 toointegrate은?
  * 그렇다면 hello 하이브리드 identity 솔루션 수 toointegrate hello 클라우드에 있는 작업으로는?
* Hello 클라우드 id 관리 수 tooprotect hello 사용자의 자격 증명 및 hello 클라우드에 저장 된 데이터를 다른 인가요?

## <a name="data-protection-in-transit"></a>전송 중인 데이터 보호
Hello 장치와 hello 데이터 센터 간 또는 hello 장치와 hello 클라우드 간에 전송 되는 데이터를 보호 되어야 합니다. 그러나 전송 중인 상태는 반드시 클라우드 서비스 외부의 구성 요소와 통신 프로세스를 의미하지 않습니다. 또한 예를 들어 두 가상 네트워크 간에 내부적으로 이동합니다. 이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.

* Tooprotect 전송 중인 데이터를에서 회사에 필요 합니까?
  * 그렇다면 hello 하이브리드 identity 솔루션 수 toointegrate SSL/TLS 보안 컨트롤은?
* Hello 클라우드 id 관리는 hello 트래픽 tooand 서명 hello 디렉터리 저장소 (내부 및 데이터 센터 간) 내에서 유지?

## <a name="compliance"></a>규정 준수
규정, 법률 및 규정 준수 요구 사항을 회사 속하는 toohello 업계에 따라 달라 집니다. 높은 업계 규정된에 회사 id 관리 문제 관련된 toocompliance 문제를 해결 해야 합니다. Sarbanes-oxley (SOX), Health Insurance Portability hello 및 Accountability Act (HIPAA) 등의 규정 hello Gramm-Leach-Bliley Act (GLBA) 및 id 및 액세스에 대 한 hello Payment Card Industry Data Security Standard (PCI DSS)은 매우 엄격한 합니다. 회사에서 채택할 hello 하이브리드 id 솔루션에 하나 이상의 이러한 규정 hello 요구 사항에 맞는 hello 핵심 기능이 있어야 합니다. 이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.

* Hello 하이브리드 id 솔루션 hello 비즈니스 규정 요구 사항을 준수 하는?
* 회사 toobe 준수 규정 요구 사항 수 있게 해 주는 기능에는 hello 하이브리드 id 솔루션 내장? 

> [!NOTE]
> 각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다. [데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.  질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
 [콘텐츠 관리 요구 사항 결정](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

