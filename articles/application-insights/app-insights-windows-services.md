---
title: "Windows 서버 및 작업자 역할용 Azure Application Insights | Microsoft Docs"
description: "ASP.NET 응용 프로그램에 Application Insights SDK를 수동으로 추가하여 사용량, 가용성 및 성능을 분석합니다."
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
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="5e530-103">.NET 응용 프로그램에 대한 Application Insights를 수동으로 구성</span><span class="sxs-lookup"><span data-stu-id="5e530-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="5e530-104">[Application Insights](app-insights-overview.md)를 구성하여 다양한 응용 프로그램이나 응용 프로그램 역할, 구성 요소 또는 마이크로 서비스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="5e530-105">웹앱 및 서비스의 경우 Visual Studio에서 [한 단계 구성](app-insights-asp-net.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="5e530-106">백 엔드 서버 역할 또는 데스크톱 응용 프로그램과 같은 다른 유형의 .NET 응용 프로그램의 경우 Application Insights를 수동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![예제 성능 모니터링 차트](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="5e530-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5e530-108">Before you start</span></span>

<span data-ttu-id="5e530-109">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-109">You need:</span></span>

* <span data-ttu-id="5e530-110">[Microsoft Azure](http://azure.com)구독.</span><span class="sxs-lookup"><span data-stu-id="5e530-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="5e530-111">팀 또는 조직에 Azure 구독이 있는 경우 소유자가 [Microsoft 계정](http://live.com)을 사용하여 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="5e530-112">Visual Studio 2013 이상.</span><span class="sxs-lookup"><span data-stu-id="5e530-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="5e530-113"><a name="add"></a>1. Application Insights 리소스 선택</span><span class="sxs-lookup"><span data-stu-id="5e530-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="5e530-114">'리소스'는 Azure Portal에서 데이터를 수집하여 표시하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="5e530-115">새로운 리소스를 만들지, 아니면 기존 리소스를 공유할지를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="5e530-116">더 큰 앱의 일부: 기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="5e530-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="5e530-117">웹 응용 프로그램에 프런트 엔드 웹앱과 하나 이상의 백 엔드 서비스와 같은 여러 구성 요소가 있는 경우 모든 구성 요소의 원격 분석을 동일한 리소스로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="5e530-118">이렇게 하면 단일 Application Map에 표시할 수 있으며 한 구성 요소에서 다른 구성 요소로의 요청을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="5e530-119">따라서 이 앱의 다른 구성 요소를 이미 모니터링하고 있으면 동일한 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="5e530-120">[Azure Portal](https://portal.azure.com/)에서 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="5e530-121">자체 포함된 앱: 새 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="5e530-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="5e530-122">새 앱이 다른 응용 프로그램과 관련이 없으면 자체 리소스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="5e530-123">[Azure 포털](https://portal.azure.com/)에 로그인한 다음 새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="5e530-124">응용 프로그램 유형으로 ASP.NET을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-124">Choose ASP.NET as the application type.</span></span>

![새로 만들기, Application Insights 클릭](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="5e530-126">응용 프로그램 유형을 선택하면 리소스 블레이드의 기본 항목이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="5e530-127">2. 계측 키 복사</span><span class="sxs-lookup"><span data-stu-id="5e530-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="5e530-128">키는 리소스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-128">The key identifies the resource.</span></span> <span data-ttu-id="5e530-129">데이터를 리소스로 보내기 위해 SDK에서 바로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![속성 클릭, 키 선택 및 ctrl+C 누르기](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="5e530-131"><a name="sdk"></a>3. Application Insights 패키지를 응용 프로그램에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="5e530-132">Application Insights 패키지의 설치 및 구성은 작업하는 플랫폼에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="5e530-133">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Nuget 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![마우스 오른쪽 단추로 프로젝트 클릭 및 Nuget 패키지 관리 선택](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="5e530-135">Windows 서버 앱용 Application Insights 패키지인 "Microsoft.ApplicationInsights.WindowsServer"를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    !["Application Insights" 검색](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="5e530-137">*버전은?*</span><span class="sxs-lookup"><span data-stu-id="5e530-137">*Which version?*</span></span>

    <span data-ttu-id="5e530-138">최신 기능을 사용하려면 **시험판 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="5e530-139">관련 문서 또는 블로그는 시험판 버전이 필요한지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="5e530-140">*다른 패키지를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="5e530-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="5e530-141">예.</span><span class="sxs-lookup"><span data-stu-id="5e530-141">Yes.</span></span> <span data-ttu-id="5e530-142">API를 사용하여 사용자 고유의 원격 분석을 보내려는 경우에만 "Microsoft.ApplicationInsights"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="5e530-143">Windows Server 패키지에는 API 외에도 성능 카운터 수집 및 종속성 모니터링과 같은 다양한 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="5e530-144">패키지의 나중 버전으로 업그레이드하려면</span><span class="sxs-lookup"><span data-stu-id="5e530-144">To upgrade to future package versions</span></span>
<span data-ttu-id="5e530-145">종종 새 버전의 SDK가 릴리스됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="5e530-146">[패키지의 새 릴리스](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)로 업그레이드하려면, NuGet 패키지 관리자를 다시 열고 설치된 패키지를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="5e530-147">**Microsoft.ApplicationInsights.WindowsServer**을 선택하고 **업그레이드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="5e530-148">ApplicationInsights.config에 대한 사용자 지정을 변경한 경우, 업그레이드 전에 복사본을 저장하고 나중에 변경 내용을 새 버전에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="5e530-149">4. 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="5e530-149">4. Send telemetry</span></span>
<span data-ttu-id="5e530-150">**API 패키지에만 설치한 경우:**</span><span class="sxs-lookup"><span data-stu-id="5e530-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="5e530-151">코드(예: `main()`)에서 계측 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="5e530-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";`</span><span class="sxs-lookup"><span data-stu-id="5e530-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="5e530-153">[API를 사용하여 고유한 원격 분석을 작성 합니다](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="5e530-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="5e530-154">**다른 Application Insights 패키지를 설치한 경우** 원하는 경우 .config 파일을 사용하여 계측 키를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="5e530-155">ApplicationInsights.config(NuGet 설치에 의해 추가됨)를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="5e530-156">닫는 태그 바로 전에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="5e530-157">`<InstrumentationKey>` *복사한 계측 키* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="5e530-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="5e530-158">솔루션 탐색기에서 ApplicationInsights.config라는 속성이 **빌드 작업 = 콘텐츠, 출력 디렉터리로 복사 = 복사**로 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="5e530-159">[다양한 빌드 구성을 위해 키를 전환](app-insights-separate-resources.md)하려면 계측 키를 코드로 설정하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="5e530-160">키를 코드로 설정하면 `.config` 파일에서 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="5e530-161"><a name="run"></a> 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="5e530-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="5e530-162">**F5** 키를 사용하여 응용 프로그램을 실행하고 여러 페이지를 열어 원격 분석을 생성해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="5e530-163">Visual Studio에 전송한 이벤트 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Visual Studio에서 이벤트 수](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="5e530-165"><a name="monitor"></a> 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="5e530-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="5e530-166">[Azure 포털](https://portal.azure.com/) 로 돌아가서 Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="5e530-167">개요 차트에서 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="5e530-168">처음에는 요소가 1~2개만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="5e530-169">예:</span><span class="sxs-lookup"><span data-stu-id="5e530-169">For example:</span></span>

![클릭하여 추가 데이터 확인](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="5e530-171">차트를 클릭하면 더 자세한 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="5e530-172">메트릭에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="5e530-173">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="5e530-173">No data?</span></span>
* <span data-ttu-id="5e530-174">응용 프로그램을 사용하여 여러 페이지를 열어 원격 분석을 생성해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="5e530-175">[검색](app-insights-diagnostic-search.md) 타일을 열고 개별 이벤트를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="5e530-176">경우에 따라 메트릭 파이프라인을 통해 들어오려면 이벤트가 약간 더 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="5e530-177">몇 초 정도 기다렸다가 **새로고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="5e530-178">차트는 주기적으로 새로 고쳐지지만 일부 데이터가 표시되기를 기다리는 경우에는 수동으로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="5e530-179">[문제 해결](app-insights-troubleshoot-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e530-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="5e530-180">앱 게시</span><span class="sxs-lookup"><span data-stu-id="5e530-180">Publish your app</span></span>
<span data-ttu-id="5e530-181">이제 응용 프로그램을 서버 또는 Azure에 배포하고 누적되는 데이터를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Visual Studio를 사용하여 앱을 게시합니다.](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="5e530-183">디버그 모드에서 실행할 때는 파이프라인을 통해 원격 분석이 신속하게 수행되므로 데이터가 몇 초 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="5e530-184">릴리스 구성에서 앱을 배포할 때는 데이터가 더 천천히 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="5e530-185">서버에 게시한 후 데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="5e530-185">No data after you publish to your server?</span></span>
<span data-ttu-id="5e530-186">서버 방화벽에서 나가는 트래픽에 대해 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="5e530-187">필수 주소 목록은 [이 페이지](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e530-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="5e530-188">빌드 서버에 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="5e530-188">Trouble on your build server?</span></span>
<span data-ttu-id="5e530-189">[이 문제 해결 항목](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e530-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="5e530-190">앱에서 다양한 원격 분석을 생성하는 경우 적응 샘플링 모듈은 이벤트의 대표적인 분수만 전송하여 포털에 전송되는 볼륨을 자동으로 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="5e530-191">그러나, 동일한 요청과 관련된 이벤트가 그룹으로 선택되거나 선택 취소되므로 관련 이벤트 간을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="5e530-192">[샘플링에 대해 알아봅니다](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="5e530-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="5e530-193">비디오</span><span class="sxs-lookup"><span data-stu-id="5e530-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="5e530-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e530-194">Next steps</span></span>
* <span data-ttu-id="5e530-195">[원격 분석 더 추가](app-insights-asp-net-more.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e530-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

