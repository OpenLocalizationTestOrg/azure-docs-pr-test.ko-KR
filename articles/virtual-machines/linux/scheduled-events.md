---
title: "Azure에서 Linux Vm에 대 한 이벤트 aaaScheduled | Microsoft Docs"
description: "예약 된 이벤트에 대 한 hello Azure 메타 데이터 서비스를 사용 하 여 Linux 가상 컴퓨터에 있습니다."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="51448-103">Azure 메타데이터 서비스: Linux VM에 예정된 이벤트(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="51448-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="51448-104">미리 보기 toohello 사용 약관을 동의 하는 hello 조건에 사용 가능한 tooyou를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="51448-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="51448-105">자세한 내용은 [Microsoft Azure Preview에 대한 Microsoft Azure 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51448-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="51448-106">예약 된 이벤트 hello Azure 메타 데이터 서비스에서 hello 하위 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="51448-107">응용 프로그램에서 이벤트를 준비하고 중단을 제한할 수 있도록 예정된 이벤트(예: 다시 부팅)에 대한 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51448-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="51448-108">이 기능은 PaaS 및 IaaS를 포함한 모든 Azure Virtual Machine 유형에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="51448-109">예약 된 이벤트는 이벤트의 toominimize hello 효과 가상 컴퓨터 시간 tooperform 예방 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="51448-110">예약된 이벤트를 Windows 및 Linux VM 모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="51448-111">Windows에서 예약된 이벤트에 대한 자세한 내용은 [Windows VM에 예약된 이벤트](../windows/scheduled-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51448-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="51448-112">예정된 이벤트 의의</span><span class="sxs-lookup"><span data-stu-id="51448-112">Why Scheduled Events?</span></span>

<span data-ttu-id="51448-113">예약 된 이벤트로 인해 서비스에서 단계에 플랫폼 intiated 유지 관리 또는 사용자가 시작한 작업의 toolimit hello 영향을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="51448-114">복제 기술을 toomaintain 상태를 사용 하는 다중 인스턴스 작업 인스턴스를 여러 개에서 일어나 고 취약 한 toooutages 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="51448-115">이러한 중단으로 인해 비용이 많이 드는 작업(예: 인덱스 다시 빌드) 또는 복제본 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="51448-116">대부분의 경우에서 hello 전반적인 서비스 가용성을 향상 시킬 수 있습니다와 같은 정상적인 종료 시퀀스를 수행 하 여 완료 (또는 취소) 진행 중인 트랜잭션은, hello (수동 장애 조치) 클러스터에서 작업 tooother Vm을 다시 할당 하거나 hello를 제거 합니다. 네트워크 부하 분산 장치 풀에서 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="51448-117">여기서 예정 된 이벤트에 대 한 관리자에 게 알리는 나 이러한 이벤트를 로깅하는 데 도움이 hello 클라우드에서 호스트 되는 응용 프로그램의 hello 서비스 효율성을 개선 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="51448-118">Azure 서비스 메타 데이터 표면 예약 된 이벤트 hello 다음에서 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="51448-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="51448-119">플랫폼 시작 유지 관리(예: 호스트 OS 롤아웃)</span><span class="sxs-lookup"><span data-stu-id="51448-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="51448-120">사용자 시작 호출(예: 사용자에 의한 VM 다시 시작 또는 다시 배포)</span><span class="sxs-lookup"><span data-stu-id="51448-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="51448-121">hello 기본 사항</span><span class="sxs-lookup"><span data-stu-id="51448-121">hello basics</span></span>  

<span data-ttu-id="51448-122">Azure 메타 데이터 서비스는 hello VM 내에서 액세스할 수 있는 REST 끝점을 사용 하는 가상 컴퓨터를 실행 하는 방법에 대 한 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="51448-123">hello 정보는 불가능 IP를 통해 사용할 수 있으므로 hello VM 외부에 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="51448-124">범위</span><span class="sxs-lookup"><span data-stu-id="51448-124">Scope</span></span>
<span data-ttu-id="51448-125">예약 된 이벤트는 표시 tooall 클라우드 서비스의 가상 컴퓨터 또는 가상 컴퓨터 가용성 집합에 tooall입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="51448-126">Hello를 확인 해야 하는 결과적으로, `Resources` 필드에 hello 이벤트 tooidentify Vm toobe 영향을 받는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="51448-127">Hello 끝점 검색</span><span class="sxs-lookup"><span data-stu-id="51448-127">Discovering hello endpoint</span></span>
<span data-ttu-id="51448-128">Hello 경우 가상 네트워크 (VNet) 내에서 가상 컴퓨터를 만들 위치 hello 메타 데이터 서비스에서 라우팅 불가능 고정 IP를 사용할 수는 `169.254.169.254`합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="51448-129">추가 논리 hello 가상 컴퓨터 가상 네트워크를 클라우드 서비스 및 클래식 Vm에 대 한 hello 기본 사례 내에서 만들지 않은 경우 필요한 toodiscover hello 끝점 toouse.</span><span class="sxs-lookup"><span data-stu-id="51448-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="51448-130">어떻게 너무 toothis 샘플 toolearn 참조[hello 호스트 끝점을 검색](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="51448-131">버전 관리</span><span class="sxs-lookup"><span data-stu-id="51448-131">Versioning</span></span> 
<span data-ttu-id="51448-132">hello 인스턴스 메타 데이터 서비스 버전 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="51448-133">버전은 필수 이며 hello 현재 버전은 `2017-03-01`합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="51448-134">이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기.</span><span class="sxs-lookup"><span data-stu-id="51448-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="51448-135">이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="51448-136">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="51448-136">Using headers</span></span>
<span data-ttu-id="51448-137">Hello 헤더를 제공 해야 hello 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="51448-138">예약된 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="51448-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="51448-139">hello 예약 된 이벤트에 대 한 요청을 수행 하는 처음으로 Azure 암시적으로 hello 기능을 활성화 가상 컴퓨터에 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="51448-140">따라서 지연 된 응답을 tootwo 분의 첫 번째 호출에서 하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="51448-141">사용자 시작 유지 관리</span><span class="sxs-lookup"><span data-stu-id="51448-141">User initiated maintenance</span></span>
<span data-ttu-id="51448-142">사용자 시작한 hello Azure 포털, API, CLI를 통해 가상 컴퓨터 유지 관리 또는 PowerShell 예약 된 이벤트를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="51448-143">응용 프로그램에서 tootest hello 유지 관리 준비 논리를 허용 하 고 사용자가 시작한 유지 관리에 대 한 응용 프로그램 tooprepare 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="51448-144">가상 컴퓨터를 다시 시작하면 `Reboot` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="51448-145">가상 컴퓨터를 다시 배포하면 `Redeploy` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="51448-146">현재는 사용자 시작 유지 관리 작업을 최대 10개까지 동시 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="51448-147">이 제한은 예정된 이벤트 일반 공급 이전에 완화될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="51448-148">현재는 예약된 이벤트를 실행하는 사용자 시작 유지 관리를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="51448-149">구성 기능은 이후 버전에 추가될 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="51448-150">Hello API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="51448-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="51448-151">이벤트 쿼리</span><span class="sxs-lookup"><span data-stu-id="51448-151">Query for events</span></span>
<span data-ttu-id="51448-152">호출 하는 hello 다음을 수행 하 여 예약 된 이벤트를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="51448-153">응답에는 예약된 이벤트의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="51448-154">빈 배열은 현재 예약된 이벤트가 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="51448-155">Hello 경우에서 예약 된 이벤트 인 hello 응답 이벤트의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="51448-156">이벤트 속성</span><span class="sxs-lookup"><span data-stu-id="51448-156">Event properties</span></span>
|<span data-ttu-id="51448-157">속성</span><span class="sxs-lookup"><span data-stu-id="51448-157">Property</span></span>  |  <span data-ttu-id="51448-158">설명</span><span class="sxs-lookup"><span data-stu-id="51448-158">Description</span></span> |
| - | - |
| <span data-ttu-id="51448-159">EventId</span><span class="sxs-lookup"><span data-stu-id="51448-159">EventId</span></span> | <span data-ttu-id="51448-160">이 이벤트의 GUID(Globally Unique Identifier)입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="51448-161">예제:</span><span class="sxs-lookup"><span data-stu-id="51448-161">Example:</span></span> <br><ul><li><span data-ttu-id="51448-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="51448-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="51448-163">EventType</span><span class="sxs-lookup"><span data-stu-id="51448-163">EventType</span></span> | <span data-ttu-id="51448-164">이 이벤트로 인해 발생하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="51448-165">값</span><span class="sxs-lookup"><span data-stu-id="51448-165">Values:</span></span> <br><ul><li> <span data-ttu-id="51448-166">`Freeze`: hello 가상 컴퓨터를 몇 초 동안 예약 된 toopause는 합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="51448-167">hello CPU 일시 중단 되어 있지만 메모리, 열려 있는 파일 또는 네트워크 연결에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="51448-168">`Reboot`: 가상 컴퓨터를 다시 부팅에 대 한 예약 된 hello (비 영구적인 메모리가 손실).</span><span class="sxs-lookup"><span data-stu-id="51448-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="51448-169">`Redeploy`: hello 가상 컴퓨터는 예약 된 toomove tooanother 노드 (임시 디스크는 손실 됨).</span><span class="sxs-lookup"><span data-stu-id="51448-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="51448-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="51448-170">ResourceType</span></span> | <span data-ttu-id="51448-171">이 이벤트가 영향을 주는 리소스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="51448-172">값</span><span class="sxs-lookup"><span data-stu-id="51448-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="51448-173">리소스</span><span class="sxs-lookup"><span data-stu-id="51448-173">Resources</span></span>| <span data-ttu-id="51448-174">이 이벤트가 영향을 주는 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-174">List of resources this event impacts.</span></span> <span data-ttu-id="51448-175">이 최대 하나의에서 toocontain 컴퓨터 보장 [업데이트 도메인](manage-availability.md), 하지만 hello UD의에서 모든 컴퓨터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="51448-176">예제:</span><span class="sxs-lookup"><span data-stu-id="51448-176">Example:</span></span> <br><ul><li> <span data-ttu-id="51448-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="51448-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="51448-178">이벤트 상태</span><span class="sxs-lookup"><span data-stu-id="51448-178">Event Status</span></span> | <span data-ttu-id="51448-179">이 이벤트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-179">Status of this event.</span></span> <br><br> <span data-ttu-id="51448-180">값</span><span class="sxs-lookup"><span data-stu-id="51448-180">Values:</span></span> <ul><li><span data-ttu-id="51448-181">`Scheduled`:이 이벤트는 hello에 지정 된 hello 시간 후 예약 된 toostart `NotBefore` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="51448-182">`Started`: 이 이벤트가 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="51448-183">더 `Completed` 또는 유사한 상태는 제공 된 적이; hello 이벤트 hello 이벤트가 완료 될 때 더 이상 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="51448-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="51448-184">NotBefore</span></span>| <span data-ttu-id="51448-185">이 시간이 지난 후 이 이벤트가 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51448-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="51448-186">예제:</span><span class="sxs-lookup"><span data-stu-id="51448-186">Example:</span></span> <br><ul><li> <span data-ttu-id="51448-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="51448-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="51448-188">이벤트 예약</span><span class="sxs-lookup"><span data-stu-id="51448-188">Event scheduling</span></span>
<span data-ttu-id="51448-189">각 이벤트 예약 된 이벤트 형식에 따라 이후 hello 시간의 최소 양입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="51448-190">이 시간은 이벤트의 `NotBefore` 속성에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="51448-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="51448-191">EventType</span><span class="sxs-lookup"><span data-stu-id="51448-191">EventType</span></span>  | <span data-ttu-id="51448-192">최소 공지</span><span class="sxs-lookup"><span data-stu-id="51448-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="51448-193">중지</span><span class="sxs-lookup"><span data-stu-id="51448-193">Freeze</span></span>| <span data-ttu-id="51448-194">15분</span><span class="sxs-lookup"><span data-stu-id="51448-194">15 minutes</span></span> |
| <span data-ttu-id="51448-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="51448-195">Reboot</span></span> | <span data-ttu-id="51448-196">15분</span><span class="sxs-lookup"><span data-stu-id="51448-196">15 minutes</span></span> |
| <span data-ttu-id="51448-197">재배포</span><span class="sxs-lookup"><span data-stu-id="51448-197">Redeploy</span></span> | <span data-ttu-id="51448-198">10분</span><span class="sxs-lookup"><span data-stu-id="51448-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="51448-199">이벤트 시작</span><span class="sxs-lookup"><span data-stu-id="51448-199">Starting an event</span></span> 

<span data-ttu-id="51448-200">예정 된 이벤트의 학습 하 고 정상 종료 논리를 완료 하 여 hello 처리 중인 이벤트를 승인할 수 있습니다는 `POST` hello로 toohello 메타 데이터 서비스를 호출할 `EventId`합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="51448-201">이 tooAzure hello 최소 알림을 줄일 수를 나타냅니다 (가능한 경우) 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="51448-202">모든 이벤트 tooproceed hello를 사용 하면 이벤트를 승인 `Resources` hello hello 이벤트도 인해 가상 컴퓨터 뿐 아니라 hello 이벤트에서입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="51448-203">따라서 수도 있습니다 tooelect hello hello에 첫 번째 컴퓨터 처럼 간단할 수도 있음 리더 toocoordinate hello 승인을 `Resources` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="51448-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="51448-204">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="51448-204">Python sample</span></span> 

<span data-ttu-id="51448-205">hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.</span><span class="sxs-lookup"><span data-stu-id="51448-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="51448-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51448-206">Next steps</span></span> 

- <span data-ttu-id="51448-207">Hello hello에서 사용할 수 있는 Api에 대해 자세히 읽어보세요 [인스턴스 메타 데이터 서비스](instance-metadata-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="51448-207">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="51448-208">[Azure에서 Linux 가상 컴퓨터에 대한 계획된 유지 관리](planned-maintenance.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="51448-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
