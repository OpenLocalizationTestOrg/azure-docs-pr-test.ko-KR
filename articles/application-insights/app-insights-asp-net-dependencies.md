---
title: "Azure Application Insights의 종속성 추적 | Microsoft Docs"
description: "Application Insights를 사용하여 온-프레미스 또는 Microsoft Azure 웹 응용 프로그램의 사용량, 가용성 및 성능을 분석합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="b0bce-103">Application Insights 설정: 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="b0bce-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="b0bce-104">*종속성*은 앱에서 호출하는 외부 구성 요소로,</span><span class="sxs-lookup"><span data-stu-id="b0bce-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="b0bce-105">일반적으로 HTTP, 데이터베이스 또는 파일 시스템을 사용하여 호출되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="b0bce-106">[Application Insights](app-insights-overview.md)는 응용 프로그램이 종속성을 기다리는 시간과 종속성 호출에 실패하는 빈도를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="b0bce-107">특정 호출을 조사하여 요청 및 예외와 연관지을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![예제 차트](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="b0bce-109">기본적으로 종속성 모니터는 현재 다음 유형의 종속성에 대한 호출을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="b0bce-110">서버</span><span class="sxs-lookup"><span data-stu-id="b0bce-110">Server</span></span>
  * <span data-ttu-id="b0bce-111">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="b0bce-111">SQL databases</span></span>
  * <span data-ttu-id="b0bce-112">ASP.NET 웹 및 HTTP 기반 바인딩을 사용하는 WCF 서비스</span><span class="sxs-lookup"><span data-stu-id="b0bce-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="b0bce-113">로컬 또는 원격 HTTP 호출</span><span class="sxs-lookup"><span data-stu-id="b0bce-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="b0bce-114">Azure Cosmos DB, 테이블, Blob Storage 및 큐</span><span class="sxs-lookup"><span data-stu-id="b0bce-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="b0bce-115">웹 페이지</span><span class="sxs-lookup"><span data-stu-id="b0bce-115">Web pages</span></span>
  * <span data-ttu-id="b0bce-116">AJAX 호출</span><span class="sxs-lookup"><span data-stu-id="b0bce-116">AJAX calls</span></span>

<span data-ttu-id="b0bce-117">모니터링은 선택한 방법과 관련된 [바이트 코드 계측](https://msdn.microsoft.com/library/z9z62c29.aspx)을 사용하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="b0bce-118">성능 오버 헤드가 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="b0bce-119">[TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)를 사용하여 클라이언트 및 서버 코드 모두에서 다른 종속성을 모니터링하는 사용자 고유의 SDK 호출을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="b0bce-120">종속성 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="b0bce-120">Set up dependency monitoring</span></span>
<span data-ttu-id="b0bce-121">부분 종속성 정보는 [Application Insights SDK](app-insights-asp-net.md)에서 자동으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="b0bce-122">전체 데이터를 가져오려면 호스트 서버에 대한 적절한 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="b0bce-123">플랫폼</span><span class="sxs-lookup"><span data-stu-id="b0bce-123">Platform</span></span> | <span data-ttu-id="b0bce-124">설치</span><span class="sxs-lookup"><span data-stu-id="b0bce-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="b0bce-125">IIS 서버</span><span class="sxs-lookup"><span data-stu-id="b0bce-125">IIS Server</span></span> |<span data-ttu-id="b0bce-126">[상태 모니터를 서버에 설치](app-insights-monitor-performance-live-website-now.md) 또는 [응용 프로그램을 .NET Framework 4.6 이상으로 업그레이드](http://go.microsoft.com/fwlink/?LinkId=528259)하고 앱에 [Application Insights SDK](app-insights-asp-net.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="b0bce-127">Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="b0bce-127">Azure Web App</span></span> |<span data-ttu-id="b0bce-128">웹앱 제어판에서 [Application Insights 블레이드를 열고](app-insights-azure-web-apps.md) 메시지가 표시되면 설치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="b0bce-129">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="b0bce-129">Azure Cloud Service</span></span> |<span data-ttu-id="b0bce-130">[시작 작업 사용](app-insights-cloudservices.md) 또는 [.NET Framework 4.6+ 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="b0bce-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="b0bce-131">종속성 데이터를 찾을 수 있는 위치</span><span class="sxs-lookup"><span data-stu-id="b0bce-131">Where to find dependency data</span></span>
* <span data-ttu-id="b0bce-132">[응용 프로그램 맵](#application-map): 앱과 인접 구성 요소 간의 종속성을 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="b0bce-133">[성능, 브라우저 및 실패 블레이드](#performance-and-blades): 서버 종속성 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="b0bce-134">[브라우저 블레이드](#ajax-calls): 사용자 브라우저에서의 AJAX 호출을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="b0bce-135">[느리거나 실패한 요청 클릭](#diagnose-slow-requests): 해당 종속성 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="b0bce-136">[분석](#analytics): 종속성 데이터를 쿼리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="b0bce-137">응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="b0bce-137">Application Map</span></span>
<span data-ttu-id="b0bce-138">응용 프로그램 맵은 응용 프로그램의 구성 요소 간에 종속성을 검색하는 시각화 보조 도구의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="b0bce-139">앱의 원격 분석에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="b0bce-140">이 예제에서는 두 외부 서비스에 대한 브라우저 스크립트에서의 AJAX 호출과 서버 앱에서의 REST 호출을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![응용 프로그램 맵](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="b0bce-142">**상자에서 관련 종속성 및 기타 차트로 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="b0bce-143">[대시보드](app-insights-dashboards.md)에 **맵을 고정**하면 완벽하게 작동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="b0bce-144">[자세히 알아보세요](app-insights-app-map.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b0bce-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="b0bce-145">성능 및 실패 블레이드</span><span class="sxs-lookup"><span data-stu-id="b0bce-145">Performance and failure blades</span></span>
<span data-ttu-id="b0bce-146">성능 블레이드에는 서버 앱에 실행한 종속성 호출 기간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="b0bce-147">호출별로 구분된 요약 차트와 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-147">There's a summary chart and a table segmented by call.</span></span>

![성능 블레이드 종속성 차트](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="b0bce-149">요약 차트 또는 테이블 항목을 클릭하여 이러한 호출의 원시 발생을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![종속성 호출 인스턴스](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="b0bce-151">**실패 횟수**는 **실패** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="b0bce-152">실패는 200~399 범위에 없거나 알 수 없는 반환 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="b0bce-153">**100% 실패?**</span><span class="sxs-lookup"><span data-stu-id="b0bce-153">**100% failures?**</span></span> <span data-ttu-id="b0bce-154">- 이는 부분 종속성 데이터만 가져옴을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="b0bce-155">[플랫폼에 적절한 종속성 모니터링을 설정](#set-up-dependency-monitoring)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="b0bce-156">AJAX 호출</span><span class="sxs-lookup"><span data-stu-id="b0bce-156">AJAX Calls</span></span>
<span data-ttu-id="b0bce-157">브라우저 블레이드에는 [웹 페이지의 JavaScript](app-insights-javascript.md)에서 실행한 AJAX 호출의 기간 및 실패율이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="b0bce-158">이는 종속성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="b0bce-159"><a name="diagnosis"></a> 느린 요청 진단</span><span class="sxs-lookup"><span data-stu-id="b0bce-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="b0bce-160">각 요청 이벤트는 종속성 호출, 예외 및 기타 앱에서 요청을 처리하는 동안 추적된 이벤트와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="b0bce-161">따라서 일부 요청이 잘못 수행되는 경우 종속성의 느린 응답 때문인지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="b0bce-162">이에 대한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="b0bce-163">요청에서 종속성까지 추적</span><span class="sxs-lookup"><span data-stu-id="b0bce-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="b0bce-164">성능 블레이드를 열고 요청 표를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-164">Open the Performance blade, and look at the grid of requests:</span></span>

![평균 및 개수가 포함된 요청 목록](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="b0bce-166">맨 위의 요청은 시간이 아주 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-166">The top one is taking very long.</span></span> <span data-ttu-id="b0bce-167">시간이 어디에 소비되는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="b0bce-168">개별 요청 이벤트를 보려면 해당 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-168">Click that row to see individual request events:</span></span>

![요청 항목 목록](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="b0bce-170">장기 실행 인스턴스를 클릭하여 세부 사항을 조사합니다. 이 요청과 관련된 원격 종속성 호출까지 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![원격 종속성에 대한 호출 찾기, 특별한 기간 식별](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="b0bce-172">이 요청을 서비스하는 데 걸린 시간은 대부분 로컬 서비스 호출에 소요된 시간인 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="b0bce-173">해당 행을 선택하여 자세한 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-173">Select that row to get more information:</span></span>

![해당 원격 종속성을 클릭하여 원인 식별](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="b0bce-175">여기에 문제가 있는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="b0bce-176">문제를 확인했으므로 이제 호출에 시간이 오래 걸리는 이유를 확인하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="b0bce-177">요청 시간 표시 막대</span><span class="sxs-lookup"><span data-stu-id="b0bce-177">Request timeline</span></span>
<span data-ttu-id="b0bce-178">다른 경우에는 특별히 긴 종속성 호출이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="b0bce-179">그러나 시간 표시 막대 뷰로 전환하면 내부 처리에 지연이 발생하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![원격 종속성에 대한 호출 찾기, 특별한 기간 식별](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="b0bce-181">첫 번째 종속성 호출 후 큰 간격이 있어 보이므로 코드를 보고 그 이유를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="b0bce-182">라이브 사이트 프로파일링</span><span class="sxs-lookup"><span data-stu-id="b0bce-182">Profile your live site</span></span>

<span data-ttu-id="b0bce-183">시간에 따른 위치를 알 수 없나요?</span><span class="sxs-lookup"><span data-stu-id="b0bce-183">No idea where the time goes?</span></span> <span data-ttu-id="b0bce-184">[Application Insights 프로파일러](app-insights-profiler.md)는 라이브 사이트에 대한 HTTP 호출을 추적하고 가장 오래 걸린 코드의 함수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="b0bce-185">실패한 요청</span><span class="sxs-lookup"><span data-stu-id="b0bce-185">Failed requests</span></span>
<span data-ttu-id="b0bce-186">실패한 요청은 종속성에 대한 실패한 호출과 연관이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="b0bce-187">문제를 클릭하여 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-187">Again, we can click through to track down the problem.</span></span>

![실패한 요청 차트 클릭](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="b0bce-189">실패한 요청 발생을 클릭하고 연관된 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![요청 유형을 클릭하고, 인스턴스를 클릭하여 동일한 인스턴스의 다른 보기로 이동하고, 클릭하여 예외 세부 정보를 표시합니다.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="b0bce-191">분석</span><span class="sxs-lookup"><span data-stu-id="b0bce-191">Analytics</span></span>
<span data-ttu-id="b0bce-192">[Log Analytics 쿼리 언어](https://docs.loganalytics.io/)에서 종속성을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="b0bce-193">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-193">Here are some examples.</span></span>

* <span data-ttu-id="b0bce-194">실패한 종속성 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="b0bce-195">AJAX 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="b0bce-196">요청과 연관된 종속성 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="b0bce-197">페이지 보기와 관련된 AJAX 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="b0bce-198">사용자 지정 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="b0bce-198">Custom dependency tracking</span></span>
<span data-ttu-id="b0bce-199">표준 종속성 추적 모듈은 데이터베이스 및 REST API와 같은 외부 종속성을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="b0bce-200">하지만 일부 추가 구성 요소를 동일한 방식으로 취급할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="b0bce-201">표준 모듈에 의해 사용되는 동일한 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) 를 사용하여 종속성 정보를 보내는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="b0bce-202">예를 들면, 사용자가 직접 작성하지 않은 어셈블리 코드를 작성하는 경우, 응답 시간 기여도를 알아보기 위해 모든 호출의 시간을 잴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="b0bce-203">Application Insights에서 종속성 차트에 표시되는 이 데이터를 가지려면, `TrackDependency`을 사용하여 이것을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="b0bce-204">표준 종속성 추적 모듈을 해제하려는 경우, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 DependencyTrackingTelemetryModule에 대한 참조를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b0bce-205">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b0bce-205">Troubleshooting</span></span>
<span data-ttu-id="b0bce-206">*종속성 성공 플래그는 항상 true 또는 false로 표시됩니다.*</span><span class="sxs-lookup"><span data-stu-id="b0bce-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="b0bce-207">*SQL 쿼리가 일부만 표시됩니다.*</span><span class="sxs-lookup"><span data-stu-id="b0bce-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="b0bce-208">최신 버전의 SDK로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="b0bce-209">.NET 버전이 4.6 미만인 경우:</span><span class="sxs-lookup"><span data-stu-id="b0bce-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="b0bce-210">IIS 호스트: 호스트 서버에 [Application Insights 에이전트](app-insights-monitor-performance-live-website-now.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="b0bce-211">Azure 웹앱: 웹앱 제어판에서 Application Insights 탭을 열고 Application Insights를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b0bce-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="b0bce-212">비디오</span><span class="sxs-lookup"><span data-stu-id="b0bce-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b0bce-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0bce-213">Next steps</span></span>
* [<span data-ttu-id="b0bce-214">예외</span><span class="sxs-lookup"><span data-stu-id="b0bce-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="b0bce-215">사용자 및 페이지 데이터</span><span class="sxs-lookup"><span data-stu-id="b0bce-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="b0bce-216">Availability</span><span class="sxs-lookup"><span data-stu-id="b0bce-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
