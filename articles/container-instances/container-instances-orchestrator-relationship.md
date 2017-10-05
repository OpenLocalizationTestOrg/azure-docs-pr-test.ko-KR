---
title: "Azure Container Instances 및 컨테이너 오케스트레이션"
description: "Azure Container Instances가 컨테이너 오케스트레이터와 상호 작용하는 방법을 이해합니다"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="de76d-103">Azure Container Instances 및 컨테이너 오케스트레이터</span><span class="sxs-lookup"><span data-stu-id="de76d-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="de76d-104">크기가 작고 응용 프로그램 방향이기 때문에 컨테이너는 신속한 배달 환경 및 마이크로 서비스 기반 아키텍처에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="de76d-105">많은 수의 컨테이너를 자동화하고 관리하는 방법 및 상호 작용하는 방법을 *오케스트레이션*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="de76d-106">Kubernetes, DC/OS 및 Docker Swarm과 같은 인기 있는 컨테이너 오케스트레이터를 [Azure Container Service](https://docs.microsoft.com/azure/container-service/)에서 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="de76d-107">Azure Container Instances에서는 오케스트레이션 플랫폼의 기본 예약 기능 중 일부를 제공하지만 실제로 해당 플랫폼이 제공하는 고급 서비스를 제공하지 않고 보완할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="de76d-108">이 문서에서는 Azure Container Instances에서 처리하는 범위 및 전체 컨테이너 오케스트레이터가 상호 작용할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="de76d-109">기존 오케스트레이션</span><span class="sxs-lookup"><span data-stu-id="de76d-109">Traditional orchestration</span></span>

<span data-ttu-id="de76d-110">오케스트레이션의 표준 정의에는 다음 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="de76d-111">**예약**: 컨테이너 이미지 및 리소스 요청을 지정하여 컨테이너를 실행할 적절한 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="de76d-112">**선호도/반선호도**: 서로 가깝거나(성능 목적) 충분히 멀리 떨어져 있는(가용성 목적) 컨테이너 집합이 실행되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="de76d-113">**상태 모니터링**: 컨테이너 오류를 관찰하여 자동으로 일정을 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="de76d-114">**장애 조치**: 각 컴퓨터에서 실행되는 작업을 추적하고 실패한 컴퓨터의 컨테이너를 정상 노드로 다시 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="de76d-115">**크기 조정**: 수동 또는 자동으로 요청에 맞게 Container Instance를 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="de76d-116">**네트워킹**: 여러 호스트 컴퓨터 간에 통신하도록 컨테이너를 조정하는 오버레이 네트워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="de76d-117">**서비스 검색**: 컨테이너가 호스트 컴퓨터 간에 이동하면서 IP 주소를 변경하는 경우에도 자동으로 서로 찾을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="de76d-118">**조정된 응용 프로그램 업그레이드**: 응용 프로그램 작동 중단 시간을 방지하고 문제가 발생한 경우 롤백할 수 있도록 컨테이너 업그레이드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="de76d-119">Azure Container Instances와 오케스트레이션: 계층화된 접근 방식</span><span class="sxs-lookup"><span data-stu-id="de76d-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="de76d-120">Azure Container Instances를 사용하여 계층화된 접근 방식을 오케스트레이션할 수 있고 단일 컨테이너를 실행하는 데 필요한 예약 및 관리 기능을 제공하면서 동시에 오케스트레이터 플랫폼이 다중 컨테이너 작업을 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="de76d-121">Container Instances에 대한 기본 인프라가 모두 Azure에서 관리되는 때문에 오케스트레이터 플랫폼은 단일 컨테이너를 실행하는 적절한 호스트 컴퓨터를 찾는 작업을 처리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="de76d-122">클라우드의 탄력성을 항상 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="de76d-123">대신, 오케스트레이터는 크기 조정 및 조정된 업그레이드를 비롯한 다중 컨테이너 아키텍처의 개발을 간소화하는 작업에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="de76d-124">잠재적 시나리오</span><span class="sxs-lookup"><span data-stu-id="de76d-124">Potential scenarios</span></span>

<span data-ttu-id="de76d-125">Azure Container Instances를 포함한 오케스트레이터 통합이 여전히 초기 상태인 동안 몇 가지 다양한 환경이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="de76d-126">Container Instances의 오케스트레이션 독점</span><span class="sxs-lookup"><span data-stu-id="de76d-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="de76d-127">신속하게 시작하고 즉시 요금을 청구하기 때문에 Azure Container Instances에 기반한 독점 환경은 매우 가변적인 작업을 시작하고 처리하는 가장 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="de76d-128">Virtual Machines에서 Container Instances 및 컨테이너 조합</span><span class="sxs-lookup"><span data-stu-id="de76d-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="de76d-129">안정된 장기 실행 작업의 경우 전용 가상 컴퓨터의 클러스터에 있는 컨테이너를 조정하는 작업은 일반적으로 Container Instances와 동일한 컨테이너를 실행하는 것보다 비용이 더 적게 듭니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="de76d-130">그러나 Container Instances는 예기치 않은 단기 사용량 급증을 다루는 전체 수용작업량을 신속하게 확장하고 축소하는 최고의 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="de76d-131">클러스터에서 가상 컴퓨터의 수를 확장하고 해당 컴퓨터에 추가 컨테이너를 배포하는 대신 오케스트레이터는 단순하게 Container Instances를 사용하여 추가 컨테이너를 예약하고 더 이상 필요하지 않은 경우 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="de76d-132">샘플 구현: Kubernetes의 Azure Container Instances 커넥터</span><span class="sxs-lookup"><span data-stu-id="de76d-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="de76d-133">컨테이너 오케스트레이션 플랫폼이 Azure Container Instances와 통합하는 방법을 보여주기 위해 [Kubernetes의 샘플 커넥터][aci-connector-k8s]를 빌드하기 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="de76d-134">Kubernetes의 커넥터는 수용작업량이 무제한인 노드로 등록하고 [포드][pod-doc] 생성을 Azure Container Instances의 컨테이너 그룹으로 디스패치하여 [kubelet][kubelet-doc]을 모방합니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="de76d-135">다른 오케스트레이터의 커넥터는 Azure Container Instances에서 컨테이너를 관리하는 신속성 및 간소성을 통해 오케스트레이터 API의 기능을 결합하기 위해 플랫폼 기본 형식과 마찬가지로 통합되어 빌드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="de76d-136">Kubernetes용 ACI 커넥터는 *실험적*이므로 프로덕션에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de76d-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="de76d-137">Next steps</span></span>

<span data-ttu-id="de76d-138">[빠른 시작 가이드](container-instances-quickstart.md)를 사용하여 Azure Container Instances에서 첫 번째 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de76d-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/