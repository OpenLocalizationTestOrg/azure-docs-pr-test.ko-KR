---
title: "이벤트 추적으로 문제 해결 | Microsoft Docs"
description: "Microsoft Azure 서비스 패브릭에 서비스를 배포하는 동안 발생하는 가장 일반적인 문제."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="7d4ee-103">Azure 서비스 패브릭에서 서비스 배포 시 일반적인 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7d4ee-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="7d4ee-104">개발자 컴퓨터에서 서비스를 실행하는 경우에는 [Visual Studio의 디버깅 도구](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="7d4ee-105">원격 클러스터의 경우 [상태 보고서](service-fabric-view-entities-aggregated-health.md) 에서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="7d4ee-106">이러한 보고서에 액세스하는 가장 쉬운 방법은 PowerShell 또는 [SFX](service-fabric-visualizing-your-cluster.md)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="7d4ee-107">이 문서는 사용자가 원격 클러스터를 디버그 중이며 이 도구 중 한 가지를 사용하는 방법에 대해 기본적인 이해력이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="7d4ee-108">응용 프로그램 작동 중단</span><span class="sxs-lookup"><span data-stu-id="7d4ee-108">Application crash</span></span>
<span data-ttu-id="7d4ee-109">"Partition is below target replica or instance count"(파티션이 대상 복제본 또는 인스턴스 수 이하입니다) 보고서는 서비스 작동이 중단된다는 것을 알리는 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="7d4ee-110">서비스의 어느 부분에서 작동이 중단되는지를 알아내려면 조사가 더 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="7d4ee-111">서비스가 큰 규모로 실행되는 경우 최고의 자료는 면밀한 추적 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="7d4ee-112">[Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md)를 사용하여 추적을 수집하고 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)와 같은 솔루션을 사용하여 추적을 보고 검색하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![SFX 파티션 상태](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="7d4ee-114">서비스 또는 행위자 초기화 과정</span><span class="sxs-lookup"><span data-stu-id="7d4ee-114">During service or actor initialization</span></span>
<span data-ttu-id="7d4ee-115">서비스 유형이 초기화되기 전에 예외가 발생하면 프로세스 중단이 유발됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="7d4ee-116">이러한 유형의 작동 중단은, 응용 프로그램 이벤트 로그에 서비스의 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="7d4ee-117">서비스가 초기화되기 전에 볼 수 있는 가장 일반적인 예외는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="7d4ee-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="7d4ee-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="7d4ee-119">이 오류는 대체로 어셈블리 종속성이 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="7d4ee-120">Visual Studio에서 CopyLocal 속성을 확인하거나 노드의 전역 어셈블리 캐시를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="7d4ee-121">***System.Runtime.InteropServices.COMException*** *System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)에서*</span><span class="sxs-lookup"><span data-stu-id="7d4ee-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="7d4ee-122">등록된 서비스 유형 이름이 서비스 매니페스트와 일치하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="7d4ee-123">[Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md) 을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="7d4ee-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="7d4ee-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="7d4ee-125">등록된 서비스 유형 또는 행위자를 초기화하거나 실행하는 중에 작동이 중단되면 Azure 서비스 패브릭이 예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="7d4ee-126">이 내용은 EventSource 공급자를 통해 볼 수 있으며 “다음 단계” 섹션에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d4ee-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d4ee-127">Next steps</span></span>
<span data-ttu-id="7d4ee-128">서비스 패브릭에 제공되는 기존 진단에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ee-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="7d4ee-129">Reliable Actors 진단</span><span class="sxs-lookup"><span data-stu-id="7d4ee-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="7d4ee-130">Reliable Services 진단</span><span class="sxs-lookup"><span data-stu-id="7d4ee-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

