---
title: ".NET 응용 프로그램에 대 한 응용 프로그램 통찰력 스냅숏 디버거 aaaAzure | Microsoft Docs"
description: "프로덕션 .NET 앱에서 예외가 throw되면 디버그 스냅숏이 자동으로 수집됨"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="00ba5-103">.NET 앱의 예외에 대한 디버그 스냅숏</span><span class="sxs-lookup"><span data-stu-id="00ba5-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="00ba5-104">예외가 발생할 때 라이브 웹 응용 프로그램에서 자동으로 디버그 스냅숏을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="00ba5-105">hello 스냅숏 소스 코드의 hello 상태를 보여주며, hello 순간 hello 예외에서 변수 throw 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="00ba5-106">hello 스냅숏 디버거 (미리 보기)에서 [Azure Application Insights](app-insights-overview.md) 웹 앱에서 예외 원격 분석을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="00ba5-107">프로덕션에서 toodiagnose 문제 필요한 hello 정보를 프로그램 최상위 예외를 throw 한 예외에 스냅숏을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="00ba5-108">Hello 포함 [스냅숏 수집기 NuGet 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램 및 필요에 따라 컬렉션 매개 변수에서 구성 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다. 스냅숏은 표시에 [예외](app-insights-asp-net-exceptions.md) hello Application Insights 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="00ba5-109">Hello 포털 toosee hello 호출 스택에 있는 디버그 스냅숏을 볼 수 있으며 각 호출 스택 프레임에서 변수를 검사 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="00ba5-110">소스 코드를 하 여 Visual Studio 2017 Enterprise를 사용 하 여 열고 스냅숏 더 강력한 디버깅 환경 tooget [Visual Studio에 대 한 hello 스냅숏 디버거 확장을 다운로드](https://aka.ms/snapshotdebugger)합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="00ba5-111">스냅숏 컬렉션을 다음에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="00ba5-112">.NET Framework 및 .NET Framework 4.5 이상을 실행하는 ASP.NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="00ba5-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="00ba5-113">.NET Core 2.0 및 Windows에서 실행되는 ASP.NET Core 2.0 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="00ba5-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="00ba5-114">ASP.NET 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="00ba5-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="00ba5-115">이 작업을 아직 수행하지 않은 경우 [웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="00ba5-116">Hello 포함 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="00ba5-117">패키지를 너무 추가 hello hello 기본 옵션을 검토[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="00ba5-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="00ba5-118">스냅숏은 보고 tooApplication Insights 예외에 대해서만 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="00ba5-119">경우에 따라 (예를 들어 hello.NET 플랫폼의 이전 버전) 할 수 있습니다 너무[예외 수집을 구성](app-insights-asp-net-exceptions.md#exceptions) hello 포털에서 스냅숏과 함께 toosee 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="00ba5-120">ASP.NET Core 2.0 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="00ba5-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="00ba5-121">이 작업을 아직 수행하지 않은 경우 [ASP.NET Core 웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net-core.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="00ba5-122">Hello 포함 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="00ba5-123">Hello 수정 `ConfigureServices` 응용 프로그램에서 `Startup` tooadd hello 스냅숏 수집기의 원격 분석 프로세서 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="00ba5-124">hello 참조 되는 버전의 hello Microsoft.ApplicationInsights.ASPNETCore NuGet 패키지에 추가 해야 하는 hello 코드에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="00ba5-125">Microsoft.ApplicationInsights.AspNetCore 2.1.0의 경우 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="00ba5-126">Microsoft.ApplicationInsights.AspNetCore 2.1.1의 경우 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="00ba5-127">다른 .NET 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="00ba5-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="00ba5-128">응용 프로그램은 이미 Application insights 계측 되지 않는 경우 하 여 시작 [Application Insights 및 설정 hello 계측 키를 사용 하도록 설정](app-insights-windows-desktop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="00ba5-129">Hello 추가 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="00ba5-130">스냅숏은 보고 tooApplication Insights 예외에 대해서만 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="00ba5-131">코드 tooreport toomodify를 할 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="00ba5-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="00ba5-132">응용 프로그램의 hello 구조 hello 예외 처리 코드를 고려해 지만 아래 예제는:</span><span class="sxs-lookup"><span data-stu-id="00ba5-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="00ba5-133">권한 부여</span><span class="sxs-lookup"><span data-stu-id="00ba5-133">Grant permissions</span></span>

<span data-ttu-id="00ba5-134">Hello Azure 구독 소유자는 스냅숏을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="00ba5-135">다른 사용자는 소유자에 의해 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="00ba5-136">toogrant 권한, 할당 hello `Application Insights Snapshot Debugger` 역할 toousers 스냅숏을 검사 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="00ba5-137">Tooindividual 사용자 또는 hello 대상 Application Insights 리소스에 대 한 구독 소유자가 그룹 또는 리소스 그룹이 나 구독에는이 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="00ba5-138">Hello 액세스 제어 (IAM) 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="00ba5-139">안녕하세요 + 추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="00ba5-140">Hello 역할 드롭 다운 목록에서 응용 프로그램 통찰력 스냅숏 디버거를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="00ba5-141">검색 하 여 사용자 tooadd hello에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="00ba5-142">Hello 저장 단추 tooadd hello 사용자 toohello 역할을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="00ba5-143">스냅숏은 변수 및 매개 변수 값의 개인 정보 및 기타 중요한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="00ba5-144">디버그 hello Application Insights 포털의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="00ba5-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="00ba5-145">주어진된 예외 또는 문제 ID에 대 한 스냅숏을 경우는 **디버그 스냅숏 열기** hello에 단추가 표시 [예외](app-insights-asp-net-exceptions.md) hello Application Insights 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![예외에서 디버그 스냅숏 열기 단추](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="00ba5-147">Hello 디버그 스냅숏 보기, 호출 스택 및 변수 창 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="00ba5-148">선택 하면 hello 호출 스택 창에 프레임 hello 호출 스택, 지역 변수를 볼 수 있습니다 및 hello 변수 창에서 해당 함수에 대 한 매개 변수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Hello 포털에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="00ba5-150">스냅숏에는 중요한 정보가 포함될 수 있으며 기본적으로는 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="00ba5-151">tooview 스냅숏이 있어야 hello `Application Insights Snapshot Debugger` tooyou 할당 된 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="00ba5-152">Visual Studio 2017 Enterprise에서 스냅숏 디버그</span><span class="sxs-lookup"><span data-stu-id="00ba5-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="00ba5-153">Hello 클릭 **다운로드 스냅숏** 단추 toodownload는 `.diagsession` 파일을 Visual Studio 2017 Enterprise에서 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="00ba5-154">tooopen hello `.diagsession` 파일을 먼저 [다운로드 하 고 Visual Studio에 대 한 hello 스냅숏 디버거 확장을 설치](https://aka.ms/snapshotdebugger)합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="00ba5-155">Hello 스냅숏 파일을 연 후에 Visual Studio에서 hello 미니 덤프 디버깅 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="00ba5-156">클릭 **관리 코드 디버그** toostart hello 스냅숏 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="00ba5-157">hello 스냅숏 toohello hello hello 프로세스의 현재 상태를 디버깅할 수 있도록 hello 예외가 throw 된 코드 줄을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Visual Studio에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="00ba5-159">다운로드 된 스냅숏 hello 웹 응용 프로그램 서버에서 발견 된 모든 기호 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="00ba5-160">이러한 기호 파일은 소스 코드를 사용 하 여 필요한 tooassociate 스냅숏 데이터.</span><span class="sxs-lookup"><span data-stu-id="00ba5-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="00ba5-161">앱 서비스 앱에 대 한 웹 앱을 게시할 때 tooenable 기호 배포 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="00ba5-162">스냅숏 작동 방식</span><span class="sxs-lookup"><span data-stu-id="00ba5-162">How snapshots work</span></span>

<span data-ttu-id="00ba5-163">응용 프로그램이 시작되면 응용 프로그램에서 스냅숏 요청을 모니터링하는 별도 스냅숏 업로더 프로세스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="00ba5-164">스냅숏을 요청 될 때 프로세스를 실행 하는 hello의 섀도 복사본이 약 10 too20 분 후에 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="00ba5-165">hello 섀도 프로세스 다음 분석 되 고 스냅숏이 hello 주 프로세스 계속 toorun 동안 만들어지고 트래픽 toousers 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="00ba5-166">hello 스냅숏 위 항목은 다음 업로드 된 tooApplication Insights 파일인 관련 기호 (.pdb) 파일을 함께 필요한 tooview hello 스냅숏 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="00ba5-167">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="00ba5-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="00ba5-168">기호 게시</span><span class="sxs-lookup"><span data-stu-id="00ba5-168">Publish symbols</span></span>
<span data-ttu-id="00ba5-169">hello 스냅숏 디버거 기호 파일을 hello 프로덕션 서버 toodecode 변수 및 tooprovide Visual Studio의 디버깅 환경에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="00ba5-170">Visual Studio 2017 hello 15.2 릴리스의 tooApp 서비스 게시 되 면 기본적으로 릴리스 빌드에 대 한 기호를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="00ba5-171">이전 버전에서는 tooadd hello 다음 필요한 줄 tooyour 게시 프로필 `.pubxml` 기호 릴리스 모드에서 게시 된 파일:</span><span class="sxs-lookup"><span data-stu-id="00ba5-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="00ba5-172">Azure 계산 및 다른 형식에 대 한 hello 기호 파일이 되도록 hello에 hello 주 응용 프로그램.dll의 같은 폴더 (일반적으로 `wwwroot/bin`) 또는 hello 현재 경로에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="00ba5-173">최적화된 빌드</span><span class="sxs-lookup"><span data-stu-id="00ba5-173">Optimized builds</span></span>
<span data-ttu-id="00ba5-174">경우에 따라 hello 빌드 프로세스 동안 적용 되는 최적화로 인해 지역 변수 릴리스 빌드에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="00ba5-175">문제 해결</span><span class="sxs-lookup"><span data-stu-id="00ba5-175">Troubleshooting</span></span>

<span data-ttu-id="00ba5-176">이러한 팁에는 스냅숏 디버거 hello로 문제를 해결 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="00ba5-177">Hello 계측 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="00ba5-178">게시 된 응용 프로그램에서 hello 올바른 계측 키를 사용 하는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="00ba5-179">일반적으로 Application Insights 계측 키를 hello를 hello ApplicationInsights.config 파일에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="00ba5-180">hello 값은 hello 동일 hello 포털에서 볼 수 있는 hello Application Insights 리소스에 대 한 hello 계측 키로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="00ba5-181">Hello 업 로더 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-181">Check hello uploader logs</span></span>

<span data-ttu-id="00ba5-182">스냅숏을 만들면 디스크에 미니덤프 파일(.dmp)이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="00ba5-183">별도 업 로더 프로세스는 미니 덤프 파일을 사용 하 고 모든 관련된 Pdb tooApplication Insights 스냅숏 디버거 저장소와 함께,를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="00ba5-184">Hello 미니 덤프에 성공적으로 업로드 한 후 디스크에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="00ba5-185">미니 덤프 업 로더 hello에 대 한 hello 로그 파일은 디스크에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="00ba5-186">App Service 환경에서는 `D:\Home\LogFiles\Uploader_*.log`에서 이러한 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="00ba5-187">사용 하 여 hello Kudu 관리 사이트에 대 한 앱 서비스 toofind 이러한 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="00ba5-188">Hello Azure 포털에서에서 응용 프로그램 서비스 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="00ba5-189">선택 hello **고급 도구** 블레이드에서 또는 검색에 대 한 **Kudu**합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="00ba5-190">**이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-190">Click **Go**.</span></span>
4. <span data-ttu-id="00ba5-191">Hello에 **디버그 콘솔** 드롭다운 목록 상자에서 **CMD**합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="00ba5-192">**LogFiles**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-192">Click **LogFiles**.</span></span>

<span data-ttu-id="00ba5-193">이름이 `Uploader_`로 시작하고 확장명이 `.log`인 파일이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="00ba5-194">Hello 해당 아이콘 toodownload 있는 모든 로그 파일을 클릭 하거나 브라우저에서 열.</span><span class="sxs-lookup"><span data-stu-id="00ba5-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="00ba5-195">hello 파일 이름에는 hello 컴퓨터 이름이 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="00ba5-196">App Service 인스턴스가 둘 이상의 컴퓨터에서 호스팅되는 경우 각 컴퓨터에 대한 별도의 로그 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="00ba5-197">Hello 업 로더 새 미니 덤프 파일을 감지 하면 hello 로그 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="00ba5-198">성공적인 업로드의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="00ba5-199">이전 예에서 hello hello 계측 키는 `c12a605e73c44346a984e00000000000`합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="00ba5-200">이 값은 응용 프로그램에 대 한 hello 계측 키를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="00ba5-201">hello 미니 덤프 스냅숏으로 hello ID와 연관 된 `139e411a23934dc0b9ea08a626db16c5`합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="00ba5-202">이 ID를 사용할 수 이후 toolocate hello Insights 분석 응용 프로그램에서에서 예외 원격 분석에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="00ba5-203">hello 업 로더 15 분 마다 한 번에 대 한 새 Pdb를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="00ba5-204">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="00ba5-205">응용 프로그램을 _하지_ hello hello 업 로더 로그는 앱 서비스에서 호스트를 hello 미니 덤프와 같은 폴더: `%TEMP%\Dumps\<ikey>` (여기서 `<ikey>` 계측 키입니다).</span><span class="sxs-lookup"><span data-stu-id="00ba5-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="00ba5-206">Application Insights를 사용 하 여 검색 스냅숏과 함께 toofind 예외</span><span class="sxs-lookup"><span data-stu-id="00ba5-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="00ba5-207">예외를 throw 하는 hello 스냅숏 id 태그가 지정 된 스냅숏을 만들 때</span><span class="sxs-lookup"><span data-stu-id="00ba5-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="00ba5-208">보고 된 tooApplication Insights hello 예외 원격 분석을 사용 하는 경우 해당 스냅숏 ID가 사용자 지정 속성으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="00ba5-209">Application Insights에서 검색 블레이드 hello를 사용 hello로 모든 원격 분석을 찾을 수 `ai.snapshot.id` 사용자 지정 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="00ba5-210">Hello Azure 포털에서에서 tooyour Application Insights 리소스를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="00ba5-211">**검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-211">Click **Search**.</span></span>
3. <span data-ttu-id="00ba5-212">형식 `ai.snapshot.id` 에 검색 텍스트 상자 hello 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Hello 포털에서 스냅숏 ID로 원격 분석을 위한 검색](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="00ba5-214">이 검색 결과 반환 하면 스냅숏이 없습니다 hello 선택한 시간 범위에서 응용 프로그램에 대해 보고 된 tooApplication Insights 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="00ba5-215">hello 업 로더 로그에서 특정 스냅숏 ID에 대 한 toosearch hello 검색 상자에 해당 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="00ba5-216">업로드된 것을 알고 있는 스냅숏에 대한 원격 분석을 찾을 수 없는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="00ba5-217">찾고 Application Insights 리소스를 오른쪽 hello hello 계측 키를 확인 하 여 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="00ba5-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="00ba5-218">Hello 업 로더 로그에서 hello 타임 스탬프를 사용 하 여이 시간 범위 hello 검색 toocover의 시간 범위 필터 hello 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="00ba5-219">해당 스냅숏 ID 사용 하 여 예외를 표시 되지 않는 경우 hello 예외 원격 분석 보고 tooApplication Insights 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="00ba5-220">걸리는 hello 스냅숏 후 응용 프로그램에서 충돌 하지만 hello 예외 원격 분석을 보고 하기 전에 이러한 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="00ba5-221">이 경우 앱 서비스에서 기록 하는 hello 확인 `Diagnose and solve problems` toosee 예상 되지 않았습니다 경우 다시 시작 하거나 처리 되지 않은 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00ba5-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00ba5-222">Next steps</span></span>

* <span data-ttu-id="00ba5-223">[코드에 snappoints 설정](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) 예외를 기다리지 않고 tooget 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="00ba5-224">[웹 응용 프로그램의 예외를 진단](app-insights-asp-net-exceptions.md) 설명 방법을 toomake 자세한 예외 표시 tooApplication Insights 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="00ba5-225">[스마트 검색](app-insights-proactive-diagnostics.md)은 성능 예외를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="00ba5-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
