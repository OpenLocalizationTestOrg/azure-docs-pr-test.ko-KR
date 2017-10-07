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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="975ab-103">필터링 및 hello Application Insights SDK의에서 원격 분석을 전처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="975ab-104">작성 및 hello Application Insights SDK toocustomize 원격 분석은 캡처하고 toohello Application Insights 서비스에 전송 되기 전에 처리 하는 방법에 대 한 플러그 인을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="975ab-105">[샘플링](app-insights-sampling.md) hello 양의 원격 분석 통계에 영향을 주지 않고 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="975ab-106">관련 데이터 요소를 함께 유지하여 문제를 진단할 때 데이터 요소 간을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="975ab-107">Hello 포털 hello 총 개수는 hello 샘플링에 대 한 toocompensate를 곱한 값된입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="975ab-108">원격 분석 프로세서를 사용 하 여 필터링 [ASP.NET에 대 한](#filtering) 또는 [Java](app-insights-java-filter-telemetry.md) 선택 하거나 toohello 서버 전송 하기 전에 hello SDK의에서 원격 분석을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="975ab-109">예를 들어 로봇에서 요청을 제외 하 여 원격 분석의 hello 볼륨을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="975ab-110">하지만 필터링은 샘플링 보다 더 기본적인 방법은 tooreducing 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="975ab-111">전송 작업을 통해 더 많은 제어 기능 그러나 toobe 통계-예를 들어 영향 모든 성공한 요청을 필터링 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="975ab-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="975ab-112">[속성을 추가 하는 원격 분석 이니셜라이저](#add-properties) hello 기본 모듈에서 원격 분석을 포함 하 여 응용 프로그램에서 보낸 tooany 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="975ab-113">예를 들어 계산 된 값이 있습니다.; 추가할 수 있습니다. 또는 hello 포털에서 toofilter hello 데이터 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="975ab-114">[hello SDK API](app-insights-api-custom-events-metrics.md) toosend 사용 되는 사용자 지정 이벤트 및 메트릭이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="975ab-115">시작하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-115">Before you start:</span></span>

* <span data-ttu-id="975ab-116">Hello Application Insights 설치 [ASP.NET에 대 한 SDK](app-insights-asp-net.md) 또는 [SDK for Java](app-insights-java-get-started.md) 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="975ab-117">필터링: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="975ab-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="975ab-118">이 기법을 사용 하면 원격 분석 스트림에 hello에서 제외 되거나 포함 무엇 보다 직접적으로 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="975ab-119">샘플링과 함께 사용할 수도 있고 또는 따로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="975ab-120">toofilter 원격 분석을 작성 한 원격 분석 프로세서 hello SDK로 등록.</span><span class="sxs-lookup"><span data-stu-id="975ab-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="975ab-121">모든 원격 분석 해당 프로세서를 거친 toodrop를 선택할 수 있습니다 hello에서 스트림, 또는 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="975ab-122">Hello HTTP 요청 수집기 hello 종속성 수집기 등의 표준 모듈 hello에서에서 원격 분석와 사용자가 직접 작성 한 원격 분석이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="975ab-123">예를 들어 로봇 또는 성공적인 종속성 호출에서 요청에 대한 원격 분석을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="975ab-124">Hello SDK에서에서 전송 하는 hello 원격 분석 필터링 기울일 수 프로세서를 사용 하 여 관련 된 항목 hello 통계 hello 포털에서 참조 하 고 어려운 toofollow 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="975ab-125">대신 [샘플링](app-insights-sampling.md)사용을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="975ab-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="975ab-126">원격 분석 프로세서 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="975ab-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="975ab-127">프로젝트에 해당 hello Application Insights SDK 버전 2.0.0 확인 이상.</span><span class="sxs-lookup"><span data-stu-id="975ab-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="975ab-128">Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="975ab-129">NuGet 패키지 관리자에서 Microsoft.ApplicationInsights.Web을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="975ab-130">필터를 toocreate ITelemetryProcessor를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="975ab-131">원격 분석 모듈, 원격 분석 이니셜라이저 및 원격 분석 채널와 같은 또 다른 확장성 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="975ab-132">원격 분석 프로세서는 일련의 프로세싱을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="975ab-133">원격 분석 처리기를 인스턴스화할 hello 체인 링크 toohello 다음 프로세서를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="975ab-134">원격 분석 데이터 요소 toohello 프로세스 메서드를 전달 되는 작업을 수행 및 다음 호출 hello hello 체인의 다음 원격 분석 프로세서.</span><span class="sxs-lookup"><span data-stu-id="975ab-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="975ab-135">ApplicationInsights.config에 다음을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="975ab-136">(이 hello 동일한 섹션 샘플링 필터를 초기화 합니다.)</span><span class="sxs-lookup"><span data-stu-id="975ab-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="975ab-137">클래스의 공용 명명 된 속성을 제공 하 여 hello.config 파일에서 문자열 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="975ab-138">Toomatch hello 형식 이름 및 hello.config 파일 toohello 클래스의 속성 이름 및 hello 코드의 속성 이름에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="975ab-139">Hello.config 파일에서 존재 하지 않는 형식 또는 속성을 참조 하는 경우 SDK hello 실패할 수 있습니다 자동으로 toosend 모든 원격 분석.</span><span class="sxs-lookup"><span data-stu-id="975ab-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="975ab-140">**또는** 코드에서 hello 필터를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="975ab-141">적합 한 초기화를 클래스-예를 들어 Global.asax.cs에 AppStart-hello 체인에 프로세서를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="975ab-142">이 시점 이후에 만든 TelemetryClients는 프로세서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="975ab-143">예제 필터</span><span class="sxs-lookup"><span data-stu-id="975ab-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="975ab-144">가상 요청</span><span class="sxs-lookup"><span data-stu-id="975ab-144">Synthetic requests</span></span>
<span data-ttu-id="975ab-145">보트 및 웹 테스트를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-145">Filter out bots and web tests.</span></span> <span data-ttu-id="975ab-146">메트릭 탐색기를 사용 하면 가상 원본을 옵션 toofilter hello를이 옵션 hello SDK에서 필터링 하 여 트래픽을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="975ab-147">실패한 인증</span><span class="sxs-lookup"><span data-stu-id="975ab-147">Failed authentication</span></span>
<span data-ttu-id="975ab-148">"401" 응답을 사용하여 요청을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="975ab-149">빠른 원격 종속성 호출을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="975ab-150">느린 toodiagnose 호출만 하려는 경우 hello fast 것을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="975ab-151">이 hello 포털에 표시 하는 hello 통계 왜곡 됩니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="975ab-152">hello 종속성 차트 hello 종속성 호출 모든 오류가 발생 하는 경우 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="975ab-153">종속성 문제 진단</span><span class="sxs-lookup"><span data-stu-id="975ab-153">Diagnose dependency issues</span></span>
<span data-ttu-id="975ab-154">[이 블로그](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) 일반 ping toodependencies를 자동으로 전송 하 여 프로젝트 toodiagnose 종속성 문제에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="975ab-155">속성 추가: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="975ab-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="975ab-156">된 모든 원격 분석; 보내는 원격 분석 이니셜라이저 toodefine 전역 속성을 사용 하 여 및 toooverride hello 표준 원격 분석 모듈의 동작을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="975ab-157">예를 들어 hello Application Insights 웹 패키지에 대 한 HTTP 요청에 대 한 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="975ab-158">기본적으로, 모든 요청을 응답 코드 > = 400으로 실패한 것으로 플래그합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="975ab-159">하지만 성공으로 400 tootreat 원하는 hello 성공 속성을 설정 하는 원격 분석 이니셜라이저를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="975ab-160">hello Track*() 때마다 호출 됩니다는 원격 분석 이니셜라이저를 제공 하는 경우 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="975ab-161">Hello 표준 원격 분석 모듈에 의해 호출 되는 메서드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="975ab-162">규칙에 따라 이러한 모듈은 이니셜라이저에서 이미 설정된 모든 속성을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="975ab-163">**이니셜라이저 정의**</span><span class="sxs-lookup"><span data-stu-id="975ab-163">**Define your initializer**</span></span>

<span data-ttu-id="975ab-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="975ab-164">*C#*</span></span>

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

<span data-ttu-id="975ab-165">**이니셜라이저 로드**</span><span class="sxs-lookup"><span data-stu-id="975ab-165">**Load your initializer**</span></span>

<span data-ttu-id="975ab-166">ApplicationInsights.config에서:</span><span class="sxs-lookup"><span data-stu-id="975ab-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="975ab-167">*또는* Global.aspx.cs 예를 들어 코드에서 hello 이니셜라이저를 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="975ab-168">이 샘플에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="975ab-169">JavaScript 원격 분석 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="975ab-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="975ab-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="975ab-170">*JavaScript*</span></span>

<span data-ttu-id="975ab-171">원격 분석 이니셜라이저 hello 포털에서 가져온 hello 초기화 코드 바로 뒤에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="975ab-172">에 대 한 요약 hello hello telemetryItem에 사용할 수 있는 사용자 지정이 아닌 속성을 참조 하세요. [응용 프로그램 통찰력 내보낼 데이터 모델](app-insights-export-data-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="975ab-173">이니셜라이저를 원하는 수만큼 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="975ab-174">ITelemetryProcessor 및 ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="975ab-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="975ab-175">Hello 프로세서 원격 분석 및 원격 분석 이니셜라이저 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="975ab-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="975ab-176">이러한 수행할 수 있는 작업에 몇 가지 overlaps는: 모두 사용 하는 tooadd 속성 tootelemetry 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="975ab-177">TelemetryInitializers는 항상 TelemetryProcessors 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="975ab-178">TelemetryProcessors는 toocompletely 덮어쓰기를 허용 하거나 원격 분석 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="975ab-179">TelemetryProcessors는 성능 카운터 원격 분석을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="975ab-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="975ab-180">참조 문서</span><span class="sxs-lookup"><span data-stu-id="975ab-180">Reference docs</span></span>
* [<span data-ttu-id="975ab-181">API 개요</span><span class="sxs-lookup"><span data-stu-id="975ab-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="975ab-182">ASP.NET 참조</span><span class="sxs-lookup"><span data-stu-id="975ab-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="975ab-183">SDK 코드</span><span class="sxs-lookup"><span data-stu-id="975ab-183">SDK Code</span></span>
* [<span data-ttu-id="975ab-184">ASP.NET 핵심 SDK</span><span class="sxs-lookup"><span data-stu-id="975ab-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="975ab-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="975ab-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="975ab-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="975ab-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="975ab-187"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="975ab-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="975ab-188">검색 이벤트 및 로그</span><span class="sxs-lookup"><span data-stu-id="975ab-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="975ab-189">샘플링</span><span class="sxs-lookup"><span data-stu-id="975ab-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="975ab-190">문제 해결</span><span class="sxs-lookup"><span data-stu-id="975ab-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
