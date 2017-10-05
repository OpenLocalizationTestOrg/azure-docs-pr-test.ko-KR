---
title: "Azure Application Insights로 라이브 ASP.NET 웹앱 모니터링 | Microsoft Docs"
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
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="0ea38-104">Application Insights를 사용한 런타임 시 웹앱 계측</span><span class="sxs-lookup"><span data-stu-id="0ea38-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="0ea38-105">코드를 수정하거나 다시 배포할 필요 없이 Azure Application Insights를 사용하여 라이브 웹앱을 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="0ea38-106">앱이 온-프레미스 IIS 서버에서 호스트되는 경우 상태 모니터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="0ea38-107">Azure 웹앱이거나 Azure VM에서 실행되는 경우 Azure 제어판의 Application Insights 모니터링에서 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="0ea38-108">([라이브 J2EE 웹앱](app-insights-java-live.md) 및 [Azure Cloud Services](app-insights-cloudservices.md)를 계측하는 방법을 설명하는 별도의 문서도 있습니다.) [Microsoft Azure](http://azure.com) 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![예제 차트](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="0ea38-110">Application Insights를 .NET 웹 응용 프로그램에 적용하는 세 가지 경로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="0ea38-111">**빌드 시간:** 웹앱 코드에 [Application Insights SDK를 추가][greenbrown]합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="0ea38-112">**실행 시간:** 코드를 다시 빌드하거나 다시 작성하지 않고 아래 설명된 대로 서버에서 웹앱을 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="0ea38-113">**모두:** 웹앱 코드에 SDK를 빌드하고 런타임 확장도 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="0ea38-114">두 옵션의 좋은 점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-114">Get the best of both options.</span></span>

<span data-ttu-id="0ea38-115">다음은 각 루트의 장점을 요약한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="0ea38-116">빌드 시간</span><span class="sxs-lookup"><span data-stu-id="0ea38-116">Build time</span></span> | <span data-ttu-id="0ea38-117">실행 시간</span><span class="sxs-lookup"><span data-stu-id="0ea38-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ea38-118">요청 및 예외</span><span class="sxs-lookup"><span data-stu-id="0ea38-118">Requests & exceptions</span></span> |<span data-ttu-id="0ea38-119">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-119">Yes</span></span> |<span data-ttu-id="0ea38-120">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-120">Yes</span></span> |
| [<span data-ttu-id="0ea38-121">자세한 예외 정보</span><span class="sxs-lookup"><span data-stu-id="0ea38-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="0ea38-122">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-122">Yes</span></span> |
| [<span data-ttu-id="0ea38-123">종속성 진단</span><span class="sxs-lookup"><span data-stu-id="0ea38-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="0ea38-124">.NET 4.6+, 간단히</span><span class="sxs-lookup"><span data-stu-id="0ea38-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="0ea38-125">예, 전체 세부 정보: 결과 코드, SQL 명령 텍스트, HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="0ea38-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="0ea38-126">시스템 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="0ea38-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="0ea38-127">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-127">Yes</span></span> |<span data-ttu-id="0ea38-128">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-128">Yes</span></span> |
| <span data-ttu-id="0ea38-129">[사용자 지정 원격 분석에 대 한 API][api]</span><span class="sxs-lookup"><span data-stu-id="0ea38-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="0ea38-130">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-130">Yes</span></span> |<span data-ttu-id="0ea38-131">아니요</span><span class="sxs-lookup"><span data-stu-id="0ea38-131">No</span></span> |
| [<span data-ttu-id="0ea38-132">추적 로그 통합</span><span class="sxs-lookup"><span data-stu-id="0ea38-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="0ea38-133">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-133">Yes</span></span> |<span data-ttu-id="0ea38-134">아니요</span><span class="sxs-lookup"><span data-stu-id="0ea38-134">No</span></span> |
| [<span data-ttu-id="0ea38-135">페이지 보기 및 사용자 데이터</span><span class="sxs-lookup"><span data-stu-id="0ea38-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="0ea38-136">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-136">Yes</span></span> |<span data-ttu-id="0ea38-137">아니요</span><span class="sxs-lookup"><span data-stu-id="0ea38-137">No</span></span> |
| <span data-ttu-id="0ea38-138">코드를 다시 빌드해야 함</span><span class="sxs-lookup"><span data-stu-id="0ea38-138">Need to rebuild code</span></span> |<span data-ttu-id="0ea38-139">예</span><span class="sxs-lookup"><span data-stu-id="0ea38-139">Yes</span></span> | <span data-ttu-id="0ea38-140">아니요</span><span class="sxs-lookup"><span data-stu-id="0ea38-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="0ea38-141">라이브 Azure 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="0ea38-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="0ea38-142">응용 프로그램을 Azure 웹 서비스로 실행 중인 경우 모니터링을 켜는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="0ea38-143">Azure에서 앱 제어판에서 Application Insights를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Azure 웹앱의 Application Insights 설정](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="0ea38-145">Application Insights 요약 페이지가 열리면 맨 아래쪽에 있는 링크를 클릭하여 전체 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Application Insights를 클릭해 갑니다.](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="0ea38-147">[클라우드 및 VM 앱 모니터링](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0ea38-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="0ea38-148">Azure에서 클라이언트 쪽 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="0ea38-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="0ea38-149">Azure에서 Application Insights를 사용하도록 설정한 경우 페이지 보기 및 사용자 원격 분석을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="0ea38-150">설정 > 응용 프로그램 설정 선택</span><span class="sxs-lookup"><span data-stu-id="0ea38-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="0ea38-151">앱 설정 아래에서 새로운 키 값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="0ea38-152">키: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="0ea38-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="0ea38-153">값: `true`</span><span class="sxs-lookup"><span data-stu-id="0ea38-153">Value: `true`</span></span>
3. <span data-ttu-id="0ea38-154">설정을 **저장**하고 앱을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="0ea38-155">Application Insights JavaScript SDK가 이제 각 웹 페이지에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="0ea38-156">라이브 IIS 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="0ea38-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="0ea38-157">IIS 서버에서 앱이 호스트되는 경우 상태 모니터를 사용하여 Application Insights를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="0ea38-158">IIS 웹 서버에서 관리자 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="0ea38-159">Application Insights 상태 모니터가 설치되어 있지 않으면 [상태 모니터 설치 관리자](http://go.microsoft.com/fwlink/?LinkId=506648)를 다운로드하고 실행합니다.(또는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)를 실행하고 Application Insights 상태 모니터를 검색합니다.)</span><span class="sxs-lookup"><span data-stu-id="0ea38-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="0ea38-160">상태 모니터에서 모니터링할 설치된 웹 응용 프로그램 또는 웹 사이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="0ea38-161">Azure 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="0ea38-162">Application Insights 포털에서 결과를 표시할 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="0ea38-163">(일반적으로 새 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="0ea38-164">이 앱에 대해 [웹 테스트][availability] 또는 [클라이언트 모니터링][client]이 이미 있으면 기존 리소스를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="0ea38-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![앱과 리소스를 선택합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="0ea38-166">IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-166">Restart IIS.</span></span>

    ![대화 상자의 위쪽에 있는 다시 시작을 선택합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="0ea38-168">웹 서비스가 잠시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="0ea38-169">모니터링 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0ea38-169">Customize monitoring options</span></span>

<span data-ttu-id="0ea38-170">Application Insights를 사용하면 DLL 및 ApplicationInsights.config가 웹앱에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="0ea38-171">[이 .config 파일을 편집](app-insights-configuration-with-applicationinsights-config.md)하여 일부 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="0ea38-172">앱을 다시 게시할 때 Application Insights 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="0ea38-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="0ea38-173">앱을 다시 게시하기 전에 [Application Insights를 Visual Studio에서 코드에 추가][greenbrown]하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="0ea38-174">이렇게 하면 자세한 원격 분석을 얻을 수 있고 사용자 지정 원격 분석을 작성하는 기능도 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="0ea38-175">Application Insights를 코드에 추가하지 않고 다시 게시하려는 경우, 배포 과정에서 게시된 웹 사이트의 DLL 및 ApplicationInsights.config가 삭제될 수 있으니 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea38-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="0ea38-176">따라서</span><span class="sxs-lookup"><span data-stu-id="0ea38-176">Therefore:</span></span>

1. <span data-ttu-id="0ea38-177">ApplicationInsights.config를 편집한 경우 앱을 다시 게시하기 전에 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="0ea38-178">앱을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-178">Republish your app.</span></span>
3. <span data-ttu-id="0ea38-179">Application Insights 모니터링을 다시 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="0ea38-180">(적절한 방법 즉, Azure 웹앱 제어판 또는 IIS 호스트의 상태 모니터를 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="0ea38-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="0ea38-181">.config 파일에 수행했던 편집 내용을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="0ea38-182">Application Insights의 런타임 구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0ea38-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="0ea38-183">연결할 수 없나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-183">Can't connect?</span></span> <span data-ttu-id="0ea38-184">원격 분석이 없나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-184">No telemetry?</span></span>

* <span data-ttu-id="0ea38-185">상태 모니터가 작동할 수 있도록 서버 방화벽에서 [필요한 송신 포트](app-insights-ip-addresses.md#outgoing-ports)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="0ea38-186">상태 모니터를 열고 왼쪽 창에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="0ea38-187">"구성 알림" 섹션에 이 응용 프로그램에 대한 진단 메시지가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![성능 블레이드를 열어 요청, 응답 시간, 종속성 및 기타 데이터를 확인합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="0ea38-189">서버에서 "권한 부족"에 대한 메시지가 표시되는 경우 다음을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="0ea38-190">IIS 관리자에서 응용 프로그램 풀을 선택하고 **고급 설정**을 연 다음 **프로세스 모델**에서 ID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="0ea38-191">컴퓨터 관리 제어판에서 성능 모니터 사용자 그룹에 이 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="0ea38-192">서버에 MMA/SCOM(Systems Center Operations Manager)이 설치된 경우 일부 버전이 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="0ea38-193">SCOm과 상태 모니터를 제거한 다음 최신 버전을 다시 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea38-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="0ea38-194">[문제 해결][qna]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea38-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="0ea38-195">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0ea38-195">System Requirements</span></span>
<span data-ttu-id="0ea38-196">Server에서 Application Insights 상태 모니터에 대한 OS 지원:</span><span class="sxs-lookup"><span data-stu-id="0ea38-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="0ea38-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="0ea38-197">Windows Server 2008</span></span>
* <span data-ttu-id="0ea38-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0ea38-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="0ea38-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0ea38-199">Windows Server 2012</span></span>
* <span data-ttu-id="0ea38-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0ea38-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="0ea38-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0ea38-201">Windows Server 2016</span></span>

<span data-ttu-id="0ea38-202">최신 SP 및 .NET Framework 4.5 포함</span><span class="sxs-lookup"><span data-stu-id="0ea38-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="0ea38-203">클라이언트 쪽 Windows 7, 8, 8.1 및 10에서, 역시 .NET Framework 4.5 포함</span><span class="sxs-lookup"><span data-stu-id="0ea38-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="0ea38-204">IIS 지원: IIS 7, 7.5, 8, 8.5(IIS 필요)</span><span class="sxs-lookup"><span data-stu-id="0ea38-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="0ea38-205">PowerShell을 사용한 자동화</span><span class="sxs-lookup"><span data-stu-id="0ea38-205">Automation with PowerShell</span></span>
<span data-ttu-id="0ea38-206">IIS 서버에서 PowerShell을 사용하여 모니터링을 시작하고 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="0ea38-207">먼저 Application Insights 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="0ea38-208">어떤 앱을 모니터링 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="0ea38-209">`-Name` (선택 사항) 웹앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="0ea38-210">이 IIS 서버에서 각 웹앱(또는 명명된 앱)에 대한 상태를 모니터링하여 Application Insights를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="0ea38-211">각 앱에 대해 `ApplicationInsightsApplication`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="0ea38-212">`SdkState==EnabledAfterDeployment`: 상태 모니터 도구 또는 `Start-ApplicationInsightsMonitoring`에서 앱을 모니터링하고 런타임 시 계측했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="0ea38-213">`SdkState==Disabled`: 앱이 Application insights에 대해 계측되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="0ea38-214">앱을 계측하지 않았거나 상태 모니터 도구 또는 `Stop-ApplicationInsightsMonitoring`을(를) 사용하여 런타임 모니터링이 비활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="0ea38-215">`SdkState==EnabledByCodeInstrumentation`: 소스 코드에 SDK를 추가하여 앱을 계측했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="0ea38-216">해당 SDK은 업데이트되거나 중지될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="0ea38-217">`SdkVersion`은(는) 이 앱을 모니터링하는 데 사용하는 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="0ea38-218">`LatestAvailableSdkVersion`은(는) NuGet 갤러리에서 현재 사용할 수 있는 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="0ea38-219">앱을 이 버전으로 업그레이드하려면 `Update-ApplicationInsightsMonitoring`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="0ea38-220">`-Name` IIS에서 앱의 이름</span><span class="sxs-lookup"><span data-stu-id="0ea38-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="0ea38-221">`-InstrumentationKey` 결과를 표시하려는 Application Insights 리소스의 ikey입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="0ea38-222">이 cmdlet은 아직 계측되지 않은 앱에만 영향을 줍니다. 즉, SdkState==NotInstrumented입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="0ea38-223">cmdlet은 이미 계측된 앱에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="0ea38-224">앱이 빌드 시 코드에 SDK를 추가하거나 런타임 시 이전에 이 cmdlet을 사용하여 계측되었는지 여부는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="0ea38-225">앱을 계측하는 데 사용한 SDK 버전은 가장 최근에 이 서버에 다운로드된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="0ea38-226">최신 버전을 다운로드하려면 Update-ApplicationInsightsVersion을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="0ea38-227">성공 시 `ApplicationInsightsApplication`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="0ea38-228">실패한 경우 stderr에 대한 추적을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="0ea38-229">`-Name` IIS에서 앱의 이름</span><span class="sxs-lookup"><span data-stu-id="0ea38-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="0ea38-230">`-All` `SdkState==EnabledAfterDeployment`인 이 IIS 서버에서 모든 앱에 대한 모니터링을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="0ea38-231">지정된 앱의 모니터링을 중지하고 계측을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="0ea38-232">실행 시 상태 모니터링 도구 또는 Start-ApplicationInsightsApplication을 사용하여 계측된 앱에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="0ea38-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="0ea38-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="0ea38-234">ApplicationInsightsApplication을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="0ea38-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="0ea38-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="0ea38-236">`-Name`: IIS에서 웹앱의 이름</span><span class="sxs-lookup"><span data-stu-id="0ea38-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="0ea38-237">`-InstrumentationKey`(옵션) 이를 사용하여 앱의 원격 분석이 전송되는 리소스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="0ea38-238">이 cmdlet은:</span><span class="sxs-lookup"><span data-stu-id="0ea38-238">This cmdlet:</span></span>
  * <span data-ttu-id="0ea38-239">최근에 이 컴퓨터에 다운로드된 SDK 버전으로 명명된 앱을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="0ea38-240">(`SdkState==EnabledAfterDeployment`인 경우에만 작동)</span><span class="sxs-lookup"><span data-stu-id="0ea38-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="0ea38-241">계측 키를 제공하는 경우 명명된 앱은 해당 키가 있는 리소스에 원격 분석을 전송하도록 다시 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="0ea38-242">( `SdkState != Disabled`인 경우 작동)</span><span class="sxs-lookup"><span data-stu-id="0ea38-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="0ea38-243">서버에 최신 Application Insights SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="0ea38-244"><a name="questions"></a>상태 모니터에 대한 질문</span><span class="sxs-lookup"><span data-stu-id="0ea38-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="0ea38-245">상태 모니터란?</span><span class="sxs-lookup"><span data-stu-id="0ea38-245">What is Status Monitor?</span></span>

<span data-ttu-id="0ea38-246">IIS 웹 서버에 설치한 데스크톱 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="0ea38-247">웹앱을 계측하고 구성하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="0ea38-248">언제 상태 모니터를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="0ea38-249">이미 실행 중인 경우에라도 IIS 서버에서 실행 중인 모든 웹앱을 계측하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="0ea38-250">컴파일 시 [Application Insights SDK를 사용하여 빌드한](app-insights-asp-net.md) 웹앱에 대한 추가 원격 분석을 사용하도록 설정하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="0ea38-251">실행한 후에 닫을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-251">Can I close it after it runs?</span></span>

<span data-ttu-id="0ea38-252">예.</span><span class="sxs-lookup"><span data-stu-id="0ea38-252">Yes.</span></span> <span data-ttu-id="0ea38-253">선택한 웹 사이트를 계측한 후에 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="0ea38-254">자체로 원격 분석을 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="0ea38-255">웹앱을 구성하고 일부 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="0ea38-256">상태 모니터의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-256">What does Status Monitor do?</span></span>

<span data-ttu-id="0ea38-257">계측할 상태 모니터에 대한 웹앱을 선택하는 경우:</span><span class="sxs-lookup"><span data-stu-id="0ea38-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="0ea38-258">웹앱의 이진 파일 폴더에서 Application Insights 어셈블리 및 .config 파일을 다운로드하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="0ea38-259">`web.config`을 수정하여 Application Insights HTTP 추적 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="0ea38-260">CLR 프로파일링을 사용하여 종속성 호출을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="0ea38-261">앱을 업데이트할 때마다 상태 모니터를 실행해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="0ea38-262">증분 방식으로 다시 배포하는 경우에는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="0ea38-263">게시 프로세스에서 '기존 파일 삭제' 옵션을 선택하는 경우 상태 모니터를 다시 실행하여 Application Insights를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="0ea38-264">어떤 원격 분석이 수집되나요?</span><span class="sxs-lookup"><span data-stu-id="0ea38-264">What telemetry is collected?</span></span>

<span data-ttu-id="0ea38-265">상태 모니터를 사용하여 런타임 시에만 계측하는 응용 프로그램의 경우:</span><span class="sxs-lookup"><span data-stu-id="0ea38-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="0ea38-266">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="0ea38-266">HTTP requests</span></span>
* <span data-ttu-id="0ea38-267">종속성에 대한 호출</span><span class="sxs-lookup"><span data-stu-id="0ea38-267">Calls to dependencies</span></span>
* <span data-ttu-id="0ea38-268">예외</span><span class="sxs-lookup"><span data-stu-id="0ea38-268">Exceptions</span></span>
* <span data-ttu-id="0ea38-269">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="0ea38-269">Performance counters</span></span>

<span data-ttu-id="0ea38-270">컴파일 시 이미 계측된 응용 프로그램의 경우:</span><span class="sxs-lookup"><span data-stu-id="0ea38-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="0ea38-271">프로세스 카운터</span><span class="sxs-lookup"><span data-stu-id="0ea38-271">Process counters.</span></span>
 * <span data-ttu-id="0ea38-272">종속성 호출(.NET 4.5); 종속성 호출(.NET 4.6)에 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="0ea38-273">예외 스택 추적 값</span><span class="sxs-lookup"><span data-stu-id="0ea38-273">Exception stack trace values.</span></span>

[<span data-ttu-id="0ea38-274">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="0ea38-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="0ea38-275">비디오</span><span class="sxs-lookup"><span data-stu-id="0ea38-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="0ea38-276"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ea38-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="0ea38-277">원격 분석 보기:</span><span class="sxs-lookup"><span data-stu-id="0ea38-277">View your telemetry:</span></span>

* <span data-ttu-id="0ea38-278">[메트릭을 탐색하여](app-insights-metrics-explorer.md) 성능 및 사용량을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="0ea38-279">[이벤트 및 로그를 검색하여][diagnostic] 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="0ea38-280">[분석](app-insights-analytics.md)을 통해 고급 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* <span data-ttu-id="0ea38-281">[대시보드를 만듭니다](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="0ea38-281">[Create dashboards](app-insights-dashboards.md)</span></span>

<span data-ttu-id="0ea38-282">원격 분석 더 추가:</span><span class="sxs-lookup"><span data-stu-id="0ea38-282">Add more telemetry:</span></span>

* <span data-ttu-id="0ea38-283">[웹 테스트를 만들어][availability] 사이트가 라이브 상태로 유지되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="0ea38-284">[웹 클라이언트 원격 분석을 추가][usage]하여 웹 페이지 코드에서 예외를 확인하고 추적 호출을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="0ea38-285">[Application Insights SDK를 코드에 추가하여][greenbrown] 추적 및 로그 호출을 삽입할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea38-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
