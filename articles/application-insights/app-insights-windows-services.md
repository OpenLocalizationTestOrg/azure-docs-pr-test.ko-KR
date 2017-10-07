---
title: "Windows 용 Insights 응용 프로그램 서버 및 작업자 역할 aaaAzure | Microsoft Docs"
description: "Hello Application Insights SDK tooyour ASP.NET 응용 프로그램 tooanalyze 사용, 가용성 및 성능에 수동으로 추가 합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="1765f-103">.NET 응용 프로그램에 대한 Application Insights를 수동으로 구성</span><span class="sxs-lookup"><span data-stu-id="1765f-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="1765f-104">구성할 수 있습니다 [Application Insights](app-insights-overview.md) toomonitor 다양 한 응용 프로그램 또는 응용 프로그램 역할, 구성 요소 또는 microservices 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="1765f-105">웹앱 및 서비스의 경우 Visual Studio에서 [한 단계 구성](app-insights-asp-net.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="1765f-106">백 엔드 서버 역할 또는 데스크톱 응용 프로그램과 같은 다른 유형의 .NET 응용 프로그램의 경우 Application Insights를 수동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![예제 성능 모니터링 차트](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="1765f-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1765f-108">Before you start</span></span>

<span data-ttu-id="1765f-109">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-109">You need:</span></span>

* <span data-ttu-id="1765f-110">구독 너무[Microsoft Azure](http://azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="1765f-111">팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit를 사용 하 여 프로그램 [Microsoft 계정](http://live.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="1765f-112">Visual Studio 2013 이상.</span><span class="sxs-lookup"><span data-stu-id="1765f-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="1765f-113"><a name="add"></a>1. Application Insights 리소스 선택</span><span class="sxs-lookup"><span data-stu-id="1765f-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="1765f-114">hello 'resource' 데이터 수집 되 고 hello Azure 포털에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="1765f-115">Toodecide 여부 필요한 toocreate 한 새 또는 기존 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="1765f-116">더 큰 앱의 일부: 기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="1765f-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="1765f-117">웹 응용 프로그램-예: 프런트 엔드 웹 응용 프로그램 및 하나 이상의 백 엔드 서비스-여러 구성 요소에 경우 모든 hello 구성 요소 toohello에서 원격 분석을 전송 해야 동일한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="1765f-118">있도록 toobe 단일 응용 프로그램 지도에 표시 되 고 가능한 tootrace tooanother 하나의 구성 요소에서에서 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="1765f-119">따라서이 앱의 다른 구성 요소를 이미 모니터링 하는 경우 다음 사용할 hello 동일한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="1765f-120">Hello에 hello 리소스 열기 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="1765f-121">자체 포함된 앱: 새 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1765f-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="1765f-122">관련 없는 tooother 응용 프로그램 hello 새 앱을 사용 하는 경우 자체 리소스가 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="1765f-123">Toohello 로그인 [Azure 포털](https://portal.azure.com/), 새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="1765f-124">ASP.NET hello 응용 프로그램 유형으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-124">Choose ASP.NET as hello application type.</span></span>

![새로 만들기, Application Insights 클릭](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="1765f-126">응용 프로그램 종류의 hello 선택 hello 리소스 블레이드 hello 기본 콘텐츠를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="1765f-127">2. Hello 계측 키 복사</span><span class="sxs-lookup"><span data-stu-id="1765f-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="1765f-128">hello 키 hello 리소스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-128">hello key identifies hello resource.</span></span> <span data-ttu-id="1765f-129">순서 toodirect 데이터 toohello 리소스에 SDK, hello에 곧에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![속성을 클릭 hello 키를 선택 하 고 ctrl + C를 누릅니다.](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="1765f-131"><a name="sdk"></a>3. 응용 프로그램에서 hello Application Insights 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="1765f-132">설치 및 구성 hello Application Insights 패키지에서 작업 하는 hello 플랫폼에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="1765f-133">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Nuget 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Nuget 패키지 관리 선택](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="1765f-135">Windows server 응용 프로그램의 경우 "Microsoft.ApplicationInsights.WindowsServer" hello Application Insights 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="1765f-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    !["Application Insights" 검색](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="1765f-137">*버전은?*</span><span class="sxs-lookup"><span data-stu-id="1765f-137">*Which version?*</span></span>

    <span data-ttu-id="1765f-138">확인 **시험판 포함** tootry 우리의 최신 기능을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="1765f-139">hello 관련 문서 또는 블로그 시험판 버전 해야 할지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="1765f-140">*다른 패키지를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="1765f-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="1765f-141">예.</span><span class="sxs-lookup"><span data-stu-id="1765f-141">Yes.</span></span> <span data-ttu-id="1765f-142">원하는 경우 toouse hello API toosend 직접 원격 분석 "Microsoft.ApplicationInsights"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="1765f-143">hello Windows Server 패키지 hello API와 다양 한 성능 카운터를 수집 및 종속성을 모니터링 하는 등의 다른 패키지를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="1765f-144">tooupgrade toofuture 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="1765f-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="1765f-145">새 버전의 SDK에서 시간 tootime hello 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="1765f-146">tooupgrade tooa [hello 패키지의 새 릴리스](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)를 NuGet 패키지 관리자를 다시 열고 설치 된 패키지를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="1765f-147">**Microsoft.ApplicationInsights.WindowsServer**을 선택하고 **업그레이드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="1765f-148">모든 사용자 지정 tooApplicationInsights.config를 수행한 경우, 업그레이드 하 고 나중에 변경 내용을 hello 새 버전에 병합 하기 전에 해당 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="1765f-149">4. 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="1765f-149">4. Send telemetry</span></span>
<span data-ttu-id="1765f-150">**Hello API 패키지만 설치:**</span><span class="sxs-lookup"><span data-stu-id="1765f-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="1765f-151">예를 들어에 코드의 hello 계측 키를 설정 `main()`:</span><span class="sxs-lookup"><span data-stu-id="1765f-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="1765f-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";`</span><span class="sxs-lookup"><span data-stu-id="1765f-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="1765f-153">[Hello API를 사용 하 여 사용자 고유의 원격 분석을 작성](app-insights-api-custom-events-metrics.md#ikey)합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="1765f-154">**다른 Application Insights 패키지를 설치한 경우** 사용할 수 있습니다, 원하는 경우 hello.config 파일 tooset hello 계측 키:</span><span class="sxs-lookup"><span data-stu-id="1765f-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="1765f-155">ApplicationInsights.config (있음 hello NuGet을 설치 하 여 추가 된)를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="1765f-156">이 hello 닫는 태그 바로 앞에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="1765f-157">`<InstrumentationKey>`*hello 계측 키를 복사한*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="1765f-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="1765f-158">솔루션 탐색기에서 ApplicationInsights.config의 hello 속성 너무 설정 되어 있는지 확인**빌드 작업 콘텐츠를 복사 tooOutput 디렉터리 = = 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="1765f-159">너무 원하는 경우 코드에서 유용한 tooset hello 계측 키에는[다양 한 빌드 구성에 대 한 스위치 hello 키](app-insights-separate-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="1765f-160">코드에서 hello 키를 설정 하면 없으면 tooset hello에서 `.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="1765f-161"><a name="run"></a> 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="1765f-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="1765f-162">사용 하 여 hello **F5** toorun 응용 프로그램을 사용해 보세요: 다른 열기 페이지 toogenerate 일부 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="1765f-163">Visual Studio에서 전송 된 hello 이벤트 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Visual Studio에서 이벤트 수](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="1765f-165"><a name="monitor"></a> 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="1765f-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="1765f-166">Toohello 반환 [Azure 포털](https://portal.azure.com/) tooyour Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="1765f-167">Hello 개요 차트의 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="1765f-168">처음에는 요소가 1~2개만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="1765f-169">예:</span><span class="sxs-lookup"><span data-stu-id="1765f-169">For example:</span></span>

![클릭 하 여 toomore 데이터](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="1765f-171">클릭 하 여 더 자세한 메트릭을 통해 모든 차트 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="1765f-172">메트릭에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="1765f-173">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="1765f-173">No data?</span></span>
* <span data-ttu-id="1765f-174">일부 원격 분석을 생성할 수 있도록 각기 다른 페이지를 여는 hello 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="1765f-175">열기 hello [검색](app-insights-diagnostic-search.md) 타일을 toosee 개별 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="1765f-176">경우에 따라 이벤트 hello 메트릭 파이프라인을 통해 약간 더 오래 동안 tooget을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="1765f-177">몇 초 정도 기다렸다가 **새로고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="1765f-178">차트 자체 주기적으로 새로 고쳐집니다, 하지만 일부 데이터 tooshow 기다리는 경우 수동으로 새로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="1765f-179">[문제 해결](app-insights-troubleshoot-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1765f-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="1765f-180">앱 게시</span><span class="sxs-lookup"><span data-stu-id="1765f-180">Publish your app</span></span>
<span data-ttu-id="1765f-181">이제 응용 프로그램 tooyour 서버를 배포 하거나 tooAzure 및 조사식 hello 데이터를 누적 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Visual Studio toopublish 응용 프로그램 사용](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="1765f-183">디버그 모드에서 실행 하는 경우 원격 분석 신속히 처리 hello 파이프라인을 통해 초 내에 나타나는 데이터를 찾도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="1765f-184">릴리스 구성에서 앱을 배포할 때는 데이터가 더 천천히 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="1765f-185">데이터가 없는 tooyour 서버를 게시 한 후?</span><span class="sxs-lookup"><span data-stu-id="1765f-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="1765f-186">서버 방화벽에서 나가는 트래픽에 대해 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="1765f-187">참조 [이 페이지](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello 목록이 필요한 주소에 대 한</span><span class="sxs-lookup"><span data-stu-id="1765f-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="1765f-188">빌드 서버에 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="1765f-188">Trouble on your build server?</span></span>
<span data-ttu-id="1765f-189">[이 문제 해결 항목](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1765f-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="1765f-190">응용 프로그램 원격 분석을 많이 생성, hello 적응 샘플링 모듈 toohello 포털 이벤트의 대표 일부만 전송 하 여 전송 된 hello 볼륨을 자동으로 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="1765f-191">그러나 이벤트 하는 동일한 요청 선택 하거나 그룹으로 선택 취소 해야 하는 관련된 toohello 관련된 이벤트를 탐색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1765f-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="1765f-192">[샘플링에 대해 알아봅니다](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="1765f-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="1765f-193">비디오</span><span class="sxs-lookup"><span data-stu-id="1765f-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="1765f-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1765f-194">Next steps</span></span>
* <span data-ttu-id="1765f-195">[더 많은 원격 분석 추가](app-insights-asp-net-more.md) tooget hello 응용 프로그램의 전체 360도 보기.</span><span class="sxs-lookup"><span data-stu-id="1765f-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

