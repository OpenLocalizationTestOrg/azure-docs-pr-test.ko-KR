---
title: "여러 구성 요소, microservices, 및 컨테이너에 대 한 aaaAzure Application Insights 지원 | Microsoft Docs"
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
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="2bcc0-103">Application Insights(미리 보기)로 다중 구성 요소 응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="2bcc0-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="2bcc0-104">[Azure Application Insights](app-insights-overview.md)에서는 여러 서버 구성 요소, 역할 또는 서비스로 이루어진 앱을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2bcc0-105">hello 구성 요소 및 이들 간의 관계 hello hello 상태는 단일 응용 프로그램 지도에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="2bcc0-106">자동 HTTP 상관 관계가 있는 여러 구성 요소를 통해 개별 작업을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="2bcc0-107">컨테이너 진단을 응용 프로그램 원격 분석과 통합하고 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="2bcc0-108">응용 프로그램의 모든 hello 구성 요소에 대 한 단일 Application Insights 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![다중 구성 요소 응용 프로그램 맵](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="2bcc0-110">'구성 요소' 사용 하 여 여기서 toomean 대형 응용 프로그램의 모든 작동 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="2bcc0-111">예를 들어 tooone 통신의 대상이 되는 웹 브라우저에서 실행 되는 클라이언트 코드는 일반적인 비즈니스 응용 프로그램 구성 될 수 있습니다 또는 사용 하 여 다시는 더 많은 웹 응용 프로그램 서비스 서비스를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="2bcc0-112">서버 구성 요소 호스트 된 온-프레미스에 hello 클라우드 또는 Azure 웹 및 작업자 역할 수 있습니다 중이거나 Docker 또는 서비스 패브릭와 같은 컨테이너에서 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="2bcc0-113">단일 Application Insights 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="2bcc0-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="2bcc0-114">hello 핵심 기술은 여기 toosend 원격 분석이 응용 프로그램 toohello의 모든 구성 요소에서 사용 하 여 hello 있지만 같은 Application Insights 리소스 `cloud_RoleName` 필요한 경우 속성 toodistinguish 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="2bcc0-115">hello Application Insights SDK 추가 hello `cloud_RoleName` 속성 toohello 원격 분석 구성 요소에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="2bcc0-116">웹 사이트 이름 또는 서비스 역할 이름 toohello hello SDK 예를 들어 추가할 `cloud_RoleName` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="2bcc0-117">이 값은 원격 분석 이니셜라이저(telemetryinitializer)를 통해 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="2bcc0-118">응용 프로그램 맵 hello hello를 사용 하 여 `cloud_RoleName` hello 맵에 tooidentify hello 구성 요소 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="2bcc0-119">수행 방법에 대 한 자세한 내용은 hello 재정의 `cloud_RoleName` 속성 참조 [속성 추가: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="2bcc0-120">경우에 따라 적절 하 게 수 있으며 toouse 다양 한 구성 요소 그룹에 대 한 별도 리소스를 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="2bcc0-121">예를 들어, 관리 또는 청구 목적을 위한 toouse 다양 한 리소스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="2bcc0-122">별도 리소스를 사용 하 여 단일 응용 프로그램 맵을;에 표시 되는 모든 hello 구성 요소를 표시 되지 않는 의미 및에서 구성 요소에서 쿼리할 수 없는 [분석](app-insights-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="2bcc0-123">Tooset hello 별도 리소스를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="2bcc0-124">해당 다 경고와 함께에서는 hello이이 문서의 나머지 부분에서 여러 구성 요소 tooone Application Insights 리소스에서에서 toosend 데이터 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="2bcc0-125">다중 구성 요소 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="2bcc0-125">Configure multi-component applications</span></span>

<span data-ttu-id="2bcc0-126">tooget 다중 구성 요소는 응용 프로그램 매핑 tooachieve 이러한 목표를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="2bcc0-127">**Hello 최신 시험판 설치** hello 응용 프로그램의 각 구성 요소에서 Application Insights 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="2bcc0-128">**단일 Application Insights 리소스를 공유** 모든 hello 응용 프로그램 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="2bcc0-129">**다중 역할 응용 프로그램 맵 활성화** hello 미리 보기 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="2bcc0-130">Hello 적절 한 메서드를 사용 하 여 해당 형식에 대 한 응용 프로그램의 각 구성 요소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="2bcc0-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="2bcc0-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="2bcc0-132">1. Hello 최신 시험판 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="2bcc0-133">업데이트 하거나 각 서버 구성 요소에 대 한 hello 프로젝트에서 hello Insights 응용 프로그램 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="2bcc0-134">Visual Studio를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="2bcc0-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="2bcc0-135">프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="2bcc0-136">**시험판 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="2bcc0-137">Application Insights 패키지가 업데이트에 표시되면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="2bcc0-138">그렇지 않으면 찾아보기 및 hello 적절 한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="2bcc0-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="2bcc0-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="2bcc0-140">Microsoft.ApplicationInsights.ServiceFabric - 게스트 실행 파일로 실행되는 구성 요소 및 Service Fabric 응용 프로그램에서 실행되는 Docker 컨테이너의 경우</span><span class="sxs-lookup"><span data-stu-id="2bcc0-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="2bcc0-141">Microsoft.ApplicationInsights.ServiceFabric.Native - ServiceFabric 응용 프로그램에서 Reliable Services의 경우</span><span class="sxs-lookup"><span data-stu-id="2bcc0-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="2bcc0-142">Microsoft.ApplicationInsights.Kubernetes - Kubernetes의 Docker에서 실행되는 구성 요소의 경우</span><span class="sxs-lookup"><span data-stu-id="2bcc0-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="2bcc0-143">2. 단일 Application Insights 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="2bcc0-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="2bcc0-144">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights 구성** 또는 **Application Insights > 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="2bcc0-145">Hello 첫 번째 프로젝트에 대 한 hello 마법사 toocreate Application Insights 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="2bcc0-146">후속 프로젝트에 대 한 선택 hello 동일한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="2bcc0-147">Application Insights 메뉴가 없는 경우 수동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="2bcc0-148">[Azure 포털](https://portal,azure.com)를 이미 다른 구성 요소에 대해 만든 hello Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="2bcc0-149">Hello 개요 블레이드에, 열기 hello Essentials 드롭 다운 탭 및 복사 hello **계측 키입니다.**</span><span class="sxs-lookup"><span data-stu-id="2bcc0-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="2bcc0-150">프로젝트에서 ApplicationInsights.config를 열고 다음을 삽입합니다. `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="2bcc0-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Hello 계측 키 toohello.config 파일을 복사 합니다.](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="2bcc0-152">3. 다중 역할 Application Map 활성화</span><span class="sxs-lookup"><span data-stu-id="2bcc0-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="2bcc0-153">Hello Azure 포털에서에서 응용 프로그램에 대 한 hello 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="2bcc0-154">사용 하도록 설정 hello 미리 보기 블레이드에서 *다중 역할 응용 프로그램 맵*합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="2bcc0-155">4. Docker 메트릭 사용(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="2bcc0-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="2bcc0-156">구성 요소 Windows Azure VM에서 호스트 되는 Docker를 실행 하는 경우 hello 컨테이너에서 추적을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="2bcc0-157">[Azure 진단](../monitoring-and-diagnostics/azure-diagnostics.md) 구성 파일에 다음을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="2bcc0-158">Cloud_RoleName tooseparate 구성 요소를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2bcc0-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="2bcc0-159">hello `cloud_RoleName` 속성은 연결 된 tooall 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="2bcc0-160">-Hello 역할 또는 서비스-hello 원격 분석을 시작 하는 hello 구성 요소를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="2bcc0-161">(이 하지으로 여러 서버 프로세스 또는 컴퓨터에 병렬로 실행 되는 동일한 역할을 구분 하는 cloud_RoleInstance hello 동일 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2bcc0-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="2bcc0-162">Hello 포털에서 필터링 하거나이 속성을 사용 하 여 원격 분석을 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="2bcc0-163">이 예제에서는 hello 오류 블레이드는 hello CRM API 백 엔드에서 오류를 필터링 hello 프런트 엔드 웹 서비스에서 필터링 된 tooshow 정당한 정보:</span><span class="sxs-lookup"><span data-stu-id="2bcc0-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![클라우드 역할 이름에 따라 분할된 메트릭 차트](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="2bcc0-165">구성 요소 간 추적 작업</span><span class="sxs-lookup"><span data-stu-id="2bcc0-165">Trace operations between components</span></span>

<span data-ttu-id="2bcc0-166">구성 요소를 하나 tooanother, 개별 작업을 처리 하는 동안 hello 호출에서에서 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![작업에 대한 원격 분석 표시](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="2bcc0-168">Hello 프런트 엔드 웹 서버와 백 엔드 API hello 전반에서이 작업에 대 한 원격 분석의 tooa 상관 관계가 지정 된 목록에서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bcc0-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![구성 요소 검색](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="2bcc0-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2bcc0-170">Next steps</span></span>

* [<span data-ttu-id="2bcc0-171">개발, 테스트 및 프로덕션의 원격 분석 구분</span><span class="sxs-lookup"><span data-stu-id="2bcc0-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
