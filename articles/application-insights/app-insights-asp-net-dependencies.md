---
title: "aaaDependency Azure Application Insights에서 추적 | Microsoft Docs"
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="ee399-103">Application Insights 설정: 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="ee399-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="ee399-104">*종속성*은 앱에서 호출하는 외부 구성 요소로,</span><span class="sxs-lookup"><span data-stu-id="ee399-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="ee399-105">일반적으로 HTTP, 데이터베이스 또는 파일 시스템을 사용하여 호출되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="ee399-106">[Application Insights](app-insights-overview.md)는 응용 프로그램이 종속성을 기다리는 시간과 종속성 호출에 실패하는 빈도를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="ee399-107">특정 호출을 조사할 수 있으며 toorequests는 예외와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![예제 차트](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="ee399-109">hello의 기본 종속성 모니터는 현재 호출 toothese 종류의 종속성을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="ee399-110">서버</span><span class="sxs-lookup"><span data-stu-id="ee399-110">Server</span></span>
  * <span data-ttu-id="ee399-111">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="ee399-111">SQL databases</span></span>
  * <span data-ttu-id="ee399-112">ASP.NET 웹 및 HTTP 기반 바인딩을 사용하는 WCF 서비스</span><span class="sxs-lookup"><span data-stu-id="ee399-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="ee399-113">로컬 또는 원격 HTTP 호출</span><span class="sxs-lookup"><span data-stu-id="ee399-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="ee399-114">Azure Cosmos DB, 테이블, Blob Storage 및 큐</span><span class="sxs-lookup"><span data-stu-id="ee399-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="ee399-115">웹 페이지</span><span class="sxs-lookup"><span data-stu-id="ee399-115">Web pages</span></span>
  * <span data-ttu-id="ee399-116">AJAX 호출</span><span class="sxs-lookup"><span data-stu-id="ee399-116">AJAX calls</span></span>

<span data-ttu-id="ee399-117">모니터링은 선택한 방법과 관련된 [바이트 코드 계측](https://msdn.microsoft.com/library/z9z62c29.aspx)을 사용하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="ee399-118">성능 오버 헤드가 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="ee399-119">사용자 고유의 SDK toomonitor 둘 다 hello 클라이언트와 서버 코드에서 다른 종속성을 사용 하 여 호출 hello를 작성할 수도 있습니다 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="ee399-120">종속성 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="ee399-120">Set up dependency monitoring</span></span>
<span data-ttu-id="ee399-121">Hello 하 여 부분 종속성 정보를 자동으로 수집 [Application Insights SDK](app-insights-asp-net.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="ee399-122">tooget 전체 데이터 hello hello 호스트 서버에 대 한 적절 한 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="ee399-123">플랫폼</span><span class="sxs-lookup"><span data-stu-id="ee399-123">Platform</span></span> | <span data-ttu-id="ee399-124">설치</span><span class="sxs-lookup"><span data-stu-id="ee399-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="ee399-125">IIS 서버</span><span class="sxs-lookup"><span data-stu-id="ee399-125">IIS Server</span></span> |<span data-ttu-id="ee399-126">어느 [상태 모니터 서버에 설치](app-insights-monitor-performance-live-website-now.md) 또는 [응용 프로그램 too.NET framework 4.6 이상 업그레이드](http://go.microsoft.com/fwlink/?LinkId=528259) hello를 설치 하 고 [Application Insights SDK](app-insights-asp-net.md) 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="ee399-127">Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="ee399-127">Azure Web App</span></span> |<span data-ttu-id="ee399-128">웹 응용 프로그램 제어 패널에서 [웹 응용 프로그램 제어판에서 Application Insights 블레이드 열기 hello](app-insights-azure-web-apps.md) 메시지가 표시 되 면 설치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="ee399-129">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="ee399-129">Azure Cloud Service</span></span> |<span data-ttu-id="ee399-130">[시작 작업 사용](app-insights-cloudservices.md) 또는 [.NET Framework 4.6+ 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="ee399-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="ee399-131">여기서 toofind 종속성 데이터</span><span class="sxs-lookup"><span data-stu-id="ee399-131">Where toofind dependency data</span></span>
* <span data-ttu-id="ee399-132">[응용 프로그램 맵](#application-map): 앱과 인접 구성 요소 간의 종속성을 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="ee399-133">[성능, 브라우저 및 실패 블레이드](#performance-and-blades): 서버 종속성 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="ee399-134">[브라우저 블레이드](#ajax-calls): 사용자 브라우저에서의 AJAX 호출을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="ee399-135">[클릭 하 여 느리거나 실패 한 요청에서](#diagnose-slow-requests) toocheck 해당 종속성 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="ee399-136">[분석](#analytics) 사용된 tooquery 종속성 데이터 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="ee399-137">응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="ee399-137">Application Map</span></span>
<span data-ttu-id="ee399-138">응용 프로그램 맵 hello 응용 프로그램 구성 요소 간의 시각 toodiscovering 종속성으로 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="ee399-139">응용 프로그램에서 hello 원격 분석에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="ee399-140">이 예제 응용 프로그램 tootwo 외부 서비스 hello 브라우저 스크립트에서 AJAX 호출 및 hello 서버에서 REST 호출 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![응용 프로그램 맵](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="ee399-142">**Hello 상자에서 이동할** toorelevant 종속성 및 기타 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="ee399-143">**Pin hello 지도** toohello [대시보드](app-insights-dashboards.md)여기서 완벽 하 게 작동 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="ee399-144">[자세히 알아봅니다](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="ee399-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="ee399-145">성능 및 실패 블레이드</span><span class="sxs-lookup"><span data-stu-id="ee399-145">Performance and failure blades</span></span>
<span data-ttu-id="ee399-146">hello 성능 블레이드 hello 서버 응용 프로그램에서 수행한 종속성 호출의 hello 기간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="ee399-147">호출별로 구분된 요약 차트와 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-147">There's a summary chart and a table segmented by call.</span></span>

![성능 블레이드 종속성 차트](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="ee399-149">요약 차트 hello 또는 hello 테이블 항목 toosearch 원시 횟수 이러한 호출을 통해 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![종속성 호출 인스턴스](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="ee399-151">**실패 수가** hello에 표시 되는 **오류** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="ee399-152">오류가는 hello 범위 200-399, 또는 알 수 없음에 있지 않은 모든 반환 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="ee399-153">**100% 실패?**</span><span class="sxs-lookup"><span data-stu-id="ee399-153">**100% failures?**</span></span> <span data-ttu-id="ee399-154">- 이는 부분 종속성 데이터만 가져옴을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="ee399-155">너무 필요한[모니터링 적절 한 tooyour 플랫폼 종속성 설정](#set-up-dependency-monitoring)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="ee399-156">AJAX 호출</span><span class="sxs-lookup"><span data-stu-id="ee399-156">AJAX Calls</span></span>
<span data-ttu-id="ee399-157">hello 브라우저 블레이드 hello 기간을 표시 및에서 호출에 AJAX의 실패율 [웹 페이지에서 JavaScript](app-insights-javascript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="ee399-158">이는 종속성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="ee399-159"><a name="diagnosis"></a> 느린 요청 진단</span><span class="sxs-lookup"><span data-stu-id="ee399-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="ee399-160">종속성 호출 hello와 연결 된 각 요청 이벤트, 예외 및 앱을 처리 하는 동안 추적 되는 다른 이벤트 hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="ee399-161">따라서 일부 요청이 잘못 수행 하는 경우에 종속성의 응답을 tooslow 때문 인지 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="ee399-162">이에 대한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="ee399-163">요청 toodependencies에서 추적</span><span class="sxs-lookup"><span data-stu-id="ee399-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="ee399-164">Hello 성능 블레이드를 열고 요청 hello 표를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![평균 및 개수가 포함된 요청 목록](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="ee399-166">hello 최상위 매우 오래 걸리면 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-166">hello top one is taking very long.</span></span> <span data-ttu-id="ee399-167">Hello 시간이 소요 된 위치 알 수 하는 경우를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="ee399-168">해당 행 toosee 개별 요청 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-168">Click that row toosee individual request events:</span></span>

![요청 항목 목록](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="ee399-170">또한 하 고 toohello 원격 종속성 호출 관련된 toothis 요청 아래로 스크롤하여 모든 장기 실행 인스턴스 tooinspect를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![호출 tooRemote 종속성 찾기, 비정상적인 기간을 식별 합니다.](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="ee399-172">대부분이이 요청 호출 tooa 로컬 서비스에 소요 된 시간의 hello 시간 서비스의 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="ee399-173">자세한 내용은 해당 행 tooget를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-173">Select that row tooget more information:</span></span>

![클릭 하 여 해당 원격 종속성 tooidentify hello 원인](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="ee399-175">이 hello 문제는 여기서 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="ee399-176">म hello 문제 원인을 해결 한, 방금 이제 이유 호출 하는 시간이 걸리거나 너무 오래 아웃 toofind 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="ee399-177">요청 시간 표시 막대</span><span class="sxs-lookup"><span data-stu-id="ee399-177">Request timeline</span></span>
<span data-ttu-id="ee399-178">다른 경우에는 특별히 긴 종속성 호출이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="ee399-179">하지만 toohello 타임 라인 보기를 전환 하 여 았습니다 hello 지연 내부 처리에서 발생 한 위치:</span><span class="sxs-lookup"><span data-stu-id="ee399-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![호출 tooRemote 종속성 찾기, 비정상적인 기간을 식별 합니다.](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="ee399-181">즉 이유 코드 toosee 우리의 표시 해야 하므로 hello 첫 번째 종속성 호출 이후의 toobe 큰 간격 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="ee399-182">라이브 사이트 프로파일링</span><span class="sxs-lookup"><span data-stu-id="ee399-182">Profile your live site</span></span>

<span data-ttu-id="ee399-183">어떠한 정보도 표시 hello 시간 흐름 방향은? hello [Application Insights 프로파일러](app-insights-profiler.md) tooyour 라이브 사이트를 호출 하 고 사용자 코드에서 함수를 표시 하는 HTTP 추적 hello 가장 긴 시간이 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="ee399-184">실패한 요청</span><span class="sxs-lookup"><span data-stu-id="ee399-184">Failed requests</span></span>
<span data-ttu-id="ee399-185">실패 한 요청 실패 한 호출 toodependencies와 연결 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="ee399-186">다시, tootrack hello 문제를 통해 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-186">Again, we can click through tootrack down hello problem.</span></span>

![Hello 실패 한 요청 차트를 클릭 합니다.](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="ee399-188">해당 연결 된 이벤트를 실패 한 요청 tooan 번째 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Hello 인스턴스 tooget tooa의 서로 다른 뷰를 요청 유형을 클릭 한 다음 동일한 인스턴스에 hello를 tooget 예외 세부 정보를 클릭 합니다.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="ee399-190">분석</span><span class="sxs-lookup"><span data-stu-id="ee399-190">Analytics</span></span>
<span data-ttu-id="ee399-191">Hello에서 종속성을 추적할 수 있습니다 [로그 분석 쿼리 언어](https://docs.loganalytics.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="ee399-192">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-192">Here are some examples.</span></span>

* <span data-ttu-id="ee399-193">실패한 종속성 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="ee399-194">AJAX 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="ee399-195">요청과 연관된 종속성 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="ee399-196">페이지 보기와 관련된 AJAX 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="ee399-197">사용자 지정 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="ee399-197">Custom dependency tracking</span></span>
<span data-ttu-id="ee399-198">hello 표준 종속성 추적 모듈은 데이터베이스 및 REST Api와 같은 외부 종속성이 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="ee399-199">그러나 몇 가지 추가 구성 요소 toobe에서에서 처리 하는 hello 동일한 경우가 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="ee399-200">종속성 정보를 보내는 코드를 작성할 수 동일 hello를 사용 하 여 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello 표준 모듈에 의해 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="ee399-201">예를 들어 코드 어셈블리와 사용자가 직접 작성 하지 않은, 모든 hello 호출 tooit 시간 수를 빌드하면 tooyour 응답은 어떤 기여 아웃 toofind 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="ee399-202">사용 하 여 toohave hello Application Insights 종속성 차트에 표시 된이 데이터 보내기 `TrackDependency`합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="ee399-203">Tooswitch hello 표준 종속성 추적 모듈 해제 하려는 경우 제거에 hello 참조 tooDependencyTrackingTelemetryModule [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ee399-204">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ee399-204">Troubleshooting</span></span>
<span data-ttu-id="ee399-205">*종속성 성공 플래그는 항상 true 또는 false로 표시됩니다.*</span><span class="sxs-lookup"><span data-stu-id="ee399-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="ee399-206">*SQL 쿼리가 일부만 표시됩니다.*</span><span class="sxs-lookup"><span data-stu-id="ee399-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="ee399-207">Toohello hello SDK의 최신 버전을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="ee399-208">.NET 버전이 4.6 미만인 경우:</span><span class="sxs-lookup"><span data-stu-id="ee399-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="ee399-209">IIS 호스트: 설치 [Application Insights 에이전트](app-insights-monitor-performance-live-website-now.md) hello 호스트 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="ee399-210">Azure 웹 앱: 열기 Application Insights hello 웹 응용 프로그램 제어 패널의 탭 및 Application Insights를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee399-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="ee399-211">비디오</span><span class="sxs-lookup"><span data-stu-id="ee399-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="ee399-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ee399-212">Next steps</span></span>
* [<span data-ttu-id="ee399-213">예외</span><span class="sxs-lookup"><span data-stu-id="ee399-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="ee399-214">사용자 및 페이지 데이터</span><span class="sxs-lookup"><span data-stu-id="ee399-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ee399-215">Availability</span><span class="sxs-lookup"><span data-stu-id="ee399-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
