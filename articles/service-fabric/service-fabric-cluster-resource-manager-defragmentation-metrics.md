---
title: "Azure 서비스 패브릭에서 메트릭 aaaDefragmentation | Microsoft Docs"
description: "서비스 패브릭에서 메트릭에 대한 전략으로써 조각 모음 또는 압축 사용의 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>서비스 패브릭에서 부하 및 메트릭의 조각 모음
hello 클러스터의 부하 메트릭을 관리 하기 위한 hello 서비스 패브릭 클러스터 리소스 관리자의 기본 전략은 toodistribute hello load입니다. 노드는 균등 하 게 사용 되 고 있는 보장 tooboth 경합 및 리소스를 불필요 하 게 이어지는 핫 및 콜드 스폿은 방지할 수 있습니다. 오류는 높은 비율의 특정된 작업을 사용 하지 않습니다을 보장 하므로 이후 오류 되지 않고 남아 측면에서 가장 안전한 hello 이기도 hello 클러스터에서 워크 로드를 배포 합니다. 

서비스 패브릭 클러스터 리소스 관리자 hello 부하는 조각 모음을 관리 하기 위한 다른 전략을 지원지 않습니다. 조각 모음을 메트릭 toodistribute hello 사용률 hello 클러스터 전체 말고 것은 통합을 의미 합니다. 통합은 방금의 순서를 변경 hello 기본 균형 조정 전략 – 메트릭 부하의 hello 평균 표준 편차를 최소화 하는 대신, 클러스터 리소스 관리자 hello 시도 tooincrease 것입니다.

## <a name="when-toouse-defragmentation"></a>때 toouse 조각 모음
Hello 클러스터의 부하를 분산 각 노드에 hello 리소스 중 일부를 사용 합니다. 일부 워크로드는 매우 커서 노드의 대부분 또는 전체를 사용하는 서비스를 만듭니다. 이러한 경우에는 없는 큰 경우 충분 하지 않으므로 생성 가져오기 작업 간격을 모든 노드에 toorun에 게 수는. 큰 작업 서비스 패브릭;에서 문제가 되지 않습니다. 이러한 경우 hello 클러스터 리소스 관리자 작업이이 대 한 tooreorganize hello 클러스터 toomake 공간이 필요 함을 확인 합니다. 그러나 hello 그 동안 워크 로드에 hello 클러스터에 예약 된 toowait toobe 있습니다.

가 없을 경우 많은 서비스와 상태 toomove 주위 hello 작업이 toobe hello 클러스터에 배치에 대 한 오래를 걸릴 수 있습니다. 이 hello 클러스터의 다른 워크 로드는 또한 큰 고 긴 tooreorganize 그러니까 가능성이 높습니다. 서비스 패브릭 팀 hello 생성 시간에 따라이 시나리오의 시뮬레이션에서 측정 됩니다. 클러스터 사용률이 30%~50%보다 높아지자마자, 대규모 서비스를 만드는 데 훨씬 더 오래 걸린다는 사실이 확인되었습니다. toohandle이이 시나리오에서는 분산 전략으로 조각 모음을 사용 했습니다. 대규모 워크 로드에 대 한 특히 된 작성 시간을 조각 모음에는 실제로 새 워크 로드에서는 중요 한 예약 hello 클러스터에 있습니다.

노드 수가 더 적은를 조각 모음 메트릭 toohave hello hello 서비스의 클러스터 리소스 관리자 tooproactively try toocondense hello 부하를 구성할 수 있습니다. 이렇게 하면 hello 클러스터를 다시 구성 하지 않고 큰 서비스를 위한 공간이 거의 항상 인지 확인 합니다. Tooreorganize hello 클러스터 고 다니지 않아도 큰 작업을 신속 하 게 만들 수 있습니다.

대부분의 경우에는 디스크 조각 모음이 필요하지 않습니다. 서비스는 hello 클러스터의 해당 위한 하드 toofind 공간 되기 때문에 일반적으로 작은 됩니다. 다시 구성할 수 있으면 대부분의 서비스가 작으며 동시에 빠르게 이동될 수 있으므로 다시 구성 작업도 빠르게 진행됩니다. 그러나 큰 서비스 하 고 신속 하 게 만들 필요 다음 경우 hello를 조각 모음 전략은입니다. 다음 조각 모음을 사용 하 여 hello 장단점에 설명 합니다. 

## <a name="defragmentation-tradeoffs"></a>조각 모음의 장단점
실패한 노드에서 실행되는 서비스가 더 많기 때문에 조각 모음에 미치는 오류의 영향이 커질 수 있습니다. 조각 모음 대량의 작업의 hello 만들기 위해 대기 하는 예약에 hello 클러스터 리소스를 보유 해야 하므로 비용을 높일 수도 있습니다.

hello 다음 다이어그램은 두 클러스터의 시각적 표현, 조각화를 방지 하 고 다른 하나는 없습니다. 

<center>
![분산된 클러스터 및 조각 모음 클러스터 비교][Image1]
</center>

Hello 분산 된 경우에서 이동 hello 최대 서비스 개체 중 하나는 필요한 tooplace 될 hello 수를 고려 합니다. Hello 조각 모음 된 클러스터의 다른 서비스 toomove에 대 한 toowait 필요 없이 hello 작업이 노드 4 개 또는 5에 배치할 수 있습니다.

## <a name="defragmentation-pros-and-cons"></a>조각 모음 장점 및 단점
그러면 다른 개념적 절충은 무엇입니까? 에 대 한 빠른 목차 항목 toothink 다음과 같습니다.

| 조각 모음 장점 | 조각 모음 단점 |
| --- | --- |
| 큰 서비스를 빠르게 만들 수 있습니다 |더 적은 노드에 부하가 집중되어 경합을 늘립니다 |
| 생성하는 동안 데이터 이동을 줄입니다 |실패한 경우 더 많은 서비스에 영향을 주고 더 많은 이탈이 발생할 수 있습니다 |
| 풍부한 요구 사항에 대한 설명 및 공간의 확보가 가능합니다. |전체 리소스 관리 구성이 더 복잡합니다 |

조각 모음 된 혼합할 수 있습니다 및 일반 메트릭을 hello 동일한 클러스터입니다. hello 클러스터 리소스 관리자 시도 tooconsolidate hello 조각 모음 메트릭 분산 하는 동안 최대한 많이 다른 hello 합니다. 조각 모음 능력 분산 전략의 hello 결과 등의 여러 가지 요인에 따라 달라 집니다.
  - 균형 조정 hello 수의 조각 모음 메트릭 및 메트릭을 hello 수
  - 서비스가 두 가지 유형의 메트릭을 모두 사용하는지 여부 
  - hello 메트릭 가중치
  - 현재 메트릭 부하
  
실험은 필요한 toodetermine hello 정확 하 게 구성 필요 합니다. 프로덕션에서 조각 모음 메트릭을 사용하도록 설정하기 전에 워크로드를 철저하게 측정하는 것이 좋습니다. 조각 모음 및 균형 잡힌된 메트릭은 hello 혼합 하는 경우이 특히 동일한 서비스입니다. 

## <a name="configuring-defragmentation-metrics"></a>조각 모음 메트릭 구성
조각 모음 메트릭 구성 hello 클러스터의 적절 한 글로벌 이며 조각 모음에 대 한 개별 메트릭을 선택할 수 있습니다. 다음 구성 조각 hello에 대 한 메트릭을 tooconfigure 조각 모음 하는 방법을 보여 줍니다. 이 경우 "Metric1"는 "Metric2" toobe 균형을 정상적으로 계속 해 서 동안를 조각 모음 기준으로 구성 됩니다. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>다음 단계
- 클러스터 리소스 관리자 hello에 매뉴얼 hello 클러스터를 설명 하는 옵션이 있습니다. toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)
- 메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다. 메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 및 [이 문서](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
