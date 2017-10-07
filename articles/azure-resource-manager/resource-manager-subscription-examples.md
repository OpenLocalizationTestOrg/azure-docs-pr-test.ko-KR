---
title: "aaaScenarios 구독 거 버 넌 스 예 | Microsoft Docs"
description: "방법의 예제를 제공 tooimplement 일반적인 시나리오에 대 한 구독을 관리 합니다."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Azure 엔터프라이즈 스캐폴드 구현 예제
이 항목에서는 엔터프라이즈에 대 한 hello 권장 사항을 구현 방법의 예는 [Azure enterprise 스 캐 폴드](resource-manager-subscription-governance.md)합니다. 일반적인 시나리오에 대 한 Contoso tooillustrate에 대 한 유용한 정보를 라는 가상의 회사를 사용 합니다.

## <a name="background"></a>백그라운드
Contoso는 고객 "소프트웨어 as a Service" 모델 tooa 패키지에 포함 된 모델에서 모든 항목에 대 한 공급 체인 솔루션을 제공 하는 전 세계 회사 온-프레미스를 배포 합니다.  인도, hello 미국 및 캐나다 상당한 개발 센터와 hello 전세계 소프트웨어를 개발 합니다.

hello ISV 부분 hello 회사의 중요 한 비즈니스에 제품을 관리 하는 여러 독립적인 비즈니스 단위도 구분 됩니다. 각 사업부에는 고유한 개발자, 제품 관리자 및 설계자가 있습니다.

hello 엔터프라이즈 기술 서비스 ETS () 사업부 중앙된 IT 기능을 제공 하 고 비즈니스 단위 응용 프로그램을 호스트 하는 여러 데이터 센터를 관리 합니다. Hello 데이터 센터를 관리, ETS 조직 hello를 제공 하 고 (예: 전자 메일 및 웹 사이트) 중앙 집중식된 공동 작업 및 네트워크/전화 통신 서비스를 관리 합니다. 또한 운영 담당자가 없는 소규모 사업부를 위한 고객 관련 워크로드도 관리합니다.

이 항목에서는 가상 사용자를 다음 hello 사용 됩니다.

* Dave는 hello ETS Azure 관리자입니다.
* Alice는 hello 공급 체인 사업부에서 개발 Director Contoso의 합니다.

Contoso는 고객 지향 앱 toobuild는의 기간 업무 앱에 있어야합니다. Azure에서 toorun hello 앱은 결정 했습니다. Dave 읽고 hello [규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md) 항목 이며 이제 준비 tooimplement hello 권장 사항입니다.

## <a name="scenario-1-line-of-business-application"></a>시나리오 1: 기간 업무 응용 프로그램
Contoso는 hello world에서 개발자가 사용 되는 소스 코드 관리 시스템 (BitBucket) toobe를 만드는 중입니다.  hello 응용 프로그램 서비스 (IaaS) 인프라를 사용 하 여 호스트의 경우 및 웹 서버 및 데이터베이스 서버로 구성 됩니다. 개발자는 개발 환경에서 서버에 액세스 하지만 Azure의 toohello 서버를 액세스 필요 하지 않습니다. Contoso ETS tooallow hello 응용 프로그램 소유자와 팀 toomanage hello 응용 프로그램 하지 않고자 합니다. hello 응용 프로그램은 Contoso의 회사 네트워크에서 사용할 수만 있습니다. Dave이 응용이 프로그램에 대 한 hello 구독을 tooset이 필요합니다. hello 구독은 또한 hello 향후 다른 개발자와 관련 된 소프트웨어를 호스팅합니다.  

### <a name="naming-standards--resource-groups"></a>이름 지정 표준 및 리소스 그룹
Dave 모든 hello 사업부에서 공통 된 toosupport 개발자 도구는 구독을 만듭니다. Hello 구독에 대 한 의미 있는 이름을 toocreate 및 리소스 그룹 (hello 네트워크 hello 응용 프로그램에 대해) 해야 합니다. 그런 다음 구독 및 리소스 그룹을 다음 hello:

| 항목 | 이름 | 설명 |
| --- | --- | --- |
| 구독 |Contoso ETS DeveloperTools Production |일반적인 개발자 도구 지원 |
| 리소스 그룹 |rgBitBucket |Hello 응용 프로그램 웹 서버와 데이터베이스 서버를 포함합니다. |
| 리소스 그룹 |rgCoreNetworks |Hello 가상 네트워크와 사이트 간 게이트웨이 연결을 포함합니다. |

### <a name="role-based-access-control"></a>역할 기반 액세스 제어
그의 구독을 만든 후 Dave가 적절 한 팀 hello tooensure 및 응용 프로그램 소유자가 해당 리소스에 액세스할 수 있습니다. Dave는 팀마다 요구 사항이 서로 다르다는 것을 알게 됩니다. 그는 Contoso의 온-프레미스 AD (Active Directory) tooAzure Active Directory에서에서 동기화 된 hello 그룹을 사용 하 여 고 hello 적절 한 수준으로 액세스 toohello 팀을 제공 합니다.

Dave는 hello 구독에 대 한 역할을 수행 하는 hello를 할당 합니다.

| 역할 | 너무 할당| 설명 |
| --- | --- | --- |
| [소유자](../active-directory/role-based-access-built-in-roles.md#owner) |Contoso AD에서 관리되는 ID |이 ID는 Contoso의 ID 관리 도구를 통해 JIT(Just-in-Time) 액세스로 제어되며 구독 소유자 액세스가 완전히 감사되는지 확인합니다. |
| [보안 관리자](../active-directory/role-based-access-built-in-roles.md#security-manager) |보안 및 위험 관리 부서 |이 역할에는 hello Azure 보안 센터에서 사용자가 toolook와 hello 리소스의 hello 상태 수 있습니다. |
| [네트워크 참여자](../active-directory/role-based-access-built-in-roles.md#network-contributor) |네트워크 팀 |이 역할 Contoso의 네트워크 팀 toomanage hello 사이트 tooSite VPN 있으며이 가상 네트워크를 hello 합니다. |
| *사용자 지정 역할* |응용 프로그램 소유자 |Dave는 hello 리소스 그룹 내의 hello 기능 toomodify 리소스를 부여 하는 역할을 만듭니다. 자세한 내용은 [Azure RBAC에서 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md)을 참조하세요. |

### <a name="policies"></a>정책
Dave는 hello 구독에서 리소스를 관리 하기 위한 요구 사항을 준수 하는 hello에 있습니다.

* Hello 개발 도구 개발자는 hello world 간를 지원 하기 때문에 모든 지역에서 리소스를 만들지 못하도록 tooblock 사용자 않으려면 하지 않습니다. 그러나 tooknow 리소스가 생성 해야 합니다.
* 그는 비용에 대해 고민합니다. 따라서 비용이 많이 드는 불필요 하 게 가상 컴퓨터를 만들지 못하도록 응용 프로그램 소유자 tooprevent 하고자 했습니다.  
* 많은 비즈니스 단위에 개발자가 제공 하는이 응용 프로그램, tootag를 각 리소스를 하고자 했습니다 hello 비즈니스 단위 및 응용 프로그램 소유자와 합니다. 이러한 태그를 사용 하 여 ETS hello 적절 한 팀을 청구할 수 있습니다.

그런 다음 hello 다음 [리소스 관리자 정책](resource-manager-policy.md):

| 필드 | 결과 | 설명 |
| --- | --- | --- |
| 위치 |감사 |모든 지역에서 hello 리소스 감사 hello 만들기 |
| type |deny |G-시리즈 가상 컴퓨터 생성 거부 |
| tags |deny |응용 프로그램 소유자 태그 필요 |
| tags |deny |비용 센터 태그 필요 |
| tags |추가 |태그 이름을 추가 **사업부** 태그 값 및 **ETS** tooall 리소스 |

### <a name="resource-tags"></a>리소스 태그
Dave는 hello BitBucket 구현에 대 한 hello bill tooidentify hello 비용 센터에 대 한 정보를 toohave 야 한다는 것을 이해 합니다. 또한 Dave가 tooknow 모든 hello ETS 소유 하는 리소스입니다.

Hello 다음 추가 [태그](resource-group-using-tags.md) toohello 리소스 그룹 및 리소스.

| 태그 이름 | 태그 값 |
| --- | --- |
| ApplicationOwner |이 응용 프로그램을 관리 하 고 hello 사용자의 hello 이름입니다. |
| CostCenter |hello hello Azure 사용량에 대 한 부담 hello 그룹의 비용 센터 합니다. |
| BusinessUnit |**ETS** (hello 구독과 관련 된 hello 비즈니스 단위) |

### <a name="core-network"></a>핵심 네트워크
정보 보안 및 위험 관리 팀 검토 Dave의 제안 된 Contoso ETS hello toomove hello 응용 프로그램 tooAzure 계획 합니다. Hello 응용 프로그램에는 없는 tooensure 노출 toohello 원하는 인터넷 합니다.  Dave hello 나중에 이동된 tooAzure 수 있는 개발자 응용 프로그램에 있습니다. 이러한 앱에는 공용 인터페이스가 필요합니다.  toomeet 내부 및 외부 가상 네트워크와 네트워크 보안 그룹의 toorestrict 액세스 제공 이러한 요구 사항입니다.

그런 다음 리소스를 다음 hello:

| 리소스 종류 | 이름 | 설명 |
| --- | --- | --- |
| 가상 네트워크 |vnInternal |Hello BitBucket 응용 프로그램을 함께 사용 하 고 ExpressRoute tooContoso 회사 네트워크를 통해 연결 되어 있습니다.  서브넷 (sbBitBucket) 특정 IP 주소 공간으로 hello 응용 프로그램을 제공합니다. |
| 가상 네트워크 |vnExternal |공용 끝점이 필요한 향후 응용 프로그램에 사용 가능합니다. |
| 네트워크 보안 그룹 |nsgBitBucket |해당 hello를 사용 하면 hello 응용 프로그램 (sbBitBucket) 거주 hello 서브넷에 대 한 포트 443에 대해서만 연결을 허용 하 여이 작업의 공격 노출 영역 최소화 됩니다. |

### <a name="resource-locks"></a>리소스 잠금
Dave 인식 Contoso의 회사 네트워크 toohello 내부 가상 네트워크에서 hello 연결에서 불규칙 스크립트 또는 실수로 삭제 되는 보호 되어야 합니다.

그런 다음 hello 다음 [리소스 잠금](resource-group-lock-resources.md):

| 잠금 유형 | 리소스 | 설명 |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |삭제 hello 가상 네트워크 또는 서브넷에서 사용자가 방지 하지만 새 서브넷의 hello 추가 방지 하지 않습니다. |

### <a name="azure-automation"></a>Azure Automation
Dave 영향을 주지 tooautomate이 응용이 프로그램에 대 한 합니다. Azure Automation 계정을 만들기는 했지만 아예 사용하지 않습니다.

### <a name="azure-security-center"></a>Azure 보안 센터
Contoso IT 서비스 관리 요구 tooquickly 식별 하 고 위협 요소를 처리 합니다. 또한 있을 수 있는 문제 toounderstand 합니다.  

toofulfill 이러한 요구 사항, Dave 사용 hello [Azure 보안 센터](../security-center/security-center-intro.md), 액세스 toohello 보안 관리자 역할을 제공 합니다.

## <a name="scenario-2-customer-facing-app"></a>시나리오 2: 고객에게 표시되는 앱
hello 경영진 hello 공급 체인 사업부의 충성도 카드를 사용 하 여 다양 한 기회 tooincrease 커뮤니케이션: Contoso의 식별 했습니다. Alice의 팀이 응용이 프로그램을 만들어야 하 고 Azure의 기능 toomeet 증가 한다는 결정 hello 비즈니스 요구 사항입니다. Alice Dave ETS tooconfigure 두 개의 구독을 개발 하 고 작동 하는이 응용 프로그램에서 작동 합니다.

### <a name="azure-subscriptions"></a>Azure 구독
Dave는 toohello Azure Enterprise Portal에 로그인 하 고 해당 hello 공급 체인 부서 이미 표시 합니다.  그러나이 프로젝트는 Azure의 hello 공급 체인 팀에 대 한 첫 번째 개발 프로젝트 hello Dave Alice의 개발 팀에 대 한 새 계정에 대 한 hello 필요성을 인식 합니다.  그 그녀의 팀에 대 한 hello "r&d" 계정을 만들고 액세스 tooAlice를 할당 합니다. Alice hello Azure 포털을 통해 로그인 하 고 두 개의 구독을 만듭니다: 하나의 toohold hello 개발 서버와 하나의 toohold hello 프로덕션 서버.  그녀 hello 다음 구독을 만들 때 이전에 설정 하는 hello 명명 표준을 따릅니다.

| 구독 용도 | 이름 |
| --- | --- |
| 개발 |SupplyChain ResearchDevelopment LoyaltyCard Development |
| 프로덕션 |SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>정책
Dave 및 Alice hello 응용 프로그램에 설명 하 고이 응용 프로그램에만 hello 북미 지역에 고객 역할을 식별 합니다.  Alice와 그녀의 팀 toouse Azure의 응용 프로그램 서비스 환경 및 Azure SQL toocreate hello 응용 프로그램을 계획합니다. 개발 중 toocreate 가상 컴퓨터를 할 수 있습니다.  Alice가 그녀의 개발자는 tooexplore 필요 하며 ETS 끌어와서 없이 문제를 확인 하는 hello 리소스가 있는 tooensure 합니다.

Hello에 대 한 **개발 구독**, 정책에 따라 hello를 만듭니다.

| 필드 | 결과 | 설명 |
| --- | --- | --- |
| 위치 |감사 |모든 지역에서 hello 리소스 hello 만들기를 감사 합니다. |

Hello 유형의 sku 개발 중 이며 사용자가 만들 수를 제한 하지 않습니다 하 고 모든 리소스 그룹 또는 리소스에 대 한 태그가 필요 하지 않습니다.

Hello에 대 한 **프로덕션 구독**, 다음 정책 hello를 만듭니다.

| 필드 | 결과 | 설명 |
| --- | --- | --- |
| 위치 |deny |미국 hello 데이터 센터 외부의 리소스 hello 생성을 거부 합니다. |
| tags |deny |응용 프로그램 소유자 태그 필요 |
| tags |deny |부서 태그가 필요합니다. |
| tags |추가 |프로덕션 환경을 나타내는 태그 tooeach 리소스 그룹을 추가 합니다. |

Hello 유형의 sku 프로덕션 환경에서 사용자가 만들 수는 제한 하지 않습니다.

### <a name="resource-tags"></a>리소스 태그
Dave 대금 청구 및 소유권에 대 한 특정 정보 tooidentify hello 올바른 비즈니스 그룹 toohave 야 한다는 것을 이해 합니다. 리소스 그룹 및 리소스에 대한 리소스 태그를 정의합니다.

| 태그 이름 | 태그 값 |
| --- | --- |
| ApplicationOwner |이 응용 프로그램을 관리 하 고 hello 사용자의 hello 이름입니다. |
| department |hello hello Azure 사용량에 대 한 부담 hello 그룹의 비용 센터 합니다. |
| EnvironmentType |**프로덕션** (hello 구독에 포함 되어 있지만 **프로덕션** hello 이름에이 태그를 포함 하 여 사용 하면 쉽게 식별할 수 있도록 hello 포털에서 또는 hello bill의 리소스를 찾을 때.) |

### <a name="core-networks"></a>코어 네트워크
정보 보안 및 위험 관리 팀 검토 Dave의 제안 된 Contoso ETS hello toomove hello 응용 프로그램 tooAzure 계획 합니다. 원하는 충성도 카드 응용 프로그램 hello tooensure 제대로 분리 및 DMZ 네트워크에 보호 합니다.  toofulfill이 요구이 사항을 Dave 및 Alice 외부 가상 네트워크 및 네트워크 보안 그룹 tooisolate hello 충성도 카드 응용 프로그램에서에서 만들기 hello Contoso 회사 네트워크  

Hello에 대 한 **개발 구독**를 만듭니다.

| 리소스 종류 | 이름 | 설명 |
| --- | --- | --- |
| 가상 네트워크 |vnInternal |Hello Contoso 충성도 카드 개발 환경을 사용 하 고 ExpressRoute tooContoso 회사 네트워크를 통해 연결 됩니다. |

Hello에 대 한 **프로덕션 구독**를 만듭니다.

| 리소스 종류 | 이름 | 설명 |
| --- | --- | --- |
| 가상 네트워크 |vnExternal |Hello 충성도 카드 응용 프로그램을 호스트 하 고 tooContoso의 ExpressRoute 직접 연결 되어 있지 않습니다. 코드의 소스 코드 시스템을 통해 푸시됩니다 직접 toohello PaaS 서비스입니다. |
| 네트워크 보안 그룹 |nsgBitBucket |해당 hello를 사용 하면만 TCP 443에서 인바운드 통신을 허용 하 여이 작업의 공격 노출 영역 최소화 됩니다.  Contoso는 또한 추가 보호를 위해 웹 응용 프로그램 방화벽을 사용하여 조사 중입니다. |

### <a name="resource-locks"></a>리소스 잠금
Dave과 alice가 제공 하 고 hello hello 환경 tooprevent 실수로 삭제 되는 잘못 된 코드 푸시 중에 주요 리소스 중 일부에 대해 tooadd 리소스 잠금을 결정 합니다.

Lock 뒤 hello 만들:

| 잠금 유형 | 리소스 | 설명 |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |tooprevent 사람에서 hello 가상 네트워크 또는 서브넷을 삭제 합니다. hello 잠금 새 서브넷의 hello 추가 방해 되지는 않습니다. |

### <a name="azure-automation"></a>Azure Automation
Alice와 그녀가 속한 개발 팀에는이 응용 프로그램에 대 한 광범위 한 runbook toomanage hello 환경이 제공 됩니다. hello runbook hello 응용 프로그램에 대 한 노드의 hello 추가/삭제 및 기타 DevOps 작업에 대 한 허용합니다.

toouse 통해 이러한 runbook [자동화](../automation/automation-intro.md)합니다.

### <a name="azure-security-center"></a>Azure 보안 센터
Contoso IT 서비스 관리 요구 tooquickly 식별 하 고 위협 요소를 처리 합니다. 또한 있을 수 있는 문제 toounderstand 합니다.  

toofulfill Dave 이러한 요구 사항을 Azure 보안 센터를 사용 하도록 설정 합니다. 그 hello Azure 보안 센터는 hello 리소스를 모니터링 하 고 액세스할 수 toohello DevOps 및 보안 팀을 확인 합니다.

## <a name="next-steps"></a>다음 단계
* 리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](resource-manager-template-best-practices.md)합니다.

