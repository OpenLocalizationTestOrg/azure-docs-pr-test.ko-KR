---
title: "aaaAzure 컨테이너 인스턴스 및 컨테이너 오케스트레이션"
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
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="f06d7-103">Azure Container Instances 및 컨테이너 오케스트레이터</span><span class="sxs-lookup"><span data-stu-id="f06d7-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="f06d7-104">크기가 작고 응용 프로그램 방향이기 때문에 컨테이너는 신속한 배달 환경 및 마이크로 서비스 기반 아키텍처에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="f06d7-105">hello를 자동화 하 고 작업을 많은 수의 컨테이너 및 조작 방법을 관리 라고 *오케스트레이션*합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="f06d7-106">인기 있는 컨테이너 orchestrators Kubernetes, DC/OS 및 docker는 Docker Swarm 중 일부는 hello에서 사용할 수 있는 포함 [Azure 컨테이너 서비스](https://docs.microsoft.com/azure/container-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="f06d7-107">Azure 컨테이너 인스턴스 hello 기본 일정 오케스트레이션 플랫폼의 기능 중 일부를 제공 하지만 해당 플랫폼을 제공 하 고 실제로 이러한 보완 될 수 있습니다 hello 보다 중요 서비스를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="f06d7-108">이 문서에서는 hello 범위 컨테이너 인스턴스를 Azure의 처리 및 컨테이너 orchestrators 상호 작용할 수 정도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="f06d7-109">기존 오케스트레이션</span><span class="sxs-lookup"><span data-stu-id="f06d7-109">Traditional orchestration</span></span>

<span data-ttu-id="f06d7-110">오케스트레이션의 hello 표준 정의 작업을 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="f06d7-111">**예약**: 어떤 toorun hello 컨테이너에 적합 한 컴퓨터를 찾을 컨테이너 이미지 및 리소스 요청을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="f06d7-112">**선호도/반선호도**: 서로 가깝거나(성능 목적) 충분히 멀리 떨어져 있는(가용성 목적) 컨테이너 집합이 실행되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="f06d7-113">**상태 모니터링**: 컨테이너 오류를 관찰하여 자동으로 일정을 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="f06d7-114">**장애 조치**: 추적 각 컴퓨터에서 실행 되는 대상 및 컨테이너 toohealthy 노드 모두 실패 한 컴퓨터에서에서 일정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="f06d7-115">**크기 조정**: 추가 하거나 수동 또는 자동으로 컨테이너 인스턴스 toomatch 요구를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="f06d7-116">**네트워킹**: 여러 호스트 컴퓨터 간에 컨테이너 toocommunicate 조정에 대 한 오버레이 네트워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="f06d7-117">**서비스 검색**: 컨테이너 toolocate 서로 자동으로 활성화 호스트 컴퓨터 간에 이동 하면서을 IP 주소를 변경 하는 때에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="f06d7-118">**응용 프로그램 업그레이드 조정**: 작동 중단이 컨테이너 업그레이드 tooavoid 응용 프로그램을 관리 하 고 문제가 발생 한 경우 롤백 기능을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="f06d7-119">Azure Container Instances와 오케스트레이션: 계층화된 접근 방식</span><span class="sxs-lookup"><span data-stu-id="f06d7-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="f06d7-120">Azure 컨테이너 인스턴스 계층된 방식을 tooorchestration hello 예약 모든 있으며 특정 관리 기능이 필요한 toorun 단일 컨테이너 orchestrator 그 위에 플랫폼 toomanage 다중 컨테이너 작업 하면서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="f06d7-121">Azure 관리 않으므로 모든 인프라 컨테이너 인스턴스에 대 한 기본 hello, orchestrator 플랫폼에 어떤 toorun에 적절 한 호스트 컴퓨터를 단일 컨테이너를 검색할 tooconcern 자체 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="f06d7-122">hello 클라우드의 hello 탄력성 하나는 항상 사용할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="f06d7-123">대신, hello orchestrator 다중 컨테이너 아키텍처별 크기 조정 및 조정 된 업그레이드 hello 개발을 단순화 하는 hello 작업에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="f06d7-124">잠재적 시나리오</span><span class="sxs-lookup"><span data-stu-id="f06d7-124">Potential scenarios</span></span>

<span data-ttu-id="f06d7-125">Azure Container Instances를 포함한 오케스트레이터 통합이 여전히 초기 상태인 동안 몇 가지 다양한 환경이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="f06d7-126">Container Instances의 오케스트레이션 독점</span><span class="sxs-lookup"><span data-stu-id="f06d7-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="f06d7-127">신속 하 게 시작 하 여 hello 요금을 청구 하기 때문에 두 번째를 기반으로 단독으로 환경을 Azure 컨테이너 인스턴스 제공 hello 가장 빠른 방법은 tooget 시작 및 toodeal 매우 가변적 워크 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="f06d7-128">Virtual Machines에서 Container Instances 및 컨테이너 조합</span><span class="sxs-lookup"><span data-stu-id="f06d7-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="f06d7-129">장기 실행에 대 한 전용된 가상 컴퓨터의 클러스터에 있는 컨테이너를 조정 하는 안정적인 작업 컨테이너 인스턴스와 hello 동일한 컨테이너를 실행 하는 보다 저렴 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="f06d7-130">그러나 컨테이너 인스턴스 신속 하 게 확장 하 고 축소 하면 전체 용량 toodeal 사용량에서 예기치 않은 또는 단기 스파이크 뛰어난 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="f06d7-131">Hello 클러스터의 가상 컴퓨터 수를 확장 하는 대신 다음 해당 컴퓨터에 추가 컨테이너 배포 hello orchestrator 단순히 컨테이너 인스턴스를 사용 하 여 hello 추가 컨테이너를 예약할 수 및가 있으면 삭제 없음 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="f06d7-132">샘플 구현: Kubernetes의 Azure Container Instances 커넥터</span><span class="sxs-lookup"><span data-stu-id="f06d7-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="f06d7-133">컨테이너 오케스트레이션 플랫폼 Azure 컨테이너 인스턴스와 통합 하는 방법을 toodemonstrate, 건물 시작 했습니다. 한 [Kubernetes에 대 한 샘플 커넥터][aci-connector-k8s]합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="f06d7-134">Kubernetes 모방 hello에 대 한 커넥터 hello [kubelet] [ kubelet-doc] 무제한 용량으로 노드로 등록 하 고 hello 만들기 디스패치 하 여 [포드] [ pod-doc] Azure 컨테이너 인스턴스 컨테이너 그룹으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="f06d7-135">다른 orchestrators에 대 한 커넥터 플랫폼 hello orchestrator hello 속도 사용 하 여 API의 기본 형식 toocombine hello 전원과 간결성을 컨테이너 인스턴스를 Azure의 컨테이너 관리와 마찬가지로 통합 구축 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="f06d7-136">Kubernetes은 ACI 커넥터 hello *실험적* 이므로 프로덕션 환경에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f06d7-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f06d7-137">Next steps</span></span>

<span data-ttu-id="f06d7-138">Azure 컨테이너 인스턴스 hello를 사용 하 여 첫 번째 컨테이너 만들기 [빠른 시작 가이드](container-instances-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f06d7-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/