---
title: "사용자 지정 이벤트 및 메트릭을 대 한 인 사이트 API aaaApplication | Microsoft Docs"
description: "장치 또는 데스크톱 응용 프로그램, 웹 페이지 또는 서비스에 tootrack 사용량에 몇 줄의 코드를 삽입 하 고 문제를 진단 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>사용자 지정 이벤트 및 메트릭용 Application Insights API

프로그램 응용 프로그램 toofind, 사용자가 수행 하는 아웃에 몇 줄의 코드를 넣거나 toohelp 문제를 진단 합니다. 장치 및 데스크톱 앱, 웹 클라이언트, 웹 서버에서 원격 분석을 보낼 수 있습니다. 사용 하 여 hello [Azure Application Insights](app-insights-overview.md) 원격 분석 API toosend 사용자 지정 이벤트 및 메트릭 및 사용자가 자체 버전 표준 원격 분석의 핵심입니다. 이 API는 동일한 API Application Insights 데이터 수집기를 사용 하 여 hello 표준에 hello 됩니다.

## <a name="api-summary"></a>API 요약
hello API는 몇 가지 작은 변형 외에도 모든 플랫폼에 걸쳐 균일 한 합니다.

| 메서드 | 용도 |
| --- | --- |
| [`TrackPageView`](#page-views) |페이지, 화면, 블레이드 또는 양식. |
| [`TrackEvent`](#trackevent) |사용자 작업 및 기타 이벤트. Tootrack 사용자 동작 또는 toomonitor 성능을 사용합니다. |
| [`TrackMetric`](#trackmetric) |큐 길이 같은 성능 측정 toospecific 이벤트와 무관 합니다. |
| [`TrackException`](#trackexception) |진단 예외를 기록합니다. 추적 관계 tooother 이벤트에서 발생 및 스택 추적을 검사 합니다. |
| [`TrackRequest`](#trackrequest) |Hello 빈도 / 기간 서버 요청의 성능 분석에 대 한 로깅을 구성 합니다. |
| [`TrackTrace`](#tracktrace) |진단 로그 메시지. 타사 로그도 캡처할 수 있습니다. |
| [`TrackDependency`](#trackdependency) |Hello 기간 및 빈도 응용 프로그램에 의존 하는 호출 tooexternal 구성 요소의 로깅을 구성 합니다. |

할 수 있습니다 [연결 속성 및 메트릭을](#properties) toomost 이러한 원격 분석 호출 합니다.

## <a name="prep"></a>시작하기 전에
Application Insights SDK에 대한 참조가 아직 없는 경우:

* Hello Application Insights SDK tooyour 프로젝트를 추가 합니다.

  * [ASP.NET 프로젝트](app-insights-asp-net.md)
  * [Java 프로젝트](app-insights-java-get-started.md)
  * [각 웹 페이지의 JavaScript](app-insights-javascript.md) 
* 장치 또는 웹 서버 코드에 다음을 포함합니다.

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic:* `Imports Microsoft.ApplicationInsights`

    *Java:* `import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>TelemetryClient 인스턴스 생성
`TelemetryClient`의 인스턴스를 생성합니다(웹 페이지의 JavaScript는 제외).

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient는 스레드로부터 안전합니다.

앱의 각 모듈에 대해 TelemetryClient 인스턴스를 사용하는 것이 좋습니다. 예를 들어, 웹 서비스 tooreport 들어오는 HTTP 요청을 받은 및 미들웨어 클래스 tooreport 비즈니스 논리 이벤트에서 다른 TelemetryClient 인스턴스 하나를 할 수 있습니다. 와 같은 속성을 설정할 수 있습니다 `TelemetryClient.Context.User.Id` tootrack 사용자와 세션, 또는 `TelemetryClient.Context.Device.Id` tooidentify hello 컴퓨터입니다. 이 정보는 hello 인스턴스 전송 하는 연결 된 tooall 이벤트입니다.

## <a name="trackevent"></a>TrackEvent
Application Insights에서 *사용자 지정 이벤트*는 [메트릭 탐색기](app-insights-metrics-explorer.md)에 집계된 개수로 표시하고 [진단 검색](app-insights-diagnostic-search.md)에 개별 항목으로 표시할 수 있는 데이터 요소입니다. (관련된 tooMVC 또는 다른 프레임 워크 "이벤트입니다." 하지)

삽입 `TrackEvent` 코드 toocount의 다양 한 이벤트를 호출 합니다. 사용자가 특정 기능을 얼마나 자주 선택하는지, 특정 목표를 얼마나 자주 달성하는지 또는 특정 유형의 실수를 얼마나 자주 하는지를 계산할 수 있습니다.

예를 들어 게임 응용 프로그램에서 사용자 hello 승리는 이벤트를 전송 합니다.

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Hello Microsoft Azure 포털에서 이벤트 보기
사용자 이벤트의 개수 toosee 열고는 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드에서 새 차트를 추가 하 고 선택 **이벤트**합니다.  

![사용자 지정 이벤트 수 보기](./media/app-insights-api-custom-events-metrics/01-custom.png)

다른 이벤트의 toocompare hello 횟수 hello 차트 종류를 너무 설정**그리드**, 이벤트 이름으로 그룹화 하 고:

![Hello 차트 종류와 그룹화를 설정 합니다.](./media/app-insights-api-custom-events-metrics/07-grid.png)

Hello 표에서 이벤트 이름 toosee의 개별 항목에 해당 이벤트를 클릭 합니다. toosee는 hello 목록에서 임의의 발생 항목 클릭 자세히-자세히 설명 합니다.

![Hello 이벤트 드릴스루](./media/app-insights-api-custom-events-metrics/03-instances.png)

관심이 있는 집합 hello 블레이드 필터 toohello 이벤트 이름 검색 또는 메트릭 탐색기에서 특정 이벤트에 toofocus:

![필터를 열고 이벤트 이름을 확장한 다음 하나 이상의 값을 선택합니다.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>분석의 사용자 지정 이벤트

hello 원격 분석은 hello에서 사용할 수 있는 `customEvents` 테이블에 [응용 프로그램 통찰력 분석](app-insights-analytics.md)합니다. 각 행 너무 대 한 호출을 나타내는`trackEvent(..)` 응용 프로그램에서 합니다. 

경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다. 예제 itemCount는 10 개의 호출이 tootrackEvent()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다. 사용자 지정 이벤트의 정확한 개수 tooget 사용 해야 하므로와 같은 사용 가능한 코드 `customEvent | summarize sum(itemCount)`합니다.


## <a name="trackmetric"></a>TrackMetric

Application Insights에 연결 된 tooparticular 이벤트가 메트릭을 차트 수입니다. 예를 들어 정기적으로 큐 길이를 모니터링할 수 있습니다. 메트릭을 사용 하 여 hello 개별 측정 하는 hello 변형 및 추세를 보다 작음 관심 되며 따라서 통계 차트 유용 합니다.

toosend 메트릭 tooApplication Insights 순서, hello를 사용할 수 있습니다 `TrackMetric(..)` API입니다. 두 가지 방법으로 toosend 메트릭 

* 단일 값. 응용 프로그램에서 측정 한 값을 수행할 때마다 해당 값 hello tooApplication Insights 보냅니다. 예를 들어 hello 컨테이너의 항목 수를 설명 하는 메트릭이 있다고 가정 합니다. 특정 기간 동안 hello 컨테이너에 처음 세 개의 품목을 넣은 하 고 그런 다음 두 항목을 제거 합니다. 호출 하는 것이 그에 따라, `TrackMetric` 두 번: hello 값을 전달 하는 먼저 `3` 다음 값을 hello 및 `-2`합니다. Application Insights는 두 값을 자동으로 저장합니다. 

* 집계. 메트릭을 사용하여 작업하는 경우 모든 단일 측정값은 거의 유용하지 않습니다. 대신 특정 기간 동안 발생한 내용의 요약이 중요합니다. 이러한 요약을 _집계_라고 합니다. 위 예제는 hello, hello 해당 기간에 대 한 집계 메트릭 합계는 `1` hello hello 메트릭 값 개수 이며 `2`합니다. Hello 집계 방법을 사용할 때는 호출 하면 `TrackMetric` 시간 기간 및 송신 hello 집계 값 마다 한 번씩입니다. 이 hello 권장 접근법 hello 비용을 크게 줄일 수 있고 성능 오버 헤드가 적은 데이터를 보내 여전히 모든 관련 정보를 수집 하는 동안 tooApplication 통찰력을 가리킵니다.

### <a name="examples"></a>예제:

#### <a name="single-values"></a>단일 값

toosend 단일 메트릭 값:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>메트릭 집계

응용 프로그램, tooreduce 대역폭, 비용 및 tooimprove 성능에서 보내기 전에 tooaggregate 메트릭을 좋습니다.
다음은 집계 코드 예제입니다.

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>메트릭 탐색기의 사용자 지정 메트릭

toosee hello 결과 메트릭 탐색기를 열고 새 차트를 추가 합니다. 프로그램 메트릭을 hello 차트 tooshow를 편집 합니다.

> [!NOTE]
> 사용자의 사용자 지정 메트릭을 사용 가능한 메트릭 hello 목록에서 몇 분 tooappear를 걸릴 수 있습니다.
>

![새 차트를 추가하거나 차트를 선택하고, 사용자 지정 아래에서 메트릭을 선택합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>분석의 사용자 지정 메트릭

hello 원격 분석은 hello에서 사용할 수 있는 `customMetrics` 테이블에 [응용 프로그램 통찰력 분석](app-insights-analytics.md)합니다. 각 행 너무 대 한 호출을 나타내는`trackMetric(..)` 응용 프로그램에서 합니다.
* `valueSum`-이 hello 측정 hello 합계입니다. tooget hello 평균 값으로 나누기 `valueCount`합니다.
* `valueCount`-이에 집계 된 단위 수를 hello `trackMetric(..)` 호출 합니다.

## <a name="page-views"></a>페이지 보기
장치 또는 웹 페이지 앱에서 각 화면 또는 페이지가 로드되면 기본적으로 페이지 보기 원격 분석이 전송됩니다. 하지만 또는 다른 시간에 해당 tootrack 페이지 뷰를 변경할 수 있습니다. 예를 들어, 탭 또는 블레이드를 표시 하는 응용 프로그램에 수 tootrack 페이지 때마다 원하는 hello 사용자는 새 블레이드가 열립니다.

![개요 블레이드의 사용 현황 렌즈](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

사용자 및 세션 데이터는 페이지 보기와 함께 속성 페이지 보기 원격 분석 때 생기는 사용자 및 세션 차트를 따라서 hello으로 전송 됩니다.

### <a name="custom-page-views"></a>사용자 지정 페이지 보기
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


여러 HTML 페이지 내에서 여러 탭이 있는 경우 너무 hello URL을 지정할 수 있습니다.

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>페이지 보기 시간
기본적으로 hello 번으로 보고 **페이지 보기 로드 시간** hello 브라우저 hello 브라우저 페이지 로드 이벤트를 호출할 때까지 hello 요청을 보낼 때에서 측정 됩니다.

대신, 다음을 수행할 수 있습니다.

* Hello에 명시적 기간 설정 [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) 호출: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`합니다.
* Hello 페이지 보기 타이밍 호출을 사용 하 여 `startTrackPage` 및 `stopTrackPage`합니다.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

hello hello 첫 번째 매개 변수 연결 hello 시작으로를 사용 하는 이름 및 호출을 중지 합니다. 현재 페이지 이름 toohello 기본값으로 사용 합니다.

메트릭 탐색기에 표시 된 기간 사이의 hello hello 간격에서 파생 된 hello 결과 페이지 로드 시작 및 호출을 중지 합니다. 가 tooyou 실제로 시간 어떤 간격입니다.

### <a name="page-telemetry-in-analytics"></a>분석의 페이지 원격 분석

[분석](app-insights-analytics.md)에서 두 테이블이 브라우저 작업의 데이터를 보여 줍니다.

* hello `pageViews` hello URL 및 페이지 제목에 대 한 데이터를 포함 하는 테이블
* hello `browserTimings` hello에 걸린 시간 tooprocess hello 들어오는 데이터와 같은 클라이언트 성능에 대 한 데이터 테이블에 포함

toofind hello 브라우저 사용 시간이 얼마나 걸리는지 tooprocess 서로 다른 페이지:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

다양 한 브라우저의 toodiscover hello popularities:

```
pageViews | summarize count() by client_Browser
```

종속성이 있는 tooassociate 페이지 뷰 tooAJAX 호출에 가입 시킵니다.

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
hello 서버 SDK TrackRequest toolog HTTP 요청을 사용합니다.

호출할 수 있습니다도 직접 컨텍스트에서 요청을 toosimulate 없는 hello 웹 서비스 모듈이 실행 중입니다.

그러나 hello 권장 방법은 toosend 요청 원격 분석은 hello 요청 역할도 <a href="#operation-context">작업 컨텍스트</a>합니다.

## <a name="operation-context"></a>작업 컨텍스트
일반적인 Operationid toothem 연결 하 여 원격 분석 항목을 함께 연결할 수 있습니다. 기본 요청 추적 모듈이 hello 예외 및 HTTP 요청을 처리 하는 동안 전송 된 다른 이벤트에 대해 수행 하지 않습니다. [검색](app-insights-diagnostic-search.md) 및 [분석](app-insights-analytics.md), hello ID tooeasily 찾기 hello 요청과 관련 된 모든 이벤트를 사용할 수 있습니다.

이 패턴을 사용 하 여 tooset 작업 컨텍스트를가 하는 hello 가장 쉬운 방법은 tooset hello ID:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

작업 컨텍스트를 설정 하는 함께 `StartOperation` 지정 하는 hello 유형의 원격 분석 항목을 만듭니다. 보내는 hello 원격 분석 항목 hello 작업을 삭제 하거나 명시적으로 호출 하는 경우 `StopOperation`합니다. 사용 하는 경우 `RequestTelemetry` 지속 시간이 toohello 간격 시작 및 중지 hello 원격 분석 유형으로 설정 되어 있습니다.

작업 컨텍스트는 중첩할 수 없습니다. 컨텍스트가 이미 있는 작업, 경우 해당 ID는 연결 된 모든 hello 포함 된 항목을 사용 하 여 만든 hello 항목을 포함 하 여 `StartOperation`합니다.

검색에서 hello 작업 컨텍스트는 사용 되는 toocreate hello **관련 항목** 목록:

![관련 항목](./media/app-insights-api-custom-events-metrics/21.png)

사용자 지정 작업 추적에 대한 자세한 내용은 [application-insights-custom-operations-tracking.md]를 참조하세요.

### <a name="requests-in-analytics"></a>분석의 요청 

[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 표시를 요청 `requests` 테이블입니다.

경우 [샘플링](app-insights-sampling.md) 은 작업에서 hello itemCount 속성은 값이 표시는 1 보다 큰 경우. 예제 itemCount는 10 개의 호출이 tootrackRequest()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다. 요청 이름별 tooget 요청 및 평균 기간 올바른 수 분할와 같은 코드를 사용 하 여:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
예외 tooApplication Insights 보내기:

* 너무[합계를 구하고](app-insights-metrics-explorer.md), 문제의 hello 빈도를 확인 합니다.
* 너무[개별 발생 수가 검사](app-insights-diagnostic-search.md)합니다.

hello 보고서 hello 스택 추적에 포함 합니다.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

hello Sdk 바랍니다 항상 toocall TrackException 명시적으로 자동으로 대부분의 예외를 catch 합니다.

* ASP.NET: [toocatch 예외 코드를 작성](app-insights-asp-net-exceptions.md)합니다.
* J2EE: [예외가 자동으로 catch됨](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: 예외가 자동으로 catch됨. Toodisable 자동 수집 하려는 경우 웹 페이지에서 삽입 하는 줄 toohello 코드 조각을 추가 합니다.

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>분석의 예외

[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 예외가 표시 `exceptions` 테이블입니다.

경우 [샘플링](app-insights-sampling.md) 작업에 포함 되어, hello `itemCount` 속성 값이 1 보다 큰 표시 합니다. 예제 itemCount는 10 개의 호출이 tootrackException()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다. 예외의 유형을 통해 tooget 올바른 수 없는 예외 수 분할와 같은 코드를 사용 하 여:

```
exceptions | summarize sum(itemCount) by type
```

대부분의 중요 한 스택 정보는 개별 변수로 추출 이미 하지만 더 많이 떨어져 있는 hello를 끌어올 수 hello `details` 구조 tooget 더 합니다. 이 구조는 동적 이므로 hello 결과 toohello 형식을 예상 캐스팅 해야 합니다. 예:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

조인을 사용 하 여 해당 관련된 요청을 사용 하 여 tooassociate 예외:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
사용 하 여 TrackTrace toohelp "이동 경로 트레일에서" tooApplication 통찰력을 전송 하 여 문제를 진단 합니다. 진단 데이터의 청크를 보내고 [진단 검색](app-insights-diagnostic-search.md)에서 검사할 수 있습니다.

[어댑터 로그](app-insights-asp-net-trace-logs.md) 이 API toosend 제 3 자 로그 toohello 포털을 사용 합니다.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


메시지 내용을 검색할 수 있지만 속성 값과는 달리 필터링할 수는 없습니다.

hello 크기 제한에 `message` hello 속성에 대 한도 보다 훨씬 비쌉니다.
TrackTrace 경우의 이점은 hello 메시지에 상대적으로 긴 데이터를 지정할 수 있습니다. 예를 들어, POST 데이터를 인코딩할 수 있습니다.  

또한, 심각도 수준 tooyour 메시지를 추가할 수 있습니다. 와 같은 다른 원격 분석을 필터링 할 속성 값 toohelp 또는 다른 집합이 추적에 대 한 검색 추가할 수 있습니다. 예:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

[검색](app-insights-diagnostic-search.md), tooa 특정 데이터베이스와 관련 된 특정 심각도 수준의 모든 hello 메시지를 쉽게 필터링 할 수 있습니다.


### <a name="traces-in-analytics"></a>분석의 추적

[응용 프로그램 통찰력 분석](app-insights-analytics.md)를 실행 tooTrackTrace 표시 hello에 `traces` 테이블입니다.

경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다. 10의 호출 하는 너무 10 의미 = = 연산자 예제 itemCount`trackTrace()`, 그 중 하나는 hello 샘플링 프로세스만 전송 합니다. tooget 추적 호출의 올바른 수를 사용 해야 하므로 코드와 같은 `traces | summarize sum(itemCount)`합니다.

## <a name="trackdependency"></a>TrackDependency
Tootrack hello 응답 시간과 성공률 호출 tooan 외부 코드 조각에 사용 하 여 hello TrackDependency를 호출 합니다. hello 결과가 hello 포털 hello 종속성 차트에 나타납니다.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

해당 hello 서버 Sdk 포함 된다는 점에 유의 [종속성 모듈](app-insights-asp-net-dependencies.md) 검색 하 고 특정 종속성 호출을 자동으로-예: toodatabases 및 REST Api에 대 한 추적입니다. Tooinstall 서버 toomake hello 모듈에서 에이전트를 작동 해야 합니다. 자동화 된 추적 hello tootrack 호출 catch 하지 않으려는 경우 나 tooinstall hello 에이전트를 표시 하지 않으려는 경우이 호출을 사용 합니다.

기본 종속성 추적 모듈 hello 오프 tooturn 편집 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 너무 hello 참조를 삭제 하 고`DependencyCollector.DependencyTrackingTelemetryModule`합니다.

### <a name="dependencies-in-analytics"></a>분석의 종속성

[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 trackDependency 호출 표시 `dependencies` 테이블입니다.

경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다. 예제 itemCount는 10 개의 호출이 tootrackDependency()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다. 대상 구성 요소에 의해 tooget 종속성의 올바른 수 분할와 같은 코드를 사용 하 여:

```
dependencies | summarize sum(itemCount) by target
```

조인을 사용 하 여 해당 관련된 요청이 포함 된 tooassociate 종속성:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>데이터 플러시
일반적으로 SDK hello 때때로 hello 사용자에 미치는 영향을 toominimize hello를 선택 하는 데이터를 보냅니다. 하지만, 일부 경우에 필요할 수 있습니다 tooflush hello 버퍼-예를 들어 종료 하는 응용 프로그램에 hello SDK를 사용 하는 경우.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Hello 함수 hello에 대 한 비동기는 [서버 원격 분석 채널](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)합니다.

## <a name="authenticated-users"></a>인증된 사용자
웹앱에서 사용자는 기본적으로 쿠키로 식별됩니다. 사용자가 다른 컴퓨터 또는 브라우저에서 앱에 액세스하거나 쿠키를 삭제하는 경우 두 번 이상 계산될 수 있습니다.

사용자가 tooyour 앱에 로그인 하는 경우에 hello 브라우저 코드에서 hello 인증 된 사용자 ID를 설정 하 여 보다 정확한 수를 얻을 수 있습니다.

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

ASP.NET 웹 MVC 응용 프로그램에서의 예:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

필요한 toouse hello 사용자의 실제 로그인 이름이 아닙니다. Toobe id는 고유 toothat 사용자 ID만에 있습니다. 공백이 나 hello 문자를 포함 하지 않아야 `,;=|`합니다.

hello 사용자 ID도 세션 쿠키에 설정 되 고 toohello 서버에 전송 합니다. Hello 서버 SDK가 설치 되어 hello ID가 클라이언트와 서버 모두의 원격 분석의 hello 컨텍스트 속성의 일부로 전송 되는 사용자를 인증 합니다. 필터링하고 검색할 수 있습니다.

사용자 계정으로 그룹화 하는 응용 프로그램, hello 계정에 대 한 식별자 전달할 수도 있습니다 (hello로 동일한 문자 제한).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

[메트릭 탐색기](app-insights-metrics-explorer.md)에서 **사용자, 인증** 및 **사용자 계정**을 계산하는 차트를 만들 수 있습니다.

특정 사용자 이름과 계정으로 클라이언트 데이터 지점을 [검색](app-insights-diagnostic-search.md)할 수도 있습니다.

## <a name="properties"></a>속성을 사용하여 데이터를 필터링, 검색 및 세분화
속성 및 측정 tooyour 이벤트 (및 또한 toometrics, 페이지 보기, 예외 및 기타 원격 분석 데이터)를 연결할 수 있습니다.

*속성* 는 사용할 수 있는 toofilter 원격 분석 hello 사용 현황 보고서에는 문자열 값입니다. 예를 들어 여러 게임을 제공 하는 앱을 더 많이 사용 되는 게임을 볼 수 있도록 hello 게임 tooeach 이벤트의 hello 이름을 연결할 수 있습니다.

Hello 문자열 길이 8192의 제한이 있습니다. (Toosend 큰 데이터 청크의 경우의 hello 메시지 매개 변수를 사용할 [TrackTrace](#track-trace).)

*메트릭* 은 그래픽으로 표시할 수 있는 숫자 값입니다. 예를 들어 프로그램 게이머 달성 하는 hello 점수에 점진적으로 증가 하면 toosee를 원하는 수 있습니다. hello 그래프 얻을 수 있도록 hello 이벤트와 함께 전송 되는 속성을 구분 하는 hello 나눌 수 있습니다 또는 다른 게임에 대 한 그래프를 누적 합니다.

메트릭 값 toobe 올바로 표시에 대 한 보다 크거나 같은 too0 수 있어야 합니다.

일부 [속성, 속성 값, 및 메트릭을 hello 수에 대 한 제한](#limits) 사용할 수 있는 합니다.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> 개인 식별이 가능한 정보 속성에서 toolog 주의 해야 합니다.
>
>

*메트릭을 사용 하는 경우*메트릭 탐색기를 열고 hello에서 hello 메트릭을 선택 **사용자 지정** 그룹:

![메트릭 탐색기를 선택 하는 hello 차트를 열고 hello 메트릭을 선택 합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> 프로그램 메트릭을 표시 되지 않으면 또는 경우 hello **사용자 지정** 제목 없는 선택 영역 블레이드 닫기 hello 및 나중에 다시 시도 하십시오. 한 시간 메트릭 오래 걸릴 수도 toobe hello 파이프라인을 통해 집계 합니다.

*속성 및 메트릭을 사용 하는 경우*, hello 속성을 기준으로 hello 메트릭을 구분 합니다.

![그룹화를 설정 하 고 그룹화 기준 hello 속성을 선택 합니다](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*진단 검색*, hello 속성 및 이벤트의 개별 항목의 메트릭을 볼 수 있습니다.

![인스턴스를 선택한 다음 '...'를 선택합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

사용 하 여 hello **검색** 특정 속성 값을 가진 toosee 이벤트 항목만 필드입니다.

![검색에 용어를 입력합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[검색 식에 대해 자세히 알아보세요](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>다른 방법으로 tooset 속성 및 메트릭
더 편리 이면 hello 매개 변수는 별도 개체에 이벤트를 수집할 수 있습니다.

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Hello를 다시 사용 하지 마세요 동일한 원격 분석 항목 인스턴스 (`event` 이 예에서) toocall Track*() 여러 번입니다. 잘못 된 구성으로 전송 하는 원격 분석 toobe를 않을 수 있습니다.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>분석의 사용자 지정 측정 및 속성

[분석](app-insights-analytics.md), hello에 대 한 사용자 지정 메트릭 및 속성 표시 `customMeasurements` 및 `customDimensions` 각 원격 분석 레코드의 특성입니다.

예를 들어 "게임" tooyour 요청 원격 분석 라는 속성을 추가한 경우이 쿼리 hello 발생 "게임"의 서로 다른 값의 수를 세 않으며 hello의 hello 평균 점수"사용자 지정 메트릭"를 표시 합니다.

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

다음에 유의합니다.

* 가 동적 형식이 고 캐스팅 해야 하므로 hello customDimensions 또는 customMeasurements JSON에서 값을 추출할 때 `tostring` 또는 `todouble`합니다.
* hello 가능성 tootake 계정 [샘플링](app-insights-sampling.md)를 사용 해야 `sum(itemCount)`이 아니라 `count()`합니다.



## <a name="timed"></a> 타이밍 이벤트
소요 tooperform 동작 toochart를 경우가 있습니다. 예를 들어 tooknow 경우가 사용자 게임에서 tooconsider 선택 항목을 사용 하는 기간. 이 대 한 hello 측정 매개 변수를 사용할 수 있습니다.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>사용자 지정 원격 분석에 대한 기본 속성
일부 사용자가 작성 하는 hello 사용자 지정 이벤트에 대 한 tooset 기본 속성 값을 원하는 경우 TelemetryClient 인스턴스에서 설정할 수 있습니다. 이들은 연결 된 tooevery 원격 분석 항목은 해당 클라이언트에서 전송 된입니다.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



원격 분석 개별 호출 자신의 속성 사전에 hello 기본 값을 재정의할 수 있습니다.

*JavaScript 웹 클라이언트의 경우*[JavaScript 원격 분석 이니셜라이저를 사용합니다](#js-initializer).

*tooadd 속성 tooall 원격 분석*, 표준 컬렉션 모듈 hello 데이터를 포함 하 여 [구현 `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties)합니다.

## <a name="sampling-filtering-and-processing-telemetry"></a>원격 분석 샘플링, 필터링 및 처리
Hello SDK에서에서 전송 하기 전에 원격 분석 코드 tooprocess을 작성할 수 있습니다. hello 처리와 같은 HTTP 요청 컬렉션과 종속성 컬렉션 hello 표준 원격 분석 모듈에서 전송 된 데이터가 포함 됩니다.

[속성 추가](app-insights-api-filtering-sampling.md#add-properties) 구현 하 여 tootelemetry `ITelemetryInitializer`합니다. 예를 들어 다른 속성에서 계산된 버전 번호 또는 값을 추가할 수 있습니다.

[필터링](app-insights-api-filtering-sampling.md#filtering) 수정 하거나 구현 하 여 hello SDK에서에서 전송 하기 전에 원격 분석을 취소 `ITelemetryProcesor`합니다. 전송 되었거나 무시 된 항목을 제어 있는데 tooaccount 하면 메트릭이에 hello 영향에 대 한 합니다. 항목을 삭제 하는 방법에 따라 관련된 항목 간의 hello 기능 toonavigate를 손실 될 수 있습니다.

[샘플링](app-insights-api-filtering-sampling.md) 앱 toohello 포털에서 전송 된 데이터를 패키지에 포함 된 솔루션 tooreduce hello 볼륨이 합니다. 메트릭을 표시 하는 hello 영향을 주지 않고을 수행 합니다. 한 예외, 요청 및 페이지 보기 등의 관련된 항목 간에 이동 하 여 기능 toodiagnose 문제 영향을 주지 않고 작업을 수행 합니다.

[자세히 알아봅니다](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>원격 분석 사용 안 함
너무*동적으로 중지 하 고 시작* 수집 및 원격 분석 전송을 hello:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

너무*선택한 표준 수집기를 해제*-예를 들어 성능 카운터, HTTP 요청-종속성을 삭제 하거나 hello 관련 줄의 주석 처리 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다. 이렇게 하려면, 예를 들어 toosend TrackRequest 자신만 데이터를 원하는 경우.

## <a name="debug"></a>개발자 모드
디버깅 하는 동안 원격 분석 결과 즉시 볼 수 있도록 hello 파이프라인을 통해 신속한 유용 toohave 것 합니다. 된 hello 원격 분석 문제를 추적할도 get 추가 메시지 수 있습니다. 앱이 느려질 수 있으므로 프로덕션 환경에서는 끄는 것이 좋습니다.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>선택한 사용자 지정 원격 분석을 위한 hello 계측 키를 설정합니다.
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> 동적 계측 키
개발, 테스트 및 프로덕션 환경에서 원격 분석을 혼합 tooavoid 할 수 있습니다 [별도 Application Insights 리소스 만들기](app-insights-create-new-resource.md) hello 환경에 따라 해당 키를 변경 합니다.

Hello 구성 파일에서 hello 계측 키를 가져오는 대신 코드에서 설정할 수 있습니다. 초기화 메서드에서 global.aspx.cs ASP.NET 서비스에서 같은 hello 키를 설정 합니다.

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



웹 페이지에 tooset 수도 hello 웹 서버의 상태를 보다는 hello 스크립트에 문자 그대로 코딩 옵니다. 예를 들어 ASP.NET 앱에서 생성된 웹 페이지에서 다음과 같이 설정합니다.

*Razor에서 JavaScript*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient에는 컨텍스트 속성이 있고, 이 속성은 모든 원격 분석 데이터와 함께 전송되는 값을 포함하고 있습니다. 일반적으로 hello 표준 원격 분석 모듈에 의해 설정 하지만 또한 속성을 설정할 수 직접 합니다. 예:

    telemetry.Context.Operation.Name = "MyOperationName";

직접 설정할 경우 다음이 값 중 하나를 고려 hello에서 관련 줄을 제거 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)값과 hello 표준 값의 혼동 되도록 합니다.

* **구성 요소**: hello 앱 및 해당 버전입니다.
* **장치**: hello 앱이 실행 되는 hello 장치에 대 한 데이터입니다. (웹 응용 프로그램에서이 hello 서버 또는 클라이언트 장치에서 보내는 hello 원격 분석.)
* **InstrumentationKey**: hello Azure hello 원격 분석 표시 되는 위치에서 Application Insights 리소스입니다. 일반적으로 ApplicationInsights.config에서 선택합니다.
* **위치**: hello hello 장치의 지리적 위치입니다.
* **작업**: 웹 응용 프로그램에서 현재 HTTP 요청을 hello 합니다. 다른 응용 프로그램 형식에서는이 toogroup 이벤트를 함께 설정할 수 있습니다.
  * **Id**: 진단 검색의 이벤트를 검사할 때 "항목 관련"을 찾을 수 있도록 여러 이벤트를 상호 연결하는 생성된 값입니다.
  * **이름**: 일반적으로 hello 요청 URL의 HTTP hello 식별자입니다.
  * **SyntheticSource**: 경우 하지 null 이거나 비어 hello 요청의 hello 원본을 나타내는 문자열 확인 되었습니다 로봇 또는 웹 테스트로 합니다. 기본적으로 메트릭 탐색기의 계산에서 제외됩니다.
* **Properties**: 모든 원격 분석 데이터와 함께 전송되는 속성입니다. 개별 Track* 호출에서 재정의될 수 있습니다.
* **세션**: hello 사용자의 세션입니다. hello ID hello 사용자가 하지 상태인 동안 때 변경 되는 tooa 생성 값으로 설정 됩니다.
* **User**: 사용자 정보입니다.

## <a name="limits"></a>제한
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

사용 하 여 hello 데이터 속도 제한에 도달 tooavoid [샘플링](app-insights-sampling.md)합니다.

toodetermine 긴 데이터를 유지 하는 방법 참조 [데이터 보존 및 개인 정보 보호](app-insights-data-retention-privacy.md)합니다.

## <a name="reference-docs"></a>참조 문서
* [ASP.NET 참조](https://msdn.microsoft.com/library/dn817570.aspx)
* [Java 참조](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [JavaScript 참조](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>SDK 코드
* [ASP.NET 핵심 SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Windows Server 패키지](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)
* [모든 플랫폼](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>질문
* *Track_() 호출에서 발생할 수 있는 예외는 무엇인가요?*

    없음. Toowrap 않아도 try catch 절에서 해당 합니다. Hello 디버그 콘솔 출력에서 메시지를 기록 합니다 hello SDK에서 문제가 발생 하는 경우 및--인 경우 hello 메시지 될-를 통해 진단 검색 합니다.
* *Hello 포털에서 REST API tooget 데이터는 무엇입니까?*

    예, hello [데이터 액세스 API](https://dev.applicationinsights.io/)합니다. 다른 방법으로 tooextract 데이터 포함 [분석 tooPower BI에서에서 내보낼](app-insights-export-power-bi.md) 및 [연속 내보내기를](app-insights-export-telemetry.md)합니다.

## <a name="next"></a>다음 단계
* [검색 이벤트 및 로그](app-insights-diagnostic-search.md)

* [문제 해결](app-insights-troubleshoot-faq.md)


