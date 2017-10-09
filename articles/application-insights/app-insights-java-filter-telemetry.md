---
title: "Java 웹 앱의 Azure Application Insights 원격 분석 aaaFilter | Microsoft Docs"
description: "원격 분석 트래픽을 줄이기 hello 이벤트를 필터링 하 여 toomonitor 필요 하지 않습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a>Java 웹앱에서 원격 분석 필터링

필터 제공 방법을 tooselect hello 원격 분석 하 여 [Java 웹 응용 프로그램 보내는 tooApplication Insights](app-insights-java-get-started.md)합니다. 사용할 수 있는 몇 가지 기본 필터가 있으며 사용자 지정 필터를 직접 작성할 수도 있습니다.

hello 기본적으로 필터는 다음과 같습니다.

* 추적 심각도 수준
* 특정 URL, 키워드 또는 응답 코드
* 빠른 응답-요청을 toowhich 즉, 앱 tooquickly을 응답 했습니다.
* 특정 이벤트 이름

> [!NOTE]
> 필터를 왜곡 시킬 응용 프로그램의 hello 메트릭. 예를 들어, 순서 toodiagnose 느린 응답을 설정 해 필터 toodiscard 빠른 응답 시간을 결정할 수 있습니다. 하지만 Application Insights에서 보고 한 hello 평균 응답 시간 hello true 속도 보다 느린 됩니다 및 요청의 hello 수 hello 실제 개수 보다 작아야 알고 있어야 합니다.
> 이것이 문제가 될 경우 대신 [샘플링](app-insights-sampling.md)을 사용합니다.

## <a name="setting-filters"></a>필터 설정

ApplicationInsights.xml에서 다음 예제와 같이 `TelemetryProcessors` 섹션을 추가합니다.


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




[기본 제공 프로세서 중 일부만 hello 검사](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor)합니다.

## <a name="built-in-filters"></a>기본 제공 필터

### <a name="metric-telemetry-filter"></a>메트릭 원격 분석 필터

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` - 쉼표로 구분된 사용자 지정 메트릭 목록입니다.


### <a name="page-view-telemetry-filter"></a>페이지 보기 원격 분석 필터

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-기간 toohello 백업의 tooload hello 페이지를 참조 합니다. 이 값으로 설정하는 경우 이 시간보다 더 빠르게 로드된 페이지는 보고되지 않습니다.
* `NotNeededNames` - 쉼표로 구분된 페이지 이름 목록입니다.
* `NotNeededUrls` - 쉼표로 구분된 URL 조각 목록입니다. 예를 들어 `"home"` "홈" hello URL에 있는 모든 페이지를 필터링 합니다.


### <a name="request-telemetry-filter"></a>요청 원격 분석 필터


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>가상 원본 필터

Hello SyntheticSource 속성에에서 값을 가진 모든 원격 분석 필터링 합니다. 여기에는 봇, 스파이더 및 가용성 테스트에 대한 요청이 포함됩니다.

모든 가상 요청에 대한 원격 분석을 필터링합니다.


```XML

           <Processor type="SyntheticSourceFilter" />
```

특정 가상 원본에 대한 원격 분석을 필터링합니다.


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` - 쉼표로 구분된 가상 원본 이름 목록입니다.

### <a name="telemetry-event-filter"></a>원격 분석 이벤트 필터

사용자 지정 이벤트를 필터링합니다([TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)를 사용하여 로깅됨).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` - 쉼표로 구분된 이벤트 이름 목록입니다.


### <a name="trace-telemetry-filter"></a>추적 원격 분석 필터

로그 추적을 필터링합니다([TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 또는 [로깅 프레임워크 수집기](app-insights-java-trace-logs.md)를 사용하여 로깅됨).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* `FromSeverityLevel` 유효한 값은 다음과 같습니다.
 *  OFF             - 모든 추적 필터링
 *  TRACE           - 필터링하지 않음 equals tooTrace 수준
 *  INFO            - TRACE 수준 필터링
 *  WARN            - TRACE 및 INFO 필터링
 *  ERROR           - WARN, INFO, TRACE 필터링
 *  CRITICAL        - CRITICAL를 제외하고 모두 필터링


## <a name="custom-filters"></a>사용자 지정 필터

### <a name="1-code-your-filter"></a>1. 필터 코드

코드에서 `TelemetryProcessor`를 구현하는 클래스를 만듭니다.

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Hello 구성 파일에 대 한 필터 호출

ApplicationInsights.xml:

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a>문제 해결

*내 필터가 작동하지 않습니다.*

* 유효한 매개 변수 값을 제공했는지 확인합니다. 예를 들어 기간은 정수여야 합니다. 잘못 된 값 hello 필터 toobe 무시 하면 됩니다. 사용자 지정 필터가 생성자 또는 set 메서드에서 예외를 throw하는 경우 무시됩니다.

## <a name="next-steps"></a>다음 단계

* [샘플링](app-insights-sampling.md) - 메트릭을 스큐하지 않는 대안으로 샘플링을 고려합니다.
