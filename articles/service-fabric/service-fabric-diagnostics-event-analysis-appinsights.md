---
title: "Application Insights를 사용 하 여 서비스 패브릭 이벤트 분석 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터의 모니터링 및 진단을 위해 Application Insights를 사용하여 이벤트를 시각화 및 분석하는 방법에 대해 알아봅니다."
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Application Insights를 사용하여 이벤트 분석 및 시각화

Azure Application Insights는 응용 프로그램 모니터링 및 진단을 위한 확장 가능한 플랫폼입니다. 여기에는 강력한 분석 및 쿼리 도구, 사용자 지정 가능한 대시보드 및 시각화, 자동화된 경고 등의 추가 옵션이 포함됩니다. 이 권장 모니터링 하기 위한 플랫폼 및 서비스 패브릭 응용 프로그램 및 서비스에 대 한 진단 hello입니다.

## <a name="setting-up-application-insights"></a>Application Insights 설정

### <a name="creating-an-ai-resource"></a>AI 리소스 만들기

Azure 마켓플레이스 toohello 및 "Application Insights" 검색을 통해 헤드는 AI toocreate 리소스입니다. Hello 첫 번째 솔루션 (에 "웹 + 모바일" 범주 아래)으로 보입니다. 클릭 **만들기** hello 오른쪽 리소스를 찾을 때 (사용자의 경로 아래 hello 이미지와 일치 하는지 확인).

![새 Application Insights 리소스](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

몇 가지 정보 tooprovision hello 리소스 아웃 toofill 올바르게 필요 합니다. Hello에 *응용 프로그램 종류* "ASP.NET 웹 응용 프로그램"를 사용 하 여 사용 하려는 서비스 패브릭의 경우의 프로그래밍 모델 또는 게시 하는.NET 응용 프로그램 toohello 클러스터에는 필드입니다. 게스트 실행 파일과 컨테이너를 배포하려면 "일반"을 사용합니다. 일반적으로 기본 toousing "ASP.NET 웹 응용 프로그램" tookeep 옵션에서에서 열기 이후 hello hello 이름은 tooyour 우선, 위로 이며 hello 리소스 그룹 및 구독을 모두는 hello 리소스의 배포 후 변경할 수 없습니다. AI 리소스가 hello 인지 하는 것이 좋습니다 클러스터와 동일한 리소스 그룹입니다. 자세한 내용은 [Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.

이벤트 집계 도구와 hello AI 계측 키 tooconfigure AI 해야합니다. AI 리소스가 (hello 배포의 유효성을 검사 한 후 몇 분이 걸립니다) 설정 되 고 나면 tooit 이동한 hello **속성** hello 왼쪽된 탐색 모음에서 섹션. *계측 키*를 보여 주는 새 블레이드가 열립니다. Toochange hello 구독 또는 hello 리소스의 리소스 그룹을 해야 하는 경우 수행할 수 있습니다 여기 뿐입니다.

### <a name="configuring-ai-with-wad"></a>WAD를 사용하여 AI 구성

두 가지 기본 단계에서 설명한 대로 AI 싱크 toohello WAD 구성을 추가 하 여 이루어집니다 WAD tooAzure AI에서에서 toosend 데이터 [이 여기서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)합니다.

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Azure Portal에서 클러스터를 만들 때 AI 계측 키 추가

![AIKey 추가](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

클러스터 진단 "on"으로 설정 되어 있으면를 만들 때 필드는 선택 사항 tooenter 응용 프로그램 Insights 계측 키가 표시 됩니다. 여기에 AI IKey에 붙여 넣으면 hello AI 싱크에 자동으로 지워집니다 자동으로 구성에 사용 되는 toodeploy hello 리소스 관리자 템플릿을 클러스터입니다.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Hello AI 싱크 toohello 리소스 관리자 템플릿 추가

리소스 관리자 템플릿 hello "WadCfg" hello에서 다음 두 가지 변경 내용이 hello를 포함 하 여 "Sink"를 추가 합니다.

1. Hello 싱크 구성 추가:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. 다음 줄에 "DiagnosticMonitorConfiguration" hello "WadCfg" hello의 추가 하 여 hello를 싱크 DiagnosticMonitorConfiguration hello에 포함 시킵니다.

    ```json
    "sinks": "applicationInsights"
    ```

Hello 위의 두 hello 코드 조각에 사용 되는 toodescribe hello 싱크 된 이름은 "applicationInsights"입니다. 필요 하지 않습니다 및 hello 이름 tooany 문자열 hello 싱크의 hello 이름을 "싱크" ´ â,으로 설정할 수 있습니다.

현재 로그 hello 클러스터에서로 표시 됩니다 AI의 로그 뷰어에서 추적을 살펴보세요. 대부분의 hello 플랫폼에서 들어오는 hello 추적 수준 "Informational" 이므로 "Critical" 또는 "Error" 유형의 hello 싱크 구성 tooonly 송신 로그 변경을 고려해볼 수도 있습니다. 이렇게 "채널" tooyour 싱크를 추가 하 여에서 같이 [이 여기서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)합니다.

>[!NOTE]
>잘못 된 AI IKey을 포털에서 또는 리소스 관리자 템플릿을 사용 하면 toomanually hello 키 변경 / 업데이트 hello 클러스터 및 다시 배포 해야 합니다. 

### <a name="configuring-ai-with-eventflow"></a>EventFlow를 사용하여 AI 구성

EventFlow tooaggregate 이벤트를 사용 하는 경우 확인 되었는지 tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 패키지 합니다. hello 다음에 hello에 포함 된 toobe *출력* hello 섹션 *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

필터를 있는지 toomake hello 필요한 변경 작업을 수행할으로 해당 NuGet 패키지) (함께 다른 입력을 포함 합니다.

## <a name="aisdk"></a>AI.SDK

일반적으로 toouse EventFlow 좋습니다 및 집계 솔루션으로 WAD 모듈식 방법 toodiagnostics을 허용 하 고 실제 변경 tooyour 없습니다 필요한 경우에 모니터링, 즉, toochange EventFlow 프로그램 출력을 원하는, 때문에 계측을 간단히 수정 tooyour config 파일 뿐입니다. 하지만 tooinvest Application Insights를 사용 하 여 결정 없는 가능성이 toochange tooa 다른 플랫폼을 하는 경우 AI의 새 SDK를 사용 하 여 이벤트를 집계 하 고 tooAI 보내 살펴보아야 합니다. 즉, 사용자가 더 이상 tooconfigure EventFlow toosend 사용자 데이터 tooAI 있지만 대신 hello ApplicationInsight 서비스 패브릭 NuGet 패키지 설치 합니다. Hello 패키지에 대 한 자세한 내용은 [여기](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)합니다.

[Application Insights Microservices 및 컨테이너에 대 한 지원](https://azure.microsoft.com/app-insights-microservices/) 일부를 보여 줍니다 (여전히 현재 베타) 작업 중인 하는 새로운 기능 hello, 수 있도록 허용 하기 AI와 toohave 제공 하는 기본적으로 다양 한 모니터링 옵션입니다. 여기에 추적 (더 나은 매크로나 hello에서 문제에 사용 하면 서비스에서 오는의 더 나은 상관 관계 및 종속성 추적 (모든 서비스 및 응용 프로그램 간에 클러스터 및 hello 통신의 AppMap 작성에 사용 됨) 워크플로 응용 프로그램 또는 서비스의)입니다.

.NET에서 개발 하는 고 될 경우 일부 서비스 패브릭 프로그래밍 모델을 사용 하며 기꺼이 toouse AI를 시각화 하는 이동 hello를 통해 모니터링으로 AI SDK 경로 것이 좋습니다 이벤트 및 로그 데이터를 분석 하기 위한 플랫폼 및 진단 워크플로입니다. 읽기 [이](../application-insights/app-insights-asp-net-more.md) 및 [이](../application-insights/app-insights-asp-net-trace-logs.md) tooget AI toocollect를 사용 하 여 시작 하 고 로그를 표시 합니다.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Hello AI 리소스가 Azure 포털에서 탐색

AI 이벤트 및 로그에 대 한 출력으로 구성한 후 정보 시작 해야 tooshow AI 리소스가 몇 분 후에서입니다. 이 하면 toohello AI 리소스 대시보드를 toohello AI 리소스를 이동 합니다. 클릭 **검색** hello AI 작업 표시줄 toosee hello 최신 하는 추적, 수신한 및 toobe 수 toofilter 표시가 있습니다.

*메트릭 탐색기*는 응용 프로그램, 서비스 및 클러스터가 보고할 수 있는 메트릭을 기반으로 사용자 지정 대시보드를 만드는 데 유용한 도구입니다. 참조 [Application Insights에서 메트릭을 탐색](../application-insights/app-insights-metrics-explorer.md) 자신에 대 한 몇 가지 차트를 tooset hello 데이터를 수집 하는 기준입니다.

클릭 하면 **분석** 걸립니다 toohello 응용 프로그램 통찰력 분석 포털 이벤트 및 큰 범위 및 옵션을 사용 하 여 추적을 쿼리할 수 있습니다. 자세한 내용은 [Application Insights의 분석](../application-insights/app-insights-analytics.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [AI에서 경고를 설정](../application-insights/app-insights-alerts.md) toobe 변경 성능 및 사용 현황에 대 한 알림이 표시
* [Application Insights에서 검색을 스마트](../application-insights/app-insights-proactive-diagnostics.md) 사전 분석 tooAI toowarn 송신할 hello 원격 분석을 수행 하면 잠재적 성능 문제
