---
title: "Azure Service Fabric 서비스 프로세스에서 직접 로그 수집 | Microsoft Azure"
description: "Service Fabric 응용 프로그램이 Azure Diagnostics 에이전트 없이도 Azure Application Insights 또는 Elasticsearch 등의 중앙 위치에 직접 로그를 보낼 수 있음을 설명합니다."
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
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="7b186-103">Azure Service Fabric 서비스 프로세스에서 직접 로그 수집 </span><span class="sxs-lookup"><span data-stu-id="7b186-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="7b186-104">프로세스에서 로그 수집</span><span class="sxs-lookup"><span data-stu-id="7b186-104">In-process log collection</span></span>
<span data-ttu-id="7b186-105">로그 원본과 대상의 집합이 작고, 자주 변경되지 않으며, 원본과 대상 간의 매핑이 단순하다면 [Azure Diagnostics 확장](service-fabric-diagnostics-how-to-setup-wad.md)을 사용한 응용 프로그램 로그 수집이 **Azure Service Fabric** 서비스에 좋은 옵션입니다. </span><span class="sxs-lookup"><span data-stu-id="7b186-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="7b186-106">그렇지 않은 경우 서비스가 중앙 위치에 직접 로그를 보내도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="7b186-107">이 프로세스를 **프로세스에서 로그 수집**이라고 하며 다음과 같은 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="7b186-108">*쉬운 구성 및 배포*</span><span class="sxs-lookup"><span data-stu-id="7b186-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="7b186-109">진단 데이터 수집 구성이 서비스 구성의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="7b186-110">응용 프로그램 나머지와 항상 "동기화" 상태로 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="7b186-111">응용 프로그램당 또는 서비스당 구성은 쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="7b186-112">에이전트 기반 로그 수집이 일반적으로 추가 관리 작업 및 잠재적인 오류 소스인 진단 에이전트의 별도 배포 및 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="7b186-113">종종 가상 컴퓨터(노드)당 하나의 에이전트 인스턴스만 허용되며, 해당 노드에서 실행 중인 모든 응용 프로그램과 서비스 간에 에이전트 구성을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="7b186-114">*유연성*</span><span class="sxs-lookup"><span data-stu-id="7b186-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="7b186-115">응용 프로그램은 대상 데이터 저장소 시스템을 지원하는 클라이언트 라이브러리가 있는 한 데이터를 필요한 어느 곳이든 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="7b186-116">새로운 대상을 원하는 대로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="7b186-117">복잡한 캡처, 필터링 및 데이터 집계 규칙을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="7b186-118">에이전트 기반 로그 수집은 종종 에이전트가 지원하는 데이터 싱크에 의해 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="7b186-119">일부 에이전트는 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-119">Some agents are extensible.</span></span>

* <span data-ttu-id="7b186-120">*내부 응용 프로그램 데이터 및 컨텍스트에 대한 액세스*</span><span class="sxs-lookup"><span data-stu-id="7b186-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="7b186-121">응용 프로그램/서비스 프로세스 내에서 실행되는 진단 하위 시스템은 컨텍스트 정보와 함께 추적을 쉽게 보강할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="7b186-122">에이전트 기반 로그 수집에서 ETW(Windows용 이벤트 추적)와 같은 일부 프로세스간 통신 메커니즘을 통해 에이전트에 데이터를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="7b186-123">이 메커니즘에 따라 추가 제한 사항이 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="7b186-124">두 가지 수집 방법을 결합하여 양쪽의 이점을 누릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="7b186-125">실제로 많은 응용 프로그램에는 이 방법이 최적의 솔루션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="7b186-126">에이전트 기반 수집은 전체 클러스터와 개별 클러스터 노드와 관련한 로그를 수집하기 위한 자연스러운 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="7b186-127">프로세스에서 로그 수집보다 훨씬 안정적으로 서비스 시작 문제와 충돌을 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="7b186-128">또한 Service Fabric 클러스터 안에서 실행되는 많은 서비스에서는 자체적으로 프로세스에서 로그 수집을 수행하는 각 서비스로 인해 클러스터로부터 나가는 연결이 매우 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="7b186-129">나가는 연결이 많으면 네트워크 하위 시스템과 로그 대상 모두에 부담이 초래됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="7b186-130">[**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) 같은 에이전트는 여러 서비스로부터 데이터를 수집하고 몇 번의 연결을 통해 모든 데이터를 보내므로 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="7b186-131">이 문서에서는 [**EventFlow 오픈 소스 라이브러리**](https://github.com/Azure/diagnostics-eventflow)를 사용하여 프로세스에서 로그 수집을 설정하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="7b186-132">같은 용도로 다른 라이브러리를 사용할 수도 있지만 EventFlow에는 Service Fabric 서비스를 지원하고 프로세스에서 로그 수집을 위해 특별히 설계된 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="7b186-133">[**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/)를 로그 대상으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="7b186-134">[**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) 또는 [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) 같은 다른 대상도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="7b186-135">EventFlow 구성 파일에서 적합한 NuGet 패키지를 설치하고 대상을 구성하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="7b186-136">Application Insights 이외의 로그 대상에 대한 자세한 내용은 [EventFlow 설명서](https://github.com/Azure/diagnostics-eventflow)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b186-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="7b186-137">Service Fabric 서비스 프로젝트에 EventFlow 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="7b186-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="7b186-138">EventFlow 이진을 NuGet 패키지 집합으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="7b186-139">EventFlow를 Service Fabric 서비스 프로젝트에 추가하려면 Solution Explorer에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 “NuGet 패키지 관리”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="7b186-140">"찾아보기" 탭으로 전환하고 "`Diagnostics.EventFlow`"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 패키지 관리자 UI에서 EventFlow NuGet 패키지][1]

<span data-ttu-id="7b186-142">EventFlow를 호스팅하는 서비스는 응용 프로그램 로그에 대해 원본과 대상에 따라 적합한 패키지를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="7b186-143">다음 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="7b186-144">(서비스의 EventSource 클래스 및 표준 EventSources에서 데이터 캡처, 예: *Microsoft-ServiceFabric-Services* 및 *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="7b186-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="7b186-145">(여기서는 Azure Application Insights 리소스에 로그를 보낼 것임)</span><span class="sxs-lookup"><span data-stu-id="7b186-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="7b186-146">(Service Fabric 서비스 구성에서 EventFlow 파이프라인의 초기화를 활성화하고 진단 데이터를 Service Fabric 상태 보고서로 보내 모든 문제를 보고)</span><span class="sxs-lookup"><span data-stu-id="7b186-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="7b186-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 패키지에서는 서비스 프로젝트가 .NET Framework 4.6 이상을 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="7b186-148">이 패키지를 설치하기 전에 프로젝트 속성에서 적합한 대상 프레임워크를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="7b186-149">모든 패키지를 설치한 다음에는 서비스에서 EventFlow를 구성하여 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="7b186-150">로그 수집 구성 및 사용</span><span class="sxs-lookup"><span data-stu-id="7b186-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="7b186-151">로그 보내기를 담당하는 EventFlow 파이프라인은 구성 파일에 저장된 사양으로부터 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="7b186-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`패키지는 시작 EventFlow 구성 파일을 `PackageRoot\Config` 솔루션 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="7b186-153">이 파일 이름은 `eventFlowConfig.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="7b186-154">기본 서비스 `EventSource` 클래스에서 데이터를 수집하고 Application Insights 서비스로 데이터를 보내기 위해 이 구성 파일을 수정해야 합니다. </span><span class="sxs-lookup"><span data-stu-id="7b186-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="7b186-155">여기서는 사용자가 **Azure Application Insights** 서비스에 대해 잘 알고 있고 Service Fabric 서비스의 모니터링에 사용할 Application Insights 리소스가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="7b186-156">자세한 내용은 [Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b186-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="7b186-157">편집기에서 `eventFlowConfig.json` 파일을 열고 다음과 같이 콘텐츠를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="7b186-158">주석에 따라 ServiceEventSource 이름 및 Application Insights 계측 키를 변경합니다. </span><span class="sxs-lookup"><span data-stu-id="7b186-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="7b186-159">서비스의 ServiceEventSource 이름은ServiceEventSource 클래스에 적용된 `EventSourceAttribute`의 Name 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="7b186-160">모두 `ServiceEventSource.cs` 파일에서 지정하며 서비스 코드의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="7b186-161">예를 들어 다음 코드 조각에서 ServiceEventSource의 이름은 *MyCompany-Application1-Stateless1*입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="7b186-162">`eventFlowConfig.json` 파일은 서비스 구성 패키지의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="7b186-163">이 파일에 대한 변경 사항은 서비스의 전체 또는 구성 전용 업그레이드에 포함될 수 있습니다. 업그레이드 실패 시 Service Fabric 업그레이드 상태 확인과 자동 롤백의 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="7b186-164">자세한 내용은 [Service Fabric 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b186-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="7b186-165">마지막 단계는 `Program.cs` 파일에 있는 서비스 시작 코드에서 EventFlow 파이프라인을 인스턴스화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="7b186-166">다음 예제에서는 EventFlow 관련 추가 `****`로 시작하는 주석으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="7b186-167">`ServiceFabricDiagnosticsPipelineFactory`의 `CreatePipeline` 메서드 매개 변수 형태로 전달되는 이름은 EventFlow 로그 수집 파이프라인을 나타내는 *상태 개체*의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="7b186-168">EventFlow에서 오류가 발생하고 Service Fabric 상태 하위 시스템을 통해 보고할 경우 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="7b186-169">확인</span><span class="sxs-lookup"><span data-stu-id="7b186-169">Verification</span></span>
<span data-ttu-id="7b186-170">서비스를 시작하고 Visual Studio의 출력 창에서 디버그를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="7b186-171">서비스를 시작한 후 서비스에서 "Application Insights 원격 분석" 레코드를 보내면 증거를 확인하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="7b186-172">웹 브라우저를 열고 Application Insights 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="7b186-173">"검색" 탭(기본 "개요" 블레이드의 맨 위)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="7b186-174">잠깐 지연된 후 Application Insights 포털에서 추적이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b186-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Service Fabric 응용 프로그램 로그를 표시하는 Application Insights 포털 ][2]

## <a name="next-steps"></a><span data-ttu-id="7b186-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b186-176">Next steps</span></span>
* [<span data-ttu-id="7b186-177">서비스 패브릭 서비스 진단 및 모니터링에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7b186-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="7b186-178">EventFlow 설명서</span><span class="sxs-lookup"><span data-stu-id="7b186-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
