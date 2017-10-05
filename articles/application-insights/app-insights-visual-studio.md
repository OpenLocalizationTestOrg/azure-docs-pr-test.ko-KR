---
title: "Visual Studio에서 Azure Application Insights로 응용 프로그램 디버그 | Microsoft Docs"
description: "디버깅 및 프로덕션 중에 웹앱 성능 분석 및 진단입니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="a7e8d-103">Visual Studio에서 Azure Application Insights로 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="a7e8d-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="a7e8d-104">Visual Studio(2015 이상)에서 [Azure Application Insights](app-insights-overview.md)의 원격 분석을 사용하여 디버깅 및 프로덕션의 성능을 분석하고 ASP.NET 웹앱의 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="a7e8d-105">Visual Studio 2017 이상을 사용하여 ASP.NET 웹앱을 만든 경우 이미 Application Insights SDK가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="a7e8d-106">그렇지 않은 경우 아직 수행하지 않았다면 [앱에 Application Insights를 추가합니다](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a7e8d-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="a7e8d-107">앱이 라이브 프로덕션 상태인 경우 모니터링하려면 일반적으로 [Azure Portal](https://portal.azure.com)에서 Application Insights 원격 분석을 봅니다. 여기서 경고를 설정하고 강력한 모니터링 도구를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="a7e8d-108">그러나 디버깅하려면 Visual Studio에서 원격 분석 데이터를 검색하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="a7e8d-109">Visual Studio를 사용하여 개발 컴퓨터에서 프로덕션 사이트 및 디버깅 실행의 원격 분석을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="a7e8d-110">후자의 경우 Azure Portal에 원격 분석을 보내도록 SDK를 아직 구성하지 않더라도 디버깅 실행을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="a7e8d-111"><a name="run"></a> 프로젝트 디버깅</span><span class="sxs-lookup"><span data-stu-id="a7e8d-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="a7e8d-112">F5 키를 사용하여 로컬 디버그 모드로 웹앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="a7e8d-113">다른 페이지를 열어서 일부 원격 분석을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="a7e8d-114">Visual Studio에서 프로젝트의 Application Insights 모듈에 의해 기록된 이벤트의 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![Visual Studio에서 Application Insights 단추는 디버깅하는 동안 표시됩니다.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="a7e8d-116">원격 분석을 검색하려면 이 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="a7e8d-117">Application Insights 검색</span><span class="sxs-lookup"><span data-stu-id="a7e8d-117">Application Insights search</span></span>
<span data-ttu-id="a7e8d-118">Application Insights 검색 창에서는 기록된 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="a7e8d-119">(Azure에 로그인한 경우 Application Insights를 설정할 때 Azure Portal에서 동일한 이벤트를 검색할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a7e8d-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 및 검색을 선택합니다.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="a7e8d-121">필터를 선택하거나 선택을 취소한 후에 텍스트 검색 필드의 끝에 있는 검색 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="a7e8d-122">자유 텍스트 검색은 이벤트의 필드에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="a7e8d-123">예를 들어 페이지의 URL의 일부 또는 클라이언트 시티와 같은 속성의 값 또는 추적 로그에서 특정 단어를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="a7e8d-124">이벤트를 클릭하여 자세한 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="a7e8d-125">웹앱에 대한 요청의 경우 코드를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-125">For requests to your web app, you can click through to the code.</span></span>

![요청 세부 정보 아래에서 코드를 클릭합니다.](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="a7e8d-127">또한 관련된 항목 탭을 열어 실패한 요청 또는 예외를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![요청 세부 정보에서 관련된 항목까지 아래로 스크롤합니다.](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="a7e8d-129">예외 및 실패한 요청 보기</span><span class="sxs-lookup"><span data-stu-id="a7e8d-129">View exceptions and failed requests</span></span>
<span data-ttu-id="a7e8d-130">검색 창에서 예외 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="a7e8d-131">(일부 ASP.NET 응용 프로그램의 이전 유형에서는 [예외 모니터링을 설정](app-insights-asp-net-exceptions.md)하여 프레임워크에 의해 처리되는 예외를 볼 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a7e8d-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="a7e8d-132">예외를 클릭하여 스택 추적을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="a7e8d-133">앱의 코드가 Visual Studio에서 열린 경우 스택 추적에서 코드의 관련된 줄까지 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![예외 스택 추적](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="a7e8d-135">코드의 요청 및 예외 요약 보기</span><span class="sxs-lookup"><span data-stu-id="a7e8d-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="a7e8d-136">각 처리기 메서드 위의 코드 렌즈 줄에서는 지난 24시간 동안 Application Insights에 의해 기록된 요청 및 예외 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![예외 스택 추적](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="a7e8d-138">[Application Insights 포털에 원격 분석을 전송하도록 앱을 구성](app-insights-asp-net.md)한 경우 코드 렌즈에서는 Application Insights 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="a7e8d-139">코드 렌즈의 Application Insights에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a7e8d-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="a7e8d-140">추세</span><span class="sxs-lookup"><span data-stu-id="a7e8d-140">Trends</span></span>
<span data-ttu-id="a7e8d-141">추세는 시간이 지남에 따라 앱의 동작 방식을 시각화하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="a7e8d-142">Application Insights 도구 모음 단추 또는 Application Insights 검색 창에서 **원격 분석 추세 탐색** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="a7e8d-143">시작하려면 일반적인 5개의 쿼리 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="a7e8d-144">원격 분석 유형, 시간 범위 및 기타 속성에 따라 서로 다른 데이터 집합을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="a7e8d-145">데이터에서 잘못된 부분을 찾으려면 "유형 보기" 드롭다운에서 비정상 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="a7e8d-146">창의 아래쪽에서 필터링 옵션을 사용하면 쉽게 원격 분석의 특정 하위 집합을 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![추세](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="a7e8d-148">[추세 자세히 알아보기](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="a7e8d-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="a7e8d-149">로컬 모니터링</span><span class="sxs-lookup"><span data-stu-id="a7e8d-149">Local monitoring</span></span>
<span data-ttu-id="a7e8d-150">(Visual Studio 2015 업데이트 2에서) Application Insights 포털에 원격 분석을 보내도록 SDK를 구성하지 않은 경우(따라서 ApplicationInsights.config에 계측 키가 없음) 최신 디버깅 세션의 원격 분석이 진단 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="a7e8d-151">이전 버전의 앱을 이미 게시한 경우에 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="a7e8d-152">게시된 앱의 Application Insights 포털에서 원격 분석과 디버깅 세션의 원격 분석을 혼합하려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="a7e8d-153">포털에 원격 분석을 보내기 전에 디버깅하려는 [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md) 이 있는 경우에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="a7e8d-154">*우선 Application Insights를 완전히 구성하여 포털에 원격 분석을 전송했습니다. 하지만 이제 Visual Studio에서만 원격 분석을 확인하려 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a7e8d-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="a7e8d-155">검색 창 설정에서 앱이 포털에 원격 분석을 전송하는 경우 로컬 진단을 검색하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="a7e8d-156">포털에 전송되는 원격 분석을 중지하려면 ApplicationInsights.config에서 `<instrumentationkey>...` 줄을 주석으로 처리합니다. 원격 분석을 포털에 다시 보낼 준비가 되면 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7e8d-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7e8d-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="a7e8d-158">**[더 많은 데이터 추가](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="a7e8d-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="a7e8d-159">사용량, 가용성, 종속성, 예외를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="a7e8d-160">로깅 프레임 워크의 추적을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="a7e8d-161">사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-161">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="a7e8d-163">**[Application Insights 포털 사용](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="a7e8d-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="a7e8d-164">대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 내보낸 원격 분석 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7e8d-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual studio](./media/app-insights-visual-studio/62.png) |

