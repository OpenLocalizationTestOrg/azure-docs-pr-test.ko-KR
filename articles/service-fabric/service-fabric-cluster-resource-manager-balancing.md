---
title: "aaaBalance Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "소개 toobalancing hello 서비스 패브릭 클러스터 리소스 관리자를 사용 하 여 클러스터입니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>서비스 패브릭 클러스터 분산
서비스 패브릭 클러스터 리소스 관리자 hello 동적 로드 변경 내용, 응답할 tooadditions 또는 노드 또는 서비스의 제거를 지원합니다. 제약 조건 위반을 자동으로 수정 하 고 사전 hello 클러스터를 변경 합니다. 그러나 이러한 작업은 얼마나 자주 수행될까요? 그리고 이러한 작업을 트리거하는 것은 무엇일까요?

해당 hello 클러스터 리소스 관리자가 수행 하는 작업의 세 가지 범주가 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

1. 배치 – 이 단계는 상태 저장 복제본 또는 누락된 상태 비저장 인스턴스 배치를 처리합니다. 배치에는 새로운 서비스와 실패한 상태 저장 복제본 또는 상태 비저장 인스턴스 모두가 포함됩니다. 복제본 또는 인스턴스 삭제와 제거도 여기에서 다룹니다.
2. 제약 조건 검사-이 단계에 대 한 확인 하 고 hello 다른 배치 제약 조건 (규칙) hello 시스템 내에서 위반을 수정 합니다. 규칙의 예로는 노드 용량을 초과하지 않고 서비스 배치 제약 조건을 충족하도록 하는 것을 들 수 있습니다.
3. 분산-이 단계 toosee 균형 조정이 필요한 경우 hello 구성에 따라 원하는 수준의 다른 메트릭에 대 한 균형을 확인 합니다. 그렇다면 toofind hello에 정렬을 클러스터 즉 분산 더 시도 합니다.

## <a name="configuring-cluster-resource-manager-timers"></a>클러스터 리소스 관리자 타이머 구성
hello 주위 균형 조정 컨트롤의 첫 번째 집합은 타이머의 집합입니다. 이러한 타이머 얼마나 자주 hello 클러스터 리소스 관리자 hello 클러스터를 검사 하 고 수정 동작을 수행을 제어 합니다.

이러한 각 유형의 다른의 수정 사항 hello 클러스터 리소스 관리자를 만들 수는 해당 빈도 제어 하는 다른 타이머에 의해 제어 됩니다. 각 타이머 발생 하는 경우에 hello 작업이 예약 됩니다. 기본적으로 리소스 관리자를 hello:

* 1/10초마다 상태를 검색하고 업데이트를 적용합니다(예: 노드가 다운된 기록).
* hello 배치 확인 플래그를 설정 
* 1 초 마다 hello 제약 조건 검사 플래그를 설정합니다.
* 분산 플래그 5 초 마다 hello를 설정 합니다.

이러한 타이머를 관리 하는 hello 구성의는 예제는 다음과 같습니다.

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

오늘 hello 클러스터 리소스 관리자만 수행 이러한 작업 중 하나가 한 번에 순차적으로 합니다. 이 때문에 "최소 간격"으로 toothese 타이머를 참조 하 고 hello 플래그로"설정" hello 타이머 꺼질 때 수행 가져오기 작업을 합니다. 예를 들어 보류 중인 클러스터 리소스 관리자를 담당 하는 hello hello 클러스터 균형 조정 하기 전에 toocreate 서비스를 요청 합니다. Hello 기본 시간 간격을 지정 하 여 볼 수 있듯이 hello 클러스터 리소스 관리자를 검사할 항목에 대해 요구 사항을 toodo 자주 합니다. 일반적으로이 중 각 단계에 변경한 hello 집합이 작은 임을 의미 합니다. 약간 변경 자주 사용 하면 클러스터 리소스 관리자 toobe hello 응답 hello 클러스터에서 상황이 발생할 때. hello 기본 타이머 제공 몇 가지 일괄 처리 다양 한 hello 이후 동일한 유형의 이벤트는 동시에 toooccur 경향이 있습니다. 

예를 들어 노드가 실패할 경우 전체 장애 도메인 작업을 한 번에 수행할 수 있습니다. 이러한 오류는 hello 다음 상태로 도중 캡처하는 모든 업데이트 hello 후 *PLBRefreshGap*합니다. hello, 배치 제약 조건 검사 하 고 실행을 분산 하는 동안 hello 수정 사항이 결정 됩니다. 기본 hello로 클러스터 리소스 관리자는 hello 클러스터의 변경 사항 시간 알아보기가 및 tooaddress 모든 변경 내용을 한 번에 시도 되지 않는 합니다. 이렇게 하면 toobursts는 변동 될 것입니다.

hello 클러스터 리소스 관리자도 필요 몇 가지 추가 정보 toodetermine hello 클러스터 경우 균형이 맞지 않는 합니다. 이를 위해 *BalancingThresholds(분산 임계값)*과 *ActivityThresholds(활동 임계값)*의 다른 두 가지 구성 요소가 있습니다.

## <a name="balancing-thresholds"></a>분산 임계값
균형 조정 임계값은 hello를 리 밸런스 트리거하 주 제어 합니다. hello 메트릭에 대 한 균형 조정 임계값은 한 _비율_합니다. 노드 초과 하는 해당 메트릭이 hello에 메트릭에 대 한 hello 부하 가장 적은 hello에 hello 양의 부하로 나눈 값 노드를 로드 하는 경우 *BalancingThreshold*, hello 클러스터 불균형 됩니다. 결과적으로 균형 조정은 트리거된 hello 다음 시간 hello 클러스터 리소스 관리자를 확인 합니다. hello *MinLoadBalancingInterval* 타이머 얼마나 자주 hello 클러스터 리소스 관리자 확인 해야 균형 조정이 필요한 경우를 정의 합니다. 확인은 아무 것도 발생하지 않는다는 의미입니다. 

균형 조정 임계값 메트릭을 당 별로 hello 클러스터 정의의 일부로 정의 됩니다. 메트릭에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요.

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![분산 임계값 예][Image1]
</center>

이 예제에서는 각 서비스에서 한 단위의 메트릭을 사용합니다. Hello 상위 예에서 노드에서 hello 최대 부하는 5 하 고 hello 최소값은 2입니다. 이 메트릭에 대 한 임계값을 분산 하는 hello는 3 개입니다 경우를 가정해 봅니다. Hello 클러스터에서 hello 비율이 5/2 이므로 = 2.5 및 즉 hello 3 hello 클러스터의 임계값을 분산 균형이 조정 된 지정 된 것 보다 작습니다. 분산 없음은 hello 클러스터 리소스 관리자를 확인 하는 경우에 트리거됩니다.

Hello 아래 예제에서는 노드의 최대 부하 hello은 hello 최소값은 2, 5의 비율이 동안 10,입니다. 포함 된 5의 경우 해당 메트릭에 대 한 세 hello 지정 된 균형 조정 임계값 보다 큽니다. 결과적으로, 균형 조정 실행 되는 예약 된 다음 번 hello 타이머 발생 균형 조정 됩니다. 이런 경우 몇 가지 부하가 tooNode3 일반적으로 분산된 합니다. 서비스 패브릭 클러스터 리소스 관리자 hello greedy 접근 방식을 사용 하지 않습니다, 때문에 일부 부하 분산된 tooNode2 수도 있습니다. 

<center>
![분산 임계값 예제 작업][Image2]
</center>

> [!NOTE]
> "분산"은 클러스터에서 로드를 관리하기 위한 두 가지 전략을 처리합니다. 클러스터 리소스 관리자 사용 하 여 hello hello 기본 전략은 hello 클러스터의 hello 노드에서 toodistribute load입니다. hello 다른 전략은 [조각 모음](service-fabric-cluster-resource-manager-defragmentation-metrics.md)합니다. Hello 중 조각 모음을 실행 하는 동일한 분산 실행 합니다. hello 분산과 조각 모음 전략에 사용할 수 있습니다 다른 메트릭은 hello 동일한 클러스터입니다. 서비스에서는 분산 및 조각 모음 메트릭을 모두 사용할 수 있습니다. 조각 모음 메트릭에 대 한 hello의 hello 비율 로드 되었을 때를 리 밸런스 hello 클러스터 트리거 _아래_ hello 임계값 균형 조정 합니다. 
>

임계값을 분산 하는 hello 아래 가져오는 것은 명시적 목표 아닙니다. 분산 임계값은 *트리거*입니다. 실행 부하를 분산 시키는 hello 클러스터 리소스 관리자 있는 경우 수행할 수 있는 향상 된 기능을 결정 합니다. 분산 검색이 시작되었기 때문에 어떤 항목도 이동하지 않는다는 의미는 아닙니다. 경우에 따라 hello 클러스터는 불균형 하지만 너무 제한 된 toocorrect입니다. Hello 향상도 이동 해야 하는 또는 [비용이 많이 드는](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>활동 임계값
노드는 비교적 불균형, 경우에 따라 hello *총* hello 클러스터의 부하의 양은 적습니다. 자격 증명 부하 hello 부족 일시적인 dip 수 또는 hello 클러스터는 새롭고 바로 가져오기 때문에 부트스트랩 합니다. 두 경우 모두 할 필요가 거의 toobe 얻은 있기 때문에 분산 hello 클러스터 toospend 시간입니다. Hello 클러스터 분산 했습니다, 하는 경우 네트워크를 소비 하는 모든 큰 하지 않고 리소스 toomove 작업만 계산 *절대* 차이입니다. 활동 임계값으로 알려진 다른 제어 방법이 tooavoid 불필요 한 이동입니다. 활동 임계값 toospecify를 활동에 대 한 절대 하한값 몇 가지 있습니다. 노드가 없으면이 임계값을 초과 이면 hello 균형 조정 임계값을 충족 하는 경우에 발생 되지 않습니다 균형 조정 합니다.

이 메트릭에 대해 세 개의 분산 임계값을 유지한다고 가정해 보겠습니다. 활동 임계값도 1,536이라고 가정해 보겠습니다. Hello 첫 번째 경우에 hello 클러스터는 hello 당 균형이 맞지 않는 균형 조정 임계값 없는 노드 충족 활동 임계값에를 발생 하므로 아무것도 표시 되지 않음. Node1은 hello 아래 예제에서는 활동 임계값 hello 끝났습니다. 균형 조정 임계값 hello 둘 다 이므로 hello 메트릭에 대 한 hello 활동 임계값이 초과 되는 예약 된 균형 조정 합니다. 예를 들어 살펴보겠습니다 다이어그램을 다음 hello: 

<center>
![활동 임계값 예][Image3]
</center>

균형 조정 임계값와 동일 하 게 활동 임계값에는 정의 된 당-메트릭을 통해 hello 클러스터 정의

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

균형 조정 및 활동 임계값이 모두 동률된 tooa 특정 메트릭을-분산 균형 조정 임계값 hello 모두 hello에 대 한 활동 임계값을 초과 하는 경우에 트리거됩니다 동일한 메트릭을 합니다.

## <a name="balancing-services-together"></a>분산 서비스 함께 사용
Hello 클러스터 불균형 인지 여부를 클러스터 전체 의사 결정 됩니다. 그러나 개별 서비스 복제본과 인스턴스 문제를 해결 하는 방법에 대 한 있네요 hello 방식으로 이동 합니다. 참 합리적이지 않은가요? 메모리는 한 노드에서 쌓입니다, 여러 복제본 또는 인스턴스 tooit을 원인이 수 있습니다. 해결 hello 불균형 hello 상태 저장 복제본 또는 hello 균형이 맞지 않는 메트릭을 사용 하는 상태 비저장 인스턴스 이동 필요할 수 있습니다.

그러나을 받았으나 불균형 자체 서비스 옮긴 (hello 설명 참조의 로컬 및 전역 가중치를 이전 버전). 모든 서비스의 메트릭이 분산되었을 때 서비스가 이동하는 이유는 무엇인가요? 예를 들어 살펴보겠습니다.

- 4개 서비스, 즉 서비스 1, 서비스 2, 서비스 3 및 서비스 4를 가정해 보겠습니다. 
- 서비스 1에서 메트릭 1 및 메트릭 2를 보고합니다. 
- 서비스 2에서 메트릭 2 및 메트릭 3을 보고합니다. 
- 서비스 3에서 메트릭 3 및 메트릭 4를 보고합니다.
- 서비스 4에서 메트릭 99를 보고합니다. 

확실히 여기에 있다는 것을 알 수 있습니다. 즉 체인이 있습니다! 실제로 4개의 독립된 서비스가 있는 것이 아니라, 3개의 서비스가 관련되어 있고 하나는 자체적으로 꺼져 있습니다.

<center>
![분산 서비스 함께 사용][Image4]
</center>

이 체인으로 인해 메트릭 1-4 불균형 될 수 있다는 복제본 또는 tooservices 속하는 인스턴스가 주위 1-3 toomove 수는. 메트릭 1, 2 또는 3이 분산되지 않으므로 서비스 4에서 이동이 발생하지 않음을 알 수 있습니다. Hello 복제본 이동 이후 지점이 없는 것 하거나 수 주위 tooService4 속하는 인스턴스가 절대 tooimpact hello 균형 메트릭 1-3입니다.

자동으로 hello 클러스터 리소스 관리자는 서비스와 관련 된 찾습니다. 추가, 제거 또는 서비스에 대 한 변경 hello 메트릭 간의 관계를 달라질 수 있습니다. 예를 들어 Service2 분산의 두 실행 간의 되었을 수 있습니다 Metric2 tooremove를 업데이트 합니다. Service1와 Service2 사이의 hello 체인을 중단합니다. 이제는 관련된 두 개의 서비스 그룹 대신 세 개 그룹이 있습니다.

<center>
![분산 서비스 함께 사용][Image5]
</center>

## <a name="next-steps"></a>다음 단계
* 메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다. 메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 및 [이 문서](service-fabric-cluster-resource-manager-metrics.md)
* 이동 비용은 하나의 방법 특정 서비스는 다른 항목 보다 더 비용이 많이 드는 toomove toohello 클러스터 리소스 관리자 신호입니다. 이동 비용에 대 한 자세한 참조 너무[이 문서](service-fabric-cluster-resource-manager-movement-cost.md)
* hello 클러스터 리소스 관리자에는 몇 가지 스로틀 hello 클러스터에서 변동 아래로 tooslow를 구성할 수 있습니다. 일반적으로 필요하지는 않지만 필요할 경우 [여기](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
