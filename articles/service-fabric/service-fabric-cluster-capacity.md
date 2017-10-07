---
title: "서비스 패브릭 클러스터 용량 aaaPlanning hello | Microsoft Docs"
description: "서비스 패브릭 클러스터 용량 계획 고려 사항입니다. 노드 유형, 내구성 및 안정성 계층"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>서비스 패브릭 클러스터 용량 계획 고려 사항
프로덕션 배포의 경우 용량 계획은 중요한 단계입니다. 다음은 해당 프로세스의 일부로 tooconsider 있다고 hello 항목 중 일부입니다.

* 노드 수가 hello와 아웃 클러스터 요구 toostart 형식
* 각 노드 형식 (크기, 기본, 인터넷 연결 Vm 수)의 hello 속성
* hello 안정성과 영속성 hello 클러스터의 특징

이러한 각 항목을 간단히 검토해보겠습니다.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>노드 수가 hello와 아웃 클러스터 요구 toostart 형식
먼저 만들려는 어떤 hello 클러스터에 사용 되는 toobe 이며 계획 어떤 종류의 응용 프로그램 아웃 toofigure toodeploy이이 클러스터에 있습니다. Hello 클러스터의 hello 목적에서 지우기 작업 중이지 않은 없는 가능성이 가장 높은 아직 tooenter hello 용량 계획 프로세스를 준비 합니다.

클러스터 된 아웃 toostart 필요한 노드 유형의 hello 수를 설정 합니다.  각 노드 유형은 매핑된 tooa 가상 컴퓨터 크기 집합입니다. 각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다. 따라서 노드 유형의 hello 수를 결정 하는 hello 기본적으로 관건은 toohello 다음 고려 사항:

* 응용 프로그램에 여러 서비스 하 고 그 중 어느 필요가 toobe 공용 또는 인터넷 연결? 일반적인 응용 프로그램의 클라이언트에서 입력을 수신 하는 프런트 엔드 게이트웨이 서비스 및 하나 이상의 백 엔드 서비스 통신 하는 hello 프런트 엔드 서비스와 함께 포함 합니다. 따라서 이 경우에 두 개 이상의 노드 유형을 보유하게 됩니다.
* 서비스(응용 프로그램을 구성함)에는 더 유용한 RAM  또는 더 높은 CPU 사용률과 같은 서로 다른 인프라가 필요한가요? 예를 들어 가정 프런트 엔드 서비스와 백 엔드 서비스로 toodeploy 포함 되도록 해당 hello 응용 프로그램입니다. hello 프런트 엔드 서비스를 실행할 수 있는 포트를 열어 toohello 더 작은 Vm (예: D2 VM 크기)에서 인터넷 합니다.  그러나 hello 백 엔드 서비스은 계산 집약적 이며 요구 toorun (d 4, d 6 d 15 같은 VM 크기)와 인터넷 않은 더 큰 Vm에 연결 합니다.
  
  이 예제에서는 tooput를 결정할 수 모든 hello 하나의 노드 형식에는 서비스를 배치 하는 클러스터에 두 개의 노드 유형이 있는 것이 좋습니다.  따라서 속성에 대 한 각 노드 형식 toohave 고유한 인터넷 연결 또는 VM 크기와 같은 수 있습니다. 독립적으로 hello Vm 수를 확장할 수 있습니다.  
* Hello 미래를 예측할 수 없으므로, 이후 알고 팩트와 이동 하 고 hello 다양 한 응용 프로그램으로 toostart 해야 하는 노드 형식에서 결정 합니다. 나중에 노드 유형을 추가하거나 제거할 수 있습니다. 서비스 패브릭 클러스터에는 하나 이상의 노드 유형이 있어야 합니다.

## <a name="hello-properties-of-each-node-type"></a>각 노드 유형에의 hello 속성
hello **노드 형식** 클라우드 서비스에 해당 하는 tooroles로 볼 수 있습니다. 노드 형식은 hello VM 크기, Vm, hello 수 및 해당 속성을 정의합니다. Service Fabric 클러스터에 정의된 모든 노드 형식은 별도의 가상 컴퓨터 확장 집합으로 설정됩니다. 가상 컴퓨터 크기 집합에는 Azure 계산 리소스 toodeploy를 사용 하 고 집합으로 가상 컴퓨터의 컬렉션을 관리할 수 있습니다. 고유한 가상 컴퓨터 확장 집합으로 정의된 각 노드 형식은 독립적으로 확장 또는 축소되고 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.

읽기 [이 문서](service-fabric-cluster-nodetypes.md) Nodetypes toovirtual 컴퓨터 크기 집합의 hello 관계에 대 한 자세한 내용은 어떻게 tooRDP hello 인스턴스 중 하나에 새 포트 열기 등입니다.

클러스터에서 둘 이상의 프로덕션 작업에 사용 되는 클러스터에 대 한 5 개 이상의 Vm (또는 테스트 클러스터에 대 한 최소 세 개의 Vm) 노드 형식이 아니라 hello 주 노드 유형 (첫 번째 hello 포털에서 정의 하는 hello) 가져야 합니다. 리소스 관리자 템플릿을 사용 하 여 hello 클러스터를 만드는 경우 찾습니다 **은 Primary** hello 노드 형식 정의 아래에 특성입니다. hello 주 노드 유형은 서비스 패브릭 시스템 서비스 위치 hello 노드 형식이입니다.  

### <a name="primary-node-type"></a>주 노드 유형
여러 노드 유형으로 클러스터의 경우 필요한 toochoose 그 중 하나가 toobe 기본 합니다. 다음은 하나의 주 노드 종류의 hello 특성입니다.

* hello **Vm의 최소 크기** hello 따라 hello 주 노드 유형이 결정 됩니다 **내구성 계층** 있습니다. hello hello 내구성 계층에 대 한 기본값이 동입니다. 어떤 hello 내구성 계층 이며 값이 지나야 hello에 대 한 자세한 내용은 아래로 스크롤하십시오.  
* hello **Vm의 최소 수** hello 따라 hello 주 노드 유형이 결정 됩니다 **안정성 계층** 있습니다. hello hello 안정성 계층에 대 한 기본값이 실버입니다. 어떤 hello 안정성 계층 이며 값이 지나야 hello에 대 한 자세한 내용은 아래로 스크롤하십시오. 


* (예를 들어 hello 클러스터 관리자 서비스 또는 Image Store 서비스) hello 서비스 패브릭 시스템 서비스는 hello 주 노드 유형 및 등 hello 안정성에 배치 되 고 hello 클러스터의 내구성 hello 안정성 계층 값과 지 속성 계층에 의해 결정 됩니다. hello 기본 노드 형식에 대 한 선택 값입니다.

![두 가지 노드 유형이 있는 클러스터의 스크린 샷 ][SystemServices]

### <a name="non-primary-node-type"></a>주가 아닌 노드 유형
여러 노드 유형으로 클러스터의 경우 하나의 주 노드 형식이 며 hello 나머지는 기본이 아닌 합니다. 다음은 기본이 아닌 노드 유형의 hello 특성입니다.

* 이 노드 형식에 대 한 Vm의 hello 최소 크기는 선택한 hello 내구성 계층에 의해 결정 됩니다. hello hello 내구성 계층에 대 한 기본값이 동입니다. 어떤 hello 내구성 계층 이며 값이 지나야 hello에 대 한 자세한 내용은 아래로 스크롤하십시오.  
* 이 노드 형식에 대 한 Vm의 hello 최소 수 하나일 수 있습니다. 그러나 hello hello 응용 프로그램/서비스 싶다는 의사를이 노드 형식에서 toorun의 복제본 수에 따라이 번호를 선택 해야 합니다. hello 클러스터를 배포한 후 hello 노드 형식에서 Vm 수를 늘릴 수 있습니다.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>hello 클러스터의 hello 내구성 특징
hello 내구성 계층은 Vm hello 기본 Azure 인프라에 포함 된 사용 되는 tooindicate toohello 시스템 hello 권한이 있습니다. Hello 주 노드 종류에서이 권한을 VM 수준 인프라 (예: VM 다시 부팅, VM 이미지로 다시 설치, 또는 VM 마이그레이션) 하는 모든 요청 hello 시스템 서비스와 상태 저장 서비스에 대 한 hello 쿼럼의 요구 사항에 영향 서비스 패브릭 toopause을 허용 합니다. Hello 기본이 아닌 노드 형식에서 VM 수준 인프라 VM 다시 부팅, VM 이미지로 다시 설치, VM 마이그레이션 등에서와 같은 하는 모든 요청에서 실행 되는 프로그램 상태 저장 서비스에 대 한 hello 쿼럼의 요구 사항에 영향을 줄이 사용 권한을 서비스 패브릭 toopause을 허용 합니다.

이 권한은 다음 값에는 hello에 표시 됩니다.

* "Gold"-hello 인프라 UD 당 두 개의 시간 기간에 대 한 작업을 일시 중지할 수 있습니다. 골드 지속성은 D15_V2, G5 등과 같이 전체 노드 VM sku에서만 사용되도록 설정할 수 있습니다.
* 실버-hello 인프라 UD 당 10 분 동안 일시 중지할 수 작업과 단일 코어 이상을 모든 표준 Vm에서 사용할 수 있습니다.
* 브론즈 - 권한이 없습니다. Hello 기본값입니다. 상태 비저장 워크로드_만_ 실행하는 노드 형식의 경우 이 지속성 수준만 사용합니다. 

> [!WARNING]
> 브론즈 지속성으로 실행되는 노드 형식은 _권한 없음_이 됩니다. 즉, 상태 비저장 워크로드에 영향을 주는 인프라 작업은 중지되거나 지연되지 않습니다. 이러한 작업은 워크로드에 계속 영향을 미쳐 가동 중지 시간 또는 기타 문제를 야기할 수 있습니다. 프로덕션 워크로드의 경우에는 실버 이상으로 실행하는 것이 좋습니다. 
> 

각 노드 종류에 대 한 내구성 수준을 toochoose를 가져옵니다. 한 노드 형식을 toohave "gold" 내구성 수준을 선택할 수 있습니다 또는 실버 및 다른 hello 동 hello 경우 동일한 클러스터입니다. **"Gold" 또는 내구성 있는 모든 노드 형식에 대해 5 개의 노드가 최소 수를 유지 해야**합니다. 

**실버 또는 골드 내구성 수준 사용 시 장점**
 
1. Hello에 대 한 크기 조정 작업에 필요한 단계 수가 줄어 (즉, 노드 비활성화 하 고 제거 ServiceFabricNodeState은 자동으로 호출)
2. Hello tooa 고객에서 시작 된 내부 VM SKU 변경 작업 또는 Azure 인프라 작업 인해 데이터 손실 위험을 줄입니다.
     
**실버 또는 골드 내구성 수준 사용 시 단점**
 
1. 가상 컴퓨터 크기 집합 배포 tooyour 및 기타 관련된 Azure 리소스) 지연 될 수 있습니다, 시간을 초과 될 수 또는 hello 인프라 수준에서 나 클러스터에 문제가 완전히 차단 될 수 있습니다. 
2. 증가 hello 수가 [복제 데이터베이스 수명 주기 이벤트](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (예를 들어 기본 교체) Azure 인프라 작업 중 tooautomated 노드 deactivations 때문입니다.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>경우에 대 한 권장 사항은 toouse 실버 또는 "gold" 내구성 수준

사용 하 여 실버 또는 "gold" 내구성 모든 노드 형식은 해당 호스트 상태에 대 한 서비스를 tooscale에서 예상 (VM 인스턴스 수를 감소) 자주 하는 요청 크기 조정에서 이러한 작업을 단순화 하기 위해 배포 작업을 지연 합니다. (Vm 인스턴스 추가) hello 확장 시나리오 선택 하는 hello 내구성 계층으로 재생 되지 않으면만 눈금으로 수행 하는 합니다.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Hello 노드에 대 한 운영 권장 사항 설정 toosilver 또는 "gold" 내구성 수준를 입력 합니다.

1. 클러스터 및 응용 프로그램을 항상 정상 유지 하 고 응용 프로그램 tooall 응답할 [서비스 복제본 수명 주기 이벤트](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (예: 빌드에 대 한 복제본 걸려) 시기 적절 하 게에서 합니다.
2. 보다 안전한 방법으로 toomake VM SKU 변경 (배율 위쪽/아래쪽) 채택: 변경 hello 가상 컴퓨터 크기 집합의 VM SKU는 기본적으로 안전 하지 않은 연산 등 피해 야 가능한 경우. 다음은 hello 프로세스 tooavoid 일반적인 문제를 따를 수 있습니다.
    - **기본이 아닌 nodetypes에 대 한:** 를 만들고 새 가상 컴퓨터 크기 집합, hello 서비스 배치 제약 조건 tooinclude hello 새 가상 컴퓨터 크기 집합/노드 형식을 수정 하 다음 줄일 것이 좋습니다 hello 이전 가상 컴퓨터 크기 집합 (이 toomake hello 노드 제거 hello 안정성 hello 클러스터의 영향을 주지 있는지) 한 번에 한 노드에서 인스턴스 개수 too0 합니다.
    - **Hello 주 노드 종류에 대 한:** hello 주 노드 종류의 VM SKU를 변경 하지 않는 것을 권장 합니다. Hello에 대 한 hello 새로운 SKU 용량 이유를 더 많은 인스턴스를 추가 하는 것이 좋습니다 또는 가능한 경우 새 클러스터를 만들 했습니다. 여지가 없는 수정 toohello 가상 컴퓨터 크기 조정 설정 모델 정의 tooreflect hello 새로운 SKU를 확인 합니다. 클러스터에 하나의 nodetype, 확인 프로그램 상태 저장 응용 프로그램 tooall 응답할 [서비스 복제본 수명 주기 이벤트](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) 적절 한 시간 내에 서비스 복제본 다시 (예: 빌드에 대 한 복제본 고정 됩니다.) 기간은 5 분 (은색 내구성 수준)에 대 한입니다. 


> [!WARNING]
> 마스킹할 권장 변경 hello VM SKU 크기를 VM 크기 집합이 이상 은색 내구성 실행 되 고 있지 않습니다. VM SKU 크기 변경은 데이터 파괴적 내부 인프라 작업입니다. 일부 기능 toodelay 또는 모니터 없이 이러한 변경 있기 hello 작업 상태 저장 서비스에 대 한 dataloss 발생 하거나 다른 unforseen 작동 문제 상태 비저장 워크 로드에도 발생할 수 있습니다. 
> 
    
3. MR이 활성화된 가상 컴퓨터 확장 집합의 노드 수는 5개 이상으로 유지하세요.
4. 임의의 VM 인스턴스를 삭제하지 말고 항상 가상 컴퓨터 확장 집합 규모 축소 기능을 사용하세요. 임의 VM 인스턴스 hello 삭제 불균형 UD와 FD 분산 hello VM 인스턴스를 만들면 한가 있습니다. 이 불균형 hello 서비스 인스턴스/서비스 복제본 간에 hello 시스템 기능 tooproperly 부하 분산에 부정적인 영향을 줄 수 있습니다.
6. 자동 크기 조정을 사용 하는 경우 배율 (VM 인스턴스 제거)에 한 번에 하나의 노드만 완료 되도록 hello 규칙을 설정 합니다. 한 번에 여러 인스턴스의 규모를 축소하는 방식은 안전하지 않습니다.
7. 주 노드 종류를 축소 하는 경우 어떤 hello 안정성 계층에서 허용 하는 보다 더 아래쪽 하지 확장 해야 있습니다.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>hello 클러스터의 hello 안정성 특성
hello 안정성 계층은 사용 되는 hello 기본 노드 형식에서이 클러스터의 toorun 원하는 hello 시스템 서비스는 복제본의 tooset hello 수 있습니다. 복제본 hello 수가 더 hello, hello 안정적 hello 시스템 서비스는 클러스터의입니다.  

hello 안정성 계층 hello 다음 값을 사용할 수 있습니다.

* 플래티넘-9 대상 복제본 집합 수와 함께 실행 hello 시스템 서비스
* "Gold"-7 대상 복제본 집합 수와 함께 실행 hello 시스템 서비스
* 실버-hello 시스템 서비스는 대상 복제본 집합 횟수가 5 인 실행 
* 동-3 대상 복제본 집합 수와 함께 실행 hello 시스템 서비스

> [!NOTE]
> hello 안정성 계층을 선택 하면 기본 노드 형식에 있어야 하는 노드의 hello 최소 수를 결정 합니다. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Hello 안정성 계층에 대 한 권장 사항입니다.

 클러스터 (모든 노드 형식에 있는 VM 인스턴스의 hello 합)의 hello 크기를 늘리거나 하는 경우에 하나의 계층 tooanother에서 클러스터의 hello 안정성을 업데이트 해야 합니다. 이 작업을 수행 hello 클러스터 업그레이드가 필요한 toochange hello 시스템 서비스 복제 집합 개수를 트리거합니다. 모든 다른 변경 내용을 toohello 클러스터 노드를 추가 하는 등을 수행 하기 전에 진행 toocomplete hello 업그레이드를 기다립니다.  서비스 패브릭 탐색기 또는 실행 하 여 hello 업그레이드의 hello 진행률을 모니터링할 수 있습니다 [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

다음은 hello 권장 hello 안정성 계층을 선택 하는 방법입니다.

| **클러스터 크기** | **안정성 계층** |
| --- | --- |
| 1 |지정 하지 않으면 hello 안정성 계층 매개 변수를 계산 하는 hello 시스템 |
| 3 |Bronze |
| 5 또는 6|Silver |
| 7 또는 8 |Gold |
| 9 이상 |플래티넘 |




## <a name="primary-node-type---capacity-guidance"></a>주 노드 유형 - 용량 지침

다음은 hello 주 노드 유형 용량 계획에 대 한 hello 지침

1. **Azure의 모든 프로덕션 작업 toorun 인스턴스 VM의 수:** 5의 최소 주 노드 유형 크기를 지정 해야 합니다. 
2. **Azure에서 테스트 작업 toorun 인스턴스 하는 VM 수** 1 또는 3의 최소 주 노드 유형 크기를 지정할 수 있습니다. 하나의 노드 클러스터에서 실행 된 특별 한 구성이 사용 하 고 있어서 hello, 배율 해당 클러스터에서 지원 되지 않습니다. hello 개 노드 클러스터에 안정성 하므로 리소스 관리자 서식 파일에 있게 되며 tooremove/not 그 구성을 지정 (hello 구성 값을 설정 하지 않으면 충분 하지 않습니다). 설정한 경우 hello 하나의 노드만 클러스터는 포털을 통해 설정 다음 hello 구성 자동으로 처리 되었음을 합니다. 1 및 3 노드 클러스터는 프로덕션 워크로드 실행에 대해 지원되지 않습니다. 
3. **VM SKU:** 주 노드 유형이 이므로 hello 시스템 서비스 실행 하는 위치,에 대 한 전반적인 피크 계정 hello 고려 로드 해야 하면 선택한 VM SKU hello hello 클러스터로 tooplace를 계획 합니다. 어떻게 다시 말해 여기-생각 hello 주 노드 종류의 프로그램 "Lungs"로 발견 tooyour 뇌 제공 하는 예를 들어 tooillustrate 다음과 같습니다 있고 따라서 hello 뇌 충분 한 발견을 받지 못한 경우 보세요. 

그러나 클러스터의 hello 용량 요구 사항 작업에 의해 결정 됩니다 toorun hello 클러스터의 계획, 특정 작업에 대 한 질적 지침을 제공할 수 없습니다, 여기는 hello 광범위 한 지침 toohelp 시작.

프로덕션 워크로드 


- hello 표준 D3 또는 표준 D3_V2 또는 이와 동등한 14GB 로컬 SSD 최소 VM SKU가 하는 것이 좋습니다.
- hello 최소 지원 사용 하 여 VM SKU은 표준 D1 또는 표준 D1_V2 14GB 로컬 SSD 이상에 해당 합니다. 
- 프로덕션 작업에는 표준 A0과 같은 부분 코어 VM SKU가 지원되지 않습니다.
- 표준 A1 SKU는 성능상의 이유로 프로덕션 워크로드에 지원되지 않습니다.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>상태 저장 워크로드에 대한 주가 아닌 노드 유형 - 용량 지침

서비스 패브릭을 사용 하 여 상태 저장 작업을 위해이 설명서는 [신뢰할 수 있는 컬렉션 또는 reliable Actors](service-fabric-choose-framework.md) hello 기본이 아닌 노드 형식에서 실행 중인 합니다.


**VM 인스턴스 수:** 상태 저장 방식의 프로덕션 워크로드의 경우, 최소 5개의 대상 복제본을 사용하여 실행하는 것이 좋습니다. 즉, 각 장애 도메인 및 업그레이드 도메인에 1개의 복제본(복제본 세트 중)이 있으면 안정적인 것입니다. hello 기본 노드 형식에 대 한 hello 전체 안정성 계층 개념은 방식으로 toospecify 시스템 서비스에 대 한이 설정 합니다. 따라서 동일한 hello 고려 tooyour 상태 저장 서비스도 적용 됩니다.

따라서 프로덕션 작업에 대 한 hello 최소 권장된 비-주 노드 유형 크기는 5, 그 안에 상태 저장 작업을 실행 하는 경우입니다.


**VM SKU:** 이므로 hello 노드 유형 응용 프로그램 서비스를 실행 하는 위치를 각 노드에 tooplace를 계획 하는 hello VM SKU,에 대 한 선택에 고려해 야 계정 hello 최대 부하 있습니다. 그러나 hello hello nodetype의 용량 요구 사항, 시작 하는 데 hello 광범위 한 지침 toohelp 같습니다 특정 워크 로드에 대 한 질적 지침을 제공할 수 없습니다 것 있도록 toorun hello 클러스터의 계획 작업에 의해 결정 됩니다

프로덕션 워크로드 

- hello 표준 D3 또는 표준 D3_V2 또는 이와 동등한 14GB 로컬 SSD 최소 VM SKU가 하는 것이 좋습니다.
- hello 최소 지원 사용 하 여 VM SKU은 표준 D1 또는 표준 D1_V2 14GB 로컬 SSD 이상에 해당 합니다. 
- 프로덕션 작업에는 표준 A0과 같은 부분 코어 VM SKU가 지원되지 않습니다.
- 특히 표준 A1 SKU는 성능상의 이유로 프로덕션 워크로드에 지원되지 않습니다.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>상태 비저장 워크로드에 대한 주가 아닌 노드 유형 - 용량 지침

기본이 아닌 nodetype hello에서 실행 되는 상태 비저장 워크 로드의이 안내 합니다.

**VM 인스턴스 수:** 는 상태 비저장 프로덕션 작업에 대 한 최소 지원 hello 아닌 주 노드 유형 크기는 2입니다. 이렇게 하면 toorun 있습니다 상태 비저장의 두 인스턴스 응용 프로그램 및 서비스 toosurvive 허용 hello VM 인스턴스의 손실 합니다. 

> [!NOTE]
> 클러스터 서비스 패브릭 보다 이전 버전이 5.6에서 실행 되는 경우 tooa 결함 hello로 인해 런타임 (이 문제는 5.6 해결), 5, 보다 기본이 아닌 노드 유형 tooless 아래쪽 크기 조정으로 인해 클러스터 상태를 호출할 때까지 비정상 설정 [ 제거 ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) hello 적합 한 노드 이름의 합니다. 자세한 내용은 [내부 또는 외부에서 Service Fabric 클러스터 수행](service-fabric-cluster-scale-up-down.md)을 읽어보세요.
> 
>

**VM SKU:** 이므로 hello 노드 유형 응용 프로그램 서비스를 실행 하는 위치를 각 노드에 tooplace를 계획 하는 hello VM SKU,에 대 한 선택에 고려해 야 계정 hello 최대 부하 있습니다. 그러나 hello hello nodetype의 용량 요구 사항, 시작 하는 데 hello 광범위 한 지침 toohelp 같습니다 특정 워크 로드에 대 한 질적 지침을 제공할 수 없습니다 것 있도록 toorun hello 클러스터의 계획 작업에 의해 결정 됩니다

프로덕션 워크로드 


- hello VM SKU가 표준 D3 또는 표준 D3_V2 또는 이와 동등한 하는 것이 좋습니다. 
- 최소 지원 hello 용도 VM SKU에는 표준 D1 또는 표준 D1_V2 또는 해당 하는 것입니다. 
- 프로덕션 작업에는 표준 A0과 같은 부분 코어 VM SKU가 지원되지 않습니다.
- 표준 A1 SKU는 성능상의 이유로 프로덕션 워크로드에 지원되지 않습니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>다음 단계
용량 계획을 완료 하 고 클러스터를 설정 되 면 hello 다음을 읽어 보십시오.

* [서비스 패브릭 클러스터 보안](service-fabric-cluster-security.md)
* [서비스 패브릭 상태 모델 소개](service-fabric-health-introduction.md)
* [Nodetypes tooVirtual 컴퓨터 크기의 관계 설정](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
