---
title: "Azure Service Fabric 엔터티에서 집계한 상태를 보는 방법 | Microsoft Docs"
description: "상태 쿼리 및 일반 쿼리를 통해 Azure 서비스 패브릭 엔터티에서 집계한 상태를 쿼리, 확인 및 평가하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="acd53-103">서비스 패브릭 상태 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="acd53-103">View Service Fabric health reports</span></span>
<span data-ttu-id="acd53-104">Azure Service Fabric은 시스템 구성 요소와 워치독이 모니터링하는 로컬 조건을 보고할 수 있는 상태 엔터티가 있는 [상태 모델](service-fabric-health-introduction.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="acd53-105">[상태 저장소](service-fabric-health-introduction.md#health-store) 는 모든 상태 데이터를 집계하여 엔터티가 정상인지 여부를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="acd53-106">자동으로 클러스터는 시스템 구성 요소에 의해 전송되는 상태 보고서로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="acd53-107">추가 정보는 [시스템 상태 보고서를 사용하여 문제 해결](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd53-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="acd53-108">서비스 패브릭은 엔터티의 집계한 상태를 가져올 수 있는 여러 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="acd53-109">[서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 또는 기타 시각화 도구</span><span class="sxs-lookup"><span data-stu-id="acd53-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="acd53-110">상태 쿼리(PowerShell, API 또는 REST를 통해)</span><span class="sxs-lookup"><span data-stu-id="acd53-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="acd53-111">속성 중 하나로 상태를 가지고 있는 엔터티 목록을 반환하는 일반 쿼리(PowerShell, API 또는 REST를 통해)</span><span class="sxs-lookup"><span data-stu-id="acd53-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="acd53-112">이러한 옵션을 설명하기 위해 5개의 노드와 [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp)이 있는 로컬 클러스터를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="acd53-113">**fabric:/WordCount** 응용 프로그램에는 상태 저장 서비스 유형 `WordCountServiceType` 및 상태 비저장 서비스 유형 `WordCountWebServiceType` 등, 두 기본 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="acd53-114">`ApplicationManifest.xml`을 상태 저장 서비스에 대해 7개의 대상 복제본과 1개의 파티션을 요구하도록 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="acd53-115">클러스터에는 노드가 5개뿐이라 목표 수에 미달하므로 시스템 구성 요소는 서비스 파티션에 대해 경고를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="acd53-116">서비스 패브릭 탐색기 내 상태</span><span class="sxs-lookup"><span data-stu-id="acd53-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="acd53-117">서비스 패브릭 탐색기는 클러스터의 시각적 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="acd53-118">아래 이미지에서 다음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="acd53-119">속성 **가용성**에 대해 **MyWatchdog**에서 보고한 오류 이벤트가 있으므로 응용 프로그램 **fabric:/WordCount**가 빨간색(오류 시)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="acd53-120">해당 서비스 중 하나인 **패브릭:/WordCount/WordCountService** 가 노란색입니다(경고 시).</span><span class="sxs-lookup"><span data-stu-id="acd53-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="acd53-121">서비스는 7개의 복제본으로 구성되나 클러스터에는 5개의 노드가 있으므로 두 복제본을 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="acd53-122">여기에 표시되지 않았지만 서비스 파티션은 `System.FM`에서의 시스템 보고(`Partition is below target replica or instance count`) 때문에 노란색입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="acd53-123">노란색 파티션은 노란색 서비스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="acd53-124">클러스터는 빨간색 응용 프로그램으로 인해 빨간색입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="acd53-125">평가는 클러스터 매니페스트 및 응용 프로그램 매니페스트의 기본 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="acd53-126">엄격한 정책이며 오류를 용납하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="acd53-127">서비스 패브릭 탐색기로 클러스터 보기:</span><span class="sxs-lookup"><span data-stu-id="acd53-127">View of the cluster with Service Fabric Explorer:</span></span>

![서비스 패브릭 탐색기로 클러스터 보기.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="acd53-129">[서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="acd53-130">상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="acd53-130">Health queries</span></span>
<span data-ttu-id="acd53-131">서비스 패브릭은 각각의 지원되는 [엔터티 유형](service-fabric-health-introduction.md#health-entities-and-hierarchy)에 대해 상태 쿼리를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="acd53-132">이러한 항목은 [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlet 및 REST의 메서드를 사용하여 API를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="acd53-133">이러한 쿼리는 집계된 성능 상태, 엔터티 상태 이벤트, 자식 상태(해당되는 경우), 엔터티가 정상이 아닐 때 비정상적 평가 및 자식 상태 통계(해당되는 경우) 등을 포함한 엔터티에 대한 완전한 상태 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="acd53-134">상태 엔터티는 Health 스토어에서 완전히 채워지면 사용자에게 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="acd53-135">엔터티는 활성화 상태이고(삭제되지 않음) 시스템 보고서를 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="acd53-136">또한 계층 구조 체인에서 부모 엔터티는 시스템 보고서를 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="acd53-137">이러한 조건 중 하나라도 만족되지 않으면 상태 쿼리가 엔터티가 반환되지 않는 이유를 보여 주는 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound`와 함께 [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="acd53-138">상태 쿼리는 엔터티 유형에 따라 달라지는 엔터티 식별자를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="acd53-139">쿼리는 옵션인 상태 정책 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="acd53-140">상태 정책이 지정되지 않으면 클러스터 또는 응용 프로그램 매니페스트의 [상태 정책](service-fabric-health-introduction.md#health-policies) 이 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="acd53-141">매니페스트가 상태 정책에 대한 정의를 포함하지 않을 경우 평가에 기본 상태 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="acd53-142">기본 상태 정책에는 오류가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="acd53-143">또한 쿼리는 지정된 필터를 유지하는 부분 자녀 또는 이벤트만 반환하기 위한 필터를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="acd53-144">다른 필터에서는 하위 통계 제외가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="acd53-145">출력 필터는 서버 쪽에 적용되므로 메시지 회신 크기가 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="acd53-146">클라이언트 쪽에서 필터를 적용하는 것보다 반환된 데이터를 제한하는 출력 필터를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="acd53-147">엔터티의 상태는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-147">An entity's health contains:</span></span>

* <span data-ttu-id="acd53-148">엔터티의 집계된 성능 상태.</span><span class="sxs-lookup"><span data-stu-id="acd53-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="acd53-149">엔터티 상태 보고서, 자녀 상태(해당되는 경우) 및 상태 정책을 기반으로 Health 스토어에 의해 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="acd53-150">[엔터티 상태 평가](service-fabric-health-introduction.md#health-evaluation)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="acd53-151">엔터티에 대한 상태 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-151">The health events on the entity.</span></span>
* <span data-ttu-id="acd53-152">자녀를 가질 수 있는 엔터티에 대한 모든 자녀의 성능 상태 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="acd53-153">성능 상태에는 엔터티 식별자와 집계된 성능 상태가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="acd53-154">자녀에 대한 완전한 상태를 얻으려면 자녀 엔터티 유형에 대한 쿼리 상태를 호출하고 자녀 식별자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="acd53-155">엔터티가 비정상일 경우 비정상인 평가는 엔터티의 상태를 트리거한 보고서를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="acd53-156">평가는 재귀적이며 현재 상태를 트리거한 자식 상태 평가를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="acd53-157">예를 들어, 워치독이 복제본에 대해 오류를 보고했습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="acd53-158">응용 프로그램 상태는 비정상 서비스로 인해 비정상 평가를 표시하며, 서비스는 파티션 오류로 인해 비정상 상태가 되고, 파티션은 복제본 오류로 인해 비정상 상태가 되며, 복제본은 다시 워치독 오류 상태 보고서로 인해 비정상 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="acd53-159">자식이 있는 엔터티의 모든 자식 유형에 대한 상태 통계.</span><span class="sxs-lookup"><span data-stu-id="acd53-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="acd53-160">예를 들어, 클러스터 상태는 클러스터의 총 응용 프로그램, 서비스, 파티션, 복제본 및 배포 엔터티수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="acd53-161">서비스 상태는 특정 서비스의 총 파티션 및 복제본 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="acd53-162">클러스터 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-162">Get cluster health</span></span>
<span data-ttu-id="acd53-163">클러스터 엔터티의 상태를 반환하고 응용 프로그램 및 노드의 상태를 포함합니다(클러스터의 자녀).</span><span class="sxs-lookup"><span data-stu-id="acd53-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="acd53-164">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-164">Input:</span></span>

* <span data-ttu-id="acd53-165">[옵션] 노드 및 클러스터 이벤트를 평가하는 데 사용되는 클러스터 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="acd53-166">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 상태 정책이 있는 응용 프로그램 상태 정책 맵.</span><span class="sxs-lookup"><span data-stu-id="acd53-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="acd53-167">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트, 노드 및 응용 프로그램에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-168">모든 이벤트, 노드 및 응용 프로그램은 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="acd53-169">[선택 사항] 상태 통계를 제외하는 필터</span><span class="sxs-lookup"><span data-stu-id="acd53-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="acd53-170">[선택 사항] 상태 통계에 fabric:/System 상태 통계를 포함하는 필터.</span><span class="sxs-lookup"><span data-stu-id="acd53-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="acd53-171">상태 통계가 제외되지 않는 경우에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="acd53-172">기본적으로 상태 통계에는 시스템 응용 프로그램이 아닌 사용자 응용 프로그램에 대한 통계만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-173">API</span><span class="sxs-lookup"><span data-stu-id="acd53-173">API</span></span>
<span data-ttu-id="acd53-174">클러스터 상태를 얻으려면 **HealthManager**에서 `FabricClient`를 만들고 [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="acd53-175">다음 호출은 클러스터 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="acd53-176">다음 코드는 노드 및 응용 프로그램에 대한 사용자 지정 클러스터 상태 정책 및 필터를 사용하여 클러스터 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="acd53-177">상태 통계가 fabric:/System 통계를 포함하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="acd53-178">입력 정보를 포함하는 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="acd53-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-179">PowerShell</span></span>
<span data-ttu-id="acd53-180">클러스터 상태를 가져오려는 cmdlet은 [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="acd53-181">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-182">클러스터의 상태는 설명된 대로 구성된 5개의 노드 및 시스템 응용 프로그램 및 fabric:/WordCount입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="acd53-183">다음 cmdlet은 기본 상태 정책을 사용하여 클러스터 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="acd53-184">fabric:/WordCount 응용 프로그램이 경고이기 때문에 집계된 성능 상태는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="acd53-185">비정상 평가가 집계된 상태를 트리거한 조건을 어떻게 자세히 제공하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="acd53-186">다음 PowerShell cmdlet이 사용자 지정 응용 프로그램 정책을 사용하여 클러스터의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="acd53-187">오류 또는 경고 응용 프로그램 및 노드만 가져오도록 결과를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="acd53-188">결과적으로 모두 정상이므로 반환되는 노드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="acd53-189">패브릭:/WordCount 응용 프로그램만 응용 프로그램 필터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="acd53-190">사용자 지정 정책이 경고를 패브릭:/WordCount 응용 프로그램에 대해 오류로 고려하도록 지정하므로 응용 프로그램이 오류 시 평가되며 클러스터도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="acd53-191">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-191">REST</span></span>
<span data-ttu-id="acd53-192">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy)를 사용하여 클러스터 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="acd53-193">노드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-193">Get node health</span></span>
<span data-ttu-id="acd53-194">노드 엔터티의 상태를 반환하고 노드에서 보고된 상태 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="acd53-195">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-195">Input:</span></span>

* <span data-ttu-id="acd53-196">[필수] 노드를 식별하는 노드 이름.</span><span class="sxs-lookup"><span data-stu-id="acd53-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="acd53-197">[옵션] 상태를 평가하는 데 사용되는 클러스터 상태 정책 설정.</span><span class="sxs-lookup"><span data-stu-id="acd53-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="acd53-198">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-199">모든 이벤트는 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-200">API</span><span class="sxs-lookup"><span data-stu-id="acd53-200">API</span></span>
<span data-ttu-id="acd53-201">API를 통해 노드 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="acd53-202">다음 코드는 지정된 노드 이름에 대한 노드 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="acd53-203">다음 코드는 지정된 노드 이름에 대한 노드 상태를 가져오고 [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription)을 통해 이벤트 필터와 사용자 지정 정책을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="acd53-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-204">PowerShell</span></span>
<span data-ttu-id="acd53-205">노드 상태를 가져오려는 cmdlet은 [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="acd53-206">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="acd53-207">다음 cmdlet은 기본 상태 정책을 사용하여 노드 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="acd53-208">다음 cmdlet은 클러스터 내에서 모든 노드의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="acd53-209">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-209">REST</span></span>
<span data-ttu-id="acd53-210">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy)를 사용하여 노드 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="acd53-211">응용 프로그램 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-211">Get application health</span></span>
<span data-ttu-id="acd53-212">응용프로그램 엔터티의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-212">Returns the health of an application entity.</span></span> <span data-ttu-id="acd53-213">배포된 응용 프로그램 및 서비스 자녀의 성능 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="acd53-214">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-214">Input:</span></span>

* <span data-ttu-id="acd53-215">[필수] 응용 프로그램을 식별하는 응용 프로그램 이름(URI).</span><span class="sxs-lookup"><span data-stu-id="acd53-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="acd53-216">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="acd53-217">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트, 서비스 및 배포된 응용 프로그램에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-218">모든 이벤트, 서비스 및 배포된 응용 프로그램은 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="acd53-219">[선택 사항] 상태 통계를 제외하는 필터</span><span class="sxs-lookup"><span data-stu-id="acd53-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="acd53-220">지정하지 않은 경우 상태 통계는 모든 응용 프로그램 자녀(서비스, 파티션, 복제본, 배포된 응용 프로그램, 배포된 서비스 패키지)에 대한 양호, 경고 및 오류 수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-221">API</span><span class="sxs-lookup"><span data-stu-id="acd53-221">API</span></span>
<span data-ttu-id="acd53-222">응용 프로그램 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="acd53-223">다음 코드는 지정된 응용 프로그램 이름(URI)에 대한 응용 프로그램 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="acd53-224">다음 코드는 [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription)을 통해 지정된 필터와 사용자 지정 정책으로 지정된 응용 프로그램 이름(URI)에 대한 응용 프로그램 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="acd53-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-225">PowerShell</span></span>
<span data-ttu-id="acd53-226">응용 프로그램 상태를 가져오기 위한 cmdlet은 [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="acd53-227">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-228">다음 cmdlet은 **fabric:/WordCount** 응용 프로그램의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="acd53-229">다음 PowerShell cmdlet은 사용자 지정 정책을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="acd53-230">또한 자녀와 이벤트를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="acd53-231">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-231">REST</span></span>
<span data-ttu-id="acd53-232">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy)를 사용하여 응용 프로그램 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="acd53-233">서비스 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-233">Get service health</span></span>
<span data-ttu-id="acd53-234">서비스 엔터티의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-234">Returns the health of a service entity.</span></span> <span data-ttu-id="acd53-235">파티션 성능 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-235">It contains the partition health states.</span></span> <span data-ttu-id="acd53-236">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-236">Input:</span></span>

* <span data-ttu-id="acd53-237">[필수] 서비스를 식별하는 서비스 이름(URI)</span><span class="sxs-lookup"><span data-stu-id="acd53-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="acd53-238">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="acd53-239">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트 및 파티션에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-240">모든 이벤트 및 파티션은 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="acd53-241">[선택 사항] 상태 통계를 제외하는 필터</span><span class="sxs-lookup"><span data-stu-id="acd53-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="acd53-242">지정하지 않은 경우 상태는 서비스의 모든 파티션 및 복제본에 대해 양호, 경고 및 오류 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-243">API</span><span class="sxs-lookup"><span data-stu-id="acd53-243">API</span></span>
<span data-ttu-id="acd53-244">API를 통해 서비스 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="acd53-245">다음 예제는 지정된 서비스 이름(URI)을 가진 서비스 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="acd53-246">다음 코드는 [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription)을 통해 필터와 사용자 지정 정책을 지정하면서 지정된 서비스 이름(URI)에 대한 서비스 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="acd53-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-247">PowerShell</span></span>
<span data-ttu-id="acd53-248">서비스 상태를 가져오는 cmdlet은 [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="acd53-249">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-250">다음 cmdlet은 기본 상태 정책을 사용하여 서비스 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="acd53-251">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-251">REST</span></span>
<span data-ttu-id="acd53-252">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy)를 사용하여 서비스 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="acd53-253">파티션 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-253">Get partition health</span></span>
<span data-ttu-id="acd53-254">파티션 엔터티의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="acd53-255">복제본 성능 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-255">It contains the replica health states.</span></span> <span data-ttu-id="acd53-256">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-256">Input:</span></span>

* <span data-ttu-id="acd53-257">[필수] 파티션을 식별하는 파티션 ID (GUID).</span><span class="sxs-lookup"><span data-stu-id="acd53-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="acd53-258">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="acd53-259">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트 및 복제본에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-260">모든 이벤트 및 복제본은 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="acd53-261">[선택 사항] 상태 통계를 제외하는 필터</span><span class="sxs-lookup"><span data-stu-id="acd53-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="acd53-262">지정하지 않은 경우 상태 통계는 양호, 경고 및 오류 상태인 복제본 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-263">API</span><span class="sxs-lookup"><span data-stu-id="acd53-263">API</span></span>
<span data-ttu-id="acd53-264">API를 통해 파티션 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="acd53-265">옵션인 매개 변수를 지정하려면 [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="acd53-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-266">PowerShell</span></span>
<span data-ttu-id="acd53-267">파티션 상태를 가져오기 위한 cmdlet은 [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="acd53-268">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-269">다음 cmdlet은 **fabric:/WordCount/WordCountService** 서비스의 모든 파티션 상태를 가져오며 복제본 상태를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="acd53-270">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-270">REST</span></span>
<span data-ttu-id="acd53-271">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy)를 사용하여 파티션 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="acd53-272">복제본 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-272">Get replica health</span></span>
<span data-ttu-id="acd53-273">상태 저장 서비스 복제본 또는 상태 비저장 서비스 인스턴스의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="acd53-274">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-274">Input:</span></span>

* <span data-ttu-id="acd53-275">[필수] 복제본을 식별하는 파티션 ID(GUID) 및 복제본 ID.</span><span class="sxs-lookup"><span data-stu-id="acd53-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="acd53-276">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="acd53-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="acd53-277">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-278">모든 이벤트는 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-279">API</span><span class="sxs-lookup"><span data-stu-id="acd53-279">API</span></span>
<span data-ttu-id="acd53-280">API를 통해 복제본 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="acd53-281">고급 매개 변수를 지정하려면 [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="acd53-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-282">PowerShell</span></span>
<span data-ttu-id="acd53-283">복제본 상태를 가져오는 cmdlet은 [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="acd53-284">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-285">다음 cmdlet은 서비스의 모든 파티션에 대한 주 복제본의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="acd53-286">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-286">REST</span></span>
<span data-ttu-id="acd53-287">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy)를 사용하여 복제본 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="acd53-288">배포된 응용 프로그램 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-288">Get deployed application health</span></span>
<span data-ttu-id="acd53-289">노드 엔터티에 배포된 응용 프로그램의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="acd53-290">배포된 서비스 패키지 성능 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="acd53-291">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-291">Input:</span></span>

* <span data-ttu-id="acd53-292">[필수] 배포된 응용 프로그램을 식별하는 응용 프로그램 이름(URI) 및 노드 이름(문자열)</span><span class="sxs-lookup"><span data-stu-id="acd53-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="acd53-293">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="acd53-294">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트 및 배포된 서비스 패키지에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-295">모든 이벤트 및 배포된 서비스 패키지는 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="acd53-296">[선택 사항] 상태 통계를 제외하는 필터</span><span class="sxs-lookup"><span data-stu-id="acd53-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="acd53-297">지정하지 않은 경우 상태 통계는 양호, 경고 및 오류 상태인 배포 서비스 패키지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-298">API</span><span class="sxs-lookup"><span data-stu-id="acd53-298">API</span></span>
<span data-ttu-id="acd53-299">API 통해 노드에 배포된 응용 프로그램의 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="acd53-300">옵션인 매개 변수를 지정하려면 [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="acd53-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-301">PowerShell</span></span>
<span data-ttu-id="acd53-302">배포된 응용 프로그램 상태를 가져오기 위한 cmdlet은 [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="acd53-303">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="acd53-304">응용 프로그램이 배포되는 위치를 확인하려면 [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) 를 실행하고 배포된 응용 프로그램 자녀를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="acd53-305">다음 cmdlet은 **_Node_2**에 배포된 **fabric:/WordCount** 응용 프로그램의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="acd53-306">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-306">REST</span></span>
<span data-ttu-id="acd53-307">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy)를 사용하여 배포된 응용 프로그램 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="acd53-308">배포된 서비스 패키지 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="acd53-308">Get deployed service package health</span></span>
<span data-ttu-id="acd53-309">배포된 서비스 패키지 엔터티의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="acd53-310">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-310">Input:</span></span>

* <span data-ttu-id="acd53-311">[필수] 배포된 서비스 패키지를 식별하는 응용 프로그램 이름(URI), 노드 이름(문자열) 및 서비스 매니페스트 이름(문자열).</span><span class="sxs-lookup"><span data-stu-id="acd53-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="acd53-312">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 응용 프로그램 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="acd53-313">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 이벤트에 대한 필터(예: 오류만 또는 경고 및 오류).</span><span class="sxs-lookup"><span data-stu-id="acd53-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="acd53-314">모든 이벤트는 필터에 관계 없이 엔터티 집계된 상태 평가에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-315">API</span><span class="sxs-lookup"><span data-stu-id="acd53-315">API</span></span>
<span data-ttu-id="acd53-316">API 통해 배포된 서비스 패키지 상태를 가져오려면 HealthManager에서 `FabricClient` 를 만들고 [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="acd53-317">옵션인 매개 변수를 지정하려면 [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="acd53-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-318">PowerShell</span></span>
<span data-ttu-id="acd53-319">배포된 서비스 패키지 상태를 가져오는 cmdlet은 [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="acd53-320">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="acd53-321">응용 프로그램이 배포되는 위치를 확인하려면 [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) 를 실행하고 배포된 응용 프로그램을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="acd53-322">응용 프로그램에 어떤 서비스 패키지가 있는지 보려면 [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) 출력에 배포된 서비스 패키지 자녀를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="acd53-323">다음 cmdlet은 **_Node_2**에 배포된 **fabric:/WordCount** 응용 프로그램의 **WordCountServicePkg** 서비스 패키지 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="acd53-324">엔터티에 성공적인 서비스 패키지 및 진입점 활성화와 성공적인 서비스 유형 등록을 위한 **System.Hosting** 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="acd53-325">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-325">REST</span></span>
<span data-ttu-id="acd53-326">본문에 설명된 상태 정책을 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy)를 사용하여 배포된 서비스 패키지 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="acd53-327">상태 청크 쿼리</span><span class="sxs-lookup"><span data-stu-id="acd53-327">Health chunk queries</span></span>
<span data-ttu-id="acd53-328">상태 청크 쿼리는 입력 필터당 여러 수준의 클러스터 자식(재귀적)을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="acd53-329">반환할 자식을 선택할 수 있는 유연성 높은 고급 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="acd53-330">필터는 고유의 식별자나 다른 그룹 식별자 및/또는 상태를 통해 자식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="acd53-331">항상 첫 번째 수준 자식이 포함되는 상태 명령과는 다르게, 기본적으로 자식이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="acd53-332">[상태 쿼리](service-fabric-view-entities-aggregated-health.md#health-queries) 는 필요한 필터마다 지정된 엔터티의 첫 번째 수준 자식만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="acd53-333">자식의 자식을 가져오려면 관심이 있는 각 엔터티에 대해 추가 상태 API를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="acd53-334">마찬가지로, 특정 엔터티의 상태를 가져오려면 원하는 각 엔터티에 대해 하나의 상태 API를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="acd53-335">청크 쿼리 고급 필터링을 사용하면 쿼리 하나로 원하는 여러 항목을 요청할 수 있으므로 메시지 크기와 메시지의 수를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="acd53-336">청크 쿼리의 값은 한 번의 호출로 더 많은 클러스터 엔터티(필요한 루트에서 시작하여 잠재적으로 모든 클러스터 엔터티)의 상태 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="acd53-337">복잡한 상태 쿼리를 다음과 같이 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="acd53-338">오류 상태인 응용 프로그램만 반환하고, 이러한 응용 프로그램에 대해 경고 또는 오류 상태인 모든 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="acd53-339">반환된 서비스의 경우 모든 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="acd53-340">이름으로 지정한 4개 응용 프로그램의 상태만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="acd53-341">원하는 유형의 응용 프로그램 상태만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="acd53-342">노드에 배포된 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="acd53-343">모든 응용 프로그램, 지정된 노드에 배포된 모든 응용 프로그램, 해당 노드에 배포된 모든 서비스 패키지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="acd53-344">오류 상태인 모든 복제본을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-344">Return all replicas in error.</span></span> <span data-ttu-id="acd53-345">모든 응용 프로그램, 서비스, 파티션 및 오류 상태인 복제본만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="acd53-346">모든 응용 프로그램을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-346">Return all applications.</span></span> <span data-ttu-id="acd53-347">지정된 서비스의 경우 모든 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="acd53-348">현재, 상태 청크 쿼리는 클러스터 엔터티에 대해서만 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="acd53-349">상태 청크 쿼리는 클러스터 상태 청크를 반환하며, 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="acd53-350">클러스터 집계 성능 상태.</span><span class="sxs-lookup"><span data-stu-id="acd53-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="acd53-351">입력 필터를 준수하는 노드의 상태 청크 목록.</span><span class="sxs-lookup"><span data-stu-id="acd53-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="acd53-352">입력 필터를 준수하는 응용 프로그램의 상태 청크 목록.</span><span class="sxs-lookup"><span data-stu-id="acd53-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="acd53-353">각 응용 프로그램 상태 청크는 입력 필터를 준수하는 모든 서비스가 포함된 청크 목록과 필터를 준수하는 모든 배포된 응용 프로그램이 포함된 청크 목록을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="acd53-354">서비스 자식 및 배포된 응용 프로그램에도 동일한 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="acd53-355">이러한 방식으로, 요청이 있을 경우 클러스터의 모든 엔터티를 계층적 방식으로 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="acd53-356">클러스터 상태 청크 쿼리</span><span class="sxs-lookup"><span data-stu-id="acd53-356">Cluster health chunk query</span></span>
<span data-ttu-id="acd53-357">클러스터 엔터티의 상태를 반환하며 필수 자식의 계층적 상태 청크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="acd53-358">입력:</span><span class="sxs-lookup"><span data-stu-id="acd53-358">Input:</span></span>

* <span data-ttu-id="acd53-359">[옵션] 노드 및 클러스터 이벤트를 평가하는 데 사용되는 클러스터 상태 정책.</span><span class="sxs-lookup"><span data-stu-id="acd53-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="acd53-360">[옵션] 응용 프로그램 매니페스트 정책을 재정의하는 데 사용되는 상태 정책이 있는 응용 프로그램 상태 정책 맵.</span><span class="sxs-lookup"><span data-stu-id="acd53-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="acd53-361">[옵션] 관심 있는 엔터티를 지정하고 결과에 반환되어야 하는 노드 및 응용 프로그램에 대한 필터.</span><span class="sxs-lookup"><span data-stu-id="acd53-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="acd53-362">필터는 엔터티/엔터티 그룹에 한정적으로 적용하거나 해당 수준의 모든 엔터티에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="acd53-363">쿼리에서 반환하는 엔터티를 세분화할 수 있도록 필터 목록에 일반 필터 하나 그리고/또는 특정 식별자에 대한 필터가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="acd53-364">필터 목록이 비어 있으면 기본적으로 자식이 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="acd53-365">필터에 대한 자세한 내용은 [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) 및 [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd53-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="acd53-366">응용 프로그램 필터는 자식에 대한 고급 필터를 재귀적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="acd53-367">청크 결과에는 필터를 준수하는 하위 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="acd53-368">현재, 청크 쿼리 비정상 평가 또는 엔터티 이벤트를 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="acd53-369">이러한 추가 정보는 기존 클러스터 상태 쿼리를 사용하여 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="acd53-370">API</span><span class="sxs-lookup"><span data-stu-id="acd53-370">API</span></span>
<span data-ttu-id="acd53-371">클러스터 상태 청크를 가져오려면 해당 **HealthManager**에서 `FabricClient`를 만들고 [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="acd53-372">상태 정책 및 고급 필터를 설명하는 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription)을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="acd53-373">다음 코드는 고급 필터가 포함된 클러스터 상태 청크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="acd53-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd53-374">PowerShell</span></span>
<span data-ttu-id="acd53-375">클러스터 상태를 가져오려는 cmdlet은 [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="acd53-376">먼저 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="acd53-377">다음 코드는 항상 반환되어야 하는 특정 노드를 제외하고 노드에 오류가 있을 때에만 해당 노드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="acd53-378">다음 cmdlet은 응용 프로그램 필터가 포함된 클러스터 청크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="acd53-379">다음 cmdlet은 노드에 배포된 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="acd53-380">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="acd53-380">REST</span></span>
<span data-ttu-id="acd53-381">본문에 설명된 상태 정책 및 고급 필터를 포함하는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster)를 사용하여 클러스터 상태 청크를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="acd53-382">일반 쿼리</span><span class="sxs-lookup"><span data-stu-id="acd53-382">General queries</span></span>
<span data-ttu-id="acd53-383">일반 쿼리는 지정된 형식의 서비스 패브릭 엔터티 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="acd53-384">이러한 쿼리는 API( **FabricClient.QueryManager**상의 메서드를 통해), PowerShell cmdlet 및 REST를 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="acd53-385">이러한 쿼리는 여러 구성 요소에서 하위 쿼리를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="acd53-386">둘 중 하나는 [Health 스토어](service-fabric-health-introduction.md#health-store)로 각 쿼리 결과에 대해 집계된 상태를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="acd53-387">일반 쿼리는 엔터티의 집계된 성능 상태를 반환 하고 풍부한 상태 데이터를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="acd53-388">엔터티가 비정상이면 상태 쿼리를 따라서 이벤트, 자녀 성능 상태 및 비정상 평가를 포함하는 모든 상태 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="acd53-389">일반 쿼리가 엔터티에 대해 알 수 없는 성능 상태를 반환하는 경우 상태 저장소에 해당 엔터티에 대해 완전한 데이터가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="acd53-390">또한 상태 저장소에 대한 하위 쿼리에 성공하지 못한 것일 수 있습니다(예: 통신 오류가 있거나 상태 저장소가 정체됨).</span><span class="sxs-lookup"><span data-stu-id="acd53-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="acd53-391">엔터티에 대한 상태 쿼리를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="acd53-392">네트워크 문제와 같은 하위 쿼리에 일시적인 오류가 발생한 경우 후속 쿼리는 성공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="acd53-393">또한 엔터티가 상태 저장소로부터 노출되지 않은 자세한 이유를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="acd53-394">엔터티에 대한 **HealthState** 가 포함된 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="acd53-395">노드 목록: 클러스터의 목록 노드(페이징)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="acd53-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="acd53-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="acd53-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="acd53-398">응용 프로그램 목록: 클러스터의 응용 프로그램 목록(페이징)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="acd53-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="acd53-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="acd53-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="acd53-401">서비스 목록: 응용 프로그램의 서비스 목록(페이징)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="acd53-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="acd53-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="acd53-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="acd53-404">파티션 목록: 서비스의 파티션 목록(페이징)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="acd53-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="acd53-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="acd53-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="acd53-407">복제본 목록: 파티션의 복제본 목록(페이징)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="acd53-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="acd53-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="acd53-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="acd53-410">배포된 응용 프로그램 목록: 노드에 배포된 응용 프로그램의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="acd53-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="acd53-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="acd53-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="acd53-413">배포된 서비스 패키지 목록: 배포된 응용 프로그램에서 서비스 패키지 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="acd53-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="acd53-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="acd53-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="acd53-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="acd53-416">일부 쿼리는 페이징된 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-416">Some of the queries return paged results.</span></span> <span data-ttu-id="acd53-417">반환되는 이러한 쿼리는 [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1)에서 파생된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="acd53-418">결과가 메시지와 맞지 않으면 한 페이지만 반환되고 열거형이 중지된 위치를 추적하는 ContinuationToken이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="acd53-419">다음 결과를 얻으려면 계속해서 동일한 쿼리를 호출하고 이전 쿼리의 연속 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="acd53-420">예</span><span class="sxs-lookup"><span data-stu-id="acd53-420">Examples</span></span>
<span data-ttu-id="acd53-421">다음 코드는 클러스터에서 비정상 응용 프로그램을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="acd53-422">다음 cmdlet은 패브릭:/WordCount 응용 프로그램에 대한 응용 프로그램 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="acd53-423">성능 상태는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="acd53-424">다음 cmdlet은 성능 상태가 오류인 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="acd53-425">클러스터 및 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="acd53-425">Cluster and application upgrades</span></span>
<span data-ttu-id="acd53-426">클러스터 및 응용 프로그램의 모니터링된 업그레이드 중 서비스 패브릭이 상태를 점검하여 모든 것이 정상으로 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="acd53-427">엔터티가 구성된 상태 정책을 사용한 평가로 비정상인 경우 업그레이드는 다음 작업을 결정하는 업그레이드 관련 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="acd53-428">업그레이드는 사용자 상호 작용을 허용하도록 일시 중지되거나(예: 오류 조건 해결 또는 정책 변경) 이전 버전으로 자동으로 롤백할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="acd53-429">*클러스터* 업그레이드 중 클러스터 업그레이드 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="acd53-430">업그레이드 상태는 클러스터에서 비정상인 항목을 가리키는 비정상 평가를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="acd53-431">상태 문제로 인해 업그레이드가 롤백되는 경우 업그레이드 상태가 마지막 비정상 이유를 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="acd53-432">이 정보는 업그레이드가 롤백되거나 중지된 후에 무엇이 잘못되었는지를 관리자가 조사하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="acd53-433">마찬가지로, *응용 프로그램* 업그레이드 중에 응용 프로그램 업그레이드 상태에 비정상 평가가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="acd53-434">다음은 수정된 패브릭:/WordCount 응용 프로그램에 대한 응용 프로그램 업그레이드 상태를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="acd53-435">watchdog에서 복제본 하나에서 오류를 보고했습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="acd53-436">상태 검사를 준수하지 않기 때문에 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="acd53-437">[Service Fabric 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="acd53-438">상태 평가를 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="acd53-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="acd53-439">클러스터 또는 응용 프로그램에 문제가 있을 때마다 클러스터나 응용 프로그램 상태를 확인하여 무엇이 잘못인지 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="acd53-440">비정상 평가는 현재 비정상 상태를 무엇이 트리거했는지에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="acd53-441">필요한 경우 비정상 자녀 엔터티로 드릴다운하여 근본 원인을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="acd53-442">예를 들어, 복제본 중 하나에서 오류를 보고하여 상태가 비정상인 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="acd53-443">다음 Powershell cmdlet은 비정상 평가를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="acd53-444">복제본을 살펴 자세한 정보를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="acd53-445">비정상 평가는 엔터티가 현재 상태로 평가된 첫 번째 이유를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="acd53-446">이 상태를 트리거하는 다른 여러 이벤트가 있을 수 있지만 평가에 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="acd53-447">자세한 내용을 알아보려면 클러스터의 모든 비정상 보고서를 산출하는 상태 엔터티를 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="acd53-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="acd53-448">다음 단계</span><span class="sxs-lookup"><span data-stu-id="acd53-448">Next steps</span></span>
[<span data-ttu-id="acd53-449">시스템 상태 보고서를 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="acd53-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="acd53-450">사용자 지정 서비스 패브릭 상태 보고서 추가</span><span class="sxs-lookup"><span data-stu-id="acd53-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="acd53-451">서비스 상태를 보고 및 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="acd53-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="acd53-452">로컬로 서비스 모니터링 및 진단</span><span class="sxs-lookup"><span data-stu-id="acd53-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="acd53-453">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="acd53-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
