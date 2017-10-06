---
title: "Azure Application Insights에서 aaaTelemetry 샘플링 | Microsoft Docs"
description: "어떻게 tookeep hello 양의 원격 분석 제어 합니다."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Application Insights의 샘플링


샘플링은 [Azure Application Insights](app-insights-overview.md)의 기능입니다. 이 응용 프로그램 데이터의 올바른 통계적으로 분석을 계속 사용 하면서 방식으로 tooreduce 원격 분석 트래픽 및 저장소를 권장 하는 hello입니다. hello 필터 진단 조사를 수행 하는 경우 항목 간을 탐색할 수 있도록 관련 된 항목을 선택 합니다.
메트릭 개수 tooyou hello 포털에서 표시 하는 경우 이러한는 구하고 다시 정규화 된의 샘플링의 경우 모든 hello 통계에 영향을 toominimize hello tootake 계정.

샘플링은 트래픽 및 데이터 비용을 줄여주며 제한을 피하는 데 도움이 됩니다.

## <a name="in-brief"></a>개요:
* 샘플링에 1 유지  *n*  기록 되 고 hello 나머지를 무시 합니다. 예를 들어 20%의 샘플링 속도로 5개의 이벤트 1을 유지할 수 있습니다. 
* 응용 프로그램이 다양한 원격 분석을 보내는 경우 샘플링은 ASP.NET 웹 서버 앱에서 자동으로 발생합니다.
* 샘플링 중 하나에 hello 수동으로 설정할 수도 있습니다 가격 책정 페이지; hello에 포털 또는 hello.config 파일의 ASP.NET SDK hello에 tooalso는 hello 네트워크 트래픽이 감소 합니다.
* 사용자 지정 이벤트를 기록 경우 toomake 하는 이벤트 집합이 유지 되는지 아니면 함께 삭제 되었는지 같은 OperationId 값을 hello가 있는지 확인 합니다.
* hello 샘플링 divisor  *n*  hello 속성의 각 레코드에 보고 `itemCount`, 검색에는 hello 이름 "요청 수" 또는 "event count" 아래에 나타납니다. 샘플링이 작업 중이지 않을 때 `itemCount==1`입니다.
* 분석 쿼리를 작성하는 경우 [샘플링을 고려](app-insights-analytics-tour.md#counting-sampled-data)해야 합니다. 특히, 레코드를 단순히 세는 대신 `summarize sum(itemCount)`를 사용해야 합니다.

## <a name="types-of-sampling"></a>샘플링 유형
다음은 세 가지 대체 샘플링 방법입니다.

* **적응 샘플링** ASP.NET 응용 프로그램에서 SDK hello에서 전송 하는 원격 분석의 hello 볼륨을 자동으로 조정 합니다. 기본 버전은 SDK v 2.0.0-beta3입니다. 현재 ASP.NET 서버 측 원격 분석만 사용할 수 있습니다. 
* **고정 비율 샘플링** ASP.NET 서버 모두에서 사용자의 브라우저에서 전송 하는 원격 분석의 hello 볼륨을 줄일 수 있습니다. Hello 속도 설정할 수 있습니다. hello 클라이언트와 서버 동기화의 샘플링 되므로 해당에 검색 관련된 페이지 보기 및 요청 간에 이동할 수 있습니다.
* **수집 샘플링** hello Azure 포털에서에서 작동 합니다. 설정 하는 속도로 응용 프로그램에서 도착 하는 hello 원격 분석 중 일부를 삭제 합니다. 원격 분석 트래픽을 줄이지는 않지만 월간 할당량 내로 유지하는 데 도움이 됩니다. 수집 샘플링의 큰 장점은 hello 응용 프로그램을 다시 배포 하지 않고 설정할 수 있습니다 및 모든 서버와 클라이언트에 대 한 균일 하 게 작동 됩니다. 

적응 또는 고정 비율 샘플링이 작업 중인 경우 수집 샘플링은 비활성화됩니다.

## <a name="ingestion-sampling"></a>수집 샘플링
이러한 형태의 샘플링 웹 서버, 브라우저 및 장치에서 원격 분석 hello hello Application Insights 서비스 끝점에 도달 하면 여기서 hello 지점에서 작동 합니다. Hello 양을 줄일 수는 있지만 응용 프로그램에서 전송 하는 hello 원격 분석 사용량을 줄이기 위해 하지 않는 것 처리 하 고 보존 (및 유료로 제공) Application Insights에서 합니다.

이러한 종류의 샘플링을 사용 하 여 앱 월별 할당량을 초과 자주 초과 샘플링의 hello SDK 기반 유형 중 하나를 사용 하 여 hello 옵션이 없는 경우. 

Hello 샘플링 속도 hello 할당량 및 가격 책정 블레이드를 설정 합니다.

![Hello 응용 프로그램 개요 블레이드에서 샘플링 주기, 설정, 할당량, 샘플를 클릭 한 다음 선택한 업데이트를 클릭 합니다.](./media/app-insights-sampling/04.png)

다른 종류의 샘플링와 마찬가지로 hello 알고리즘 관련된 원격 분석 항목을 유지합니다. 예를 들어 검색의 hello 원격 분석을 검사 하려는 경우 수 toofind hello 요청과 관련 tooa 특정 예외입니다. 요청 빈도 및 예외 처리 빈도와 같은 메트릭 수는 올바르게 유지됩니다.

샘플링에서 무시된 데이터 요소는 [연속 내보내기](app-insights-export-telemetry.md)와 같은 Application Insights 기능에서 사용할 수 없습니다.

SDK 기반 적응 또는 고정 비율 샘플링이 작동되는 동안에는 수집 샘플링이 작동하지 않습니다. 100% 보다 작은 hello SDK hello 샘플링 비율을 사용 하는 경우 다음 hello 설정한 수집 샘플링 속도 무시 됩니다.

> [!WARNING]
> hello 타일에 표시 된 hello 값 수집 샘플링에 대해 설정한 hello 값을 나타냅니다. 샘플링 SDK가 작동 하는 경우 hello 실제 샘플링 속도 이므로 나타낼 하지 않습니다.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>웹 서버의 적응 샘플링
적응 샘플링 hello Application Insights SDK v 2.0.0-beta3 ASP.NET 및 이후 버전에 대해 사용할 수 있으며 기본적으로 사용 됩니다. 

적응 샘플링 hello 볼륨을 웹 서버 응용 프로그램 toohello Application Insights 서비스에서에서 보낸 원격 분석의 영향을 줍니다. hello 볼륨은 자동으로 조정 tookeep 트래픽의 지정 된 최대 속도로 내에서.

적은 양의 원격 분석에서는 작동하지 않으므로 사용량이 적은 웹 사이트 또는 디버그 중인 앱은 영향을 받지 않습니다.

생성 된 hello 원격 분석 중 일부 tooachieve hello 대상 볼륨 삭제 됩니다. 하지만 다른 형식의 샘플링의 경우와 마찬가지로 hello 알고리즘 관련된 원격 분석 항목을 보유 합니다. 예를 들어 검색의 hello 원격 분석을 검사 하려는 경우 수 toofind hello 요청과 관련 tooa 특정 예외입니다. 

메트릭 또는 같은 요청 속도 예외 비율 샘플링 주기, hello에 대 한 조정 된 toocompensate 메트릭 탐색기에서 올바른 약 값 표시 되도록를 계산 합니다.

**프로젝트의 NuGet 업데이트** toohello를 최신 패키지 *시험판* 버전의 Application Insights: hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭, NuGet 패키지 관리 선택 확인 **포함 시험판** Microsoft.ApplicationInsights.Web으로 검색 합니다. 

[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), hello에 여러 매개 변수를 조정할 수 있습니다 `AdaptiveSamplingTelemetryProcessor` 노드. 표시 된 hello 수치 hello 기본값으로 사용 됩니다.

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    hello 적응 알고리즘 hello 대상 비율 목표에 대 한 **각 서버 호스트에서**합니다. 웹 앱에서는 많은 호스트에서 실행 하는 경우이 값을 따라서 hello Application Insights 포털에서 트래픽 속도가 대상 내에서 tooremain으로 줄입니다.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    hello 간격을 현재 속도입니다. 원격 분석에는 hello 다시 평가 됩니다. 평가는 이동 평균으로 수행됩니다. 원격 분석은 책임 toosudden 급증 하는 경우이 간격은 tooshorten 할 수 있습니다.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    샘플링 백분율 값을 얼마나 빨리 후 변경이 경우 데이터를 적게 toocapture 백분율을 다시 샘플링 toolower 허용 했습니다.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    샘플링 백분율 값을 얼마나 빨리 후 변경이 म 허용 백분율을 다시 샘플링 tooincrease toocapture 더 많은 데이터입니다.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Hello 최소값 비율 샘플링 변경 됨에 따라 란 tooset 허용 하는 것입니다.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Hello 최 댓 값 이란 비율 샘플링 변경 됨에 따라 tooset 허용 하는 것입니다.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    이동 평균 hello hello 계산을 hello 가중치 toohello 최신 값을 할당 합니다. 1 보다 작은 값 같은 tooor를 사용 합니다. Hello 알고리즘 덜 사후 toosudden 변경을 수행 하는 값이 작을수록 하십시오.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    hello 앱만 시작 될 때 할당 하는 hello 값입니다. 디버깅하는 동안 이 값을 줄이지 마십시오. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    세미콜론으로 구분한 목록 toobe 샘플링 하지 않으려면 형식입니다. 인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적 Hello의 모든 인스턴스를 지정 된 형식을 전송 됩니다. 지정 되지 않은 hello 형식 샘플링 됩니다.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    샘플링 toobe 원하는 형식의 세미콜론으로 구분 된 목록입니다. 인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적 hello 지정 형식을 샘플링 됩니다. 모든 인스턴스 hello의 유형도 항상 전송 되지 것입니다.


**off tooswitch** 적응 샘플링을 applicationinsights-config에서 hello AdaptiveSamplingTelemetryProcessor 노드를 제거 합니다.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>대체: 코드에서 적응 샘플링 구성
Hello.config 파일의 샘플링을 조정 하는 대신 코드를 사용할 수 있습니다. 그러면 toospecify hello 샘플링 비율을 다시 평가할 때마다 호출 되는 콜백 함수. 사용할 수 있습니다, 샘플링 속도 아웃 toofind 사용량 예를 들어 있습니다.

Hello 제거 `AdaptiveSamplingTelemetryProcessor` hello.config 파일에서 노드.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>JavaScript를 사용하는 웹 페이지에 대한 샘플링
서버에서 고정 비율 샘플링에 대한 웹 페이지를 구성할 수 있습니다. 

때 있습니다 [Application Insights에 대 한 hello 웹 페이지 구성](app-insights-javascript.md), hello Application Insights 포털에서 얻을 수 있는 hello 조각 수정 합니다. (ASP.NET 응용 프로그램에서 hello 조각은 일반적으로에 포함할지 _Layout.cshtml.)  같은 줄을 삽입 `samplingPercentage: 10,` hello 계측 키 하기 전에:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Hello 샘플링 비율에 대 한 백분율을 닫기 too100/N 여기서 N은 정수를 선택 합니다.  현재 샘플링은 다른 값을 지원하지 않습니다.

Hello 서버에서 고정 비율 샘플링 사용 하면, 해당에 검색 관련된 페이지 보기 및 요청 간에 탐색할 수 있도록 hello 클라이언트와 서버 동기화 됩니다.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>ASP.NET 웹 사이트에 대한 고정 비율 샘플링
웹 서버와 웹 브라우저에서 전송 하는 hello 트래픽이 감소 하는 고정된 비율 샘플링 합니다. 적응 샘플링과 달리 사용자가 결정한 고정 비율로 원격 분석을 줄어듭니다. 것도 동기화 hello 클라이언트와 서버 샘플링 하므로 관련된 항목의 보존-예를 들어 검색에서 페이지 보기를 보면 관련된 요청을 찾을 수 있습니다 수 있도록 합니다.

hello 샘플링 알고리즘 관련된 항목을 유지합니다. 각 HTTP 요청 이벤트에 대해 해당 이벤트와 관련 이벤트가 삭제되거나 전송됩니다. 

메트릭 탐색기에서 예외 및 요청 수 같은 속도 곱할 hello 샘플링 속도 대 한 계수 toocompensate 약 올바른 되도록 합니다.

1. **프로젝트의 NuGet 패키지를 업데이트** toohello 최신 *시험판* Application Insights의 버전입니다. 솔루션 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭, NuGet 패키지 관리 선택 확인 **시험판 포함** Microsoft.ApplicationInsights.Web으로 검색 합니다. 
2. **적응 샘플링을 사용 하지 않도록 설정**:에서 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), 제거 하거나 주석으로 hello `AdaptiveSamplingTelemetryProcessor` 노드.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Hello 고정 비율 샘플링 모듈을 사용 하도록 설정 합니다.** 이 코드 조각이 너무 추가[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Hello 샘플링 비율에 대 한 백분율을 닫기 too100/N 여기서 N은 정수를 선택 합니다.  현재 샘플링은 다른 값을 지원하지 않습니다.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>대체: 서버 코드에서 고정 비율 샘플링을 사용하도록 설정
Hello.config 파일의 hello 샘플링 매개 변수를 설정 하는 대신 코드를 사용할 수 있습니다. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>때 toouse 샘플링?
ASP.NET SDK 버전 2.0.0-beta3 hello를 사용 하는 경우 적응 샘플링 자동으로 활성화 이상. 사용하는 SDK 버전에 상관없이 서버에서 수집 샘플링을 사용할 수 있습니다.

대부분의 중소 응용 프로그램은 샘플링하지 않아도 됩니다. hello 가장 유용한 진단 정보와 가장 정확한 통계는 모든 사용자 활동에서 데이터를 수집 하 여 가져옵니다. 

hello 샘플링의 주요 이점은 다음과 같습니다.

* 앱이 짧은 시간 간격으로 매우 높은 비율의 원격 분석을 전송할 때 Application Insights 서비스는 ("제한") 데이터 요소를 삭제합니다. 
* hello 내 tookeep [할당량](app-insights-pricing.md) 의 가격 책정 계층에 대 한 데이터 요소입니다. 
* 원격 분석의 hello 컬렉션에서 tooreduce 네트워크 트래픽 

### <a name="which-type-of-sampling-should-i-use"></a>어떤 유형의 샘플링을 사용해야 합니까?
**다음과 같은 경우 수집 샘플링을 사용합니다.**

* 원격 분석의 월간 할당량을 자주 초과하는 경우
* 2 이전 hello 샘플링-예를 지원 하지 않는 SDK, hello Java SDK 또는 ASP.NET 버전의 버전을 사용 하는 합니다.
* 사용자의 웹 브라우저에서 많은 원격 분석이 전송되는 경우

**다음과 같은 경우 고정 비율 샘플링을 사용합니다.**

* ASP.NET 웹 서비스 버전 2.0.0 hello Application Insights SDK를 사용 하는 이후 버전 및
* 원하는 클라이언트와 서버 간에 동기화 된 샘플링의 이벤트를 조사 하려는 경우 있도록 [검색](app-insights-diagnostic-search.md), hello 클라이언트에서 관련된 이벤트 및 페이지 보기 및 http 요청 등 서버 간에 이동할 수 있습니다.
* 확신할 hello 적절 한 샘플링 비율의 앱에 대 한 합니다. 충분히 높은 tooget 정확한 메트릭을 하지만 아래 hello 가격의 할당량을 초과 하는 속도 hello 조절 제한 합니다. 

**다음과 같은 경우 적응 샘플링을 사용합니다.**

그렇지 않은 경우 적응 샘플링을 사용하는 것이 좋습니다. 이 기능은 hello ASP.NET 서버 SDK, 2.0.0-beta3 버전에서는 기본적으로 사용 이상. 특정 최소 속도까지 트래픽을 줄이지 않으므로 사용량이 적은 사이트에는 영향을 주지 않습니다.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>샘플링이 작업 중인지 어떻게 알 수 있나요?
실제 toodiscover hello 샘플링 속도 적용 한에 관계 없이 사용 하 여 프로그램 [분석 쿼리에서](app-insights-analytics.md) 이와 같은:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

각 레코드를 유지 `itemCount` hello 원래 레코드 수를 나타내는 것 같으면 too1 + 이전 레코드는 삭제 된 hello 수를 나타냅니다. 

## <a name="how-does-sampling-work"></a>샘플링은 어떻게 작동되나요?
고정 속도 및 적응 샘플링은 2.0.0부터에서 ASP.NET 버전 hello SDK의 기능입니다. 수집 샘플링 hello Application Insights 서비스의 기능이 며 hello SDK에서 샘플링을 수행 하지 않는 경우 작업에서 될 수 있습니다. 

hello 샘플링 알고리즘을 원격 분석 항목 toodrop 및 어떤 경우라 tookeep (인지 hello SDK 또는 hello Application Insights 서비스)를 결정 합니다. hello 샘플링 의사 결정 toopreserve 모든 서로 관련 된 데이터 요소를 실행 하 고 축소 된 데이터 집합 된 경우에 신뢰할 수 있는 Application Insights에서 진단 환경을 유지 관리 그대로 유지를 목표로 하는 몇 가지 규칙을 기반으로 합니다. 예를 들어 실패한 요청의 경우 앱이 추가 원격 분석 항목을 전송하면(예: 해당 요청에서 기록된 예외 및 추적) 샘플링은 해당 요청 및 기타 원격 분석을 분할하지 않습니다. 전체를 유지하거나 삭제합니다. 결과적으로, Application Insights에서 hello 요청 세부 정보를 볼 때에 항상 보고서 항목과 연결 된 원격 분석 항목 함께 hello 요청을 볼 수 있습니다. 

"User"를 정의 하는 응용 프로그램에 대 한 (즉, 가장 일반적인 웹 응용 프로그램), 즉, 특정 사용자에 대 한 모든 원격 분석은 유지 없거나 삭제 hello 사용자 id의 hello 해시를 기반으로 하는 hello 샘플링 결정 합니다. Hello 유형의 사용자 (예: 웹 서비스)를 정의 하지 않은 응용 프로그램에 대 한 hello 샘플링 의사 결정은 hello 요청의 hello 작업 id를 기반으로 합니다. 마지막으로, (항목에 대 한 예에서는 원격 분석 http 컨텍스트가 없는 비동기 스레드에서 보고) 설정 하는 사용자와 작업 id를도 hello 원격 분석 항목에 대 한 샘플링 간단히 파악 각 유형의 원격 분석 항목의 비율입니다. 

원격 분석 백 tooyou를 표시할 때 hello Application Insights 서비스 조정 하 여 hello 메트릭 hello toocompensate hello 누락 된 데이터 요소에 대 한 컬렉션의 hello 시간에 사용 된 동일한 샘플링 비율입니다. 따라서 Application Insights의 hello 원격 분석을 살펴볼 때는 hello 사용자가 매우 가까운 toohello 실수 있는 올바른 통계적으로 어림 값이 표시 됩니다.

hello 근사값의 hello 정확도 대부분 hello 구성 샘플링 비율에 따라 다릅니다. 또한 많은 양의 다양 한 사용자에서에서 일반적으로 유사한 요청을 처리 하는 응용 프로그램에 대 한 hello 정확도 증가 합니다. 에 상당한 부하를 사용 하지 않는 응용 프로그램에 대 한 다른 손 hello, 이러한 응용 프로그램 수 hello 할당량 제한에서 데이터 손실이 발생 하지 않고 이내로 자신의 모든 원격 분석을 전송 일반적으로 샘플링은 필요 하지 않습니다. 

Note Application Insights 샘플링 하지 메트릭 및 세션 원격 분석 유형을 이후에 이러한 형식에 대 한, 감소 hello 정밀도에 방해가 될 수 있습니다. 

### <a name="adaptive-sampling"></a>적응 샘플링
적응 샘플링 hello SDK에서에서 해당 모니터 hello 현재 속도입니다. 전송 구성 요소를 추가 하 고 hello 샘플링 비율 tootry toostay 내 hello 대상 최대 속도 조정 합니다. hello 조정 정기적으로 다시 계산 및 전송 속도 나가는 hello의 이동 평균을 기반으로 합니다.

## <a name="sampling-and-hello-javascript-sdk"></a>샘플링 및 hello JavaScript SDK
서버 쪽 hello와 함께에서 고정 비율 샘플링에 참여 하는 hello 클라이언트 쪽 (JavaScript) SDK SDK입니다. hello 계측 페이지에서 동일한 사용자에는 hello에 대 한 서버 쪽 결정 해당 너무 "sample에." hello만 클라이언트 쪽 원격 분석을 전송 합니다. 이 논리는 디자인 된 toomaintain 무결성 사용자 세션을 통해 클라이언트-및 서버-면입니다. 결과적으로 Application Insights의 특정 원격 분석 항목에서 해당 사용자 또는 세션에 대한 다른 모든 원격 분석 항목을 찾을 수 있습니다. 

*위에 설명한 대로 내 클라이언트 및 서버 측 원격 분석은 조정된 샘플을 표시하지 않습니다.*

* 서버 및 클라이언트 모두에서 고정 비율 샘플링을 사용할 수 있는지 확인합니다.
* 해당 hello SDK 버전 2.0 인지 확인 이상.
* 설정 하는 검사 hello 같은 hello 클라이언트와 서버 모두에서 비율 샘플링 합니다.

## <a name="frequently-asked-questions"></a>질문과 대답
*샘플링은 왜 간단히 "각 원격 분석 형식의 X 퍼센트를 수집"하지 않습니까?*

* 이 샘플링 방법을 사용 메트릭 어림 값의 자릿수가 매우 높은 제공 하는 사용자, 세션 및 요청 진단에 대 한 중요 한 당 기능 toocorrelate 진단 데이터 끊어지기 합니다. 따라서 샘플링은 "앱 사용자의 X 퍼센트에 대해 모든 원격 분석 항목 수집" 또는 "앱 요청의 X퍼센트에 대한 모든 원격 분석 수집" 논리를 사용하여 더 잘 작동합니다. Hello 요청 (예: 백그라운드 비동기 처리)와 연관 되지 않은 hello 원격 분석 항목에 대 한 hello 년으로 돌아가는 것은 너무 "수집 각 원격 분석 형식에 대 한 모든 항목의 %X." 

*Hello 샘플링 백분율 시간이 지나면서 달라질 수 있습니까?*

* 예, 적응 샘플링 점진적으로 현재 hello 원격 분석의 볼륨을 관찰 하는 hello에 따라 hello 샘플링 비율을 변경 합니다.

*고정 비율 샘플링을 사용 하는 경우 어떻게 알 수 있는 샘플링 비율 작동할지 hello 내 앱에 대 한 최상의?*

* 한 가지 방법은 toostart 적응 샘플링,에 settles 비율 기능에 대해 알아봅니다 (위 질문 hello 참조) 및 스위치 toofixed 속도 비율을 사용 하 여 다음을 샘플링 합니다. 
  
    그렇지 않으면, tooguess를 만들어야 합니다. 즉 발생 하 고 예상 hello 양의 원격 분석 수집 hello 제한을 눈를 AI에서 현재 원격 분석 사용량을 분석 합니다. 선택한 가격 책정 계층을 함께 이러한 세 개의 입력을 얼마나 tooreduce hello 양의 원격 분석 수집 hello 할 수 있습니다 하는 것이 좋습니다. 그러나 hello 사용자 수가 증가 또는 일부 다른 시프트 hello 볼륨 원격 분석의 추정치를 무효화 될 수도 있습니다.

*샘플링 비율을 너무 낮게 구성하는 경우 어떻게 됩니까?*

* Application Insights 시도 hello 데이터 볼륨 축소에 대 한 hello 데이터의 toocompensate hello 시각화 하는 경우 지나치게 낮다고 샘플링 비율 (지나친 샘플링) hello 어림 값의 hello 정확도를 줄여 줍니다. 또한 진단 환경을 부정적인 영향을 받을 수, 일부 자주 실패 하는 hello로 또는 느린 요청 아웃 샘플링할 수 있습니다.

*샘플링 비율을 너무 높게 구성하는 경우 어떻게 됩니까?*

* 원격 분석을 수집 하는 hello 볼륨 hello의 부족 하 여 감소는에서 너무 높게 샘플링 비율 (하지 적극적인 충분히) 결과 구성 합니다. 원격 분석 데이터 손실을 toothrottling와 Application Insights를 사용 하 여 hello 비용 인해 toooverage 요금 계획 된 것 보다 더 높을 수와 관련 된 여전히 발생할 수 있습니다.

*샘플링을 어떤 플랫폼에서 사용할 수 있습니까?*

* 수집 샘플링 hello SDK에서 샘플링을 수행 하지 않는 경우 특정 볼륨, 위의 모든 원격 분석을 위한 자동으로 발생할 수 있습니다. 이 작동할 것, 예를 들어 앱 Java 서버를 사용 하거나 이전 버전의 ASP.NET SDK hello 사용 하는 경우.
* ASP.NET SDK 버전 2.0.0을 사용 하 여 이상 (자체 서버 또는 Azure에서 호스팅), 기본적으로 샘플링 적응 얻을 수 있지만 위에 설명 된 대로 toofixed 속도 전환할 수 있습니다. 고정 비율 샘플링으로 hello 브라우저 SDK를 자동으로 동기화 toosample 관련 이벤트입니다. 

*드문 이벤트 toosee 항상 원하는 것은 아닙니다. 어떻게 확인할 수 있 습에 hello 샘플링 모듈을 지 나?*

* 새 TelemetryConfiguration (hello 기본값이 아닌 활성)와 TelemetryClient의 별도 인스턴스를 초기화 합니다. 해당 toosend 드문 이벤트를 사용 합니다.

## <a name="next-steps"></a>다음 단계
* [필터링](app-insights-api-filtering-sampling.md) 은 SDK에서 보내는 항목을 더 엄격하게 제어할 수 있습니다.

