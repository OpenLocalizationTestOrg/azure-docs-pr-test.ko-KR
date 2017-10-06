---
title: "Service Fabric 클러스터 리소스 관리자: 이동 비용 | Microsoft Docs"
description: "Service Fabric 서비스의 이동 비용 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>서비스 이동 비용
서비스 패브릭 클러스터 리소스 관리자 hello 하는 요소는 동안 toodetermine 어떤 변경 toomake tooa 클러스터는 해당 변경 내용이 hello 비용을 고려 합니다. hello 클러스터 크기를 향상 시킬 수에 대 한 "cost"의 hello 개념 들여서 합니다. 분산, 조각 모음 및 기타 요구 사항을 위해 서비스를 이동할 때 비용이 고려됩니다. hello ´ ֲ toomeet hello 요구 사항 hello에 최소 중단 되었거나 비용이 많이 드는 방식으로 합니다. 

서비스 이동에는 최소한의 CPU 시간과 네트워크 대역폭이 필요합니다. 상태 저장 서비스에 대 한 추가 메모리와 디스크를 사용해 이러한 서비스의 상태 hello 복사 해야 합니다. Azure 서비스 패브릭 클러스터 리소스 관리자를 생성 하는 hello 솔루션의 hello 저하를 최소화 하면 hello 클러스터의 리소스를 불필요 하 게 소비 되지 않습니다. 그러나도 않을 hello hello 클러스터의 리소스 할당을 크게 향상 시켜 주는 tooignore 솔루션입니다.

hello 클러스터 리소스 관리자는 컴퓨팅 비용 및 toomanage hello 클러스터 시도 하는 동안 제한의 두 가지 방법에 있습니다. hello 첫 번째 메커니즘 하기가 이동할 때마다 계산 하기만 하면 됩니다. Hello에 대 한 두 개의 솔루션으로 생성 되는 경우 동일한 균형을 맞출 (점수) hello 클러스터 리소스 관리자 (총 이동 수)를 가장 낮은 비용 hello로 하나 hello를 선호 합니다.

이 전략은 효과가 좋습니다. 하지만 복잡한 시스템에서도 기본 또는 정적 부하와 마찬가지로 모든 이동이 동일할 가능성은 거의 없습니다. 일부는 훨씬 더 비용이 많이 드는 가능성이 toobe입니다.

## <a name="setting-move-costs"></a>이동 비용 설정 
만들어질 때 서비스에 대 한 hello 기본 이동 비용을 지정할 수 있습니다.

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

수도 지정 하거나 hello 서비스를 만든 후 서비스에 대 한 MoveCost를 동적으로 업데이트할 수 있습니다. 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>복제본별 이동 비용을 동적으로 지정

hello 이전 조각은 모든 외부 hello 서비스 자체에서 한 번에 전체 서비스에 대 한 MoveCost를 지정 하는 데 있습니다. 그러나 이동 비용이 가장 유용한 경우 hello 이동 비용 특정 서비스 개체의 수명이 따라 변경 합니다. Hello 아마도 자체 서비스 얼마나 많은 비용이 toomove 한 번의 hello 최상의 파악할 서비스 tooreport 런타임 동안 자신의 개별 이동 비용에 대 한 API가입니다. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>이동 비용의 영향
MoveCost에는 0, 낮음, 중간, 높음의 4개 수준이 있습니다. MoveCosts 기타, 0을 제외한 상대 tooeach 됩니다. 이동 비용이 0 이동 무료 이며 hello 솔루션의 hello 점수에 계산 되지 해야 의미 합니다. 설정 tooHigh 비용의 이전 않습니다 *하지* 한 곳에 유지 되므로 해당 hello 복제본을 보장 합니다.

<center>
![이동할 복제본 선택 시의 요인으로 사용되는 이동 비용][Image1]
</center>

MoveCost를 사용 하면 원인 중단을 최소화 전반적인 hello 및 쉬운 tooachieve 여전히 해당 균형에 도착 하는 동안에 hello 솔루션을 찾을 수 있습니다. 서비스의 개념이 비용의 상대 toomany 작업이 될 수 있습니다. hello 가장 일반적인 요소 이동 비용 계산에 같습니다.

- 상태 또는 toomove hello 서비스에 데이터의 hello 양입니다.
- 클라이언트의 연결이 끊어지는의 hello 비용입니다. 주 복제본을 이동 하는 것은 일반적으로 보조 복제본을 이동 하는 hello 비용 보다 더 비쌉니다.
- 진행 중인 작업을 중단의 hello 비용입니다. 일부 작업 hello 데이터 저장소 수준 또는 응답 tooa 클라이언트 호출에서 수행 하는 작업은 비용이 많이 드는 합니다. 특정 시점이 지나면 toostop 원하지 경우 필요가 없습니다. 따라서 hello 작업이 진행 되는 동안에이 서비스 개체 tooreduce hello 가능성을 이동의 hello 이동 비용이 증가 합니다. Hello 작업이 완료 되 면 hello 비용 백 toonormal을 설정 합니다.

## <a name="enabling-move-cost-in-your-cluster"></a>클러스터에서 이동 비용 사용
에 대 한 순서 대로 고려 하는 보다 세부적인 MoveCosts toobe hello, MoveCost 클러스터에서 사용할 수 있어야 합니다. 이 설정이 없으면 hello 기본 모드로 이동 계산 MoveCost, 계산에 사용 되 고 MoveCost 보고서가 무시 됩니다.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>다음 단계
- 서비스 패브릭 클러스터 리소스 관리자 hello 클러스터의 메트릭 toomanage 소비 및 용량을 사용합니다. 메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 하 고 [관리 리소스 소비와 메트릭 사용 하 여 서비스 패브릭에서 부하](service-fabric-cluster-resource-manager-metrics.md)합니다.
- toolearn hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 부하를 분산 시키고 방법,에 체크 아웃 [분산 서비스 패브릭 클러스터](service-fabric-cluster-resource-manager-balancing.md)합니다.

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
