---
title: "aaaService 패브릭 클러스터 리소스 관리자-선호도 | Microsoft Docs"
description: "서비스 패브릭 서비스에 대한 선호도 구성의 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>서비스 패브릭에서 서비스 선호도 구성 및 사용
선호도 주로 toohelp 용이성 hello 전환 hello 클라우드와 microservices 업계에 더 큰 단일 응용 프로그램에 제공 되는 컨트롤입니다. 또한 사용 됩니다 최적화 방법으로 서비스의 hello 성능 향상을 위한 부작용이 있을 수 있지만.

더 큰 앱 또는 방금 microservices 유의 tooService 패브릭 (또는 분산된 환경)에 두고 설계 되지 않은 상태로 전환 하는 경우를 가정해 봅니다. 이 유형의 전환이 일반적입니다. 먼저 hello 전체 앱 hello 환경에 올리기, 패키지 및 문제 없이 실행 되 고 확인 합니다. 그런 다음 다른 작은 서비스는 모든 통신 tooeach 다른 분할 시작.

결국 hello 응용 프로그램의 몇 가지 문제가 발생 하는 경우가 있습니다. hello 문제는 일반적으로 이러한 범주 중 하나에 속합니다.

1. 일부 구성 요소 X hello 구식 응용 프로그램에 Y 구성 요소에 대해 문서화 되지 않은 종속성 되었고 방금 별도 서비스에 해당 구성 요소를 설정 합니다. 이러한 서비스를 현재 hello 클러스터의 다른 노드에서 실행 하 고, 이후 끊어진 일입니다.
2. 이러한 구성 요소를 통해 통신 (로컬 명명 된 파이프 | 공유 메모리 | 디스크에 파일) 및 실제로 필요한 toobe 수 toowrite 공유 tooa 로컬 리소스 성능상의 이유로 지금 바로 합니다. 이러한 강한 종속성은 나중에 제거될 것입니다.
3. 모든 것이 좋지만, 이들 두 구성 요소는 실제 통신이 잦고 성능에 민감한 것으로 나타났습니다. 이들을 별도의 서비스로 이동시켰을 때 응용 프로그램의 전반적인 성능이 나빠지거나 대기 시간이 늘어났습니다. 결과적으로, hello 전반적인 응용 프로그램 일치 하지 않을 기대 합니다.

이러한 경우에서는 하지 않을 toolose 리팩터링 작업을 하 고 toogo 백 toohello monolith 않으려고 합니다. hello 마지막 조건 일반 최적화로 바람직하지 않을 수 있습니다. 그러나 우리 다시 디자인할 수 hello 구성 요소 toowork 자연스럽 게 서비스로 될 때까지 (또는 hello 성능 기대 사항을 다른 방법으로 해결할 수까지) 여기 tooneed 근접성의 어떤 의미 합니다.

어떤 toodo? 이제 선호도를 켤 수 있습니다.

## <a name="how-tooconfigure-affinity"></a>어떻게 tooconfigure 선호도
선호도를 tooset, 서로 다른 두 서비스 간의 선호도 관계를 정의 합니다. 선호도를 다른 서비스에 있는 한 서비스를 "가리키고" "이 서비스는 해당 서비스가 실행되고 있는 장소에서만 실행될 수 있습니다."라고 생각할 수 있습니다. 경우에 따라 부모/자식 관계 (여기서 가리키는 hello 자식 hello 부모)으로 tooaffinity를 이라고 합니다. 선호도 hello 복제본 또는 하나의 서비스의 인스턴스는 저장 하는 hello에 동일 하면 노드를 다른 서비스의 인수와로 합니다.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> 자식 서비스는 단일 선호도 관계에만 참여할 수 있습니다. 한 번에 hello 자식 선호도 toobe tootwo 부모 서비스 사용 하려는 경우 몇 가지 옵션이 있습니다.
> - Hello 역관계 (한 parentService1 hello 현재 자식 서비스 요소를 가리키고 parentService2), 또는
> - 규칙에 따라 허브 hello 부모 중 하나 지정 하 고 모든 서비스가 해당 서비스를 가리키도록 합니다. 
>
> hello 클러스터의 배치 동작으로 인해 발생 하는 hello는 같은 hello 해야 합니다.
>

## <a name="different-affinity-options"></a>서로 다른 선호도 옵션
선호도는 몇 가지 상관 관계 구성표 중 하나를 통해 표시되며, 두 가지 모드가 있습니다. 선호도의 hello 가장 일반적인 모드 NonAlignedAffinity 주기입니다. NonAlignedAffinity에서 복제본 hello 또는 hello 서로 다른 서비스 인스턴스의에 사항이 hello 동일한 노드. hello 다른 모드는 AlignedAffinity입니다. 정렬된 선호도는 상태 저장 서비스에서만 유용합니다. 동일한 노드가 각 다른 hello 하 구성 두 개의 상태 저장 서비스 정렬 toohave 선호도 사용 하면 이러한 서비스의 기본 hello에 배치 됩니다. 동일한 hello에 이러한 서비스 toobe 배치에 대 한 보조 복제본의 각 쌍 하면 노드. 또한 상태 저장 서비스에 대 한 tooconfigure NonAlignedAffinity (그러나 덜 일반적인). NonAlignedAffinity, hello 서로 다른 복제본에서 두 개의 상태 저장 서비스를 실행 하는 hello의 같은 노드에 hello 하지만 자신의 기본 서로 다른 노드에 있을 수 있습니다.

<center>
![선호도 모드 및 그 영향][Image1]
</center>

### <a name="best-effort-desired-state"></a>최상의 노력이 필요한 상태
선호도 관계는 최상의 노력입니다. Hello 제공 하지 않습니다 배치 또는 hello에서 실행 중인 동일한 실행 가능 프로세스를 수행 하는 안정성의 동일한 보장 합니다. hello 서비스 선호도 관계에는 실패할 수 있으며 독립적으로 이동할 수 있는 다른 엔터티입니다. 선호도 관계도 중단될 수 있지만 이러한 중단은 일시적입니다. 예를 들어 용량 제한이 지정된 된 노드의에 맞출 수 있는 hello 선호도 관계의 hello 서비스 개체의 일부만 의미할 수 있습니다. 이러한 경우 장소에 선호도 관계가 있는 경우에이 적용 될 수 없습니다 due toohello 다른 제약 조건입니다. 따라서 가능한 toodo 있으면 hello 위반 나중에 자동으로 수정 됩니다.

### <a name="chains-vs-stars"></a>체인 모양과 별 모양의 비교
오늘 hello 클러스터 리소스 관리자 수 toomodel 관계 체인을 선호도 하지 않습니다. 즉, 한 선호도 관계에서 자식인 서비스는 다른 선호도 관계에서 부모가 될 수 없습니다. Toomodel 이러한 유형의 관계 toomodel을 원하는 경우 효과적으로 가질 수 체인 것이 아니라는 별모양으로 합니다. 체인 tooa 별 hello 최하위 자식에서에서 toomove 것 부모가 toohello 첫 번째 자식 부모 대신입니다. 서비스의 hello 정렬에 따라이 작업을 여러 번 toodo을 할 수 있습니다. 자연 부모 서비스가 없는 경우에 자리 표시자 역할을 하나 toocreate 할 수 있습니다. 요구 사항에 따라 할 수 있습니다에 toolook [응용 프로그램 그룹](service-fabric-cluster-resource-manager-application-groups.md)합니다.

<center>
![선호도 관계의 컨텍스트에서 체인 모양과 Hello 선호도 관계 상황에 맞는에서 별][Image2]
</center>

현재 선호도 관계에 대 한 또 다른 사항은 toonote은 방향 않는다는입니다. 즉, 해당 hello 선호도 규칙에만 해당 hello 자식 hello 부모와 함께 배치 강제 합니다. 해당 hello 부모는 자식 hello와 함께 확인 하지 않습니다. 선호도 관계가 hello toonote 적용할 수 없으므로 이상적 또는 즉시 서로 다른 서비스는 다른 주기 실패 하 고 수 독립적으로 이동 하므로 중요 한 이기도 합니다. 예를 들어 hello 부모에서 갑자기 장애가 발생 tooanother 노드에 대해 충돌 하기 때문에 가정해 보겠습니다. hello 클러스터 리소스 관리자 및 장애 조치 관리자 핸들 hello 장애 조치 먼저 hello 우선 순위는 따라가고 hello 서비스를 일관 되 고 사용할 수 있습니다. Hello 장애 조치가 완료 되 면 hello 선호도 관계가 끊어지지만 hello 클러스터 리소스 관리자도 괜찮습니다 hello 자식이 발견 될 때까지 생각을 hello 부모를 찾을 수 없는 합니다. 이러한 종류의 검사는 정기적으로 수행됩니다. Hello 클러스터 리소스 관리자 제약 조건을 평가 하는 방법에 자세한 정보가 표시 됩니다 [이 여기서](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), 및 [이것과](service-fabric-cluster-resource-manager-balancing.md) tooconfigure 흐름 이러한 제약 조건이 있는 hello 하는 방법에 대해 자세히 설명 평가합니다.   


### <a name="partitioning-support"></a>분할 지원
선호도 대 한 hello 할 사항이 toonotice는 hello 부모 분할 된 선호도 관계가 지원 되지 않습니다. 분할된 부모 서비스는 결국 지원될 수 있지만 오늘날에는 허용되지 않습니다.

## <a name="next-steps"></a>다음 단계
- 서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.
- toolimit 서비스 tooa 작은 집합이 컴퓨터 또는 서비스를 사용 하 여 집계 hello 부하 [응용 프로그램 그룹](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png