---
title: "Application Insights의 성능 카운터 | Microsoft Docs"
description: "Application Insights에서 시스템 및 사용자 지정 .NET 성능 카운터를 모니터링합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="1b60c-103">Application Insights의 시스템 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="1b60c-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="1b60c-104">Windows는 광범위한 [성능 카운터](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters)(예: CPU 점유율, 메모리, 디스크, 네트워크 사용량 등)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="1b60c-105">또한 직접 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-105">You can also define your own.</span></span> <span data-ttu-id="1b60c-106">[Application Insights](app-insights-overview.md)는 관리 액세스 권한이 있는 온-프레미스 호스트 또는 가상 컴퓨터의 IIS에서 응용 프로그램이 실행되는 경우 이러한 성능 카운터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="1b60c-107">차트에서는 라이브 응용 프로그램에 사용할 수 있는 리소스를 나타내고 서버 인스턴스 간의 불균형 부하를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="1b60c-108">성능 카운터는 서버 블레이드에 나타나며, 이 블레이드에는 서버 인스턴스에서 분할한 테이블이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="1b60c-110">(성능 카운터는 Azure Web Apps에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="1b60c-111">하지만 [Azure 진단을 Application Insights에 보낼 수 있습니다](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="1b60c-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="1b60c-112">카운터 보기</span><span class="sxs-lookup"><span data-stu-id="1b60c-112">View counters</span></span>
<span data-ttu-id="1b60c-113">서버 블레이드에서 성능 카운터의 기본 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="1b60c-114">다른 카운터를 보려면 서버 블레이드에서 차트를 편집하거나 새 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드를 열어 새 차트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="1b60c-115">차트를 편집할 때 사용 가능한 카운터가 메트릭으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="1b60c-117">한 곳에서 가장 유용한 차트를 모두 보려면 [대시보드](app-insights-dashboards.md)를 만들어 이 대시보드에 해당 차트를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="1b60c-118">카운터 추가</span><span class="sxs-lookup"><span data-stu-id="1b60c-118">Add counters</span></span>
<span data-ttu-id="1b60c-119">메트릭 목록에서 원하는 성능 카운터를 표시하지 않을 경우 Application Insights SDK에서 웹 서버의 메트릭을 수집하지 않기 때문에 표시하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="1b60c-120">성능 카운터를 표시하지 않도록 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="1b60c-121">서버에서 다음 PowerShell 명령을 사용하여 서버에서 사용할 수 있는 카운터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="1b60c-122">([`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx) 참조)</span><span class="sxs-lookup"><span data-stu-id="1b60c-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="1b60c-123">ApplicationInsights.config를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="1b60c-124">앱에 개발 중인 Application Insights를 추가한 경우 프로젝트에서 ApplicationInsights.config를 편집한 다음 서버에 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="1b60c-125">상태 모니터를 사용하여 런타임 시 웹앱을 계측한 경우 IIS에서 앱의 루트 디렉터리에 있는 ApplicationInsights.config를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="1b60c-126">각 서버 인스턴스에서 해당 ApplicationInsights.config를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="1b60c-127">다음과 같이 성능 수집기 지시문을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="1b60c-128">표준 카운터 및 사용자가 직접 구현한 카운터를 모두 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="1b60c-129">`\Objects\Processes`는 모든 Windows 시스템에서 사용할 수 있는 표준 카운터의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="1b60c-130">`\Sales(photo)\# Items Sold`는 웹 서비스에서 구현할 수 있는 사용자 지정 카운터의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="1b60c-131">형식은 `\Category(instance)\Counter"`이며, 인스턴스가 없는 범주인 경우에는 `\Category\Counter`입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="1b60c-132">`ReportAs`는 `[a-zA-Z()/-_ \.]+`와 일치하지 않는 카운터 이름에 필요합니다. 즉 문자, 둥근 괄호, 슬래시, 하이픈, 밑줄, 공백, 점이 아닌 글자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="1b60c-133">인스턴스를 지정하면 보고된 메트릭의 "CounterInstanceName" 차원으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="1b60c-134">코드에서 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="1b60c-134">Collecting performance counters in code</span></span>
<span data-ttu-id="1b60c-135">시스템 성능 카운터를 수집하고 Application Insights에 보내려면 다음과 같은 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="1b60c-136">또는 만든 사용자 지정 메트릭과 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="1b60c-137">분석에서의 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="1b60c-137">Performance counters in Analytics</span></span>
<span data-ttu-id="1b60c-138">[분석](app-insights-analytics.md)에서 성능 카운터 보고서를 검색하고 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="1b60c-139">**performanceCounters** 스키마는 `category`, `counter` 이름 및 각 성능 카운터의 `instance` 이름을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="1b60c-140">각 응용 프로그램에 대한 원격 분석 데이터에는 해당 응용 프로그램에 대한 카운터에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="1b60c-141">예를 들면 어떤 카운터를 사용할 수 있는지 알아보기:</span><span class="sxs-lookup"><span data-stu-id="1b60c-141">For example, to see what counters are available:</span></span> 

![Application Insights 분석의 성능 카운터](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="1b60c-143">(여기서의 '인스턴스'는 역할이나 서버 컴퓨터 인스턴스가 아니라 성능 카운터 인스턴스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="1b60c-144">성능 카운터 인스턴스 이름은 일반적으로 프로세스 또는 응용 프로그램의 이름을 기준으로 프로세서 시간과 같은 카운터를 분할합니다.)</span><span class="sxs-lookup"><span data-stu-id="1b60c-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="1b60c-145">최근 기간 동안 사용 가능한 메모리의 차트를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="1b60c-145">To get a chart of available memory over the recent period:</span></span> 

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="1b60c-147">다른 원격 분석과 마찬가지로 **performanceCounters**에도 앱이 실행되는 호스트 서버 인스턴스의 ID를 나타내는 `cloud_RoleInstance` 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="1b60c-148">예를 들어, 서로 다른 컴퓨터에서 앱의 성능을 비교하려면:</span><span class="sxs-lookup"><span data-stu-id="1b60c-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="1b60c-150">ASP.NET 및 Application Insights 개수</span><span class="sxs-lookup"><span data-stu-id="1b60c-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="1b60c-151">*예외 속도와 예외 메트릭 간의 차이점은 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="1b60c-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="1b60c-152">*예외 속도* 는 시스템 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="1b60c-153">CLR은 발생하는 처리된 예외 및 처리되지 않은 예외를 모두 계산하고 샘플링 간격의 합계를 간격 길이로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="1b60c-154">Application Insights SDK는 이 결과를 수집하여 포털에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="1b60c-155">*예외* 는 차트의 샘플링 간격에 포털이 받은 TrackException 보고서 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="1b60c-156">코드에서 TrackException 호출을 작성한 처리된 예외만 포함하며, [처리되지 않은 예외](app-insights-asp-net-exceptions.md)는 모두 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="1b60c-157">경고</span><span class="sxs-lookup"><span data-stu-id="1b60c-157">Alerts</span></span>
<span data-ttu-id="1b60c-158">다른 메트릭과 마찬가지로 성능 카운터에서 지정한 제한을 벗어나는 경우 경고 메시지를 표시하도록 [경고를 설정](app-insights-alerts.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="1b60c-159">경고 블레이드를 열고 경고 추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b60c-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="1b60c-160"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b60c-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="1b60c-161">종속성 추적</span><span class="sxs-lookup"><span data-stu-id="1b60c-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="1b60c-162">예외 추적</span><span class="sxs-lookup"><span data-stu-id="1b60c-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

