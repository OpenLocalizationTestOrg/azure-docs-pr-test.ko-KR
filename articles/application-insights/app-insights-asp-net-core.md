---
title: "ASP.NET Core용 Azure Application Insights | Microsoft Docs"
description: "응용 프로그램의 가용성, 성능 및 사용 현황을 모니터링합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="06e37-103">ASP.NET Core용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="06e37-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="06e37-104">[Application Insights](app-insights-overview.md)를 사용하여 웹 응용 프로그램의 가용성, 성능 및 사용량을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="06e37-105">앱의 성능 및 효과에 대한 생생한 피드백을 통해 충분한 정보를 바탕으로 각 개발 수명 주기의 디자인 방향을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![예](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="06e37-107">[Microsoft Azure](http://azure.com)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="06e37-108">Microsoft 계정으로 로그인합니다. Windows, XBox Live 또는 기타 Microsoft 클라우드 서비스의 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="06e37-109">팀에서 Azure를 단체 구독할 수도 있습니다. 소유자에게 Microsoft 계정을 사용하여 추가해 달라고 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="06e37-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="06e37-110">시작</span><span class="sxs-lookup"><span data-stu-id="06e37-110">Getting started</span></span>

* <span data-ttu-id="06e37-111">Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights 구성** 또는 **추가 > Application Insights**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="06e37-112">[자세히 알아봅니다](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="06e37-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="06e37-113">이러한 메뉴 명령이 보이지 않으면 [수동 시작 가이드](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="06e37-114">Visual Studio 2017 이전 버전을 사용하여 프로젝트를 만든 경우 이 작업을 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="06e37-115">Application Insights 사용</span><span class="sxs-lookup"><span data-stu-id="06e37-115">Using Application Insights</span></span>
<span data-ttu-id="06e37-116">[Microsoft Azure Portal](https://portal.azure.com)에 로그인하고, **모든 리소스** 또는 **Application Insights**를 선택하고, 만든 리소스를 선택하여 앱을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="06e37-117">별도의 브라우저 창에서 잠시 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="06e37-118">Application Insights 차트에 데이터가 표시되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="06e37-119">(새로 고침을 클릭해야 할 수 있습니다.) 개발하는 동안은 소량의 데이터만 표시되지만, 앱을 게시하고 많은 사용자가 확보되면 차트가 흥미로워집니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="06e37-120">개요 페이지에는 서버 응답 시간, 페이지 로드 시간, 실패한 요청의 수 등 핵심 성능 차트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="06e37-121">차트와 데이터를 더 보려면 아무 차트나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="06e37-122">포털의 보기는 다음 세 가지 주요 범주로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="06e37-123">[메트릭 탐색기](app-insights-metrics-explorer.md)에는 응답 시간, 실패율 또는 사용자가 [API](app-insights-api-custom-events-metrics.md)로 만든 메트릭 및 개수의 테이블과 그래프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="06e37-124">속성 값에 따라 데이터를 필터링하고 분할하여 앱 및 사용자에 대한 이해를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="06e37-125">[검색 탐색기](app-insights-diagnostic-search.md)에는 특정 요청, 예외, 로그 추적 또는 [API](app-insights-api-custom-events-metrics.md)로 만든 이벤트와 같은 개별적인 이벤트가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="06e37-126">이벤트를 필터링하고 검색하여 관련된 이벤트를 탐색하여 문제를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="06e37-127">[분석](app-insights-analytics.md) 은 원격 분석에 대해 SQL 유사 쿼리를 실행할 수 있도록 하는 강력한 분석 및 진단 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="06e37-128">경고</span><span class="sxs-lookup"><span data-stu-id="06e37-128">Alerts</span></span>
* <span data-ttu-id="06e37-129">실패율 및 기타 메트릭의 비정상적인 변경 내용을 알려 주는 [사전 진단 경고](app-insights-proactive-diagnostics.md)를 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="06e37-130">전 세계에서 지속적으로 웹 사이트를 테스트하고 테스트가 실패하면 즉시 전자 메일을 받으려면 [가용성 테스트](app-insights-monitor-web-app-availability.md) 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="06e37-131">응답 시간 또는 예외 속도 같은 메트릭이 허용 한도를 벗어나는지 파악하려면 [메트릭 경고](app-insights-monitor-web-app-availability.md) 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="06e37-132">비디오</span><span class="sxs-lookup"><span data-stu-id="06e37-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="06e37-133">공개 소스</span><span class="sxs-lookup"><span data-stu-id="06e37-133">Open source</span></span>
[<span data-ttu-id="06e37-134">코드를 읽고 참여하기</span><span class="sxs-lookup"><span data-stu-id="06e37-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="06e37-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06e37-135">Next steps</span></span>
* <span data-ttu-id="06e37-136">[웹 페이지에 원격 분석을 추가](app-insights-javascript.md) 하여 페이지 사용 현황 및 성능을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="06e37-137">[종속성을 모니터링](app-insights-asp-net-dependencies.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="06e37-138">[API를 사용](app-insights-api-custom-events-metrics.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="06e37-139">[가용성 테스트](app-insights-monitor-web-app-availability.md) 는 사용자의 앱을 전 세계에서 지속적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06e37-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

