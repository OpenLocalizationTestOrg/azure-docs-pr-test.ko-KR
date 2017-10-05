---
title: "Azure Application Insights에서 개발, 테스트 및 릴리스의 원격 분석 구분 | Microsoft Docs"
description: "개발, 테스트 및 프로덕션 스탬프에 대한 다양한 리소스에 직접 원격 분석"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="96577-103">개발, 테스트 및 프로덕션의 원격 분석 구분</span><span class="sxs-lookup"><span data-stu-id="96577-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="96577-104">웹 응용 프로그램의 다음 버전을 개발할 때 새 버전과 이미 릴리스된 버전의 [Application Insights](app-insights-overview.md) 원격 분석이 혼동되지 않도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="96577-105">혼동을 방지하기 위해 서로 다른 개발 단계의 원격 분석을 별도의 계측 키(ikeys)와 함께 별도의 Application Insights 리소스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="96577-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="96577-106">버전이 단계별로 이동됨에 따라 계측 키 변경을 보다 쉽게 하기 위해서는 구성 파일 대신 코드에 ikey를 설정하는 것이 더 나을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="96577-107">시스템이 Azure 클라우드 서비스인 경우 [별도의 ikey를 설정하는 다른 방법](app-insights-cloudservices.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="96577-108">리소스 및 계측 키 정보</span><span class="sxs-lookup"><span data-stu-id="96577-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="96577-109">사용자 웹앱에 대해 Application Insights 모니터링을 설정할 경우 Microsoft Azure에서 Application Insights *리소스*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96577-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="96577-110">앱에서 수집된 원격 분석을 보고 분석하기 위해서는 Azure Portal에서 이 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96577-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="96577-111">리소스는 해당 *계측 키*(ikey)로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="96577-112">앱을 모니터링하기 위해 Application Insights 패키지를 설치하는 경우 원격 분석을 보낼 위치를 파악할 수 있도록 계측 키로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="96577-113">일반적으로 다양한 시나리오에 별도의 리소스 또는 단일 공유 리소스를 사용하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="96577-114">서로 다른 독립적인 응용 프로그램 - 각 앱에 대해 별도의 리소스와 ikey를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="96577-115">한 비즈니스 응용 프로그램의 여러 구성 요소 또는 역할 - 모든 구성 요소 앱에 대해 [단일 공유 리소스](app-insights-monitor-multi-role-apps.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="96577-116">cloud_RoleName 속성에 따라 원격 분석을 필터링 또는 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="96577-117">개발, 테스트 및 릴리스 - '스탬프' 프로덕션 단계에서 시스템 버전에 따라 별도의 리소스 및 ikey를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="96577-118">A | B 테스트 - 단일 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="96577-119">변형을 식별하는 원격 분석에 속성을 추가하는 TelemetryInitializer를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96577-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="96577-120"><a name="dynamic-ikey"></a> 동적 계측 키</span><span class="sxs-lookup"><span data-stu-id="96577-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="96577-121">코드가 프로덕션 단계 간에 이동함에 따라 보다 쉽게 ikey를 변경할 수 있도록 구성 파일 대신 코드에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="96577-122">ASP.NET 서비스의 global.aspx.cs 같은 초기화 메서드에서 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="96577-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="96577-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="96577-124">이 예제에서는 서로 다른 리소스에 대한 ikeys는 다른 버전의 웹 구성 파일에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="96577-125">웹 구성 파일 교체는 릴리스 스크립트의 일부로 수행될 수 있고 대상 리소스를 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="96577-126">웹 페이지</span><span class="sxs-lookup"><span data-stu-id="96577-126">Web pages</span></span>
<span data-ttu-id="96577-127">iKey는 [빠른 시작 블레이드에서 가져온 스크립트](app-insights-javascript.md)내의 응용 프로그램 웹페이지에서도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="96577-128">스크립트에 문자 그대로 코딩하는 대신, 서버 상태로부터 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="96577-129">예를 들어, ASP.NET 응용 프로그램에서:</span><span class="sxs-lookup"><span data-stu-id="96577-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="96577-130">*Razor에서 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="96577-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="96577-131">추가 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="96577-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="96577-132">동일한 구성 요소의 다른 응용 프로그램 구성 요소 또는 다른 스탬프(개발/테스트/프로덕션)에 대한 원격 분석을 분리하려면 새 Application Insights 리소스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="96577-133">[portal.azure.com](https://portal.azure.com)에서 Application Insights 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![새로 만들기, Application Insights 클릭](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="96577-135">**응용 프로그램 유형** 은 개요 블레이드에 표시되는 내용 및 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 사용할 수 있는 속성에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96577-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="96577-136">앱 유형이 표시되지 않으면 웹 페이지에 대해 웹 유형 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="96577-137">**리소스 그룹** 은 [액세스 제어](app-insights-resources-roles-access-control.md)와 같은 속성을 관리하기 위한 편의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="96577-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="96577-138">개발, 테스트 및 프로덕션 환경에 대 한 별도 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="96577-139">**구독** 은 Azure의 지불 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="96577-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="96577-140">**위치** 는 데이터를 보관하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="96577-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="96577-141">현재는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="96577-142">**대시보드에 추가** 는 Azure 홈 페이지에 리소스에 대한 빠른 액세스 타일을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="96577-143">리소스 생성 시 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="96577-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="96577-144">완료되면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="96577-145">(리소스를 자동으로 만드는 [PowerShell 스크립트](app-insights-powershell-script-create-resource.md) 를 작성할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="96577-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="96577-146">계측 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="96577-146">Getting the instrumentation key</span></span>
<span data-ttu-id="96577-147">계측 키는 사용자가 만든 리소스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-147">The instrumentation key identifies the resource that you created.</span></span> 

![Essentials과 계측 키를 차례로 클릭하고, CTRL + C 누릅니다.](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="96577-149">사용자의 앱이 데이터를 보낼 모든 리소스의 계측 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="96577-150">빌드 번호 필터링</span><span class="sxs-lookup"><span data-stu-id="96577-150">Filter on build number</span></span>
<span data-ttu-id="96577-151">앱의 새 버전을 게시하면서 다른 빌드의 원격 분석을 구분하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="96577-152">응용 프로그램 버전 속성을 설정하여 [검색](app-insights-diagnostic-search.md) 및 [메트릭 탐색기](app-insights-metrics-explorer.md) 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![속성 필터링](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="96577-154">응용 프로그램 버전 속성은 몇 가지 다른 방법으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="96577-155">직접 설정:</span><span class="sxs-lookup"><span data-stu-id="96577-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="96577-156">[원격 분석 이니셜라이저](app-insights-api-custom-events-metrics.md#defaults) 에서 해당 줄을 래핑하여 모든 TelemetryClient 인스턴스가 일관되게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="96577-157">[ASP.NET] `BuildInfo.config`에서 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="96577-158">웹 모듈은 BuildLabel 노드에서 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="96577-159">프로젝트에 이 파일을 포함하고 솔루션 탐색기에서 항상 복사 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="96577-160">[ASP.NET] MSBuild에서 BuildInfo.config를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="96577-161">이 작업을 수행하려면 `.csproj` 파일에 몇 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="96577-162">그러면 *yourProjectName*.BuildInfo.config 파일이 생성됩니다. 게시 프로세스의 이름이 BuildInfo.config로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="96577-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="96577-163">Visual Studio를 사용하여 빌드할때 빌드 레이블에는 자리 표시자(AutoGen_...)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="96577-164">MSBuild로 빌드할 때는 정확한 버전 번호가 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="96577-165">MSBuild가 버전 번호를 생성하게 하려면 AssemblyReference.cs에서 `1.0.*` 같이 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="96577-166">버전 및 릴리스 추적</span><span class="sxs-lookup"><span data-stu-id="96577-166">Version and release tracking</span></span>
<span data-ttu-id="96577-167">응용 프로그램 버전을 추적하려면 `buildinfo.config`가 Microsoft Build Engine 프로세스에 의해 생성되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="96577-168">.csproj 파일에서 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="96577-169">빌드 정보가 있는 경우 Application Insights 웹 모듈에서 원격 분석의 모든 항목에 **응용 프로그램 버전** 을 속성으로 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="96577-170">이렇게 하면 [진단 검색](app-insights-diagnostic-search.md)을 수행하거나 [메트릭을 탐색](app-insights-metrics-explorer.md)할 때 버전을 기준으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96577-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="96577-171">그러나 빌드 버전 번호는 Visual Studio의 개발자 빌드가 아니라 Microsoft Build Engine에서만 생성된다는 점에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96577-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="96577-172">릴리스 주석</span><span class="sxs-lookup"><span data-stu-id="96577-172">Release annotations</span></span>
<span data-ttu-id="96577-173">Visual Studio Team Services를 사용하는 경우 새 버전을 릴리스할 때마다 [주석 표식](app-insights-annotations.md)이 차트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="96577-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="96577-174">다음 이미지는 이러한 표식이 어떻게 나타나는지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="96577-174">The following image shows how this marker appears.</span></span>

![차트의 샘플 릴리스 주석 스크린샷](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="96577-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96577-176">Next steps</span></span>

* [<span data-ttu-id="96577-177">여러 역할에 대한 공유 리소스</span><span class="sxs-lookup"><span data-stu-id="96577-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="96577-178">A|B 변형을 구분하는 원격 분석 이니셜라이저 만들기</span><span class="sxs-lookup"><span data-stu-id="96577-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
