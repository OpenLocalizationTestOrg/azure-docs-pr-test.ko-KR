---
title: "Azure Application Insights란? | Microsoft Docs"
description: "라이브 웹 응용 프로그램의 응용 프로그램 성능을 관리하고 사용 현황을 추적합니다.  문제를 감지, 심사, 진단하고 사람들이 앱을 사용하는 방식을 이해합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: 4b863f7421488a76aab60729286b48b65055d8f4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-application-insights"></a><span data-ttu-id="c75d9-105">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="c75d9-105">What is Application Insights?</span></span>
<span data-ttu-id="c75d9-106">Application Insights는 여러 플랫폼의 웹 개발자를 위한 확장 가능한 APM(응용 프로그램 성능 관리) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-106">Application Insights is an extensible Application Performance Management (APM) service for web developers on multiple platforms.</span></span> <span data-ttu-id="c75d9-107">이를 사용하여 라이브 웹 응용 프로그램을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-107">Use it to monitor your live web application.</span></span> <span data-ttu-id="c75d9-108">성능 이상을 자동으로 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-108">It will automatically detect performance anomalies.</span></span> <span data-ttu-id="c75d9-109">사용자가 문제를 진단하고 앱을 사용하여 실제로 수행할 작업을 이해할 수 있도록 돕는 강력한 분석 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-109">It includes powerful analytics tools to help you diagnose issues and to understand what users actually do with your app.</span></span>  <span data-ttu-id="c75d9-110">성능 및 가용성을 지속적으로 향상시킬 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-110">It's designed to help you continuously improve  performance and usability.</span></span> <span data-ttu-id="c75d9-111">.NET, Node.js 및 J2EE, 호스팅된 온-프레미스 또는 클라우드의 다양한 플랫폼에서 앱과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-111">It works for apps on a wide variety of platforms including .NET, Node.js and J2EE, hosted on-premises or in the cloud.</span></span> <span data-ttu-id="c75d9-112">DevOps 프로세스와 통합되며, 다양한 개발 도구와의 연결 지점을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-112">It  integrates with your devOps process, and has connection points to a variety of development tools.</span></span>

![사용자 활동 통계, 차트 또는 특정 이벤트를 드릴합니다.](./media/app-insights-overview/00-sample.png)

<span data-ttu-id="c75d9-114">[소개 애니메이션을 살펴보겠습니다](https://www.youtube.com/watch?v=fX2NtGrh-Y0).</span><span class="sxs-lookup"><span data-stu-id="c75d9-114">[Take a look at the intro animation](https://www.youtube.com/watch?v=fX2NtGrh-Y0).</span></span>

## <a name="how-does-application-insights-work"></a><span data-ttu-id="c75d9-115">Application Insights의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="c75d9-115">How does Application Insights work?</span></span>
<span data-ttu-id="c75d9-116">응용 프로그램에 작은 계측 패키지를 설치하고 Microsoft Azure 포털에서 Application Insights 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-116">You install a small instrumentation package in your application, and set up an Application Insights resource in the Microsoft Azure portal.</span></span> <span data-ttu-id="c75d9-117">이 계측 기능이 앱을 모니터링하여 포털에 원격 분석 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-117">The instrumentation monitors your app and sends telemetry data to the portal.</span></span> <span data-ttu-id="c75d9-118">응용 프로그램을 어디서나 실행할 수 있습니다. Azure에 호스트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-118">(The application can run anywhere - it doesn't have to be hosted in Azure.)</span></span>

<span data-ttu-id="c75d9-119">웹 서비스 응용 프로그램뿐 아니라 모든 백그라운드 구성 요소와 웹 페이지 자체의 JavaScript까지 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-119">You can instrument not only the web service application, but also any background components, and the JavaScript in the web pages themselves.</span></span> 

![앱의 Application Insights 계측 기능은 Application Insights 리소스로 원격 분석을 보냅니다.](./media/app-insights-overview/01-scheme.png)


<span data-ttu-id="c75d9-121">뿐만 아니라 호스트 환경에서 성능 카운터, Azure 진단, Docker 로그 등의 원격 분석을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-121">In addition, you can pull in telemetry from the host environments such as performance counters, Azure diagnostics, or Docker logs.</span></span> <span data-ttu-id="c75d9-122">웹 서비스에 주기적으로 가상 요청을 보내는 웹 테스트를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-122">You can also set up web tests that periodically send synthetic requests to your web service.</span></span>

<span data-ttu-id="c75d9-123">이러한 원격 분석 스트림은 강력한 분석 및 검색 도구를 원시 데이터에 적용할 수 있는 Azure Portal에 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-123">All these telemetry streams are integrated in the Azure portal, where you can apply powerful analytic and search tools to the raw data.</span></span>


### <a name="whats-the-overhead"></a><span data-ttu-id="c75d9-124">오버헤드는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c75d9-124">What's the overhead?</span></span>
<span data-ttu-id="c75d9-125">앱 성능에 미치는 영향을 매우 작습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-125">The impact on your app's performance is very small.</span></span> <span data-ttu-id="c75d9-126">추적 호출은 차단되지 않으며, 별도의 스레드로 일괄 처리 및 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-126">Tracking calls are non-blocking, and are batched and sent in a separate thread.</span></span>

## <a name="what-does-application-insights-monitor"></a><span data-ttu-id="c75d9-127">Application Insights는 무엇을 모니터링하나요?</span><span class="sxs-lookup"><span data-stu-id="c75d9-127">What does Application Insights monitor?</span></span>

<span data-ttu-id="c75d9-128">Application Insights는 응용 프로그램 팀에서 앱의 작동 방식과 사용 방식을 이해하는 데 도움을 주기 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-128">Application Insights is aimed at the development team, to help you understand how your app is performing and how it's being used.</span></span> <span data-ttu-id="c75d9-129">다음 사항을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-129">It monitors:</span></span>

* <span data-ttu-id="c75d9-130">**요청 속도, 응답 시간 및 실패율** - 하루 중 어느 시간에 어떤 페이지를 가장 많이 방문하는지, 사용자가 어디에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-130">**Request rates, response times, and failure rates** - Find out which pages are most popular, at what times of day, and where your users are.</span></span> <span data-ttu-id="c75d9-131">어떤 페이지가 가장 성능이 우수한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-131">See which pages perform best.</span></span> <span data-ttu-id="c75d9-132">요청이 더 있는데 응답 시간과 실패율이 높아지면 아마도 리소스 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-132">If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.</span></span> 
* <span data-ttu-id="c75d9-133">**종속성 비율, 응답 시간 및 실패율** - 외부 서비스 때문에 속도가 느려지는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-133">**Dependency rates, response times, and failure rates** - Find out whether external services are slowing you down.</span></span>
* <span data-ttu-id="c75d9-134">**예외** - 집계 통계를 분석하거나 특정 인스턴스를 선택하여 스택 추적 및 관련 요청을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-134">**Exceptions** - Analyse the aggregated statistics, or pick specific instances and drill into the stack trace and related requests.</span></span> <span data-ttu-id="c75d9-135">서버 및 브라우저 예외가 전부 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-135">Both server and browser exceptions are reported.</span></span>
* <span data-ttu-id="c75d9-136">**페이지 보기 및 로드 성능** - 사용자의 브라우저에서 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-136">**Page views and load performance** - reported by your users' browsers.</span></span>
* <span data-ttu-id="c75d9-137">웹 페이지의 **AJAX 호출** - 속도, 응답 시간 및 실패율.</span><span class="sxs-lookup"><span data-stu-id="c75d9-137">**AJAX calls** from web pages - rates, response times, and failure rates.</span></span>
* <span data-ttu-id="c75d9-138">**사용자 및 세션 수**.</span><span class="sxs-lookup"><span data-stu-id="c75d9-138">**User and session counts**.</span></span>
* <span data-ttu-id="c75d9-139">Windows 또는 Linux 서버 컴퓨터의 **성능 카운터** - CPU, 메모리, 네트워크 사용량 등.</span><span class="sxs-lookup"><span data-stu-id="c75d9-139">**Performance counters** from your Windows or Linux server machines, such as CPU, memory, and network usage.</span></span> 
* <span data-ttu-id="c75d9-140">Docker 또는 Azure의 **호스트 진단**.</span><span class="sxs-lookup"><span data-stu-id="c75d9-140">**Host diagnostics** from Docker or Azure.</span></span> 
* <span data-ttu-id="c75d9-141">앱의 **진단 추적 로그** - 추적 이벤트를 요청과 상호 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-141">**Diagnostic trace logs** from your app - so that you can correlate trace events with requests.</span></span>
* <span data-ttu-id="c75d9-142">판매된 품목, 승리한 게임 등의 비즈니스 이벤트를 추적하기 위해 개발자가 직접 클라이언트 또는 서버 코드로 작성하는 **사용자 지정 이벤트 및 메트릭**.</span><span class="sxs-lookup"><span data-stu-id="c75d9-142">**Custom events and metrics** that you write yourself in the client or server code, to track business events such as items sold or games won.</span></span>

## <a name="where-do-i-see-my-telemetry"></a><span data-ttu-id="c75d9-143">원격 분석은 어디서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c75d9-143">Where do I see my telemetry?</span></span>

<span data-ttu-id="c75d9-144">다양한 방법으로 데이터를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-144">There are plenty of ways to explore your data.</span></span> <span data-ttu-id="c75d9-145">다음 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d9-145">Check out these articles:</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="c75d9-146">**스마트 검색 및 수동 경고**</span><span class="sxs-lookup"><span data-stu-id="c75d9-146">**Smart detection and manual alerts**</span></span>](app-insights-proactive-diagnostics.md)<br/><span data-ttu-id="c75d9-147">자동 경고는 앱의 일반적인 원격 분석 패턴에 맞게 조정되고, 일반적인 패턴을 벗어나는 항목이 있으면 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-147">Automatic alerts adapt to your app's normal patterns of telemetry and trigger when there's something outside the usual pattern.</span></span> <span data-ttu-id="c75d9-148">특정 수준의 사용자 지정 또는 표준 메트릭에 대해 [경고를 설정](app-insights-alerts.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-148">You can also [set alerts](app-insights-alerts.md) on particular levels of custom or standard metrics.</span></span> |![경고 샘플](./media/app-insights-overview/alerts-tn.png) |
| [<span data-ttu-id="c75d9-150">**응용 프로그램 맵**</span><span class="sxs-lookup"><span data-stu-id="c75d9-150">**Application map**</span></span>](app-insights-app-map.md)<br/><span data-ttu-id="c75d9-151">주요 메트릭 및 경고가 포함된 앱의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-151">The components of your app, with key metrics and alerts.</span></span> |![응용 프로그램 맵](./media/app-insights-overview/appmap-tn.png)  |
| [<span data-ttu-id="c75d9-153">**프로파일러**</span><span class="sxs-lookup"><span data-stu-id="c75d9-153">**Profiler**</span></span>](app-insights-profiler.md)<br/><span data-ttu-id="c75d9-154">샘플링된 요청의 실행 프로필을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-154">Inspect the execution profiles of sampled requests.</span></span> |![프로파일러](./media/app-insights-overview/profiler.png) |
| [<span data-ttu-id="c75d9-156">**사용 현황 분석**</span><span class="sxs-lookup"><span data-stu-id="c75d9-156">**Usage analysis**</span></span>](app-insights-usage-overview.md)<br/><span data-ttu-id="c75d9-157">사용자 구분 및 재방문 주기를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-157">Analyze user segmentation and retention.</span></span>|![재방문 주기 도구](./media/app-insights-overview/retention.png) |
| [<span data-ttu-id="c75d9-159">**인스턴스 데이터에 대한 진단 검색**</span><span class="sxs-lookup"><span data-stu-id="c75d9-159">**Diagnostic search for instance data**</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="c75d9-160">요청, 예외, 종속성 호출, 로그 추적 및 페이지 보기와 같은 이벤트를 검색하고 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-160">Search and filter events such as requests, exceptions, dependency calls, log traces, and page views.</span></span>  |![원격 분석 검색](./media/app-insights-overview/search-tn.png) |
| [<span data-ttu-id="c75d9-162">**집계된 데이터에 대한 메트릭 탐색기**</span><span class="sxs-lookup"><span data-stu-id="c75d9-162">**Metrics Explorer for aggregated data**</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="c75d9-163">요청, 오류 및 예외의 비율과 응답 시간, 페이지 로드 시간과 같은 집계된 데이터를 탐색, 필터링 및 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-163">Explore, filter, and segment aggregated data such as rates of requests, failures, and exceptions; response times, page load times.</span></span> |![메트릭](./media/app-insights-overview/metrics-tn.png) |
| [<span data-ttu-id="c75d9-165">**대시보드**</span><span class="sxs-lookup"><span data-stu-id="c75d9-165">**Dashboards**</span></span>](app-insights-dashboards.md#dashboards)<br/><span data-ttu-id="c75d9-166">여러 리소스의 데이터를 매시업한 후 다른 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-166">Mash up data from multiple resources and share with others.</span></span> <span data-ttu-id="c75d9-167">다중 구성 요소 응용 프로그램에서 사용하거나 단체방에 연속으로 표시하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-167">Great for multi-component applications, and for continuous display in the team room.</span></span> |![대시보드 샘플](./media/app-insights-overview/dashboard-tn.png) |
| [<span data-ttu-id="c75d9-169">**라이브 메트릭 스트림**</span><span class="sxs-lookup"><span data-stu-id="c75d9-169">**Live Metrics Stream**</span></span>](app-insights-live-stream.md)<br/><span data-ttu-id="c75d9-170">새 빌드를 배포할 때 이러한 실시간에 가까운 성능 표시기를 확인하여 모든 항목이 예상대로 작동하는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-170">When you deploy a new build, watch these near-real-time performance indicators to make sure everything works as expected.</span></span> |![라이브 메트릭 샘플](./media/app-insights-overview/live-metrics-tn.png) |
| [<span data-ttu-id="c75d9-172">**분석**</span><span class="sxs-lookup"><span data-stu-id="c75d9-172">**Analytics**</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="c75d9-173">이 강력한 쿼리 언어를 사용하여 앱의 성능 및 사용 현황에 대한 까다로운 질문에 답변할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-173">Answer tough questions about your app's performance and usage by using this powerful query language.</span></span> |![분석 샘플](./media/app-insights-overview/analytics-tn.png) |
| [<span data-ttu-id="c75d9-175">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="c75d9-175">**Visual Studio**</span></span>](app-insights-visual-studio.md)<br/><span data-ttu-id="c75d9-176">코드의 성능 데이터를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d9-176">See performance data in the code.</span></span> <span data-ttu-id="c75d9-177">스택 추적의 코드로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d9-177">Go to code from stack traces.</span></span>|![Visual studio](./media/app-insights-overview/visual-studio-tn.png) |
| [<span data-ttu-id="c75d9-179">**스냅숏 디버거**</span><span class="sxs-lookup"><span data-stu-id="c75d9-179">**Snapshot debugger**</span></span>](app-insights-snapshot-debugger.md)<br/><span data-ttu-id="c75d9-180">실시간 작업에서 샘플링된 스냅숏을 매개 변수 값으로 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-180">Debug snapshots sampled from live operations, with parameter values.</span></span>|![Visual studio](./media/app-insights-overview/snapshot.png) |
| [<span data-ttu-id="c75d9-182">**Power BI**</span><span class="sxs-lookup"><span data-stu-id="c75d9-182">**Power BI**</span></span>](app-insights-export-power-bi.md)<br/><span data-ttu-id="c75d9-183">사용 현황 메트릭을 다른 비즈니스 인텔리전스와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-183">Integrate usage metrics with other business intelligence.</span></span>| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [<span data-ttu-id="c75d9-185">**REST API**</span><span class="sxs-lookup"><span data-stu-id="c75d9-185">**REST API**</span></span>](https://dev.applicationinsights.io/)<br/><span data-ttu-id="c75d9-186">메트릭 및 원시 데이터에 대한 쿼리를 실행하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-186">Write code to run queries over your metrics and raw data.</span></span>| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [<span data-ttu-id="c75d9-188">**연속 내보내기**</span><span class="sxs-lookup"><span data-stu-id="c75d9-188">**Continuous export**</span></span>](app-insights-export-telemetry.md)<br/><span data-ttu-id="c75d9-189">원시 데이터가 도착하는 즉시 저장소에 대량으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-189">Bulk export of raw data to storage as soon as it arrives.</span></span> |![내보내기](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a><span data-ttu-id="c75d9-191">Application Insights를 어떻게 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="c75d9-191">How do I use Application Insights?</span></span>

### <a name="monitor"></a><span data-ttu-id="c75d9-192">모니터</span><span class="sxs-lookup"><span data-stu-id="c75d9-192">Monitor</span></span>
<span data-ttu-id="c75d9-193">앱에 Application Insights를 설치하고, [가용성 웹 테스트를 설정](app-insights-monitor-web-app-availability.md)하고, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-193">Install Application Insights in your app, set up [availability web tests](app-insights-monitor-web-app-availability.md), and:</span></span>

* <span data-ttu-id="c75d9-194">종속성, 페이지 로드 및 AJAX 호출의 부하, 응답성 및 성능을 모니터링하기 위한 팀 공간용 [대시보드](app-insights-dashboards.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-194">Set up a [dashboard](app-insights-dashboards.md) for your team room to keep an eye on load, responsiveness, and the performance of your dependencies, page loads, and AJAX calls.</span></span>
* <span data-ttu-id="c75d9-195">가장 느리고 대부분 실패한 요청을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-195">Discover which are the slowest and most failing requests.</span></span>
* <span data-ttu-id="c75d9-196">새 릴리스를 배포할 때 [라이브 스트림](app-insights-live-stream.md)을 보고 성능 저하를 즉시 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-196">Watch [Live Stream](app-insights-live-stream.md) when you deploy a new release, to know immediately about any degradation.</span></span>

### <a name="detect-diagnose"></a><span data-ttu-id="c75d9-197">감지, 진단</span><span class="sxs-lookup"><span data-stu-id="c75d9-197">Detect, Diagnose</span></span>
<span data-ttu-id="c75d9-198">경고를 수신하거나 문제를 검색한 경우:</span><span class="sxs-lookup"><span data-stu-id="c75d9-198">When you receive an alert or discover a problem:</span></span>

* <span data-ttu-id="c75d9-199">얼마나 많은 사용자가 영향을 받는지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-199">Assess how many users are affected.</span></span>
* <span data-ttu-id="c75d9-200">오류는 예외, 종속성 호출 및 추적과 연관이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-200">Correlate failures with exceptions, dependency calls and traces.</span></span>
* <span data-ttu-id="c75d9-201">프로파일러, 스냅숏, 스택 덤프 및 추적 로그를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-201">Examine profiler, snapshots, stack dumps, and trace logs.</span></span>

### <a name="build-measure-learn"></a><span data-ttu-id="c75d9-202">빌드, 측정, 학습</span><span class="sxs-lookup"><span data-stu-id="c75d9-202">Build, Measure, Learn</span></span>
<span data-ttu-id="c75d9-203">배포하는 새로운 각 기능의 [효율성을 측정](app-insights-usage-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-203">[Measure the effectiveness](app-insights-usage-overview.md) of each new feature that you deploy.</span></span>

* <span data-ttu-id="c75d9-204">고객이 새 UX 또는 비즈니스 기능을 사용하는 방식을 측정하도록 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-204">Plan to measure how customers use new UX or business features.</span></span>
* <span data-ttu-id="c75d9-205">코드에 사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-205">Write custom telemetry into your code.</span></span>
* <span data-ttu-id="c75d9-206">원격 분석에서 얻은 구체적인 증거를 기반으로 다음 개발 주기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-206">Base the next development cycle on hard evidence from your telemetry.</span></span>

## <a name="get-started"></a><span data-ttu-id="c75d9-207">시작</span><span class="sxs-lookup"><span data-stu-id="c75d9-207">Get started</span></span>
<span data-ttu-id="c75d9-208">Application Insights는 Microsoft Azure에서 호스트되는 다양한 서비스 중 하나이며, 원격 분석이 분석 및 프레젠테이션을 위해 이 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-208">Application Insights is one of the many services hosted within Microsoft Azure, and telemetry is sent there for analysis and presentation.</span></span> <span data-ttu-id="c75d9-209">따라서 다른 작업을 수행하기 전에 [Microsoft Azure](http://azure.com)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-209">So before you do anything else, you'll need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="c75d9-210">등록은 무료이며 Application Insights에 대해 기본 [가격 책정 계획](https://azure.microsoft.com/pricing/details/application-insights/)을 선택하는 경우 응용 프로그램 사용량이 특정 크기로 커질 때까지 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-210">It's free to sign up, and if you choose the basic [pricing plan](https://azure.microsoft.com/pricing/details/application-insights/) of Application Insights, there's no charge until your application has grown to have substantial usage.</span></span> <span data-ttu-id="c75d9-211">조직에 이미 구독이 있으면 해당 구독에 Microsoft 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-211">If your organization already has a subscription, they could add your Microsoft account to it.</span></span>

<span data-ttu-id="c75d9-212">시작하는 데는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-212">There are several ways to get started.</span></span> <span data-ttu-id="c75d9-213">본인에게 적합한 방법으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-213">Begin with whichever works best for you.</span></span> <span data-ttu-id="c75d9-214">나중에 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-214">You can add the others later.</span></span>

* <span data-ttu-id="c75d9-215">**런타임: 서버에서 웹앱을 계측합니다.**</span><span class="sxs-lookup"><span data-stu-id="c75d9-215">**At run time: instrument your web app on the server.**</span></span> <span data-ttu-id="c75d9-216">코드에 대한 업데이트를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-216">Avoids any update to the code.</span></span> <span data-ttu-id="c75d9-217">서버에 대한 관리자 액세스 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-217">You need admin access to your server.</span></span>
  * [<span data-ttu-id="c75d9-218">**IIS 온-프레미스 또는 VM**</span><span class="sxs-lookup"><span data-stu-id="c75d9-218">**IIS on-premises or on a VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="c75d9-219">**Azure 웹앱 또는 VM**</span><span class="sxs-lookup"><span data-stu-id="c75d9-219">**Azure web app or VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="c75d9-220">**J2EE**</span><span class="sxs-lookup"><span data-stu-id="c75d9-220">**J2EE**</span></span>](app-insights-java-live.md)
* <span data-ttu-id="c75d9-221">**개발 타임: 코드에 Application Insights를 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="c75d9-221">**At development time: add Application Insights to your code.**</span></span> <span data-ttu-id="c75d9-222">사용자 지정 원격 분석을 작성하고 백 엔드 및 데스크톱 앱을 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-222">Allows you to write custom telemetry and to instrument back-end and desktop apps.</span></span>
  * <span data-ttu-id="c75d9-223">[Visual Studio](app-insights-asp-net.md) 2013 업데이트 2 이상</span><span class="sxs-lookup"><span data-stu-id="c75d9-223">[Visual Studio](app-insights-asp-net.md) 2013 update 2 or later.</span></span>
  * <span data-ttu-id="c75d9-224">[Eclipse](app-insights-java-eclipse.md)의 Java 또는 [기타 도구](app-insights-java-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c75d9-224">Java in [Eclipse](app-insights-java-eclipse.md) or [other tools](app-insights-java-get-started.md)</span></span>
  * [<span data-ttu-id="c75d9-225">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c75d9-225">Node.js</span></span>](app-insights-nodejs.md)
  * [<span data-ttu-id="c75d9-226">기타 플랫폼</span><span class="sxs-lookup"><span data-stu-id="c75d9-226">Other platforms</span></span>](app-insights-platforms.md)
* <span data-ttu-id="c75d9-227">페이지 보기, AJAX 및 기타 클라이언트 쪽 원격 분석에 대해 **[웹 페이지를 계측](app-insights-javascript.md)**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-227">**[Instrument your web pages](app-insights-javascript.md)** for page view, AJAX and other client-side telemetry.</span></span>
* <span data-ttu-id="c75d9-228">**[가용성 테스트](app-insights-monitor-web-app-availability.md)** -서버에서 정기적으로 웹 사이트를 ping합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d9-228">**[Availability tests](app-insights-monitor-web-app-availability.md)** - ping your website regularly from our servers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c75d9-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c75d9-229">Next steps</span></span>
<span data-ttu-id="c75d9-230">다음을 사용하여 런타임에 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d9-230">Get started at runtime with:</span></span>

* [<span data-ttu-id="c75d9-231">IIS 서버</span><span class="sxs-lookup"><span data-stu-id="c75d9-231">IIS server</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="c75d9-232">J2EE 서버</span><span class="sxs-lookup"><span data-stu-id="c75d9-232">J2EE server</span></span>](app-insights-java-live.md)

<span data-ttu-id="c75d9-233">다음을 사용하여 개발 시에 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d9-233">Get started at development time with:</span></span>

* [<span data-ttu-id="c75d9-234">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c75d9-234">ASP.NET</span></span>](app-insights-asp-net.md)
* [<span data-ttu-id="c75d9-235">Java</span><span class="sxs-lookup"><span data-stu-id="c75d9-235">Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="c75d9-236">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c75d9-236">Node.js</span></span>](app-insights-nodejs.md)

## <a name="support-and-feedback"></a><span data-ttu-id="c75d9-237">지원 및 피드백</span><span class="sxs-lookup"><span data-stu-id="c75d9-237">Support and feedback</span></span>
* <span data-ttu-id="c75d9-238">질문 및 문제:</span><span class="sxs-lookup"><span data-stu-id="c75d9-238">Questions and Issues:</span></span>
  * <span data-ttu-id="c75d9-239">[문제 해결][qna]</span><span class="sxs-lookup"><span data-stu-id="c75d9-239">[Troubleshooting][qna]</span></span>
  * [<span data-ttu-id="c75d9-240">MSDN 포럼</span><span class="sxs-lookup"><span data-stu-id="c75d9-240">MSDN Forum</span></span>](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [<span data-ttu-id="c75d9-241">StackOverflow</span><span class="sxs-lookup"><span data-stu-id="c75d9-241">StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)
* <span data-ttu-id="c75d9-242">사용자 제안:</span><span class="sxs-lookup"><span data-stu-id="c75d9-242">Your suggestions:</span></span>
  * [<span data-ttu-id="c75d9-243">UserVoice</span><span class="sxs-lookup"><span data-stu-id="c75d9-243">UserVoice</span></span>](https://visualstudio.uservoice.com/forums/357324)
* <span data-ttu-id="c75d9-244">블로그:</span><span class="sxs-lookup"><span data-stu-id="c75d9-244">Blog:</span></span>
  * [<span data-ttu-id="c75d9-245">Application Insights 블로그</span><span class="sxs-lookup"><span data-stu-id="c75d9-245">Application Insights blog</span></span>](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a><span data-ttu-id="c75d9-246">비디오</span><span class="sxs-lookup"><span data-stu-id="c75d9-246">Videos</span></span>

<span data-ttu-id="c75d9-247">[![애니메이션 소개](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span><span class="sxs-lookup"><span data-stu-id="c75d9-247">[![Animated introduction](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
