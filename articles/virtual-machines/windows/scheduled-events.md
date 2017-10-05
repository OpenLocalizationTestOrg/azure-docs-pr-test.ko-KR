---
title: "Azure에서 Windows VM에 예정된 이벤트 | Microsoft Docs"
description: "Windows 가상 컴퓨터에서 Azure 메타데이터 서비스를 사용하여 예정된 이벤트입니다."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: 7198fa8d1a512d10ca7022078aa2ea7bde3a4c02
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="0f3dd-103">Azure 메타데이터 서비스: Windows VM에 예정된 이벤트(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0f3dd-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="0f3dd-104">사용 약관에 동의하게 되면 미리 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="0f3dd-105">자세한 내용은 [Microsoft Azure Preview에 대한 Microsoft Azure 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="0f3dd-106">예약된 이벤트는 Azure 메타데이터 서비스의 하위 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="0f3dd-107">응용 프로그램에서 이벤트를 준비하고 중단을 제한할 수 있도록 예정된 이벤트(예: 다시 부팅)에 대한 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="0f3dd-108">이 기능은 PaaS 및 IaaS를 포함한 모든 Azure Virtual Machine 유형에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="0f3dd-109">예약된 이벤트는 가상 컴퓨터에 예방 작업을 수행하여 이벤트의 영향을 최소화할 수 있는 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="0f3dd-110">예약된 이벤트를 Linux 및 Windows VM 모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="0f3dd-111">Linux에서 예약된 이벤트에 대한 자세한 내용은 [Linux VM에 예약된 이벤트](../windows/scheduled-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="0f3dd-112">예정된 이벤트 의의</span><span class="sxs-lookup"><span data-stu-id="0f3dd-112">Why Scheduled Events?</span></span>

<span data-ttu-id="0f3dd-113">예약된 이벤트를 사용하면 플랫폼에서 시작된 유지 관리 또는 사용자가 시작한 서비스 작업의 영향을 제한하는 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="0f3dd-114">복제 기술을 사용하여 상태를 유지 관리하는 다중 인스턴스 워크로드는 여러 인스턴스에서 발생하는 중단에 취약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="0f3dd-115">이러한 중단으로 인해 비용이 많이 드는 작업(예: 인덱스 다시 빌드) 또는 복제본 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="0f3dd-116">그 밖에 많은 경우, 진행 중인 트랜잭션을 완료(또는 취소)하거나, 클러스터의 다른 VM에 작업을 다시 할당(수동 장애 조치)하거나, 네트워크 부하 분산 장치 풀에서 가상 컴퓨터를 제거하는 등 정상적인 종료 시퀀스를 수행하여 전체 서비스 가용성을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="0f3dd-117">예정된 이벤트에 대해 관리자에게 알리거나 그러한 이벤트를 로깅하는 것만으로도 클라우드에 호스팅된 응용 프로그램의 서비스 효율성을 개선하는 데 도움이 되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="0f3dd-118">Azure 메타데이터 서비스는 다음 사용 사례에서 예정된 이벤트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="0f3dd-119">플랫폼 시작 유지 관리(예: 호스트 OS 롤아웃)</span><span class="sxs-lookup"><span data-stu-id="0f3dd-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="0f3dd-120">사용자 시작 호출(예: 사용자에 의한 VM 다시 시작 또는 다시 배포)</span><span class="sxs-lookup"><span data-stu-id="0f3dd-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="0f3dd-121">기본 사항</span><span class="sxs-lookup"><span data-stu-id="0f3dd-121">The basics</span></span>  

<span data-ttu-id="0f3dd-122">Azure 메타데이터 서비스는 VM 내에서 액세스할 수 있는 REST 끝점을 사용하여 Virtual Machines 실행에 대한 정보를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="0f3dd-123">이 정보는 라우팅할 수 없는 IP를 통해 사용할 수 있으므로 VM 외부에 공개되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="0f3dd-124">범위</span><span class="sxs-lookup"><span data-stu-id="0f3dd-124">Scope</span></span>
<span data-ttu-id="0f3dd-125">Scheduled Events는 클라우드 서비스의 모든 Virtual Machines 또는 가용성 집합의 모든 Virtual Machines에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="0f3dd-126">따라서 이벤트의 `Resources` 필드를 확인하여 영향을 받을 VM을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="0f3dd-127">끝점 검색</span><span class="sxs-lookup"><span data-stu-id="0f3dd-127">Discovering the endpoint</span></span>
<span data-ttu-id="0f3dd-128">가상 컴퓨터가 VNet(가상 네트워크) 내에 생성된 경우, 라우팅할 수 없는 고정 IP(`169.254.169.254`)에서 메타데이터 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="0f3dd-129">클라우드 서비스 및 클래식 VM의 기본 사례처럼 가상 컴퓨터가 가상 네트워크에 생성되지 않은 경우 사용할 끝점을 검색하려면 추가 논리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="0f3dd-130">[호스트 끝점을 검색](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)하는 방법은 이 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="0f3dd-131">버전 관리</span><span class="sxs-lookup"><span data-stu-id="0f3dd-131">Versioning</span></span> 
<span data-ttu-id="0f3dd-132">인스턴스 메타데이터 서비스에는 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0f3dd-133">버전은 필수이며 최신 버전은 `2017-03-01`입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0f3dd-134">예약된 이벤트의 이전 미리 보기 릴리스는 api-version으로 {최신 버전}을 지원했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="0f3dd-135">이 형식은 더 이상 지원되지 않으며 향후 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0f3dd-136">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="0f3dd-136">Using headers</span></span>
<span data-ttu-id="0f3dd-137">메타데이터 서비스를 쿼리할 때 요청이 실수로 리디렉션되지 않도록 `Metadata: true` 헤더를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="0f3dd-138">예약된 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="0f3dd-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="0f3dd-139">처음으로 예약된 이벤트를 요청하면 Azure는 가상 컴퓨터의 기능을 암시적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="0f3dd-140">결과적으로 최대 2분인 첫 번째 호출에서 지연된 응답을 예상해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="0f3dd-141">사용자 시작 유지 관리</span><span class="sxs-lookup"><span data-stu-id="0f3dd-141">User initiated maintenance</span></span>
<span data-ttu-id="0f3dd-142">사용자가 예정된 이벤트에서 Azure Portal, API, CLI 또는 PowerShell을 통해 가상 컴퓨터 유지 관리를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="0f3dd-143">그러면 응용 프로그램의 유지 관리 준비 논리를 테스트할 수 있으며, 응용 프로그램에서 사용자 시작 유지 관리를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="0f3dd-144">가상 컴퓨터를 다시 시작하면 `Reboot` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="0f3dd-145">가상 컴퓨터를 다시 배포하면 `Redeploy` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0f3dd-146">현재는 사용자 시작 유지 관리 작업을 최대 10개까지 동시 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="0f3dd-147">이 제한은 예정된 이벤트 일반 공급 이전에 완화될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="0f3dd-148">현재는 예약된 이벤트를 실행하는 사용자 시작 유지 관리를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="0f3dd-149">구성 기능은 이후 버전에 추가될 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="0f3dd-150">API 사용</span><span class="sxs-lookup"><span data-stu-id="0f3dd-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="0f3dd-151">이벤트 쿼리</span><span class="sxs-lookup"><span data-stu-id="0f3dd-151">Query for events</span></span>
<span data-ttu-id="0f3dd-152">다음과 같이 호출하여 예약된 이벤트를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="0f3dd-153">응답에는 예약된 이벤트의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="0f3dd-154">빈 배열은 현재 예약된 이벤트가 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="0f3dd-155">예약된 이벤트가 있는 경우 응답에 다음과 같은 이벤트의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="0f3dd-156">이벤트 속성</span><span class="sxs-lookup"><span data-stu-id="0f3dd-156">Event properties</span></span>
|<span data-ttu-id="0f3dd-157">속성</span><span class="sxs-lookup"><span data-stu-id="0f3dd-157">Property</span></span>  |  <span data-ttu-id="0f3dd-158">설명</span><span class="sxs-lookup"><span data-stu-id="0f3dd-158">Description</span></span> |
| - | - |
| <span data-ttu-id="0f3dd-159">EventId</span><span class="sxs-lookup"><span data-stu-id="0f3dd-159">EventId</span></span> | <span data-ttu-id="0f3dd-160">이 이벤트의 GUID(Globally Unique Identifier)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="0f3dd-161">예제:</span><span class="sxs-lookup"><span data-stu-id="0f3dd-161">Example:</span></span> <br><ul><li><span data-ttu-id="0f3dd-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="0f3dd-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="0f3dd-163">EventType</span><span class="sxs-lookup"><span data-stu-id="0f3dd-163">EventType</span></span> | <span data-ttu-id="0f3dd-164">이 이벤트로 인해 발생하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="0f3dd-165">값</span><span class="sxs-lookup"><span data-stu-id="0f3dd-165">Values:</span></span> <br><ul><li> <span data-ttu-id="0f3dd-166">`Freeze`: 몇 초 동안 가상 컴퓨터를 일시 중지하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="0f3dd-167">CPU가 일시 중단되지만 메모리, 열려 있는 파일 또는 네트워크 연결에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="0f3dd-168">`Reboot`: 가상 컴퓨터를 다시 부팅하도록 예약합니다(비영구 메모리가 손실됨).</span><span class="sxs-lookup"><span data-stu-id="0f3dd-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="0f3dd-169">`Redeploy`: 가상 컴퓨터를 다른 노드로 이동하도록 예약합니다(임시 디스크가 손실됨).</span><span class="sxs-lookup"><span data-stu-id="0f3dd-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="0f3dd-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="0f3dd-170">ResourceType</span></span> | <span data-ttu-id="0f3dd-171">이 이벤트가 영향을 주는 리소스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="0f3dd-172">값</span><span class="sxs-lookup"><span data-stu-id="0f3dd-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="0f3dd-173">리소스</span><span class="sxs-lookup"><span data-stu-id="0f3dd-173">Resources</span></span>| <span data-ttu-id="0f3dd-174">이 이벤트가 영향을 주는 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-174">List of resources this event impacts.</span></span> <span data-ttu-id="0f3dd-175">최대 하나의 [업데이트 도메인](manage-availability.md)에 있는 컴퓨터를 포함하지만 UD의 모든 컴퓨터를 포함할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="0f3dd-176">예제:</span><span class="sxs-lookup"><span data-stu-id="0f3dd-176">Example:</span></span> <br><ul><li> <span data-ttu-id="0f3dd-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="0f3dd-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="0f3dd-178">이벤트 상태</span><span class="sxs-lookup"><span data-stu-id="0f3dd-178">Event Status</span></span> | <span data-ttu-id="0f3dd-179">이 이벤트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-179">Status of this event.</span></span> <br><br> <span data-ttu-id="0f3dd-180">값</span><span class="sxs-lookup"><span data-stu-id="0f3dd-180">Values:</span></span> <ul><li><span data-ttu-id="0f3dd-181">`Scheduled`: `NotBefore` 속성에 지정된 시간 이후 시작하도록 이 이벤트를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="0f3dd-182">`Started`: 이 이벤트가 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="0f3dd-183">`Completed` 또는 유사한 상태가 제공된 적이 없습니다. 이벤트가 완료되면 더 이상 이벤트가 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="0f3dd-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="0f3dd-184">NotBefore</span></span>| <span data-ttu-id="0f3dd-185">이 시간이 지난 후 이 이벤트가 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="0f3dd-186">예제:</span><span class="sxs-lookup"><span data-stu-id="0f3dd-186">Example:</span></span> <br><ul><li> <span data-ttu-id="0f3dd-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="0f3dd-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="0f3dd-188">이벤트 예약</span><span class="sxs-lookup"><span data-stu-id="0f3dd-188">Event scheduling</span></span>
<span data-ttu-id="0f3dd-189">각 이벤트는 이벤트 유형에 따라 향후 최소한의 시간으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="0f3dd-190">이 시간은 이벤트의 `NotBefore` 속성에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="0f3dd-191">EventType</span><span class="sxs-lookup"><span data-stu-id="0f3dd-191">EventType</span></span>  | <span data-ttu-id="0f3dd-192">최소 공지</span><span class="sxs-lookup"><span data-stu-id="0f3dd-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="0f3dd-193">중지</span><span class="sxs-lookup"><span data-stu-id="0f3dd-193">Freeze</span></span>| <span data-ttu-id="0f3dd-194">15분</span><span class="sxs-lookup"><span data-stu-id="0f3dd-194">15 minutes</span></span> |
| <span data-ttu-id="0f3dd-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="0f3dd-195">Reboot</span></span> | <span data-ttu-id="0f3dd-196">15분</span><span class="sxs-lookup"><span data-stu-id="0f3dd-196">15 minutes</span></span> |
| <span data-ttu-id="0f3dd-197">재배포</span><span class="sxs-lookup"><span data-stu-id="0f3dd-197">Redeploy</span></span> | <span data-ttu-id="0f3dd-198">10분</span><span class="sxs-lookup"><span data-stu-id="0f3dd-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="0f3dd-199">이벤트 시작</span><span class="sxs-lookup"><span data-stu-id="0f3dd-199">Starting an event</span></span> 

<span data-ttu-id="0f3dd-200">예정된 이벤트에 대해 알게 되고 정상 종료를 위한 논리를 완료하면 `EventId`로 메타데이터 서비스에 대한 `POST` 호출을 실행하여 처리 중인 이벤트를 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="0f3dd-201">이는 Azure에 최소 알림 시간을 단축할 수 있음(가능한 경우)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="0f3dd-202">이벤트를 승인하면 해당 이벤트를 승인한 가상 컴퓨터뿐만 아니라 이벤트의 모든 `Resources`에 대해 이벤트가 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="0f3dd-203">따라서 승인을 조정할 리더를 선택할 수 있으며, 이는 `Resources` 필드의 첫 번째 컴퓨터처럼 간단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="0f3dd-204">PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="0f3dd-204">PowerShell sample</span></span> 

<span data-ttu-id="0f3dd-205">다음 샘플은 예약된 이벤트에 대한 메타데이터 서비스를 쿼리하고 처리 중인 각 이벤트를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="0f3dd-206">C\# 샘플</span><span class="sxs-lookup"><span data-stu-id="0f3dd-206">C\# sample</span></span> 

<span data-ttu-id="0f3dd-207">다음 샘플은 메타데이터 서비스와 통신하는 단순한 클라이언트의 샘플입니다</span><span class="sxs-lookup"><span data-stu-id="0f3dd-207">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="0f3dd-208">예약된 이벤트는 다음 데이터 구조를 사용하여 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-208">Scheduled Events can be represented using the following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="0f3dd-209">다음 샘플은 예약된 이벤트에 대한 메타데이터 서비스를 쿼리하고 처리 중인 각 이벤트를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-209">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter to approve executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter to repeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="0f3dd-210">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="0f3dd-210">Python sample</span></span> 

<span data-ttu-id="0f3dd-211">다음 샘플은 예약된 이벤트에 대한 메타데이터 서비스를 쿼리하고 처리 중인 각 이벤트를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-211">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0f3dd-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f3dd-212">Next steps</span></span> 

- <span data-ttu-id="0f3dd-213">[인스턴스 메타데이터 서비스](instance-metadata-service.md)에서 사용 가능한 API에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-213">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="0f3dd-214">[Azure에서 Windows 가상 컴퓨터에 대한 계획된 유지 관리](planned-maintenance.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f3dd-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

