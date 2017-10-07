---
title: "Application Insights에서 카운터 aaaPerformance | Microsoft Docs"
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
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="fb523-103">Application Insights의 시스템 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="fb523-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="fb523-104">Windows는 광범위한 [성능 카운터](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters)(예: CPU 점유율, 메모리, 디스크, 네트워크 사용량 등)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="fb523-105">또한 직접 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-105">You can also define your own.</span></span> <span data-ttu-id="fb523-106">[Application Insights](app-insights-overview.md) 응용 프로그램에서 실행 중인 경우 IIS에서 온-프레미스 가상 컴퓨터 또는 호스트 toowhich 하면 이러한 성능 카운터에 대 한 관리 권한이 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="fb523-107">hello 차트 hello 리소스 사용 가능한 tooyour 라이브 응용 프로그램을 나타내고 서버 인스턴스 간의 tooidentify 불균형된 부하의 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="fb523-108">서버 인스턴스에서 분할 하는 테이블을 포함 하는 hello 서버 블레이드 성능 카운터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="fb523-110">(성능 카운터는 Azure Web Apps에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="fb523-111">하 고 있지만 [Azure 진단 tooApplication Insights 보낼](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="fb523-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="fb523-112">카운터 보기</span><span class="sxs-lookup"><span data-stu-id="fb523-112">View counters</span></span>
<span data-ttu-id="fb523-113">hello 서버 블레이드 성능 카운터의 기본 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="fb523-114">toosee 다른 카운터 hello 서버 블레이드의 hello 차트를 편집 하거나 새 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드 및 새 차트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="fb523-115">차트를 편집할 때 hello 사용 가능한 카운터 메트릭을으로 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="fb523-117">toosee를 한 곳에서 가장 유용한 모든 차트 만들기는 [대시보드](app-insights-dashboards.md) tooit를 고정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="fb523-118">카운터 추가</span><span class="sxs-lookup"><span data-stu-id="fb523-118">Add counters</span></span>
<span data-ttu-id="fb523-119">원하는 hello 성능 카운터 메트릭 hello Application Insights SDK 웹 서버에서 수집 되지 않습니다 때문에 hello 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="fb523-120">구성할 수 있습니다 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="fb523-121">어떤 카운터는 hello 서버에서이 PowerShell 명령을 사용 하 여 서버에서 사용할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="fb523-122">([`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx) 참조)</span><span class="sxs-lookup"><span data-stu-id="fb523-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="fb523-123">ApplicationInsights.config를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="fb523-124">Application Insights tooyour 응용 프로그램을 개발 하는 동안 추가한 경우 프로젝트에서 ApplicationInsights.config를 편집 하 고 다시 배포 tooyour 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="fb523-125">런타임에 상태 모니터 tooinstrument 웹 응용 프로그램을 사용 하는 경우 IIS에서 hello 응용 프로그램의 루트 디렉터리 hello에에서 ApplicationInsights.config를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="fb523-126">각 서버 인스턴스에서 해당 ApplicationInsights.config를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="fb523-127">Hello 성능 수집기 지시문을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="fb523-128">표준 카운터 및 사용자가 직접 구현한 카운터를 모두 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="fb523-129">`\Objects\Processes`는 모든 Windows 시스템에서 사용할 수 있는 표준 카운터의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="fb523-130">`\Sales(photo)\# Items Sold`는 웹 서비스에서 구현할 수 있는 사용자 지정 카운터의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="fb523-131">hello 형식은 `\Category(instance)\Counter"`, 인스턴스가 없는 범주에 대 한 바로 또는 `\Category\Counter`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="fb523-132">`ReportAs`일치 하지 않는 카운터 이름에 대 한 필요 `[a-zA-Z()/-_ \.]+` -hello 관계 집합에 없는 문자가 포함 되어, 즉: 편지, 대괄호, 슬래시, 하이픈, 밑줄, 공간, 둥근 점입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="fb523-133">인스턴스를 지정 하면 차원 "CounterInstanceName" hello의 메트릭을 보고 수집 될지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="fb523-134">코드에서 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="fb523-134">Collecting performance counters in code</span></span>
<span data-ttu-id="fb523-135">toocollect 시스템 성능 카운터 및 tooApplication Insights 보내거나, 아래 hello 조각 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="fb523-136">작업을 수행할 수 있습니다 또는 동일한 작업을 만든 사용자 지정 메트릭 hello:</span><span class="sxs-lookup"><span data-stu-id="fb523-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="fb523-137">분석에서의 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="fb523-137">Performance counters in Analytics</span></span>
<span data-ttu-id="fb523-138">[분석](app-insights-analytics.md)에서 성능 카운터 보고서를 검색하고 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="fb523-139">hello **performanceCounters** 스키마는 hello 노출 `category`, `counter` 이름 및 `instance` 각 성능 카운터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="fb523-140">각 응용 프로그램에 대 한 hello 원격 분석에서 해당 응용 프로그램에 대 한 hello 카운터에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="fb523-141">예를 들어 toosee 어떤 카운터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-141">For example, toosee what counters are available:</span></span> 

![Application Insights 분석의 성능 카운터](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="fb523-143">(Toohello 성능 카운터 인스턴스는 여기 '인스턴스', 역할이 나 서버 컴퓨터 인스턴스를 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="fb523-144">hello 성능 카운터 인스턴스 이름은 일반적으로 분할 하 프로세서 시간 비율 등 카운터 hello 프로세스 또는 응용 프로그램의 hello 이름별 합니다.)</span><span class="sxs-lookup"><span data-stu-id="fb523-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="fb523-145">tooget hello 최근 기간을 통해 사용 가능한 메모리의 차트:</span><span class="sxs-lookup"><span data-stu-id="fb523-145">tooget a chart of available memory over hello recent period:</span></span> 

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="fb523-147">마찬가지로 다른 원격 분석 **performanceCounters** 열도 `cloud_RoleInstance` hello 호스트 서버 인스턴스가 실행 되는 앱의 hello id를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="fb523-148">예를 들어 toocompare hello 응용 프로그램의 성능을 hello 서로 다른 컴퓨터에서:</span><span class="sxs-lookup"><span data-stu-id="fb523-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="fb523-150">ASP.NET 및 Application Insights 개수</span><span class="sxs-lookup"><span data-stu-id="fb523-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="fb523-151">*Hello 예외 속도 예외 메트릭 hello 차이 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="fb523-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="fb523-152">*예외 속도* 는 시스템 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="fb523-153">hello CLR 모든 처리 하는 hello와 처리 되지 않은 예외를 throw 되 고 샘플링 간격의 hello 간격의 길이 hello hello 총 나눕니다를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="fb523-154">Application Insights SDK hello이이 결과 수집 하 고 toohello 포털 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="fb523-155">*예외* hello 개수 TrackException 보고서 hello 차트의 hello 샘플링 간격의 hello 포털에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="fb523-156">Hello TrackException 코드에서 호출 하 고 모든 포함 되지 않으면을 작성 하 한 예외 처리에 포함 [처리 되지 않은 예외](app-insights-asp-net-exceptions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="fb523-157">경고</span><span class="sxs-lookup"><span data-stu-id="fb523-157">Alerts</span></span>
<span data-ttu-id="fb523-158">수 다른 메트릭과 마찬가지로 [경고를 설정](app-insights-alerts.md) toowarn 성능 카운터 제한 외부 라인 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="fb523-159">Hello 경고 블레이드를 열고 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb523-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="fb523-160"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb523-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="fb523-161">종속성 추적</span><span class="sxs-lookup"><span data-stu-id="fb523-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="fb523-162">예외 추적</span><span class="sxs-lookup"><span data-stu-id="fb523-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

