---
title: "서비스 패브릭 서비스 aaaPartitioning | Microsoft Docs"
description: "설명 방법을 toopartition 서비스 패브릭 상태 저장 서비스입니다. 데이터 및 계산 함께 배율을 조정할 수 있으므로 파티션을 hello 로컬 컴퓨터에 데이터 저장소를 수 있습니다."
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
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="c4768-104">서비스 패브릭 Reliable Services 분할</span><span class="sxs-lookup"><span data-stu-id="c4768-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="c4768-105">이 문서에서는 소개 toohello 분할 신뢰할 수 있는 Azure 서비스 패브릭 서비스의 기본 개념을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="c4768-106">hello hello 문서에 사용 되는 소스 코드에서 사용할 수도 있습니다 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="c4768-107">분할</span><span class="sxs-lookup"><span data-stu-id="c4768-107">Partitioning</span></span>
<span data-ttu-id="c4768-108">분할은 고유 tooService 패브릭 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="c4768-109">사실, 분할은 확장 가능한 서비스 구축의 코어 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="c4768-110">넓은 의미에서 상태 (데이터)로 나눈 개념으로 서 분할 하는 방법에 대 한 생각 하 고 더 작은 액세스할 수 있는 단위 tooimprove 확장성 및 성능에 계산 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="c4768-111">분할의 잘 알려진 양식은 [데이터 분할][wikipartition]로서 분할이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="c4768-112">서비스 패브릭 상태 비저장 분할 서비스</span><span class="sxs-lookup"><span data-stu-id="c4768-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="c4768-113">상태 비저장 서비스의 경우 하나 이상의 서비스의 인스턴스를 포함하는 논리 단위가 되는 파티션으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="c4768-114">그림 1에서는 하나의 파티션을 사용하는 클러스터에 분산된 5개의 인스턴스로 상태 비저장 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![상태 비저장 서비스](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="c4768-116">실제로 두 종류의 상태 비저장 서비스 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="c4768-117">hello 먼저 하나입니다 (예: hello 세션 정보 및 데이터를 저장 하는 웹 사이트)는 Azure SQL 데이터베이스에서 예를 들어 외부적으로 상태를 유지 하는 서비스.</span><span class="sxs-lookup"><span data-stu-id="c4768-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="c4768-118">hello 두 번째 메서드는 모든 영구 상태를 관리 하지 않는 서비스 (예: 미리 보기 계산기 또는 이미지) 계산 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="c4768-119">두 경우 모두 상태 비저장 서비스 분할은 매우 드문 시나리오이며 확장성 및 가용성은 일반적으로 더 많은 인스턴스를 추가하여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="c4768-120">상태 비저장 서비스 인스턴스를 여러 파티션에 특별 한 라우팅 toomeet 해야 할 때 tooconsider 원하는 hello 유일한 시간을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="c4768-121">한 예로 특정 범위의 ID가 있는 사용자가 특정한 서비스 인스턴스로만 제공되어야 하는 경우 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="c4768-122">상태 비저장 서비스를 분할 수 때의 또 다른 예는 진정으로 분할 된 백 엔드 (예: 분할 된 SQL 데이터베이스) 있고 toocontrol 대상 서비스 인스턴스 해야 toohello 데이터베이스 분할 영역-쓰거나 내에서 다른 준비 작업을 수행 하려는 경우 hello 요구 하는 상태 비저장 서비스 hello 동일 hello 백 엔드에 사용 되는 정보를 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="c4768-123">이러한 유형의 시나리오는 다른 방법으로 해결될 수 있으며 서비스 분할이 반드시 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="c4768-124">이 연습의 나머지 부분에서는 hello 상태 저장 서비스에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="c4768-125">서비스 패브릭 상태 저장 분할 서비스</span><span class="sxs-lookup"><span data-stu-id="c4768-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="c4768-126">서비스 패브릭을 사용 하면 쉽게 toodevelop 확장 가능한 상태 저장 서비스는 최상의 방법을 제공 하 여 toopartition 상태 (데이터).</span><span class="sxs-lookup"><span data-stu-id="c4768-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="c4768-127">개념적으로 생각해볼 수 있겠습니다 상태 저장 서비스의 파티션을 통해 매우 신뢰할 수 있는 확장 단위로 [복제본](service-fabric-availability-services.md) 분산 되 고 클러스터의 노드 hello에서 균형이 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="c4768-128">서비스 패브릭 상태 저장 서비스의 hello 컨텍스트에서 분할은 특정 서비스 파티션 hello 서비스의 전체 상태 hello의 일부에 대 한 책임 지는 결정 하는 toohello 프로세스를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="c4768-129">(앞서 언급했듯이 파티션은 [복제본](service-fabric-availability-services.md)의 집합입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4768-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="c4768-130">서비스 패브릭에 대 한 훌륭한 점 hello 파티션을 서로 다른 노드에 배치 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="c4768-131">따라서 toogrow tooa 노드 리소스 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="c4768-132">Hello 데이터 요구 사항이 증가, 파티션을 증가 하 고 서비스 패브릭 노드 간에 파티션이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="c4768-133">이렇게 하면 hello 계속 하드웨어 리소스를 효율적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="c4768-134">toogive 예를 들어 알고 계십니까 있습니다 5 노드 클러스터와 구성 된 toohave 10 파티션과 대상 세 개의 복제본은 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="c4768-135">이 경우 서비스 패브릭은 균형을 조정 hello 복제본 hello 클러스터-분산 고 결국에 두 개의 주와 [복제본](service-fabric-availability-services.md) 노드당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="c4768-136">Hello 클러스터 too10 노드 tooscale, 필요 하면 서비스 패브릭은 균형을 다시 조정할 hello 기본 [복제본](service-fabric-availability-services.md) 10 모든 노드에 걸쳐 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="c4768-137">마찬가지로, 백 too5 노드를 배율 조정 경우 서비스 패브릭은 균형을 다시 조정 모든 hello 복제본 hello 5 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="c4768-138">그림 2는 10 개의 파티션의 hello 클러스터 크기 조정을 전후 hello 배포를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![상태 저장 서비스](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="c4768-140">결과적으로, 클라이언트의 요청 된 컴퓨터에 분산 hello 응용 프로그램의 전체적인 성능이 향상 됩니다 하 고 데이터 액세스 toochunks 경합이 감소 hello 확장 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="c4768-141">분할에 대한 계획</span><span class="sxs-lookup"><span data-stu-id="c4768-141">Plan for partitioning</span></span>
<span data-ttu-id="c4768-142">서비스를 구현 하기 전에 항상 분할 전략을 아웃 필요한 tooscale hello를 고려해 야 합니다. 다양 한 방식으로 있지만 어떤 hello 일일이 tooachieve에 집중 모두.</span><span class="sxs-lookup"><span data-stu-id="c4768-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="c4768-143">이 문서의 hello 컨텍스트에 대해 생각해 봅시다 일부 hello 더 중요 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="c4768-144">좋은 방법은 toothink toobe hello 첫 번째 단계로 분할 해야 하는 hello 상태의 hello 구조에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="c4768-145">간단한 예를 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="c4768-145">Let's take a simple example.</span></span> <span data-ttu-id="c4768-146">Toobuild countywide 설문 조사에 대 한 서비스 인 경우 hello 지방의 각 도시에 대 한 파티션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="c4768-147">그런 다음 해당 toothat 도시는 hello 파티션에 hello 도시에 있는 모든 사람에 대 한 hello 투표를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="c4768-148">그림 3에 존재 하는 사람 및 hello city의 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![간단한 파티션](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="c4768-150">도시, 000 명의 hello 다르거나 처럼 많은 양의 데이터 (예: Seattle)를 포함 하는 일부 파티션이 거의 상태 (예: Kirkland)와 다른 파티션에 있는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="c4768-151">따라서 불균형 한 양의 상태를 사용 하 여 파티션을의 hello 영향이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c4768-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="c4768-152">Hello 예에 대 한 다시 생각 되 면 hello 시애틀에 대 한 응답을 보유 하는 hello 파티션 하나 hello Kirkland 보다 더 많은 트래픽을 받게 됩니다을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="c4768-153">서비스 패브릭에서는 있어야 hello에 대 한 기본적으로 동일한 수의 각 노드에서 기본 및 보조 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="c4768-154">노드의 어떤 복제본은 트래픽을 더 많이 처리하고 어떤 복제본은 트래픽을 더 적게 처리하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="c4768-155">이 경우 가급적 할 tooavoid 핫 및 콜드 스폿은 클러스터에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="c4768-156">이 tooavoid 주문에서 분할 관점에서 다음 두 가지를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="c4768-157">모든 파티션에 균등 하 게 분포 되도록 toopartition hello 상태를 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c4768-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="c4768-158">각각 hello 서비스에 대 한 hello 복제본의 부하를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="c4768-159">(방법에 대한 자세한 정보는 이 문서의 [메트릭 및 부하](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요).</span><span class="sxs-lookup"><span data-stu-id="c4768-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="c4768-160">서비스 패브릭 레코드의 수 또는 메모리 양 등의 서비스에서 사용 하는 hello 기능 tooreport 부하를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="c4768-161">Hello 메트릭을 보고에 따르면 서비스 패브릭 일부 파티션이 다른 항목 보다 높은 부하를 서비스 하 고 이동 복제본 toomore 적합 한 노드를 통해 hello 클러스터 변경 되도록 검색 전반적인 노드가 없습니다는 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="c4768-162">때때로 지정된 파티션에 얼마나 많은 데이터가 있는지 알 수 없는 경우가 있으므로</span><span class="sxs-lookup"><span data-stu-id="c4768-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="c4768-163">일반적인 권장 사항은 두-toodo 이므로 먼저 분할 전략을 채택 하 여 하는 전체에 분산 hello 데이터 균등 하 게 hello 파티션 및 두 번째 보고 로드에서.</span><span class="sxs-lookup"><span data-stu-id="c4768-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="c4768-164">첫 번째 방법은 hello hello hello 둘째 데는 도움이 되지만 액세스 또는 부하에서 임시 차이 부드러운 시간이 지남에 따라 예제에서 투표에 설명 된 상황을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="c4768-165">파티션 계획의 또 다른 측면에는 toochoose hello 올바른 수와 파티션 toobegin입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="c4768-166">서비스 패브릭 관점에서 시나리오의 예상 파티션 수보다 더 많은 파티션으로 시작하지 못할 이유는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="c4768-167">실제로 가정 hello 최대 파티션 수는 올바른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="c4768-168">드물기는 하지만 처음에 선택한 것보다 더 많은 파티션이 필요하게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="c4768-169">Hello 팩트 후 hello 파티션 수를 변경할 수 없습니다, 해야 tooapply 일부 고급 파티션 방법, 동일한 서비스 유형을 hello의 새 서비스 인스턴스를 만드는 등.</span><span class="sxs-lookup"><span data-stu-id="c4768-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="c4768-170">또한 tooimplement hello 라우팅하는 일부 클라이언트 쪽 논리가 toohello 올바른 서비스 인스턴스를 클라이언트 코드를 유지 해야 하는 클라이언트 정보에 따라를 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="c4768-171">계획을 분할에 대 한 또 다른 고려 사항은 hello 사용할 수 있는 컴퓨터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="c4768-172">Hello 상태 toobe 액세스 하 고 저장 요구 사항에 맞춰, 바인딩된 toofollow 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="c4768-173">네트워크 대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="c4768-173">Network bandwidth limits</span></span>
* <span data-ttu-id="c4768-174">시스템 메모리 제한</span><span class="sxs-lookup"><span data-stu-id="c4768-174">System memory limits</span></span>
* <span data-ttu-id="c4768-175">디스크 저장소 제한</span><span class="sxs-lookup"><span data-stu-id="c4768-175">Disk storage limits</span></span>

<span data-ttu-id="c4768-176">따라서 실행 중인 클러스터의 리소스 제약 조건으로 실행 하는 경우는 것이 되나요? hello 대답은 간단히 hello 클러스터 tooaccommodate hello 새 요구 사항을 확장할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="c4768-177">[hello 용량 계획 가이드](service-fabric-capacity-planning.md) 방법에 대 한 지침을 제공 toodetermine 얼마나 많은 노드를 클러스터 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="c4768-178">분할 시작</span><span class="sxs-lookup"><span data-stu-id="c4768-178">Get started with partitioning</span></span>
<span data-ttu-id="c4768-179">이 섹션에서는 서비스를 분할 tooget 시작 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="c4768-180">서비스 패브릭은 세 가지 파티션 체계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="c4768-181">범위 지정된 분할(UniformInt64Partition이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="c4768-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="c4768-182">이름 지정된 분할.</span><span class="sxs-lookup"><span data-stu-id="c4768-182">Named partitioning.</span></span> <span data-ttu-id="c4768-183">일반적으로 이 모델을 사용한 응용 프로그램에는 제한된 집합 내에 버킷 가능한 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="c4768-184">이름 지정된 파티션 키로 사용되는 데이터 필드의 몇 가지 일반적인 예는 지역, 우편 번호, 고객 그룹 또는 기타 비즈니스 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="c4768-185">단일 분할</span><span class="sxs-lookup"><span data-stu-id="c4768-185">Singleton partitioning.</span></span> <span data-ttu-id="c4768-186">단일 파티션이 hello 서비스 추가 라우팅가 필요 하지 않는 경우에 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="c4768-187">예를 들어 상태 비저장 서비스는 기본적으로 이 파티션 체계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="c4768-188">이름 지정된 분할 체계 및 단일 분할 체계는 범위 지정된 파티션의 특별한 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="c4768-189">기본적으로 서비스 패브릭 사용에 대 한 Visual Studio 템플릿 hello 범위 분할을 hello 그대로 하나 가장 일반적이 고 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="c4768-190">이 문서의 나머지 부분에서는 hello hello 범위가 지정 된 파티션 구성표에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="c4768-191">범위 지정된 분할 체계</span><span class="sxs-lookup"><span data-stu-id="c4768-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="c4768-192">이 사용 되는 toospecify 정수 범위 (낮은 키와 높은 키로 식별) 및 (n) 파티션의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="c4768-193">각각의 hello 겹치지 않는 하위 범위를 담당 n 파티션을 만듭니다 전체 키 범위를 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="c4768-194">예를 들어 하위 키 0, 상위 키 99 및 숫자 4로 범위 지정된 분할 체계는 다음과 같이 4개의 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![범위 분할](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="c4768-196">일반적인 방법은 toocreate hello 데이터 집합 내에서 고유 키에 기반 하 여 해시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="c4768-197">키의 일부 일반적인 예로는 차량 식별 번호(VIN), 직원 ID 또는 고유 문자열을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="c4768-198">이 고유 키를 사용 하 여 있습니다 다음 생성 된 해시 코드, 모듈러스 hello 키 범위, toouse 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="c4768-199">Hello 상한 및 하 한의 hello 허용 되는 키 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="c4768-200">해시 알고리즘 선택</span><span class="sxs-lookup"><span data-stu-id="c4768-200">Select a hash algorithm</span></span>
<span data-ttu-id="c4768-201">해시의 중요한 부분은 해시 알고리즘을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="c4768-202">고려 하는 것이 hello 목표 인지 (집약성 중요 한 해시)-서로 가까이 toogroup 유사한 키 또는 활동 (배포 해시) 하는 모든 파티션에 광범위 하 게 배포 되어야 합니다는 더 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="c4768-203">적절 한 배포 해시 알고리즘의 hello 특성에는 쉽게 toocompute, 몇 가지 충돌이 되며 hello 키 균등 하 게 분산은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="c4768-204">효율적인 해시 알고리즘의 좋은 예는 hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="c4768-205">일반 해시 코드 알고리즘 선택에 대 한 좋은 자료는 hello [해시 함수에 대 한 Wikipedia 페이지](http://en.wikipedia.org/wiki/Hash_function)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="c4768-206">여러 파티션으로 상태 저장 서비스 구축</span><span class="sxs-lookup"><span data-stu-id="c4768-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="c4768-207">여러 파티션으로 첫 번째 신뢰할 수 있는 상태 저장 서비스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="c4768-208">이 예제에서는 작성 합니다 toostore 원하는 매우 간단한 응용 프로그램 hello에 문자 동일 hello로 시작 하는 성이 같은 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="c4768-209">모든 코드를 작성 하기 전에 hello 파티션과 파티션 키에 대 한 toothink을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="c4768-210">에 대 한 (하나씩 hello 알파벳의 각 문자에 대 한) 26 파티션이 제공 하기는 하지만 필요 하면 낮은 임계값과 높은 키 hello?</span><span class="sxs-lookup"><span data-stu-id="c4768-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="c4768-211">문자 당 하나의 파티션을 toohave 문자 그대로 원하는 대로 사용할 수 있습니다 0 hello 낮은 키와 25로 hello 높은 키로 각 문자가 자체 키.</span><span class="sxs-lookup"><span data-stu-id="c4768-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="c4768-212">이 실제로 hello 배포는 일정 하지 않게는 간단한 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="c4768-213">"S" 또는 "M"는 "X"로 시작 하는 hello 것 보다 일반적 hello 문자로 시작 하는 마지막 이름 또는 "Y"입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="c4768-214">**Visual Studio** > **파일** > **새로 만들기** > **프로젝트**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="c4768-215">Hello에 **새 프로젝트** 대화 상자에서 hello 서비스 패브릭 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="c4768-216">"AlphabetPartitions" hello 프로젝트를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="c4768-217">Hello에 **서비스를 만들** 대화 상자에서 선택 **Stateful** 서비스 및 hello 이미지 아래에 나와 있는 것 처럼 "Alphabet.Processing"을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="c4768-218">![Visual Studio의 새 서비스 대화 상자][1]</span><span class="sxs-lookup"><span data-stu-id="c4768-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="c4768-219">Hello 파티션 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-219">Set hello number of partitions.</span></span> <span data-ttu-id="c4768-220">열기 hello Applicationmanifest.xml 파일 hello AlphabetPartitions 프로젝트 및 업데이트 hello 매개 변수 아래와 같이 Processing_PartitionCount too26 ApplicationPackageRoot 폴더를 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="c4768-221">LowKey tooupdate hello와 ApplicationManifest.xml 아래와 같이 hello에 대 한 hello StatefulService 요소의 HighKey 속성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="c4768-222">Hello 서비스 toobe 액세스할 수 있는에 대 한 hello 아래와 같이 Alphabet.Processing 서비스에 대 한 (hello PackageRoot 폴더에 있음) ServiceManifest.xml의 hello 끝점 요소를 추가 하 여 포트에서 끝점을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="c4768-223">이제 hello 서비스는 구성 된 toolisten 26 파티션과 tooan 내부 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="c4768-224">다음으로, toooverride hello 해야 `CreateServiceReplicaListeners()` hello 처리 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4768-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4768-225">이 샘플의 경우 간단한 HttpCommunicationListener를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="c4768-226">신뢰할 수 있는 서비스 통신에 대 한 자세한 내용은 참조 하십시오. [hello 신뢰할 수 있는 서비스 통신 모델](service-fabric-reliable-services-communication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="c4768-227">복제를 수신 하는 hello URL에 대 한 권장된 패턴은 형식에 따라 hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="c4768-228">따라서 원하는 tooconfigure 통신 수신기 toolisten hello 올바른 끝점에이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="c4768-229">Hello에 호스트할 수는이 서비스의 여러 복제본이이 주소 toobe 고유 toohello 복제 하므로 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c4768-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="c4768-230">이 때문에 파티션 ID + 복제본 ID hello URL에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="c4768-231">HttpListener는 hello hello URL 접두사는 고유으로 동일한 포트에서 주소에서 수신 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="c4768-232">hello 추가 GUID는 보조 복제본이도 읽기 전용 요청을 수신 하는 고급 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="c4768-233">않은 hello 경우 원하는 toomake व न 기본 toosecondary tooforce 클라이언트 toore 해결 hello 주소에서 전환할 때 사용 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="c4768-234">'+' hello 주소를 여기 hello 복제 복 수신 대기 모든 사용 가능한 호스트 (예: IP, FQDM, localhost, 등) hello 코드 아래에 있도록 예를 보여 줍니다으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="c4768-235">또한 해당 hello 게시 URL을 확인 하는 것은 URL 접두사를 수신 대기 하는 hello과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="c4768-236">hello 수신 URL tooHttpListener 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="c4768-237">게시 된 URL이 hello URL을 게시 된 toohello 서비스 패브릭 명명 서비스, 서비스 검색에 사용 되는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="c4768-238">클라이언트는 해당 검색 서비스를 통해 이 주소에 대해 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="c4768-239">클라이언트 요구 toohave hello에 대 한 실제 IP 또는 FQDN hello 노드의 순서 tooconnect에서 발생 하는 hello 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="c4768-240">Tooreplace 필요는 '+'와 노드의 IP 또는 FQDN 같이 위의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="c4768-241">hello 마지막 단계는 아래와 같이 논리 toohello 서비스 처리 tooadd hello입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
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
   
    <span data-ttu-id="c4768-242">`ProcessInternalRequest`읽기 값 hello 쿼리 문자열 매개 변수가 사용 toocall hello 파티션 및 호출 hello `AddUserAsync` tooadd hello lastname toohello 신뢰할 수 있는 사전 `dictionary`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="c4768-243">상태 비저장 서비스 toohello 프로젝트 toosee 추가해보겠습니다 어떻게 특정 파티션의 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="c4768-244">이 서비스는 hello lastname 쿼리 문자열 매개 변수로 수락 하 고, hello 파티션 키를 결정 하며, 처리를 위해 toohello Alphabet.Processing 서비스로 전송 하는 간단한 웹 인터페이스로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="c4768-245">Hello에 **서비스를 만들** 대화 상자에서 선택 **Stateless** 서비스 하 고 아래와 같이 "Alphabet.Web"을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![상태 비저장 서비스 스크린 샷](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="c4768-247">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-247">.</span></span>
12. <span data-ttu-id="c4768-248">아래 표시 된 대로 포트를 hello Alphabet.WebApi 서비스 tooopen의 hello ServiceManifest.xml의에서 hello 끝점 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="c4768-249">Tooreturn hello 클래스 웹에서에서 ServiceInstanceListeners 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="c4768-250">다시, 간단한 HttpCommunicationListener tooimplement를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="c4768-251">이제 tooimplement hello 처리 논리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="c4768-252">HttpCommunicationListener 호출 hello `ProcessInputRequest` 요청 제공 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c4768-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="c4768-253">따라서 계속 해 서 하 고 아래 hello 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-253">So let's go ahead and add hello code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="c4768-254">단계 별로 안내하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-254">Let's walk through it step by step.</span></span> <span data-ttu-id="c4768-255">hello 코드 hello 첫 문자 hello 쿼리 문자열 매개 변수를 읽고 `lastname` char에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="c4768-256">그런 다음,이 문자에 대 한 hello 파티션 키의 hello 16 진수 값을 빼는 방식으로 결정 `A` hello hello 성 첫 번째 문자의 16 진수 값에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="c4768-257">이 예제에서 파티션당 하나의 파티션 키를 가진 26개의 파티션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="c4768-258">Hello 서비스 파티션을 구한 다음으로, `partition` hello를 사용 하 여이 키에 대 한 `ResolveAsync` 메서드 hello `servicePartitionResolver` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="c4768-259">`servicePartitionResolver` 는 다음으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="c4768-260">hello `ResolveAsync` 메서드는 hello 서비스 URI, hello 파티션 키와 매개 변수로 취소 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="c4768-261">처리 서비스는 hello에 대 한 서비스 URI를 hello `fabric:/AlphabetPartitions/Processing`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="c4768-262">다음으로 hello 파티션의 hello 끝점을 구했습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="c4768-263">마지막으로 hello 끝점 URL 및 hello 쿼리 문자열을 작성 하 고 처리 서비스는 hello를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="c4768-264">Hello 처리 작업이 완료 되 면에서는 쓰기 hello 출력 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="c4768-265">hello 마지막 단계는 tootest hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="c4768-266">Visual Studio에서는 로컬 및 클라우드 배포에 대해 응용 프로그램 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="c4768-267">26 파티션과 로컬로 tootest hello 서비스 해야 tooupdate hello `Local.xml` 아래와 같이 hello AlphabetPartitions 프로젝트의 hello ApplicationParameters 폴더에 파일:</span><span class="sxs-lookup"><span data-stu-id="c4768-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="c4768-268">배포를 마치면 hello 서비스와 모든 파티션에 hello 서비스 패브릭 탐색기에서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![서비스 패브릭 탐색기 스크린 샷](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="c4768-270">브라우저에서 분할을 입력 하 여 hello를 테스트할 수 있습니다 `http://localhost:8081/?lastname=somename`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="c4768-271">동일한 문자 hello 저장 되 고 hello로 시작 하 각 성 나타납니다 같은 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![브라우저 스크린 샷](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="c4768-273">hello 샘플의 hello 전체 소스 코드에서 사용할 수는 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4768-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4768-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4768-274">Next steps</span></span>
<span data-ttu-id="c4768-275">서비스 패브릭 개념에 대 한 정보를 보려면 hello 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c4768-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="c4768-276">서비스 패브릭 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="c4768-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="c4768-277">서비스 패브릭 서비스의 확장성</span><span class="sxs-lookup"><span data-stu-id="c4768-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="c4768-278">서비스 패브릭 응용 프로그램의 용량 계획</span><span class="sxs-lookup"><span data-stu-id="c4768-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png