---
title: "aaaManage Azure 마이크로 서비스 부하 메트릭을 사용 하 여 | Microsoft Docs"
description: "서비스 패브릭 toomanage tooconfigure 및 사용 메트릭을 리소스 소비를 서비스 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>메트릭을 사용하여 Service Fabric에서 리소스 부하 및 소비 관리
*메트릭* hello 클러스터의 노드에 hello에 대 한 서비스 관리 프로그램 및입니다 제공 하는 hello 리소스가 있습니다. 서비스의 순서 tooimprove 또는 모니터 hello 성능이 toomanage 원하는 메트릭을 됩니다. 예를 들어 서비스를 사용 하는 오버 로드 된 경우 메모리 소비 tooknow를 조사할 수 있습니다. 또 다른 용도 toofigure 아웃 hello 서비스 여기서 메모리 순서 tooget 더 나은 성능을에 제한 된 작은 다른 위치를 이동할 수 있는지 여부입니다.

메모리, 디스크, CPU 사용량 등이 모두 메트릭의 예입니다. 이러한 메트릭은 물리적 메트릭, toophysical 리소스 toobe 관리 해야 하는 hello 노드에 해당 하는 리소스입니다. 메트릭은 논리 메트릭이 될 수도 있으며 이것이 일반적인 경우이기도 합니다. “MyWorkQueueDepth”, "MessagesToProcess" 또는 "TotalRecords" 등이 논리 메트릭입니다. 논리는 응용 프로그램 정의 메트릭과 toosome 물리적 리소스 소비를 직접 해당 합니다. 논리 메트릭은 하드 toomeasure 및 서비스별 단위로 물리적 리소스의 보고서 소비 수 있기 때문에 일반적인 있습니다. 측정 하 고 보고 직접 실제 메트릭 hello 복잡성 서비스 패브릭 몇 가지 기본 메트릭을 제공 하는 이유 이기도 합니다.

## <a name="default-metrics"></a>기본 메트릭
Tooget 작성 및이 서비스 배포를 시작 하려는 경우를 가정해 봅니다. 이 시점에서는 어떤 물리적 또는 논리적 리소스를 사용하는지 알 수 없습니다. 이것으로 끝입니다. 서비스 패브릭 클러스터 리소스 관리자 hello 없는 다른 메트릭을 지정 되 면 몇 가지 기본 메트릭을 사용 합니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

  - PrimaryCount-hello 노드의 주 복제본의 수 
  - ReplicaCount-hello 노드에서 총 상태 저장 복제본의 수
  - Count-hello 노드에서 모든 서비스 개체 (상태 비저장 및 상태 저장)의 수

| 메트릭 | 상태 비저장 인스턴스 부하 | 상태 저장 보조 부하 | 상태 저장 기본 부하 |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| 개수 |1 |1 |1 |

기본 작업에 대 한 hello 기본 메트릭 hello 클러스터에서 작업의 좋은 분포를 제공합니다. 다음 예제는 hello에서 두 가지 서비스를 생성 하 고 균형 조정에 대 한 기본 메트릭 hello에 의존 하는 경우 어떻게 되는지 확인해 보겠습니다. hello 첫 번째 서비스는 세 개의 파티션이 있는 상태 저장 서비스 및 대상 복제본 집합 크기의 3입니다. hello 두 번째 서비스는 하나의 파티션 3의 인스턴스 수와 상태 비저장 서비스입니다.

다음을 알 수 있습니다.

<center>
![기본 메트릭으로 클러스터 레이아웃][Image1]
</center>

일부 작업 toonote:
  - 여러 노드에 분산 hello 상태 저장 서비스에 대 한 주 복제본
  - 다른 노드에서 동일한 파티션에 hello에 대 한 복제본
  - 기본 및 보조 복제본의 총 hello는 hello 클러스터에 배포
  - 각 노드에 할당 된 균등 하 게는 서비스 개체의 hello 총 수

좋습니다.

기본 메트릭 hello로 시작 하는 잘 작동합니다. 그러나 hello 기본 메트릭만 이동 지금까지 합니다. 예: 모든 파티션에 의해 완벽 하 게도 사용률의 결과 선택는 체계 hello 분할 hello 가능성 란? 지정된 된 서비스에 대 한 부하를 hello hello 확률이 이란는 시간이 지남에 따라 상수 또는 심지어 환영 동일한 여러 파티션에서 지금 바로?

방금 hello 기본 메트릭을 사용 하 여 실행할 수 있습니다. 그러나 이렇게 하면 일반적으로 클러스터 사용률이 원하는 것보다 낮고 균등하지 않습니다. 이 hello 기본 메트릭 적응 아닌 모든 항목은 해당 하는 것으로 가정할 때문입니다. 예를 들어, 사용 된 주 서버와 이름이 아닌 두 "1" toohello PrimaryCount 메트릭에 영향을 줍니다. Hello 최악의 경우에서 기본 메트릭만 hello를 사용 하 여 유발할 수도 있습니다 overscheduled 노드 성능 문제가 발생 합니다. Hello 클러스터 외부로 대부분 가져오고 성능 문제를 방지 하는 데 관심이 인 경우 toouse 사용자 지정 메트릭 및 동적 로드를 보고 하는 것이 해야 합니다.

## <a name="custom-metrics"></a>사용자 지정 메트릭
메트릭은 hello 서비스를 작성할 때 명명 된-서비스-인스턴스 단위 별로 구성 됩니다.

모든 메트릭에는 자체에 대해 설명하는 이름,가중치 및 기본 로드와 같은 몇 가지 속성이 있습니다.

* Hello 메트릭의 메트릭 이름: hello 이름입니다. hello 메트릭 이름은 hello 리소스 관리자의 관점에서 hello 클러스터 내에서 hello 메트릭에 대 한 고유 식별자입니다.
* 가중치: 메트릭 가중치 정의 얼마나 중요 한지이 측정값은 상대 toohello이이 서비스에 대 한 다른 메트릭을 합니다.
* 기본 로드: hello 기본 부하 상태 저장 또는 상태 비저장 hello 서비스 인지에 따라 다르게 표현 됩니다.
  * 상태 비저장 서비스의 경우 각 메트릭에는 DefaultLoad라는 단일 속성만 있습니다.
  * 상태 저장 서비스의 경우 다음과 같이 정의합니다.
    * 이 메트릭은 기본 되었을 때이 서비스를 소비 양을 hello 기본 primaryDefaultLoad:
    * 이 메트릭은 보조 되었을 때이 서비스를 소비 양을 hello 기본 secondaryDefaultLoad:

> [!NOTE]
> Too_explicitly_ 사용자 지정 메트릭 정의 too_also_ hello 기본 메트릭을 사용 하려는 경우 해야 hello 기본 메트릭 백업 하 고 가중치 및 값 정의 추가 합니다. 즉, 사용자 지정 사항과 hello 기본 메트릭 간의 hello 관계를 정의 해야 합니다. 예를 들어 ConnectionCount 또는 WorkQueueDepth에 대한 관심이 기본 배포 이상일 수 있습니다. Hello PrimaryCount의 기본 hello 가중치로 메트릭을 높음, 있습니다 tooreduce 것 tooMedium 우선 하 여 다른 메트릭을 tooensure를 추가 합니다.
>

### <a name="defining-metrics-for-your-service---an-example"></a>서비스에 대한 메트릭 정의 - 예
같은 구성이 hello를 원하는 경우를 가정해 보십시오.

  - 서비스에서 "ConnectionCount"라는 메트릭을 보고합니다.
  - 시겠습니까 toouse hello 기본 메트릭 
  - 몇 가지 측정을 수행했으며 일반적으로 해당 서비스의 주 복제본에서 20단위의 "ConnectionCount"를 차지한다는 것을 알고 있습니다.
  - 보조 복제본에서 5단위의 "ConnectionCount"를 사용합니다.
  - "ConnectionCount" hello 성능이 특정 서비스의 관리 측면에서 가장 중요 한 메트릭을 hello입니다.
  - 여전히 분산된 주 복제본을 원합니다. 주 복제본의 분산이 무엇이든 간에 일반적으로 좋은 아이디어입니다. 이렇게 하면 다 수의 함께 주 복제본에 영향을 주는 일부 노드 또는 오류 도메인의 hello 손실을 방지 합니다. 
  - Hello 기본 메트릭을 만족 하는 그렇지 않은 경우

Hello 코드를 작성 toocreate 메트릭 해당 구성 사용 하 여 서비스는 다음과 같습니다.

코드:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> 위의 예제 hello 및 hello이 문서의 나머지 부분에 대해 설명 관리 메트릭 당-명명 된 서비스 별로 합니다. Hello 서비스에서 서비스에 대 한 가능한 toodefine 메트릭을 이기도 _형식_ 수준입니다. 이는 서비스 매니페스트에 지정하여 수행됩니다. 유형 수준 메트릭을 정의하는 것은 여러 가지 이유로 권장되지 않습니다. 첫 번째 이유 hello 메트릭 이름이 자주 환경별 한다는 것입니다. 현재 위치에 회사 계약 있지 않은 한 환경에서 해당 hello 메트릭이 "코어"에 "MiliCores" 또는 "코어" 있고 다른 없어야 수 없습니다. 매니페스트에 하면 메트릭이 정의 된 경우 환경당 toocreate 새 매니페스트 해야 합니다. 이 가지 매니페스트 tooa 확산 됨에 따라를 약간의 차이만, toomanagement 문제가 될 수 있는와 일반적으로 이어집니다.  
>
> 메트릭 로드는 일반적으로 명명된 서비스 인스턴스별로 할당됩니다. 예를 들어 가정해 hello의 한 인스턴스를 만들고 서비스 CustomerA toouse 계획을 사용자에 대 한 가끔 합니다. 더 큰 워크로드를 가지고 있는 CustomerB에 대해서도 다른 하나의 서비스 인스턴스를 만든다고 가정해 보겠습니다. 이 경우 할 tootweak hello 기본 이러한 서비스에 대해 로드 합니다. 메트릭 있고 매니페스트를 통해 정의 된 로드 toosupport이이 시나리오를 사용할 경우 각 고객에 대 한 다른 응용 프로그램 및 서비스 유형 필요 합니다. 서비스를 만들 때 정의 된 hello 값 이므로 해당 tooset hello 특정 기본값을 사용할 수 있습니다 hello 매니페스트에서 정의 된 재정의 합니다. 그러나 하는 작업을 실행 하면 hello 값을 사용 하는 hello 서비스가 실제로 실행 하는 hello 매니페스트 toonot 일치에서 선언 합니다. Tooconfusion을 발생할 수 있습니다. 
>

참고로: tootouch hello 메트릭 컬렉션을 전혀 필요 하지 않거나 서비스를 만들 때 별도 작업 toouse hello 기본 메트릭만 하려는 경우. hello 기본 메트릭 get 에서만 정의 되어 있는 경우 자동으로 사용 합니다. 

이제 이러한 각 설정의 더 자세히 살펴보겠습니다를 높여 hello 동작에 설명 합니다.

## <a name="load"></a>로드
메트릭 정의 hello toorepresent 일부 로드 됩니다. *로드*는 지정된 노드의 일부 서비스 인스턴스 또는 복제본에서 지정된 메트릭을 사용하는 양입니다. 로드는 거의 모든 지점에서 구성될 수 있습니다. 예:

  - 서비스를 만들 때 로드를 정의할 수 있습니다. 이를 _기본 로드_라고 합니다.
  - 서비스는 hello 서비스를 만든 후 업데이트 수에 대 한 기본 등의 hello 메트릭 정보를 로드 합니다. 이를 _서비스 업데이트_라고 합니다. 
  - 지정 된 파티션의 hello 로드에는 해당 서비스에 대 한 재설정 toohello 기본값 수 있습니다. 이를 _파티션 로드 다시 설정_이라고 합니다.
  - 로드는 런타임에 동적으로 서비스 개체별로 보고될 수 있습니다. 이를 _로드 보고_라고 합니다. 
  
다음이 전략 중 모든 hello 해당 수명 동안 동일한 서비스 내에서 사용할 수 있습니다. 

## <a name="default-load"></a>기본 부하
*기본 로드* 는이 서비스의 각 서비스 개체 (상태 저장 복제본 또는 상태 비저장 인스턴스)를 사용 하는 hello 메트릭의 매우 간단 합니다. hello 클러스터 리소스 관리자 동적 부하 보고서 등의 정보를 받을 때까지 hello 부하 hello 서비스 개체의에이 번호를 사용 합니다. 간단한 서비스에 대 한 hello 기본 로드 정적 정의입니다. hello 기본 로드 업데이트 되지 않고 고 hello 서비스의 수명과 hello에 대 한 사용 됩니다. 기본 단순 용량 특정 양의 리소스는 전용된 toodifferent 작업 하 고 변경 하지 않는 시나리오를 계획에 대 한 작동 좋은 로드 합니다.

> [!NOTE]
> 용량 관리 및 클러스터의 hello 노드에 대 한 용량 정의에 대 한 자세한 내용은 참조 하십시오 [이 여기서](service-fabric-cluster-resource-manager-cluster-description.md#capacity)합니다.
> 

hello 클러스터 리소스 관리자가 기본 및 보조 복제본에 대 한 상태 저장 서비스 toospecify 다른 기본 부하를 수 있습니다. 상태 비저장 서비스 tooall 인스턴스에 적용 되는 하나의 값만 지정할 수 있습니다. 상태 저장 서비스에 대 한 기본 및 보조 복제본에 대 한 hello 기본 로드 되므로 일반적으로 다른 복제본 다른 종류의 각 역할에서 작업을 수행입니다. 예를 들어 기본 일반적으로 읽기 및 쓰기를 모두 한 제공 하지만 보조 데이터베이스는 그렇지 않습니다 hello 계산 부담을 대부분 처리할 합니다. 일반적으로 주 복제본에 대 한 기본 부하 hello 보조 복제본에 대 한 기본 부하 hello 보다 높습니다. hello 실수 사용자 고유의 측정값에 의존 해야 합니다.

## <a name="dynamic-load"></a>동적 부하
한동안 서비스를 실행했다고 가정해 보겠습니다. 일부 모니터링에서 다음을 확인했습니다.

1. 일부 파티션 또는 특정 서비스의 인스턴스가 다른 항목보다 더 많은 리소스를 소비합니다.
2. 일부 서비스에 시간 경과에 따라 달라지는 부하가 있습니다.

많은 요소가 이러한 유형의 부하 변동을 야기할 수 있습니다. 예를 들어 서비스 또는 파티션마다 별도의 요구 사항을 가진 서로 다른 고객과 연관됩니다. Hello 양을 작업 hello 서비스는 hello 하루의 hello 과정 동안 달라 지므로 부하 변경할 수도 있습니다. Hello 이유 때문에 관계 없이 일반적으로 기본에 사용할 수 있는 단일 번호가 없습니다. Tooget hello hello 클러스터 외부로 대부분 사용률을 하려는 경우 특히 유용 합니다. 기본 로드에 대 한 선택 된 모든 값이 일부 hello 시간이 잘못 되었습니다. 잘못 된 기본 hello 클러스터 리소스 관리자 또는 리소스를 할당 하는 아래에 결과 로드 합니다. 결과적으로, 또는 초과 사용 되는지에 hello 클러스터 리소스 관리자 hello 클러스터는 균형을 확인 하는 경우에 된 노드가 있는 경우. 기본 로드는 초기 배치에 대한 일부 정보를 제공하기 때문에 여전히 유용하지만 실제 워크로드에 대해 완전하게 알려주지는 않습니다. 리소스 요구 사항, hello 클러스터 리소스 관리자 변경 tooaccurately 캡처 각 서비스 개체 tooupdate 자체 부하 런타임 중 허용 합니다. 이를 동적 부하 보고라 합니다.

동적 부하 보고서 복제본 또는 인스턴스 tooadjust 자신의 할당이/보고 부하 메트릭 수명이 허용합니다. 콜드 상태이며 아무 작업도 수행하지 않는 서비스 복제본 또는 인스턴스는 보통 특정 메트릭을 적게 사용했다고 보고합니다. 사용 중인 복제본 또는 인스턴스는 더 많은 양을 사용 중이라 보고할 것입니다.

복제본 또는 인스턴스 당 로드를 보고 하면 클러스터 리소스 관리자 tooreorganize hello hello 개별 서비스 개체 hello 클러스터에 있습니다. Hello 서비스를 다시 구성 되도록 hello 리소스를 차지 하는 데 도움이 됩니다. 사용 중인 서비스가 효과적으로 가져올 너무 리소스 다른 복제본 또는 콜드 또는 더 적은 작업을 수행 하는 현재 인스턴스를 "회수할"입니다.

신뢰할 수 있는 서비스 내에서 hello 코드 tooreport 부하는 동적으로 다음과 같이 보입니다.

코드:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

서비스를 만들 때 정의 된 hello 메트릭 중 하나에 보고할 수 있습니다. 없음을 메트릭에 대 한 서비스 보고서 부하 toouse 구성, 서비스 패브릭 해당 보고서를 무시 합니다. 다른 경우 메트릭에서 보고 된 hello 동일 허용이 보고서를 사용할 수 있는 시간입니다. 서비스 코드 수를 측정 및 모든 hello 알고 메트릭을 보고 방법, 고 연산자 toochange hello 서비스 코드를 필요 없이 hello 메트릭 구성 toouse를 지정할 수 있습니다. 

### <a name="updating-a-services-metric-configuration"></a>서비스의 메트릭 구성 업데이트
hello 서비스와 관련 된 메트릭 hello 목록 및 이러한 메트릭 hello 속성 hello 서비스는 라이브 동안 동적으로 업데이트할 수 있습니다. 이렇게 하면 실험과 유연성을 허용합니다. 유용한 경우의 몇 가지 예는 다음과 같습니다.

  - 특정 서비스에 대한 버그가 포함된 보고서로 메트릭 비활성화
  - 원하는 동작을 기반으로 메트릭의 hello 가중치를 다시 구성
  - hello 코드 이미 배포 되어 다른 메커니즘을 통해 유효성을 검사 한 후에 새 메트릭을 사용 하도록 설정
  - 관찰 된 동작 및 소비에 따라 서비스에 대 한 hello 기본 부하를 변경 합니다.

hello 메트릭 구성 변경에 대 한 기본 Api는 `FabricClient.ServiceManagementClient.UpdateServiceAsync` C# 및 `Update-ServiceFabricService` PowerShell에서 합니다. 이러한 Api를 사용 하 여 지정한 모든 정보는 즉시 hello hello 서비스에 대 한 기존 메트릭 정보를 대체 합니다. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>기본 부하 값 및 동적 부하 보고서 혼합
기본 로드 및 동적 부하 hello에 사용할 수 있습니다 동일한 서비스입니다. 서비스에서 기본 로드 및 동적 로드 보고서를 모두 사용하는 경우 동적 보고서가 표시될 때까지 기본 로드가 추정값으로 사용됩니다. 기본 로드와 toowork 어떤 hello 클러스터 리소스 관리자도 제공 좋습니다. hello 기본 로드 하면 클러스터 리소스 관리자 tooplace hello 좋은 위치에 hello 서비스 개체 생성 될 때 있습니다. 기본 로드 정보를 제공하지 않으면 서비스 배치가 사실상 무작위로 수행됩니다. 부하 보고서는 나중에 도착할 때 hello 초기 무작위 배치는 잘못 된 수 있으며 hello 클러스터 리소스 관리자가 toomove 서비스.

이전 예제에서 몇 가지 사용자 지정 메트릭과 동적 부하 보고를 추가하면 어떻게 되는지 살펴보겠습니다. 이 예제에서는 "MemoryInMb"를 예제 메트릭으로 사용합니다.

> [!NOTE]
> 메모리를 사용 하면 서비스 패브릭 수 hello 시스템 메트릭을 중 하나인 [리소스 제어](service-fabric-resource-governance.md), 일반적으로 어렵습니다 직접 보고 하 고 있습니다. 실제로으로 예상 하면 tooreport 메모리 소비; 메모리가 사용 되는 보조 toolearning hello 클러스터 리소스 관리자의 hello 기능에 대 한로 합니다.
>

다음 명령을 hello로 hello 상태 저장 서비스를 처음 만든 가정 하겠습니다.

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

참고로, 이 구문은 ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad")입니다.

가능한 클러스터 레이아웃의 모양을 살펴보겠습니다.

<center>
![기본 및 사용자 지정 메트릭으로 클러스터 부하 분산][Image2]
</center>

주목할 만한 몇 가지가 있습니다.

* 파티션 내의 보조 복제본은 각각 고유한 로드를 가질 수 있습니다.
* 전반적인 hello 메트릭 균형을 찾습니다. 메모리에 대 한 최대 hello 사이의 비율 hello 및 최소 부하는 1.75 (hello 노드 hello로 최대 부하는 N3, N2 및 16/28/hello은 1.75 =) 합니다.

일부의 tooexplain을 계속 합니다.

* 1.75의 비율이 합리적인지를 무엇이 결정했나요? 어떻게는 클러스터 리소스 관리자 hello 알 수 정도 되는 경우 또는 작업 toodo 더 있는 경우?
* 언제 부하가 분산되나요?
* 메모리의 가중치가 "높음"은 무슨 의미인가요?

## <a name="metric-weights"></a>메트릭 가중치
동일 추적 hello 다른 서비스에서 메트릭이 중요 합니다. 전역 보기 인지 hello hello 클러스터의 클러스터 리소스 관리자 tootrack 소비 하 고, 노드를 소비 분산할 노드 용량 지나치게 확인 수 있습니다. 하지만 서비스의 hello toohello 중요도 서로 다른 뷰 있을 수 있습니다 동일한 메트릭을 합니다. 또한 메트릭과 서비스가 많은 클러스터에서는 모든 메트릭에 대해 완벽하게 분산된 솔루션이 없을 수도 있습니다. 클러스터 리소스 관리자 hello 이러한 상황을 처리할 방법

메트릭 가중치는 완벽 한 응답이 없을 때 toobalance hello 어떻게 클러스터에 클러스터 리소스 관리자 toodecide hello를 허용 합니다. 메트릭 가중치도 hello 클러스터 리소스 관리자 toobalance 특정 서비스의 허용 다르게 합니다. 메트릭은 0, 낮음, 보통, 높음 등 네 가지 가중치 수준을 사용할 수 있습니다. 작업이 분산되는지 여부를 고려할 때 가중치가 0인 메트릭은 작업에 아무런 영향을 주지 않습니다. 그러나 해당 부하는 toocapacity 관리 여전히 영향을 줍니다. 가중치가 0인 메트릭은 여전히 유용하며, 서비스 동작 및 성능 모니터링의 일부로 자주 사용됩니다. [이 문서](service-fabric-diagnostics-event-generation-infra.md) 모니터링에 대 한 메트릭 사용 하 여 hello 및 서비스의 진단에 자세한 정보를 제공 합니다. 

hello 실제 영향 hello 클러스터의 서로 다른 메트릭 가중치는 hello 클러스터 리소스 관리자 생성 다양 한 솔루션입니다. 메트릭 가중치 확인할 hello 클러스터 리소스 관리자는 특정 메트릭을 다른 항목 보다 더 중요 한 있습니다. 완벽 한 솔루션 hello 경우 클러스터 리소스 관리자 수 더 높은 가중치가 적용 된 메트릭 hello 더 나은 균형 솔루션을 선호 합니다. 서비스에서 특정 메트릭이 중요하지 않다고 인식하면 해당 메트릭의 사용이 분산되지 않았다고 확인할 수 있습니다. 이렇게 하면 다른 서비스 tooget 중요 tooit은 일부 메트릭의 균등 한 분포가 있습니다.

일부 부하 보고서와 어떻게 다른 메트릭을의 예를 살펴 보겠습니다 hello 클러스터의 다른 할당에는 결과 가중치를 적용 합니다. 이 예제를 hello hello 메트릭 상대 가중치를 전환 하면 클러스터 리소스 관리자 toocreate hello 서비스의 다른 정렬 작업을 참조 합니다.

<center>
![메트릭 가중치 예제 및 부하 분산 솔루션에 미치는 영향][Image3]
</center>

이 예에서는 별도의 두 메트릭인 메트릭 A 및 메트릭 B에 대해 모두 서로 다른 값을 보고하는 별도의 4가지 서비스가 있습니다. 한 경우, 모든 hello 서비스 정의 MetricA는 hello 중 가장 중요 한 (가중치 = 높음) 및 중요 하지 않은으로 MetricB (가중치 = 낮음). 결과적으로, 해당 hello 클러스터 리소스 관리자 MetricA는 균형 잡힌 MetricB 보다 더 잘 되도록 hello 서비스를 배치 하는 것이 보면 됩니다. "더 잘 분산됨"은 메트릭 B보다 낮은 표준 편차가 메트릭 A에 있음을 의미합니다. Hello 두 번째 경우에서 hello 메트릭 가중치 리버스 했습니다. 결과적으로, hello 클러스터 리소스 관리자 치환 서비스 A와 B toocome를 MetricB MetricA 보다 균형 있는 향상 되는 할당 합니다.

> [!NOTE]
> 메트릭 가중치 hello 클러스터 리소스 관리자 간의 균형 어떻게, 하지만 때 분산 해야 발생 하지 결정 합니다. 분산에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-balancing.md)를 확인하세요.
>

### <a name="global-metric-weights"></a>전역 메트릭 가중치
ServiceA MetricA 높음, 가중치를 부여 하는 대로 정의 하 고 ServiceB MetricA tooLow 또는 0에 대 한 hello 가중치 설정 하는 경우를 가정해 보십시오. 익숙해지려면 최종적 hello 실제 가중치 이란?

모든 메트릭에 대해 추적되는 여러 가중치가 있습니다. hello 첫 번째 두께 hello 서비스를 만드는 경우 hello 메트릭을 대해 정의 된 hello입니다. hello 다른 가중치는 한 글로벌 가중치를 자동으로 계산 됩니다. hello 클러스터 리소스 관리자는 솔루션의 점수를 매길 때 이러한 두 가중치를 사용 합니다. 두 가중치를 모두 고려해야 합니다. 이렇게 하면 클러스터 리소스 관리자 toobalance hello 각 서비스에 따라 tooits 우선 순위를 소유 하 고 해당 hello 클러스터 전체 올바르게 할당 됩니다.

어떻게 되는지를 hello 클러스터 리소스 관리자는 전역 및 지역 균형에 대 한 중요 하지 않은 경우? 분산 되는 전역적으로, 하지만 개별 서비스에 대 한 저하 리소스 균형의 응답이 느려져서 될 쉽게 tooconstruct 솔루션은 합니다. 다음 예제는 hello에서 hello 기본 메트릭만을 사용 하 여 구성 하는 서비스를 확인 하 고 글로벌 분산만 고려할 때 수행 되는 작업을 참조 해 보겠습니다 합니다.

<center>
![hello 글로벌만 솔루션의 영향][Image4]
</center>

예에서 hello 상위 글로벌 분산에 따라서만 hello 클러스터에 전체적으로는 실제로 균형. 모든 노드에 있는 동일한 됨으로 항목과 동일 hello hello 총 복제본 번호입니다. 그러나이 할당의 hello 실제 영향을 보면 없는 경우 좋지 않습니다: 모든 노드의 hello 손실을 영향 특정 작업 비례적, 모든 해당 기본 사용 하기 때문에 있습니다. 예를 들어 hello 첫 번째 노드에 장애가 hello 원 서비스의 세 가지 서로 다른 파티션 hello에 대 한 세 가지 기본 hello 모두 손실 됩니다. 반대로, 삼각형 hello 및 양쪽 대괄호 서비스에는 파티션이 복제 손실 합니다. 이렇게 하면 복제본 다운 toorecover hello 해야 중단 없이 됩니다.

Hello 아래 예제에서는 hello 클러스터 리소스 관리자를 두 hello 전역 및 서비스 당 균형에 따라 hello 복제본 배포 했습니다. Hello 솔루션의 hello 점수를 계산할 때 대부분의 (구성 가능) 부분 tooindividual 서비스 및 hello 가중치 toohello 글로벌 솔루션을 제공 합니다. 메트릭에 대 한 전역 균형 hello 메트릭 가중치는 각 서비스에서의 hello 평균에 따라 계산 됩니다. 각 서비스에 따라 tooits 직접 정의 된 메트릭 가중치 균형이 조정 됩니다. 이렇게 하면 hello 서비스 tootheir 고유의 요구에 따라 자체 내에서 분산 됩니다. 결과적으로, hello 동일한 첫 번째 노드가 실패 하면 hello 실패 하는 경우 모든 서비스의 모든 파티션에 분산 됩니다. hello 영향 tooeach 동일 hello 됩니다.

## <a name="next-steps"></a>다음 단계
- 서비스 구성에 대한 자세한 내용은 [서비스 구성](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.
- 조각 모음 메트릭을 정의 하는 것은 확산 하는 대신 노드에 대 한 가지 방법은 tooconsolidate 로드 합니다. toolearn 어떻게 tooconfigure 조각 모음, 너무 참조[이 문서](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)
- Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)
- 이동 비용은 하나의 방법 특정 서비스는 다른 항목 보다 더 비용이 많이 드는 toomove toohello 클러스터 리소스 관리자 신호입니다. 이동 비용에 대해 자세히 toolearn 너무 참조[이 문서](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
