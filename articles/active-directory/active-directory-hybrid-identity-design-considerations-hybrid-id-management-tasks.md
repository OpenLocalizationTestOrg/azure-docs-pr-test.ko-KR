---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-하이브리드 identity 관리 작업을 확인 | Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory hello 사용자를 인증할 때 및 toohello 응용 프로그램 액세스를 허용 하기 전에 선택 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>하이브리드 ID 수명 주기에 대한 계획
Id는 hello 기반 엔터프라이즈 이동성 및 응용 프로그램 액세스 전략 중 하나입니다. 사용자의 신분을 tooyour 모바일 장치 또는 SaaS 앱에 로그인 하는 인지 hello 키 toogaining 액세스 tooeverything 합니다. 가장 높은 수준에서 id 관리 솔루션에 통합 하 고 자동화 하 고 리소스를 프로 비전의 hello 프로세스를 중앙에서 관리를 포함 하는 사용자 id 리포지토리에 간의 동기화 포함 되어 있습니다. hello id 솔루션 중앙 집중화 된 id를 온-프레미스와 클라우드 전반에서 및 특정 형태의 id 페더레이션 toomaintain 중앙 집중식된 인증을 사용 하 여 수도 및 안전 하 게 공유와 외부 사용자와 비즈니스와 공동으로 작업 합니다. 운영 체제 및 응용 프로그램 toopeople in, 또는 관련 된, 조직에서 리소스 사이입니다. 조직 구조는 변경 된 tooaccommodate hello 프로비저닝 정책과 절차 될 수 있습니다.

것도 중요 toohave id 솔루션 넓히려는 tooempower 사용자를 사용 하 여 제공 하 여 셀프 서비스 환경을 tookeep 생산성을 합니다. Id 솔루션은 보다 강력한 single sign on 사용자에 대 한 모든 hello 리소스 관리자에 액세스 하는 것이 필요할 수 있는 경우 수준은 사용자 자격 증명을 관리 하기 위한 표준화 된 절차를 사용할 수 있습니다. 일부 수준의 관리 감소 또는 hello 다양 한 관리 솔루션을 프로 비전 하는 hello에 따라 제거할 수 있습니다. 관리의 일부 수준이 프로비전 관리 솔루션의 너비에 따라 감소하거나 제거될 수 있습니다. 예를 들어 도메인 관리자는 hello 사람 및 해당 도메인의 리소스에에서만 사용할 수 있습니다. 이 사용자 관리 및 프로 비전 작업을 수행할 수 있지만 인증된 되지 않았습니다. toodo 워크플로 만드는 등 구성 작업은 합니다.

## <a name="determine-hybrid-identity-management-tasks"></a>하이브리드 ID 관리 작업 결정
조직에서 관리 작업을 배포 hello 정확도 및 관리 효율성을 개선 하 고 조직의 hello 작업 부하의 hello 균형을 향상 시킵니다. 다음은 강력한 id 관리 시스템을 정의 하는 hello 피벗 합니다.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

toodefine 하이브리드 identity 관리 작업, 하이브리드 id 채택 하는 hello 조직의 몇 가지 중요 특성을 이해 해야 합니다. 중요 한 toounderstand hello 현재 저장소 identity 소스를 사용 하는 경우 이러한 핵심 요소 알면, hello 기본 요구 사항을 갖습니다 및 tooask 해야 한다는 것에 따라 더 세분화 된 질문 하는 Id 솔루션에 대 한 더 나은 설계 결정 tooa 연결 됩니다.  

이러한 요구 사항을 정의 하는 동안 수행 하는 적어도 hello 확인 질문에 대답

* 프로비전 옵션: 
  
  * 강력한 계정 액세스 관리 및 프로 비전 시스템 hello 하이브리드 id 솔루션 지원 합니까?
  * 사용자, 그룹 및 암호 관리 toobe 라인 인가요?
  * 가 응답 id 수명 주기 관리 hello? 
    * 암호 업데이트 계정을 일시 중단하는 데 시간이 얼마나 걸립니까?
* 라이선스 관리: 
  
  * 하이브리드 id 솔루션 핸들 라이선스 관리 hello?
    * 그렇다면 어떤 기능을 사용할 수 있습니까?
* 솔루션 핸들 그룹 기반의 라이선스 관리 hello? 
  
      - 그러한 경우 가능한 tooassign 보안 그룹 tooit는 무엇입니까? 
       - 그렇다면 hello 클라우드 디렉터리 자동으로 할당 합니다 라이선스 tooall hello 그룹 구성원 hello? 
        - 사용자 추가, 이후에 hello 그룹에서 제거 되거나, 경우 됩니다 라이선스가 자동으로 할당 / 제거할 적절 하 게 되나요? 
* 다른 타사 ID 공급자와 통합:
* 이 하이브리드 솔루션 타사 id 공급자 tooimplement single sign on과 통합할 수 있습니다.
* 가능한 toounify은 모든 화합 id 시스템에 서로 다른 id 공급자를 hello?
* 그렇다면 공급자의 종류 및 상태는 어떠하며 어떤 기능을 사용할 수 있습니까?

## <a name="synchronization-management"></a>동기화 관리
identity manager toobe 수 toobring hello 목표 중 하나 모든 id 공급자를 hello 및 동기화 상태를 유지 합니다. Hello 데이터 동기화를 유지 마스터 권한 있는 id 공급자에 따라 합니다. 동기화 된 관리 모델을 사용 하는 하이브리드 id 시나리오에서 온-프레미스 서버에서 모든 사용자 및 장치 id 관리 및 hello 계정 및 필요에 따라 암호 toohello 클라우드를 동기화 합니다. hello 사용자 hello hello id 솔루션에서 확인 자신이 hello 클라우드 및 hello 암호 로그인에 마찬가지로 동일한 온-프레미스 암호를 입력 합니다. 이 모델은 디렉터리 동기화 도구를 사용합니다.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)하이브리드 id 솔루션의 tooproper 디자인 hello 동기화 확인 질문에 따라 해당 hello에 대 한 답변은: • hello 하이브리드 id 솔루션에 사용할 수 있는 hello 동기화 솔루션은 무엇입니까?
• Hello single sign-on 기능을 사용할 수 있는 무엇 인가요?
• B2B와 B2C 간에 id 페더레이션에 대 한 hello 옵션은 무엇입니까?

## <a name="next-steps"></a>다음 단계
[하이브리드 ID 관리 채택 전략 결정](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

