---
title: "Azure 웹 앱 성능 aaaMonitor | Microsoft Docs"
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
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="3383d-104">Azure 웹앱 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="3383d-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="3383d-105">Hello에 [Azure 포털](https://portal.azure.com) 에 대 한 응용 프로그램 성능 모니터링을 설정할 수 있습니다 프로그램 [Azure 웹 앱](../app-service-web/app-service-web-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="3383d-106">[Azure Application Insights](app-insights-overview.md) 해당 활동 toohello Application Insights 서비스에 저장 되 고 분석 하는 방법에 대 한 앱 toosend 원격 분석을 계측 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="3383d-107">메트릭 차트 및 검색 도구 사용할 수 있습니다, toohelp 문제를 진단, 성능 향상을 및 사용량 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="3383d-108">실행 시간 또는 빌드 시간</span><span class="sxs-lookup"><span data-stu-id="3383d-108">Run time or build time</span></span>
<span data-ttu-id="3383d-109">두 가지 방법 중 하나로 hello 응용 프로그램을 계측 하 여 모니터링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="3383d-110">**런타임** - 웹앱이 이미 라이브 상태인 경우 성능 모니터링 확장을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="3383d-111">필요한 toorebuild 아니거나 다시 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="3383d-112">응답 시간, 성공률, 예외, 종속성 등을 모니터링하는 패키지의 표준 집합을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="3383d-113">**빌드 시간** - 개발 중인 앱에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="3383d-114">이 옵션은 융통성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-114">This option is more versatile.</span></span> <span data-ttu-id="3383d-115">또한 toohello에서 같은 표준 패키지를 작성할 수 있습니다 코드 toocustomize hello 원격 분석 또는 toosend 직접 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="3383d-116">특정 작업 또는 응용 프로그램 도메인의 toohello 의미 체계에 따라 레코드 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="3383d-117">Application Insights를 사용하여 시간 계측 실행</span><span class="sxs-lookup"><span data-stu-id="3383d-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="3383d-118">Azure에서 웹앱을 이미 실행 중인 경우 이미 일부 요청 및 오류 비율을 모니터링하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="3383d-119">Application Insights tooget 응답 시간, 모니터링 호출 toodependencies, 스마트 검색 및 hello 강력한 로그 분석 쿼리 언어 같은 더 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="3383d-120">**Application Insights 선택** hello Azure 제어판에서 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![모니터링 아래에서 Application Insights 선택](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="3383d-122">설정 하지 않는 한 이미이 앱에 대 한 Application Insights 리소스 다른 경로 의해 toocreate 새 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="3383d-123">Application Insights를 설치한 후 **웹앱을 계측**합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![웹앱 계측](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="3383d-125">페이지 보기 및 사용자 원격 분석을 위해 **클라이언트 쪽 모니터링을 사용하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="3383d-126">설정 > 응용 프로그램 설정 선택</span><span class="sxs-lookup"><span data-stu-id="3383d-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="3383d-127">앱 설정 아래에서 새로운 키 값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="3383d-128">키: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="3383d-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="3383d-129">값: `true`</span><span class="sxs-lookup"><span data-stu-id="3383d-129">Value: `true`</span></span>
   * <span data-ttu-id="3383d-130">**저장** 설정 hello 및 **다시 시작** 앱.</span><span class="sxs-lookup"><span data-stu-id="3383d-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="3383d-131">**앱을 모니터링합니다**.</span><span class="sxs-lookup"><span data-stu-id="3383d-131">**Monitor your app**.</span></span>  <span data-ttu-id="3383d-132">[Expore hello 데이터](#explore-the-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="3383d-133">이상에서는 원하는 경우 Application Insights를 사용한 hello 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="3383d-134">*Application Insights를 제거 하거나 toosending tooanother 리소스를 전환 하려면 어떻게 합니까?*</span><span class="sxs-lookup"><span data-stu-id="3383d-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="3383d-135">Azure에서 열기 hello 웹 응용 프로그램 제어 블레이드 및 개발 도구를 열 **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="3383d-136">Hello Application Insights 확장을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="3383d-137">다음에서 모니터링에서 Application Insights를 선택 하 고 만들기 하거나 hello 자원을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="3383d-138">Application Insights를 사용한 hello 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="3383d-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="3383d-139">Application Insights는 앱에 SDK를 설치하여 더 자세한 원격 분석을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="3383d-140">특히 추적 로그를 수집하고 [사용자 지정 원격 분석을 작성](app-insights-api-custom-events-metrics.md)하고 보다 자세한 예외 보고서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="3383d-141">**Visual Studio**(2013 업데이트 2 이상)에서 프로젝트를 위한 Application Insights를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="3383d-142">Hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 > Application Insights** 또는 **Configure Application Insights**합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가 또는 Application Insights 구성 선택](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="3383d-144">toosign 묻는 경우 Azure 계정에 대 한 hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="3383d-145">hello 작업에는 두 개의 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="3383d-146">원격 분석을 저장하고, 분석하고 표시할 수 있는 Azure에서 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="3383d-147">Hello Application Insights NuGet 패키지 tooyour 코드 (있지 않은 경우 있습니다)를 추가 하 고 toosend 원격 분석 toohello Azure 리소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="3383d-148">**Hello 원격 분석 테스트** 여 (F5) 개발 컴퓨터에서 실행 중인 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="3383d-149">**Hello 앱 게시** tooAzure hello에 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="3383d-150">*Toosending tooa 다른 Application Insights 리소스를 전환 하는 방법*</span><span class="sxs-lookup"><span data-stu-id="3383d-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="3383d-151">Visual Studio를 마우스 오른쪽 단추로 클릭 hello 프로젝트에서 선택할 **Configure Application Insights** 원하는 hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="3383d-152">새 리소스를 hello 옵션 toocreate를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="3383d-153">다시 빌드하고 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="3383d-154">Hello 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="3383d-154">Explore hello data</span></span>
1. <span data-ttu-id="3383d-155">라이브 메트릭, 두 번째 또는 두 개만이 내 요청 및 오류의 보여 주는 웹 앱 제어판의 Application Insights 블레이드에서 hello 표시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="3383d-156">모든 문제를 즉시 확인할 수 있으므로 앱을 다시 게시하는 경우 매우 유용한 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="3383d-157">Toohello 완전 한 Application Insights 리소스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-157">Click through toohello full Application Insights resource.</span></span>

    ![클릭](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="3383d-159">Azure 리소스 탐색에서 직접 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="3383d-160">클릭 하 여 모든 차트 tooget 자세히:</span><span class="sxs-lookup"><span data-stu-id="3383d-160">Click through any chart tooget more detail:</span></span>
   
    ![Hello Application Insights 개요 블레이드에에서 차트를 클릭 합니다.](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="3383d-162">[메트릭 블레이드를 사용자 지정](app-insights-metrics-explorer.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="3383d-163">추가 toosee 개별 이벤트 및 해당 속성을 통해를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-163">Click through further toosee individual events and their properties:</span></span>
   
    ![해당 형식에 검색을 필터링 하는 이벤트 유형을 tooopen 클릭](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="3383d-165">Hello "..." 링크 tooopen 모든 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="3383d-166">[검색을 사용자 지정](app-insights-diagnostic-search.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="3383d-167">원격 분석을 통해 더 강력한 검색에 대 한 hello를 사용 하 여 [로그 분석 쿼리 언어](app-insights-analytics-tour.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="3383d-168">추가 원격 분석</span><span class="sxs-lookup"><span data-stu-id="3383d-168">More telemetry</span></span>

* [<span data-ttu-id="3383d-169">웹 페이지 로드 데이터</span><span class="sxs-lookup"><span data-stu-id="3383d-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="3383d-170">사용자 지정 원격 분석</span><span class="sxs-lookup"><span data-stu-id="3383d-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="3383d-171">비디오</span><span class="sxs-lookup"><span data-stu-id="3383d-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="3383d-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3383d-172">Next steps</span></span>
* <span data-ttu-id="3383d-173">[라이브 앱에서 hello 프로파일러를 실행](app-insights-profiler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="3383d-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - Application Insights로 Azure Functions 모니터링</span><span class="sxs-lookup"><span data-stu-id="3383d-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="3383d-175">[Azure 진단을 사용 하도록 설정](app-insights-azure-diagnostics.md) 전송 toobe tooApplication Insights 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="3383d-176">[서비스 상태 메트릭을 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="3383d-177">작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="3383d-178">사용 하 여 [JavaScript 앱과 웹 페이지에 대 한 Application Insights](app-insights-javascript.md) 웹 페이지를 방문 하는 hello 브라우저에서 tooget 클라이언트 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="3383d-179">[가용성 웹 테스트 설정](app-insights-monitor-web-app-availability.md) toobe 사이트가 다운 된 경우 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3383d-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

