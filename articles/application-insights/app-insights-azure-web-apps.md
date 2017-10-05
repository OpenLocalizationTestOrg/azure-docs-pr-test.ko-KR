---
title: "Azure 웹앱 성능 모니터링 | Microsoft Docs"
description: "Azure 웹앱에 대한 응용 프로그램 성능 모니터링입니다. 차트 부하 및 응답 시간, 종속성 정보 및 성능에 대한 경고를 설정합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="f4f40-104">Azure 웹앱 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="f4f40-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="f4f40-105">[Azure Portal](https://portal.azure.com)에서 [Azure 웹앱](../app-service-web/app-service-web-overview.md)의 응용 프로그램 성능 모니터링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="f4f40-106">[Azure Application Insights](app-insights-overview.md)는 해당 작업에 대한 원격 분석을 저장하고 분석하는 Application Insights 서비스에 보내는 앱을 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="f4f40-107">여기서 메트릭 차트 및 검색 도구를 사용하여 문제를 진단하고 성능을 개선하며 사용량 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="f4f40-108">실행 시간 또는 빌드 시간</span><span class="sxs-lookup"><span data-stu-id="f4f40-108">Run time or build time</span></span>
<span data-ttu-id="f4f40-109">다음과 같은 두 가지 방법 중 하나로 앱을 계측하여 모니터링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="f4f40-110">**런타임** - 웹앱이 이미 라이브 상태인 경우 성능 모니터링 확장을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="f4f40-111">앱을 다시 빌드하거나 설치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="f4f40-112">응답 시간, 성공률, 예외, 종속성 등을 모니터링하는 패키지의 표준 집합을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="f4f40-113">**빌드 시간** - 개발 중인 앱에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="f4f40-114">이 옵션은 융통성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-114">This option is more versatile.</span></span> <span data-ttu-id="f4f40-115">동일한 표준 패키지 외에도 원격 분석 데이터를 사용자 지정하거나 고유한 원격 분석을 보내는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="f4f40-116">앱 도메인의 의미 체계에 따라 특정 작업 또는 레코드 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="f4f40-117">Application Insights를 사용하여 시간 계측 실행</span><span class="sxs-lookup"><span data-stu-id="f4f40-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="f4f40-118">Azure에서 웹앱을 이미 실행 중인 경우 이미 일부 요청 및 오류 비율을 모니터링하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="f4f40-119">Application Insights를 추가하여 응답 시간, 종속성 호출 모니터링, 스마트 검색, 강력한 Log Analytics 쿼리 언어 등 더 많은 것을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="f4f40-120">웹앱의 Azure 제어판에서 **Application Insights를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![모니터링 아래에서 Application Insights 선택](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="f4f40-122">다른 경로로 이 앱에 대한 Application Insights 리소스를 설정하지 않은 경우 새 리소스 만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="f4f40-123">Application Insights를 설치한 후 **웹앱을 계측**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![웹앱 계측](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="f4f40-125">페이지 보기 및 사용자 원격 분석을 위해 **클라이언트 쪽 모니터링을 사용하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="f4f40-126">설정 > 응용 프로그램 설정 선택</span><span class="sxs-lookup"><span data-stu-id="f4f40-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="f4f40-127">앱 설정 아래에서 새로운 키 값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="f4f40-128">키: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="f4f40-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="f4f40-129">값: `true`</span><span class="sxs-lookup"><span data-stu-id="f4f40-129">Value: `true`</span></span>
   * <span data-ttu-id="f4f40-130">설정을 **저장**하고 앱을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="f4f40-131">**앱을 모니터링합니다**.</span><span class="sxs-lookup"><span data-stu-id="f4f40-131">**Monitor your app**.</span></span>  <span data-ttu-id="f4f40-132">[데이터를 내보냅니다](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="f4f40-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="f4f40-133">나중에 원하는 경우 Application Insights로 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="f4f40-134">*Application Insights를 제거하거나 다른 리소스에 보내기로 전환하려면 어떻게 해야 합니까?*</span><span class="sxs-lookup"><span data-stu-id="f4f40-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="f4f40-135">Azure에서 웹앱 제어 블레이드를 열고 개발 도구 아래에서 **확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="f4f40-136">Application Insights 확장을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="f4f40-137">그런 다음 모니터링 아래에서 Application Insights를 선택하고 원하는 리소스를 만들거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="f4f40-138">Application Insights로 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="f4f40-138">Build the app with Application Insights</span></span>
<span data-ttu-id="f4f40-139">Application Insights는 앱에 SDK를 설치하여 더 자세한 원격 분석을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="f4f40-140">특히 추적 로그를 수집하고 [사용자 지정 원격 분석을 작성](app-insights-api-custom-events-metrics.md)하고 보다 자세한 예외 보고서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="f4f40-141">**Visual Studio**(2013 업데이트 2 이상)에서 프로젝트를 위한 Application Insights를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="f4f40-142">웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가 > Application Insights** 또는 **Application Insights 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 추가 또는 구성 선택](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="f4f40-144">로그인이 요청되면 자신의 Azure 계정에 대한 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="f4f40-145">작업에는 두 가지 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="f4f40-146">원격 분석을 저장하고, 분석하고 표시할 수 있는 Azure에서 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="f4f40-147">Application Insights NuGet 패키지를 사용자 코드에 추가하고(없는 경우) 원격 분석을 Azure 리소스로 전송하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="f4f40-148">개발 컴퓨터(F5)에서 앱을 실행하여 **원격 분석을 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="f4f40-149">일반적인 방법으로 Azure에 **앱을 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="f4f40-150">*다른 Application Insights 리소스에 보내기로 전환하려면 어떻게 해야 합니까?*</span><span class="sxs-lookup"><span data-stu-id="f4f40-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="f4f40-151">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **Application Insights 구성**을 선택한 다음, 원하는 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="f4f40-152">새 리소스를 만드는 옵션이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-152">You get the option to create a new resource.</span></span> <span data-ttu-id="f4f40-153">다시 빌드하고 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="f4f40-154">데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="f4f40-154">Explore the data</span></span>
1. <span data-ttu-id="f4f40-155">웹앱 제어판의 Application Insights 블레이드에 두 번째 또는 두 개의 발생 내에서 요청 및 실패를 보여 주는 라이브 메트릭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="f4f40-156">모든 문제를 즉시 확인할 수 있으므로 앱을 다시 게시하는 경우 매우 유용한 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="f4f40-157">전체 Application Insights 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-157">Click through to the full Application Insights resource.</span></span>

    ![클릭](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="f4f40-159">Azure 리소스 탐색에서 직접 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="f4f40-160">차트를 클릭하여 자세한 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-160">Click through any chart to get more detail:</span></span>
   
    ![Application Insights 개요 블레이드에서 차트를 클릭합니다.](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="f4f40-162">[메트릭 블레이드를 사용자 지정](app-insights-metrics-explorer.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="f4f40-163">개별 이벤트와 해당 속성을 보려면 또 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-163">Click through further to see individual events and their properties:</span></span>
   
    ![해당 유형에 대해 필터링된 검색을 열려면 이벤트 유형을 클릭합니다.](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="f4f40-165">"..." 링크를 확인하여 모든 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="f4f40-166">[검색을 사용자 지정](app-insights-diagnostic-search.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="f4f40-167">원격 분석을 통해 보다 강력하게 검색하려면 [Log Analytics 쿼리 언어](app-insights-analytics-tour.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="f4f40-168">추가 원격 분석</span><span class="sxs-lookup"><span data-stu-id="f4f40-168">More telemetry</span></span>

* [<span data-ttu-id="f4f40-169">웹 페이지 로드 데이터</span><span class="sxs-lookup"><span data-stu-id="f4f40-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="f4f40-170">사용자 지정 원격 분석</span><span class="sxs-lookup"><span data-stu-id="f4f40-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="f4f40-171">비디오</span><span class="sxs-lookup"><span data-stu-id="f4f40-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="f4f40-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4f40-172">Next steps</span></span>
* <span data-ttu-id="f4f40-173">[라이브 앱에서 프로파일러를 실행합니다](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="f4f40-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="f4f40-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - Application Insights로 Azure Functions 모니터링</span><span class="sxs-lookup"><span data-stu-id="f4f40-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="f4f40-175">[Azure 진단을 사용](app-insights-azure-diagnostics.md) 하여 Application Insights에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="f4f40-176">[서비스 상태 메트릭을 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)하여 서비스를 사용 가능하며 응답할 수 있는 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="f4f40-177">작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="f4f40-178">[JavaScript 앱 및 웹 페이지용 Application Insights](app-insights-javascript.md)를 사용하여 웹 페이지로 이동하는 브라우저에서 클라이언트 원격 분석을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="f4f40-179">[가용성 웹 테스트를 설정](app-insights-monitor-web-app-availability.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f40-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

