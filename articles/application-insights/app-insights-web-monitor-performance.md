---
title: "Application Insights로 앱 상태 및 사용 현황 모니터링"
description: "Application Insights를 시작합니다. 온-프레미스 또는 Microsoft Azure 웹 응용 프로그램의 사용량, 가용성 및 성능을 분석합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="3115d-104">웹 응용 프로그램의 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="3115d-104">Monitor performance in web applications</span></span>


<span data-ttu-id="3115d-105">응용 프로그램이 정상적으로 작동하는지 확인하고 오류가 발생하는지 신속하게 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="3115d-106">[Application Insights][start]는 성능 문제 및 예외에 대한 정보와, 이러한 현상에 대한 근본 원인을 확인하고 진단하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="3115d-107">Application Insights에서 Java 및 ASP.NET 웹 응용 프로그램과 서비스, WCF 서비스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="3115d-108">온-프레미스, 가상 컴퓨터에서 또는 Microsoft Azure 웹 사이트로 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="3115d-109">Application Insights는 클라이언트쪽에서 iOS, Android 및 Windows 스토어 앱을 포함하여 다양한 장치 및 웹 페이지에서 원격 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="3115d-110">웹 응용 프로그램에서 느리게 작동하는 페이지 찾기에 사용할 수 있는 새 환경을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="3115d-111">액세스 권한이 없는 경우 [미리 보기 블레이드](app-insights-previews.md)로 미리 보기 옵션을 구성하여 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="3115d-112">[대화형 성능 조사를 사용하여 성능 병목 현상 찾기 및 해결](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation)에서 이 새로운 환경에 대해 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="3115d-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="3115d-113"><a name="setup"></a>성능 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="3115d-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="3115d-114">Application Insights를 아직 프로젝트에 추가하지 않은 경우(프로젝트에 ApplicationInsights.config가 없음) 다음 방법 중 하나를 선택하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="3115d-115">ASP.NET 웹 앱</span><span class="sxs-lookup"><span data-stu-id="3115d-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="3115d-116">예외 모니터링 추가</span><span class="sxs-lookup"><span data-stu-id="3115d-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="3115d-117">종속성 모니터링 추가</span><span class="sxs-lookup"><span data-stu-id="3115d-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="3115d-118">J2EE 웹앱</span><span class="sxs-lookup"><span data-stu-id="3115d-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="3115d-119">종속성 모니터링 추가</span><span class="sxs-lookup"><span data-stu-id="3115d-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="3115d-120"><a name="view"></a>성능 메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="3115d-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="3115d-121">[Azure 포털](https://portal.azure.com)에서 응용 프로그램에 대해 설정한 Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="3115d-122">개요 블레이드에 기본 성능 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="3115d-123">무엇이든 클릭하면 추가 세부 정보와 장기간에 걸친 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="3115d-124">예를 들어 요청 타일을 클릭하고 시간 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-124">For example, click the Requests tile and then select a time range:</span></span>

![클릭하여 추가 데이터를 표시한 다음 시간 범위 선택](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="3115d-126">차트를 클릭하여 표시되는 메트릭을 선택하거나 새 차트를 추가하고 해당 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![그래프를 클릭하여 메트릭 선택](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="3115d-128">**모든 메트릭의 선택을 취소합니다** .</span><span class="sxs-lookup"><span data-stu-id="3115d-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="3115d-129">메트릭은 그룹으로 구분되며 그룹 내의 모든 멤버를 선택하면 해당 그룹의 다른 멤버만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="3115d-130"><a name="metrics"></a>성능 메트릭의 의미</span><span class="sxs-lookup"><span data-stu-id="3115d-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="3115d-131">성능 타일 및 보고서</span><span class="sxs-lookup"><span data-stu-id="3115d-131">Performance tiles and reports</span></span>
<span data-ttu-id="3115d-132">다양한 성능 메트릭을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="3115d-133">먼저 응용 프로그램 블레이드에 기본적으로 표시되는 메트릭부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="3115d-134">요청</span><span class="sxs-lookup"><span data-stu-id="3115d-134">Requests</span></span>
<span data-ttu-id="3115d-135">지정한 기간에 수신된 HTTP 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="3115d-136">이 메트릭을 다른 보고서의 결과와 비교하여 로드의 변화에 따른 앱의 동작 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="3115d-137">HTTP 요청에는 페이지, 데이터 및 이미지에 대한 모든 GET 또는 POST 요청이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="3115d-138">특정 URL에 대한 요청 수를 가져오려면 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="3115d-139">평균 응답 시간</span><span class="sxs-lookup"><span data-stu-id="3115d-139">Average response time</span></span>
<span data-ttu-id="3115d-140">웹 요청이 응용 프로그램에 도착하는 시점과 응답이 반환되는 시점 사이의 시간을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="3115d-141">점은 이동 평균을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-141">The points show a moving average.</span></span> <span data-ttu-id="3115d-142">요청 수가 많으면 그래프에서는 요청 수가 크게 늘어나거나 줄어들지 않아도 일부 점이 평균에서 벗어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="3115d-143">요청 수의 비정상적인 증가를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-143">Look for unusual peaks.</span></span> <span data-ttu-id="3115d-144">일반적으로는 요청 수가 증가하면 응답 시간은 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="3115d-145">그러나 이처럼 요청 수와 응답 시간이 비례하지 않는 경우에는 앱이 사용하는 서비스의 용량 또는 CPU와 같은 리소스 제한에 도달해서 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="3115d-146">특정 URL에 대한 요청 시간을 가져오려면 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="3115d-147">가장 느린 요청</span><span class="sxs-lookup"><span data-stu-id="3115d-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="3115d-148">성능 튜닝이 필요할 수 있는 요청을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="3115d-149">실패한 요청</span><span class="sxs-lookup"><span data-stu-id="3115d-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="3115d-150">catch되지 않은 예외를 throw한 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="3115d-151">타일을 클릭하면 특정 오류의 세부 정보를 확인할 수 있으며 개별 요청을 선택하면 해당 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="3115d-152">오류의 대표 샘플만 개별적으로 조사할 수 있도록 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="3115d-153">기타 메트릭</span><span class="sxs-lookup"><span data-stu-id="3115d-153">Other metrics</span></span>
<span data-ttu-id="3115d-154">표시할 수 있는 기타 메트릭을 보려면 그래프를 클릭하고 모든 메트릭의 선택을 취소하여 사용 가능한 전체 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="3115d-155">(i)를 클릭하면 각 메트릭의 정의가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-155">Click (i) to see each metric's definition.</span></span>

![모든 메트릭의 선택을 취소하여 전체 집합 표시](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="3115d-157">메트릭을 선택하면 같은 차트에 표시할 수 없는 다른 메트릭은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="3115d-158">경고 설정</span><span class="sxs-lookup"><span data-stu-id="3115d-158">Set alerts</span></span>
<span data-ttu-id="3115d-159">메트릭의 비정상적인 값에 대한 알림을 메일로 받으려면 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="3115d-160">계정 관리자나 특정 메일 주소로 메일을 보내도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="3115d-161">다른 속성에 앞서 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-161">Set the resource before the other properties.</span></span> <span data-ttu-id="3115d-162">성능 또는 사용 메트릭에 대한 경고를 설정하려면 webtest 리소스를 선택하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3115d-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="3115d-163">임계값을 입력하라는 단위에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="3115d-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="3115d-164">*경고 추가 단추가 보이지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="3115d-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="3115d-165">-이것은 읽기 전용 액세스 권한이 있는 그룹 계정입니까?</span><span class="sxs-lookup"><span data-stu-id="3115d-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="3115d-166">계정 관리자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3115d-166">Check with the account administrator.</span></span>

## <span data-ttu-id="3115d-167"><a name="diagnosis"></a>문제 진단</span><span class="sxs-lookup"><span data-stu-id="3115d-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="3115d-168">아래에는 성능 문제를 찾고 진단하기 위한 몇 가지 팁이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="3115d-169">웹 사이트의 작동이 중단되거나 응답이 잘못되거나 속도가 느려지는 경우 경고를 받도록 [웹 테스트][availability]를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="3115d-170">요청 수를 다른 메트릭과 비교하여 오류 또는 느린 응답이 부하와 관련되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="3115d-171">코드에서 [검사 추적 문을 삽입 및 검색][diagnostic]하여 문제를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="3115d-172">[라이브 메트릭 스트림][livestream]을 사용하여 작업에서 웹앱을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="3115d-173">[스냅숏 디버거][snapshot]를 사용하여 .Net 응용 프로그램의 상태를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="3115d-174">대화형 성능 조사를 사용하여 성능 병목 현상 찾기 및 해결</span><span class="sxs-lookup"><span data-stu-id="3115d-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="3115d-175">새 Application Insights 대화형 성능 조사를 사용하여 전반적인 성능이 저하되는 웹앱의 영역을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="3115d-176">저하되는 특정 페이지를 신속하게 찾을 수 있으며 이러한 페이지 간의 상관 관계를 확인하기 위해 [프로파일링 도구](app-insights-profiler.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="3115d-177">느리게 작동하는 페이지 목록 만들기</span><span class="sxs-lookup"><span data-stu-id="3115d-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="3115d-178">성능 문제를 찾기 위한 첫 번째 단계는 느린 응답 페이지의 목록을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="3115d-179">아래 스크린샷은 성능 블레이드를 사용하여 추가 조사를 위해 잠재적인 페이지의 목록을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="3115d-180">이 페이지에서 약 오후 6시와 약 오후 10시에 다시 앱의 응답 시간에 저하가 있었음을 신속하게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="3115d-181">또한 고객/세부 정보 가져오기 작업에 507.05밀리초의 중앙 응답 시간으로 일부 장기 실행 작업이 있었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Application Insights 대화형 성능](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="3115d-183">특정 페이지에 대해 드릴다운</span><span class="sxs-lookup"><span data-stu-id="3115d-183">Drill down on specific pages</span></span>

<span data-ttu-id="3115d-184">앱의 성능에 대한 스냅숏을 만든 후 느리게 작동하는 특정 작업에 대한 자세한 세부 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="3115d-185">아래와 같이 세부 정보를 보려면 목록에서 모든 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="3115d-186">차트에서 성능이 종속성을 기반으로 했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="3115d-187">또한 다양한 응답 시간을 경험한 사용자 수를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-187">You can also see how many users experienced the various response times.</span></span> 

![Application insights 작업 블레이드](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="3115d-189">특정 기간에 대해 드릴다운</span><span class="sxs-lookup"><span data-stu-id="3115d-189">Drill down on a specific time period</span></span>

<span data-ttu-id="3115d-190">조사할 특정 시점을 식별한 후 성능 저하를 발생시켰을 수도 있는 특정 작업을 살펴보도록 더 자세히 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="3115d-191">특정 시점을 클릭할 때 다음과 같은 페이지의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="3115d-192">아래 예제에서 서버 응답 코드 및 작업 기간과 함께 지정된 기간에 대해 나열된 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="3115d-193">또한 이 정보를 개발 팀에 전송해야 하는 경우 TFS 작업 항목을 열기 위한 url이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Application Insights 시간 조각](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="3115d-195">특정 작업에 대해 드릴다운</span><span class="sxs-lookup"><span data-stu-id="3115d-195">Drill down on a specific operation</span></span>

<span data-ttu-id="3115d-196">조사할 특정 시점을 식별한 후 성능 저하를 발생시켰을 수도 있는 특정 작업을 살펴보도록 더 자세히 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="3115d-197">아래와 같이 작업의 세부 정보를 보려면 목록에서 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="3115d-198">이 예제에서 작업이 실패하고 Application Insights에서 응용 프로그램에서 throw했던 예외의 세부 정보를 제공한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="3115d-199">다시, 이 블레이드에서 TFS 작업 항목을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application insights 작업 블레이드](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="3115d-201"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="3115d-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="3115d-202">[웹 테스트][availability] - 전 세계에서 웹 요청이 일정한 간격으로 응용 프로그램에 전송되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="3115d-203">[진단 추적 캡처 및 검색][diagnostic] - 추적 호출을 삽입하고 결과를 확인하여 문제를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="3115d-204">[사용 현황 추적][usage] - 사용자의 응용 프로그램 사용 방식을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="3115d-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="3115d-205">[문제 해결][qna] - 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="3115d-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



