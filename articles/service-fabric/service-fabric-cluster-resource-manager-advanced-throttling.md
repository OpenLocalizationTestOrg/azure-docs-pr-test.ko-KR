---
title: "hello 서비스 패브릭 클러스터 리소스 관리자의 aaaThrottling | Microsoft Docs"
description: "Hello 서비스 패브릭 클러스터 리소스 관리자에서 제공 하는 tooconfigure hello 스로틀에 알아봅니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Hello 서비스 패브릭 클러스터 리소스 관리자를 제한합니다.
클러스터 리소스 관리자 hello을 올바르게 구성한 경우에 hello 클러스터 중단 얻을 수 있습니다. 예를 들어 동시 노드 및 오류 도메인 오류-업그레이드 하는 동안 발생 한 경우 어떻게 되는지 있을 수 있습니까? 클러스터 리소스 관리자 hello 항상 시도 toofix hello 클러스터 tooreorganize 및 해결 하는 hello 클러스터의 리소스를 사용 하 여 모든 합니다. 스로틀 hello 클러스터 리소스 toostabilize צ ְ ײ-hello 노드 돌아와서 있도록 백업을 제공 하는 데 도움이 되 hello 네트워크 파티션을 치료, 수정 된 bits 배포 합니다.

가 이러한 유형의 상황 toohelp, hello 서비스 패브릭 클러스터 리소스 관리자에 몇 가지 스로틀 포함 되어 있습니다. 이러한 제한은 꽤 큰 장애물입니다. 일반적으로 신중한 계획 및 테스트 없이 변경해서는 안 됩니다.

Hello 클러스터 리소스 관리자의 스로틀을 변경한 경우 조정 해야 해당 tooyour 예상 되는 실제 로드 합니다. 상황에 따라 긴 toostabilize를 사용 하는 hello 클러스터 것을 의미 하는 경우에 일부 나와 있는 원위치에서 toohave 필요를 결정할 수 있습니다. 테스트는 필요한 toodetermine hello 스로틀에 대 한 올바른 값입니다. 스로틀 toobe 충분히 높은 tooallow hello 클러스터 toorespond toochanges 상당한 시간이 필요 하며 충분 한 tooactually 너무 많은 리소스 소비를 방지 하는 하위. 

대부분의 고객을 살펴본 hello 시간 경과 했는데도 문제가 있다면 리소스 제한 된 환경에서 이미 프로그램이 스로틀을 사용 합니다. 몇 가지 예는 각 노드 또는의 많은 상태 저장 복제본 수 toobuild 아닌 디스크에 대 한 제한 된 네트워크 대역폭 것 병렬 toothroughput 제한 사항 때문입니다. 스로틀, 없이 수 있습니다. 작업 toofail 발생 하는 이러한 리소스를 가득 채울 또는 작업 속도가 느려질 수 있습니다. 이러한 상황에서는 고객 스로틀을 사용 하 고 hello 클러스터 tooreach 안정적인 상태 걸리는 시간의 hello 크기를 확장 하는 것을 알고 있는. 고객은 또한 제한된 상태에서는 전반적인 안정성이 낮은 상태로 실행될 수 있다는 사실도 알고 있습니다.


## <a name="configuring-hello-throttles"></a>구성 hello 스로틀

서비스 패브릭은 hello 복제본 이동 수 제한에 대 한 두 가지 메커니즘이 있습니다. 서비스 패브릭 5.7 이전부터 있던 hello 기본 메커니즘 이동 수의 절대값 수치로 제한 나타냅니다. 이러한 방식이 모든 규모의 클러스터에 맞지는 않습니다. 특히, 대규모 클러스터 hello 기본값에 대 한 값 너무 작아서도 필요한 경우, 더 작은 클러스터에 아무런 영향을 주지 않고 분산 속도가 크게 느려지지 수 있습니다. 이 이전 메커니즘으로 대체 되었습니다. 백분율 기반 조정을 확장성이 좋아집니다 동적 클러스터 서비스는 hello 수의 노드 정기적으로 변경 하십시오.

hello 스로틀 hello 클러스터에 있는 복제본의 hello 수의 백분율을 기반으로 합니다. 표현 hello 규칙을 사용 하는 기반 Percetage 스로틀: "로 이동 하지 마십시오 복제본의 10% 이상을 10 분 간격 에서" 예.

백분율 기반 조정에 대 한 hello 구성 설정은 다음과 같습니다.

  - Hello 클러스터에 있는 복제본의 총 수 비율로 표현 되 GlobalMovementThrottleThresholdPercentage-이동 언제 든 지 클러스터에서 허용 되는 최대 수입니다. 0은 제한하지 않음을 나타냅니다. hello 기본값은 0입니다. 이 설정 및 GlobalMovementThrottleThreshold를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.
  - GlobalMovementThrottleThresholdPercentageForPlacement-이동 hello 배치 단계 중에 허용 된 hello 클러스터에 있는 복제본의 총 수 비율로 표현 되는 최대 수입니다. 0은 제한하지 않음을 나타냅니다. hello 기본값은 0입니다. 이 설정 및 GlobalMovementThrottleThresholdForPlacement를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.
  - GlobalMovementThrottleThresholdPercentageForBalancing-이동 hello hello 클러스터에 있는 복제본의 총 수 비율로 표현 되는 단계를 분산 하는 동안 허용 된 최대 수입니다. 0은 제한하지 않음을 나타냅니다. hello 기본값은 0입니다. 이 설정 및 GlobalMovementThrottleThresholdForBalancing를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.

Hello 스로틀 백분율을 지정할 때 5 %0.05로 지정 합니다. hello 간격 이러한 스로틀 제어 되는 초에 지정 된 GlobalMovementThrottleCountingInterval hello입니다.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>기본 횟수 기반 제한
이 정보는 이전 클러스터가 있거나 클러스터가 업그레이드된 후에도 이러한 구성을 계속 유지하는 경우에 제공됩니다. 일반적으로 이러한 hello 백분율을 기준으로 스로틀 위의으로 바뀌는 것이 좋습니다. 백분율 기반 조정 하지 않으면 기본적으로 하므로 이러한 스로틀 비활성화 되 고 hello 백분율을 기준으로 스로틀으로 대체 될 때까지 클러스터에 대 한 기본 스로틀 hello 남아 있습니다. 

  - GlobalMovementThrottleThreshold –이 설정은 일부 시간별 hello 클러스터에 이동 hello 총 수를 제어합니다. hello 기간 hello GlobalMovementThrottleCountingInterval 초에 지정 됩니다. hello GlobalMovementThrottleThreshold hello에 대 한 기본값은 1000 및 hello GlobalMovementThrottleCountingInterval hello에 대 한 기본값은 600입니다.
  - MovementPerPartitionThrottleThreshold –이 설정은 일부 시간에 따라 모든 서비스 파티션에 대 한 이동 hello 총 수를 제어합니다. hello 기간 hello MovementPerPartitionThrottleCountingInterval 초에 지정 됩니다. hello MovementPerPartitionThrottleThreshold hello에 대 한 기본값은 50 및 hello MovementPerPartitionThrottleCountingInterval hello에 대 한 기본값은 600입니다.

이 스로틀에 대 한 hello 구성 hello hello 백분율 기반 조정을으로 같은 패턴을 따릅니다.

## <a name="next-steps"></a>다음 단계
- toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)
- 클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다. toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)
