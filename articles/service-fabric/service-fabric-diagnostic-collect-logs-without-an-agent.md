---
title: "aaaCollect 로그 직접 Azure 서비스 패브릭에서 서비스 프로세스 | Microsoft Azure"
description: "서비스 패브릭 tooa 중앙 위치 또는 같은 Azure Application Insights Elasticsearch를 Azure 진단 에이전트가에 의존 하지 않고 직접 응용 프로그램 로그를 보낼 수에 대해 설명 합니다."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="9d354-103">Azure Service Fabric 서비스 프로세스에서 직접 로그 수집 </span><span class="sxs-lookup"><span data-stu-id="9d354-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="9d354-104">프로세스에서 로그 수집</span><span class="sxs-lookup"><span data-stu-id="9d354-104">In-process log collection</span></span>
<span data-ttu-id="9d354-105">사용 하 여 로그 응용 프로그램을 수집 [Azure 진단 확장](service-fabric-diagnostics-how-to-setup-wad.md) 에 적합 한 옵션은 **Azure 서비스 패브릭** 서비스 로그 원본과 대상의 hello 집합이 작으면 바뀌지 않으면 간격과 있습니다 hello 원본과 대상 사이 간단 하 게 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="9d354-106">그렇지 않은 경우는 대체 항목은 toohave 서비스 로그를 직접 tooa 중앙 위치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="9d354-107">이 프로세스를 **프로세스에서 로그 수집**이라고 하며 다음과 같은 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="9d354-108">*쉬운 구성 및 배포*</span><span class="sxs-lookup"><span data-stu-id="9d354-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="9d354-109">진단 데이터 수집의 hello 구성은 hello 서비스 구성의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="9d354-110">것 hello 응용 프로그램의 놓을 것 "동기화" hello로 쉽게 tooalways 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="9d354-111">응용 프로그램당 또는 서비스당 구성은 쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="9d354-112">로그 에이전트 기반 컬렉션에는 일반적으로 별도 배포 및 추가 관리 작업 및 오류의 잠재적 소스 hello 진단 에이전트의 구성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="9d354-113">종종 hello 에이전트 당 가상 컴퓨터 (노드) 수의 인스턴스가 하나만 이며 hello 에이전트 구성은 모든 응용 프로그램 및 해당 노드에서 실행 되는 서비스 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="9d354-114">*유연성*</span><span class="sxs-lookup"><span data-stu-id="9d354-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="9d354-115">hello 응용 프로그램 데이터 보낼 수 있습니다 hello toogo, 필요한 경우 항상으로 hello 대상 데이터 저장소 시스템을 지 원하는 수 있는 클라이언트 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="9d354-116">새로운 대상을 원하는 대로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="9d354-117">복잡한 캡처, 필터링 및 데이터 집계 규칙을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="9d354-118">로그 에이전트 기반 컬렉션 에이전트 지원 hello hello 데이터 싱크에 의해 종종 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="9d354-119">일부 에이전트는 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-119">Some agents are extensible.</span></span>

* <span data-ttu-id="9d354-120">*액세스 toointernal 응용 프로그램 데이터와 컨텍스트*</span><span class="sxs-lookup"><span data-stu-id="9d354-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="9d354-121">hello 진단 하위 시스템 hello 응용 프로그램/서비스 프로세스 내에서 실행 컨텍스트 정보를 사용 하 여 hello 추적을 쉽게 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="9d354-122">로그 에이전트 기반 컬렉션에 hello 데이터 전송 해야 tooan 에이전트 일부 프로세스 간 통신 메커니즘을 통해 Windows 용 이벤트 추적 등입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="9d354-123">이 메커니즘에 따라 추가 제한 사항이 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="9d354-124">되 가능한 toocombine 두 컬렉션 방법의 이점을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="9d354-125">실제로 대부분의 응용 프로그램에 대 한 최상의 솔루션 hello 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="9d354-126">에이전트 기반 컬렉션에는 로그 관련된 toohello 전체 클러스터 및 개별 클러스터 노드를 수집 하기 위한 자연 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="9d354-127">처리 중인 로그 수집, toodiagnose 서비스 시작 문제 및 크래시 보다 훨씬 더 신뢰할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="9d354-128">또한, 서비스 패브릭 클러스터 내에서 실행 되는 많은 서비스에서 자체 프로세스에서 로그 수집을 수행 하는 각 서비스 hello 클러스터에서 많은 나가는 연결에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="9d354-129">Hello 네트워크 하위 시스템 및 hello 로그 대상에 대 한 많은 수의 보내는 연결 읽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="9d354-130">[**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) 같은 에이전트는 여러 서비스로부터 데이터를 수집하고 몇 번의 연결을 통해 모든 데이터를 보내므로 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="9d354-131">이 문서에서는 tooset in process를 사용 하 여 컬렉션에서 로그 방법은 보여줍니다 [ **EventFlow 오픈 소스 라이브러리**](https://github.com/Azure/diagnostics-eventflow)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="9d354-132">다른 라이브러리를 사용할 수 있습니다 hello에 대 한 동일한 목적으로 있지만 EventFlow 이점이 hello 프로세스에서 로그 수집 및 toosupport 서비스 패브릭 서비스에 대 한 디자인 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="9d354-133">사용 하 여 [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) hello 로그 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="9d354-134">[**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) 또는 [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) 같은 다른 대상도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="9d354-135">방금 적절 한 NuGet 패키지를 설치 하 고 hello 대상 hello EventFlow 구성 파일에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="9d354-136">Application Insights 이외의 로그 대상에 대한 자세한 내용은 [EventFlow 설명서](https://github.com/Azure/diagnostics-eventflow)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d354-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="9d354-137">EventFlow 라이브러리 tooa 서비스 패브릭 서비스 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="9d354-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="9d354-138">EventFlow 이진을 NuGet 패키지 집합으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="9d354-139">tooadd EventFlow tooa 서비스 패브릭 서비스 프로젝트 hello 솔루션 탐색기에서에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 "관리 NuGet 패키지입니다."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="9d354-140">Toohello "찾아보기" 탭과 검색에 대 한 전환 "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="9d354-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 패키지 관리자 UI에서 EventFlow NuGet 패키지][1]

<span data-ttu-id="9d354-142">hello 서비스 EventFlow 호스팅 hello 원본과 hello 응용 프로그램 로그에 대 한 대상에 따라 적절 한 패키지를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="9d354-143">Hello 다음 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="9d354-144">(toocapture 데이터와 같은 표준 EventSources 및 hello 서비스 EventSource 클래스에서 *ServiceFabric 조항을* 및 *Microsoft-ServiceFabric 행위자*)</span><span class="sxs-lookup"><span data-stu-id="9d354-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="9d354-145">(하겠습니다 toosend hello 로그 tooan Azure Application Insights 리소스)</span><span class="sxs-lookup"><span data-stu-id="9d354-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="9d354-146">(서비스 패브릭 서비스 구성에서 hello EventFlow 파이프라인의 초기화를 사용 하도록 설정 및 진단 데이터 서비스 패브릭 상태 보고서 변수로 전송 된 모든 문제를 보고)</span><span class="sxs-lookup"><span data-stu-id="9d354-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="9d354-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`패키지에 필요한 hello 서비스 프로젝트 tootarget.NET Framework 4.6 이상.</span><span class="sxs-lookup"><span data-stu-id="9d354-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="9d354-148">프로젝트 속성에서이 패키지를 설치 하기 전에 hello 적절 한 대상 프레임 워크를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="9d354-149">결국 hello 패키지가 설치 되어, hello 다음 단계 tooconfigure는이 고 EventFlow hello 서비스에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="9d354-150">로그 수집 구성 및 사용</span><span class="sxs-lookup"><span data-stu-id="9d354-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="9d354-151">Hello 로그 전송 EventFlow 파이프라인 구성 파일에 저장 하는 사양에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="9d354-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`패키지는 시작 EventFlow 구성 파일을 `PackageRoot\Config` 솔루션 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="9d354-153">hello 파일 이름은 `eventFlowConfig.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="9d354-154">이 구성 파일 수정 toobe toocapture가에서 데이터가 필요한 hello 기본 서비스 `EventSource` 클래스 및 데이터 tooApplication Insights 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="9d354-155">에 익숙한 가정 **Azure Application Insights** 서비스 및 계획 toouse toomonitor 서비스 패브릭 서비스는 Application Insights 리소스를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="9d354-156">자세한 내용은 [Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d354-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="9d354-157">열기 hello `eventFlowConfig.json` hello 편집기에서 파일을 아래와 같이 해당 콘텐츠를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="9d354-158">있는지 tooreplace hello ServiceEventSource 이름 및 toocomments에 따라 Application Insights 계측 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="9d354-159">서비스의 ServiceEventSource의 hello 이름이 hello hello의 Name 속성의 hello 값 `EventSourceAttribute` toohello ServiceEventSource 클래스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="9d354-160">모두에 지정 된 hello `ServiceEventSource.cs` hello 서비스 코드에 포함 되어 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="9d354-161">예를 들어 hello에 다음 코드 조각 hello hello ServiceEventSource 이름은 *MyCompany-응용 프로그램 1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="9d354-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="9d354-162">`eventFlowConfig.json` 파일은 서비스 구성 패키지의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="9d354-163">변경 toothis 파일 hello 서비스의 전체 또는 구성-전용 업그레이드에 포함 될 수 이므로 주체 tooService Fabric 업그레이드 상태 검사 및 자동 롤백 업그레이드에 실패할 경우.</span><span class="sxs-lookup"><span data-stu-id="9d354-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="9d354-164">자세한 내용은 [Service Fabric 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d354-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="9d354-165">hello 마지막 단계는 tooinstantiate EventFlow 파이프라인에 있는 서비스의 시작 코드에 `Program.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="9d354-166">Hello에서 다음 예제에서는 EventFlow 관련 항목이 추가 주석으로 표시 됩니다 `****`:</span><span class="sxs-lookup"><span data-stu-id="9d354-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="9d354-167">hello 이름이 hello의 hello 매개 변수로 전달 `CreatePipeline` hello 방식의 `ServiceFabricDiagnosticsPipelineFactory` hello의 hello 이름인 *상태 엔터티* hello EventFlow 로그 컬렉션 파이프라인을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="9d354-168">EventFlow 발생 한 경우이 이름을 사용 및 오류 hello 서비스 패브릭 상태 하위 시스템을 통해 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="9d354-169">확인</span><span class="sxs-lookup"><span data-stu-id="9d354-169">Verification</span></span>
<span data-ttu-id="9d354-170">서비스를 시작 하 고 디버그 hello 관찰 Visual Studio의 출력 창.</span><span class="sxs-lookup"><span data-stu-id="9d354-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="9d354-171">Hello 서비스를 시작한 후 서비스에서 "Application Insights 원격 분석" 레코드를 보내면 증거 표시를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="9d354-172">웹 브라우저를 열고 이동 tooyour Application Insights 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="9d354-173">(Hello 기본 "개요" 블레이드 맨 위 hello)에서 "검색" 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="9d354-174">짧은 지연 후 hello Application Insights 포털에서 추적을 표시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d354-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Service Fabric 응용 프로그램 로그를 표시하는 Application Insights 포털 ][2]

## <a name="next-steps"></a><span data-ttu-id="9d354-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d354-176">Next steps</span></span>
* [<span data-ttu-id="9d354-177">서비스 패브릭 서비스 진단 및 모니터링에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9d354-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="9d354-178">EventFlow 설명서</span><span class="sxs-lookup"><span data-stu-id="9d354-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
