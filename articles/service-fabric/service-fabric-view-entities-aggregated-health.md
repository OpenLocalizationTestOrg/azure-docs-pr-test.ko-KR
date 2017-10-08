---
title: "aaaHow tooview Azure Service Fabric 엔터티의 집계 상태 | Microsoft Docs"
description: "Tooquery, 보고, 하 고 상태 쿼리 수 및 일반 쿼리를 통해 Azure 서비스 패브릭 엔터티의 집계 상태를 평가 하는 방법을 설명 합니다."
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="26618-103">서비스 패브릭 상태 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="26618-103">View Service Fabric health reports</span></span>
<span data-ttu-id="26618-104">Azure Service Fabric은 시스템 구성 요소와 워치독이 모니터링하는 로컬 조건을 보고할 수 있는 상태 엔터티가 있는 [상태 모델](service-fabric-health-introduction.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="26618-105">hello [상태 저장소](service-fabric-health-introduction.md#health-store) 엔터티가 정상 상태 인지 여부를 모든 상태 데이터 toodetermine를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="26618-106">hello 클러스터 hello 시스템 구성 요소에서 보낸 상태 보고서에 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="26618-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="26618-107">자세한 내용을 [사용 하 여 시스템 상태 보고서를 tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="26618-108">서비스 패브릭 hello 엔터티의 여러 방법으로 tooget hello 집계 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="26618-109">[서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 또는 기타 시각화 도구</span><span class="sxs-lookup"><span data-stu-id="26618-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="26618-110">상태 쿼리(PowerShell, API 또는 REST를 통해)</span><span class="sxs-lookup"><span data-stu-id="26618-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="26618-111">일반 쿼리 (PowerShell, API, REST 통해) hello 속성 중 하나로 상태는 포함 하는 엔터티 반환 하는 목록을</span><span class="sxs-lookup"><span data-stu-id="26618-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="26618-112">toodemonstrate 보겠습니다 이러한 옵션을 로컬 클러스터를 사용 하 여 5 개 노드와 hello와 [패브릭: / WordCount 응용 프로그램](http://aka.ms/servicefabric-wordcountapp)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="26618-113">hello **패브릭: / WordCount** 두 개의 기본 서비스 형식의 상태 저장 서비스를 포함 하는 응용 프로그램 `WordCountServiceType`, 및 형식의 상태 비저장 서비스 `WordCountWebServiceType`합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="26618-114">Hello 변경한 다음 `ApplicationManifest.xml` hello 상태 저장 서비스 파티션 한 개에 대 한 7 toorequire 대상 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="26618-115">Hello 클러스터에는 5 개의 노드가 있습니다, 때문에 hello 시스템 구성 요소 hello 대상 수 있기 때문에 hello 서비스 파티션에 경고를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="26618-116">서비스 패브릭 탐색기 내 상태</span><span class="sxs-lookup"><span data-stu-id="26618-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="26618-117">서비스 패브릭 탐색기 hello 클러스터의 시각적 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="26618-118">아래 hello 이미지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="26618-119">응용 프로그램 hello **패브릭: / WordCount** 에서 보고 하는 오류 이벤트를 있기 때문에 빨간색 (오류)는 **MyWatchdog** hello 속성에 대 한 **가용성**합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="26618-120">해당 서비스 중 하나인 **패브릭:/WordCount/WordCountService** 가 노란색입니다(경고 시).</span><span class="sxs-lookup"><span data-stu-id="26618-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="26618-121">7 개의 복제본 hello 서비스를 구성 하 고 hello 클러스터에는 5 개의 노드가 두 repicas 배치 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="26618-122">보고서를 시스템으로 인해 hello 서비스 파티션은 노란색 여기 표시 되지 않는 있지만 `System.FM` 되었다는 `Partition is below target replica or instance count`합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="26618-123">hello 노란색 파티션 트리거 hello 노란색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="26618-124">hello 클러스터는 빨간색 hello 응용 프로그램으로 인해 빨간색입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="26618-125">hello 평가 기본 정책에서 hello 클러스터 매니페스트 및 응용 프로그램 매니페스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="26618-126">엄격한 정책이며 오류를 용납하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="26618-127">서비스 패브릭 탐색기로 hello 클러스터의 보기:</span><span class="sxs-lookup"><span data-stu-id="26618-127">View of hello cluster with Service Fabric Explorer:</span></span>

![서비스 패브릭 탐색기를 사용 하는 hello 클러스터의 보기입니다.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="26618-129">[서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="26618-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="26618-130">상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="26618-130">Health queries</span></span>
<span data-ttu-id="26618-131">각 지원 hello에 대 한 상태 쿼리 수를 노출 하는 서비스 패브릭 [엔터티 형식](service-fabric-health-introduction.md#health-entities-and-hierarchy)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="26618-132">Hello에 메서드를 사용 하는 API 통해 액세스할 수 있습니다 [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlet 및 REST 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="26618-133">이러한 쿼리가 hello 엔터티에 대 한 전체 상태 정보를 반환할: hello 성능 상태, 엔터티 상태 이벤트, 해당 하는 경우 자식 상태, 비정상 상태의 평가 (hello 엔터티 정상이 아님) 하는 경우 및 자식 상태 통계를 집계 (때 해당).</span><span class="sxs-lookup"><span data-stu-id="26618-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="26618-134">상태 엔터티는 완전히 채워지면 hello health store에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="26618-135">hello 엔터티 (삭제 됨) 활성 상태 여야 하 고 시스템 보고서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="26618-136">Hello 계층 구조 체인에서 해당 부모 엔터티에 system 보고서 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="26618-137">이러한 조건 중 하나라도 충족 되지 않은 경우 hello 상태 반환을 쿼리 하는 한 [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) 와 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` hello 엔터티 반환 되지 않습니다 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="26618-138">상태 쿼리 수 hello hello 엔터티 형식에 따라 달라 지는 hello 엔터티 식별자를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="26618-139">hello 쿼리 선택적 상태 정책 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="26618-140">상태 정책이 지정 된 경우 hello [상태 정책을](service-fabric-health-introduction.md#health-policies) hello 클러스터 또는 응용 프로그램 매니페스트에서 평가에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="26618-141">Hello 매니페스트 상태 정책에 대 한 정의 포함 하지, hello 기본 상태 정책 평가 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="26618-142">hello 기본 상태 정책을 발생 한 모든 오류를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="26618-143">hello 쿼리 부분 자식만 반환에 대 한 필터를 적용할 수도 또는 지정 된 필터를 hello 이벤트-hello 것을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="26618-144">다른 필터 hello 자식 통계 제외 하 고 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="26618-145">hello 출력 필터 hello 서버 쪽에서 적용 되므로 hello 메시지 회신 크기가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="26618-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="26618-146">Toolimit hello 데이터 반환 hello 클라이언트 쪽에서 필터를 적용 하지 않고 hello 출력 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="26618-147">엔터티의 상태는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-147">An entity's health contains:</span></span>

* <span data-ttu-id="26618-148">hello는 hello 엔터티의 상태를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="26618-149">엔터티 상태 보고서, 하위 상태 (있는 경우), 및 상태 정책을 기반으로 하는 hello 상태 저장소에 의해 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="26618-150">[엔터티 상태 평가](service-fabric-health-introduction.md#health-evaluation)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="26618-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="26618-151">hello 상태 이벤트를 hello 엔터티 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="26618-152">hello 컬렉션의 모든 자식 항목 자식을 가질 수 있는 hello 엔터티에 대 한 성능 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="26618-153">hello 상태 엔터티 식별자를 포함 하 고 hello 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="26618-154">자식에 대 한 전체 상태 tooget hello 자식 엔터티 형식에 대 한 hello 쿼리 상태를 호출 하 고 hello 자식 식별자 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="26618-155">해당 지점 toohello 보고 하는 hello 비정상 상태의 평가 hello 엔터티 상태가 정상이 아닌 경우 hello 엔터티의 hello 상태가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="26618-156">hello 평가 재귀, 현재 상태를 트리거한 hello 자식 상태 평가 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="26618-157">예를 들어, 워치독이 복제본에 대해 오류를 보고했습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="26618-158">hello 응용 프로그램 상태 tooan 비정상적인 서비스; 인해 비정상 평가 버전을 보여 줍니다. 오류가; tooa 파티션 인해 hello 서비스가 정상이 아님을 hello 파티션 오류가; tooa 복제본 인해 손상 되었습니다. hello 복제본 toohello watchdog 오류 상태 보고서 인해 손상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="26618-159">자식이 있는 hello 엔터티의 모든 하위 형식에 대 한 hello 상태 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="26618-160">예를 들어 클러스터 상태 hello 응용 프로그램, 서비스, 파티션, 복제본의 총 수를 표시 하 고 hello 클러스터의 엔터티를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="26618-161">서비스 상태 hello 총 파티션 수를 보여주며, hello에서 복제본 서비스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="26618-162">클러스터 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-162">Get cluster health</span></span>
<span data-ttu-id="26618-163">반환 상태 hello 클러스터 엔터티의 hello를 hello 응용 프로그램 및 상태 (hello 클러스터의 자식) 노드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="26618-164">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-164">Input:</span></span>

* <span data-ttu-id="26618-165">[선택 사항] hello 클러스터 상태 정책 tooevaluate hello 노드와 hello 클러스터 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="26618-166">[선택 사항] hello 응용 프로그램 상태 정책 지도 hello 상태 정책을 사용 하 여 toooverride hello 응용 프로그램 매니페스트 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="26618-167">[선택 사항] 이벤트, 노드 및 되는 항목을 지정 하는 응용 프로그램에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-168">모든 이벤트, 노드 및 응용 프로그램은 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="26618-169">[선택 사항] Tooexclude 상태 통계를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="26618-170">[선택 사항] 필터링 tooinclude 패브릭: / 시스템 상태 통계에 hello 상태 통계.</span><span class="sxs-lookup"><span data-stu-id="26618-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="26618-171">Hello 상태 통계 제외 되지 않은 경우에 적용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="26618-172">기본적으로 hello 상태 통계에는 사용자 응용 프로그램 및 하지 hello 시스템 응용 프로그램에 대 한 통계만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="26618-173">API</span><span class="sxs-lookup"><span data-stu-id="26618-173">API</span></span>
<span data-ttu-id="26618-174">tooget 상태 클러스터를 만들기는 `FabricClient` 및 호출 hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) 메서드를 해당 **HealthManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="26618-175">hello 다음 호출이 가져옵니다 hello 클러스터 상태를:</span><span class="sxs-lookup"><span data-stu-id="26618-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="26618-176">hello 다음 코드는 사용자 지정 클러스터 상태 정책을 사용 하 여 hello 클러스터 상태를 가져옵니다을 노드 및 응용 프로그램에 대 한 필터.</span><span class="sxs-lookup"><span data-stu-id="26618-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="26618-177">Hello 상태 통계 포함 hello 패브릭 지정 것: / 시스템 통계.</span><span class="sxs-lookup"><span data-stu-id="26618-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="26618-178">만들 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), hello 입력된 정보가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="26618-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-179">PowerShell</span></span>
<span data-ttu-id="26618-180">hello cmdlet tooget hello 클러스터 상태 설명이 [Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="26618-181">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-182">hello hello 클러스터의 상태는 5 개의 노드가, hello 시스템 응용 프로그램 및 패브릭: / WordCount 설명 된 대로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="26618-183">cmdlet을 다음 hello 기본 상태 정책을 사용 하 여 클러스터 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26618-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="26618-184">hello 집계 된 상태 (경고), 때문에 패브릭 hello: WordCount 응용 프로그램은 경고에 /입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="26618-185">참고 되는 조건은 hello 비정상 상태의 평가 hello에 세부 정보를 제공 하는 방법에 hello 집계 상태가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="26618-186">hello 다음 PowerShell cmdlet을 가져옵니다 hello 클러스터의 hello 상태를 사용자 지정 응용 프로그램 정책을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="26618-187">결과 tooget 응용 프로그램만의 및 노드 오류 또는 경고를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="26618-188">결과적으로 모두 정상이므로 반환되는 노드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="26618-189">패브릭만 hello: WordCount 응용 프로그램에서는 hello 응용 프로그램 필터 /입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="26618-190">사용자 지정 정책 hello hello 패브릭에 대 한 오류로 tooconsider 경고를 지정 하기 때문에: / WordCount 응용 프로그램을 hello 응용 프로그램은 오류를 평가 이며 hello 클러스터도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-191">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-191">REST</span></span>
<span data-ttu-id="26618-192">사용 하 여 클러스터 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="26618-193">노드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-193">Get node health</span></span>
<span data-ttu-id="26618-194">반환 상태 노드 엔터티의 hello와 hello 노드에서 보고 된 hello 상태 이벤트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="26618-195">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-195">Input:</span></span>

* <span data-ttu-id="26618-196">Hello 노드를 식별 하는 [필수] hello 노드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="26618-197">[선택 사항] hello 클러스터 상태 정책 설정은 tooevaluate 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="26618-198">[선택 사항] 어떤 항목을 지정 하는 이벤트에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-199">모든 이벤트는 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="26618-200">API</span><span class="sxs-lookup"><span data-stu-id="26618-200">API</span></span>
<span data-ttu-id="26618-201">hello API 통해 tooget 노드 상태 만들기는 `FabricClient` 및 호출 hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="26618-202">hello 다음 코드를 가져옵니다 hello 지정 된 노드 이름에 대 한 hello 노드 상태를:</span><span class="sxs-lookup"><span data-stu-id="26618-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="26618-203">hello 다음 코드를 가져옵니다 hello 노드 상태 hello 노드 이름과 전달 및에 지정 된 이벤트 필터를 통해 사용자 지정 정책에 대 한 [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="26618-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="26618-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-204">PowerShell</span></span>
<span data-ttu-id="26618-205">hello cmdlet tooget hello 노드 상태는 [Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="26618-206">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="26618-207">cmdlet을 다음 hello 기본 상태 정책을 사용 하 여 hello 노드 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26618-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="26618-208">hello 다음 cmdlet을 가져옵니다 모든 노드의 상태를 hello hello 클러스터:</span><span class="sxs-lookup"><span data-stu-id="26618-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-209">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-209">REST</span></span>
<span data-ttu-id="26618-210">사용 하 여 노드 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="26618-211">응용 프로그램 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-211">Get application health</span></span>
<span data-ttu-id="26618-212">응용 프로그램 엔터티 hello 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="26618-213">Hello hello 배포 응용 프로그램 및 서비스의 하위 항목의 상태가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="26618-214">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-214">Input:</span></span>

* <span data-ttu-id="26618-215">[필수] hello 응용 프로그램 이름 (URI) hello 응용 프로그램을 식별 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="26618-216">[선택 사항] hello 응용 프로그램 상태 정책이 toooverride hello 응용 프로그램 매니페스트 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="26618-217">[선택 사항] 이벤트, 서비스 및 되는 항목을 지정 하는 배포 된 응용 프로그램에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-218">모든 이벤트, 서비스 및 배포 된 응용 프로그램은 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="26618-219">[선택 사항] Tooexclude hello 상태 통계를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="26618-220">Hello 상태 통계 포함 hello 확인, 경고 및 모든 응용 프로그램 자식에 대 한 오류 수를 지정 하지: 서비스, 파티션, 복제본, 응용 프로그램을 배포 하 고 서비스 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="26618-221">API</span><span class="sxs-lookup"><span data-stu-id="26618-221">API</span></span>
<span data-ttu-id="26618-222">tooget 응용 프로그램 상태 만들기는 `FabricClient` 및 호출 hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="26618-223">hello 다음 코드를 가져옵니다 (URI) hello 지정 된 응용 프로그램 이름에 대 한 hello 응용 프로그램 상태를:</span><span class="sxs-lookup"><span data-stu-id="26618-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="26618-224">hello 다음 코드 hello 지정 된 응용 프로그램 이름 (URI)에 대 한 hello 응용 프로그램 상태 필터와 함께 가져오고을 통해 지정 된 사용자 지정 정책을 [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="26618-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-225">PowerShell</span></span>
<span data-ttu-id="26618-226">hello cmdlet tooget hello 응용 프로그램 상태를 [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="26618-227">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-228">hello 다음 cmdlet이 반환 hello의 hello 상태 **패브릭: / WordCount** 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="26618-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="26618-229">다음 사용자 지정 정책에서 PowerShell cmdlet 패스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="26618-230">또한 자녀와 이벤트를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-231">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-231">REST</span></span>
<span data-ttu-id="26618-232">사용 하 여 응용 프로그램 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="26618-233">서비스 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-233">Get service health</span></span>
<span data-ttu-id="26618-234">서비스는 엔터티의 hello 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="26618-235">Hello 파티션 성능 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-235">It contains hello partition health states.</span></span> <span data-ttu-id="26618-236">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-236">Input:</span></span>

* <span data-ttu-id="26618-237">[필수] hello 서비스 이름 (URI) hello 서비스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="26618-238">[선택 사항] hello 응용 프로그램 상태 정책을 toooverride hello 응용 프로그램 매니페스트 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="26618-239">[선택 사항] 필터 이벤트 및 되는 항목을 지정 하는 파티션에 대 한 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-240">모든 이벤트 및 파티션에 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="26618-241">[선택 사항] Tooexclude 상태 통계를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="26618-242">지정 하지 않으면 확인 상태 통계 표시 hello hello, 모든 파티션과 hello 서비스의 복제본에 대 한 경고 및 오류를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="26618-243">API</span><span class="sxs-lookup"><span data-stu-id="26618-243">API</span></span>
<span data-ttu-id="26618-244">hello API 통해 서비스 상태 tooget 만들기는 `FabricClient` 및 호출 hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="26618-245">hello 다음 예제에서는 가져옵니다 지정 된 서비스 이름 (URI)으로 서비스의 hello 상태를:</span><span class="sxs-lookup"><span data-stu-id="26618-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="26618-246">hello 다음 코드를 가져옵니다 (URI) hello 지정 된 서비스 이름에 대 한 hello 서비스 상태를 통해 사용자 지정 정책 및 필터를 지정 하 [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="26618-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="26618-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-247">PowerShell</span></span>
<span data-ttu-id="26618-248">hello cmdlet tooget hello 서비스 상태는 [Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="26618-249">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-250">cmdlet을 다음 hello 기본 상태 정책을 사용 하 여 hello 서비스 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26618-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-251">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-251">REST</span></span>
<span data-ttu-id="26618-252">사용 하 여 서비스 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="26618-253">파티션 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-253">Get partition health</span></span>
<span data-ttu-id="26618-254">파티션 엔터티의 hello 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="26618-255">Hello 복제 데이터베이스 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-255">It contains hello replica health states.</span></span> <span data-ttu-id="26618-256">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-256">Input:</span></span>

* <span data-ttu-id="26618-257">[필수] hello 파티션 hello 파티션을 식별 하는 ID (GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="26618-258">[선택 사항] hello 응용 프로그램 상태 정책을 toooverride hello 응용 프로그램 매니페스트 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="26618-259">[선택 사항] 이벤트와 되는 항목을 지정 하는 복제본에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-260">모든 이벤트 및 복제본은 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="26618-261">[선택 사항] Tooexclude 상태 통계를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="26618-262">지정 하지 않으면 hello 상태 통계 상태 확인, 경고 및 오류에는 복제본의 수는 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26618-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="26618-263">API</span><span class="sxs-lookup"><span data-stu-id="26618-263">API</span></span>
<span data-ttu-id="26618-264">hello API 통해 tooget 파티션 상태 만들기는 `FabricClient` 및 호출 hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="26618-265">toospecify 선택적 매개 변수를 만들 [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="26618-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-266">PowerShell</span></span>
<span data-ttu-id="26618-267">hello cmdlet tooget hello 파티션 상태는 [Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="26618-268">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-269">hello 다음 cmdlet을 가져옵니다 hello의 모든 파티션에 대 한 hello 상태 **패브릭: / WordCount/WordCountService** 서비스 및 복제 상태는 필터링:</span><span class="sxs-lookup"><span data-stu-id="26618-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="rest"></a><span data-ttu-id="26618-270">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-270">REST</span></span>
<span data-ttu-id="26618-271">사용 하 여 파티션 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="26618-272">복제본 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-272">Get replica health</span></span>
<span data-ttu-id="26618-273">상태 저장 서비스 복제본 또는 상태 비저장 서비스 인스턴스의 hello 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="26618-274">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-274">Input:</span></span>

* <span data-ttu-id="26618-275">[필수] hello 파티션 ID (GUID) 및 복제본 ID hello 복제 데이터베이스를 식별 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="26618-276">[선택 사항] hello 응용 프로그램 상태 정책 매개 변수 toooverride hello 응용 프로그램 매니페스트 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="26618-277">[선택 사항] 어떤 항목을 지정 하는 이벤트에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-278">모든 이벤트는 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="26618-279">API</span><span class="sxs-lookup"><span data-stu-id="26618-279">API</span></span>
<span data-ttu-id="26618-280">hello API 통해 tooget hello 복제 데이터베이스 상태 만들기는 `FabricClient` 및 호출 hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="26618-281">고급 매개 변수를 사용 하 여 toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="26618-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-282">PowerShell</span></span>
<span data-ttu-id="26618-283">hello cmdlet tooget hello 복제 데이터베이스 상태는 [Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="26618-284">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-285">hello 다음 cmdlet을 가져옵니다 hello 서비스의 모든 파티션에 대 한 hello 주 복제본의 hello 상태를:</span><span class="sxs-lookup"><span data-stu-id="26618-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-286">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-286">REST</span></span>
<span data-ttu-id="26618-287">사용 하 여 복제 데이터베이스 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="26618-288">배포된 응용 프로그램 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-288">Get deployed application health</span></span>
<span data-ttu-id="26618-289">노드 엔터티에 배포 된 응용 프로그램의 hello 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="26618-290">배포 된 hello 서비스 패키지 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="26618-291">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-291">Input:</span></span>

* <span data-ttu-id="26618-292">[필수] hello 응용 프로그램 이름 (URI) 및 노드 이름 (문자열) hello를 식별 하는 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="26618-293">[선택 사항] hello 응용 프로그램 상태 정책이 toooverride hello 응용 프로그램 매니페스트 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="26618-294">[선택 사항] 이벤트 및 되는 항목을 지정 하는 배포 된 서비스 패키지에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-295">모든 이벤트 및 배포 된 서비스 패키지는 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="26618-296">[선택 사항] Tooexclude 상태 통계를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="26618-297">지정 하지 않으면 hello 상태 통계 확인, 경고 및 오류 상태에서 배포 된 서비스 패키지의 hello 번호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="26618-298">API</span><span class="sxs-lookup"><span data-stu-id="26618-298">API</span></span>
<span data-ttu-id="26618-299">hello API 통해 노드에서 배포 된 응용 프로그램의 tooget hello 상태 만들기는 `FabricClient` 및 호출 hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="26618-300">toospecify 선택적 매개 변수를 사용 하 여 [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="26618-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-301">PowerShell</span></span>
<span data-ttu-id="26618-302">hello cmdlet tooget hello 배포 응용 프로그램 상태를 [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="26618-303">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="26618-304">응용 프로그램 배포 되는 위치 아웃 toofind 실행 [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) hello에 자식 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="26618-305">hello 다음 cmdlet을 가져옵니다 hello의 hello 상태 **패브릭: / WordCount** 응용 프로그램에 배포 된 **_Node_2**합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="26618-306">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-306">REST</span></span>
<span data-ttu-id="26618-307">사용 하 여 배포 된 응용 프로그램 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="26618-308">배포된 서비스 패키지 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="26618-308">Get deployed service package health</span></span>
<span data-ttu-id="26618-309">반환 상태는 배포 된 서비스 패키지 엔터티의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="26618-310">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-310">Input:</span></span>

* <span data-ttu-id="26618-311">[필수] hello 응용 프로그램 이름 (URI), 노드 이름 (문자열) 및 서비스 매니페스트 이름 (string) hello를 식별 하는 서비스 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="26618-312">[선택 사항] hello 응용 프로그램 상태 정책을 toooverride hello 응용 프로그램 매니페스트 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="26618-313">[선택 사항] 어떤 항목을 지정 하는 이벤트에 대 한 필터 관심 및 hello 결과 (예를 들어 오류만, 또는 경고 및 오류)으로 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="26618-314">모든 이벤트는 hello 필터에 관계 없이 사용 되는 tooevaluate hello 엔터티의 집계 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="26618-315">API</span><span class="sxs-lookup"><span data-stu-id="26618-315">API</span></span>
<span data-ttu-id="26618-316">hello API 통해 배포 된 서비스 패키지의 tooget hello 상태 만들기는 `FabricClient` 호출 hello 및 [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) 해당 HealthManager 메서드.</span><span class="sxs-lookup"><span data-stu-id="26618-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="26618-317">toospecify 선택적 매개 변수를 사용 하 여 [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="26618-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-318">PowerShell</span></span>
<span data-ttu-id="26618-319">hello cmdlet tooget hello 배포 된 서비스 패키지 상태는 [Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="26618-320">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="26618-321">응용 프로그램 배포 되는 위치 toosee 실행 [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) hello 배포 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="26618-322">서비스 패키지 응용 프로그램에서 조회에 있는 hello toosee 배포 hello 서비스 패키지 자식의 [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="26618-323">hello 다음 cmdlet을 가져옵니다 hello의 hello 상태 **WordCountServicePkg** 서비스 패키지의 hello **패브릭: / WordCount** 응용 프로그램에 배포 된 **_Node_2**합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="26618-324">hello 엔터티에 **System.Hosting** 성공적인 서비스 패키지 및 진입점 활성화 및 성공적인 서비스 유형을 등록에 대 한 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="26618-325">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-325">REST</span></span>
<span data-ttu-id="26618-326">사용 하 여 배포 된 서비스 패키지 상태를 가져올 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) hello 본문에 설명 된 상태 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="26618-327">상태 청크 쿼리</span><span class="sxs-lookup"><span data-stu-id="26618-327">Health chunk queries</span></span>
<span data-ttu-id="26618-328">hello 상태 청크 쿼리는 여러 수준의 클러스터 당 자녀 수 (재귀적) 입력된 필터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="26618-329">Hello 자식 선택에 유연성을 많이 사용할 수 있는 고급 필터를 지원 toobe 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="26618-330">hello 필터 hello 고유 식별자 또는 다른 그룹 식별자 및/또는 상태 자식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="26618-331">기본적으로 자식 항상 첫 번째 수준의 하위 항목을 포함 하는 것과 반대로 toohealth 명령으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="26618-332">hello [상태 쿼리 수](service-fabric-view-entities-aggregated-health.md#health-queries) hello의 반환 첫 번째 수준 자식 당 필요한 필터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="26618-333">hello 자식의 tooget hello 자식 관심 있는 각 엔터티에 대 한 추가 상태 Api를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="26618-334">마찬가지로, 특정 엔터티의 tooget hello 상태, 원하는 각 엔터티에 대 한 상태 API를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="26618-335">hello 청크 쿼리 고급 필터링 있습니다 toorequest 여러 관심 있는 항목의 hello 메시지 크기와 hello 메시지 수를 최소화 한 쿼리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="26618-336">hello hello 청크 쿼리의 기간은 파악할 수 상태 추가 클러스터 엔터티 (잠재적으로 모든 클러스터 엔터티에 필요한 루트부터 시작)에 대 한 한 번의 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="26618-337">복잡한 상태 쿼리를 다음과 같이 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="26618-338">오류 상태인 응용 프로그램만 반환하고, 이러한 응용 프로그램에 대해 경고 또는 오류 상태인 모든 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="26618-339">반환된 서비스의 경우 모든 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="26618-340">해당 이름으로 지정 된 네 가지 응용 프로그램의 hello 상태만를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="26618-341">원하는 응용 프로그램 종류의 응용 프로그램의 hello 상태만를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="26618-342">노드에 배포된 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="26618-343">모든 응용 프로그램, hello 지정 노드에서 배포 된 모든 응용 프로그램 및 해당 노드의 모든 배포 된 hello 서비스 패키지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="26618-344">오류 상태인 모든 복제본을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-344">Return all replicas in error.</span></span> <span data-ttu-id="26618-345">모든 응용 프로그램, 서비스, 파티션 및 오류 상태인 복제본만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="26618-346">모든 응용 프로그램을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-346">Return all applications.</span></span> <span data-ttu-id="26618-347">지정된 서비스의 경우 모든 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="26618-348">현재 hello 상태 청크 쿼리는 hello 클러스터 엔터티에 대해서만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="26618-349">상태 청크 쿼리는 클러스터 상태 청크를 반환하며, 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="26618-350">hello 클러스터 상태를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="26618-351">hello 상태 상태 청크는 노드의 목록이 입력된 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="26618-352">hello 상태 상태 청크 목록이 입력된 필터를 적용 하는 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="26618-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="26618-353">입력된 필터 및 청크 목록이 hello 필터를 적용 하는 모든 배포 된 응용 프로그램으로 적용 하는 모든 서비스와 청크 목록을 포함 하는 각 응용 프로그램 상태 상태 청크 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="26618-354">서비스 및 응용 프로그램 배포 된 hello 자식에 대 한 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="26618-355">이러한 방식으로를 계층 형태로 요청 하는 경우 hello 클러스터의 모든 엔터티를 잠재적으로 반환 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="26618-356">클러스터 상태 청크 쿼리</span><span class="sxs-lookup"><span data-stu-id="26618-356">Cluster health chunk query</span></span>
<span data-ttu-id="26618-357">반환 상태 hello 클러스터 엔터티의 hello를 필수 자식의 hello 계층적 상태 상태 청크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="26618-358">입력:</span><span class="sxs-lookup"><span data-stu-id="26618-358">Input:</span></span>

* <span data-ttu-id="26618-359">[선택 사항] hello 클러스터 상태 정책 tooevaluate hello 노드와 hello 클러스터 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="26618-360">[선택 사항] hello 응용 프로그램 상태 정책 지도 hello 상태 정책을 사용 하 여 toooverride hello 응용 프로그램 매니페스트 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="26618-361">[선택 사항] 노드 및 되는 항목을 지정 하는 응용 프로그램에 대 한 필터 관심 및 hello 결과에 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="26618-362">hello 필터 특정 tooan 엔터티/엔터티 그룹 이거나 해당 수준에서 적용 가능한 tooall 엔터티 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="26618-363">필터 목록 hello 하나의 일반적인 필터 및/또는 필터 hello 쿼리에 의해 반환 되는 특정 식별자 toofine 세부 수준 엔터티를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="26618-364">비어 있는 경우 기본적으로 hello 자식은 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="26618-365">Hello 필터에 대 한 자세한 설명 [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) 및 [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="26618-366">hello 응용 프로그램 필터 수 재귀적으로 자식에 대 한 고급 필터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="26618-367">hello 청크 결과 hello 필터를 적용 하는 hello 자식을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="26618-368">현재 비정상 상태의 평가 또는 엔터티 이벤트 hello 청크 쿼리 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="26618-369">Hello 기존 클러스터 상태 쿼리를 사용 하 여 추가 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="26618-370">API</span><span class="sxs-lookup"><span data-stu-id="26618-370">API</span></span>
<span data-ttu-id="26618-371">tooget 클러스터 상태 청크를 만들고는 `FabricClient` 및 호출 hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) 메서드를 해당 **HealthManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="26618-372">에 전달할 수 있습니다 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe 상태 정책 및 고급 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="26618-373">hello 다음 코드 청크를 가져옵니다 클러스터 상태 고급 필터.</span><span class="sxs-lookup"><span data-stu-id="26618-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="26618-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26618-374">PowerShell</span></span>
<span data-ttu-id="26618-375">hello cmdlet tooget hello 클러스터 상태 설명이 [Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="26618-376">첫째, toohello 클러스터 hello를 사용 하 여 연결 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26618-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="26618-377">hello 다음 코드에서는 노드 항상 반환 되어야 하는 특정 노드를 제외 하 고 오류가 있는 경우에</span><span class="sxs-lookup"><span data-stu-id="26618-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="26618-378">hello cmdlet을 다음 응용 프로그램 필터와 클러스터 청크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26618-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="26618-379">hello 다음 cmdlet 엔터티를 반환 배포 된 모든 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="26618-380">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="26618-380">REST</span></span>
<span data-ttu-id="26618-381">클러스터 상태 청크를 얻을 수 있습니다는 [GET 요청](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) 또는 [POST 요청](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) 이 포함 된 상태 정책을 hello 본문에서 설명 하는 고급 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="26618-382">일반 쿼리</span><span class="sxs-lookup"><span data-stu-id="26618-382">General queries</span></span>
<span data-ttu-id="26618-383">일반 쿼리는 지정된 형식의 서비스 패브릭 엔터티 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="26618-384">Hello API 통해 노출 됩니다 (hello에 대 한 메서드를 통해 **FabricClient.QueryManager**), PowerShell cmdlet 및 REST 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="26618-385">이러한 쿼리는 여러 구성 요소에서 하위 쿼리를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="26618-386">그 중 하나는 hello [상태 저장소](service-fabric-health-introduction.md#health-store), 각 쿼리 결과 대 한 성능 상태를 집계 하는 hello를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="26618-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="26618-387">일반 쿼리는 hello 엔터티의 집계 hello 성능 상태를 반환 하 고 풍부한 상태 데이터가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="26618-388">엔터티 상태가 정상이 아닌 경우 있습니다 수 구성에 따라 상태 쿼리 tooget 이벤트, 자식 상태 및 비정상 상태의 평가 비롯 한 모든 상태 정보를 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="26618-389">엔터티에 대 한 알 수 없는 상태를 반환 하는 일반 쿼리 불가능 해당 hello 상태 저장소에 없는 hello 엔터티에 대 한 완전 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="26618-390">하위 쿼리 toohello 상태 저장소 되지 않았지만 있는지 수 이기도 (예를 들어, 통신 오류 또는 hello 상태 저장소 제한 되었다는).</span><span class="sxs-lookup"><span data-stu-id="26618-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="26618-391">Hello 엔터티에 대 한 상태 쿼리 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="26618-392">Hello 하위 네트워크 문제와 같은 일시적인 오류를 발생 하는 경우이 후속 쿼리는 성공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="26618-393">또한을 줄 수 자세히 hello 엔터티 노출 되지 않는 하는 방법에 대 한 hello health store에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="26618-394">쿼리를 포함 하는 hello **HealthState** 엔터티는:</span><span class="sxs-lookup"><span data-stu-id="26618-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="26618-395">노드 목록: (페이징) hello 클러스터 hello 목록 노드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="26618-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="26618-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="26618-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="26618-398">응용 프로그램 목록: (페이징) hello 클러스터의 응용 프로그램 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="26618-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="26618-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="26618-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="26618-401">서비스 목록: (페이징) 응용 프로그램에서 서비스 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="26618-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="26618-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="26618-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="26618-404">파티션 목록: (페이징) 서비스에 있는 파티션의 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="26618-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="26618-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="26618-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="26618-407">복제본 목록: (페이징) 파티션의 복제본 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="26618-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="26618-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="26618-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="26618-410">배포 응용 프로그램 목록: 노드에 배포 된 응용 프로그램의 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="26618-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="26618-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="26618-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="26618-413">서비스 패키지 목록 배포: 배포 된 응용 프로그램의 서비스 패키지 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="26618-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="26618-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="26618-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="26618-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="26618-416">Hello 쿼리의 일부 페이지 된 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="26618-417">hello 반환 이러한 쿼리는 목록에서 파생 된 [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="26618-418">Hello 결과 메시지에 맞지 않으면, 페이지에만 반환 되 고 열거형에서 중지 된 추적는 ContinuationToken 하는.</span><span class="sxs-lookup"><span data-stu-id="26618-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="26618-419">동일한 쿼리 한 hello 이전 쿼리 tooget 다음 결과에서 hello continuation 토큰을 전달 toocall hello를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="26618-420">예</span><span class="sxs-lookup"><span data-stu-id="26618-420">Examples</span></span>
<span data-ttu-id="26618-421">hello 다음 코드 hello 비정상 상태 응용 프로그램을의 가져옵니다 hello 클러스터:</span><span class="sxs-lookup"><span data-stu-id="26618-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="26618-422">hello 다음 cmdlet을 가져옵니다 hello 패브릭에 대 한 hello 응용 프로그램 세부 정보: / WordCount 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="26618-423">성능 상태는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="26618-424">hello 다음 cmdlet을 가져옵니다 상태가 error 사용 하 여 hello 서비스를:</span><span class="sxs-lookup"><span data-stu-id="26618-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="26618-425">클러스터 및 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="26618-425">Cluster and application upgrades</span></span>
<span data-ttu-id="26618-426">서비스 패브릭 hello 클러스터와 응용 프로그램의 모니터링 되는 업그레이드 중 모든 남아 정상 상태 tooensure를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="26618-427">엔터티를 구성 된 상태 정책을 사용 하 여 계산한 정상 없으면 hello 업그레이드 업그레이드 관련 정책을 toodetermine hello 다음 동작을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="26618-428">이 자동으로 롤백합니다 toohello 이전 버전 되었거나 hello 업그레이드 (예: 오류 상태를 수정 하거나 정책이 변경), 일시 중지 된 tooallow 사용자 상호 작용을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="26618-429">중는 *클러스터* 업그레이드를 얻을 수 있습니다 hello 클러스터 업그레이드 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="26618-430">hello 업그레이드 상태 비정상 상태의 평가, 어떤 지점 toowhat hello 클러스터의 상태가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="26618-431">Hello 업그레이드가 롤백되면 toohealth 문제 인해 hello 업그레이드 상태 hello 마지막 비정상 이유를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="26618-432">이 정보에는 관리자 hello 업그레이드 롤백 또는 중지 후 잘못 된 부분을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="26618-433">마찬가지로, 동안는 *응용 프로그램* 업그레이드, 모든 비정상 상태의 평가 hello 응용 프로그램 업그레이드 상태에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26618-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="26618-434">hello 다음 테이블에 나와 hello 응용 프로그램 업그레이드 상태에 대 한 수정 된 패브릭: / WordCount 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="26618-435">watchdog에서 복제본 하나에서 오류를 보고했습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="26618-436">hello 상태 검사를 준수 하지 않을 서 hello 업그레이드 중입니다.</span><span class="sxs-lookup"><span data-stu-id="26618-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="26618-437">Hello에 대 한 자세한 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="26618-438">상태 평가 tootroubleshoot를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="26618-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="26618-439">Hello 클러스터 또는 응용 프로그램에 문제가 있을 때마다 확인 hello 클러스터 또는 응용 프로그램 상태 toopinpoint 문제가 무엇 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="26618-440">비정상 상태의 평가 hello 트리거된 hello 현재 비정상 상태에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="26618-441">해야 할 경우에 비정상 상태의 자식 엔터티 tooidentify hello 근본 원인을 다운 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="26618-442">예를 들어, 복제본 중 하나에서 오류를 보고하여 상태가 비정상인 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="26618-443">hello 다음 Powershell cmdlet으로 다음과 같은 hello 비정상 상태의 평가</span><span class="sxs-lookup"><span data-stu-id="26618-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="26618-444">자세한 내용은 hello 복제본 tooget를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="26618-445">hello 비정상 상태의 평가 표시 hello 첫 번째 이유 hello 엔터티는 평가 toocurrent 상태.</span><span class="sxs-lookup"><span data-stu-id="26618-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="26618-446">이 상태를 트리거하는 여러 다른 이벤트가 있을 수 있지만 hello 평가에 반영 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26618-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="26618-447">tooget 자세한 내용은 hello 상태 엔터티 toofigure hello 클러스터의 모든 hello 비정상 보고서로 드릴 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="26618-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="26618-448">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26618-448">Next steps</span></span>
[<span data-ttu-id="26618-449">시스템 상태 보고서 tootroubleshoot를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="26618-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="26618-450">사용자 지정 서비스 패브릭 상태 보고서 추가</span><span class="sxs-lookup"><span data-stu-id="26618-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="26618-451">어떻게 tooreport 및 확인 서비스 상태</span><span class="sxs-lookup"><span data-stu-id="26618-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="26618-452">로컬로 서비스 모니터링 및 진단</span><span class="sxs-lookup"><span data-stu-id="26618-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="26618-453">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="26618-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
