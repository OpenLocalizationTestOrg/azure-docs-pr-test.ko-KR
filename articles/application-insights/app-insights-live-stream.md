---
title: "사용자 지정 메트릭 및 Azure Application Insights에서 진단 기능을 사용 하 여 메트릭 스트림 aaaLive | Microsoft Docs"
description: "사용자 지정 메트릭으로 웹앱을 실시간으로 모니터링하고 오류, 추적 및 이벤트의 라이브 피드를 통해 문제를 진단할 수 있습니다."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>라이브 메트릭 스트림: 1초 대기 시간으로 모니터링 및 진단 

실시간 메트릭 스트림을 사용 하 여 라이브, 프로덕션에서 웹 응용 프로그램의 hello 됐지만 핵심 프로브 [Application Insights](app-insights-overview.md)합니다. 선택한 메트릭 및 성능 카운터 toowatch 모든 발생 tooyour 서비스 없이 실시간으로 필터링 합니다. 실패한 요청 및 예외 샘플에서 스택 추적을 검사합니다. [프로파일러](app-insights-profiler.md), [스냅숏 디버거](app-insights-snapshot-debugger.md) 및 [성능 테스트](app-insights-monitor-web-app-availability.md#performance-tests)와 함께 라이브 메트릭 스트림은 라이브 웹 사이트에 강력하고 비침해적인 진단 도구를 제공합니다.

라이브 메트릭 스트림을 사용하여 다음을 수행할 수 있습니다.

* 릴리스되는 동안 성능 및 실패 수를 확인하여 수정된 부분의 유효성을 검사합니다.
* 부하를 테스트 하 고 문제를 진단 hello 효과 시청 라이브 합니다. 
* 특정 테스트 세션에 중점을 두거나 선택 하 고 toowatch hello 메트릭을 필터링 하 여 알려진된 문제를 필터링 합니다.
* 예외 추적이 발생하면 가져옵니다.
* 필터와 실험 toofind hello 관련성이 가장 높은 Kpi입니다.
* 모든 Windows 성능 카운터를 실시간 모니터링합니다.
* 쉽게는 문제가 되는 서버를 식별 하 고 모든 hello KPI/라이브 피드 toojust 포함 해당 서버를 필터링 합니다.

[![라이브 메트릭 스트림 비디오](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

메트릭 스트림이 라이브 hello 클라우드 또는 온-프레미스를 실행 중인 ASP.NET 응용 프로그램에서 현재 사용할 수 있습니다. 

## <a name="get-started"></a>시작

1. 아직 ASP.NET 웹앱 또는 [Windows 서버 앱](app-insights-windows-services.md)에 [Application Insights를 설치](app-insights-asp-net.md)하지 않은 경우 지금 설치합니다. 
2. **업데이트 toohello 최신 버전** hello Application Insights 패키지의 합니다. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Nuget 패키지 관리**를 선택합니다. 열기 hello **업데이트** 탭 **시험판 포함**, 모든 hello Microsoft.ApplicationInsights.* 패키지를 선택 합니다.

    응용 프로그램을 다시 배포 합니다.

3. Hello에 [Azure 포털](https://portal.azure.com), 응용 프로그램에 대 한 Application Insights 리소스 hello 연 다음 라이브 스트림을 엽니다.

4. [Hello 보안 제어 채널](#secure-the-control-channel) 고객 이름과 같은 중요 한 데이터 필터에 사용 하려는 경우.


![Hello 개요 블레이드에에서 라이브 스트림을 클릭 합니다.](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>데이터가 없나요? 서버 방화벽을 확인합니다.

Hello 확인 [라이브 메트릭 스트림에 대 한 포트를 나가는](app-insights-ip-addresses.md#outgoing-ports) 서버 hello 방화벽에서 열려 있습니다. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>라이브 메트릭 스트림과 메트릭 탐색기 및 분석과의 차이점

| |라이브 스트림 | 메트릭 탐색기 및 분석 |
|---|---|---|
|대기 시간|데이터가 1초 내에 표시됨|몇 분에 걸쳐 집계됨|
|보존 없음|Hello 차트를 만들고 다음 삭제 됩니다 하는 동안 데이터 유지|[데이터가 90일 동안 유지됨](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|주문형|라이브 메트릭을 여는 동안 데이터가 스트리밍됨|데이터는 hello SDK 설치 되었고 사용 될 때마다 전송 됩니다.|
|무료|라이브 스트림 데이터 무료|너무 주체[가격](app-insights-pricing.md)
|샘플링|선택한 모든 메트릭 및 카운터가 전송되고 오류 및 스택 추적이 샘플링되며 TelemetryProcessors가 적용되지 않음|이벤트가 [샘플링](app-insights-api-filtering-sampling.md)될 수 있음|
|컨트롤 채널|필터 제어 신호 toohello SDK 전송 됩니다. [이 채널을 보호](#secure-channel)하는 것이 좋음|통신은 단방향 toohello 포털|


## <a name="select-and-filter-your-metrics"></a>메트릭 선택 및 필터링

(클래식에서 사용할 수 있는 ASP.NET 앱 hello 최신 SDK.)

Hello 포털에서 모든 Application Insights 원격 분석에 임의 필터를 적용 하 여 실시간 사용자 지정 KPI를 모니터링할 수 있습니다. 때 하면 마우스를 위에 hello 차트 중 하나를 보여 주는 hello 필터 컨트롤을 클릭 합니다. hello 차트 다음 URL 및 지속 시간 특성에 대 한 필터와 사용자 지정 요청 개수 KPI 그래프에 표시 됩니다. 언제 든 지 시간에서 지정한 hello 조건과 일치 하는 원격 분석의 라이브 피드를 보여 주는 스트림 미리 보기 섹션 hello로 필터의 유효성을 검사 합니다. 

![사용자 지정 요청 KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Count와 다른 값을 모니터링할 수 있습니다. hello 옵션 모든 Application Insights 원격 분석 될 수 있는 스트림 hello 유형에 따라 다릅니다: 요청, 종속성, 예외, 추적, 이벤트 또는 메트릭. 이것은 사용자 고유의 [사용자 지정 측정](app-insights-api-custom-events-metrics.md#properties)일 수 있습니다.

![값 옵션](./media/app-insights-live-stream/live-stream-valueoptions.png)

또한 tooApplication Insights 원격 분석을 모니터링할 수도 있습니다 Windows 성능 카운터를 사용 하는 hello 스트림 옵션 중에서 선택 하 고 hello 성능 카운터의 hello 이름을 제공 하 여 합니다.

라이브 메트릭은 각 서버에서 로컬로 집계된 후 모든 서버에서 집계됩니다. Hello 해당 드롭다운 목록에서 다른 옵션을 선택 하 여 하나에 hello 기본값을 변경할 수 있습니다.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>샘플 원격 분석: 사용자 지정 라이브 진단 이벤트
기본적으로 이벤트의 라이브 피드 hello 샘플 실패 한 요청 및 종속성 호출, 예외, 이벤트 및 추적을 표시 합니다. 시간에 언제 든 지 hello 필터 아이콘 toosee 적용 hello 조건을 클릭 합니다. 

![기본 라이브 피드](./media/app-insights-live-stream/live-stream-eventsdefault.png)

메트릭 hello Application Insights 원격 분석 유형 중 임의의 조건 tooany 모든 지정할 수 있습니다. 이 예제에서는 특정 요청 실패, 추적 및 이벤트를 선택합니다. 모든 예외 및 종속성 오류도 선택합니다.

![사용자 지정 라이브 피드](./media/app-insights-live-stream/live-stream-events.png)

참고: 현재 예외에 대 한 메시지 기반 조건을 사용 하 여 hello 가장 바깥쪽 예외 메시지입니다. 예제에서는 앞에 오는 hello에 내부 예외 메시지를 사용 하 여 hello 심각 하지 않은 예외 아웃 toofilter (다음과 hello "<-" 구분 기호) "hello 클라이언트 연결 끊김." "요청 콘텐츠를 읽는 동안 오류 발생" 조건을 포함하지 않는 메시지를 사용합니다.

클릭 하 여 피드를 라이브 hello에 있는 항목의 hello 정보를 참조 하십시오. Hello를 클릭 하 여 피드를 두면 **일시 중지** 또는 단순히 아래로 스크롤하여 하거나 항목을 클릭 하면 합니다. 라이브 피드 백 toohello 위쪽 스크롤한 후 다시 시작 됩니다 또는 항목의 hello 카운터를 클릭 하 여 일시 중지 된 동안 수집 합니다.

![샘플링된 라이브 실패](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>서버 인스턴스별 필터링

Toomonitor 특정 서버 역할 인스턴스를 원하는 경우에 서버에서 필터링 할 수 있습니다.

![샘플링된 라이브 실패](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>SDK 요구 사항
사용자 지정 라이브 메트릭 스트림은 버전 2.4.0-beta2 또는 최신 버전의 [웹용 Application Insights SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)에서 사용할 수 있습니다. NuGet 패키지 관리자에서 tooselect "시험판 포함" 옵션을 기억 합니다.

## <a name="secure-hello-control-channel"></a>Hello 컨트롤 채널을 보호
hello 지정 하는 사용자 지정 필터 기준은 hello Application Insights SDK에서에서 뒤로 toohello 라이브 메트릭 구성 요소를 보냅니다. hello 필터 Customerid 같은 중요 한 정보를 잠재적으로 포함할 수 있습니다. 또한 toohello 계측 키 비밀 API 키를 사용 하 여 보안 hello 채널을 만들 수 있습니다.
### <a name="create-an-api-key"></a>API 키 만들기

![API 키 만들기](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>API 키 tooConfiguration 추가
Hello applicationinsights.config 파일에서 hello AuthenticationApiKey toohello QuickPulseTelemetryModule를 추가 합니다.
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
또는 코드에서 QuickPulseTelemetryModule hello에 설정:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

그러나 인식 하 고 모든 hello 연결 된 서버를 신뢰 하는 경우 인증 하는 hello 채널 없이 hello 사용자 지정 필터를 시도할 수 있습니다. 이 옵션은 6개월 동안 사용할 수 있습니다. 이 재정의는 새 세션마다 한 번씩 또는 새 서버가 온라인 상태가 될 때마다 필요합니다.

![라이브 메트릭 인증 옵션](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Hello 필터 조건에 CustomerID와 같은 잠재적으로 중요 한 정보를 입력 하기 전에 인증 하는 hello 채널을 설정 하는 것이 좋습니다.
>

## <a name="generating-a-performance-test-load"></a>성능 테스트 로드 생성

Toowatch hello 효과 부하의 증가 사용 하 여 hello 성능 테스트 블레이드입니다. 여러 동시 사용자의 요청을 시뮬레이트합니다. 어느 "수동 테스트"를 실행할 수 (ping 테스트)의 단일 URL 또는 실행할 수는 [multi-step 웹 성능 테스트](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (동일한 가용성으로 방식으로 테스트 하는 hello)에 업로드 하 합니다.

> [!TIP]
> Hello 성능 테스트를 만든 후 hello 테스트 열고 별도 창에서 라이브 스트림을 블레이드 hello 합니다. Hello 대기 중인 경우 성능 테스트 시작 되 고 조사식 hello에서 라이브 스트림을 볼 수 있습니다 동시 합니다.
>


## <a name="troubleshooting"></a>문제 해결

데이터가 없나요? 응용 프로그램이 보호된 네트워크에 있는 경우: 라이브 메트릭 스트림은 Application Insights 원격 분석과는 다른 IP 주소를 사용합니다. 방화벽에서 [해당 포트](app-insights-ip-addresses.md)가 열려 있는지 확인합니다.



## <a name="next-steps"></a>다음 단계
* [Application Insights를 사용하여 사용량 모니터링](app-insights-web-track-usage.md)
* [진단 검색 사용](app-insights-diagnostic-search.md)
* [프로파일러](app-insights-profiler.md)
* [스냅숏 디버거](app-insights-snapshot-debugger.md)
