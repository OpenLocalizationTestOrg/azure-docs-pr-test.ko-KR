---
title: "EventFlow를 사용하여 Azure Service Fabric 이벤트 집계 | Microsoft Docs"
description: "Azure Service Fabric 클러스터 모니터링 및 진단을 위해 EventFlow를 사용하여 이벤트를 집계 및 수집하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="6483a-103">EventFlow를 사용하여 이벤트 집계 및 수집</span><span class="sxs-lookup"><span data-stu-id="6483a-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="6483a-104">[Microsoft 진단 EventFlow](https://github.com/Azure/diagnostics-eventflow)(영문)는 노드의 이벤트를 하나 이상의 모니터링 대상으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="6483a-105">EventFlow가 서비스 프로젝트에 NuGet 패키지로 포함되어 있어 EventFlow 코드와 구성이 서비스와 함께 이동하므로 Azure 진단에 대해 앞에서 언급한 노드별 구성 문제가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="6483a-106">EventFlow는 서비스 프로세스 내에서 실행되며 구성된 출력에 직접 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="6483a-107">이러한 직접 연결로 인해 EventFlow는 Azure, 컨테이너 및 온-프레미스 서비스 배포에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="6483a-108">각 EventFlow 파이프라인이 외부 연결을 만들기 때문에 컨테이너와 같이 고밀도 시나리오에서 EventFlow를 실행하는 경우 신중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="6483a-109">따라서 여러 프로세스를 호스트하는 경우 몇 가지 아웃바운드 연결이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="6483a-110">이 경우`ServiceType`의 모든 복제본이 동일한 프로세스에서 실행되어 아웃바운드 연결 수를 제한하므로 Service Fabric 응용 프로그램에 별로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="6483a-111">EventFlow는 이벤트 필터링도 제공하므로 지정된 필터와 일치하는 이벤트만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="6483a-112">EventFlow 설정</span><span class="sxs-lookup"><span data-stu-id="6483a-112">Setting up EventFlow</span></span>

<span data-ttu-id="6483a-113">EventFlow 이진을 NuGet 패키지 집합으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="6483a-114">EventFlow를 Service Fabric 서비스 프로젝트에 추가하려면 Solution Explorer에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 “NuGet 패키지 관리”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="6483a-115">"찾아보기" 탭으로 전환하고 "`Diagnostics.EventFlow`"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 패키지 관리자 UI에서 EventFlow NuGet 패키지](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="6483a-117">"입력" 및 "출력" 레이블이 지정된 다양한 패키지 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="6483a-118">EventFlow는 다양한 로깅 공급자 및 분석기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="6483a-119">EventFlow를 호스팅하는 서비스는 응용 프로그램 로그에 대해 원본과 대상에 따라 적합한 패키지를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="6483a-120">핵심 ServiceFabric 패키지 외에도 최소한 하나의 입력 및 출력이 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="6483a-121">예를 들어 다음 패키지를 추가하여 EventSource 이벤트를 Application Insights에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="6483a-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`(서비스의 EventSource 클래스 및 표준 EventSources에서 데이터 캡처, 예: *Microsoft-ServiceFabric-Services* 및 *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="6483a-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="6483a-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(여기서는 Azure Application Insights 리소스에 로그를 보낼 것임)</span><span class="sxs-lookup"><span data-stu-id="6483a-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="6483a-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(Service Fabric 서비스 구성에서 EventFlow 파이프라인의 초기화를 활성화하고 진단 데이터를 Service Fabric 상태 보고서로 보내 모든 문제를 보고)</span><span class="sxs-lookup"><span data-stu-id="6483a-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="6483a-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` 패키지에서는 서비스 프로젝트가 .NET Framework 4.6 이상을 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="6483a-126">이 패키지를 설치하기 전에 프로젝트 속성에서 적합한 대상 프레임워크를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="6483a-127">모든 패키지를 설치한 다음에는 서비스에서 EventFlow를 구성하여 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="6483a-128">로그 수집 구성 및 사용</span><span class="sxs-lookup"><span data-stu-id="6483a-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="6483a-129">로그 보내기를 담당하는 EventFlow 파이프라인은 구성 파일에 저장된 사양으로부터 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="6483a-130">`Microsoft.Diagnostics.EventFlow.ServiceFabric` 패키지는 시작 EventFlow 구성 파일을 `PackageRoot\Config` 솔루션 폴더에 `eventFlowConfig.json` 이름으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="6483a-131">기본 서비스 `EventSource` 클래스 및 구성하려는 다른 입력에서 데이터를 수집하고 적절한 위치로 데이터를 보내도록 이 구성 파일을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="6483a-132">다음은 위에서 언급한 NuGet 패키지를 기반으로 하는 샘플 *eventFlowConfig.json*입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="6483a-133">서비스의 ServiceEventSource 이름은ServiceEventSource 클래스에 적용된 `EventSourceAttribute`의 Name 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="6483a-134">모두 `ServiceEventSource.cs` 파일에서 지정하며 서비스 코드의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="6483a-135">예를 들어 다음 코드 조각에서 ServiceEventSource의 이름은 *MyCompany-Application1-Stateless1*입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="6483a-136">`eventFlowConfig.json` 파일은 서비스 구성 패키지의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="6483a-137">이 파일에 대한 변경 사항은 서비스의 전체 또는 구성 전용 업그레이드에 포함될 수 있습니다. 업그레이드 실패 시 Service Fabric 업그레이드 상태 확인과 자동 롤백의 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="6483a-138">자세한 내용은 [Service Fabric 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6483a-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="6483a-139">구성의 *filters* 섹션을 사용하면 EventFlow 파이프라인을 통해 출력으로 전송하려는 정보를 추가로 사용자 지정하여 특정 정보를 삭제 또는 포함하거나 이벤트 데이터의 구조를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="6483a-140">필터링에 대한 자세한 내용은 [EventFlow 필터](https://github.com/Azure/diagnostics-eventflow#filters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6483a-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="6483a-141">마지막 단계는 `Program.cs` 파일에 있는 서비스 시작 코드에서 EventFlow 파이프라인을 인스턴스화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="6483a-142">`ServiceFabricDiagnosticsPipelineFactory`의 `CreatePipeline` 메서드 매개 변수 형태로 전달되는 이름은 EventFlow 로그 수집 파이프라인을 나타내는 *상태 개체*의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="6483a-143">EventFlow에서 오류가 발생하고 Service Fabric 상태 하위 시스템을 통해 보고할 경우 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="6483a-144">eventFlowConfig에서 Service Fabric 설정 및 응용 프로그램 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="6483a-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="6483a-145">EventFlow는 Service Fabric 설정 및 응용 프로그램 매개 변수를 사용하여 EventFlow 설정 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="6483a-146">값에 대해 다음 특수 구문을 사용하여 Service Fabric 설정 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="6483a-147">`<section-name>`은 Service Fabric 구성 섹션의 이름이고 `<setting-name>`은 EventFlow 설정을 구성하는 데 사용할 값을 제공하는 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="6483a-148">이 작업을 수행하는 방법에 대한 자세한 내용을 보려면 [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters)(Service Fabric 설정 및 응용 프로그램 매개 변수 지원)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6483a-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="6483a-149">확인</span><span class="sxs-lookup"><span data-stu-id="6483a-149">Verification</span></span>

<span data-ttu-id="6483a-150">서비스를 시작하고 Visual Studio의 출력 창에서 디버그를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="6483a-151">서비스가 시작되면 구성된 출력으로 서비스가 레코드를 보내는 증거를 확인하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6483a-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="6483a-152">이벤트 분석 및 시각화 플랫폼으로 이동하여 로그가 나타나는지 확인합니다(몇 분이 소요될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="6483a-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6483a-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6483a-153">Next steps</span></span>

* [<span data-ttu-id="6483a-154">Application Insights를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="6483a-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="6483a-155">OMS를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="6483a-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="6483a-156">EventFlow 설명서</span><span class="sxs-lookup"><span data-stu-id="6483a-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)