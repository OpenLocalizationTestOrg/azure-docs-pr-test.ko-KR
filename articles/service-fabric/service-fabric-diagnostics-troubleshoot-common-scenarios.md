---
title: "이벤트 추적으로 aaaTroubleshooting | Microsoft Docs"
description: "hello 가장 일반적인 문제에 Microsoft Azure 서비스 패브릭 서비스 배포 동안 발생 합니다."
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
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="21e22-103">Azure 서비스 패브릭에서 서비스 배포 시 일반적인 문제 해결</span><span class="sxs-lookup"><span data-stu-id="21e22-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="21e22-104">서비스 개발자 컴퓨터에서를 실행 중인 경우에 쉽게 toouse [Visual Studio의 디버깅 도구](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="21e22-105">원격 클러스터에 대 한 [상태 보고서](service-fabric-view-entities-aggregated-health.md) 은 항상 좋습니다 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="21e22-106">PowerShell을 통해 이러한 보고서는 가장 쉬운 방법으로 tooaccess hello 또는 [SFX](service-fabric-visualizing-your-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="21e22-107">이 문서에서는 원격 클러스터를 디버깅 하는 방법에 대 한 기본 이해를 가정 toouse 도구 둘 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="21e22-108">응용 프로그램 작동 중단</span><span class="sxs-lookup"><span data-stu-id="21e22-108">Application crash</span></span>
<span data-ttu-id="21e22-109">hello "파티션 미만인 대상 복제본 또는 인스턴스 수보다" 보고서는 상태 서비스 오류는 크래시가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="21e22-110">서비스 오류 크래시가 발생 아웃 toofind는 약간 더 많은 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="21e22-111">서비스가 큰 규모로 실행되는 경우 최고의 자료는 면밀한 추적 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="21e22-112">시도 하는 것이 좋습니다 [Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md) 를 추적을 수집 하 고 같은 솔루션을 사용 하 여 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 보기 및 hello 추적을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![SFX 파티션 상태](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="21e22-114">서비스 또는 행위자 초기화 과정</span><span class="sxs-lookup"><span data-stu-id="21e22-114">During service or actor initialization</span></span>
<span data-ttu-id="21e22-115">모든 예외는 hello 서비스 유형을 초기화 되기 전에 hello 프로세스 toocrash를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="21e22-116">이러한 유형의 충돌에 대 한 hello 응용 프로그램 이벤트 로그에는 서비스에서 hello 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="21e22-117">이들은 hello 서비스를 초기화 하기 전에 hello 가장 일반적인 예외 toosee입니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="21e22-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="21e22-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="21e22-119">이 오류는 toomissing 어셈블리 종속성 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="21e22-120">Visual Studio 또는 hello 노드에 대 한 hello 전역 어셈블리 캐시에서 hello CopyLocal 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="21e22-121">***System.Runtime.InteropServices.COMException*** *System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)에서*</span><span class="sxs-lookup"><span data-stu-id="21e22-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="21e22-122">이 hello 등록 된 서비스 유형 이름이 일치 하지 않는 hello 서비스 매니페스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="21e22-123">[Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md) 모든 노드에 대 한 구성된 tooupload hello 응용 프로그램 이벤트 로그를 자동으로 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="21e22-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="21e22-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="21e22-125">Hello 크래시 hello 초기화 또는 등록 된 서비스 형식 또는 작업 자가 실행 하는 동안 문제가 발생 하면 Azure 서비스 패브릭에서 hello 예외가 발견 되었습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="21e22-126">Hello "다음 단계" 섹션에에서 자세히 설명 하는 hello EventSource 공급자에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e22-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21e22-127">Next steps</span></span>
<span data-ttu-id="21e22-128">서비스 패브릭에 제공되는 기존 진단에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="21e22-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="21e22-129">Reliable Actors 진단</span><span class="sxs-lookup"><span data-stu-id="21e22-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="21e22-130">Reliable Services 진단</span><span class="sxs-lookup"><span data-stu-id="21e22-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

