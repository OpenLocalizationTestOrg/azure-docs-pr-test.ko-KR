---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-콘텐츠 관리 요구 사항을 결정 | Microsoft Docs"
description: "어떻게 toodetermine hello 비즈니스의 콘텐츠 관리 요구 사항에 대 한 정보를 제공 합니다. 일반적으로 사용자가 자신의 장치에 있을 때 있다고 생각할 수 또한 여러 자격 증명을 사용 하 여 그에 따라 toohello 응용 프로그램을 대체 합니다. 것이 중요 한 toodifferentiate 콘텐츠 hello 회사 자격 증명을 사용 하 여 만든 것과 개인 자격 증명을 사용 하 여 생성 합니다. Id 솔루션 해야 클라우드 서비스 tooprovide와 수 toointeract 동안 원활한 환경을 toohello 최종 사용자가 개인 정보 보호 및 데이터 유출 로부터 보호 하는 hello 기능을 강화 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>하이브리드 ID 솔루션에 대한 콘텐츠 관리 요구 사항 확인
Hello 콘텐츠 관리 요구 사항 이해 비즈니스가 필요할 수에 대 한 영향을 결정 하는 하이브리드 identity 솔루션 toouse에. 와 hello 확산 됨에 따라 여러 장치 및 사용자가 toobring의 hello 기능이 자신의 장치 ([BYOD](http://aka.ms/byodcg)), hello 회사는 자체 데이터를 보호 해야 하지만 또한 유지 하도록 사용자의 개인 정보 그대로 유지 합니다. 일반적으로 사용자가 자신의 장치에 있을 때 있다고 생각할 수 또한 여러 자격 증명을 사용 하 여 그에 따라 toohello 응용 프로그램을 대체 합니다. 것이 중요 한 toodifferentiate 콘텐츠 hello 회사 자격 증명을 사용 하 여 만든 것과 개인 자격 증명을 사용 하 여 생성 합니다. Id 솔루션 해야 클라우드 서비스 tooprovide와 수 toointeract 동안 원활한 환경을 toohello 최종 사용자가 개인 정보 보호 및 데이터 유출 로부터 보호 하는 hello 기능을 강화 합니다. 

Id 솔루션 아래 hello 그림에 나와 있는 것 처럼 순서 tooprovide 콘텐츠 관리의 다른 기술 제어에서 활용 됩니다.

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**ID 관리 시스템을 활용하는 보안 컨트롤**

일반적으로 콘텐츠 관리 요구 사항을 hello 다음 영역에서에서 id 관리 시스템과 활용 됩니다.

* 개인 정보: 리소스를 소유 하는 hello 사용자를 식별 하 고 hello 적절 한 컨트롤 toomaintain 무결성을 적용 합니다.
* 데이터 분류: hello 사용자 또는 그룹 및 tooits 분류에 따라 액세스 tooan 개체의 수준을 식별 합니다. 
* 데이터를 유출할 보호: tooavoid 유출 데이터를 보호 하는 일을 담당 하는 보안 제어 hello id 시스템 toovalidate hello 사용자의 id 가진 toointeract이 필요 합니다. 이는 감사 내역을 위해서도 중요합니다.

> [!NOTE]
> 데이터 분류에 대한 모범 사례 및 지침에 대한 자세한 내용은 [클라우드 준비를 위한 데이터 분류](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 를 참조하세요.
> 
> 

다음 해당 hello 확인 하이브리드 id 솔루션을 계획 하는 경우 게시 된 질문은 tooyour 조직의 요구 사항에 따라:

* 회사에가 보안 제어 위치 tooenforce 데이터 개인 정보 보호에 있습니까?
  * 그러한 경우 해당 보안 제어 삭제 됩니다 계속 tooadopt는 hello 하이브리드 id 솔루션으로 수 toointegrate?
* 회사에서 데이터 분류를 사용하나요?
  * 그러한 경우 진행 중인 tooadopt는 hello 하이브리드 id 솔루션으로 hello 현재 솔루션 수 toointegrate은?
* 현재 회사에 데이터 유출에 대한 솔루션이 있나요? 
  * 그러한 경우 진행 중인 tooadopt는 hello 하이브리드 id 솔루션으로 hello 현재 솔루션 수 toointegrate은?
* Tooaudit 액세스 tooresources 회사에 필요 합니까?
  * 그렇다면 어떤 유형의 리소스인가요?
  * 그렇다면 어떤 수준의 정보가 필요한가요?
  * 예, 여기서 hello 감사 로그 상주해 야 합니다. 온-프레미스 또는 클라우드에서 hello?
* 회사에 tooencrypt 필요 합니까 (SSNs, 신용 카드 번호 등)의 중요 한 데이터가 포함 된 모든 메일?
* 회사에 tooencrypt 필요 합니까 외부 비즈니스 파트너와 공유 하는 모든 문서/콘텐츠?
* 회사 전자 메일의 특정 종류의 tooenforce 회사 정책에 필요 합니까 (모든 회신 없음 수행, 전달 금지)?

> [!NOTE]
> 각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다. [데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.  질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
[액세스 제어 요구 사항 확인](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

