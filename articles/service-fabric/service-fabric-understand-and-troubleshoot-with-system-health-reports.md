---
title: "시스템 상태 보고서 문제 해결 | Microsoft Docs"
description: "Azure 서비스 패브릭 구성 요소에서 보낸 상태 보고서와 클러스터 또는 응용 프로그램 문제 해결에 대한 사용을 설명합니다."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="9c455-103">시스템 상태 보고서를 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9c455-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="9c455-104">Azure 서비스 패브릭 구성 요소가 클러스터 내의 모든 엔터티에 대해 즉각적으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="9c455-105">[Health 스토어](service-fabric-health-introduction.md#health-store) 는 시스템 보고서를 기반으로 엔터티를 만들고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="9c455-106">또한 엔터티 상호 작용을 캡처하는 계층 구조에서 보고서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="9c455-107">상태 관련 개념을 이해하려면 [Service Fabric 상태 모델](service-fabric-health-introduction.md)을 자세히 읽어봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="9c455-108">시스템 상태 보고서는 상태를 통해 클러스터 및 응용 프로그램의 기능 및 플래그 문제에 대한 가시성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="9c455-109">응용 프로그램 및 서비스의 경우, 시스템 상태 보고서는 서비스 패브릭 관점에서 엔터티가 올바르게 구현되고 동작하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="9c455-110">보고서는 응답이 없는 프로세스의 감지 또는 서비스의 비즈니스 논리의 상태 모니터링은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="9c455-111">사용자 서비스는 논리에 고유한 정보로 건강 데이터를 보강할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="9c455-112">Watchdogs 상태 보고서는 시스템 구성 요소가 엔터티를 만든 *후*에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="9c455-113">엔터티가 삭제되면 Health 스토어가 연결된 모든 상태 보고서를 자동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="9c455-114">엔터티의 새 인스턴스를 만들 때에도 동일합니다(예를 들어 새로운상태 저장 영속 서비스 복제 인스턴스 생성).</span><span class="sxs-lookup"><span data-stu-id="9c455-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="9c455-115">이전 인스턴스와 연결된 모든 보고서는 삭제되고 저장소에서 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="9c455-116">시스템 구성 요소 보고서는 "**System.**" 접두사로 시작되는 원본에 의해</span><span class="sxs-lookup"><span data-stu-id="9c455-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="9c455-117">식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-117">prefix.</span></span> <span data-ttu-id="9c455-118">잘못된 매개 변수가 있는 보고서가 거부되므로 Watchdogs는 소스에 대해 동일한 접두사를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="9c455-119">일부 시스템 보고서를 검토하여 이들이 어떻게 트리거되고 이들이 나타내는 발생 가능한 문제를 수정하는 방법을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="9c455-120">서비스 패브릭이 클러스터 및 응용 프로그램에서 일어나는 상황에 대한 가시성을 향상시켜주는 관심 조건에 대한 보고서를 계속해서 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="9c455-121">기존 보고서를 더 상세한 정보로 강화하여 더 신속하게 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="9c455-122">클러스터 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-122">Cluster system health reports</span></span>
<span data-ttu-id="9c455-123">클러스터 상태 엔터티는 Health 스토어에서 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="9c455-124">모든 것이 제대로 작동하면 시스템 보고서는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="9c455-125">환경 손실</span><span class="sxs-lookup"><span data-stu-id="9c455-125">Neighborhood loss</span></span>
<span data-ttu-id="9c455-126">**System.Federation** 은 환경 손실을 감지하면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="9c455-127">보고서는 개별 노드에서 나오며 노드 ID는 속성 이름에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="9c455-128">전체 Service Fabric 링에서 하나의 환경이 손실되면 일반적으로 두 개의 이벤트를 예상할 수 있습니다(간격의 양측에서 보고함).</span><span class="sxs-lookup"><span data-stu-id="9c455-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="9c455-129">더 많은 환경이 손실된 경우 더 많은 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="9c455-130">보고서는 전역 임대 시간 제한을 TTL(Time to live)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="9c455-131">조건이 활성인 한 보고서는 TTL 기간의 절반마다 다시 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="9c455-132">이벤트는 만료되면 자동으로 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="9c455-133">보고 노드가 다운되었더라도 보고서가 Health 스토어에서 제대로 정리된 것을 만료된 동작이 보장하면 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="9c455-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="9c455-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="9c455-135">**Property**: **환경**으로 시작되고 노드 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="9c455-136">**다음 단계**: 환경이 손실된 이유를 조사합니다.(예를 들어 클러스터 노드 간 통신을 확인합니다)</span><span class="sxs-lookup"><span data-stu-id="9c455-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="9c455-137">노드 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-137">Node system health reports</span></span>
<span data-ttu-id="9c455-138">장애 조치(Failover) 관리자 서비스를 나타내는 **System.FM**은 클러스터 노드에 대한 정보를 관리하는 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="9c455-139">모든 노드는 상태를 보여주는 System.FM로부터 하나의 보고서를 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="9c455-140">노드 상태가 제거되면 노드 엔터티도 제거됩니다( [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)참조).</span><span class="sxs-lookup"><span data-stu-id="9c455-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="9c455-141">노드 위/아래</span><span class="sxs-lookup"><span data-stu-id="9c455-141">Node up/down</span></span>
<span data-ttu-id="9c455-142">System.FM은 노드가 링에 조인하는 경우 확인으로 보고합니다.(실행 중)</span><span class="sxs-lookup"><span data-stu-id="9c455-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="9c455-143">노드가 링에서 분리하는 경우 오류를 보고합니다.(업그레이드이든 단순히 실패한 것이든 중단되었습니다)</span><span class="sxs-lookup"><span data-stu-id="9c455-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="9c455-144">Health 스토어에서 작성한 상태 계층이 System.FM 노드 보고서와의 상관관계에 따라, 배포된 엔터티에 대해 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="9c455-145">배포된 모든 엔터티의 가상 부모를 노드로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="9c455-146">엔터티와 연결된 인스턴스와 동일한 인스턴스와 함께 노드가 가동 중인 것으로 System.FM에 의해 보고되면 해당 노드에 배포된 엔터티가 쿼리를 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="9c455-147">System.FM에서 노드가 다운되었거나 다시 시작한 것을 보고하면(새로운 인스턴스) Health 스토어가 다운 노드 또는 이전 노드 인스턴스에서만 존재할 수 있는 배포된 엔터티를 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="9c455-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="9c455-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="9c455-149">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="9c455-149">**Property**: State</span></span>
* <span data-ttu-id="9c455-150">**다음 단계**: 업그레이드를 위해 노드가 중지된 경우 업그레이드되면 돌아와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="9c455-151">이 경우에 상태를 확인으로 다시 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="9c455-152">노드가 다시 돌아오지 않거나 실패하면 문제는 자세한 조사가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="9c455-153">다음 예제는 노드 실행을 위해 상태가 정상인 System.FM 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="9c455-154">인증서가 만료</span><span class="sxs-lookup"><span data-stu-id="9c455-154">Certificate expiration</span></span>
<span data-ttu-id="9c455-155">**System.FabricNode** 는 노드에 의해 사용되는 인증서가 만료가 가까워질 경우 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="9c455-156">노드당 **Certificate_cluster**, **Certificate_server** 및 **Certificate_default_client**의 3가지 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="9c455-157">적어도 2주 후에 만료될 때 보고서 상태는 확인입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="9c455-158">2주 이내에 만료되면 보고서 형식은 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="9c455-159">이러한 이벤트의 TTL은 무한대이며 노드가 클러스터를 벗어나면 제거됩니다</span><span class="sxs-lookup"><span data-stu-id="9c455-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="9c455-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="9c455-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="9c455-161">**Property**: **인증서**로 시작하고 인증서 유형에 대한 추가 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="9c455-162">**다음 단계**: 만료가 가까운 경우 인증서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="9c455-163">부하 용량 위반</span><span class="sxs-lookup"><span data-stu-id="9c455-163">Load capacity violation</span></span>
<span data-ttu-id="9c455-164">노드 용량 위반이 발견되면 서비스 패브릭 부하 분산 장치에서 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="9c455-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="9c455-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="9c455-166">**Property**: **용량**으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="9c455-167">**다음 단계**: 제공된 메트릭을 확인하고 노드에서 현재 용량을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="9c455-168">응용 프로그램 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-168">Application system health reports</span></span>
<span data-ttu-id="9c455-169">클러스터 관리자 서비스를 나타내는 **System.CM**은 응용 프로그램에 대한 정보를 관리하는 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="9c455-170">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="9c455-170">State</span></span>
<span data-ttu-id="9c455-171">응용 프로그램을 만들거나 업데이트할 때 System.CM은 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="9c455-172">저장소에서 제거될 수 있도록 응용 프로그램이 언제 삭제되었는지를 Health 스토어에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="9c455-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="9c455-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="9c455-174">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="9c455-174">**Property**: State</span></span>
* <span data-ttu-id="9c455-175">**다음 단계**: 응용 프로그램이 만들어지거나 업데이트된 경우 클러스터 관리자 상태 보고서를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="9c455-176">그렇지 않은 경우 쿼리를 발행하여 응용 프로그램의 상태를 확인합니다(예: PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="9c455-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="9c455-177">다음 예제는 **fabric:/WordCount** 응용 프로그램에 대한 상태 이벤트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="9c455-178">서비스 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-178">Service system health reports</span></span>
<span data-ttu-id="9c455-179">장애 조치(failover) 관리자 서비스를 나타내는 **System.FM**은 서비스에 대한 정보를 관리하는 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="9c455-180">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="9c455-180">State</span></span>
<span data-ttu-id="9c455-181">System.FM은 서비스가 만들어질 때 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="9c455-182">서비스가 삭제될 때 Health 스토어에서 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="9c455-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="9c455-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="9c455-184">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="9c455-184">**Property**: State</span></span>

<span data-ttu-id="9c455-185">다음 예제는 서비스 **fabric:/WordCount/WordCountWebService**에 상태 이벤트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="9c455-186">서비스 상관 관계 오류 </span><span class="sxs-lookup"><span data-stu-id="9c455-186">Service correlation error</span></span>
<span data-ttu-id="9c455-187">**System.PLB**는 다른 서비스와 상관되는 서비스를 업데이트할 때 선호도 체인이 만들어지는 것을 발견하면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="9c455-188">업데이트에 성공하면 보고서가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="9c455-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="9c455-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="9c455-190">**속성**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="9c455-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="9c455-191">**다음 단계**: 상관된 서비스 설명을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="9c455-192">파티션 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-192">Partition system health reports</span></span>
<span data-ttu-id="9c455-193">장애 조치(failover) 관리자 서비스를 나타내는 **System.FM**은 서비스 파티션에 대한 정보를 관리하는 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="9c455-194">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="9c455-194">State</span></span>
<span data-ttu-id="9c455-195">System.FM은 파티션이 생성되고 정상적이면 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="9c455-196">파티션이 삭제될 때 Health 스토어에서 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="9c455-197">파티션이 최소 복제본 수 이하인 경우 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="9c455-198">파티션이 최소 복제본 개수 이하는 아니지만 대상 복제본 개수 이하라면 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="9c455-199">파티션이 쿼럼 손실인 경우 System.FM이 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="9c455-200">기타 중요한 이벤트는 재구성이 예상보다 오래 걸리며 빌드가 예상보다 오래 걸리는 경우 경고를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="9c455-201">예상되는 빌드 및 재구성 시간을 서비스 시나리오에 따라 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="9c455-202">예를 들어 서비스에 SQL Database와 같은 테라바이트 상태가 있는 경우 작은 양의 상태가 있는 서비스보다 빌드가 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="9c455-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="9c455-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="9c455-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="9c455-204">**Property**: State</span></span>
* <span data-ttu-id="9c455-205">**다음 단계**: 상태가 정상이 아니라면 일부 복제본이 주 또는 보조에 올바르게 생성되거나 열리고 승격되지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="9c455-206">대부분의 경우 근본 원인은 열기 또는 변경 역할 구현에서 서비스 버그입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="9c455-207">다음 예제는 정상 파티션을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="9c455-208">다음 예제는 대상 복제본 개수 이하인 파티션의 상태를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="9c455-209">다음 단계는 파티션이 구성된 방식을 보여 주는 파티션 설명을 가져옵니다. 여기서 **MinReplicaSetSize**는 3이고 **TargetReplicaSetSize**는 7입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="9c455-210">그런 다음 클러스터에 있는 노드 수를 가져옵니다.5</span><span class="sxs-lookup"><span data-stu-id="9c455-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="9c455-211">따라서 이 경우 복제본의 목표 수가 사용 가능한 노드 수보다 더 높으므로 두 개의 복제본을 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="9c455-212">복제본 제약 조건 위반</span><span class="sxs-lookup"><span data-stu-id="9c455-212">Replica constraint violation</span></span>
<span data-ttu-id="9c455-213">**System.PLB**는 복제본 제약 조건 위반을 감지하고 일부 파티션 복제본을 배치할 수 없는 경우 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="9c455-214">보고서 상세 정보에는 복제본 배치에 방해가 되는 제약과 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="9c455-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="9c455-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="9c455-216">**Property**: **ReplicaConstraintViolation**으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="9c455-217">복제본 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-217">Replica system health reports</span></span>
<span data-ttu-id="9c455-218">재구성 에이전트 구성 요소를 나타내는 **System.RA**는 복제본 상태의 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="9c455-219">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="9c455-219">State</span></span>
<span data-ttu-id="9c455-220">**System.RA**는 복제본이 만들어지면 정상으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="9c455-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="9c455-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="9c455-222">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="9c455-222">**Property**: State</span></span>

<span data-ttu-id="9c455-223">다음 예제는 정상 복제본을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="9c455-224">복제본 열린 상태</span><span class="sxs-lookup"><span data-stu-id="9c455-224">Replica open status</span></span>
<span data-ttu-id="9c455-225">이 상태 보고서에 대한 설명에는 API 호출이 호출된 경우 시작 시간(협정 세계시)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="9c455-226">복제본 열기가 구성된 기간(기본: 30분)보다 오래 걸릴 경우 **System.RA**는 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="9c455-227">API가 서비스 가용성에 영향을 주는 경우 보고서가 훨씬 더 빠르게 발행됩니다.(구성 가능한 간격, 기본 30초)</span><span class="sxs-lookup"><span data-stu-id="9c455-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="9c455-228">측정된 시간에는 복제기 열기 및 서비스 열기에 소요된 시간이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="9c455-229">열기가 완료되면 속성이 확인으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="9c455-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="9c455-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="9c455-231">**Property**에 상태 이벤트를 보여 줍니다. **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="9c455-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="9c455-232">**다음 단계**: 성능 상태가 정상이 아닌 경우 복제본의 열기가 예상보다 오래 걸린 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="9c455-233">느린 서비스 API 호출</span><span class="sxs-lookup"><span data-stu-id="9c455-233">Slow service API call</span></span>
<span data-ttu-id="9c455-234">**System.RAP** 및 **System.Replicator**는 사용자 서비스 코드에 대한 호출이 구성된 시간보다 오래 걸리는 경우 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="9c455-235">이 경고는 호출이 완료되면 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="9c455-236">**SourceId**: System.RAP 또는 System.Replicator</span><span class="sxs-lookup"><span data-stu-id="9c455-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="9c455-237">**Property**: 느린 API의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="9c455-238">이 설명은 API가 보류된 시간에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="9c455-239">**다음 단계**: 호출이 예상보다 오래 걸리는 이유를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="9c455-240">다음 예제에서는 쿼럼 손실 내 파티션을 보여주고 이유를 파악하기 위해 실행된 조사 단계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="9c455-241">복제본 하나는 경고 성능 상태를 가지고 있으므로 상태를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="9c455-242">이것은 서비스 작업이 예상보다 오래 걸림을 보여줍니다. System.RAP에서 보고된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="9c455-243">이 정보를 받은 후에 다음 단계는 서비스 코드를 살펴보고 조사하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="9c455-244">이 경우, 상태 저장 서비스의 **RunAsync** 구현이 처리되지 않은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="9c455-245">복제본은 재활용되므로 경고 상태에서 어떤 복제본도 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="9c455-246">상태 가져오기를 다시 시도하고 복제본 ID에서 차이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="9c455-247">경우에 따라 재시도가 단서를 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="9c455-248">디버거 하에서 결함이 있는 응용 프로그램을 시작하는 경우 진단 이벤트 창에서 RunAsync로부터 thow된 예외를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Visual Studio 2015 진단 이벤트: fabric:/HelloWorldStatefulApplication에서 RunAsync 실패][1]

<span data-ttu-id="9c455-250">Visual Studio 2015 진단 이벤트: **fabric:/HelloWorldStatefulApplication**에서 RunAsync 실패</span><span class="sxs-lookup"><span data-stu-id="9c455-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="9c455-251">복제 큐 전체</span><span class="sxs-lookup"><span data-stu-id="9c455-251">Replication queue full</span></span>
<span data-ttu-id="9c455-252">**System.Replicator**는 복제본 큐가 가득 차면 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="9c455-253">보통은 기본 데이터베이스에서는 하나 이상의 보조 복제본이 작업을 승인하는 속도가 느리기 때문에 복제본 큐가 가득차게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="9c455-254">보조 데이터베이스에서는 서비스가 작업에 적용하는 속도가 느릴 때 일반적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="9c455-255">큐가 더 이상 가득 차지 않으면 경고가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="9c455-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="9c455-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="9c455-257">**Property**: 복제본의 역할에 따라 **PrimaryReplicationQueueStatus** 또는 **SecondaryReplicationQueueStatus**입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="9c455-258">느린 이름 지정 작업</span><span class="sxs-lookup"><span data-stu-id="9c455-258">Slow Naming operations</span></span>
<span data-ttu-id="9c455-259">**System.NamingService**는 이름 지정 작업이 허용 가능한 시간보다 오래 걸리는 경우 주 복제본에 해당 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="9c455-260">이름 지정 작업의 예는 [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 또는 [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="9c455-261">FabricClient에서 더 많은 메서드를 찾을 수 있습니다. 예를 들어 [서비스 관리 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) 또는 [속성 관리 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="9c455-262">이름 지정 서비스는 클러스터의 위치에 서비스 이름을 확인하고 사용자가 서비스 이름 및 속성을 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="9c455-263">서비스 패브릭 분할된 지속형 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="9c455-264">파티션 중 하나는 모든 Service Fabric 이름 및 서비스에 대한 메타데이터를 포함하는 기관 소유자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="9c455-265">서비스 패브릭 이름은 이름 소유자 파티션이라는 다른 파티션에 매핑되므로 서비스는 확장 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="9c455-266">[이름 지정 서비스](service-fabric-architecture.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="9c455-267">이름 지정 작업이 예상보다 오래 걸리는 경우 작업은 *작업을 사용하는 이름 지정 서비스 파티션의 주 복제본*의 경고 보고서로 플래그 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="9c455-268">작업이 성공적으로 완료되면 경고는 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="9c455-269">오류와 함께 작업이 완료되면 상태 보고서는 오류에 대한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="9c455-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="9c455-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="9c455-271">**Property**: 접두사 **Duration_**으로 시작하고 느린 작업 및 작업이 적용되는 Service Fabric 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="9c455-272">예를 들어 이름 fabric:/MyApp/MyService에서 서비스 만들기가 너무 오래 걸리는 경우 속성은 Duration_AOCreateService.fabric:/MyApp/MyService입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="9c455-273">AO는 이 이름 및 작업에 대한 이름 지정 파티션의 역할을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="9c455-274">**다음 단계**: 명명 작업이 실패하는 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="9c455-275">각 작업에는 다른 원인이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-275">Each operation can have different root causes.</span></span> <span data-ttu-id="9c455-276">예를 들어 응용 프로그램 호스트가 서비스 코드의 사용자 버그로 인해 노드에 충돌이 발생하기 때문에 서비스 삭제는 노드에서 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="9c455-277">다음 예제는 서비스 만들기 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-277">The following example shows a create service operation.</span></span> <span data-ttu-id="9c455-278">작업이 구성된 기간보다 오래 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="9c455-279">AO는 다시 시도하고 NO로 작업을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="9c455-280">NO에서 시간 제한이 있는 마지막 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="9c455-281">이 경우 동일한 복제본은 AO 및 NO 역할에 대해 주 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="9c455-282">DeployedApplication 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="9c455-283">**System.Hosting** 은 배포된 엔터티에 대한 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="9c455-284">활성화</span><span class="sxs-lookup"><span data-stu-id="9c455-284">Activation</span></span>
<span data-ttu-id="9c455-285">System.Hosting은 응용 프로그램이 노드에서 성공적으로 활성화되면 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="9c455-286">그렇지 않으면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="9c455-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-288">**Property**: Activation(롤아웃 버전 포함)</span><span class="sxs-lookup"><span data-stu-id="9c455-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="9c455-289">**다음 단계**: 응용 프로그램이 비정상인 경우 활성화에 실패한 이유를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="9c455-290">다음 예제는 성공적인 활성화를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="9c455-291">다운로드</span><span class="sxs-lookup"><span data-stu-id="9c455-291">Download</span></span>
<span data-ttu-id="9c455-292">**System.Hosting** 은 응용 프로그램 패키지 다운로드에 실패하면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="9c455-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-294">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="9c455-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="9c455-295">**다음 단계**: 노드에서 다운로드에 실패한 이유를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="9c455-296">DeployedServicePackage 시스템 상태 보고서</span><span class="sxs-lookup"><span data-stu-id="9c455-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="9c455-297">**System.Hosting** 은 배포된 엔터티에 대한 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="9c455-298">서비스 패키지 활성화</span><span class="sxs-lookup"><span data-stu-id="9c455-298">Service package activation</span></span>
<span data-ttu-id="9c455-299">System.Hosting은 노드에서 서비스 패키지 활성화가 성공하면 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="9c455-300">그렇지 않으면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="9c455-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-302">**Property**: Activation</span><span class="sxs-lookup"><span data-stu-id="9c455-302">**Property**: Activation</span></span>
* <span data-ttu-id="9c455-303">**다음 단계**: 활성화가 실패한 이유를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="9c455-304">코드 패키지 활성화</span><span class="sxs-lookup"><span data-stu-id="9c455-304">Code package activation</span></span>
<span data-ttu-id="9c455-305">**System.Hosting** 은 활성화가 성공한 경우 각 코드 패키지에 대해 확인을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="9c455-306">활성화에 실패하는 경우 구성된 대로 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="9c455-307">**CodePackage**가 활성화에 실패하거나 구성된 **CodePackageHealthErrorThreshold**보다 큰 오류와 함께 종료되면 호스팅이 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="9c455-308">서비스 패키지에 여러 코드 패키지가 있다면 각 패키지에 대해 생성된 활성화 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="9c455-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-310">**Property** : 접두사 **CodePackageActivation**을 사용하고 코드 패키지 및 진입점의 이름을 **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** 로 포함합니다 (예: **CodePackageActivation:Code:SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="9c455-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="9c455-311">서비스 유형 등록</span><span class="sxs-lookup"><span data-stu-id="9c455-311">Service type registration</span></span>
<span data-ttu-id="9c455-312">**System.Hosting** 이 정상 상태로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="9c455-313">등록이 제시간에 완료되지 않으면 오류를 보고합니다( **ServiceTypeRegistrationTimeout**을 사용하여 구성된 대로).</span><span class="sxs-lookup"><span data-stu-id="9c455-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="9c455-314">런타임은 닫혀 있는 경우 서비스 유형이 노드에서 등록 해제되고 호스팅이 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="9c455-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-316">**Property**: **ServiceTypeRegistration** 접두사를 사용하고 서비스 유형 이름을 포함합니다(예: **ServiceTypeRegistration:FileStoreServiceType**).</span><span class="sxs-lookup"><span data-stu-id="9c455-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="9c455-317">다음 예제는 정상으로 배포된 서비스 패키지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="9c455-318">다운로드</span><span class="sxs-lookup"><span data-stu-id="9c455-318">Download</span></span>
<span data-ttu-id="9c455-319">**System.Hosting** 이 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="9c455-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-321">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="9c455-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="9c455-322">**다음 단계**: 노드에서 다운로드에 실패한 이유를 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="9c455-323">유효성 검사 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9c455-323">Upgrade validation</span></span>
<span data-ttu-id="9c455-324">**System.Hosting** 은 업그레이드 중에 유효성 검사에 실패하거나 노드에서 업그레이드에 실패하면 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="9c455-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="9c455-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="9c455-326">**Property**: **FabricUpgradeValidation** 접두사를 포함하고 업그레이드 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="9c455-327">**Description**: 발생한 오류를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9c455-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c455-328">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c455-328">Next steps</span></span>
[<span data-ttu-id="9c455-329">서비스 패브릭 상태 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="9c455-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="9c455-330">서비스 상태를 보고 및 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="9c455-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="9c455-331">로컬로 서비스 모니터링 및 진단</span><span class="sxs-lookup"><span data-stu-id="9c455-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="9c455-332">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9c455-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

