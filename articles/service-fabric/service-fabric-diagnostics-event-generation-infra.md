---
title: "서비스 패브릭 플랫폼 수준 모니터링 aaaAzure | Microsoft Docs"
description: "Azure 서비스 패브릭 클러스터를 진단 및 플랫폼 수준 이벤트 및 로그 사용 되는 toomonitor 알아보십시오."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>플랫폼 수준 이벤트 및 로그 생성

## <a name="monitoring-hello-cluster"></a>Hello 클러스터 모니터링

것이 중요 한 toomonitor hello 플랫폼 수준 toodetermine 예상 대로 하드웨어 및 클러스터는 작동 되는 여부에 합니다. 서비스 패브릭에서 하드웨어 오류 발생 시 실행 중인 응용 프로그램을 유지할 수는 있지만 있지만 여전히 필요 하면 toodiagnose hello 기본 인프라 또는 응용 프로그램에서 오류가 발생 하는지 여부를 합니다. 도 모니터링 해야 하는 클러스터 toobetter 계획 용량을 추가 하거나 하드웨어를 제거 하는 방법에 대 한 결정에 도움이 되.

서비스 패브릭에서는 5 개의 서로 다른 로그 채널-의-즉시 hello 다음 이벤트를 생성 하는 제공 합니다.

* 운영 채널: 서비스 패브릭 클러스터 hello 예정 배포 되는 새 응용 프로그램 노드에 대 한 이벤트를 포함 하 여 수행 하는 상위 수준 작업 또는 업그레이드 롤백 등 SF 합니다.
* 작동 채널 - 상세: 상태 보고서 및 부하 분산 결정
* 데이터 및 메시징 채널: 중요 한 로그 및 우리의 (현재만 hello ReverseProxy) 메시징 및 데이터 경로 (신뢰할 수 있는 서비스 모델)에서 생성 된 이벤트
* 세부 데이터 및 메시징 채널-: 모든 hello 중요 하지 않은 로그 데이터 및 메시징 (이 채널에는 매우 많은 양의 이벤트) hello 클러스터에 포함 된 자세한 채널   
* [Reliable Services 이벤트](service-fabric-reliable-services-diagnostics.md): 프로그래밍 모델 특정 이벤트
* [Reliable Actors 이벤트](service-fabric-reliable-actors-diagnostics.md): 프로그래밍 모델 특정 이벤트 및 성능 카운터
* 로그를 지원 합니다: 서비스 패브릭만 toobe 지원을 제공 하는 경우 미국에서 사용 하 여 생성 된 시스템 로그

이러한 다양 한 채널 설명 hello 플랫폼 수준 로깅 기능 최대한 활용 하는 것이 좋습니다. 로깅, tooimprove 플랫폼 수준 고려와에 투자 더 나은 hello 상태 모델 이해 및 사용자 지정 상태 보고서 추가 하는 추가 사용자 지정 **÷ ´ ֹ** toobuild에 영향을 hello에 대 한 실시간 이해 서비스와 hello 클러스터에서 응용 프로그램입니다.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Azure Service Fabric 상태 및 로드 보고

Service Fabric에는 다음과 같은 문서에서 자세히 설명하는 자체의 상태 모델이 있습니다.
- [소개 tooService 패브릭 상태 모니터링](service-fabric-health-introduction.md)
- [서비스 상태 보고 및 확인](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [사용자 지정 서비스 패브릭 상태 보고서 추가](service-fabric-report-health.md)
- [서비스 패브릭 상태 보고서 보기](service-fabric-view-entities-aggregated-health.md)

상태 모니터링은 서비스 운영에 중요 한 toomultiple 측면입니다. 상태 모니터링은 Service Fabric에서 명명된 응용 프로그램 업그레이드를 수행할 때 특히 중요합니다. 각 업그레이드 도메인의 hello 서비스를 업그레이드 하 고는 사용 가능한 tooyour 고객, 후 toohello 다음 업그레이드 도메인 이동 하는 hello 배포 하기 전에 hello 업그레이드 도메인 상태 검사를 통과 해야 합니다. 정상 상태를 얻을 수 없는 경우 hello 응용 프로그램은 알려진, 좋은 상태에 있도록 hello 배포 다시 롤백됩니다. 일부 고객 hello 서비스 롤백됩니다 전에 영향을 받을 수, 하지만 대부분의 고객 문제가 발생 하지 않습니다. 또한 해상도 비교적 빠르고 toowait 교환원의 동작에 대 한 필요 없이 발생 합니다. hello hello 복원 성도 뛰어납니다. 서비스 toodeployment 문제는 코드에 통합 되어 더 많은 상태 검사 합니다.

서비스 상태의 또 다른 측면은 hello 서비스에서 메트릭을 보고 합니다. 메트릭은 toobalance 사용 되는 리소스 사용 되기 때문에 서비스 패브릭에서 중요 합니다. 또한 메트릭은 시스템 상태 표시기가 될 수 있습니다. 예를 들어 많은 서비스가 있는 응용 프로그램을 가질 수 있으며, 각 인스턴스에서 RPS(초당 요청 수)를 보고합니다. 서비스 패브릭 이동 hello 클러스터 서비스 인스턴스 하나 사용 하는 경우 다른 서비스 보다 더 많은 리소스, tootry toomaintain에도 리소스 사용률입니다. 리소스 사용률이 작동하는 방식에 대한 자세한 설명은 [메트릭을 사용하여 Service Fabric에서 리소스 부하 및 소비 관리](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.

또한 메트릭을 통해 서비스 수행 방식에 대한 통찰력을 얻을 수도 있습니다. 시간이 지남에 따라 hello 서비스가 예상된 매개 변수 내에서 작동 하는 메트릭을 toocheck를 사용할 수 있습니다. 예를 들어 추세를 표시 하는 hello 월요일 아침에 오전 9 시에 평균 RPS는 1, 000 인 경우 hello RPS는 500 또는 1, 500 벗어나는 경우 경고를 표시 하는 상태 보고서를 설정할 수 있습니다. 모든 완벽 하 않을 수 있지만 고객의 경험 발생 하는 있는지는 확인 toobe 두면 유용할 수 있습니다. 서비스 상태 확인을 위해 보고 될 수 있지만 hello hello 클러스터의 리소스 균형 조정에 영향을 주지는 메트릭 집합을 정의할 수 있습니다. toodo이, 집합 hello 메트릭 가중치 toozero 합니다. 모든 메트릭 가중치 0을 시작 hello 가중치를 늘리지 아닌 경우 hello 메트릭 가중치 클러스터에 대해 분산 리소스에 미치는 영향을 이해 해야 하는 것이 좋습니다.

> [!TIP]
> 너무 높은 가중치가 적용된 메트릭은 사용하지 마세요. 이유 서비스 인스턴스 이동 하는 분산 용 어려운 toounderstand 수 있습니다. 몇 가지 메트릭에는 많은 시간이 걸릴 수 있습니다.

응용 프로그램의 hello 상태와 성능을 나타낼 수 있는 모든 정보는 메트릭 및 상태 보고서에 대 한 후보입니다. CPU 성능 카운터는 노드가 활용되는 상태를 알려주지만 단일 노드에서 여러 서비스가 실행될 수 있기 때문에 특정 서비스의 상태가 정상인지 여부는 알려주지 않습니다. 하지만, 및는 메트릭 RPS, 처리, 항목 같은 모든 요청 대기 시간에 특정 서비스의 hello 상태를 나타낼 수 있습니다.

사용 하 여 코드와 유사한 toothis tooreport 상태:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

메트릭을 tooreport 유사한 toothis 코드를 사용 합니다.

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Service Fabric 지원 로그

Azure 서비스 패브릭 클러스터와 toocontact Microsoft 지원에 대 한 도움말 해야 할 경우 지원 로그는 거의 언제나 필요 합니다. 클러스터가 Azure에서 호스팅되는 경우 클러스터를 만드는 과정의 일부로 이러한 로그를 자동으로 구성하여 수집합니다. hello 로그는 클러스터의 리소스 그룹에는 전용된 저장소 계정에 저장 됩니다. hello 저장소 계정에는 고정된 이름 없는 하지만 hello 계정에 blob 컨테이너 및로 시작 하는 이름 가진 테이블 표시 *패브릭*합니다. 독립 실행형 클러스터의 로그 수집 설정에 대한 자세한 내용은 [독립 실행형 Azure Service Fabric 클러스터 만들기 및 관리](service-fabric-cluster-creation-for-windows-server.md) 및 [독립 실행형 Windows 클러스터에 대한 구성 설정](service-fabric-cluster-manifest.md)을 참조하세요. 독립 실행형 서비스 패브릭 인스턴스에 대 한 hello 로그 tooa 로컬 파일 공유를 전송 합니다. **필요한** toohave 이러한 로그에 대 한 지원, 있지만 의도 한 toobe 외부 hello Microsoft 고객 지원 팀에서 모든 사용자가 사용할 수 없는 합니다.

## <a name="enabling-diagnostics-for-a-cluster"></a>클러스터에 대한 진단 사용

이러한 로그의 순서 tootake 혜택에 클러스터를 만드는 동안 "진단"를 사용할 수 있음을 것이 좋습니다. 진단을 설정 하 여 hello 클러스터를 배포할 때 Windows Azure 진단 수 tooacknowledge hello Operational, 신뢰할 수 있는 서비스 및 Reliable actors 채널은 및에서 자세히 설명한 것 처럼 저장소 hello 데이터 [사용 하 여 이벤트를 집계 합니다. Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md)합니다.

위의 예제와 같이 이기도 선택적 필드 tooadd 응용 프로그램 통찰력 (AI) 계측 키 합니다. 모든 이벤트 분석을 위한 AI toouse를 선택 하는 경우 (이에 대 한 자세한 [Application Insights를 사용 하 여 이벤트 분석](service-fabric-diagnostics-event-analysis-appinsights.md)), 여기에 hello AppInsights 리소스 instrumentationKey (GUID)를 포함 합니다.


Toodeploy 컨테이너 tooyour 클러스터를 사용 하도록 하려는 경우이 tooyour "WadCfg > DiagnosticMonitorConfiguration"를 추가 하 여 docker 통계를 WAD toopick 사용:

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>성능 측정

클러스터의 성능을 측정 클러스터를 확장에 관한 수 toohandle 부하 및 드라이브 결정은 방법을 이해 하는 데 도움이 됩니다 (클러스터 크기 조정에 대 한 자세한 참조 [Azure에서](service-fabric-cluster-scale-up-down.md), 또는 [온-프레미스](service-fabric-cluster-windows-server-add-remove-nodes.md)). 성능 데이터를 유용한 경우에 비해 tooactions 또는 응용 프로그램 되며 서비스 될 수 있기를 hello에 대 한 로그 분석 시 이후. 

서비스 패브릭을 사용 하는 경우 성능 카운터 toocollect 목록은 참조 [서비스 패브릭에서 성능 카운터](service-fabric-diagnostics-event-generation-perf.md)

클러스터에 대한 성능 데이터 수집을 설정하는 두 가지 일반적인 방법은 다음과 같습니다.

* 에이전트를 사용 하 여:이 컴퓨터에서 성능 수집 hello 기본 설정 방법, toocollect 원하는 에이전트 일반적으로 수집할 수 있는 가능한 성능 메트릭 목록이 있고 되는 상대적으로 쉬운 프로세스 toochoose hello 메트릭 이후 또는 변경 . 에 대 한 읽기 [tooconfigure OMS 서비스 패브릭 용 hello 하는 방법을](service-fabric-diagnostics-event-analysis-oms.md) 및 [hello OMS Windows 에이전트 설정](../log-analytics/log-analytics-windows-agents.md) 위에 toopick 수 있는 이러한 하나의 모니터링 에이전트가 hello OMS 에이전트에 대 한 자세한 문서 toolearn 클러스터 Vm 및 배포 된 컨테이너에 대 한 성능 데이터입니다.

* Tooa 테이블 카운터 toowrite 성능 진단 구성: Azure에서 클러스터의 경우 즉, 클러스터의 Vm hello에서 hello Azure 진단 구성 toopick hello 적절 한 성능 카운터를 변경 하 고 위로 toopick 사용 모든 컨테이너를 구축 하려는 경우 docker 통계입니다. 구성에 대 한 읽기 [WAD에서 성능 카운터](service-fabric-diagnostics-event-aggregation-wad.md) 성능 카운터 수집을 서비스 패브릭 tooset에 있습니다.

## <a name="next-steps"></a>다음 단계

로그 및 이벤트 필요 toobe 집계 전에 tooany 분석 플랫폼 보낼 수 있습니다. 에 대 한 읽기 [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) 및 [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter hello 권장 옵션 중 일부를 이해 합니다.
