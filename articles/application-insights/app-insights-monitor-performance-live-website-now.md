---
title: "aaaMonitor 라이브 ASP.NET 웹 앱 Azure Application Insights로 | Microsoft Docs"
description: "다시 배포하지 않고 웹 사이트의 성능을 모니터링합니다. VM 또는 Azure의 온-프레미스에서 호스트되는 ASP.NET 웹앱으로 작업합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="4f6e9-104">Application Insights를 사용한 런타임 시 웹앱 계측</span><span class="sxs-lookup"><span data-stu-id="4f6e9-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="4f6e9-105">코드를 다시 배포 또는 toomodify 필요 없이 Azure Application insights는 라이브 웹 응용 프로그램을 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="4f6e9-106">앱이 온-프레미스 IIS 서버에서 호스트되는 경우 상태 모니터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="4f6e9-107">Azure VM에서 실행 하거나 Azure 웹 앱 당한, Application Insights 모니터링 hello Azure 제어판에서 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="4f6e9-108">([라이브 J2EE 웹앱](app-insights-java-live.md) 및 [Azure Cloud Services](app-insights-cloudservices.md)를 계측하는 방법을 설명하는 별도의 문서도 있습니다.) [Microsoft Azure](http://azure.com) 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![예제 차트](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="4f6e9-110">세 경로 tooapply Application Insights tooyour.NET 웹 응용 프로그램의 선택을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="4f6e9-111">**빌드 시간:** [Application Insights SDK 추가 hello] [ greenbrown] tooyour 웹 응용 프로그램 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="4f6e9-112">**실행 시간:** hello 서버에 웹 앱을 빌드하고 hello 코드를 다시 배포 하지 않고도 아래에 설명 된 대로 계측 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="4f6e9-113">**Both:** hello SDK 웹 응용 프로그램 코드를 빌드하고 hello 런타임 확장을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="4f6e9-114">두 옵션의 최상의 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-114">Get hello best of both options.</span></span>

<span data-ttu-id="4f6e9-115">다음은 각 루트의 장점을 요약한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="4f6e9-116">빌드 시간</span><span class="sxs-lookup"><span data-stu-id="4f6e9-116">Build time</span></span> | <span data-ttu-id="4f6e9-117">실행 시간</span><span class="sxs-lookup"><span data-stu-id="4f6e9-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f6e9-118">요청 및 예외</span><span class="sxs-lookup"><span data-stu-id="4f6e9-118">Requests & exceptions</span></span> |<span data-ttu-id="4f6e9-119">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-119">Yes</span></span> |<span data-ttu-id="4f6e9-120">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-120">Yes</span></span> |
| [<span data-ttu-id="4f6e9-121">자세한 예외 정보</span><span class="sxs-lookup"><span data-stu-id="4f6e9-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="4f6e9-122">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-122">Yes</span></span> |
| [<span data-ttu-id="4f6e9-123">종속성 진단</span><span class="sxs-lookup"><span data-stu-id="4f6e9-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="4f6e9-124">.NET 4.6+, 간단히</span><span class="sxs-lookup"><span data-stu-id="4f6e9-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="4f6e9-125">예, 전체 세부 정보: 결과 코드, SQL 명령 텍스트, HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="4f6e9-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="4f6e9-126">시스템 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="4f6e9-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="4f6e9-127">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-127">Yes</span></span> |<span data-ttu-id="4f6e9-128">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-128">Yes</span></span> |
| <span data-ttu-id="4f6e9-129">[사용자 지정 원격 분석에 대 한 API][api]</span><span class="sxs-lookup"><span data-stu-id="4f6e9-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="4f6e9-130">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-130">Yes</span></span> |<span data-ttu-id="4f6e9-131">아니요</span><span class="sxs-lookup"><span data-stu-id="4f6e9-131">No</span></span> |
| [<span data-ttu-id="4f6e9-132">추적 로그 통합</span><span class="sxs-lookup"><span data-stu-id="4f6e9-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="4f6e9-133">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-133">Yes</span></span> |<span data-ttu-id="4f6e9-134">아니요</span><span class="sxs-lookup"><span data-stu-id="4f6e9-134">No</span></span> |
| [<span data-ttu-id="4f6e9-135">페이지 보기 및 사용자 데이터</span><span class="sxs-lookup"><span data-stu-id="4f6e9-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="4f6e9-136">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-136">Yes</span></span> |<span data-ttu-id="4f6e9-137">아니요</span><span class="sxs-lookup"><span data-stu-id="4f6e9-137">No</span></span> |
| <span data-ttu-id="4f6e9-138">Toorebuild 코드가 필요</span><span class="sxs-lookup"><span data-stu-id="4f6e9-138">Need toorebuild code</span></span> |<span data-ttu-id="4f6e9-139">예</span><span class="sxs-lookup"><span data-stu-id="4f6e9-139">Yes</span></span> | <span data-ttu-id="4f6e9-140">아니요</span><span class="sxs-lookup"><span data-stu-id="4f6e9-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="4f6e9-141">라이브 Azure 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="4f6e9-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="4f6e9-142">Azure 웹 서비스로, 여기의 응용 프로그램을 실행 하는 경우 어떻게 tooswitch 모니터링:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="4f6e9-143">Azure의 hello 응용 프로그램의 제어판에서 Application Insights를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Azure 웹앱의 Application Insights 설정](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="4f6e9-145">Hello Application Insights에 대 한 요약 페이지를 열면 hello 아래쪽 tooopen hello 전체 Application Insights 리소스에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Insights tooApplication 클릭 하 여](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="4f6e9-147">[클라우드 및 VM 앱 모니터링](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4f6e9-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="4f6e9-148">Azure에서 클라이언트 쪽 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="4f6e9-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="4f6e9-149">Azure에서 Application Insights를 사용하도록 설정한 경우 페이지 보기 및 사용자 원격 분석을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="4f6e9-150">설정 > 응용 프로그램 설정 선택</span><span class="sxs-lookup"><span data-stu-id="4f6e9-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="4f6e9-151">앱 설정 아래에서 새로운 키 값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="4f6e9-152">키: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="4f6e9-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="4f6e9-153">값: `true`</span><span class="sxs-lookup"><span data-stu-id="4f6e9-153">Value: `true`</span></span>
3. <span data-ttu-id="4f6e9-154">**저장** 설정 hello 및 **다시 시작** 앱.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="4f6e9-155">hello Application Insights JavaScript SDK는 이제 각 웹 페이지에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="4f6e9-156">라이브 IIS 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="4f6e9-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="4f6e9-157">IIS 서버에서 앱이 호스트되는 경우 상태 모니터를 사용하여 Application Insights를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="4f6e9-158">IIS 웹 서버에서 관리자 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="4f6e9-159">Application Insights 상태 모니터 아직 설치 되지 않은 경우 다운로드 하 고 hello 실행 [상태 모니터 설치 관리자](http://go.microsoft.com/fwlink/?LinkId=506648) (실행 또는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 에 응용 프로그램 통찰력 상태에 대 한 검색 모니터)입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="4f6e9-160">상태 모니터에서 설치 하는 hello 웹 응용 프로그램 또는 toomonitor 되도록 웹 사이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="4f6e9-161">Azure 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="4f6e9-162">Hello Application Insights 포털에서 toosee hello 결과 원하는 hello 리소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="4f6e9-163">(일반적으로 것은 최상의 toocreate 새 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="4f6e9-164">이 앱에 대해 [웹 테스트][availability] 또는 [클라이언트 모니터링][client]이 이미 있으면 기존 리소스를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![앱과 리소스를 선택합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="4f6e9-166">IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-166">Restart IIS.</span></span>

    ![Hello 위쪽 hello 대화에 대 한 다시 시작을 선택 합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="4f6e9-168">웹 서비스가 잠시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="4f6e9-169">모니터링 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4f6e9-169">Customize monitoring options</span></span>

<span data-ttu-id="4f6e9-170">Application Insights를 사용 하면 Dll 및 ApplicationInsights.config 추가 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="4f6e9-171">있습니다 수 [hello.config 파일을 편집](app-insights-configuration-with-applicationinsights-config.md) toochange hello 옵션 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="4f6e9-172">앱을 다시 게시할 때 Application Insights 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="4f6e9-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="4f6e9-173">응용 프로그램을 다시 게시 하기 전에 고려해 야 [Visual Studio에서 Application Insights toohello 코드를 추가][greenbrown]합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="4f6e9-174">더 자세한 원격 분석 및 hello 기능 toowrite 사용자 지정 원격 분석을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="4f6e9-175">Toore 하려는 경우-Application Insights toohello 코드를 추가 하지 않고 게시 hello 배포 프로세스는 hello Dll을 삭제할 수 있습니다 및 웹 사이트를 게시 하는 hello에서 ApplicationInsights.config 점에 유의 하세요.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="4f6e9-176">따라서</span><span class="sxs-lookup"><span data-stu-id="4f6e9-176">Therefore:</span></span>

1. <span data-ttu-id="4f6e9-177">ApplicationInsights.config를 편집한 경우 앱을 다시 게시하기 전에 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="4f6e9-178">앱을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-178">Republish your app.</span></span>
3. <span data-ttu-id="4f6e9-179">Application Insights 모니터링을 다시 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="4f6e9-180">(적절 한 방법을 hello 사용: hello Azure 웹 앱 제어판 또는 IIS 호스트에 hello 상태 모니터입니다.)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="4f6e9-181">Hello.config 파일에서 수행 된 모든 편집을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="4f6e9-182">Application Insights의 런타임 구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4f6e9-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="4f6e9-183">연결할 수 없나요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-183">Can't connect?</span></span> <span data-ttu-id="4f6e9-184">원격 분석이 없나요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-184">No telemetry?</span></span>

* <span data-ttu-id="4f6e9-185">열기 [필요한 송신 포트를 hello](app-insights-ip-addresses.md#outgoing-ports) 서버의 방화벽 tooallow 상태 모니터 toowork에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="4f6e9-186">상태 모니터를 열고 왼쪽 창에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="4f6e9-187">Hello "구성 알림" 섹션에서에서이 응용 프로그램에 대 한 모든 진단 메시지가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Hello 성능 블레이드 toosee 요청, 응답 시간, 종속성 및 기타 데이터 열](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="4f6e9-189">Hello 서버에서 "부족 한 사용 권한"에 대 한 메시지를 표시 하는 경우 hello 다음을 보십시오.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="4f6e9-190">IIS 관리자에서 응용 프로그램 풀 선택 열고 **고급 설정**, 아래에서 **프로세스 모델** hello id에 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="4f6e9-191">컴퓨터 관리 제어판에서이 identity toohello 성능 모니터 사용자 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="4f6e9-192">서버에 MMA/SCOM(Systems Center Operations Manager)이 설치된 경우 일부 버전이 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="4f6e9-193">SCOM와 상태 모니터를 제거 하 고 다시 hello 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="4f6e9-194">[문제 해결][qna]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="4f6e9-195">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="4f6e9-195">System Requirements</span></span>
<span data-ttu-id="4f6e9-196">Server에서 Application Insights 상태 모니터에 대한 OS 지원:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="4f6e9-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="4f6e9-197">Windows Server 2008</span></span>
* <span data-ttu-id="4f6e9-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4f6e9-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="4f6e9-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4f6e9-199">Windows Server 2012</span></span>
* <span data-ttu-id="4f6e9-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4f6e9-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="4f6e9-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4f6e9-201">Windows Server 2016</span></span>

<span data-ttu-id="4f6e9-202">최신 SP 및 .NET Framework 4.5 포함</span><span class="sxs-lookup"><span data-stu-id="4f6e9-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="4f6e9-203">Hello 클라이언트 쪽에서:.NET Framework 4.5를 사용 하 여 다시 Windows 7, 8, 8.1 및 10</span><span class="sxs-lookup"><span data-stu-id="4f6e9-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="4f6e9-204">IIS 지원: IIS 7, 7.5, 8, 8.5(IIS 필요)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="4f6e9-205">PowerShell을 사용한 자동화</span><span class="sxs-lookup"><span data-stu-id="4f6e9-205">Automation with PowerShell</span></span>
<span data-ttu-id="4f6e9-206">IIS 서버에서 PowerShell을 사용하여 모니터링을 시작하고 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="4f6e9-207">먼저 hello Application Insights 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="4f6e9-208">어떤 앱을 모니터링 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="4f6e9-209">`-Name`웹 응용 프로그램의 이름 (선택 사항) hello입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="4f6e9-210">이 IIS 서버에 있는 각 웹 응용 프로그램 (또는 hello 라는 응용 프로그램)에 대 한 Application Insights 모니터링 상태를 hello 하는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="4f6e9-211">각 앱에 대해 `ApplicationInsightsApplication`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="4f6e9-212">`SdkState==EnabledAfterDeployment`: 앱 모니터링 되 고 hello 상태 모니터 도구 또는 런타임 시 계측 된 `Start-ApplicationInsightsMonitoring`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="4f6e9-213">`SdkState==Disabled`: hello 앱에 대 한 Application Insights 계측 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="4f6e9-214">계측 되지 된 또는 실행 시간 모니터링을 사용할 수 없습니다와 hello 상태 모니터 도구와 `Stop-ApplicationInsightsMonitoring`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="4f6e9-215">`SdkState==EnabledByCodeInstrumentation`: hello 앱 hello SDK toohello 소스 코드를 추가 하 여 계측 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="4f6e9-216">해당 SDK은 업데이트되거나 중지될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="4f6e9-217">`SdkVersion`이 응용 프로그램 모니터링에 사용 중인 hello 버전을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="4f6e9-218">`LatestAvailableSdkVersion`hello NuGet 갤러리에서 현재 사용할 수 있는 hello 버전을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="4f6e9-219">tooupgrade hello 응용 프로그램 toothis 버전을 사용 하 여 `Update-ApplicationInsightsMonitoring`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="4f6e9-220">`-Name`IIS에서 hello 앱의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="4f6e9-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="4f6e9-221">`-InstrumentationKey`Application Insights 리소스를 표시 하는 hello 결과 toobe 저장할 hello의 ikey를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="4f6e9-222">이 cmdlet은 아직 계측되지 않은 앱에만 영향을 줍니다. 즉, SdkState==NotInstrumented입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="4f6e9-223">hello cmdlet은 이미 계측 하는 응용 프로그램에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="4f6e9-224">Hello SDK toohello 코드를 추가 하 여 빌드 시 hello 응용 프로그램 계측 된 여부는 중요 하거나에서이 cmdlet 사용 하 여 시간을 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="4f6e9-225">hello SDK 사용 되는 버전 tooinstrument hello 앱 가장 최근에 hello 버전 다운로드 toothis 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="4f6e9-226">toodownload hello 최신 버전으로 업데이트 ApplicationInsightsVersion 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="4f6e9-227">성공 시 `ApplicationInsightsApplication`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="4f6e9-228">실패 한 경우 추적 toostderr을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="4f6e9-229">`-Name`IIS에서 응용 프로그램의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="4f6e9-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="4f6e9-230">`-All` `SdkState==EnabledAfterDeployment`인 이 IIS 서버에서 모든 앱에 대한 모니터링을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="4f6e9-231">앱을 지정 하 고 계측을 제거 하는 hello 모니터링을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="4f6e9-232">또한 런타임에 사용 하 여 계측 된 응용 프로그램 상태 모니터링 도구 또는 시작 ApplicationInsightsApplication hello에 대 한 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="4f6e9-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="4f6e9-234">ApplicationInsightsApplication을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="4f6e9-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="4f6e9-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="4f6e9-236">`-Name`: IIS의 웹 앱의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="4f6e9-237">`-InstrumentationKey`(옵션) 사용이이 toochange hello 리소스 toowhich hello 앱의 원격이 분석 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="4f6e9-238">이 cmdlet은:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-238">This cmdlet:</span></span>
  * <span data-ttu-id="4f6e9-239">가장 최근에 업그레이드 hello 앱 toohello 버전의 SDK hello 라는 toothis 컴퓨터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="4f6e9-240">(`SdkState==EnabledAfterDeployment`인 경우에만 작동)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="4f6e9-241">계측 키를 제공 하는 경우 hello 라는 응용 프로그램은 해당 키가 있는 toosend 다시 구성 된 원격 분석 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="4f6e9-242">( `SdkState != Disabled`인 경우 작동)</span><span class="sxs-lookup"><span data-stu-id="4f6e9-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="4f6e9-243">Hello 최신 Application Insights SDK toohello 서버를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="4f6e9-244"><a name="questions"></a>상태 모니터에 대한 질문</span><span class="sxs-lookup"><span data-stu-id="4f6e9-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="4f6e9-245">상태 모니터란?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-245">What is Status Monitor?</span></span>

<span data-ttu-id="4f6e9-246">IIS 웹 서버에 설치한 데스크톱 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="4f6e9-247">웹앱을 계측하고 구성하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="4f6e9-248">언제 상태 모니터를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="4f6e9-249">이미 실행 중인 경우에 모든 웹 앱-IIS 서버에서 실행 되는 tooinstrument 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="4f6e9-250">웹 앱에 대 한 추가 원격 분석 tooenable [hello Application Insights SDK를 사용 하 여 빌드한](app-insights-asp-net.md) 컴파일 타임에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="4f6e9-251">실행한 후에 닫을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-251">Can I close it after it runs?</span></span>

<span data-ttu-id="4f6e9-252">예.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-252">Yes.</span></span> <span data-ttu-id="4f6e9-253">Hello 웹 사이트를 선택 하면 계측에 그 후에이 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="4f6e9-254">자체로 원격 분석을 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="4f6e9-255">방금 hello 웹 응용 프로그램을 구성 하 고 일부 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="4f6e9-256">상태 모니터의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-256">What does Status Monitor do?</span></span>

<span data-ttu-id="4f6e9-257">상태 모니터 tooinstrument에 대 한 웹 앱 선택:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="4f6e9-258">다운로드 하 고 hello Application Insights 어셈블리와.config 파일 hello 웹 응용 프로그램의 이진 파일 폴더에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="4f6e9-259">수정 `web.config` tooadd hello 응용 프로그램 통찰력 HTTP 추적 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="4f6e9-260">CLR toocollect 종속성 호출을 프로 파일링을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="4f6e9-261">Hello 앱을 업데이트 하려면 때마다 toorun 상태 모니터 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="4f6e9-262">증분 방식으로 다시 배포하는 경우에는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="4f6e9-263">프로세스를 게시 hello에서 hello '기존 파일을 삭제 합니다.' 옵션을 선택 하는 경우, toore 실행 상태 모니터 tooconfigure Application Insights 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="4f6e9-264">어떤 원격 분석이 수집되나요?</span><span class="sxs-lookup"><span data-stu-id="4f6e9-264">What telemetry is collected?</span></span>

<span data-ttu-id="4f6e9-265">상태 모니터를 사용하여 런타임 시에만 계측하는 응용 프로그램의 경우:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="4f6e9-266">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="4f6e9-266">HTTP requests</span></span>
* <span data-ttu-id="4f6e9-267">Toodependencies 호출</span><span class="sxs-lookup"><span data-stu-id="4f6e9-267">Calls toodependencies</span></span>
* <span data-ttu-id="4f6e9-268">예외</span><span class="sxs-lookup"><span data-stu-id="4f6e9-268">Exceptions</span></span>
* <span data-ttu-id="4f6e9-269">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="4f6e9-269">Performance counters</span></span>

<span data-ttu-id="4f6e9-270">컴파일 시 이미 계측된 응용 프로그램의 경우:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="4f6e9-271">프로세스 카운터</span><span class="sxs-lookup"><span data-stu-id="4f6e9-271">Process counters.</span></span>
 * <span data-ttu-id="4f6e9-272">종속성 호출(.NET 4.5); 종속성 호출(.NET 4.6)에 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="4f6e9-273">예외 스택 추적 값</span><span class="sxs-lookup"><span data-stu-id="4f6e9-273">Exception stack trace values.</span></span>

[<span data-ttu-id="4f6e9-274">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="4f6e9-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="4f6e9-275">비디오</span><span class="sxs-lookup"><span data-stu-id="4f6e9-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="4f6e9-276"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f6e9-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="4f6e9-277">원격 분석 보기:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-277">View your telemetry:</span></span>

* <span data-ttu-id="4f6e9-278">[메트릭을 탐색](app-insights-metrics-explorer.md) toomonitor 성능 및 사용</span><span class="sxs-lookup"><span data-stu-id="4f6e9-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="4f6e9-279">[이벤트 및 로그를 검색할] [ diagnostic] toodiagnose 문제</span><span class="sxs-lookup"><span data-stu-id="4f6e9-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="4f6e9-280">[분석](app-insights-analytics.md)을 통해 고급 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* <span data-ttu-id="4f6e9-281">[대시보드를 만듭니다](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="4f6e9-281">[Create dashboards](app-insights-dashboards.md)</span></span>

<span data-ttu-id="4f6e9-282">원격 분석 더 추가:</span><span class="sxs-lookup"><span data-stu-id="4f6e9-282">Add more telemetry:</span></span>

* <span data-ttu-id="4f6e9-283">[웹 테스트를 만들] [ availability] toomake 사이트 라이브 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="4f6e9-284">[웹 클라이언트 원격 분석 추가] [ usage] 웹 페이지 코드를 삽입 하면 toolet toosee 예외 호출을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6e9-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="4f6e9-285">[Application Insights SDK tooyour 코드를 추가] [ greenbrown] 추적을 삽입 하 고 호출을 로깅할 수 있도록</span><span class="sxs-lookup"><span data-stu-id="4f6e9-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
