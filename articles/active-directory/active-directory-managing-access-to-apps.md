---
title: "Azure AD를 사용 하 여 aaaManaging 액세스 tooapps | Microsoft Docs"
description: "Azure Active Directory 조직 toospecify hello 앱 toowhich을 사용 하는 방법을 설명 합니다. 각 사용자가 액세스할 수 있습니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>액세스 tooapps 관리
지속적인 액세스 관리 사용 현황 초기값, 비교값 및 보고 응용 프로그램은 조직의 id 시스템에 통합 하 고 나면 toobe 챌린지를 계속 합니다. 대부분의 경우에서 기술 지원팀 또는 IT 관리자 역할이 있는 사용자 tootake 진행 중인 활성 tooyour 앱 액세스를 관리 합니다. 경우에 따라 할당은 일반 또는 부서 IT 팀에서 수행됩니다. 종종 hello 할당 의사 결정은 의도 한 toobe 위임된 toohello 비즈니스 의사 결정자 이며, IT는 하기 전에 해당 승인을 받도록 hello 할당 합니다.  다른 조직에서는 역할 기반 액세스 제어(RBAC) 또는 특성 기반 액세스 제어(ABAC)와 같은 기존의 자동화된 ID 및 액세스 관리 시스템의 통합에 투자합니다. Hello 통합 및 규칙 개발을 모두 특수 한 비용이 많이 드는 toobe는 경향이 있습니다. 관리 방법에 대한 모니터링 또는 보고는 별도로 비용이 드는 복잡한 투자입니다.

## <a name="how-does-azure-active-directory-help"></a>Azure Active Directory는 어떻게 지원합니까?
 조직 tooeasily를 사용 하도록 설정 하는 구성 된 응용 프로그램에 대 한 azure AD에서는 광범위 한 액세스 관리 hello 적절 한 액세스 정책을 포함 하 여 위임을 통해 자동으로 특성 기반 할당 (ABAC 또는 RBAC 시나리오)에서 범위의 달성 관리자 관리 합니다. Azure AD와 쉽게 ä à ï 복잡 한 정책을 단일 응용 프로그램에 대 한 여러 관리 모델을 결합 하 고 수 있는 응용 프로그램에서 관리 규칙에도 다시 사용 하 여 다른 사용자 들이 동일한 hello 합니다.

* [신규 또는 기존 응용 프로그램 추가](active-directory-sso-integrate-saas-apps.md)

 Azure AD의 응용 프로그램 할당은 두 가지 기본 할당 모드에 중점을 둡니다.

* **개별 할당** 디렉터리 전역 관리자 권한이 있는 IT 관리자는 개별 사용자 계정을 선택 하 고 액세스 권한을 부여할 수 toohello 응용 프로그램입니다.
* **그룹 기반 할당 (유료 Azure AD만 해당)** 는 IT 관리자가 디렉터리 전역 관리자 권한이 있는 그룹 toohello 응용 프로그램을 할당할 수 있습니다. 특정 사용자의 액세스 tooaccess hello 응용 프로그램 hello 시 hello 그룹의 구성원 인지 여부를 끄려고 의해 결정 됩니다. 즉, 관리자가 효과적으로 "hello 할당 그룹의 모든 현재 구성원에 게 액세스 toohello 응용 프로그램이" 없다는 할당 규칙을 만들 수 있습니다. 이 할당 옵션을 사용하여 관리자는 [특성 기반 동적 그룹](active-directory-accessmanagement-manage-groups.md), 외부 시스템 그룹(예: 온-프레미스 Active Directory 또는 Workday), 관리자 관리 또는 셀프 서비스 관리된 그룹을 포함하는 Azure AD 그룹 관리 옵션 중 하나에서 혜택을 줄 수 있습니다. 단일 그룹 쉽게 할당할 수 toomultiple 앱 확인 할당 선호도 있는 응용 프로그램 할당 규칙을 공유할 수 감소 전체 관리 복잡성 hello 합니다. 지원 되지 않습니다 tooapplications 그룹 기반 할당에 대 한이 이번에 해당 중첩된 그룹을 note 하십시오.

이러한 두 가지 할당 모드 관리자를 사용하면 바람직한 할당 관리 방법을 달성할 수 있습니다.

Azure AD와 사용량 및 할당 보고 완전히 통합, 할당 상태, 할당 오류 및 사용에도 tooeasily 보고서 관리자를 사용 하도록 설정 합니다.

## <a name="complex-application-assignment-with-azure-ad"></a>Azure AD를 사용하여 복잡한 응용 프로그램 할당
Salesforce와 같은 응용 프로그램을 고려합니다. 많은 조직에서 Salesforce는 hello 마케팅 및 판매 조직에서 주로 사용 됩니다. 종종 hello 마케팅 팀의 멤버는 높은 권한이 있지만 액세스 tooSalesforce hello 판매 팀의 멤버 액세스가 제한 하는 동안 합니다. 대부분의 경우에서 정보 근로자의 광범위 한 채우기를 액세스 toohello 응용 프로그램이 제한. 복잡 해질 예외 toothese 규칙입니다. 종종 hello 마케팅 또는 판매 리더십 팀 toogrant 사용자 액세스의 hello prerogative 또는 자신의 역할 이러한 일반 규칙 독립적으로 변경 됩니다.

Azure AD를 사용하여 Single Sign-On(SSO) 및 자동화된 프로비전에 Salesforce와 같은 응용 프로그램을 미리 구성할 수 있습니다. Hello 응용 프로그램 구성 되 면 관리자는 hello 일회용 작업 toocreate 걸릴 하 고 hello 적절 한 그룹을 할당할 수 있습니다. 이 예제에서는 관리자가 할당을 수행 하는 hello를 실행할 수 있습니다.

* [동적 그룹](active-directory-accessmanagement-manage-groups.md) 나타낼 수 있습니다 수 정의 tooautomatically 부서 또는 역할 같은 특성을 사용 하 여 hello 마케팅 및 판매 팀의 모든 구성원:
  
  * 마케팅 그룹의 모든 구성원이 Salesforce에서 toohello "마케팅" 역할 할당
  * Sales의 모든 구성원이 팀 그룹 Salesforce에서 toohello "sales" 역할 할당 됩니다. 보다 세부적인 toodifferent Salesforce 역할이 할당 된 지역에 영업 팀을 나타내는 여러 그룹을 사용할 수 없습니다.
* tooenable hello 예외 메커니즘에서 각 역할에 대해 셀프 서비스 그룹을 만들 수 있습니다. 예를 들어 hello "Salesforce 예외 마케팅" 그룹을 셀프 서비스 그룹으로 만들 수 있습니다. hello 그룹 toohello Salesforce 마케팅 역할을 할당할 수 있습니다 및 hello 마케팅 지도 팀 소유자를 만들 수 있습니다. Hello 마케팅 지도 팀의 멤버 수 추가 또는 사용자를 제거, 조인 정책을 설정 또는 승인 또는 개별 사용자의 요청 toojoin 거부 합니다. 소유자 또는 멤버에 대한 특별한 교육을 요구하지 않는 정보 작업자에 적절한 환경을 통해 지원됩니다.

이 경우 Salesforce에서는 역할 할당을 업데이트할 수는 추가 된 toodifferent 그룹 멤버인 모든 할당 된 사용자가 자동으로 프로 비전 된 tooSalesforce 것입니다. 사용자 수 toodiscover 라인과 hello Microsoft 응용 프로그램 액세스 패널을 Office 웹 클라이언트를 통해 또는 심지어 tootheir 조직 Salesforce 로그인 페이지를 탐색 하 여 Salesforce에 액세스 합니다. 관리자 수 tooeasily 사용 및 할당 상태 보기 Azure AD 보고를 사용 하는 것입니다.

관리자를 사용할 수 [Azure AD의 조건부 액세스](active-directory-conditional-access.md) 특정 역할에 대 한 액세스 정책을 tooset 합니다. 이러한 정책은 Multi-factor Authentication 또는 장치 요구 사항 tooachieve 액세스 다양 한 경우에도 hello 기업 환경 외부 액세스할 수 있는지 여부를 포함할 수 있습니다.

## <a name="how-can-i-get-started"></a>어떻게 시작하나요?
우선 Azure AD를 아직 사용하지 않는 IT 관리자인 경우입니다.

* [사용해 보기](https://azure.microsoft.com/trial/get-started-active-directory/) - 지금 무료 30일 평가판에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다.

계정에 공유를 사용하는 Azure AD 기능은 다음과 같습니다.

* [그룹 할당](active-directory-accessmanagement-self-service-group-management.md)
* 응용 프로그램 tooAzure AD 추가
* 할당 시작
* 응용 프로그램 할당 FAQ
* [앱 사용 대시보드/보고서](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>자세한 내용을 알아보려면 어떤 정보를 참조해야 하나요?
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [조건부 액세스를 사용한 앱 보호](active-directory-conditional-access.md)
* [셀프 서비스 그룹 관리/SSAA](active-directory-accessmanagement-self-service-group-management.md)

