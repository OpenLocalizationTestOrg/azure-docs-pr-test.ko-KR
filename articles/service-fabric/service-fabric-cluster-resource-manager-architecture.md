---
title: "Resource Manager 아키텍처 | Microsoft Docs"
description: "서비스 패브릭 클러스터 리소스 관리자의 아키텍처 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 565c20637fa93ed92bb6c52e585a4b70bdeb6f8c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a><span data-ttu-id="e443e-103">클러스터 리소스 관리자 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="e443e-103">Cluster resource manager architecture overview</span></span>
<span data-ttu-id="e443e-104">Service Fabric Cluster Resource Manager는 클러스터에서 실행되는 중앙 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-104">The Service Fabric Cluster Resource Manager is a central service that runs in the cluster.</span></span> <span data-ttu-id="e443e-105">이 서비스는 특히 리소스 소비 및 배치 규칙 측면에서 클러스터에 있는 서비스의 원하는 상태를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-105">It manages the desired state of the services in the cluster, particularly with respect to resource consumption and any placement rules.</span></span> 

<span data-ttu-id="e443e-106">클러스터의 리소스를 관리하려면 Service Fabric Cluster Resource Manager에게 일부 정보가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-106">To manage the resources in your cluster, the Service Fabric Cluster Resource Manager must have several pieces of information:</span></span>

- <span data-ttu-id="e443e-107">현재 존재하는 서비스</span><span class="sxs-lookup"><span data-stu-id="e443e-107">Which services currently exist</span></span>
- <span data-ttu-id="e443e-108">각 서비스의 현재(또는 기본) 리소스 소비량</span><span class="sxs-lookup"><span data-stu-id="e443e-108">Each service's current (or default) resource consumption</span></span> 
- <span data-ttu-id="e443e-109">나머지 클러스터 용량</span><span class="sxs-lookup"><span data-stu-id="e443e-109">The remaining cluster capacity</span></span> 
- <span data-ttu-id="e443e-110">클러스터의 노드 용량</span><span class="sxs-lookup"><span data-stu-id="e443e-110">The capacity of the nodes in the cluster</span></span> 
- <span data-ttu-id="e443e-111">각 노드에서 사용되는 리소스의 양</span><span class="sxs-lookup"><span data-stu-id="e443e-111">The amount of resources consumed on each node</span></span>

<span data-ttu-id="e443e-112">주어진 서비스의 리소스 사용은 지남에 따라 변할 수 있으며, 서비스는 일반적으로 하나 이상의 리소스 유형에 대해 주의를 기울입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-112">The resource consumption of a given service can change over time, and services usually care about more than one type of resource.</span></span> <span data-ttu-id="e443e-113">다른 서비스에 있는 실제 물리적 리소스와 물리적 리소스를 모두 측정하고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-113">Across different services, there may be both real physical and physical resources being measured.</span></span> <span data-ttu-id="e443e-114">서비스는 메모리 및 디스크 소비와 같은 물리적 메트릭을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-114">Services may track physical metrics like memory and disk consumption.</span></span> <span data-ttu-id="e443e-115">일반적으로 서비스는 "WorkQueueDepth" 또는 "TotalRequests"와 같은 논리 메트릭을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-115">More commonly, services may care about logical metrics - things like "WorkQueueDepth" or "TotalRequests".</span></span> <span data-ttu-id="e443e-116">동일한 클러스터에서 논리 및 실제 메트릭을 둘 다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-116">Both logical and physical metrics can be used in the same cluster.</span></span> <span data-ttu-id="e443e-117">메트릭은 많은 서비스에서 공유될 수도 있고 특정 서비스와만 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-117">Metrics can be shared across many services or be specific to a particular service.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="e443e-118">기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e443e-118">Other considerations</span></span>
<span data-ttu-id="e443e-119">클러스터의 소유자 및 연산자는 서비스 및 응용 프로그램 작성자와 다른 사람일 수도 있고, 최소한 여러 가지 작업을 수행하는 동일한 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-119">The owners and operators of the cluster can be different from the service and application authors, or at a minimum are the same people wearing different hats.</span></span> <span data-ttu-id="e443e-120">응용 프로그램을 개발할 때는 필요한 사항을 알 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-120">When you develop your application you know a few things about what it requires.</span></span> <span data-ttu-id="e443e-121">사용될 리소스의 예상 크기와 다른 서비스가 배포되는 방식을 알 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-121">You have an estimate of the resources it will consume and how different services should be deployed.</span></span> <span data-ttu-id="e443e-122">예를 들어 웹 계층은 인터넷에 노출되는 노드에서 실행되어야 하지만 데이터베이스 서비스는 그렇지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-122">For example, the web tier needs to run on nodes exposed to the Internet, while the database services should not.</span></span> <span data-ttu-id="e443e-123">또 다른 예로, 웹 서비스는 CPU 및 네트워크로 제한될 수 있지만 데이터 계층 서비스는 메모리 및 디스크 소비량에 의해 더 많은 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-123">As another example, the web services are probably constrained by CPU and network, while the data tier services care more about memory and disk consumption.</span></span> <span data-ttu-id="e443e-124">그러나 프로덕션 중에 해당 서비스에 대한 라이브 사이트 인시던트를 처리거나 서비스에 대한 업그레이드를 관리하는 사용자는 다양한 작업을 수행해야 하며 다양한 도구가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-124">However, the person handling a live-site incident for that service in production, or who is managing an upgrade to the service has a different job to do, and requires different tools.</span></span> 

<span data-ttu-id="e443e-125">클러스터 및 서비스 둘 다 동적인 경우:</span><span class="sxs-lookup"><span data-stu-id="e443e-125">Both the cluster and services are dynamic:</span></span>

- <span data-ttu-id="e443e-126">클러스터의 노드 수는 확장되고 축소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-126">The number of nodes in the cluster can grow and shrink</span></span>
- <span data-ttu-id="e443e-127">다양한 크기 및 형식의 노드는 오갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-127">Nodes of different sizes and types can come and go</span></span>
- <span data-ttu-id="e443e-128">서비스를 생성, 제거할 수 있고 원하는 리소스 할당 및 배치 규칙을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-128">Services can be created, removed, and change their desired resource allocations and placement rules</span></span>
- <span data-ttu-id="e443e-129">업그레이드 또는 기타 관리 작업은 인프라 수준의 응용 프로그램에서 클러스터를 통해 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-129">Upgrades or other management operations can roll through the cluster at the application on infrastructure levels</span></span>
- <span data-ttu-id="e443e-130">언제든지 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-130">Failures can happen at any time.</span></span>

## <a name="cluster-resource-manager-components-and-data-flow"></a><span data-ttu-id="e443e-131">클러스터 리소스 관리자 구성 요소 및 데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="e443e-131">Cluster resource manager components and data flow</span></span>
<span data-ttu-id="e443e-132">Cluster Resource Manager는 해당 서비스 내의 각 서비스 개체별로 각 서비스의 요구 사항 및 리소스 사용을 추적해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-132">The Cluster Resource Manager has to track the requirements of each service and the consumption of resources by each service object within those services.</span></span> <span data-ttu-id="e443e-133">Cluster Resource Manager에는 각 노드에서 실행되는 에이전트 및 내결함성 서비스라는 두 가지 개념적 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-133">The Cluster Resource Manager has two conceptual parts: agents that run on each node and a fault-tolerant service.</span></span> <span data-ttu-id="e443e-134">각 노드 트랙의 에이전트는 서비스에서 보고서를 로드하고 집계하며 주기적으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-134">The agents on each node track load reports from services, aggregate them, and periodically report them.</span></span> <span data-ttu-id="e443e-135">Cluster Resource Manager 서비스는 로컬 에이전트에서 모든 정보를 집계하고 현재 구성에 따라 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-135">The Cluster Resource Manager service aggregates all the information from the local agents and reacts based on its current configuration.</span></span>

<span data-ttu-id="e443e-136">다음 다이어그램을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-136">Let’s look at the following diagram:</span></span>

<span data-ttu-id="e443e-137"><center>
![리소스 분산 장치 아키텍처][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="e443e-137"><center>
![Resource Balancer Architecture][Image1]
</center></span></span>

<span data-ttu-id="e443e-138">런타임 중에 많은 내용이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-138">During runtime, there are many changes that could happen.</span></span> <span data-ttu-id="e443e-139">예를 들어 일부 서비스가 사용하는 리소스의 양이 변경되고 일부 서비스가 실패하고 일부 노드가 클러스터를 연결하고 연결 해제한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-139">For example, let’s say the amount of resources some services consume changes, some services fail, and some nodes join and leave the cluster.</span></span> <span data-ttu-id="e443e-140">노드에 대한 모든 변경 사항은 집계되어 Cluster Resource Manager 서비스(1, 2)로 정기적으로 전송되고, 여기서 다시 집계되고 분석되고 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-140">All the changes on a node are aggregated and periodically sent to the Cluster Resource Manager service (1,2) where they are aggregated again, analyzed, and stored.</span></span> <span data-ttu-id="e443e-141">해당 서비스에서는 몇 초마다 변경 사항을 보고 필요한 작업이 있는지 확인합니다(3).</span><span class="sxs-lookup"><span data-stu-id="e443e-141">Every few seconds that service looks at the changes and determines if any actions are necessary (3).</span></span> <span data-ttu-id="e443e-142">예를 들어 비어 있는 노드가 클러스터에 추가되었다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-142">For example, it could notice that some empty nodes have been added to the cluster.</span></span> <span data-ttu-id="e443e-143">결과적으로 일부 서비스를 해당 노드로 이동하기로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-143">As a result, it decides to move some services to those nodes.</span></span> <span data-ttu-id="e443e-144">Cluster Resource Manager는 특정 노드가 오버로드되거나 특정 서비스가 실패하거나 삭제되어 다른 곳에서 리소스를 확보했는지도 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-144">The Cluster Resource Manager could also notice that a particular node is overloaded, or that certain services have failed or been deleted, freeing up resources elsewhere.</span></span>

<span data-ttu-id="e443e-145">다음 다이어그램을 살펴보고 그 다음에 어떤 결과가 발생하는지 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-145">Let’s look at the following diagram and see what happens next.</span></span> <span data-ttu-id="e443e-146">클러스터 Resource Manager에서 변경이 필요한지 판단한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-146">Let’s say that the Cluster Resource Manager determines that changes are necessary.</span></span> <span data-ttu-id="e443e-147">이는 다른 시스템 서비스(특히 장애 조치 관리자)와 함께 필요한 변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-147">It coordinates with other system services (in particular the Failover Manager) to make the necessary changes.</span></span> <span data-ttu-id="e443e-148">그런 다음 필요한 명령을 적절한 노드(4)로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-148">Then the necessary commands are sent to the appropriate nodes (4).</span></span> <span data-ttu-id="e443e-149">예를 들어 Resource Manager에서 Node5가 오버로드되었음을 알아차리고 서비스 B를 Node5에서 Node4로 이동하기로 결정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-149">For example, let's say the Resource Manager noticed that Node5 was overloaded, and so decided to move service B from Node5 to Node4.</span></span> <span data-ttu-id="e443e-150">재구성(5)이 마무리되면 클러스터는 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-150">At the end of the reconfiguration (5), the cluster looks like this:</span></span>

<span data-ttu-id="e443e-151"><center>
![리소스 분산 장치 아키텍처][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="e443e-151"><center>
![Resource Balancer Architecture][Image2]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="e443e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e443e-152">Next steps</span></span>
- <span data-ttu-id="e443e-153">Cluster Resource Manager에는 클러스터를 설명하기 위한 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-153">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="e443e-154">이에 대해 자세히 알아보려면 [Service Fabric 클러스터 설명](./service-fabric-cluster-resource-manager-cluster-description.md)에 대한 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e443e-154">To find out more about them, check out this article on [describing a Service Fabric cluster](./service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="e443e-155">Cluster Resource Manager의 기본 임무는 클러스터의 부하를 다시 분산하고 배치 규칙을 적용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e443e-155">The Cluster Resource Manager's primary duties are rebalancing the cluster and enforcing placement rules.</span></span> <span data-ttu-id="e443e-156">이러한 동작은 구성하는 방법에 대한 자세한 내용은 [Service Fabric 클러스터 부하 분산](./service-fabric-cluster-resource-manager-balancing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e443e-156">For more information on configuring these behaviors, see [balancing your Service Fabric cluster](./service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
