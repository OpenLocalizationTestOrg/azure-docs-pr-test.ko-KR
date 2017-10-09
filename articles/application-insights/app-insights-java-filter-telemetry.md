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
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="66ac6-103">Java 웹앱에서 원격 분석 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="66ac6-104">필터 제공 방법을 tooselect hello 원격 분석 하 여 [Java 웹 응용 프로그램 보내는 tooApplication Insights](app-insights-java-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="66ac6-105">사용할 수 있는 몇 가지 기본 필터가 있으며 사용자 지정 필터를 직접 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="66ac6-106">hello 기본적으로 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="66ac6-107">추적 심각도 수준</span><span class="sxs-lookup"><span data-stu-id="66ac6-107">Trace severity level</span></span>
* <span data-ttu-id="66ac6-108">특정 URL, 키워드 또는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="66ac6-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="66ac6-109">빠른 응답-요청을 toowhich 즉, 앱 tooquickly을 응답 했습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="66ac6-110">특정 이벤트 이름</span><span class="sxs-lookup"><span data-stu-id="66ac6-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="66ac6-111">필터를 왜곡 시킬 응용 프로그램의 hello 메트릭.</span><span class="sxs-lookup"><span data-stu-id="66ac6-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="66ac6-112">예를 들어, 순서 toodiagnose 느린 응답을 설정 해 필터 toodiscard 빠른 응답 시간을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="66ac6-113">하지만 Application Insights에서 보고 한 hello 평균 응답 시간 hello true 속도 보다 느린 됩니다 및 요청의 hello 수 hello 실제 개수 보다 작아야 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="66ac6-114">이것이 문제가 될 경우 대신 [샘플링](app-insights-sampling.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="66ac6-115">필터 설정</span><span class="sxs-lookup"><span data-stu-id="66ac6-115">Setting filters</span></span>

<span data-ttu-id="66ac6-116">ApplicationInsights.xml에서 다음 예제와 같이 `TelemetryProcessors` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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




<span data-ttu-id="66ac6-117">[기본 제공 프로세서 중 일부만 hello 검사](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor)합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="66ac6-118">기본 제공 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="66ac6-119">메트릭 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="66ac6-120">`NotNeeded` - 쉼표로 구분된 사용자 지정 메트릭 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="66ac6-121">페이지 보기 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="66ac6-122">`DurationThresholdInMS`-기간 toohello 백업의 tooload hello 페이지를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="66ac6-123">이 값으로 설정하는 경우 이 시간보다 더 빠르게 로드된 페이지는 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="66ac6-124">`NotNeededNames` - 쉼표로 구분된 페이지 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="66ac6-125">`NotNeededUrls` - 쉼표로 구분된 URL 조각 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="66ac6-126">예를 들어 `"home"` "홈" hello URL에 있는 모든 페이지를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="66ac6-127">요청 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="66ac6-128">가상 원본 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-128">Synthetic Source filter</span></span>

<span data-ttu-id="66ac6-129">Hello SyntheticSource 속성에에서 값을 가진 모든 원격 분석 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="66ac6-130">여기에는 봇, 스파이더 및 가용성 테스트에 대한 요청이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="66ac6-131">모든 가상 요청에 대한 원격 분석을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="66ac6-132">특정 가상 원본에 대한 원격 분석을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="66ac6-133">`NotNeeded` - 쉼표로 구분된 가상 원본 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="66ac6-134">원격 분석 이벤트 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-134">Telemetry Event filter</span></span>

<span data-ttu-id="66ac6-135">사용자 지정 이벤트를 필터링합니다([TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)를 사용하여 로깅됨).</span><span class="sxs-lookup"><span data-stu-id="66ac6-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="66ac6-136">`NotNeededNames` - 쉼표로 구분된 이벤트 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="66ac6-137">추적 원격 분석 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-137">Trace Telemetry filter</span></span>

<span data-ttu-id="66ac6-138">로그 추적을 필터링합니다([TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 또는 [로깅 프레임워크 수집기](app-insights-java-trace-logs.md)를 사용하여 로깅됨).</span><span class="sxs-lookup"><span data-stu-id="66ac6-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="66ac6-139">`FromSeverityLevel` 유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="66ac6-140">OFF             - 모든 추적 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="66ac6-141">TRACE           - 필터링하지 않음</span><span class="sxs-lookup"><span data-stu-id="66ac6-141">TRACE           - No filtering.</span></span> <span data-ttu-id="66ac6-142">equals tooTrace 수준</span><span class="sxs-lookup"><span data-stu-id="66ac6-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="66ac6-143">INFO            - TRACE 수준 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="66ac6-144">WARN            - TRACE 및 INFO 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="66ac6-145">ERROR           - WARN, INFO, TRACE 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="66ac6-146">CRITICAL        - CRITICAL를 제외하고 모두 필터링</span><span class="sxs-lookup"><span data-stu-id="66ac6-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="66ac6-147">사용자 지정 필터</span><span class="sxs-lookup"><span data-stu-id="66ac6-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="66ac6-148">1. 필터 코드</span><span class="sxs-lookup"><span data-stu-id="66ac6-148">1. Code your filter</span></span>

<span data-ttu-id="66ac6-149">코드에서 `TelemetryProcessor`를 구현하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="66ac6-150">2. Hello 구성 파일에 대 한 필터 호출</span><span class="sxs-lookup"><span data-stu-id="66ac6-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="66ac6-151">ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="66ac6-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="66ac6-152">문제 해결</span><span class="sxs-lookup"><span data-stu-id="66ac6-152">Troubleshooting</span></span>

<span data-ttu-id="66ac6-153">*내 필터가 작동하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="66ac6-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="66ac6-154">유효한 매개 변수 값을 제공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="66ac6-155">예를 들어 기간은 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-155">For example, durations should be integers.</span></span> <span data-ttu-id="66ac6-156">잘못 된 값 hello 필터 toobe 무시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="66ac6-157">사용자 지정 필터가 생성자 또는 set 메서드에서 예외를 throw하는 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66ac6-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66ac6-158">Next steps</span></span>

* <span data-ttu-id="66ac6-159">[샘플링](app-insights-sampling.md) - 메트릭을 스큐하지 않는 대안으로 샘플링을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="66ac6-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
