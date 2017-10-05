---
title: "Azure Application Insights SDK에서 필터링 및 전처리 | Microsoft Docs"
description: "SDK용 원격 분석 프로세서 및 원격 분석 이니셜라이저를 작성하여 원격 분석이 Application Insights 포털에 전송되기 전에 데이터에 대한 속성을 필터링하거나 추가합니다."
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="fbeaf-103">Application Insights SDK에서 원격 분석 필터링 및 전처리</span><span class="sxs-lookup"><span data-stu-id="fbeaf-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="fbeaf-104">Application Insights SDK에 대한 플러그인을 작성하고 구성하여 원격 분석을 Application Insights 서비스에 전송하기 전에 캡처하고 처리하는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="fbeaf-105">[샘플링](app-insights-sampling.md) 통계를 왜곡하지 않고 원격 분석의 양을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="fbeaf-106">관련 데이터 요소를 함께 유지하여 문제를 진단할 때 데이터 요소 간을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="fbeaf-107">포털에서는 샘플링을 보완하기 위해 총 개수를 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="fbeaf-108">[ASP.NET](#filtering) 또는 [Java](app-insights-java-filter-telemetry.md)용 원격 분석 프로세서를 사용하여 필터링하면 서버에 전송되기 전에 SDK에서 원격 분석을 선택하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="fbeaf-109">예를 들어 로봇의 요청을 제외하여 원격 분석의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="fbeaf-110">하지만 필터링은 트래픽을 감소시키는 데 있어 샘플링보다 더 기본적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="fbeaf-111">이를 통해 전송된 요청을 더 잘 제어할 수 있지만 통계에 영향을 준다는 점을 알고 있어야 합니다(예: 성공한 모든 요청을 필터링하는 경우).</span><span class="sxs-lookup"><span data-stu-id="fbeaf-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="fbeaf-112">[원격 분석 이니셜라이저](#add-properties) 는 표준 모듈의 원격 분석을 포함한 앱에서 보낸 모든 원격 분석에 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="fbeaf-113">예를 들어 계산된 값을 추가하거나 포털에서 데이터를 필터링하는 데 사용할 버전 번호를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="fbeaf-114">[SDK API](app-insights-api-custom-events-metrics.md) 사용자 지정 이벤트 및 메트릭을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="fbeaf-115">시작하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-115">Before you start:</span></span>

* <span data-ttu-id="fbeaf-116">앱에 Application Insights [SDK for ASP.NET](app-insights-asp-net.md) 또는 [SDK for Java](app-insights-java-get-started.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="fbeaf-117">필터링: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="fbeaf-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="fbeaf-118">이 기술을 사용하면 원격 분석 스트림에서 포함되거나 제외된 요청을 보다 직접적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="fbeaf-119">샘플링과 함께 사용할 수도 있고 또는 따로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="fbeaf-120">원격 분석을 필터링하려면 원격 분석 프로세서를 작성하고 SDK를 사용하여 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="fbeaf-121">모든 원격 분석은 해당 프로세서를 거친 다음 스트림에서 삭제하거나 속성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="fbeaf-122">직접 작성한 원격 분석뿐만 아니라 HTTP 요청 수집기 및 종속성 수집기와 같은 표준 모듈의 원격 분석이 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="fbeaf-123">예를 들어 로봇 또는 성공적인 종속성 호출에서 요청에 대한 원격 분석을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="fbeaf-124">프로세서를 사용하는 SDK에서 보낸 원격 분석을 필터링하는 작업은 포털에 표시되는 통계를 왜곡하고 관련된 항목을 수행하기 어렵게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="fbeaf-125">대신 [샘플링](app-insights-sampling.md)사용을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="fbeaf-126">원격 분석 프로세서 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="fbeaf-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="fbeaf-127">프로젝트의 Application Insights SDK가 버전 2.0.0 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="fbeaf-128">Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="fbeaf-129">NuGet 패키지 관리자에서 Microsoft.ApplicationInsights.Web을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="fbeaf-130">필터를 만들려면 ITelemetryProcessor를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="fbeaf-131">원격 분석 모듈, 원격 분석 이니셜라이저 및 원격 분석 채널와 같은 또 다른 확장성 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="fbeaf-132">원격 분석 프로세서는 일련의 프로세싱을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="fbeaf-133">원격 분석 프로세서를 인스턴스화할 때 과정에서 다음 프로세서에 대한 링크를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="fbeaf-134">원격 분석 데이터 요소가 프로세스 메서드에 전달되는 경우 해당 작업을 수행하고 과정에서 다음 원격 분석 프로세서를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="fbeaf-135">ApplicationInsights.config에 다음을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="fbeaf-136">(샘플링 필터를 초기화하는 섹션과 동일합니다.)</span><span class="sxs-lookup"><span data-stu-id="fbeaf-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="fbeaf-137">클래스에서 명명된 공용 속성을 제공하여 .config 파일의 문자열 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="fbeaf-138">.config 파일의 형식 이름 및 모든 속성 이름이 코드의 클래스 및 속성 이름과 일치하는지 주의하여 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="fbeaf-139">.config 파일에서 존재하지 않는 형식 또는 속성을 참조하는 경우 SDK가 원격 분석을 자동으로 전송하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="fbeaf-140">**또는** 코드에서 필터를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="fbeaf-141">Global.asax.cs의 AppStart과 같은 적합한 초기화 클래스의 과정에서 프로세서를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="fbeaf-142">이 시점 이후에 만든 TelemetryClients는 프로세서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="fbeaf-143">예제 필터</span><span class="sxs-lookup"><span data-stu-id="fbeaf-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="fbeaf-144">가상 요청</span><span class="sxs-lookup"><span data-stu-id="fbeaf-144">Synthetic requests</span></span>
<span data-ttu-id="fbeaf-145">보트 및 웹 테스트를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-145">Filter out bots and web tests.</span></span> <span data-ttu-id="fbeaf-146">메트릭 탐색기가 가상 소스를 필터링하는 옵션을 제공하지만 이 옵션은 SDK에서 필터링하여 트래픽을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="fbeaf-147">실패한 인증</span><span class="sxs-lookup"><span data-stu-id="fbeaf-147">Failed authentication</span></span>
<span data-ttu-id="fbeaf-148">"401" 응답을 사용하여 요청을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="fbeaf-149">빠른 원격 종속성 호출을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="fbeaf-150">느린 호출을 진단하려는 경우 빠른 호출을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="fbeaf-151">이 포털에서 참조하는 통계를 왜곡시킵니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="fbeaf-152">종속성 차트는 종속성 호출이 모두 실패한 것처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="fbeaf-153">종속성 문제 진단</span><span class="sxs-lookup"><span data-stu-id="fbeaf-153">Diagnose dependency issues</span></span>
<span data-ttu-id="fbeaf-154">[이 블로그](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) 에서는 종속성으로 정규 ping을 자동으로 전송하여 종속성 문제를 진단하는 프로젝트에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="fbeaf-155">속성 추가: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="fbeaf-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="fbeaf-156">원격 분석 이니셜라이저를 사용하여 모든 원격 분석과 함께 전송되는 전역 속성을 정의하고 표준 원격 분석 모듈의 선택한 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="fbeaf-157">예를 들어, 웹 패키지에 대한 Application Insights는 HTTP 요청에 대한 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="fbeaf-158">기본적으로, 모든 요청을 응답 코드 > = 400으로 실패한 것으로 플래그합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="fbeaf-159">하지만 400를 성공으로 처리하려는 경우 성공 속성을 설정하는 원격 분석 이니셜라이저를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="fbeaf-160">원격 분석 이니셜라이저를 제공하는 경우 Track*() 메소드가 호출될 때마다 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="fbeaf-161">표준 원격 분석 모듈에 의해 호출되는 메서드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="fbeaf-162">규칙에 따라 이러한 모듈은 이니셜라이저에서 이미 설정된 모든 속성을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="fbeaf-163">**이니셜라이저 정의**</span><span class="sxs-lookup"><span data-stu-id="fbeaf-163">**Define your initializer**</span></span>

<span data-ttu-id="fbeaf-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="fbeaf-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="fbeaf-165">**이니셜라이저 로드**</span><span class="sxs-lookup"><span data-stu-id="fbeaf-165">**Load your initializer**</span></span>

<span data-ttu-id="fbeaf-166">ApplicationInsights.config에서:</span><span class="sxs-lookup"><span data-stu-id="fbeaf-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="fbeaf-167">*또는* , 코드에서 이니셜라이저를 인스턴스화할 수 있습니다(예: Global.aspx.cs).</span><span class="sxs-lookup"><span data-stu-id="fbeaf-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="fbeaf-168">이 샘플에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="fbeaf-169">JavaScript 원격 분석 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="fbeaf-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="fbeaf-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="fbeaf-170">*JavaScript*</span></span>

<span data-ttu-id="fbeaf-171">포털에서 가져온 초기화 코드 바로 뒤에 원격 분석 이니셜라이저를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="fbeaf-172">TelemetryItem에서 사용할 수 있는 사용자 지정이 아닌 속성의 요약은 [Application Insights 데이터 모델 내보내기](app-insights-export-data-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="fbeaf-173">이니셜라이저를 원하는 수만큼 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="fbeaf-174">ITelemetryProcessor 및 ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="fbeaf-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="fbeaf-175">원격 분석 프로세서 및 원격 분석 이니셜라이저 간의 차이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="fbeaf-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="fbeaf-176">두 프로그램으로 수행할 수 있는 작업의 일부가 겹칩니다. 모두 원격 분석에 속성을 추가하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="fbeaf-177">TelemetryInitializers는 항상 TelemetryProcessors 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="fbeaf-178">TelemetryProcessors를 사용하면 원격 분석 항목을 완전히 대체하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="fbeaf-179">TelemetryProcessors는 성능 카운터 원격 분석을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbeaf-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="fbeaf-180">참조 문서</span><span class="sxs-lookup"><span data-stu-id="fbeaf-180">Reference docs</span></span>
* [<span data-ttu-id="fbeaf-181">API 개요</span><span class="sxs-lookup"><span data-stu-id="fbeaf-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="fbeaf-182">ASP.NET 참조</span><span class="sxs-lookup"><span data-stu-id="fbeaf-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="fbeaf-183">SDK 코드</span><span class="sxs-lookup"><span data-stu-id="fbeaf-183">SDK Code</span></span>
* [<span data-ttu-id="fbeaf-184">ASP.NET 핵심 SDK</span><span class="sxs-lookup"><span data-stu-id="fbeaf-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="fbeaf-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="fbeaf-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="fbeaf-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="fbeaf-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="fbeaf-187"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbeaf-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="fbeaf-188">검색 이벤트 및 로그</span><span class="sxs-lookup"><span data-stu-id="fbeaf-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="fbeaf-189">샘플링</span><span class="sxs-lookup"><span data-stu-id="fbeaf-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="fbeaf-190">문제 해결</span><span class="sxs-lookup"><span data-stu-id="fbeaf-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
