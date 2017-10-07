---
title: "기업에서는 tooAzure 이동에 대 한 aaaBest 사례 | Microsoft Docs"
description: "기업에서는 tooensure 안전 하 고 관리할 수 있는 환경을 사용할 수 있는 스 캐 폴드를 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스
점점 더 기업에는 유연성과 민첩성 hello 공용 클라우드 채택 하는 합니다. 이러한 hello 클라우드 장점 toogenerate 수익을 활용 하는 또는 hello 비즈니스에 대 한 리소스를 최적화 합니다. Microsoft Azure는 다양 한 작업 및 응용 프로그램 기업 빌딩 블록 tooaddress 같은 어셈블할 수 다양 한 서비스를 제공 합니다. 

그러나 toobegin 어려운 방식은 알아야 합니다. Azure toouse를 결정 한 후 몇 가지 질문 일반적으로 발생 합니다.

* "특정 국가에서 데이터 독립성에 대한 법률 요구 사항을 충족하려면 어떻게 해야 하나요?"
* "누군가가 중요한 시스템을 실수로 변경하지 않도록 보장하려면 어떻게 해야 하나요?"
* "내역을 확인하고 정확하게 청구할 수 있도록 모든 리소스가 지원하는 내용을 어떻게 파악하나요?"

와 없는 가드 레일 빈 구독의 hello 잠재 하기가 어려워집니다. 이 빈 공간 이동 tooAzure 방해가 될 수 있습니다.

이 문서는 관리 및 민첩성을 위해 필요한 hello와 균형에 대 한 기술 전문가 tooaddress hello 요구 시작점을 제공 합니다. 구현 및 관리 Azure 구독 내 조직을 안내 하는 엔터프라이즈 스 캐 폴드의 hello 개념을 소개 합니다. 

## <a name="need-for-governance"></a>관리 필요성
TooAzure를 이동할 때 거 버 넌 스 초기 tooensure hello 성공적으로 사용 hello 클라우드 hello 엔터프라이즈 내에서 hello 항목을 해결 해야 합니다. 그러나 hello 시간과 포괄적인 거 버 넌 스 시스템을 만드는 아니라 관료 주의가 일부 비즈니스 그룹 이동 직접 toovendors 엔터프라이즈 IT를 포함 하지 않는 의미 합니다. 이 방법은 수 hello 리소스 제대로 관리 되지 않는 경우 hello 엔터프라이즈 열려 toovulnerabilities를 하지 않습니다. -민첩성, 유연성 및 소비 기반 가격 책정-공용 클라우드 hello의 hello 특성은 tooquickly 있어야 하는 toobusiness 그룹 (내부 및 외부) 고객의 hello 요구를 충족 중요 합니다. 하지만 엔터프라이즈 IT tooensure는 데이터와 시스템은 효과적으로 보호 해야 합니다.

실제 환경에서 스 캐 폴딩이 hello 구조의 사용 되는 toocreate hello 기초가 됩니다. hello 스 캐 폴드 hello 일반적인 개요를 안내 하 고 탑재 더 영구적인 시스템 toobe 앵커 지점을 제공 합니다. 엔터프라이즈 scaffold 동일 hello은: 하는 유연한 제어 및 hello 공용 클라우드 기반 서비스에 대 한 구조 toohello 환경과 앵커를 제공 하는 Azure 기능 집합이 있습니다. Hello 작성기를 제공 (IT 및 비즈니스 그룹) foundation toocreate 및 새로운 서비스를 연결 합니다.

hello 스 캐 폴드 많은 고객 참여를 통해 클라이언트와 다양 한 크기의에서 수집 하는 사례를 기반으로 합니다. 이러한 클라이언트는 hello 클라우드 tooFortune 500 기업과 마이그레이션 및 hello 클라우드에서 솔루션을 개발 하는 독립 소프트웨어 공급 업체에서 솔루션을 개발 하는 소규모 조직이 이르기까지 다양 합니다. hello 엔터프라이즈 스 캐 폴드가 "현실화" toobe 유연한 toosupport 기존의 IT 워크 로드와 민첩 한 작업입니다. 와 같은 소프트웨어-as a service (SaaS) 응용 프로그램을 만드는 개발자는 Azure 기능에 기반 합니다.

hello 엔터프라이즈 스 캐 폴드 Azure 내에서 각각의 새 구독의 의도 한 toobe hello 기반입니다. 조직의 관리자 tooensure 작업 충족 hello 최소 거 버 넌 스 요구를 비즈니스 그룹 및 개발자가에서 신속 하 게 자신의 목표를 충족 하면서 수 있습니다.

> [!IMPORTANT]
> 거 버 넌 스는 Azure의 중요 한 toohello success입니다. 이 문서의 대상은 hello 엔터프라이즈 scaffold의 기술적인 구현을 지만 hello 광범위 한 프로세스 및 hello 구성 요소 간의 관계에 대해서만 다룹니다. 정책 거 버 넌 스 hello 위에서 아래로 흐르고 어떤 hello 하 여 비즈니스가 tooachieve 결정 됩니다. Azure에 대 한 거 버 넌 스 모델 hello 만들기 담당자가를 포함 하는 물론 IT에 더욱 중요 한 비즈니스 그룹, 부 및 보안 및 위험 관리에서 강력한 표현이 있어야 하지만 합니다. Hello 끝은 조직의 업무 및 목표 비즈니스 위험 toofacilitate 완화 하는 방법에 대 한 엔터프라이즈 scaffold가입니다.
> 
> 

다음 이미지는 hello hello 스 캐 폴드의 hello 구성 요소를 설명 합니다. hello foundation 부서, 계정 및 구독에 대 한 단색 계획에 의존합니다. 리소스 관리자 정책 및 강력한 이름 지정 표준을 hello 독특하고 구성 됩니다. hello 스 캐 폴드 hello 나머지 Azure 기능 코어에서 온 것 이며 안전 하 고 관리할 수 있는 환경을 수 있도록 하는 기능입니다.

![스캐폴드 구성 요소](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure는 2008년에 도입된 이후로 급속도로 확장되었습니다. 이러한 증가 Microsoft 엔지니어링 팀이 서비스 배포 및 관리 하기 위한 접근 방식도 toorethink 필요 합니다. hello Azure 리소스 관리자 모델 2014에서 도입 되었으며 hello 클래식 배포 모델을 대체 합니다. 리소스 관리자는 조직을 toomore 쉽게 배포, 구성 및 Azure 리소스를 제어할 수 있습니다. Resource Manager에는 복잡하고 상호 종속적인 솔루션의 신속한 배포를 위한 리소스를 만들 때 유용한 병렬 처리가 포함됩니다. 세분화 된 액세스 제어 및 메타 데이터를 사용 하 여 hello 기능 tootag 리소스에도 포함 되어 있습니다. Hello 리소스 관리자 모델을 통해 모든 리소스를 만들어야 하는 것이 좋습니다. hello 엔터프라이즈 스 캐 폴드 hello 리소스 관리자 모델에 대 한 명시적으로 설계 되었습니다.
> 
> 

## <a name="define-your-hierarchy"></a>계층 구조 정의
hello 스 캐 폴드의 hello foundation이입니다 hello Azure Enterprise 등록 (Enterprise Portal hello). hello 기업 등록 계약 hello 셰이프를 정의 및 회사 내에서 Azure 서비스의 사용 하 여 hello 코어 거 버 넌 스 구조입니다. Hello 기업 계약 내에서 고객은 수 toofurther hello 환경을 부서, 계정 및 구독을 마지막으로 세분화 됩니다. Azure 구독 리소스를 모두 포함 된 hello 기본 단위입니다. 코어 수, 리소스 등 Azure 내에서 여러 가지 한도도 정의합니다.

![계층 구조](./media/resource-manager-subscription-governance/agreement.png)

모든 기업의 다른 이며 보다 유연 하 게 hello 회사 내에서 Azure는 구성 하는 방법에 대 한 hello 이전 이미지의 hello 계층 구조를 허용 합니다. 이 문서에 포함 된 hello 지침을 구현 하기 전에 계층 구조를 모델링 하 고 청구, 리소스 액세스 및 복잡성에 대 한 hello 영향 이해 해야 합니다.

Azure 등록에 대 한 hello 세 가지 일반적인 패턴은:

* hello **기능** 패턴
  
    ![functional](./media/resource-manager-subscription-governance/functional.png)
* hello **사업부** 패턴 
  
    ![비즈니스](./media/resource-manager-subscription-governance/business.png)
* hello **지리적** 패턴
  
    ![지리적](./media/resource-manager-subscription-governance/geographic.png)

Hello scaffold hello 구독 수준 tooextend hello 거 버 넌 스 요구 사항이 hello enterprise에 hello 구독에 적용 합니다.

## <a name="naming-standards"></a>이름 지정 표준
hello 스 캐 폴드의 첫 번째 원칙은 hello 표준 이름을 지정 하면 됩니다. 잘 디자인 된 명명 표준 hello 포털은 청구서에 이나 스크립트 내에서 tooidentify 리소스를 사용 합니다. 대부분의 경우 온-프레미스 인프라에 대한 이름 지정 표준이 이미 있습니다. Azure tooyour 환경에 추가할 때는 표준 tooyour Azure 리소스 이름을 지정 하는 것를 확장 해야 합니다. 모든 수준에서 hello 환경의 보다 효율적인 관리를 용이 하 게 명명 표준을 합니다.

> [!TIP]
> 명명 규칙:
> * 검토 하 고 가능한 경우 채택 hello [패턴 및 실습 지침](../guidance/guidance-naming-conventions.md)합니다. 이 설명서를 통해 의미 있는 이름 지정 표준을 결정할 수 있습니다.
> * 리소스 이름에 camelCasing을 사용합니다(예: myResourceGroup 및 vnetNetworkName). 참고: 있습니다, 저장소 계정 등의 특정 리소스 hello 옵션만 toouse 소문자 (및 다른 특수 문자)입니다.
> * Azure 리소스 관리자 (hello 다음 섹션에서 설명) 정책 tooenforce 명명 표준을 사용 하는 것이 좋습니다.
> 
> hello 이전 팁 유용 일관성 있는 명명 규칙을 구현 합니다.

## <a name="policies-and-auditing"></a>정책 및 감사
hello 스 캐 폴드의 두 번째 pillar hello 만들어야 [Azure 리소스 관리자 정책](resource-manager-policy.md) 및 [hello 활동 로그 감사](resource-group-audit.md)합니다. 리소스 관리자 정책을 Azure의 hello 기능 toomanage 위험을 제공합니다. 특정 작업을 제한, 적용 또는 감사하여 데이터 독립성을 보장하는 정책을 정의할 수 있습니다. 

* 정책은 시스템을 **허용하는** 기본값입니다. 정의 하 고 거부 또는 리소스에 대 한 작업을 감사 하는 정책을 tooresources 할당 하 여 동작을 제어 합니다.
* 정책은 정책 정의 언어(if-then 조건)로 된 정책 정의에 의해 설명됩니다.
* JSON(Javascript Object Notation) 형식 파일로 정책을 만듭니다. 정책을 정의한 후 할당 하 여 특정 범위 tooa: 구독, 리소스 그룹 또는 리소스입니다.

정책에는 세분화 된 접근 방식 tooyour 시나리오에 대 한 허용 하는 여러 작업이 있습니다. hello 동작은 다음과 같습니다.

* **거부**: 블록 hello 리소스 요청
* **감사**: hello 요청을 한 줄 toohello 활동 로그 (사용 되는 tooprovide 경고나 tootrigger runbook 일 수 있음) 추가 허용
* **추가**: 추가 정보 toohello 리소스를 지정 합니다. 예를 들어 리소스에 "CostCenter" 태그가 없는 경우 해당 태그를 기본값과 함께 추가합니다.

### <a name="common-uses-of-resource-manager-policies"></a>Resource Manager 정책의 일반적인 사용
Azure 리소스 관리자 정책은 hello Azure 도구 키트의에서 강력한 도구입니다. 사용 하면 tooavoid 예상치 못한 비용, tooidentify를 비용 센터 tooensure 및 태그 지정을 통해 리소스에 대 한 요구 사항이 충족 되는 준수 합니다. 정책 hello 기본 제공 감사 기능이 결합 되 면 복잡 하 고 유연한 솔루션으로 수 있습니다. 정책을 통해 회사 "기존의 IT" 작업 및 "Agile" 워크 로드; tooprovide 컨트롤 와 같은 사용자 지정 응용 프로그램을 개발합니다. 정책에 대 한 표시 하는 hello 가장 일반적인 패턴은:

* **지역-준수/데이터 sovereignty** -Azure hello 전 세계 지역에서 제공 합니다. 기업에서는 종종 toocontrol 판독기 (tooensure 데이터 sovereignty tooensure 리소스만 생성 되는 또는 hello 리소스의 닫기 toohello 최종 사용자) 여부 리소스가 생성 되는 위치.
* **비용 관리** - Azure 구독에는 다양한 유형과 규모의 리소스가 포함될 수 있습니다. 기업에서는 주로 원하는 tooensure 표준에 구독 수백 달러 한 달 이상이 소요 될 수 있습니다는 불필요 하 게 큰 리소스를 사용 하지 마십시오.
* **거 버 넌 스 필요한 태그를 통해 기본** -hello 가장 일반적인 및 높은 원하는 기능 중 하나는 태그를 요구 합니다. 기업에 수 tooensure 리소스 태그가 적절 하 게 지정 되는 Azure 리소스 관리자 정책을 사용 하 여 합니다. hello 가장 일반적인 태그는: 부서, 리소스 소유자 및 환경 형식 (예: 프로덕션, 테스트, 개발)

**예**

LOB(기간 업무) 응용 프로그램에 대한 "기존의 IT" 구독

* 모든 리소스에 부서 및 소유자 태그 적용
* 리소스 만들기 toohello 북미 지역 제한
* Hello 기능 toocreate G 시리즈 Vm 및 HDInsight 클러스터를 제한 합니다.

클라우드 응용 프로그램을 만드는 사업부를 위한 "기민한" 환경

* 리소스의 hello 만들 수 있는 toomeet 데이터 sovereignty 요구 사항, 특정 지역에만 합니다.
* 모든 리소스에서 환경 태그를 적용합니다. 리소스 태그 없이 만든 경우 추가 hello **환경: 알 수 없는** toohello 리소스 태그를 지정 합니다.
* 리소스가 북아메리카 외부에 생성되지만 방지하지 않은 경우 감사합니다.
* 비용이 높은 리소스가 생성된 경우 감사합니다.

> [!TIP]
> hello 조직 전체에서 리소스 관리자 정책의 가장 일반적인 사용은 toocontrol *여기서* 리소스를 만들 수 있습니다 및 *어떤* 유형의 리소스를 만들 수 있습니다. 또한 tooproviding 컨트롤에 *여기서* 및 *어떤*, 많은 기업 사용 하 여 정책을 tooensure 리소스 소비에 대 한 다시 hello 적절 한 메타 데이터 toobill에는 합니다. 에 대 한 hello 구독 수준에서 정책을 적용 하는 것이 좋습니다.
> 
> * 지리적 규정 준수/데이터 독립성
> * 비용 관리
> * 필수 태그(청구 대상, 응용 프로그램 소유자 등 비즈니스 요구에 따라 결정)
> 
> 하위 범위 수준에서 추가 정책을 적용할 수 있습니다.
> 
> 

### <a name="audit---what-happened"></a>감사 - 변경된 내용
환경을 작동 방식을 tooview, tooaudit 사용자 작업이 필요 합니다. Azure 내에서 대부분의 리소스 유형은 로그 도구 또는 Azure Operations Management Suite 내에서 분석할 수 있는 진단 로그를 생성합니다. 엔터프라이즈 보기 또는 부서는 여러 구독 tooprovide 간에 활동 로그를 수집할 수 있습니다. 감사 레코드는 중요 한 진단 도구와 hello Azure 환경에서에서 중요 한 메커니즘 tootrigger 이벤트 됩니다.

리소스 관리자 배포에서 작업 로그 사용 toodetermine hello **작업** 위치와 수행한 사람 하는 데 걸린 합니다. 활동 로그는 Log Analytics와 같은 도구를 사용하여 수집 및 집계할 수 있습니다.

## <a name="resource-tags"></a>리소스 태그
조직의 사용자가 리소스 toohello 구독을 추가한 hello 적절 한 부서, 고객 및 환경을 사용 하 여 점점 더 중요 해 tooassociate 리소스 됩니다. 통해 메타 데이터 tooresources 첨부할 수 [태그](resource-group-using-tags.md)합니다. Hello 리소스 또는 hello 소유자에 대 한 태그 tooprovide 정보를 사용 합니다. 태그는 toonot만 집계 하 고 다양 한 방법으로 리소스 그룹을 사용 하면 하지만 비용 정산의 hello 목적을 위해 해당 데이터를 사용 합니다. Too15 키: 값 쌍을 사용 하 여 리소스 태그를 지정할 수 있습니다. 

리소스 태그는 유연 하와 연결 된 toomost 리소스 여야 합니다. 일반적인 리소스 태그의 예는 다음과 같습니다.

* 청구 대상
* 부서(또는 사업부)
* 환경(프로덕션, 준비, 개발)
* 계층(웹 계층, 응용 프로그램 계층)
* 응용 프로그램 소유자
* ProjectName

![tags](./media/resource-manager-subscription-governance/resource-group-tagging.png)

태그에 대한 더 많은 예는 [Azure 리소스에 대한 권장되는 명명 규칙](../guidance/guidance-naming-conventions.md)을 참조하세요.

> [!TIP]
> 다음에 대한 태그 지정을 규정하는 정책을 만드는 것이 좋습니다.
> 
> * 리소스 그룹
> * 저장소
> * 가상 컴퓨터
> * 응용 프로그램 서비스 환경/웹 서버
> 
> 이 태그 전략 hello 비즈니스 "," finance "," 보안 "," 위험 관리 "및" hello 환경의 전체 관리에 필요한 메타 데이터에 구독 전반에 걸쳐 식별 합니다. 

## <a name="resource-group"></a>리소스 그룹
리소스 관리자에 사용할 수 있게 하면 tooput 리소스 관리, 청구, 또는 자연 선호도 대 한 의미 있는 그룹입니다. 앞서 설명했듯이, Azure에는 두 가지 배포 모델이 있습니다. Hello에 이전 버전의 기본 모델, 관리의 기본 단위 hello hello 구독 했습니다. 많은 구독 toohello 만들기를 초래한 구독 내에서 리소스 아래로 어려운 toobreak 있었습니다. Hello 리소스 관리자, 모델로 hello 소개를 리소스 그룹에 대해 살펴보았습니다. 리소스 그룹은 공통 수명 주기를 포함하고 "모든 SQL Server" 또는 "응용 프로그램 A"와 같은 특성을 공유하는 리소스 컨테이너입니다.

리소스 그룹은 서로 포함 될 수 없습니다 및 리소스 tooone 리소스 그룹에만 속할 수 있습니다. 리소스 그룹의 모든 리소스에 특정 작업을 적용할 수 있습니다. 예를 들어, 리소스 그룹을 삭제 하면 hello 리소스 그룹 내에서 모든 리소스를 제거 합니다. Hello에 전체 응용 프로그램 또는 관련된 시스템 배치 되는 일반적으로 동일한 리소스 그룹입니다. Hello 웹 서버, 응용 프로그램 서버 및 SQL server hello에 Contoso 웹 응용 프로그램 라는 3 계층 응용 프로그램은 포함 하는 예를 들어 동일한 리소스 그룹입니다.

> [!TIP]
> 리소스 그룹을 구성 하는 방법을 다를 수 있습니다 "기존의 IT" 워크 로드에서 너무 "Agile IT" 워크 로드:
> 
> * "기존 IT" 작업 hello 내에서 항목에 의해 가장 일반적으로 그룹화 되는 응용 프로그램과 같이 동일한 수명 주기 합니다. 응용 프로그램별 그룹화를 통해 개별 응용 프로그램 관리가 가능합니다.
> * "Agile IT" 워크 로드는 외부 고객 관련 클라우드 응용 프로그램에서 toofocus 경향이 있습니다. hello 리소스 그룹 배포 (예: 응용 프로그램 계층 웹 계층)의 hello 레이어를 반영 해야 및 관리 합니다.
> 
> 워크로드를 이해하면 리소스 그룹 전략을 개발하는 데 도움이 됩니다.

## <a name="role-based-access-control"></a>역할 기반 액세스 제어
아마도 확인 하려는 사용자가 직접 "tooresources 액세스 해야 하는 사용자?" "이 액세스를 어떻게 제어할 수 있는가?"라는 의문이 들 수 있습니다. 허용 또는 액세스 toohello Azure 포털을 허용 하지 않고 및 hello 포털에서 tooresources 액세스 제어는 중요 합니다. 

액세스 제어 tooa 구독 된 기본 Azure 처음 릴리스 되었을 때: 관리자 또는 공동 관리자입니다. Tooa 구독 hello 포털 hello 기본 사용 권한에 포함 된 모델 액세스 tooall hello 리소스에 액세스 합니다. 세분화 된 제어가이 처럼 Azure 등록에 대 한 구독 tooprovide 적절 한 액세스 제어의 수준 toohello 확산 led.

이제 더 이상 구독 수를 늘리지 않아도 됩니다. 역할 기반 액세스 제어를 사용한 toostandard 역할 (예: 일반적인 "reader" 및 "writer" 유형의 역할) 사용자에 게 할당할 수 있습니다. 사용자 지정 역할을 정의할 수도 있습니다.

> [!TIP]
> tooimplement 역할 기반 액세스 제어:
> * AD Connect 도구 hello에 회사 id 저장소 (가장 일반적으로 Active Directory) tooAzure Active Directory를 사용 하 여 연결 합니다.
> * Hello 관리자/공동 관리자는 관리 되는 id를 사용 하 여 구독을 제어 합니다. **안 함** 관리자/공동 관리자 tooa 새 구독 소유자를 할당 합니다. 대신 역할 tooprovide RBAC를 사용 하 여 **소유자** 권한 tooa 그룹 또는 개별 합니다.
> * Active Directory에서 Azure 사용자 tooa 그룹 (예: 응용 프로그램 X 소유자)을 추가 합니다. Hello 동기화 된 그룹 tooprovide 그룹 구성원 hello 적절 한 권한이 toomanage hello 리소스 그룹을 사용 hello 응용 프로그램을 포함 합니다.
> * Hello 부여 원칙을 따르며 hello **최소 권한** 필요한 toodo hello 작업을 예상 합니다. 예:
>   * 배포 그룹: 수 toodeploy 리소스만 포함 된 그룹입니다.
>   * 가상 컴퓨터 관리: A Vm을 그룹화 즉 수 toorestart (작업용)
> 
> 이러한 팁은 구독에서 사용자 액세스를 관리하는 데 도움이 됩니다.

## <a name="azure-resource-locks"></a>Azure 리소스 잠금
Core 서비스 toohello 구독에 추가 하는 조직에 이러한 서비스에 사용할 수 있는 tooavoid 비즈니스 중단도 점점 더 중요 해 tooensure 됩니다. [리소스 잠금을](resource-group-lock-resources.md) 수정 하거나 삭제 응용 프로그램 또는 클라우드 인프라에 상당한 영향을 미칠 것 여기서 중요 리소스에 toorestrict 작업을 활성화 합니다. 잠금 tooa 구독, 리소스 그룹 또는 리소스를 적용할 수 있습니다. 일반적으로 가상 네트워크, 게이트웨이 및 저장소 계정 등의 잠금 toofoundational 리소스를 적용 합니다. 

리소스 잠금은 현재 두 가지 값(CanNotDelete 및 ReadOnly)을 지원합니다. 로그인 한 사용자 (hello 적절 한) 할 수 있다는 CanNotDelete 읽을 또는 리소스 수정 있지만 삭제할 수 없습니다. ReadOnly는 권한이 있는 사용자가 리소스를 삭제 또는 수정할 수 없음을 의미합니다.

관리 잠금 toocreate 또는 delete 권한이 너무`Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 동작 합니다.
Hello 기본 제공 역할의 소유자 및 사용자 액세스 관리자에 게 이러한 작업을 부여 됩니다.

> [!TIP]
> 핵심 네트워크 옵션은 잠금으로 보호되어야 합니다. 사이트 간 VPN 게이트웨이 실수로 삭제 되는 것은 매우 위험 tooan Azure 구독 것입니다. Azure 가상 네트워크를 사용 중인 toodelete 허용 하지 않습니다 되지만 추가 제한을 적용 하는 것은 유용 예방 합니다. 
> 
> * 가상 네트워크: CanNotDelete
> * 네트워크 보안 그룹: CanNotDelete
> * 정책: CanNotDelete
> 
> 정책은 중요 한 toohello 적절 한 제어 유지 관리 됩니다. 적용 하는 것이 좋습니다는 **CanNotDelete** toopolices 사용 중인 잠금.

## <a name="core-networking-resources"></a>핵심 네트워킹 리소스
내부 (내 hello 회사의 네트워크) 또는 외부 액세스 tooresources 될 수 있습니다 (을 통해 인터넷 hello). 사용자가 조직 tooinadvertently put 리소스 hello 잘못 된 위치에 사용 되며 잠재적 열지 toomalicious 액세스 합니다. 온-프레미스 장치에서와 마찬가지로 기업은 Azure 사용자 hello 올바른 결정을 확인 하는 적절 한 컨트롤 tooensure를 추가 해야 합니다. 구독 관리를 위해 기본적인 액세스 제어를 제공하는 핵심 리소스를 식별합니다. hello 코어 리소스는 다음으로 구성 됩니다.

* **가상 네트워크**는 서브넷에 대한 컨테이너 개체입니다. 경우에 반드시 필요 하지 응용 프로그램 toointernal 회사 리소스에 연결할 때 주로 사용 됩니다.
* **네트워크 보안 그룹** 비슷한 tooa 방화벽은과 hello 네트워크를 통해 어떻게 리소스 수와 "통신"에 대 한 규칙을 제공 합니다. 서브넷 (또는 가상 컴퓨터) toohello 인터넷 또는 다른 서브넷에 연결할 수 있는 경우 동일한 hello / 방법 보다 세부적으로 제어를 제공 합니다. 이러한 가상 네트워크입니다.

![핵심 네트워킹](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> 네트워킹:
> * 가상 네트워크 전용된 tooexternal 연결 작업이 및 인트라넷 연결 작업을 만듭니다. 이 방법은 외부 웹 공간에 내부 작업을 위해 설계 된 가상 컴퓨터를 배치 실수로 hello 가능성이 줄어듭니다.
> * 네트워크 보안 그룹 toolimit 액세스를 구성 합니다. 여기에 최소한 액세스 toohello 차단 내부 가상 네트워크와 외부 가상 네트워크에서 블록 액세스 toohello 회사 네트워크에서 인터넷 합니다.
> 
> 이러한 팁은 보안 네트워킹 리소스를 구현하는 데 도움이 됩니다.

### <a name="automation"></a>Automation
리소스를 개별적으로 관리하는 것은 시간이 많이 소요될 뿐만 아니라 특정 작업에 대해 오류가 발생하기 쉽습니다. Azure에서는 Azure Automation, Logic Apps, Azure Functions를 비롯한 다양한 자동화 기능을 제공합니다. [Azure 자동화](../automation/automation-intro.md) 관리자 toocreate 있으며 특정 리소스 관리에서 runbook toohandle 일반적인 작업을 정의 합니다. PowerShell 코드 편집기 또는 그래픽 편집기를 사용하여 runbook을 만듭니다. 복잡한 다단계 워크플로를 생성할 수 있습니다. Azure 자동화는 사용 되지 않는 리소스를 종료 하거나 사용자의 개입 없이 tooa 특정 트리거가 응답에 리소스를 만드는 등의 일반적인 작업 toohandle 사용 되는 경우가 많습니다.

> [!TIP]
> Automation:
> * Azure 자동화 계정을 만들고 hello 사용 가능한 runbook (그래픽 및 명령 줄) hello에서 사용할 수 있는 검토 [Runbook 갤러리](../automation/automation-runbook-gallery.md)합니다.
> * 사용자 용도에 따라 핵심 runbook을 가져오고 사용자 지정합니다.
> 
> 일반적인 시나리오는 일정에 따라 hello tooStart/종료 가상 컴퓨터를 수 있습니다. 모두이 시나리오를 처리 하 고 방법을 설명 하는 hello 갤러리에서에서 사용할 수 있는 예제 runbook tooexpand 것입니다.
> 
> 

## <a name="azure-security-center"></a>Azure 보안 센터
아마도 가장 큰 블로 커가 toocloud 채택 hello 중 하나는 되었습니다 hello 문제 보안을 통해. IT 위험 관리자와 보안 부서 tooensure Azure의 리소스에에서 안전 하다는 필요 합니다. 

hello [Azure 보안 센터](../security-center/security-center-intro.md) 중앙 hello 구독에서 리소스의 hello 보안 상태 보기를 제공 하 고 손상 된 리소스를 방지 하는 데 도움이 되는 권장 사항을 제공 합니다. 보다 세부적인 정책 (예를 들어 적용 정책 toospecific 리소스 그룹을 실현 하 상태 toohello 위험 hello 엔터프라이즈 tootailor 허용)를 허용 합니다. 마지막으로 Azure 보안 센터에는 Microsoft 파트너 및 해당 기능을 Azure 보안 센터 tooenhance에 연결 하는 독립 소프트웨어 공급 업체 toocreate 소프트웨어 수 있도록 하는 개방형 플랫폼입니다. 

> [!TIP]
> Azure Security Center는 기본적으로 각 구독에서 사용하도록 설정됩니다. 그러나 해당 에이전트 tooallow Azure 보안 센터 tooinstall 가상 컴퓨터에서에서 데이터 수집을 사용 하도록 설정 하 고 데이터 수집을 시작 해야 합니다.
> 
> ![데이터 수집](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>다음 단계
* 이제 구독 거 버 넌 스 알아보았습니다입니다 시간 toosee 실제로 이러한 권장 합니다. [Azure 구독 관리 구현 예제](resource-manager-subscription-examples.md)를 참조하세요.

