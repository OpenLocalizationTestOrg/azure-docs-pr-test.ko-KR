---
title: "Azure 메타 데이터 서비스로 이벤트 aaaScheduled | Microsoft Docs"
description: "발생 하기 전에 가상 컴퓨터의 이벤트 tooImpactful 동작 합니다."
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="0b43b-103">Azure 메타데이터 서비스 - 예정된 이벤트(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0b43b-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="0b43b-104">미리 보기 toohello 사용 약관을 동의 하는 hello 조건에 사용 가능한 tooyou를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="0b43b-105">자세한 내용은 [Microsoft Azure Preview에 대한 Microsoft Azure 추가 사용 약관](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b43b-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="0b43b-106">예약 된 이벤트 hello Azure 메타 데이터 서비스에서 hello 하위 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="0b43b-107">응용 프로그램에서 이벤트를 준비하고 중단을 제한할 수 있도록 예정된 이벤트(예: 다시 부팅)에 대한 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="0b43b-108">이 기능은 PaaS 및 IaaS를 포함한 모든 Azure Virtual Machine 유형에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="0b43b-109">예약 된 이벤트는 이벤트의 toominimize hello 효과 가상 컴퓨터 시간 tooperform 예방 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="0b43b-110">소개 - Scheduled Events가 필요한 이유</span><span class="sxs-lookup"><span data-stu-id="0b43b-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="0b43b-111">예약 된 이벤트로 인해 서비스에서 단계에 플랫폼 intiated 유지 관리 또는 사용자가 시작한 작업의 toolimit hello 영향을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="0b43b-112">복제 기술을 toomaintain 상태를 사용 하는 다중 인스턴스 작업 인스턴스를 여러 개에서 일어나 고 취약 한 toooutages 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="0b43b-113">이러한 중단으로 인해 비용이 많이 드는 작업(예: 인덱스 다시 빌드) 또는 복제본 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="0b43b-114">대부분의 경우에서 hello 전반적인 서비스 가용성을 향상 시킬 수 있습니다와 같은 정상적인 종료 시퀀스를 수행 하 여 완료 (또는 취소) 진행 중인 트랜잭션은, hello (수동 장애 조치) 클러스터에서 작업 tooother Vm을 다시 할당 하거나 hello를 제거 합니다. 네트워크 부하 분산 장치 풀에서 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="0b43b-115">여기서 예정 된 이벤트에 대 한 관리자에 게 알리는 나 이러한 이벤트를 로깅하는 데 도움이 hello 클라우드에서 호스트 되는 응용 프로그램의 hello 서비스 효율성을 개선 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="0b43b-116">Azure 서비스 메타 데이터 표면 예약 된 이벤트 hello 다음에서 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="0b43b-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="0b43b-117">플랫폼 시작 유지 관리(예: 호스트 OS 롤아웃)</span><span class="sxs-lookup"><span data-stu-id="0b43b-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="0b43b-118">사용자 시작 호출(예: 사용자에 의한 VM 다시 시작 또는 다시 배포)</span><span class="sxs-lookup"><span data-stu-id="0b43b-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="0b43b-119">예약 된 이벤트-hello 기본 사항</span><span class="sxs-lookup"><span data-stu-id="0b43b-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="0b43b-120">Azure 메타 데이터 서비스는 hello VM 내에서 액세스할 수 있는 REST 끝점을 사용 하는 가상 컴퓨터를 실행 하는 방법에 대 한 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="0b43b-121">hello 정보는 불가능 IP를 통해 사용할 수 있으므로 hello VM 외부에 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="0b43b-122">범위</span><span class="sxs-lookup"><span data-stu-id="0b43b-122">Scope</span></span>
<span data-ttu-id="0b43b-123">예약 된 이벤트는 표시 tooall 클라우드 서비스의 가상 컴퓨터 또는 가상 컴퓨터 가용성 집합에 tooall입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="0b43b-124">Hello를 확인 해야 하는 결과적으로, `Resources` 필드에 hello 이벤트 tooidentify Vm toobe 영향을 받는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="0b43b-125">Hello 끝점 검색</span><span class="sxs-lookup"><span data-stu-id="0b43b-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="0b43b-126">Hello 경우 가상 네트워크 (VNet) 내에서 가상 컴퓨터를 만들 위치 hello 메타 데이터 서비스에서 라우팅 불가능 고정 IP를 사용할 수는 `169.254.169.254`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="0b43b-127">추가 논리 hello 가상 컴퓨터 가상 네트워크를 클라우드 서비스 및 클래식 Vm에 대 한 hello 기본 사례 내에서 만들지 않은 경우 필요한 toodiscover hello 끝점 toouse.</span><span class="sxs-lookup"><span data-stu-id="0b43b-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="0b43b-128">어떻게 너무 toothis 샘플 toolearn 참조[hello 호스트 끝점을 검색](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="0b43b-129">버전 관리</span><span class="sxs-lookup"><span data-stu-id="0b43b-129">Versioning</span></span> 
<span data-ttu-id="0b43b-130">hello 인스턴스 메타 데이터 서비스 버전 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0b43b-131">버전은 필수 이며 hello 현재 버전은 `2017-03-01`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0b43b-132">이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기.</span><span class="sxs-lookup"><span data-stu-id="0b43b-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="0b43b-133">이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0b43b-134">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="0b43b-134">Using Headers</span></span>
<span data-ttu-id="0b43b-135">Hello 헤더를 제공 해야 hello 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="0b43b-136">예약된 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="0b43b-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="0b43b-137">hello 예약 된 이벤트에 대 한 요청을 수행 하는 처음으로 Azure 암시적으로 hello 기능을 활성화 가상 컴퓨터에 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="0b43b-138">따라서 지연 된 응답을 tootwo 분의 첫 번째 호출에서 하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="0b43b-139">사용자 시작 유지 관리</span><span class="sxs-lookup"><span data-stu-id="0b43b-139">User Initiated Maintenance</span></span>
<span data-ttu-id="0b43b-140">사용자가 API, CLI hello Azure 포털을 통해 가상 컴퓨터 유지 관리를 시작 하거나, PowerShell 예약 된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="0b43b-141">응용 프로그램에서 tootest hello 유지 관리 준비 논리를 허용 하 고 사용자가 시작한 유지 관리에 대 한 응용 프로그램 tooprepare 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="0b43b-142">가상 컴퓨터를 다시 시작하면 `Reboot` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="0b43b-143">가상 컴퓨터를 다시 배포하면 `Redeploy` 유형의 이벤트가 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0b43b-144">현재는 사용자 시작 유지 관리 작업을 최대 10개까지 동시 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="0b43b-145">이 제한은 예약된 이벤트 일반 공급 이전에 완화될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="0b43b-146">현재는 예약된 이벤트를 실행하는 사용자 시작 유지 관리를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="0b43b-147">구성 기능은 이후 버전에 추가될 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="0b43b-148">Hello API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0b43b-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="0b43b-149">이벤트 쿼리</span><span class="sxs-lookup"><span data-stu-id="0b43b-149">Query for events</span></span>
<span data-ttu-id="0b43b-150">호출 하는 hello 다음을 수행 하 여 예약 된 이벤트를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="0b43b-151">응답에는 예약된 이벤트의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="0b43b-152">빈 배열은 현재 예약된 이벤트가 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="0b43b-153">Hello 경우에서 예약 된 이벤트 인 hello 응답 이벤트의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="0b43b-154">이벤트 속성</span><span class="sxs-lookup"><span data-stu-id="0b43b-154">Event Properties</span></span>
|<span data-ttu-id="0b43b-155">속성</span><span class="sxs-lookup"><span data-stu-id="0b43b-155">Property</span></span>  |  <span data-ttu-id="0b43b-156">설명</span><span class="sxs-lookup"><span data-stu-id="0b43b-156">Description</span></span> |
| - | - |
| <span data-ttu-id="0b43b-157">EventId</span><span class="sxs-lookup"><span data-stu-id="0b43b-157">EventId</span></span> | <span data-ttu-id="0b43b-158">이 이벤트의 GUID(Globally Unique Identifier)입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="0b43b-159">예제:</span><span class="sxs-lookup"><span data-stu-id="0b43b-159">Example:</span></span> <br><ul><li><span data-ttu-id="0b43b-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="0b43b-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="0b43b-161">EventType</span><span class="sxs-lookup"><span data-stu-id="0b43b-161">EventType</span></span> | <span data-ttu-id="0b43b-162">이 이벤트로 인해 발생하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="0b43b-163">값</span><span class="sxs-lookup"><span data-stu-id="0b43b-163">Values:</span></span> <br><ul><li> <span data-ttu-id="0b43b-164">`Freeze`: hello 가상 컴퓨터를 몇 초 동안 예약 된 toopause는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="0b43b-165">hello CPU 일시 중단 되지만 메모리, 열려 있는 파일 또는 네트워크 연결에 대 한 영향은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="0b43b-166">`Reboot`: 가상 컴퓨터를 다시 부팅에 대 한 예약 된 hello (비 영구적인 메모리가 손실).</span><span class="sxs-lookup"><span data-stu-id="0b43b-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="0b43b-167">`Redeploy`: hello 가상 컴퓨터는 예약 된 toomove tooanother 노드 (임시 디스크는 손실 됨).</span><span class="sxs-lookup"><span data-stu-id="0b43b-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="0b43b-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="0b43b-168">ResourceType</span></span> | <span data-ttu-id="0b43b-169">이 이벤트가 영향을 주는 리소스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="0b43b-170">값</span><span class="sxs-lookup"><span data-stu-id="0b43b-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="0b43b-171">리소스</span><span class="sxs-lookup"><span data-stu-id="0b43b-171">Resources</span></span>| <span data-ttu-id="0b43b-172">이 이벤트가 영향을 주는 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-172">List of resources this event impacts.</span></span> <span data-ttu-id="0b43b-173">이 최대 하나의에서 toocontain 컴퓨터 보장 [업데이트 도메인](windows/manage-availability.md), 하지만 hello UD의에서 모든 컴퓨터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="0b43b-174">예제:</span><span class="sxs-lookup"><span data-stu-id="0b43b-174">Example:</span></span> <br><ul><li> <span data-ttu-id="0b43b-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="0b43b-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="0b43b-176">이벤트 상태</span><span class="sxs-lookup"><span data-stu-id="0b43b-176">Event Status</span></span> | <span data-ttu-id="0b43b-177">이 이벤트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-177">Status of this event.</span></span> <br><br> <span data-ttu-id="0b43b-178">값</span><span class="sxs-lookup"><span data-stu-id="0b43b-178">Values:</span></span> <ul><li><span data-ttu-id="0b43b-179">`Scheduled`:이 이벤트는 hello에 지정 된 hello 시간 후 예약 된 toostart `NotBefore` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="0b43b-180">`Started`: 이 이벤트가 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="0b43b-181">더 `Completed` 또는 유사한 상태는 제공 된 적이; hello 이벤트 hello 이벤트가 완료 될 때 더 이상 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="0b43b-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="0b43b-182">NotBefore</span></span>| <span data-ttu-id="0b43b-183">이 시간이 지난 후 이 이벤트가 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="0b43b-184">예제:</span><span class="sxs-lookup"><span data-stu-id="0b43b-184">Example:</span></span> <br><ul><li> <span data-ttu-id="0b43b-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="0b43b-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="0b43b-186">이벤트 예약</span><span class="sxs-lookup"><span data-stu-id="0b43b-186">Event Scheduling</span></span>
<span data-ttu-id="0b43b-187">각 이벤트 예약 된 이벤트 형식에 따라 이후 hello 시간의 최소 양입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="0b43b-188">이 시간은 이벤트의 `NotBefore` 속성에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="0b43b-189">EventType</span><span class="sxs-lookup"><span data-stu-id="0b43b-189">EventType</span></span>  | <span data-ttu-id="0b43b-190">최소 공지</span><span class="sxs-lookup"><span data-stu-id="0b43b-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="0b43b-191">중지</span><span class="sxs-lookup"><span data-stu-id="0b43b-191">Freeze</span></span>| <span data-ttu-id="0b43b-192">15분</span><span class="sxs-lookup"><span data-stu-id="0b43b-192">15 minutes</span></span> |
| <span data-ttu-id="0b43b-193">Reboot</span><span class="sxs-lookup"><span data-stu-id="0b43b-193">Reboot</span></span> | <span data-ttu-id="0b43b-194">15분</span><span class="sxs-lookup"><span data-stu-id="0b43b-194">15 minutes</span></span> |
| <span data-ttu-id="0b43b-195">재배포</span><span class="sxs-lookup"><span data-stu-id="0b43b-195">Redeploy</span></span> | <span data-ttu-id="0b43b-196">10분</span><span class="sxs-lookup"><span data-stu-id="0b43b-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="0b43b-197">이벤트 시작(신속 이동)</span><span class="sxs-lookup"><span data-stu-id="0b43b-197">Starting an event (expedite)</span></span>

<span data-ttu-id="0b43b-198">예정 된 이벤트의 학습 하 고 정상 종료 논리를 완료 하 여 hello 처리 중인 이벤트를 승인할 수 있습니다는 `POST` hello로 toohello 메타 데이터 서비스를 호출할 `EventId`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="0b43b-199">이 tooAzure hello 최소 알림을 줄일 수를 나타냅니다 (가능한 경우) 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="0b43b-200">이벤트를 승인 하면 hello 이벤트 tooproceed 모든 `Resources` hello hello 이벤트도 인해 가상 컴퓨터 뿐 아니라 hello 이벤트에서입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="0b43b-201">따라서 수도 있습니다 tooelect hello hello에 첫 번째 컴퓨터 처럼 간단할 수도 있음 리더 toocoordinate hello 승인을 `Resources` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="0b43b-202">샘플</span><span class="sxs-lookup"><span data-stu-id="0b43b-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="0b43b-203">PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="0b43b-203">PowerShell Sample</span></span> 

<span data-ttu-id="0b43b-204">hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.</span><span class="sxs-lookup"><span data-stu-id="0b43b-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="0b43b-205">C\# 샘플</span><span class="sxs-lookup"><span data-stu-id="0b43b-205">C\# Sample</span></span> 

<span data-ttu-id="0b43b-206">hello 다음 예제는 hello 메타 데이터 서비스와 통신 하는 간단한 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="0b43b-207">데이터 구조를 따르면 hello를 사용 하 여 예약 된 이벤트를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-207">Scheduled Events can be represented using hello following data structures:</span></span>

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

<span data-ttu-id="0b43b-208">hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.</span><span class="sxs-lookup"><span data-stu-id="0b43b-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter tooapprove executing events\n");
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

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="0b43b-209">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="0b43b-209">Python Sample</span></span> 

<span data-ttu-id="0b43b-210">hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.</span><span class="sxs-lookup"><span data-stu-id="0b43b-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0b43b-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b43b-211">Next Steps</span></span> 

- <span data-ttu-id="0b43b-212">Hello hello에서 사용할 수 있는 Api에 대해 자세히 읽어보세요 [인스턴스 메타 데이터 서비스](virtual-machines-instancemetadataservice-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="0b43b-213">[Azure에서 Windows 가상 컴퓨터에 대한 계획된 유지 관리](windows/planned-maintenance.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="0b43b-214">[Azure에서 Linux 가상 컴퓨터에 대한 계획된 유지 관리](linux/planned-maintenance.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b43b-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
