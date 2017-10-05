---
title: ".NET 앱용 Azure Application Insights 스냅숏 디버거 | Microsoft Docs"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="df9ff-103">.NET 앱의 예외에 대한 디버그 스냅숏</span><span class="sxs-lookup"><span data-stu-id="df9ff-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="df9ff-104">예외가 발생할 때 라이브 웹 응용 프로그램에서 자동으로 디버그 스냅숏을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="df9ff-105">스냅숏은 예외가 throw되었을 때의 소스 코드 및 변수의 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="df9ff-106">[Azure Application Insights](app-insights-overview.md)의 스냅숏 디버거(미리 보기)는 웹앱에서 예외 원격 분석을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="df9ff-107">프로덕션에서 문제를 진단하는 데 필요한 정보를 유지하도록 많이 throw되는 예외에 대한 스냅숏을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="df9ff-108">[스냅숏 수집기 NuGet 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)를 응용 프로그램에 포함하고 필요에 따라, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 컬렉션 매개 변수를 구성합니다. 스냅숏은 Application Insights 포털의 [예외](app-insights-asp-net-exceptions.md)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="df9ff-109">포털에서 디버그 스냅숏을 확인하여 호출 스택을 보고 각 호출 스택 프레임에서 변수를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="df9ff-110">소스 코드가 있는 좀 더 강력한 디버깅 환경을 구현하려면 [Visual Studio용 스냅숏 디버거 확장을 다운로드](https://aka.ms/snapshotdebugger)하여 Visual Studio 2017 Enterprise에서 스냅숏을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="df9ff-111">스냅숏 컬렉션을 다음에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="df9ff-112">.NET Framework 및 .NET Framework 4.5 이상을 실행하는 ASP.NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="df9ff-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="df9ff-113">.NET Core 2.0 및 Windows에서 실행되는 ASP.NET Core 2.0 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="df9ff-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="df9ff-114">ASP.NET 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="df9ff-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="df9ff-115">이 작업을 아직 수행하지 않은 경우 [웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="df9ff-116">[Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 패키지를 앱에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="df9ff-117">패키지가 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에 추가한 기본 옵션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="df9ff-118">스냅숏은 Application Insights에 보고되는 예외에 대해서만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="df9ff-119">경우에 따라(예: 이전 버전의 .NET 플랫폼) 포털에서 스냅숏 예외를 보려면 [예외 컬렉션을 구성](app-insights-asp-net-exceptions.md#exceptions)해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="df9ff-120">ASP.NET Core 2.0 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="df9ff-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="df9ff-121">이 작업을 아직 수행하지 않은 경우 [ASP.NET Core 웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net-core.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="df9ff-122">[Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 패키지를 앱에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="df9ff-123">응용 프로그램의 `Startup` 클래스에서 `ConfigureServices` 메서드를 수정하여 스냅숏 수집기의 원격 분석 프로세서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="df9ff-124">추가해야 하는 코드는 Microsoft.ApplicationInsights.ASPNETCore NuGet 패키지의 참조된 버전에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="df9ff-125">Microsoft.ApplicationInsights.AspNetCore 2.1.0의 경우 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="df9ff-126">Microsoft.ApplicationInsights.AspNetCore 2.1.1의 경우 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="df9ff-127">다른 .NET 응용 프로그램에 대한 스냅숏 컬렉션 구성</span><span class="sxs-lookup"><span data-stu-id="df9ff-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="df9ff-128">응용 프로그램이 아직 Application Insights로 계측되지 않는 경우 먼저 [Application Insights를 사용하도록 설정하고 계측 키를 설정](app-insights-windows-desktop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="df9ff-129">[Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 패키지를 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="df9ff-130">스냅숏은 Application Insights에 보고되는 예외에 대해서만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="df9ff-131">예외를 보고하도록 코드를 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="df9ff-132">예외 처리 코드는 응용 프로그램의 구조에 따라 달라집니다. 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="df9ff-133">권한 부여</span><span class="sxs-lookup"><span data-stu-id="df9ff-133">Grant permissions</span></span>

<span data-ttu-id="df9ff-134">Azure 구독의 소유자는 스냅숏을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="df9ff-135">다른 사용자는 소유자에 의해 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="df9ff-136">사용 권한을 부여하려면 스냅숏을 검사하는 사용자에게 `Application Insights Snapshot Debugger` 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="df9ff-137">대상 Application Insights 리소스 또는 리소스 그룹이나 구독에 대한 구독 소유자가 개별 사용자 또는 그룹에 이 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="df9ff-138">Access Control(IAM) 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="df9ff-139">+추가 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-139">Click the +Add button.</span></span>
1. <span data-ttu-id="df9ff-140">역할 드롭 다운 목록에서 Application Insights 스냅숏 디버거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="df9ff-141">추가할 사용자의 이름을 검색하고 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="df9ff-142">저장 단추를 클릭하여 역할에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="df9ff-143">스냅숏은 변수 및 매개 변수 값의 개인 정보 및 기타 중요한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="df9ff-144">Application Insights 포털에서 스냅숏 디버그</span><span class="sxs-lookup"><span data-stu-id="df9ff-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="df9ff-145">지정된 예외 또는 문제 ID에 대해 스냅숏을 사용할 수 있으면 Application Insights 포털의 [예외](app-insights-asp-net-exceptions.md)에 **디버그 스냅숏 열기** 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![예외에서 디버그 스냅숏 열기 단추](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="df9ff-147">디버그 스냅숏 보기에는 호출 스택 및 변수 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="df9ff-148">호출 스택 창에서 호출 스택의 프레임을 선택하면 변수 창에 해당 함수 호출에 대한 지역 변수 및 매개 변수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![포털에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="df9ff-150">스냅숏에는 중요한 정보가 포함될 수 있으며 기본적으로는 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="df9ff-151">스냅숏을 보려면 `Application Insights Snapshot Debugger` 역할이 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="df9ff-152">Visual Studio 2017 Enterprise에서 스냅숏 디버그</span><span class="sxs-lookup"><span data-stu-id="df9ff-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="df9ff-153">**스냅숏 다운로드** 단추를 클릭하여 Visual Studio 2017 Enterprise에서 열 수 있는 `.diagsession` 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="df9ff-154">`.diagsession` 파일을 열려면 먼저 [Visual Studio용 스냅숏 디버거 확장을 다운로드하고 설치](https://aka.ms/snapshotdebugger)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="df9ff-155">스냅숏 파일을 연 후에 Visual Studio에서 미니덤프 디버깅 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="df9ff-156">**관리 코드 디버그**를 클릭하여 스냅숏을 디버깅하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="df9ff-157">예외가 throw되는 코드 줄에 스냅숏이 열리고 프로세스의 현재 상태를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Visual Studio에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="df9ff-159">다운로드된 스냅숏에는 웹 응용 프로그램 서버에서 발견된 모든 기호 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="df9ff-160">이러한 기호 파일은 소스 코드에 스냅숏 데이터를 연결하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="df9ff-161">App Service 앱의 경우 웹앱을 게시할 때 기호 배포를 사용할 수 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="df9ff-162">스냅숏 작동 방식</span><span class="sxs-lookup"><span data-stu-id="df9ff-162">How snapshots work</span></span>

<span data-ttu-id="df9ff-163">응용 프로그램이 시작되면 응용 프로그램에서 스냅숏 요청을 모니터링하는 별도 스냅숏 업로더 프로세스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="df9ff-164">스냅숏이 요청되면 약 10~20분 안에 실행 중인 프로세스의 섀도 복사본이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="df9ff-165">기본 프로세스가 계속 실행되고 사용자에게 트래픽이 공급되면서 섀도 프로세스가 분석되고 스냅숏이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="df9ff-166">스냅숏은 스냅숏을 보는 데 필요한 관련 기호(.pdb) 파일과 함께 Application Insights에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="df9ff-167">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="df9ff-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="df9ff-168">기호 게시</span><span class="sxs-lookup"><span data-stu-id="df9ff-168">Publish symbols</span></span>
<span data-ttu-id="df9ff-169">스냅숏 디버거를 사용하려면 Visual Studio에서 변수를 디코딩하고 디버깅 환경을 제공하기 위해 프로덕션 서버에 기호 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="df9ff-170">Visual Studio 2017 15.2 릴리스는 App Service에 게시할 때 기본적으로 릴리스 빌드에 대한 기호를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="df9ff-171">이전 버전에서는 기호가 릴리스 모드에서 게시될 수 있게 게시 프로필 `.pubxml` 파일에 다음 줄을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="df9ff-172">Azure Compute 및 기타 형식의 경우 기호 파일이 주 응용 프로그램 .dll의 동일한 폴더(일반적으로 `wwwroot/bin`)에 있거나 현재 경로에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="df9ff-173">최적화된 빌드</span><span class="sxs-lookup"><span data-stu-id="df9ff-173">Optimized builds</span></span>
<span data-ttu-id="df9ff-174">일부 경우에 빌드 프로세스 동안 적용된 최적화 때문에 릴리스 빌드에서 지역 변수를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="df9ff-175">문제 해결</span><span class="sxs-lookup"><span data-stu-id="df9ff-175">Troubleshooting</span></span>

<span data-ttu-id="df9ff-176">이러한 팁은 스냅숏 디버거를 사용하여 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="df9ff-177">계측 키 확인</span><span class="sxs-lookup"><span data-stu-id="df9ff-177">Verify the instrumentation key</span></span>

<span data-ttu-id="df9ff-178">게시된 응용 프로그램에서 올바른 계측 키를 사용하는 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="df9ff-179">일반적으로 Application Insights는 ApplicationInsights.config 파일에서 계측 키를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="df9ff-180">포털에 표시된 Application Insights 리소스에 대한 계측 키와 값이 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="df9ff-181">업로더 로그 확인</span><span class="sxs-lookup"><span data-stu-id="df9ff-181">Check the uploader logs</span></span>

<span data-ttu-id="df9ff-182">스냅숏을 만들면 디스크에 미니덤프 파일(.dmp)이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="df9ff-183">별도의 업로더 프로세스에서 연결된 모든 PDB와 함께 이 미니덤프 파일을 가져와 Application Insights 스냅숏 디버거 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="df9ff-184">미니덤프는 성공적으로 업로드된 후 디스크에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="df9ff-185">미니덤프 업로더에 대한 로그 파일은 디스크에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="df9ff-186">App Service 환경에서는 `D:\Home\LogFiles\Uploader_*.log`에서 이러한 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="df9ff-187">App Service에 대한 Kudu 관리 사이트를 사용하여 이러한 로그 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="df9ff-188">Azure Portal에서 App Service 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="df9ff-189">**고급 도구** 블레이드를 선택하거나, **Kudu**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="df9ff-190">**이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-190">Click **Go**.</span></span>
4. <span data-ttu-id="df9ff-191">**디버그 콘솔** 드롭다운 목록 상자에서 **CMD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="df9ff-192">**LogFiles**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-192">Click **LogFiles**.</span></span>

<span data-ttu-id="df9ff-193">이름이 `Uploader_`로 시작하고 확장명이 `.log`인 파일이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="df9ff-194">해당 아이콘을 클릭하여 모든 로그 파일을 다운로드하거나 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="df9ff-195">파일 이름에 컴퓨터 이름이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-195">The file name includes the machine name.</span></span> <span data-ttu-id="df9ff-196">App Service 인스턴스가 둘 이상의 컴퓨터에서 호스팅되는 경우 각 컴퓨터에 대한 별도의 로그 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="df9ff-197">업로더가 새 미니덤프 파일을 검색한 경우 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="df9ff-198">성공적인 업로드의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="df9ff-199">위 예에서 계측 키는 `c12a605e73c44346a984e00000000000`입니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="df9ff-200">이 값은 응용 프로그램의 계측 키와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="df9ff-201">미니덤프는 ID가 `139e411a23934dc0b9ea08a626db16c5`인 스냅숏에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="df9ff-202">나중에 이 ID를 사용하여 Application Insights Analytics에서 연결된 예외 원격 분석을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="df9ff-203">업로더는 약 15분에 한 번씩 새 PDB를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="df9ff-204">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-204">Here's an example:</span></span>

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

<span data-ttu-id="df9ff-205">App Service에서 호스팅되지 _않는_ 응용 프로그램의 경우 업로더 로그는 미니덤프와 동일한 폴더 `%TEMP%\Dumps\<ikey>`(여기서 `<ikey>`는 계측 키)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="df9ff-206">Application Insights 검색을 사용하여 스냅숏 예외 찾기</span><span class="sxs-lookup"><span data-stu-id="df9ff-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="df9ff-207">스냅숏이 생성될 때 throw되는 예외에는 스냅숏 ID로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="df9ff-208">예외 원격 분석이 Application Insights에 보고될 때 이 스냅숏 ID가 사용자 지정 속성으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="df9ff-209">Application Insights에서 검색 블레이드를 사용하여 `ai.snapshot.id` 사용자 지정 속성으로 모든 원격 분석을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="df9ff-210">Azure Portal에서 Application Insights 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="df9ff-211">**검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-211">Click **Search**.</span></span>
3. <span data-ttu-id="df9ff-212">검색 텍스트 상자에 `ai.snapshot.id`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![포털에서 스냅숏 ID로 원격 분석 검색](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="df9ff-214">이 검색에서 반환되는 결과가 없으면 선택한 시간 범위에서 응용 프로그램에 대해 Application Insights에 보고된 스냅숏이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="df9ff-215">업로더 로그에서 특정 스냅숏 ID를 검색하려면 검색 상자에 해당 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="df9ff-216">업로드된 것을 알고 있는 스냅숏에 대한 원격 분석을 찾을 수 없는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="df9ff-217">계측 키를 확인하여 올바른 Application Insights 리소스가 표시되어 있는지 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="df9ff-218">업로더 로그에서 타임스탬프를 사용하여 해당 시간 범위를 포함하도록 검색의 시간 범위 필터를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="df9ff-219">해당 스냅숏 ID가 포함된 예외가 여전히 보이지 않는 경우 Application Insights에 예외 원격 분석이 보고되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="df9ff-220">스냅숏을 만든 후 예외 원격 분석을 보고하기 전에 응용 프로그램의 작동이 중단된 경우에 이 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="df9ff-221">이 경우 `Diagnose and solve problems`에서 App Service 로그를 검사하여 예기치 않은 다시 시작 또는 처리되지 않은 예외가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df9ff-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df9ff-222">Next steps</span></span>

* <span data-ttu-id="df9ff-223">예외를 기다리지 않고 스냅숏을 가져오기 위해 [코드에서 snappoint를 설정](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="df9ff-224">[웹앱의 예외 진단](app-insights-asp-net-exceptions.md)에서는 Application Insights에서 추가 예외를 표시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="df9ff-225">[스마트 검색](app-insights-proactive-diagnostics.md)은 성능 예외를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="df9ff-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
