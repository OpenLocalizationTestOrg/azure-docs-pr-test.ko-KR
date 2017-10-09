---
title: "aaaAzure 서비스 패브릭 모니터링 및 진단 개요 | Microsoft Docs"
description: "Azure Service Fabric 클러스터, 응용 프로그램 및 서비스에 대한 모니터링 및 진단에 대해 알아봅니다."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Azure Service Fabric 모니터링 및 진단

모니터링 및 진단 테스트 및 응용 프로그램 및 모든 환경에서 서비스 배포의 중요 한 toodeveloping 됩니다. Service Fabric 솔루션은 로컬 개발 환경 또는 프로덕션 환경에서 응용 프로그램과 서비스가 예상대로 작동하는지 확인하는 데 도움이 되는 모니터링 및 진단을 계획하고 구현할 때 가장 효과적입니다.

모니터링의 주요 목표 hello 및 진단에:
* 하드웨어 및 인프라 문제 감지 및 진단
* 소프트웨어 및 앱 문제 감지, 서비스 가동 중지 시간 감소
* 리소스 사용량 이해 및 적절한 작업 의사 결정 유도
* 응용 프로그램, 서비스 및 인프라 성능 최적화
* 비즈니스 통찰력 생성 및 향상 가능 영역 식별


모니터링의 전체 워크플로 hello 및 진단 세 단계로 구성 됩니다.

1. **이벤트 생성**: 여기에 이벤트 (로그, 추적, 사용자 지정 이벤트) hello 인프라 (클러스터), 플랫폼 및 응용 프로그램 / 서비스 수준에서
2. **이벤트 집계**: 생성 된 이벤트 수집 및 집계 표시 하려면 먼저 toobe 필요
3. **분석**: 할 이벤트 toobe 시각화 된 있고 일부 형식, tooallow에 액세스할 수 있는 분석 및 필요에 따라 디스플레이 대 한

여러 개의 제품을 이러한 세 가지 영역을 포함 하는 사용할 수 있는 고 각각에 대해 무료 toochoose 다양 한 기술을 있습니다. 것이 중요 한 toomake 하는 다양 한 부분 작업 함께 toodeliver 클러스터에 대 한 종단 간 모니터링 솔루션은 hello 있는지 합니다.

## <a name="event-generation"></a>이벤트 생성

hello 모니터링 및 진단 워크플로 hello 첫 번째 단계에는 hello 생성 및 생성 이벤트 및 로그입니다. 이러한 이벤트, 로그 및 추적 두 수준에서 생성 됩니다: hello 플랫폼 레이어 (hello 클러스터, hello 컴퓨터 또는 서비스 패브릭 작업 포함) 또는 응용 프로그램 계층 hello (모든 계측 tooapps 및 서비스 배포 toohello 클러스터 추가 됨). Service Fabric은 기본적으로 일부 계측을 제공하지만 각 수준의 이벤트를 사용자 지정할 수 있습니다.

에 대해 자세히 알아보세요 [플랫폼 수준 이벤트](service-fabric-diagnostics-event-generation-infra.md) 및 [응용 프로그램 수준 이벤트](service-fabric-diagnostics-event-generation-app.md) tooadd 계측을 추가 하는 방법 및 toounderstand 제공 하는 것입니다.

Toomake 로그 되는 있는지 hello toouse 원하는 공급자를 로깅에 적절 한 확인 한 후 필요한 집계 하 고 올바르게 저장 합니다.

## <a name="event-aggregation"></a>이벤트 집계

Hello 로그 및 응용 프로그램 및 클러스터에서 생성 하는 이벤트를 수집 하려는 일반적으로 사용할 수 있는 권장 [Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md) (유사한 tooagent 기반 로그 수집) 또는 [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(in process 로그 컬렉션).

Azure 진단 확장을 사용 하 여 응용 프로그램 로그를 수집의 서비스 패브릭 서비스에 적합 한 옵션 로그 소소의 hello 설정 하는 경우 대상 자주 변경 되지 않는 및 hello 원본과 대상 간에 간단한 매핑이 지원 됩니다. hello 이유가를 구성 하 고 Azure 진단에 대 한 발생 하는 hello 리소스 관리자 계층에서 함으로써 중요 한 변경 toohello 구성 hello 클러스터 업데이트/재배포 필요 합니다. 또한 로그를 다양한 분석 플랫폼에서 액세스할 수 있고 좀 더 영구적으로 저장할 수 있는 위치에 저장하면 가장 잘 활용할 수 있습니다. 이는 EventFlow와 같은 옵션을 사용하는 것보다 파이프라인의 효율성이 떨어지는 것을 의미합니다.

사용 하 여 [EventFlow](https://github.com/Azure/diagnostics-eventflow) 허용 하면 toohave 서비스 로그를 직접 보낼 tooan 분석 및 시각화 플랫폼 및/또는 toostorage 합니다. 다른 라이브러리 (ILogger, Serilog, 등)는 사용할 수 hello에 대 한 동일한 목적으로 있지만 EventFlow 이점이 hello 프로세스에서 로그 수집 및 toosupport 서비스 패브릭 서비스에 대 한 디자인 된 것입니다. 이 방법이 toohave 몇 가지 잠재적인 이점이 있습니다.

* 쉬운 구성 및 배포
    * 진단 데이터 수집의 hello 구성은 hello 서비스 구성의 일부입니다. hello 응용 프로그램의 놓을 것 "동기화" hello로 쉽게 tooalways 유지
    * 응용 프로그램당 또는 서비스당 구성은 쉽게 달성할 수 있습니다.
    * 데이터 대상 EventFlow 통해 구성은 hello 적절 한 NuGet 패키지를 추가 하 고 hello 변경 만으로 *eventFlowConfig.json* 파일
* 유연성
    * hello 응용 프로그램 데이터 보낼 수 있습니다 hello toogo, 필요한 경우 항상으로 hello 대상 데이터 저장소 시스템을 지 원하는 수 있는 클라이언트 라이브러리입니다. 새로운 대상을 원하는 대로 추가할 수 있습니다.
    * 복잡한 캡처, 필터링 및 데이터 집계 규칙을 구현할 수 있습니다.
* 액세스 toointernal 응용 프로그램 데이터와 컨텍스트
    * hello 진단 하위 시스템 hello 응용 프로그램/서비스 프로세스 내에서 실행 컨텍스트 정보를 사용 하 여 hello 추적을 쉽게 추가할 수 있습니다.

한 가지 toonote은 이러한 두 옵션은 함께 가능한 tooget 하나를 사용 하 여 완료 한 후에 비슷한 작업 또는 다른 hello, 그 수 또한 사용자에 게 의미가 방법과 tooset입니다. 대부분의 경우 에이전트 프로세스에서 컬렉션으로 결합 tooa 안정적 수 워크플로 모니터링 될 수 있습니다. Azure 진단 확장 (에이전트) hello 수 플랫폼 수준 로그에 대 한 선택한 경로 EventFlow (in process 컬렉션)를 사용할 수도 있지만 응용 프로그램 로그에 대 한 있습니다. 가장 적합 한 있습니다 알게 될, 표시 및 분석 하 여 데이터 toobe 용도 대 한 시간 toothink이 있습니다.

## <a name="event-analysis"></a>이벤트 분석

모니터링 및 진단 데이터의 toohello 분석 및 시각화 있어 hello 시장에 존재 하는 몇 가지 훌륭한 플랫폼 가지가 있습니다. hello 두 가지 권장 되는 [OMS](service-fabric-diagnostics-event-analysis-oms.md) 및 [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tootheir와의 통합 서비스 패브릭 있지만 인해 또한 살펴보아야 hello [탄력적 스택](https://www.elastic.co/products) (특히 고려 하는 경우 오프 라인 환경에서 실행 하는 클러스터), [Splunk](https://www.splunk.com/), 또는 다른 플랫폼의 기본 설정 합니다.

hello 요점에 모든 플랫폼을 선택 해야 hello 사용자 인터페이스 및 쿼리 하는 옵션을 사용 하 여는 방법을 모두에 포함 되어 기능 toovisualize 데이터 hello 하 고 쉽게 읽을 수 있는 대시보드를 만들 하며 hello 추가 도구 제공 tooenhance 프로그램 자동화 된 경고 모니터링 합니다.

또한 toohello 플랫폼을 선택 하면 Azure 리소스로 서비스 패브릭 클러스터를 설정 하는 경우에 액세스 tooAzure 기본적으로 특정 성능에 대 한 유용할 수 있는 컴퓨터에 대 한 모니터링 및 얻게 메트릭 모니터링 합니다.

### <a name="azure-monitor"></a>Azure Monitor

사용할 수 있습니다 [Azure 모니터](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor 서비스 패브릭 클러스터 기반이 되는 Azure 리소스를 hello 다양 합니다. Hello에 대 한 메트릭 집합이 [가상 컴퓨터 크기 집합](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) 및 개별 [가상 컴퓨터](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) 자동으로 수집 되 고 hello Azure 포털에에서 표시 합니다. tooview hello hello Azure 포털 hello 서비스 패브릭 클러스터를 포함 하는 선택 hello 리소스 그룹의에서 정보를 수집 합니다. 그런 다음 선택 hello 가상 컴퓨터 크기 집합 tooview 되도록 합니다. Hello에 **모니터링** 섹션에서 **메트릭** tooview hello 값에 대 한 그래프입니다.

![수집된 메트릭 정보의 Azure Portal 보기](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

toocustomize hello 차트 hello 지침에 따라 [Microsoft Azure에서 메트릭](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)합니다. 또한 [Azure Monitor에서 Azure 서비스에 대한 알림 만들기](../monitoring-and-diagnostics/insights-alerts-portal.md)에서 설명한 대로 이러한 메트릭을 기반으로 하여 알림을 만들 수 있습니다. 에 설명 된 대로 웹 후크를 사용 하 여 tooa 알림 서비스 경고를 보낼 수 [메트릭 경고 Azure에 웹 후크로 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다. Azure Monitor는 하나의 구독만 지원합니다. 여러 구독 toomonitor 필요한 경우 또는 추가 기능이 필요한 경우 [로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/), 파트를 온-프레미스와 클라우드 기반 Microsoft Operations Management Suite의 전체적인 IT 관리 솔루션 제공 인프라입니다. Azure 모니터에서 데이터를 전달할 수 있습니다 직접 tooLog 분석, 한 곳에 전체 환경에 대 한 메트릭 및 로그를 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

### <a name="watchdogs"></a>Watchdog

그런 다음 안정성은는 별도 서비스 상태를 관찰할 수 있으며 서비스 및 보고서 상태 간에 부하를 hello 상태 모델 계층 구조에서 모든 항목입니다. 이 단일 서비스의 hello 보기를 기준으로 검색 되지 않는 오류를 방지할 수 있습니다. Watchdogs (예: 저장소에서 로그 파일을 정리 하는 특정 시간 간격) 사용자 상호 작용 없이 수정 작업을 수행 하는 것이 좋습니다 toohost 코드도 있습니다. [여기](https://github.com/Azure-Samples/service-fabric-watchdog-service)에서 샘플 watchdog 서비스 구현을 찾을 수 있습니다.

Hello에 이벤트 및 로그 가져오기 생성 하는 방법을 이해 시작 [플랫폼 수준](service-fabric-diagnostics-event-generation-infra.md) 및 hello [응용 프로그램 수준](service-fabric-diagnostics-event-generation-app.md)합니다.
