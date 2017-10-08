---
title: "서비스 패브릭 이벤트 집계 EventFlow와 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="abd26-103">EventFlow를 사용하여 이벤트 집계 및 수집</span><span class="sxs-lookup"><span data-stu-id="abd26-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="abd26-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) 노드 tooone 또는 자세한 모니터링 대상에서 이벤트를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="abd26-105">서비스 프로젝트에서 NuGet 패키지로 포함 이기 때문에 Azure 진단에 대 한 앞에서 언급 한 hello 노드 구성 문제를 제거 하는 hello 서비스와 EventFlow 코드 및 구성 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="abd26-106">EventFlow는 서비스 프로세스 내에서 실행 되며 구성 toohello 출력에 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="abd26-107">Hello 직접 연결으로 인해 EventFlow Azure, 컨테이너 및 온-프레미스 서비스 배포에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="abd26-108">각 EventFlow 파이프라인이 외부 연결을 만들기 때문에 컨테이너와 같이 고밀도 시나리오에서 EventFlow를 실행하는 경우 신중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="abd26-109">따라서 여러 프로세스를 호스트하는 경우 몇 가지 아웃바운드 연결이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="abd26-110">때문에 서비스 패브릭 응용 프로그램에 대 한 만큼 중요 하지 않습니다이 모든 복제본의는 `ServiceType` hello에 동일한 프로세스를 실행 하 고이 hello 아웃 바운드 연결 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="abd26-111">EventFlow 제공 하는 이벤트 필터링을 hello 지정 된 필터와 일치 하는 hello 이벤트만 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="abd26-112">EventFlow 설정</span><span class="sxs-lookup"><span data-stu-id="abd26-112">Setting up EventFlow</span></span>

<span data-ttu-id="abd26-113">EventFlow 이진을 NuGet 패키지 집합으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="abd26-114">tooadd EventFlow tooa 서비스 패브릭 서비스 프로젝트 hello 솔루션 탐색기에서에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 "관리 NuGet 패키지입니다."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="abd26-115">Toohello "찾아보기" 탭과 검색에 대 한 전환 "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="abd26-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 패키지 관리자 UI에서 EventFlow NuGet 패키지](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="abd26-117">"입력" 및 "출력" 레이블이 지정된 다양한 패키지 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="abd26-118">EventFlow는 다양한 로깅 공급자 및 분석기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="abd26-119">hello 서비스 EventFlow 호스팅 hello 원본과 hello 응용 프로그램 로그에 대 한 대상에 따라 적절 한 패키지를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="abd26-120">또한 toohello 핵심 ServiceFabric 패키지도 필요 하나 이상 입력 및 출력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="abd26-121">예제를 따르는 패키지 toosent EventSource 이벤트 tooApplication Insights hello를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="abd26-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`hello 서비스 EventSource 클래스에서와 같은 표준 EventSources toocapture 데이터 *ServiceFabric 조항을* 및 *Microsoft-ServiceFabric 행위자*)</span><span class="sxs-lookup"><span data-stu-id="abd26-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="abd26-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(하겠습니다 toosend hello 로그 tooan Azure Application Insights 리소스)</span><span class="sxs-lookup"><span data-stu-id="abd26-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="abd26-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(서비스 패브릭 서비스 구성에서 hello EventFlow 파이프라인의 초기화를 사용 하도록 설정 및 진단 데이터 서비스 패브릭 상태 보고서 변수로 전송 된 모든 문제를 보고)</span><span class="sxs-lookup"><span data-stu-id="abd26-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="abd26-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`패키지에 필요한 hello 서비스 프로젝트 tootarget.NET Framework 4.6 이상.</span><span class="sxs-lookup"><span data-stu-id="abd26-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="abd26-126">프로젝트 속성에서이 패키지를 설치 하기 전에 hello 적절 한 대상 프레임 워크를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="abd26-127">결국 hello 패키지가 설치 되어, hello 다음 단계 tooconfigure는이 고 EventFlow hello 서비스에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="abd26-128">로그 수집 구성 및 사용</span><span class="sxs-lookup"><span data-stu-id="abd26-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="abd26-129">hello 로그 전송 hello EventFlow 파이프라인은 구성 파일에 저장 하는 사양에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="abd26-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` 패키지 설치 시작 EventFlow 구성 파일에서 `PackageRoot\Config` 라는 솔루션 폴더 `eventFlowConfig.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="abd26-131">이 구성 파일 수정 toobe toocapture가에서 데이터가 필요한 hello 기본 서비스 `EventSource` 클래스 및 데이터 toohello 적절 한 위치로 보내고 tooconfigure를 원하는 다른 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="abd26-132">다음은 샘플 *eventFlowConfig.json* 위에서 언급 한 hello NuGet 패키지에 따라:</span><span class="sxs-lookup"><span data-stu-id="abd26-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="abd26-133">서비스의 ServiceEventSource의 hello 이름이 hello hello의 Name 속성의 hello 값 `EventSourceAttribute` toohello ServiceEventSource 클래스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="abd26-134">모두에 지정 된 hello `ServiceEventSource.cs` hello 서비스 코드에 포함 되어 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="abd26-135">예를 들어 hello에 다음 코드 조각 hello hello ServiceEventSource 이름은 *MyCompany-응용 프로그램 1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="abd26-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="abd26-136">`eventFlowConfig.json` 파일은 서비스 구성 패키지의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="abd26-137">변경 toothis 파일 hello 서비스의 전체 또는 구성-전용 업그레이드에 포함 될 수 이므로 주체 tooService Fabric 업그레이드 상태 검사 및 자동 롤백 업그레이드에 실패할 경우.</span><span class="sxs-lookup"><span data-stu-id="abd26-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="abd26-138">자세한 내용은 [Service Fabric 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abd26-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="abd26-139">hello *필터* hello config 섹션 toofurther 수 있습니다. hello EventFlow 파이프라인 toohello 출력, toodrop 있도록을 통한 지속적인 toogo는 hello 정보를 사용자 지정 또는 특정 정보를 포함 하거나 hello를 변경 합니다. hello 이벤트 데이터의 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="abd26-140">필터링에 대한 자세한 내용은 [EventFlow 필터](https://github.com/Azure/diagnostics-eventflow#filters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abd26-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="abd26-141">hello 마지막 단계는 tooinstantiate EventFlow 파이프라인에 있는 서비스의 시작 코드에 `Program.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="abd26-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="abd26-142">hello 이름이 hello의 hello 매개 변수로 전달 `CreatePipeline` hello 방식의 `ServiceFabricDiagnosticsPipelineFactory` hello의 hello 이름인 *상태 엔터티* hello EventFlow 로그 컬렉션 파이프라인을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="abd26-143">EventFlow 발생 한 경우이 이름을 사용 및 오류 hello 서비스 패브릭 상태 하위 시스템을 통해 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="abd26-144">서비스 패브릭 설정 및 응용 프로그램 매개 변수 tooin eventFlowConfig 사용</span><span class="sxs-lookup"><span data-stu-id="abd26-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="abd26-145">EventFlow는 서비스 패브릭 설정 및 응용 프로그램 매개 변수가 tooconfigure EventFlow 설정 사용을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="abd26-146">TooService 패브릭 설정 매개 변수 값에 대 한이 특수 구문을 사용 하 여 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="abd26-147">`<section-name>`hello 서비스 패브릭 구성 섹션의 hello 이름인 및 `<setting-name>` EventFlow 설정을 사용 하는 tooconfigure 될 hello 값을 제공 하는 hello 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="abd26-148">방법에 대 한 자세한 tooread toodo,이 이동 너무[서비스 패브릭 설정 및 응용 프로그램 매개 변수 지원](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="abd26-149">확인</span><span class="sxs-lookup"><span data-stu-id="abd26-149">Verification</span></span>

<span data-ttu-id="abd26-150">서비스를 시작 하 고 디버그 hello 관찰 Visual Studio의 출력 창.</span><span class="sxs-lookup"><span data-stu-id="abd26-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="abd26-151">Hello 서비스를 시작한 후 사용자가 구성한 toohello 출력을 기록 하는 증명 정보를 서비스에 보내는 표시를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd26-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="abd26-152">이벤트 분석 및 시각화 플랫폼 tooyour 이동 하 고 로그는 tooshow 시작됨인지 확인 위쪽 (몇 분 정도 걸릴 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="abd26-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="abd26-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="abd26-153">Next steps</span></span>

* [<span data-ttu-id="abd26-154">Application Insights를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="abd26-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="abd26-155">OMS를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="abd26-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="abd26-156">EventFlow 설명서</span><span class="sxs-lookup"><span data-stu-id="abd26-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)