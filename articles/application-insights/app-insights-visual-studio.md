---
title: "Visual Studio에서 Azure Application Insights를 사용한 응용 프로그램 aaaDebug | Microsoft Docs"
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
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="43d10-103">Visual Studio에서 Azure Application Insights로 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="43d10-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="43d10-104">Visual Studio(2015 이상)에서 [Azure Application Insights](app-insights-overview.md)의 원격 분석을 사용하여 디버깅 및 프로덕션의 성능을 분석하고 ASP.NET 웹앱의 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="43d10-105">Visual Studio 2017을 사용 하 여 ASP.NET 웹 앱 만들거나 나중 hello Application Insights SDK 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="43d10-106">아직 그렇게 하지 않은 경우 그렇지 [Application Insights tooyour 앱 추가](app-insights-asp-net.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="43d10-107">toomonitor 앱 라이브 프로덕션 환경에서 되었을 때 일반적으로 hello Application Insights 원격 분석에서에서 보면 hello [Azure 포털](https://portal.azure.com), 경고를 설정 하 고 수 있는 강력한 모니터링 도구의 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="43d10-108">하지만 디버깅을 위해 또한을 검색 하 고 Visual Studio에서 원격 분석 hello를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="43d10-109">프로덕션 사이트에서 한 개발 컴퓨터에서 실행 됨 디버깅에서 Visual Studio tooanalyze 원격 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="43d10-110">후자의 경우 hello에에서 hello SDK toosend 원격 분석 toohello Azure 포털을 아직 구성 하지 않은 경우에 디버깅 실행을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="43d10-111"><a name="run"></a> 프로젝트 디버깅</span><span class="sxs-lookup"><span data-stu-id="43d10-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="43d10-112">F5 키를 사용하여 로컬 디버그 모드로 웹앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="43d10-113">일부 원격 분석 toogenerate 서로 다른 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="43d10-114">Visual Studio 프로젝트에 Application Insights 모듈 hello에 의해 기록 된 hello 이벤트의 개수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![Visual Studio에서 디버깅 하는 동안 hello Application Insights 단추 표시 됩니다.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="43d10-116">이 단추 toosearch 원격 분석을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="43d10-117">Application Insights 검색</span><span class="sxs-lookup"><span data-stu-id="43d10-117">Application Insights search</span></span>
<span data-ttu-id="43d10-118">hello Application Insights 검색 창에 기록 된 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="43d10-119">(로그인 하면 tooAzure Application Insights를 설정 하는 경우 검색할 수 있습니다 hello Azure 포털의에서 동일한 이벤트 hello.)</span><span class="sxs-lookup"><span data-stu-id="43d10-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights 선택 검색](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="43d10-121">를 선택 하거나 필터를 선택 취소 한 후에 hello 텍스트 검색 필드의 hello 끝 hello 검색 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="43d10-122">hello 자유 텍스트 검색 hello 이벤트의 모든 필드에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="43d10-123">예를 들어; 페이지의 hello URL의 일부 검색 또는 클라이언트 city;와 같은 속성 값을 환영 합니다. 또는 추적 로그에 특정 단어입니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="43d10-124">모든 이벤트 toosee의 자세한 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="43d10-125">요청 tooyour 웹 앱에 대 한 toohello 코드를 통해 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-125">For requests tooyour web app, you can click through toohello code.</span></span>

![요청 세부 사항에서 toohello 코드를 통해 클릭](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="43d10-127">관련된 항목을 열 수도 있습니다 toohelp 실패 한 요청 또는 예외를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![요청 세부 사항에서 toorelated 항목 아래로 스크롤하십시오.](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="43d10-129">예외 및 실패한 요청 보기</span><span class="sxs-lookup"><span data-stu-id="43d10-129">View exceptions and failed requests</span></span>
<span data-ttu-id="43d10-130">Hello 검색 창에 예외 보고서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="43d10-131">(ASP.NET 응용 프로그램의 일부 이전 형식에서는 있는 너무[예외 모니터링 설정](app-insights-asp-net-exceptions.md) hello 프레임 워크에 의해 처리 되는 예외를 toosee.)</span><span class="sxs-lookup"><span data-stu-id="43d10-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="43d10-132">예외 tooget 스택 추적을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="43d10-133">Hello 코드 hello 앱의 Visual Studio에서 열려 있으면 hello 스택 추적 toohello 관련 코드 줄에서 hello 통해 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![예외 스택 추적](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="43d10-135">Hello 코드에서 요청 및 예외 요약 확인</span><span class="sxs-lookup"><span data-stu-id="43d10-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="43d10-136">코드 렌즈 윗줄 각 처리기 메서드 hello hello 요청 및 지난 24 시간 동안 hello에 Application Insights에 의해 기록 된 예외 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![예외 스택 추적](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="43d10-138">코드 렌즈 데이터를 보여 줍니다 Application Insights만 있으면 [응용 프로그램 원격 분석 toosend toohello Application Insights 포털 구성](app-insights-asp-net.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="43d10-139">코드 렌즈의 Application Insights에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="43d10-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="43d10-140">추세</span><span class="sxs-lookup"><span data-stu-id="43d10-140">Trends</span></span>
<span data-ttu-id="43d10-141">추세는 시간이 지남에 따라 앱의 동작 방식을 시각화하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="43d10-142">선택 **원격 분석 추세 탐색** hello Application Insights 도구 모음 단추 또는 Application Insights 검색 창에서.</span><span class="sxs-lookup"><span data-stu-id="43d10-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="43d10-143">시작 하는 일반적인 쿼리 tooget 5 개 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="43d10-144">원격 분석 유형, 시간 범위 및 기타 속성에 따라 서로 다른 데이터 집합을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="43d10-145">데이터에 잘못 된 부분 toofind hello "보기 유형" 드롭다운 아래 hello 비정상 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="43d10-146">hello 필터링 옵션 hello hello 창 맨 아래에 원격 분석의 특정 하위 집합에서에서 쉽게 toohone 지정.</span><span class="sxs-lookup"><span data-stu-id="43d10-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![추세](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="43d10-148">[추세 자세히 알아보기](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="43d10-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="43d10-149">로컬 모니터링</span><span class="sxs-lookup"><span data-stu-id="43d10-149">Local monitoring</span></span>
<span data-ttu-id="43d10-150">(Visual Studio 2015 업데이트 2)에서 Hello SDK toosend 원격 분석 toohello Application Insights 포털 (있도록 ApplicationInsights.config의 계측 키가) 구성 하지 않은 경우 hello 진단 창 최신 디버깅 세션에서 원격 분석을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="43d10-151">이전 버전의 앱을 이미 게시한 경우에 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="43d10-152">디버깅 세션 toobe 프로그램에서 원격 분석 hello 혼합 해 서 사용 hello에 대 한 hello 원격 분석 hello 게시 된 앱에서 Application Insights 포털 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="43d10-153">경우에 유용도 몇 가지 [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md) toohello 포털 원격 분석 보내기 전에 toodebug 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="43d10-154">*처음에 완전히 toosend 원격 분석 toohello 포털 Application Insights를 구성 합니다. 하지만 Visual Studio에서만 toosee hello 원격 분석을 이제 좋을 것입니다.*</span><span class="sxs-lookup"><span data-stu-id="43d10-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="43d10-155">Hello 검색 창 설정, 즉 옵션 toosearch 로컬 진단 응용 프로그램 원격 분석 toohello 포털 보낸 경우에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="43d10-156">포털 toohello hello 줄 주석 송신할 toostop 원격 분석 `<instrumentationkey>...` ApplicationInsights.config에서 합니다. 준비 toosend 원격 분석 toohello 포털을 다시 했으면 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="43d10-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43d10-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="43d10-158">**[더 많은 데이터 추가](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="43d10-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="43d10-159">사용량, 가용성, 종속성, 예외를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="43d10-160">로깅 프레임 워크의 추적을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="43d10-161">사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-161">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="43d10-163">**[Hello Application Insights 포털 작업](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="43d10-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="43d10-164">대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 내보낸 원격 분석 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="43d10-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual studio](./media/app-insights-visual-studio/62.png) |

