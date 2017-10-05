---
title: "Java 웹앱에서 Azure Application Insights 원격 분석 필터링 | Microsoft Docs"
description: "모니터링하지 않아도 되는 이벤트를 필터링하여 원격 분석 트래픽을 줄입니다."
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
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="f76ce-103">Java 웹앱에서 원격 분석 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="f76ce-104">필터는 [Java 웹앱이 Application Insights로 보내는](app-insights-java-get-started.md) 원격 분석을 선택하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="f76ce-105">사용할 수 있는 몇 가지 기본 필터가 있으며 사용자 지정 필터를 직접 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="f76ce-106">기본 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="f76ce-107">추적 심각도 수준</span><span class="sxs-lookup"><span data-stu-id="f76ce-107">Trace severity level</span></span>
* <span data-ttu-id="f76ce-108">특정 URL, 키워드 또는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="f76ce-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="f76ce-109">빠른 응답(앱이 빠르게 응답한 요청)</span><span class="sxs-lookup"><span data-stu-id="f76ce-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="f76ce-110">특정 이벤트 이름</span><span class="sxs-lookup"><span data-stu-id="f76ce-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="f76ce-111">필터는 앱 메트릭의 타이밍 스큐를 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="f76ce-112">예를 들어 느린 응답을 진단하기 위해서는 빠른 응답 시간을 삭제하는 필터를 설정하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="f76ce-113">하지만 Application Insights에서 보고하는 평균 응답 시간이 실제 속도보다 느리고 요청 수가 실제 수보다 작을 것이라는 점을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="f76ce-114">이것이 문제가 될 경우 대신 [샘플링](app-insights-sampling.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="f76ce-115">필터 설정</span><span class="sxs-lookup"><span data-stu-id="f76ce-115">Setting filters</span></span>

<span data-ttu-id="f76ce-116">ApplicationInsights.xml에서 다음 예제와 같이 `TelemetryProcessors` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want to see -->
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




<span data-ttu-id="f76ce-117">[전체 기본 제공 프로세서 집합을 검사](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor)합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="f76ce-118">기본 제공 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="f76ce-119">메트릭 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="f76ce-120">`NotNeeded` - 쉼표로 구분된 사용자 지정 메트릭 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="f76ce-121">페이지 보기 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="f76ce-122">`DurationThresholdInMS` - 기간은 페이지를 로드하는 데 걸린 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="f76ce-123">이 값으로 설정하는 경우 이 시간보다 더 빠르게 로드된 페이지는 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="f76ce-124">`NotNeededNames` - 쉼표로 구분된 페이지 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="f76ce-125">`NotNeededUrls` - 쉼표로 구분된 URL 조각 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="f76ce-126">예를 들어 `"home"`은 URL에 "home"이 포함된 모든 페이지를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="f76ce-127">요청 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="f76ce-128">가상 원본 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-128">Synthetic Source filter</span></span>

<span data-ttu-id="f76ce-129">SyntheticSource 속성에 값이 있는 모든 원격 분석을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="f76ce-130">여기에는 봇, 스파이더 및 가용성 테스트에 대한 요청이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="f76ce-131">모든 가상 요청에 대한 원격 분석을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="f76ce-132">특정 가상 원본에 대한 원격 분석을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="f76ce-133">`NotNeeded` - 쉼표로 구분된 가상 원본 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="f76ce-134">원격 분석 이벤트 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-134">Telemetry Event filter</span></span>

<span data-ttu-id="f76ce-135">사용자 지정 이벤트를 필터링합니다([TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)를 사용하여 로깅됨).</span><span class="sxs-lookup"><span data-stu-id="f76ce-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="f76ce-136">`NotNeededNames` - 쉼표로 구분된 이벤트 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="f76ce-137">추적 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-137">Trace Telemetry filter</span></span>

<span data-ttu-id="f76ce-138">로그 추적을 필터링합니다([TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 또는 [로깅 프레임워크 수집기](app-insights-java-trace-logs.md)를 사용하여 로깅됨).</span><span class="sxs-lookup"><span data-stu-id="f76ce-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="f76ce-139">`FromSeverityLevel` 유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="f76ce-140">OFF             - 모든 추적 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="f76ce-141">TRACE           - 필터링하지 않음</span><span class="sxs-lookup"><span data-stu-id="f76ce-141">TRACE           - No filtering.</span></span> <span data-ttu-id="f76ce-142">추적 수준과 같음</span><span class="sxs-lookup"><span data-stu-id="f76ce-142">equals to Trace level</span></span>
 *  <span data-ttu-id="f76ce-143">INFO            - TRACE 수준 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="f76ce-144">WARN            - TRACE 및 INFO 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="f76ce-145">ERROR           - WARN, INFO, TRACE 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="f76ce-146">CRITICAL        - CRITICAL를 제외하고 모두 필터링</span><span class="sxs-lookup"><span data-stu-id="f76ce-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="f76ce-147">사용자 지정 필터</span><span class="sxs-lookup"><span data-stu-id="f76ce-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="f76ce-148">1. 필터 코드</span><span class="sxs-lookup"><span data-stu-id="f76ce-148">1. Code your filter</span></span>

<span data-ttu-id="f76ce-149">코드에서 `TelemetryProcessor`를 구현하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
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


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="f76ce-150">2. 구성 파일에서 필터 호출</span><span class="sxs-lookup"><span data-stu-id="f76ce-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="f76ce-151">ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="f76ce-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="f76ce-152">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f76ce-152">Troubleshooting</span></span>

<span data-ttu-id="f76ce-153">*내 필터가 작동하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="f76ce-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="f76ce-154">유효한 매개 변수 값을 제공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="f76ce-155">예를 들어 기간은 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-155">For example, durations should be integers.</span></span> <span data-ttu-id="f76ce-156">잘못된 값을 설정하면 필터가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="f76ce-157">사용자 지정 필터가 생성자 또는 set 메서드에서 예외를 throw하는 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f76ce-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f76ce-158">Next steps</span></span>

* <span data-ttu-id="f76ce-159">[샘플링](app-insights-sampling.md) - 메트릭을 스큐하지 않는 대안으로 샘플링을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="f76ce-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
