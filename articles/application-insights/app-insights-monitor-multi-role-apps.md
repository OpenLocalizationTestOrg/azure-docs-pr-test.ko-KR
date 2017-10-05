---
title: "여러 구성 요소, 마이크로 서비스 및 컨테이너에 대한 Azure Application Insights 지원 | Microsoft Docs"
description: "여러 구성 요소 또는 역할로 이루어진 앱에서 성능 및 사용량을 모니터링합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="9742c-103">Application Insights(미리 보기)로 다중 구성 요소 응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="9742c-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="9742c-104">[Azure Application Insights](app-insights-overview.md)에서는 여러 서버 구성 요소, 역할 또는 서비스로 이루어진 앱을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="9742c-105">구성 요소 및 이들 간의 관계의 상태는 단일 Application Map에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="9742c-106">자동 HTTP 상관 관계가 있는 여러 구성 요소를 통해 개별 작업을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="9742c-107">컨테이너 진단을 응용 프로그램 원격 분석과 통합하고 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="9742c-108">응용 프로그램의 모든 구성 요소에 대해 단일 Application Insights 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![다중 구성 요소 응용 프로그램 맵](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="9742c-110">여기서 '구성 요소'는 큰 응용 프로그램의 작동하는 모든 부분을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="9742c-111">예를 들어 일반적인 비즈니스 응용 프로그램은 웹 브라우저에서 실행하는 클라이언트 코드로 구성되며 하나 이상의 웹앱 서비스와 통신하고 백 엔드 서비스를 차례로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="9742c-112">서버 구성 요소는 클라우드에서 온-프레미스에 호스트되거나 Azure 웹 및 작업자 역할이 될 수 있으며 Docker 또는 Service Fabric과 같은 컨테이너에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="9742c-113">단일 Application Insights 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="9742c-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="9742c-114">여기에서 핵심 기술은 응용 프로그램의 모든 구성 요소에서 동일한 Application Insights 리소스로 원격 분석을 보내되, 필요한 경우 구성 요소를 구분하기 위해 `cloud_RoleName` 속성을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="9742c-115">Application Insights SDK는 원격 분석 구성 요소 내보내기에 `cloud_RoleName` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="9742c-116">예를 들어 이 SDK는 `cloud_RoleName` 속성에 웹 사이트 이름 또는 서비스 역할 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="9742c-117">이 값은 원격 분석 이니셜라이저(telemetryinitializer)를 통해 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="9742c-118">Application Map에서는 `cloud_RoleName` 속성을 사용하여 맵에 있는 구성 요소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="9742c-119">`cloud_RoleName` 속성을 재정의하는 방법에 대한 자세한 내용은 [속성 추가: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9742c-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="9742c-120">경우에 따라 이것이 적합하지 않을 수 있으며 구성 요소 그룹마다 별도의 리소스를 사용하는 것이 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="9742c-121">예를 들어, 관리 또는 청구 목적으로 서로 다른 리소스를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="9742c-122">별도의 리소스를 사용한다는 것은 모든 구성 요소가 단일 Application Map에 표시되지 않으며 [분석](app-insights-analytics.md)에서 구성 요소 간에 쿼리할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9742c-123">또한 별도의 리소스도 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="9742c-124">이 내용을 염두에 두고, 이 문서의 나머지 부분에서는 여러 구성 요소의 데이터를 하나의 Application Insights 리소스로 보내려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="9742c-125">다중 구성 요소 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="9742c-125">Configure multi-component applications</span></span>

<span data-ttu-id="9742c-126">다중 구성 요소 Application Map을 얻으려면 다음과 같은 목표를 달성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="9742c-127">응용 프로그램의 각 구성 요소에 Application Insights 패키지의 **최신 시험판을 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="9742c-128">응용 프로그램의 모든 구성 요소에 대해 **단일 Application Insights 리소스를 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="9742c-129">미리 보기 블레이드에서 **다중 역할 Application Map을 활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="9742c-130">해당 형식에 적절한 방법을 사용하여 응용 프로그램의 각 구성 요소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="9742c-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="9742c-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="9742c-132">1. 최신 시험판 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="9742c-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="9742c-133">각 서버 구성 요소에 대한 프로젝트에서 Appication Insights 패키지를 업데이트하거나 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="9742c-134">Visual Studio를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="9742c-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="9742c-135">프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="9742c-136">**시험판 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="9742c-137">Application Insights 패키지가 업데이트에 표시되면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="9742c-138">그렇지 않으면 해당 패키지를 찾아 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="9742c-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9742c-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="9742c-140">Microsoft.ApplicationInsights.ServiceFabric - 게스트 실행 파일로 실행되는 구성 요소 및 Service Fabric 응용 프로그램에서 실행되는 Docker 컨테이너의 경우</span><span class="sxs-lookup"><span data-stu-id="9742c-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="9742c-141">Microsoft.ApplicationInsights.ServiceFabric.Native - ServiceFabric 응용 프로그램에서 Reliable Services의 경우</span><span class="sxs-lookup"><span data-stu-id="9742c-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="9742c-142">Microsoft.ApplicationInsights.Kubernetes - Kubernetes의 Docker에서 실행되는 구성 요소의 경우</span><span class="sxs-lookup"><span data-stu-id="9742c-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="9742c-143">2. 단일 Application Insights 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="9742c-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="9742c-144">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights 구성** 또는 **Application Insights > 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="9742c-145">첫 번째 프로젝트의 경우 마법사를 사용하여 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="9742c-146">후속 프로젝트에 대해 동일한 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="9742c-147">Application Insights 메뉴가 없는 경우 수동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="9742c-148">[Azure Portal](https://portal,azure.com)에서 다른 구성 요소에 대해 이미 만든 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="9742c-149">개요 블레이드에서 Essentials 드롭다운 탭을 열고 **계측 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="9742c-150">프로젝트에서 ApplicationInsights.config를 열고 다음을 삽입합니다. `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="9742c-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![계측 키를 .config 파일에 복사합니다.](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="9742c-152">3. 다중 역할 Application Map 활성화</span><span class="sxs-lookup"><span data-stu-id="9742c-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="9742c-153">Azure Portal에서 응용 프로그램에 대한 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="9742c-154">미리 보기 블레이드에서 *다중 역할 Application Map*을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="9742c-155">4. Docker 메트릭 사용(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="9742c-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="9742c-156">구성 요소가 Azure Windows VM에서 호스트되는 Docker에서 실행되는 경우 컨테이너에서 추가 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="9742c-157">[Azure 진단](../monitoring-and-diagnostics/azure-diagnostics.md) 구성 파일에 다음을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="9742c-158">cloud_RoleName을 사용하여 구성 요소 구분</span><span class="sxs-lookup"><span data-stu-id="9742c-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="9742c-159">`cloud_RoleName` 속성은 모든 원격 분석에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="9742c-160">원격 분석을 시작하는 구성 요소(역할 또는 서비스)를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="9742c-161">(여러 서버 프로세스 또는 컴퓨터에서 동시에 실행되는 동일한 역할을 구분하는 cloud_RoleInstance와 다릅니다.)</span><span class="sxs-lookup"><span data-stu-id="9742c-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="9742c-162">포털에서 이 속성을 사용하여 원격 분석을 필터 또는 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="9742c-163">이 예제에서는 CRM API 백 엔드에서 실패를 필터링하여 프런트 엔드 웹 서비스의 정보만 표시하도록 실패 블레이드가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![클라우드 역할 이름에 따라 분할된 메트릭 차트](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="9742c-165">구성 요소 간 추적 작업</span><span class="sxs-lookup"><span data-stu-id="9742c-165">Trace operations between components</span></span>

<span data-ttu-id="9742c-166">개별 작업을 처리하는 동안 한 구성 요소에서 다른 구성 요소로의 호출을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![작업에 대한 원격 분석 표시](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="9742c-168">프론트 엔드 웹 서버와 백 엔드 API 간에 이 작업에 대해 상관 관계가 지정된 원격 분석 목록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9742c-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![구성 요소 검색](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="9742c-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9742c-170">Next steps</span></span>

* [<span data-ttu-id="9742c-171">개발, 테스트 및 프로덕션의 원격 분석 구분</span><span class="sxs-lookup"><span data-stu-id="9742c-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
