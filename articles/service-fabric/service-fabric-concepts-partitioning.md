---
title: "Service Fabric 서비스 분할 | Microsoft Docs"
description: "Service Fabric 상태 저장 서비스를 분할하는 방법을 설명합니다. 파티션을 사용하면 로컬 컴퓨터에 데이터가 저장되므로 데이터와 계산을 함께 확장할 수 있습니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="6df8e-104">서비스 패브릭 Reliable Services 분할</span><span class="sxs-lookup"><span data-stu-id="6df8e-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="6df8e-105">이 문서에서는 Azure 서비스 패브릭 Reliable Services 분할의 기본 개념에 대한 소개를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="6df8e-106">문서에 사용되는 소스 코드는 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="6df8e-107">분할</span><span class="sxs-lookup"><span data-stu-id="6df8e-107">Partitioning</span></span>
<span data-ttu-id="6df8e-108">분할은 서비스 패브릭에만 있는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="6df8e-109">사실, 분할은 확장 가능한 서비스 구축의 코어 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="6df8e-110">광범위한 의미로 분할을 상태(데이터) 분할의 개념으로 생각하고 확장성 및 성능 향상을 위해 더 작은 액세스 가능한 단위로 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="6df8e-111">분할의 잘 알려진 양식은 [데이터 분할][wikipartition]로서 분할이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="6df8e-112">서비스 패브릭 상태 비저장 분할 서비스</span><span class="sxs-lookup"><span data-stu-id="6df8e-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="6df8e-113">상태 비저장 서비스의 경우 하나 이상의 서비스의 인스턴스를 포함하는 논리 단위가 되는 파티션으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="6df8e-114">그림 1에서는 하나의 파티션을 사용하는 클러스터에 분산된 5개의 인스턴스로 상태 비저장 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![상태 비저장 서비스](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="6df8e-116">실제로 두 종류의 상태 비저장 서비스 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="6df8e-117">첫 번째는 Azure SQL 데이터베이스처럼 외부적으로 상태를 유지하는 서비스(세션 정보 및 데이터를 저장하는 웹 사이트처럼)입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="6df8e-118">두 번째는 모든 영구적 상태를 관리하지 않는 계산 전용 서비스(예: 계산기 또는 이미지 미리 보기)입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="6df8e-119">두 경우 모두 상태 비저장 서비스 분할은 매우 드문 시나리오이며 확장성 및 가용성은 일반적으로 더 많은 인스턴스를 추가하여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="6df8e-120">상태 비저장 서비스 인스턴스에 대한 여러 파티션을 고려하려는 경우는 특별한 라우팅 요청을 충족해야 하는 때입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="6df8e-121">한 예로 특정 범위의 ID가 있는 사용자가 특정한 서비스 인스턴스로만 제공되어야 하는 경우 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="6df8e-122">상태 비저장 서비스를 분할할 수 있는 경우의 다른 예는 분할된 SQL 데이터베이스와 같은 실제로 분할된 백 엔드가 있는 경우와 데이터베이스 분할에 작성하거나 백 엔드에서 사용되므로 동일한 분할 정보가 필요한 상태 비저장 서비스 내에서 다른 준비 작업을 수행해야 하는 서비스 인스턴스를 제어하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="6df8e-123">이러한 유형의 시나리오는 다른 방법으로 해결될 수 있으며 서비스 분할이 반드시 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="6df8e-124">이 연습의 나머지 부분에서는 상태 저장 서비스에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="6df8e-125">서비스 패브릭 상태 저장 분할 서비스</span><span class="sxs-lookup"><span data-stu-id="6df8e-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="6df8e-126">서비스 패브릭은 파티션 상태(데이터)에 최상의 방법을 제공하여 확장 가능한 상태 저장 서비스를 쉽게 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="6df8e-127">개념적으로 상태 저장 서비스의 파티션이란 클러스터의 노드에 배포 및 분산된 [복제본](service-fabric-availability-services.md) 을 통해 매우 안정적으로 배율이 조정되는 배율 단위로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="6df8e-128">서비스 패브릭 상태 저장 서비스의 컨텍스트에서 분할은 특정 서비스 파티션이 서비스 전체 상태의 부분을 담당하는 것을 결정하는 프로세스를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="6df8e-129">(앞서 언급했듯이 파티션은 [복제본](service-fabric-availability-services.md)의 집합입니다.)</span><span class="sxs-lookup"><span data-stu-id="6df8e-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="6df8e-130">서비스 패브릭에 대한 흥미로운 사항은 다른 노드에 파티션을 배치하기 때문에</span><span class="sxs-lookup"><span data-stu-id="6df8e-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="6df8e-131">노드의 리소스 제한까지 확장이 가능하다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="6df8e-132">데이터 요구 사항이 늘어나고 파티션이 늘어나면 서비스 패브릭이 노드 간에 파티션의 균형을 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="6df8e-133">따라서 하드웨어 리소스가 계속해서 효율적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="6df8e-134">예를 들어 5 노드 클러스터와 10개의 파티션 및 세 복제본의 대상을 가지도록 구성된 서비스로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="6df8e-135">이 경우 서비스 패브릭은 클러스터에 복제본을 분산 및 배포하고 노드당 2개의 기본 [복제본](service-fabric-availability-services.md) 이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="6df8e-136">클러스터를 10개의 노드로 확장해야 하는 경우 서비스 패브릭은 10개의 모든 노드에 기본 [복제본](service-fabric-availability-services.md) 을 다시 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="6df8e-137">마찬가지로 5개의 노드로 다시 조정하는 경우 서비스 패브릭은 5개의 노드로 모든 복제본을 다시 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="6df8e-138">그림 2는 클러스터 크기 조정 전과 후의 10개의 파티션 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![상태 저장 서비스](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="6df8e-140">결과적으로 클라이언트의 요청이 컴퓨터 간에 분산되므로 확장이 달성되고 응용 프로그램의 전체 성능이 향상되며 데이터의 청크에 대한 액세스의 경합이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="6df8e-141">분할에 대한 계획</span><span class="sxs-lookup"><span data-stu-id="6df8e-141">Plan for partitioning</span></span>
<span data-ttu-id="6df8e-142">서비스를 구현하기 전에 확장하는 데 필요한 분할 전략을 항상 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="6df8e-143">여러 가지 방법이 있지만 모든 방법은 응용 프로그램이 달성해야 하는 것에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="6df8e-144">이 문서의 컨텍스트에 대해 몇 가지 더 중요한 측면을 생각해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="6df8e-145">첫 단계로 분할되어야 하는 상태의 구조에 대해 생각하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="6df8e-146">간단한 예를 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-146">Let's take a simple example.</span></span> <span data-ttu-id="6df8e-147">카운티 단위의 투표에 대한 서비스를 구축하는 경우 카운티의 각 도시에 대한 파티션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="6df8e-148">그런 다음 그 도시에 해당하는 파티션에 있는 도시에 속한 모든 사람의 투표 결과를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="6df8e-149">그림 3은 사람과 거주하는 도시의 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![간단한 파티션](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="6df8e-151">도시의 인구는 다르므로 많은 양의 데이터(예: 시애틀)를 포함하는 일부 파티션 및 매우 적은 상태(예: 커클랜드)의 다른 파티션이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="6df8e-152">따라서 상태의 균등하지 않은 양으로 파티션을 갖는 것의 영향을 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6df8e-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="6df8e-153">예를 다시 생각해 본다면 시애틀에 대한 투표를 가진 파티션이 커클랜드의 파티션에 비해 더 많은 트래픽을 얻는 것을 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="6df8e-154">기본적으로 서비스 패브릭은 각 노드의 기본 및 보조 복제본 수를 거의 비슷하게 유지하므로</span><span class="sxs-lookup"><span data-stu-id="6df8e-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="6df8e-155">노드의 어떤 복제본은 트래픽을 더 많이 처리하고 어떤 복제본은 트래픽을 더 적게 처리하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="6df8e-156">클러스터에서 다음과 같이 핫(hot) 및 콜드(cold) 지점을 방지하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="6df8e-157">이를 방지하기 위해 분할 관점에서 두 가지를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="6df8e-158">상태를 분할하도록 시도하여 모든 파티션에 균등하게 분산되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="6df8e-159">서비스에 대한 각 복제본에서 부하를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="6df8e-160">(방법에 대한 자세한 정보는 이 문서의 [메트릭 및 부하](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요).</span><span class="sxs-lookup"><span data-stu-id="6df8e-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="6df8e-161">서비스 패브릭은 메모리의 양 또는 레코드 수와 같은 서비스에서 사용한 부하를 보고하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="6df8e-162">보고된 메트릭에 따라 서비스 패브릭은 일부 파티션이 다른 파티션보다 더 높은 부하를 처리하는 것을 감지하고 복제본을 더 적합한 노드로 이동하여 클러스터를 다시 분산하므로 전체적으로 어떤 노드도 오버로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="6df8e-163">때때로 지정된 파티션에 얼마나 많은 데이터가 있는지 알 수 없는 경우가 있으므로</span><span class="sxs-lookup"><span data-stu-id="6df8e-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="6df8e-164">첫째로 파티션에 균등하게 데이터를 분산하는 분할 전략을 도입하고 둘째로 부하를 보고하여 모두를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="6df8e-165">첫 번째 방법은 투표 예제에 설명된 상황을 예방하고 두 번째 방법은 시간이 지남에 따라 액세스 또는 부하의 임시적인 차이를 해결하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="6df8e-166">파티션 계획의 다른 측면은 올바른 파티션 수로 시작하도록 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="6df8e-167">서비스 패브릭 관점에서 시나리오의 예상 파티션 수보다 더 많은 파티션으로 시작하지 못할 이유는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="6df8e-168">사실, 파티션 수를 최대로 늘리는 것도 유효한 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="6df8e-169">드물기는 하지만 처음에 선택한 것보다 더 많은 파티션이 필요하게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="6df8e-170">사후에 파티션 수를 변경할 수 없으므로 서비스 유형이 동일한 새 서비스 인스턴스를 만드는 것처럼 보다 발전된 파티션 접근 방식을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="6df8e-171">또한 클라이언트 코드에서 유지해야 하는 클라이언트 쪽 기술 자료에 따라 요청을 올바른 서비스 인스턴스로 라우팅하는 클라이언트 쪽 논리를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="6df8e-172">분할 계획에 대해 고려해야 할 다른 사항은 사용 가능한 컴퓨터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="6df8e-173">상태는 액세스되고 저장되어야 하므로 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="6df8e-174">네트워크 대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="6df8e-174">Network bandwidth limits</span></span>
* <span data-ttu-id="6df8e-175">시스템 메모리 제한</span><span class="sxs-lookup"><span data-stu-id="6df8e-175">System memory limits</span></span>
* <span data-ttu-id="6df8e-176">디스크 저장소 제한</span><span class="sxs-lookup"><span data-stu-id="6df8e-176">Disk storage limits</span></span>

<span data-ttu-id="6df8e-177">그렇다면 실행 중인 클러스터에 리소스 제약이 발생하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="6df8e-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="6df8e-178">단순히 새 요구 사항에 맞게 클러스터를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="6df8e-179">[용량 계획 가이드](service-fabric-capacity-planning.md) 는 클러스터에서 필요한 노드 수를 결정하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="6df8e-180">분할 시작</span><span class="sxs-lookup"><span data-stu-id="6df8e-180">Get started with partitioning</span></span>
<span data-ttu-id="6df8e-181">이 섹션에는 서비스 분할을 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="6df8e-182">서비스 패브릭은 세 가지 파티션 체계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="6df8e-183">범위 지정된 분할(UniformInt64Partition이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="6df8e-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="6df8e-184">이름 지정된 분할.</span><span class="sxs-lookup"><span data-stu-id="6df8e-184">Named partitioning.</span></span> <span data-ttu-id="6df8e-185">일반적으로 이 모델을 사용한 응용 프로그램에는 제한된 집합 내에 버킷 가능한 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="6df8e-186">이름 지정된 파티션 키로 사용되는 데이터 필드의 몇 가지 일반적인 예는 지역, 우편 번호, 고객 그룹 또는 기타 비즈니스 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="6df8e-187">단일 분할</span><span class="sxs-lookup"><span data-stu-id="6df8e-187">Singleton partitioning.</span></span> <span data-ttu-id="6df8e-188">단일 파티션은 서비스가 추가 라우팅이 필요하지 않은 경우에 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="6df8e-189">예를 들어 상태 비저장 서비스는 기본적으로 이 파티션 체계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="6df8e-190">이름 지정된 분할 체계 및 단일 분할 체계는 범위 지정된 파티션의 특별한 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="6df8e-191">기본적으로 서비스 패브릭에 대한 Visual Studio 템플릿은 가장 일반적이고 유용한 것이므로 범위 지정된 분할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="6df8e-192">이 문서의 나머지 부분에서는 범위 지정된 파티션 체계에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="6df8e-193">범위 지정된 분할 체계</span><span class="sxs-lookup"><span data-stu-id="6df8e-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="6df8e-194">정수 범위(하위 및 상위 키로 식별됨) 및 파티션의 수(n)를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="6df8e-195">전체 파티션 키 범위의 겹치지 않는 하위 범위를 각각 담당하는 n 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="6df8e-196">예를 들어 하위 키 0, 상위 키 99 및 숫자 4로 범위 지정된 분할 체계는 다음과 같이 4개의 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![범위 분할](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="6df8e-198">일반적인 방법은 데이터 집합 내에서 고유 키를 기반으로 해시를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="6df8e-199">키의 일부 일반적인 예로는 차량 식별 번호(VIN), 직원 ID 또는 고유 문자열을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="6df8e-200">고유 키를 사용하여 해시 코드를 생성하고 키 범위를 계수하여 키로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="6df8e-201">허용되는 키 범위의 상한 및 하한 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="6df8e-202">해시 알고리즘 선택</span><span class="sxs-lookup"><span data-stu-id="6df8e-202">Select a hash algorithm</span></span>
<span data-ttu-id="6df8e-203">해시의 중요한 부분은 해시 알고리즘을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="6df8e-204">서로 가까운 유사한 키를 그룹화하는 것이 목적인지(집약성을 중요시하는 해시), 또는 더욱 일반적인 경우인 활동이 모든 파티션에 널리 배포되는지(배포 해시) 여부를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="6df8e-205">적절한 배포 해시 알고리즘의 특징은 계산하기 쉽고 충돌이 적고 키를 균등하게 배분하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="6df8e-206">효율적인 해시 알고리즘의 좋은 예로 [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) 해시 알고리즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="6df8e-207">일반적인 해시 코드 알고리즘 선택에 대한 좋은 리소스는 [해시 기능에 대한 Wikipedia 페이지](http://en.wikipedia.org/wiki/Hash_function)입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="6df8e-208">여러 파티션으로 상태 저장 서비스 구축</span><span class="sxs-lookup"><span data-stu-id="6df8e-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="6df8e-209">여러 파티션으로 첫 번째 신뢰할 수 있는 상태 저장 서비스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="6df8e-210">이 예에서 동일한 파티션에 동일한 문자로 시작하는 모든 성을 저장하려는 매우 간단한 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="6df8e-211">모든 코드를 작성하기 전에 파티션 및 파티션 키에 대해 생각해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="6df8e-212">알파벳의 각 문자로 26개의 파티션이 필요하지만 하위 키 및 상위 키는 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="6df8e-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="6df8e-213">문자 그대로 문자당 하나의 파티션을 가지려 하기 때문에 각 문자는 해당 키이므로 하위 키로 0을, 상위 키로 25를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="6df8e-214">실제로는 균등하게 분산되지 않으므로 여기서는 간소화된 시나리오를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="6df8e-215">문자 "S" 또는 "M"으로 시작하는 성이 "X" 또는 "Y"로 시작하는 성보다 더 많습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="6df8e-216">**Visual Studio** > **파일** > **새로 만들기** > **프로젝트**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="6df8e-217">**새 프로젝트** 대화 상자에서 서비스 패브릭 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="6df8e-218">"AlphabetPartitions" 프로젝트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="6df8e-219">**서비스 만들기** 대화 상자에서 **상태 저장** 서비스를 선택하고 아래 이미지에 표시된 것처럼 "Alphabet.Processing"으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="6df8e-220">![Visual Studio의 새 서비스 대화 상자][1]</span><span class="sxs-lookup"><span data-stu-id="6df8e-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="6df8e-221">파티션 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-221">Set the number of partitions.</span></span> <span data-ttu-id="6df8e-222">AlphabetPartitions 프로젝트에서 ApplicationPackageRoot 폴더에 있는 ApplicationManifest.xml 파일을 열고 아래와 같이 매개 변수 Processing_PartitionCount를 26으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="6df8e-223">또한 아래와 같이 ApplicationManifest.xml에 있는 StatefulService 요소의 LowKey 및 HighKey 속성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="6df8e-224">서비스에 액세스할 수 있게 만들려면 아래와 같이 Alphabet.Processing 서비스에 대한 ServiceManifest.xml(PackageRoot 폴더에 있음)의 끝점 요소를 추가하여 포트의 끝점을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="6df8e-225">이제 26 파티션으로 내부 끝점을 수신하도록 서비스가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="6df8e-226">다음으로 처리 클래스의 `CreateServiceReplicaListeners()` 메서드를 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6df8e-227">이 샘플의 경우 간단한 HttpCommunicationListener를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="6df8e-228">Reliable Services 통신에 대한 자세한 내용은 [Reliable Services 통신 모델](service-fabric-reliable-services-communication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6df8e-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="6df8e-229">복제본이 수신하는 URL에 대한 권장 패턴은 `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="6df8e-230">따라서 통신 수신기가 올바른 끝점에서 이 패턴을 사용하여 수신하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="6df8e-231">이 서비스의 여러 복제본은 동일한 컴퓨터에서 호스팅될 수 있으므로 이 주소가 복제본에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="6df8e-232">이 때문에 URL에 파티션 ID와 복제본 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="6df8e-233">HttpListener는 URL 접두사가 고유하기만 하면 동일한 포트에서 여러 주소를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="6df8e-234">추가 GUID는 보조 복제본이 읽기 전용 요청을 수신하는 고급 사례에 대해 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="6df8e-235">이 경우 클라이언트가 주소를 다시 확인하도록 기본에서 보조로 전환하는 경우 고유한 새 주소가 사용되도록 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="6df8e-236">'+'는 사용 가능한 모든 호스트(IP, FQDM, localhost, 등)에서 복제본이 수신 대기할 수 있도록 주소로 사용됩니다. 아래 코드는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="6df8e-237">게시된 URL은 수신 대기 URL 접두사와 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="6df8e-238">수신 대기 URL이 HttpListener에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="6df8e-239">게시된 URL은 서비스 검색에 사용되는 서비스 패브릭 이름 명명 서비스에 게시된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="6df8e-240">클라이언트는 해당 검색 서비스를 통해 이 주소에 대해 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="6df8e-241">클라이언트가 가져오는 주소에 연결하려면 노드의 실제 IP 또는 FQDN이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="6df8e-242">따라서 아래와 같이 '+'를 노드의 IP 또는 FQDN으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="6df8e-243">마지막 단계는 아래와 같이 서비스에 처리 논리를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="6df8e-244">`ProcessInternalRequest`는 파티션을 호출하는 데 사용되는 쿼리 문자열 매개 변수의 값을 읽고 신뢰할 수 있는 사전 `dictionary`에 성을 추가하도록 `AddUserAsync`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="6df8e-245">특정 파티션을 호출할 수 있는 방법을 보도록 프로젝트에 상태 비저장 서비스를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="6df8e-246">이 서비스는 쿼리 문자열 매개 변수로 성을 수락하고 파티션 키를 결정하고 처리를 위해 Alphabet.Processing에 이를 보내는 간단한 웹 인터페이스로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="6df8e-247">**서비스 만들기** 대화 상자에서 **상태 비저장** 서비스를 선택하고 아래와 같이 “Alphabet.Web”으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![상태 비저장 서비스 스크린 샷](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="6df8e-249">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-249">.</span></span>
12. <span data-ttu-id="6df8e-250">Alphabet.WebApi 서비스의 ServiceManifest.xml에서 끝점 정보를 업데이트하여 아래와 같이 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="6df8e-251">Web 클래스의 ServiceInstanceListeners 컬렉션을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="6df8e-252">다시 간단한 HttpCommunicationListener를 구현하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="6df8e-253">이제 처리 논리를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="6df8e-254">HttpCommunicationListener는 요청이 들어올 때 `ProcessInputRequest` 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="6df8e-255">따라서 계속해서 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-255">So let's go ahead and add the code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="6df8e-256">단계 별로 안내하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-256">Let's walk through it step by step.</span></span> <span data-ttu-id="6df8e-257">코드는 쿼리 문자열 매개 변수 `lastname` 의 첫 글자를 char로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="6df8e-258">그런 다음 성의 첫 글자에 있는 16진수 값에서 `A` 의 16진수 값을 빼서 이 글자에 대한 파티션 키를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="6df8e-259">이 예제에서 파티션당 하나의 파티션 키를 가진 26개의 파티션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="6df8e-260">그런 다음 `servicePartitionResolver` 개체의 `ResolveAsync` 메서드를 사용하여 이 키에 대한 서비스 파티션 `partition`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="6df8e-261">`servicePartitionResolver` 는 다음으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="6df8e-262">`ResolveAsync` 메서드는 매개 변수로 서비스 URI, 파티션 키 및 취소 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="6df8e-263">처리 서비스의 서비스 URI는 `fabric:/AlphabetPartitions/Processing`입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="6df8e-264">그런 다음 파티션의 끝점을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="6df8e-265">마지막으로 끝점 URL 및 쿼리 문자열을 작성하고 처리 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="6df8e-266">처리가 완료되면 출력을 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="6df8e-267">마지막 단계는 서비스를 테스트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-267">The last step is to test the service.</span></span> <span data-ttu-id="6df8e-268">Visual Studio에서는 로컬 및 클라우드 배포에 대해 응용 프로그램 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="6df8e-269">26개의 파티션이 있는 서비스를 로컬에서 테스트하려면 아래와 같이 AlphabetPartitions 프로젝트의 ApplicationParameters 폴더에 있는 `Local.xml` 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="6df8e-270">배포가 완료되면 서비스 패브릭 탐색기에서 서비스 및 모든 해당 파티션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![서비스 패브릭 탐색기 스크린 샷](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="6df8e-272">브라우저에서 `http://localhost:8081/?lastname=somename`을 입력하여 분할 논리를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="6df8e-273">동일한 문자로 시작하는 각 성이 동일한 파티션에 저장되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![브라우저 스크린 샷](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="6df8e-275">샘플의 전체 소스 코드는 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df8e-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6df8e-276">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6df8e-276">Next steps</span></span>
<span data-ttu-id="6df8e-277">서비스 패브릭 개념에 대한 자세한 내용은 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6df8e-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="6df8e-278">서비스 패브릭 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="6df8e-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="6df8e-279">서비스 패브릭 서비스의 확장성</span><span class="sxs-lookup"><span data-stu-id="6df8e-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="6df8e-280">서비스 패브릭 응용 프로그램의 용량 계획</span><span class="sxs-lookup"><span data-stu-id="6df8e-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png