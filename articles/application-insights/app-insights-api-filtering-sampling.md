---
title: "aaaFiltering 및에서 전처리 hello Azure Application Insights SDK | Microsoft Docs"
description: "SDK toofilter hello에 대 한 원격 분석 프로세서 및 원격 분석 이니셜라이저를 작성 하거나 hello 원격 분석 toohello Application Insights 포털에 전송 되기 전에 속성 toohello 데이터를 추가 합니다."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>필터링 및 hello Application Insights SDK의에서 원격 분석을 전처리 합니다.


작성 및 hello Application Insights SDK toocustomize 원격 분석은 캡처하고 toohello Application Insights 서비스에 전송 되기 전에 처리 하는 방법에 대 한 플러그 인을 구성할 수 있습니다.

* [샘플링](app-insights-sampling.md) hello 양의 원격 분석 통계에 영향을 주지 않고 줄어듭니다. 관련 데이터 요소를 함께 유지하여 문제를 진단할 때 데이터 요소 간을 탐색할 수 있습니다. Hello 포털 hello 총 개수는 hello 샘플링에 대 한 toocompensate를 곱한 값된입니다.
* 원격 분석 프로세서를 사용 하 여 필터링 [ASP.NET에 대 한](#filtering) 또는 [Java](app-insights-java-filter-telemetry.md) 선택 하거나 toohello 서버 전송 하기 전에 hello SDK의에서 원격 분석을 수정할 수 있습니다. 예를 들어 로봇에서 요청을 제외 하 여 원격 분석의 hello 볼륨을 줄일 수 있습니다. 하지만 필터링은 샘플링 보다 더 기본적인 방법은 tooreducing 트래픽입니다. 전송 작업을 통해 더 많은 제어 기능 그러나 toobe 통계-예를 들어 영향 모든 성공한 요청을 필터링 하는 경우.
* [속성을 추가 하는 원격 분석 이니셜라이저](#add-properties) hello 기본 모듈에서 원격 분석을 포함 하 여 응용 프로그램에서 보낸 tooany 원격 분석 합니다. 예를 들어 계산 된 값이 있습니다.; 추가할 수 있습니다. 또는 hello 포털에서 toofilter hello 데이터 버전 번호입니다.
* [hello SDK API](app-insights-api-custom-events-metrics.md) toosend 사용 되는 사용자 지정 이벤트 및 메트릭이 됩니다.

시작하기 전에 다음을 수행합니다.

* Hello Application Insights 설치 [ASP.NET에 대 한 SDK](app-insights-asp-net.md) 또는 [SDK for Java](app-insights-java-get-started.md) 응용 프로그램에서 합니다.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>필터링: ITelemetryProcessor
이 기법을 사용 하면 원격 분석 스트림에 hello에서 제외 되거나 포함 무엇 보다 직접적으로 제어 합니다. 샘플링과 함께 사용할 수도 있고 또는 따로 사용할 수도 있습니다.

toofilter 원격 분석을 작성 한 원격 분석 프로세서 hello SDK로 등록. 모든 원격 분석 해당 프로세서를 거친 toodrop를 선택할 수 있습니다 hello에서 스트림, 또는 속성을 추가 합니다. Hello HTTP 요청 수집기 hello 종속성 수집기 등의 표준 모듈 hello에서에서 원격 분석와 사용자가 직접 작성 한 원격 분석이 포함 됩니다. 예를 들어 로봇 또는 성공적인 종속성 호출에서 요청에 대한 원격 분석을 필터링할 수 있습니다.

> [!WARNING]
> Hello SDK에서에서 전송 하는 hello 원격 분석 필터링 기울일 수 프로세서를 사용 하 여 관련 된 항목 hello 통계 hello 포털에서 참조 하 고 어려운 toofollow 확인 합니다.
>
> 대신 [샘플링](app-insights-sampling.md)사용을 고려하세요.
>
>

### <a name="create-a-telemetry-processor-c"></a>원격 분석 프로세서 만들기(C#)
1. 프로젝트에 해당 hello Application Insights SDK 버전 2.0.0 확인 이상. Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다. NuGet 패키지 관리자에서 Microsoft.ApplicationInsights.Web을 선택합니다.
2. 필터를 toocreate ITelemetryProcessor를 구현 합니다. 원격 분석 모듈, 원격 분석 이니셜라이저 및 원격 분석 채널와 같은 또 다른 확장성 지점입니다.

    원격 분석 프로세서는 일련의 프로세싱을 생성합니다. 원격 분석 처리기를 인스턴스화할 hello 체인 링크 toohello 다음 프로세서를 전달 합니다. 원격 분석 데이터 요소 toohello 프로세스 메서드를 전달 되는 작업을 수행 및 다음 호출 hello hello 체인의 다음 원격 분석 프로세서.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. ApplicationInsights.config에 다음을 삽입합니다.

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(이 hello 동일한 섹션 샘플링 필터를 초기화 합니다.)

클래스의 공용 명명 된 속성을 제공 하 여 hello.config 파일에서 문자열 값을 전달할 수 있습니다.

> [!WARNING]
> Toomatch hello 형식 이름 및 hello.config 파일 toohello 클래스의 속성 이름 및 hello 코드의 속성 이름에 주의 해야 합니다. Hello.config 파일에서 존재 하지 않는 형식 또는 속성을 참조 하는 경우 SDK hello 실패할 수 있습니다 자동으로 toosend 모든 원격 분석.
>
>

**또는** 코드에서 hello 필터를 초기화할 수 있습니다. 적합 한 초기화를 클래스-예를 들어 Global.asax.cs에 AppStart-hello 체인에 프로세서를 삽입 합니다.

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

이 시점 이후에 만든 TelemetryClients는 프로세서를 사용합니다.

### <a name="example-filters"></a>예제 필터
#### <a name="synthetic-requests"></a>가상 요청
보트 및 웹 테스트를 필터링합니다. 메트릭 탐색기를 사용 하면 가상 원본을 옵션 toofilter hello를이 옵션 hello SDK에서 필터링 하 여 트래픽을 줄입니다.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>실패한 인증
"401" 응답을 사용하여 요청을 필터링합니다.

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>빠른 원격 종속성 호출을 필터링합니다.
느린 toodiagnose 호출만 하려는 경우 hello fast 것을 필터링 합니다.

> [!NOTE]
> 이 hello 포털에 표시 하는 hello 통계 왜곡 됩니다. hello 종속성 차트 hello 종속성 호출 모든 오류가 발생 하는 경우 처럼 보입니다.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>종속성 문제 진단
[이 블로그](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) 일반 ping toodependencies를 자동으로 전송 하 여 프로젝트 toodiagnose 종속성 문제에 설명 합니다.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>속성 추가: ITelemetryInitializer
된 모든 원격 분석; 보내는 원격 분석 이니셜라이저 toodefine 전역 속성을 사용 하 여 및 toooverride hello 표준 원격 분석 모듈의 동작을 선택 합니다.

예를 들어 hello Application Insights 웹 패키지에 대 한 HTTP 요청에 대 한 원격 분석을 수집합니다. 기본적으로, 모든 요청을 응답 코드 > = 400으로 실패한 것으로 플래그합니다. 하지만 성공으로 400 tootreat 원하는 hello 성공 속성을 설정 하는 원격 분석 이니셜라이저를 제공할 수 있습니다.

hello Track*() 때마다 호출 됩니다는 원격 분석 이니셜라이저를 제공 하는 경우 메서드를 호출 합니다. Hello 표준 원격 분석 모듈에 의해 호출 되는 메서드가 포함 됩니다. 규칙에 따라 이러한 모듈은 이니셜라이저에서 이미 설정된 모든 속성을 설정하지 않습니다.

**이니셜라이저 정의**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**이니셜라이저 로드**

ApplicationInsights.config에서:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*또는* Global.aspx.cs 예를 들어 코드에서 hello 이니셜라이저를 인스턴스화할 수 있습니다.

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[이 샘플에 대해 자세히 알아봅니다.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>JavaScript 원격 분석 이니셜라이저
*JavaScript*

원격 분석 이니셜라이저 hello 포털에서 가져온 hello 초기화 코드 바로 뒤에 삽입 합니다.

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

에 대 한 요약 hello hello telemetryItem에 사용할 수 있는 사용자 지정이 아닌 속성을 참조 하세요. [응용 프로그램 통찰력 내보낼 데이터 모델](app-insights-export-data-model.md)합니다.

이니셜라이저를 원하는 수만큼 추가할 수 있습니다.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor 및 ITelemetryInitializer
Hello 프로세서 원격 분석 및 원격 분석 이니셜라이저 차이 무엇입니까?

* 이러한 수행할 수 있는 작업에 몇 가지 overlaps는: 모두 사용 하는 tooadd 속성 tootelemetry 일 수 있습니다.
* TelemetryInitializers는 항상 TelemetryProcessors 전에 실행됩니다.
* TelemetryProcessors는 toocompletely 덮어쓰기를 허용 하거나 원격 분석 항목을 삭제 합니다.
* TelemetryProcessors는 성능 카운터 원격 분석을 처리하지 않습니다.


## <a name="reference-docs"></a>참조 문서
* [API 개요](app-insights-api-custom-events-metrics.md)
* [ASP.NET 참조](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>SDK 코드
* [ASP.NET 핵심 SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>다음 단계
* [검색 이벤트 및 로그](app-insights-diagnostic-search.md)
* [샘플링](app-insights-sampling.md)
* [문제 해결](app-insights-troubleshoot-faq.md)
