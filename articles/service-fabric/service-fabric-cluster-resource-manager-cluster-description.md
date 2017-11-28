---
title: "클러스터 리소스 관리자 클러스터 설명 | Microsoft Docs"
description: "클러스터 리소스 관리자에 대한 장애 도메인, 업그레이드 도메인, 노드 속성 및 노드 용량을 지정하여 Service Fabric 클러스터를 설명합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e517eda4d3ff7ad81998003688c3cca78f76e179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="b10f2-103">서비스 패브릭 클러스터 설명</span><span class="sxs-lookup"><span data-stu-id="b10f2-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="b10f2-104">서비스 패브릭 클러스터 리소스 관리자는 클러스터를 설명하는 몇 가지 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-104">The Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="b10f2-105">런타임 중에 클러스터 Resource Manager는 이 정보를 사용하여 클러스터에서 실행되는 서비스의 높은 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-105">During runtime, the Cluster Resource Manager uses this information to ensure high availability of the services running in the cluster.</span></span> <span data-ttu-id="b10f2-106">이러한 주요 규칙을 적용하는 동시에 클러스터의 리소스 사용도 최적화되도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-106">While enforcing these important rules, it also attempts to optimize the resource consumption within the cluster.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="b10f2-107">주요 개념</span><span class="sxs-lookup"><span data-stu-id="b10f2-107">Key concepts</span></span>
<span data-ttu-id="b10f2-108">클러스터 Resource Manager는 클러스터를 설명하는 다음과 같은 몇 가지 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-108">The Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="b10f2-109">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-109">Fault Domains</span></span>
* <span data-ttu-id="b10f2-110">업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-110">Upgrade Domains</span></span>
* <span data-ttu-id="b10f2-111">노드 속성</span><span class="sxs-lookup"><span data-stu-id="b10f2-111">Node Properties</span></span>
* <span data-ttu-id="b10f2-112">노드 용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="b10f2-113">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-113">Fault domains</span></span>
<span data-ttu-id="b10f2-114">장애 도메인은 통합된 오류는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="b10f2-115">단일 컴퓨터는 장애 도메인입니다(전원 공급 장치 오류, 드라이브 오류, 잘못된 NIC 펌웨어 등 다양한 이유로 자체 실패할 수 있기 때문).</span><span class="sxs-lookup"><span data-stu-id="b10f2-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures to drive failures to bad NIC firmware).</span></span> <span data-ttu-id="b10f2-116">동일한 이더넷 스위치에 연결된 컴퓨터는 하나의 전원을 공유하는 컴퓨터 또는 단일 위치에 있는 컴퓨터와 같이 동일한 장애 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-116">Machines connected to the same Ethernet switch are in the same Fault Domain, as are machines sharing a single source of power or in a single location.</span></span> <span data-ttu-id="b10f2-117">하드웨어 오류가 중복되는 것이 당연하므로 장애 도메인은 기본적으로 계층 구조를 가지며 Service Fabric에서 URI로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-117">Since it's natural for hardware faults to overlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="b10f2-118">Service Fabric이 이러한 정보를 사용하여 서비스를 안전하게 배치하기 때문에 장애 도메인을 올바르게 설정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-118">It is important that Fault Domains are set up correctly since Service Fabric uses this information to safely place services.</span></span> <span data-ttu-id="b10f2-119">Service Fabric은 일부 구성 요소의 오류로 인해 발생하는 장애 도메인의 손실 때문에 서비스가 중단될 수 있는 서비스를 배치하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-119">Service Fabric doesn't want to place services such that the loss of a Fault Domain (caused by the failure of some component) causes a service to go down.</span></span> <span data-ttu-id="b10f2-120">Service Fabric은 Azure 환경에서 사용자 대신 클러스터의 노드를 올바르게 구성하기 위해 작업 환경에 제공되는 장애 도메인 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-120">In the Azure environment Service Fabric uses the Fault Domain information provided by the environment to correctly configure the nodes in the cluster on your behalf.</span></span> <span data-ttu-id="b10f2-121">독립 실행형 Service Fabric의 경우 클러스터를 설정할 때 장애 도메인이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-121">For Service Fabric Standalone, Fault Domains are defined at the time that the cluster is set up</span></span> 

> [!WARNING]
> <span data-ttu-id="b10f2-122">Service Fabric에 제공되는 장애 도메인 정보는 정확해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-122">It is important that the Fault Domain information provided to Service Fabric is accurate.</span></span> <span data-ttu-id="b10f2-123">예를 들어 Service Fabric 클러스터의 노드가 5개의 물리적 호스트에서 실행되는 10개의 가상 컴퓨터에서 실행된다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-123">For example, let's say that your Service Fabric cluster's nodes are running inside 10 virtual machines, running on five physical hosts.</span></span> <span data-ttu-id="b10f2-124">이 경우 10개의 가상 컴퓨터가 있지만 별도의 5개(최상위 수준) 장애 도메인만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-124">In this case, even though there are 10 virtual machines, there's only 5 different (top level) fault domains.</span></span> <span data-ttu-id="b10f2-125">동일한 물리적 호스트를 공유하면 물리적 호스트에 장애가 발생하는 경우 VM에서 조정된 오류가 발생하므로 동일한 루트 장애 도메인을 공유하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-125">Sharing the same physical host causes VMs to share the same root fault domain, since the VMs experience coordinated failure if their physical host fails.</span></span>  
>
> <span data-ttu-id="b10f2-126">Service Fabric에서 노드의 장애 도메인이 변경되지 않기를 기대하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-126">Since Service Fabric expects the Fault Domain of a node not to change.</span></span> <span data-ttu-id="b10f2-127">[HA-VM](https://technet.microsoft.com/en-us/library/cc967323.aspx)과 같이 VM의 고가용성을 보장하는 다른 메커니즘은 한 호스트에서 다른 호스트로 VM의 투명한 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-127">Other mechanisms of ensuring high availability of the VMs, such as [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use transparent migration of VMs from one host to another.</span></span> <span data-ttu-id="b10f2-128">이러한 메커니즘은 VM 내부의 실행 중인 코드를 다시 구성하거나 알리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-128">These mechanisms do not reconfigure or notify the running code inside the VM.</span></span> <span data-ttu-id="b10f2-129">따라서 Service Fabric 클러스터를 실행하기 위한 환경으로 **지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="b10f2-129">As such, they are **not supported** as environments for running Service Fabric clusters.</span></span> <span data-ttu-id="b10f2-130">Service Fabric은 사용되는 유일한 고가용성 기술이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-130">Service Fabric should be the only high-availability technology employed.</span></span> <span data-ttu-id="b10f2-131">라이브 VM 마이그레이션, SAN 또는 기타와 같은 메커니즘은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-131">Mechanisms like live VM migration, SANs, or others are not necessary.</span></span> <span data-ttu-id="b10f2-132">이러한 메커니즘은 Service Fabric과 함께 사용되는 경우 복잡성을 추가하고, 중앙 집중화된 오류 원인을 추가하며, Service Fabric과 충돌하는 안정성 및 가용성 전략을 사용하기 때문에 응용 프로그램 가용성 및 안정성을 _떨어뜨립니다_.</span><span class="sxs-lookup"><span data-stu-id="b10f2-132">If used in conjunction with Service Fabric, these mechanisms _reduce_ application availability and reliability because they introduce additional complexity, add centralized sources of failure, and utilize reliability and availability strategies that conflict with those in Service Fabric.</span></span> 
>
>

<span data-ttu-id="b10f2-133">아래 그래픽에서는 장애 도메인에 적용되고 발생한 모든 다른 장애 도메인을 나열하는 모든 엔터티에 색을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-133">In the graphic below we color all the entities that contribute to Fault Domains and list all the different Fault Domains that result.</span></span> <span data-ttu-id="b10f2-134">이 예제에는 데이터센터("DC"), 랙("R") 및 블레이드("B")가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-134">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="b10f2-135">각 블레이드에 하나 이상의 가상 컴퓨터가 있는 경우 장애 도메인 계층 구조에 또 다른 계층이 있다고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-135">Conceivably, if each blade holds more than one virtual machine, there could be another layer in the Fault Domain hierarchy.</span></span>

<span data-ttu-id="b10f2-136"><center>
![장애 도메인을 통해 구성된 노드][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-136"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="b10f2-137">런타임에 Service Fabric 클러스터 리소스 관리자는 클러스터의 장애 도메인을 고려하여 레이아웃을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-137">During runtime, the Service Fabric Cluster Resource Manager considers the Fault Domains in the cluster and plans layouts.</span></span> <span data-ttu-id="b10f2-138">지정된 서비스에 대한 상태 저장 복제본 또는 상태 비저장 인스턴스가 별도의 장애 도메인에 있도록 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-138">The stateful replicas or stateless instances for a given service are distributed so they are in separate Fault Domains.</span></span> <span data-ttu-id="b10f2-139">장애 도메인을 통해 서비스를 분산하면 장애 도메인이 모든 계층 수준에서 실패할 때 서비스의 가용성이 손상되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-139">Distributing the service across fault domains ensures the availability of the service is not compromised when a Fault Domain fails at any level of the hierarchy.</span></span>

<span data-ttu-id="b10f2-140">Service Fabric의 Cluster Resource Manager는 장애 도메인 계층 구조에 있는 계층 수를 고려하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-140">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in the Fault Domain hierarchy.</span></span> <span data-ttu-id="b10f2-141">그러나 계층 구조의 일부가 손실되어도 실행되는 서비스에 영향을 주지 않도록 보장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-141">However, it tries to ensure that the loss of any one portion of the hierarchy doesn’t impact services running in it.</span></span> 

<span data-ttu-id="b10f2-142">장애 도메인 계층 구조의 각 수준에서 노드 수가 동일한 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-142">It is best if there are the same number of nodes at each level of depth in the Fault Domain hierarchy.</span></span> <span data-ttu-id="b10f2-143">장애 도메인의 "트리"가 클러스터에서 분산되지 않은 경우 클러스터 리소스 관리자에서 최상의 서비스 재할당을 계산하기가 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-143">If the “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for the Cluster Resource Manager to figure out the best allocation of services.</span></span> <span data-ttu-id="b10f2-144">분산되지 않은 오류 도메인 레이아웃은 일부 도메인의 손실이 다른 도메인보다 서비스 가용성에 더 많은 영향을 미친다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-144">Imbalanced Fault Domains layouts mean that the loss of some domains impact the availability of services more than other domains.</span></span> <span data-ttu-id="b10f2-145">결과적으로 클러스터 리소스 관리자는 두 가지 목표 사이에서 고민합니다. 즉 서비스를 배치하여 "사용량이 많은" 도메인의 컴퓨터를 사용하려고 하며, 도메인의 손실로 인해 문제가 발생하지 않도록 다른 도메인에 서비스를 배치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-145">As a result, the Cluster Resource Manager is torn between two goals: It wants to use the machines in that “heavy” domain by placing services on them, and it wants to place services in other domains so that the loss of a domain doesn’t cause problems.</span></span> 

<span data-ttu-id="b10f2-146">분산되지 않은 도메인은 어떤 모양일까요?</span><span class="sxs-lookup"><span data-stu-id="b10f2-146">What do imbalanced domains look like?</span></span> <span data-ttu-id="b10f2-147">아래 다이어그램에서는 두 가지 클러스터 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-147">In the diagram below, we show two different cluster layouts.</span></span> <span data-ttu-id="b10f2-148">첫 번째 예의 경우 노드는 장애 도메인 간에 균등하게 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-148">In the first example, the nodes are distributed evenly across the Fault Domains.</span></span> <span data-ttu-id="b10f2-149">두 번째 예의 경우 하나의 장애 도메인에는 다른 장애 도메인보다 더 많은 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-149">In the second example, one Fault Domain has many more nodes than the other Fault Domains.</span></span> 

<span data-ttu-id="b10f2-150"><center>
![두 개의 다른 클러스터 레이아웃][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-150"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="b10f2-151">Azure에서는 장애 도메인에 노드가 포함된 선택 항목이 사용자를 위해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-151">In Azure, the choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="b10f2-152">그러나 프로비전하는 노드의 수에 따라 여전히 장애 도메인에 다른 항목보다 더 많은 노드가 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-152">However, depending on the number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="b10f2-153">예를 들어 클러스터에 5개의 장애 도메인이 있지만 지정된 NodeType에 대해 7개의 노드를 프로비전한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-153">For example, say you have five Fault Domains in the cluster but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="b10f2-154">이 경우 처음 두 장애 도메인에 더 많은 노드가 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-154">In this case, the first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="b10f2-155">몇 가지 인스턴스를 사용하여 더 많은 NodeTypes만 계속 배포하는 경우 문제가 악화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-155">If you continue to deploy more NodeTypes with only a couple instances, the problem gets worse.</span></span> <span data-ttu-id="b10f2-156">이러한 이유로 각 노드 형식의 노드 수는 장애 도메인 수의 배수가 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-156">For this reason it's recommended that the number of nodes in each node type is a multiple of the number of Fault Domains.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="b10f2-157">업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-157">Upgrade domains</span></span>
<span data-ttu-id="b10f2-158">업그레이드 도메인은 Service Fabric 클러스터 리소스 관리자에서 클러스터의 레이아웃을 이해하는 데 도움이 되는 또 다른 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-158">Upgrade Domains are another feature that helps the Service Fabric Cluster Resource Manager understand the layout of the cluster.</span></span> <span data-ttu-id="b10f2-159">업그레이드 도메인은 동시에 업그레이드된 노드 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-159">Upgrade Domains define sets of nodes that are upgraded at the same time.</span></span> <span data-ttu-id="b10f2-160">업그레이드 도메인은 클러스터 리소스 관리자에서 업그레이드와 같은 관리 작업을 이해하고 조정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-160">Upgrade Domains help the Cluster Resource Manager understand and orchestrate management operations like upgrades.</span></span>

<span data-ttu-id="b10f2-161">업그레이드 도메인은 장애 도메인과 많이 닮았지만 몇 가지 주요 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-161">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="b10f2-162">먼저 장애 도메인은 조정된 하드웨어 오류 영역으로 정의되지만,</span><span class="sxs-lookup"><span data-stu-id="b10f2-162">First, areas of coordinated hardware failures define Fault Domains.</span></span> <span data-ttu-id="b10f2-163">업그레이드 도메인은 정책으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-163">Upgrade Domains, on the other hand, are defined by policy.</span></span> <span data-ttu-id="b10f2-164">환경에 의해 결정되지 않고 사용자가 원하는 수를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-164">You get to decide how many you want, rather than it being dictated by the environment.</span></span> <span data-ttu-id="b10f2-165">노드를 갖추는 만큼 많은 업그레이드 도메인을 갖출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-165">You could have as many Upgrade Domains as you do nodes.</span></span> <span data-ttu-id="b10f2-166">장애 도메인과 업그레이드 도메인의 또 다른 차이점은 업그레이드 도메인이 계층적 구조가 아니라는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-166">Another difference between Fault Domains and Upgrade Domains is that Upgrade Domains are not hierarchical.</span></span> <span data-ttu-id="b10f2-167">대신, 간단한 태그와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-167">Instead, they are more like a simple tag.</span></span> 

<span data-ttu-id="b10f2-168">다음 다이어그램에서는 3개의 업그레이드 도메인이 세 개의 장애 도메인에 스트라이프되어 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-168">The following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="b10f2-169">또한 상태 저장 서비스의 세 개의 서로 다른 복제본을 배치하는 한 가지 방법을 보여줍니다. 여기서 각각 다른 장애 도메인 및 업그레이드 도메인에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-169">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="b10f2-170">이 배치를 사용하면 서비스를 업그레이드하는 중에 장애 도메인이 손실되어도 코드와 데이터의 복사본이 하나씩 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-170">This placement allows the loss of a Fault Domain while in the middle of a service upgrade and still have one copy of the code and data.</span></span>  

<span data-ttu-id="b10f2-171"><center>
![장애 도메인 및 업그레이드 도메인으로 배치][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-171"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="b10f2-172">많은 수의 업그레이드 도메인이 있는 경우 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-172">There are pros and cons to having large numbers of Upgrade Domains.</span></span> <span data-ttu-id="b10f2-173">업그레이드 도메인이 많으면 업그레이드의 각 단계가 더 세분화되어 더 적은 수의 노드 또는 서비스에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-173">More Upgrade Domains means each step of the upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="b10f2-174">따라서 한 번에 이동해야 하는 서비스가 줄어들어 시스템 변동이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-174">As a result, fewer services have to move at a time, introducing less churn into the system.</span></span> <span data-ttu-id="b10f2-175">그러면 서비스가 업그레이드 중에 발생된 모든 문제로 인해 영향을 받는 서비스가 줄기 때문에 안정성을 향상시키는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-175">This tends to improve reliability, since less of the service is impacted by any issue introduced during the upgrade.</span></span> <span data-ttu-id="b10f2-176">또한 업그레이드 도메인이 많아질수록 업그레이드의 영향을 처리하기 위해 다른 노드에서 사용할 수 있는 버퍼는 더 적게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-176">More Upgrade Domains also means that you need less available buffer on other nodes to handle the impact of the upgrade.</span></span> <span data-ttu-id="b10f2-177">예를 들어 5개의 업그레이드 도메인이 있으면 각각의 노드는 트래픽의 약 20%를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-177">For example, if you have five Upgrade Domains, the nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="b10f2-178">업그레이드를 위해 업그레이드 도메인을 중단해야 하는 경우 일반적으로 해당 로드를 다른 곳으로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-178">If you need to take down that Upgrade Domain for an upgrade, that load usually needs to go somewhere.</span></span> <span data-ttu-id="b10f2-179">남은 업그레이드 도메인이 4개이므로 각각에는 총 트래픽의 약 5%를 차지할 수 있는 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-179">Since you have four remaining Upgrade Domains, each must have room for about 5% of the total traffic.</span></span> <span data-ttu-id="b10f2-180">업그레이드 도메인이 많아질수록 클러스터의 노드에 필요한 버퍼는 더 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-180">More Upgrade Domains means you need less buffer on the nodes in the cluster.</span></span> <span data-ttu-id="b10f2-181">예를 들어 10개의 업그레이드 도메인을 대신 갖추는 경우를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-181">For example, consider if you had 10 Upgrade Domains instead.</span></span> <span data-ttu-id="b10f2-182">이 경우 각 UD에서는 총 트래픽의 약10%만 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-182">In that case, each UD would only be handling about 10% of the total traffic.</span></span> <span data-ttu-id="b10f2-183">클러스터를 통해 업그레이드가 진행될 때 각 도메인에는 총 트래픽의 약 1.1% 공간만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-183">When an upgrade steps through the cluster, each domain would only need to have room for about 1.1% of the total traffic.</span></span> <span data-ttu-id="b10f2-184">일반적으로 업그레이드 도메인을 더 많이 사용하면 예약되는 용량이 더 적어야 하므로 더 높은 사용률로 노드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-184">More Upgrade Domains generally allow you to run your nodes at higher utilization, since you need less reserved capacity.</span></span> <span data-ttu-id="b10f2-185">장애 도메인에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-185">The same is true for Fault Domains.</span></span>  

<span data-ttu-id="b10f2-186">많은 업그레이드 도메인을 가진 경우의 단점은 업그레이드 시간이 오래 걸린다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-186">The downside of having many Upgrade Domains is that upgrades tend to take longer.</span></span> <span data-ttu-id="b10f2-187">Service Fabric에서는 업그레이드 도메인이 완료된 후 잠시 기다렸다가 다음 업그레이드를 시작하기 전에 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-187">Service Fabric waits a short period of time after an Upgrade Domain is completed and performs checks before starting to upgrade the next one.</span></span> <span data-ttu-id="b10f2-188">이러한 지연은 업그레이드가 진행되기 전에 업그레이드로 인한 문제를 감지할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-188">These delays enable detecting issues introduced by the upgrade before the upgrade proceeds.</span></span> <span data-ttu-id="b10f2-189">이러한 단점은 한 번에 너무 많은 서비스에 영향을 주는 잘못된 변경 사항을 방지하기 때문에 받아들일 만합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-189">The tradeoff is acceptable because it prevents bad changes from affecting too much of the service at a time.</span></span>

<span data-ttu-id="b10f2-190">업그레이드 도메인이 너무 적어도 많은 부작용이 있습니다. 개별 업그레이드 도메인이 각각 중단되고 업그레이드되는 동안 전체 용량 중 상당한 부분을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-190">Too few Upgrade Domains has many negative side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="b10f2-191">예를 들어, 세 개의 업그레이드 도메인만 있는 경우 전체 서비스 또는 클러스터 용량은 약 1/3로 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-191">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="b10f2-192">워크로드를 처리하는 클러스터의 나머지 부분에 용량이 충분해야 하기 때문에 한 번에 서비스의 상당 부분이 중단되는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-192">Having so much of your service down at once isn’t desirable since you have to have enough capacity in the rest of your cluster to handle the workload.</span></span> <span data-ttu-id="b10f2-193">해당 버퍼를 유지 관리하면 정상 작업 중에 이러한 노드가 다른 경우에 로드하는 것보다 더 적게 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-193">Maintaining that buffer means that during normal operation those nodes are less loaded than they would be otherwise.</span></span> <span data-ttu-id="b10f2-194">이로 인해 서비스 실행 비용이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-194">This increases the cost of running your service.</span></span>

<span data-ttu-id="b10f2-195">환경에서 장애 도메인 또는 업그레이드 도메인의 총 수에 대한 제한이 없고 중첩 방법에 대한 제약도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-195">There’s no real limit to the total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="b10f2-196">즉 일반적인 몇 가지 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-196">That said, there are several common patterns:</span></span>

- <span data-ttu-id="b10f2-197">1:1 매핑된 장애 도메인 및 업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-197">Fault Domains and Upgrade Domains mapped 1:1</span></span>
- <span data-ttu-id="b10f2-198">노드(실제 또는 가상 OS 인스턴스) 당 하나의 업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="b10f2-198">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
- <span data-ttu-id="b10f2-199">장애 도메인 및 업그레이드 도메인이 대각선으로 실행되는 컴퓨터를 사용하여 행렬을 형성하는 "스트라이프" 또는 "매트릭스" 모델</span><span class="sxs-lookup"><span data-stu-id="b10f2-199">A “striped” or “matrix” model where the Fault Domains and Upgrade Domains form a matrix with machines usually running down the diagonals</span></span>

<span data-ttu-id="b10f2-200"><center>
![장애 도메인 및 업그레이드 도메인 레이아웃][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-200"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="b10f2-201">어떤 레이아웃을 선택하느냐에 대한 정답은 없으며, 각각 몇 가지 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-201">There’s no best answer which layout to choose, each has some pros and cons.</span></span> <span data-ttu-id="b10f2-202">예를 들어 1FD:1UD 모델의 설치는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-202">For example, the 1FD:1UD model is simple to set up.</span></span> <span data-ttu-id="b10f2-203">노드당 하나의 업그레이드 도메인 모델은 사람들이 익숙한 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-203">The 1 Upgrade Domain per Node model is most like what people are used to.</span></span> <span data-ttu-id="b10f2-204">업그레이드하는 동안 각 노드는 독립적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-204">During upgrades each node is updated independently.</span></span> <span data-ttu-id="b10f2-205">이는 이전에 수동으로 작은 컴퓨터 집합을 업그레이드한 방법과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-205">This is similar to how small sets of machines were upgraded manually in the past.</span></span> 

<span data-ttu-id="b10f2-206">가장 일반적인 모델은 FD/UD 행렬이며, 여기서 FD와 UD는 테이블을 형성하고 노드는 대각선을 따라 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-206">The most common model is the FD/UD matrix, where the FDs and UDs form a table and nodes are placed starting along the diagonal.</span></span> <span data-ttu-id="b10f2-207">이는 Azure의 Service Fabric 클러스터에서 기본적으로 사용되는 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-207">This is the model used by default in Service Fabric clusters in Azure.</span></span> <span data-ttu-id="b10f2-208">노드가 많은 클러스터의 경우 위의 조밀한 행렬 패턴처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-208">For clusters with many nodes everything ends up looking like the dense matrix pattern above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="b10f2-209">장애 도메인 및 업그레이드 도메인 제약 조건 및 결과 동작</span><span class="sxs-lookup"><span data-stu-id="b10f2-209">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="b10f2-210">Cluster Resource Manager는 장애 도메인 및 업그레이드 도메인에 분산된 서비스를 제약 조건으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-210">The Cluster Resource Manager treats the desire to keep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="b10f2-211">[이 문서](service-fabric-cluster-resource-manager-management-integration.md)에서 제약 조건에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-211">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="b10f2-212">장애 도메인 및 업그레이드 도메인 제약 조건은 다음과 같습니다. "지정된 서비스 파티션에서 두 도메인 간의 서비스 개체(상태 비저장 서비스 인스턴스 또는 상태 저장 서비스 복제본) 수는 *1개 이상* 차이가 나지 않아야 합니다."</span><span class="sxs-lookup"><span data-stu-id="b10f2-212">The Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in the number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span> <span data-ttu-id="b10f2-213">이렇게 하면 이 제약 조건을 위반하는 특정 이동 또는 배열을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-213">This prevents certain moves or arrangements that violate this constraint.</span></span>

<span data-ttu-id="b10f2-214">한 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-214">Let's look at one example.</span></span> <span data-ttu-id="b10f2-215">6개의 노드를 포함하며 5개의 장애 도메인과 5개의 업그레이드 도메인으로 구성된 클러스터가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-215">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="b10f2-216">FD0</span><span class="sxs-lookup"><span data-stu-id="b10f2-216">FD0</span></span> | <span data-ttu-id="b10f2-217">FD1</span><span class="sxs-lookup"><span data-stu-id="b10f2-217">FD1</span></span> | <span data-ttu-id="b10f2-218">FD2</span><span class="sxs-lookup"><span data-stu-id="b10f2-218">FD2</span></span> | <span data-ttu-id="b10f2-219">FD3</span><span class="sxs-lookup"><span data-stu-id="b10f2-219">FD3</span></span> | <span data-ttu-id="b10f2-220">FD4</span><span class="sxs-lookup"><span data-stu-id="b10f2-220">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="b10f2-221">**UD0**</span><span class="sxs-lookup"><span data-stu-id="b10f2-221">**UD0**</span></span> |<span data-ttu-id="b10f2-222">N1</span><span class="sxs-lookup"><span data-stu-id="b10f2-222">N1</span></span> | | | | |
| <span data-ttu-id="b10f2-223">**UD1**</span><span class="sxs-lookup"><span data-stu-id="b10f2-223">**UD1**</span></span> |<span data-ttu-id="b10f2-224">N6</span><span class="sxs-lookup"><span data-stu-id="b10f2-224">N6</span></span> |<span data-ttu-id="b10f2-225">N2</span><span class="sxs-lookup"><span data-stu-id="b10f2-225">N2</span></span> | | | |
| <span data-ttu-id="b10f2-226">**UD2**</span><span class="sxs-lookup"><span data-stu-id="b10f2-226">**UD2**</span></span> | | |<span data-ttu-id="b10f2-227">N3</span><span class="sxs-lookup"><span data-stu-id="b10f2-227">N3</span></span> | | |
| <span data-ttu-id="b10f2-228">**UD3**</span><span class="sxs-lookup"><span data-stu-id="b10f2-228">**UD3**</span></span> | | | |<span data-ttu-id="b10f2-229">N4</span><span class="sxs-lookup"><span data-stu-id="b10f2-229">N4</span></span> | |
| <span data-ttu-id="b10f2-230">**UD4**</span><span class="sxs-lookup"><span data-stu-id="b10f2-230">**UD4**</span></span> | | | | |<span data-ttu-id="b10f2-231">N5</span><span class="sxs-lookup"><span data-stu-id="b10f2-231">N5</span></span> |

<span data-ttu-id="b10f2-232">이제 TargetReplicaSetSize(또는 상태 비저장 서비스를 위한 InstanceCount)가 5인 서비스를 만든다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-232">Now let's say that we create a service with a TargetReplicaSetSize (or, for a stateless service an InstanceCount) of five.</span></span> <span data-ttu-id="b10f2-233">복제본은 N1-N5에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-233">The replicas land on N1-N5.</span></span> <span data-ttu-id="b10f2-234">실제로 많은 서비스를 만들더라도 N6은 절대 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-234">In fact, N6 is never used no matter how many services like this you create.</span></span> <span data-ttu-id="b10f2-235">그렇지만 그 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="b10f2-235">But why?</span></span> <span data-ttu-id="b10f2-236">N6을 선택하는 경우 현재 레이아웃 및 발생하는 상황 간의 차이를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-236">Let's look at the difference between the current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="b10f2-237">다음은 장애 도메인 및 업그레이드 도메인에 따른 레이아웃 및 총 복제본 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-237">Here's the layout we got and the total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="b10f2-238">FD0</span><span class="sxs-lookup"><span data-stu-id="b10f2-238">FD0</span></span> | <span data-ttu-id="b10f2-239">FD1</span><span class="sxs-lookup"><span data-stu-id="b10f2-239">FD1</span></span> | <span data-ttu-id="b10f2-240">FD2</span><span class="sxs-lookup"><span data-stu-id="b10f2-240">FD2</span></span> | <span data-ttu-id="b10f2-241">FD3</span><span class="sxs-lookup"><span data-stu-id="b10f2-241">FD3</span></span> | <span data-ttu-id="b10f2-242">FD4</span><span class="sxs-lookup"><span data-stu-id="b10f2-242">FD4</span></span> | <span data-ttu-id="b10f2-243">UDTotal</span><span class="sxs-lookup"><span data-stu-id="b10f2-243">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="b10f2-244">**UD0**</span><span class="sxs-lookup"><span data-stu-id="b10f2-244">**UD0**</span></span> |<span data-ttu-id="b10f2-245">R1</span><span class="sxs-lookup"><span data-stu-id="b10f2-245">R1</span></span> | | | | |<span data-ttu-id="b10f2-246">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-246">1</span></span> |
| <span data-ttu-id="b10f2-247">**UD1**</span><span class="sxs-lookup"><span data-stu-id="b10f2-247">**UD1**</span></span> | |<span data-ttu-id="b10f2-248">R2</span><span class="sxs-lookup"><span data-stu-id="b10f2-248">R2</span></span> | | | |<span data-ttu-id="b10f2-249">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-249">1</span></span> |
| <span data-ttu-id="b10f2-250">**UD2**</span><span class="sxs-lookup"><span data-stu-id="b10f2-250">**UD2**</span></span> | | |<span data-ttu-id="b10f2-251">R3</span><span class="sxs-lookup"><span data-stu-id="b10f2-251">R3</span></span> | | |<span data-ttu-id="b10f2-252">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-252">1</span></span> |
| <span data-ttu-id="b10f2-253">**UD3**</span><span class="sxs-lookup"><span data-stu-id="b10f2-253">**UD3**</span></span> | | | |<span data-ttu-id="b10f2-254">R4</span><span class="sxs-lookup"><span data-stu-id="b10f2-254">R4</span></span> | |<span data-ttu-id="b10f2-255">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-255">1</span></span> |
| <span data-ttu-id="b10f2-256">**UD4**</span><span class="sxs-lookup"><span data-stu-id="b10f2-256">**UD4**</span></span> | | | | |<span data-ttu-id="b10f2-257">R5</span><span class="sxs-lookup"><span data-stu-id="b10f2-257">R5</span></span> |<span data-ttu-id="b10f2-258">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-258">1</span></span> |
| <span data-ttu-id="b10f2-259">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="b10f2-259">**FDTotal**</span></span> |<span data-ttu-id="b10f2-260">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-260">1</span></span> |<span data-ttu-id="b10f2-261">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-261">1</span></span> |<span data-ttu-id="b10f2-262">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-262">1</span></span> |<span data-ttu-id="b10f2-263">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-263">1</span></span> |<span data-ttu-id="b10f2-264">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-264">1</span></span> |- |

<span data-ttu-id="b10f2-265">이 레이아웃은 장애 도메인 및 업그레이드 도메인당 노드의 측면에서 균형을 이룹니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-265">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="b10f2-266">장애 도메인 및 업그레이드 도메인에 따른 복제본의 수 측면에서도 균형을 이룹니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-266">It is also balanced in terms of the number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="b10f2-267">각 도메인에는 동일한 수의 노드 및 동일한 수의 복제본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-267">Each domain has the same number of nodes and the same number of replicas.</span></span>

<span data-ttu-id="b10f2-268">이제 N2 대신 N6를 사용하는 경우 발생하는 결과를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-268">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="b10f2-269">복제본은 어떻게 배포되나요?</span><span class="sxs-lookup"><span data-stu-id="b10f2-269">How would the replicas be distributed then?</span></span>

|  | <span data-ttu-id="b10f2-270">FD0</span><span class="sxs-lookup"><span data-stu-id="b10f2-270">FD0</span></span> | <span data-ttu-id="b10f2-271">FD1</span><span class="sxs-lookup"><span data-stu-id="b10f2-271">FD1</span></span> | <span data-ttu-id="b10f2-272">FD2</span><span class="sxs-lookup"><span data-stu-id="b10f2-272">FD2</span></span> | <span data-ttu-id="b10f2-273">FD3</span><span class="sxs-lookup"><span data-stu-id="b10f2-273">FD3</span></span> | <span data-ttu-id="b10f2-274">FD4</span><span class="sxs-lookup"><span data-stu-id="b10f2-274">FD4</span></span> | <span data-ttu-id="b10f2-275">UDTotal</span><span class="sxs-lookup"><span data-stu-id="b10f2-275">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="b10f2-276">**UD0**</span><span class="sxs-lookup"><span data-stu-id="b10f2-276">**UD0**</span></span> |<span data-ttu-id="b10f2-277">R1</span><span class="sxs-lookup"><span data-stu-id="b10f2-277">R1</span></span> | | | | |<span data-ttu-id="b10f2-278">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-278">1</span></span> |
| <span data-ttu-id="b10f2-279">**UD1**</span><span class="sxs-lookup"><span data-stu-id="b10f2-279">**UD1**</span></span> |<span data-ttu-id="b10f2-280">R5</span><span class="sxs-lookup"><span data-stu-id="b10f2-280">R5</span></span> | | | | |<span data-ttu-id="b10f2-281">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-281">1</span></span> |
| <span data-ttu-id="b10f2-282">**UD2**</span><span class="sxs-lookup"><span data-stu-id="b10f2-282">**UD2**</span></span> | | |<span data-ttu-id="b10f2-283">R2</span><span class="sxs-lookup"><span data-stu-id="b10f2-283">R2</span></span> | | |<span data-ttu-id="b10f2-284">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-284">1</span></span> |
| <span data-ttu-id="b10f2-285">**UD3**</span><span class="sxs-lookup"><span data-stu-id="b10f2-285">**UD3**</span></span> | | | |<span data-ttu-id="b10f2-286">R3</span><span class="sxs-lookup"><span data-stu-id="b10f2-286">R3</span></span> | |<span data-ttu-id="b10f2-287">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-287">1</span></span> |
| <span data-ttu-id="b10f2-288">**UD4**</span><span class="sxs-lookup"><span data-stu-id="b10f2-288">**UD4**</span></span> | | | | |<span data-ttu-id="b10f2-289">R4</span><span class="sxs-lookup"><span data-stu-id="b10f2-289">R4</span></span> |<span data-ttu-id="b10f2-290">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-290">1</span></span> |
| <span data-ttu-id="b10f2-291">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="b10f2-291">**FDTotal**</span></span> |<span data-ttu-id="b10f2-292">2</span><span class="sxs-lookup"><span data-stu-id="b10f2-292">2</span></span> |<span data-ttu-id="b10f2-293">0</span><span class="sxs-lookup"><span data-stu-id="b10f2-293">0</span></span> |<span data-ttu-id="b10f2-294">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-294">1</span></span> |<span data-ttu-id="b10f2-295">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-295">1</span></span> |<span data-ttu-id="b10f2-296">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-296">1</span></span> |- |

<span data-ttu-id="b10f2-297">이 레이아웃은 장애 도메인 제약 조건에 대한 정의를 위반합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-297">This layout violates our definition for the Fault Domain constraint.</span></span> <span data-ttu-id="b10f2-298">FD0에는 두 개의 복제본이 있는 반면 FD1에는 없으며 FD0 및 FD1이라는 총 두 번의 차이가 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-298">FD0 has two replicas, while FD1 has zero, making the difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="b10f2-299">Cluster Resource Manager는 이 정렬을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-299">The Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="b10f2-300">마찬가지로 N2 및 N6(N1 및 N2 대신)을 선택한 경우 다음에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-300">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="b10f2-301">FD0</span><span class="sxs-lookup"><span data-stu-id="b10f2-301">FD0</span></span> | <span data-ttu-id="b10f2-302">FD1</span><span class="sxs-lookup"><span data-stu-id="b10f2-302">FD1</span></span> | <span data-ttu-id="b10f2-303">FD2</span><span class="sxs-lookup"><span data-stu-id="b10f2-303">FD2</span></span> | <span data-ttu-id="b10f2-304">FD3</span><span class="sxs-lookup"><span data-stu-id="b10f2-304">FD3</span></span> | <span data-ttu-id="b10f2-305">FD4</span><span class="sxs-lookup"><span data-stu-id="b10f2-305">FD4</span></span> | <span data-ttu-id="b10f2-306">UDTotal</span><span class="sxs-lookup"><span data-stu-id="b10f2-306">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="b10f2-307">**UD0**</span><span class="sxs-lookup"><span data-stu-id="b10f2-307">**UD0**</span></span> | | | | | |<span data-ttu-id="b10f2-308">0</span><span class="sxs-lookup"><span data-stu-id="b10f2-308">0</span></span> |
| <span data-ttu-id="b10f2-309">**UD1**</span><span class="sxs-lookup"><span data-stu-id="b10f2-309">**UD1**</span></span> |<span data-ttu-id="b10f2-310">R5</span><span class="sxs-lookup"><span data-stu-id="b10f2-310">R5</span></span> |<span data-ttu-id="b10f2-311">R1</span><span class="sxs-lookup"><span data-stu-id="b10f2-311">R1</span></span> | | | |<span data-ttu-id="b10f2-312">2</span><span class="sxs-lookup"><span data-stu-id="b10f2-312">2</span></span> |
| <span data-ttu-id="b10f2-313">**UD2**</span><span class="sxs-lookup"><span data-stu-id="b10f2-313">**UD2**</span></span> | | |<span data-ttu-id="b10f2-314">R2</span><span class="sxs-lookup"><span data-stu-id="b10f2-314">R2</span></span> | | |<span data-ttu-id="b10f2-315">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-315">1</span></span> |
| <span data-ttu-id="b10f2-316">**UD3**</span><span class="sxs-lookup"><span data-stu-id="b10f2-316">**UD3**</span></span> | | | |<span data-ttu-id="b10f2-317">R3</span><span class="sxs-lookup"><span data-stu-id="b10f2-317">R3</span></span> | |<span data-ttu-id="b10f2-318">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-318">1</span></span> |
| <span data-ttu-id="b10f2-319">**UD4**</span><span class="sxs-lookup"><span data-stu-id="b10f2-319">**UD4**</span></span> | | | | |<span data-ttu-id="b10f2-320">R4</span><span class="sxs-lookup"><span data-stu-id="b10f2-320">R4</span></span> |<span data-ttu-id="b10f2-321">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-321">1</span></span> |
| <span data-ttu-id="b10f2-322">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="b10f2-322">**FDTotal**</span></span> |<span data-ttu-id="b10f2-323">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-323">1</span></span> |<span data-ttu-id="b10f2-324">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-324">1</span></span> |<span data-ttu-id="b10f2-325">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-325">1</span></span> |<span data-ttu-id="b10f2-326">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-326">1</span></span> |<span data-ttu-id="b10f2-327">1</span><span class="sxs-lookup"><span data-stu-id="b10f2-327">1</span></span> |- |

<span data-ttu-id="b10f2-328">이 레이아웃은 장애 도메인 측면에서 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-328">This layout is balanced in terms of Fault Domains.</span></span> <span data-ttu-id="b10f2-329">그러나 이제는 업그레이드 도메인 제약 조건을 위반하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-329">However, now it's violating the Upgrade Domain constraint.</span></span> <span data-ttu-id="b10f2-330">이는 UD0에는 복제본이 없고 UD1에는 두 개의 복제본이 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-330">This is because UD0 has zero replicas while UD1 has two.</span></span> <span data-ttu-id="b10f2-331">따라서 이 레이아웃도 잘못되었으며 클러스터 리소스 관리자에서 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-331">Therefore, this layout is also invalid and won't be picked by the Cluster Resource Manager.</span></span> 

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="b10f2-332">장애 도메인 및 업그레이드 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="b10f2-332">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="b10f2-333">장애 도메인 및 업그레이드 도메인 정의는 Azure 호스티드 Service Fabric 배포에서 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-333">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="b10f2-334">Service Fabric은 Azure의 환경 정보를 선택하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-334">Service Fabric picks up and uses the environment information from Azure.</span></span>

<span data-ttu-id="b10f2-335">사용자 고유의 클러스터를 만들거나 개발 중인 특정 토폴로지를 실행하려면 장애 도메인 및 업그레이드 도메인 정보를 직접 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-335">If you’re creating your own cluster (or want to run a particular topology in development), you can provide the Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="b10f2-336">이 예제에서는 각각 세 개의 랙을 가진 세 가지 "데이터 센터"에 걸쳐 있는 9개의 노드 로컬 개발 클러스터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-336">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="b10f2-337">이 클러스터에는 세 개의 해당 데이터 센터에 스트라이프된 3개의 업그레이드 도메인도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-337">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="b10f2-338">구성 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-338">An example of the configuration is below:</span></span> 

<span data-ttu-id="b10f2-339">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b10f2-339">ClusterManifest.xml</span></span>

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

<span data-ttu-id="b10f2-340">독립 실행형 배포의 경우 ClusterConfig.json을 통해</span><span class="sxs-lookup"><span data-stu-id="b10f2-340">via ClusterConfig.json for Standalone deployments</span></span>

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> <span data-ttu-id="b10f2-341">Azure 리소스 관리자를 통해 클러스터를 정의할 때 Azure에서 장애 도메인과 업그레이드 도메인이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-341">When defining clusters via Azure Resource Manager, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="b10f2-342">따라서 Azure 리소스 관리자 템플릿의 노드 형식 및 가상 컴퓨터 확장 집합의 정의에는 장애 도메인 또는 업그레이드 도메인 정보가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-342">Therefore, the definition of your Node Types and Virtual Machine Scale Sets in your Azure Resource Manager template does not include Fault Domain or Upgrade Domain information.</span></span>
>

## <a name="node-properties-and-placement-constraints"></a><span data-ttu-id="b10f2-343">노드 속성 및 배치 제약 조건</span><span class="sxs-lookup"><span data-stu-id="b10f2-343">Node properties and placement constraints</span></span>
<span data-ttu-id="b10f2-344">때로는(실제로 대부분의 경우) 특정 워크로드가 클러스터의 특정 노드 형식에서만 실행되도록 하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-344">Sometimes (in fact, most of the time) you’re going to want to ensure that certain workloads run only on certain types of nodes in the cluster.</span></span> <span data-ttu-id="b10f2-345">예를 들어, 일부 워크로드는GPU 또는 SSD가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-345">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="b10f2-346">특정 워크로드에 대한 하드웨어를 대상으로 하는 예제는 거의 모든 n계층 아키텍처입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-346">A great example of targeting hardware to particular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="b10f2-347">특정 컴퓨터는 프런트 엔드 또는 응용 프로그램에서 제공하는 API 쪽의 역할을 하며 인터넷에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-347">Certain machines serve as the front end or API serving side of the application and are exposed to the clients or the internet.</span></span> <span data-ttu-id="b10f2-348">종종 서로 다른 하드웨어 리소스를 사용하는 다양한 컴퓨터에서 계산 또는 저장소 계층의 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-348">Different machines, often with different hardware resources, handle the work of the compute or storage layers.</span></span> <span data-ttu-id="b10f2-349">이러한 컴퓨터는 대개 클라이언트 또는 인터넷에 직접 노출되지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="b10f2-349">These are usually _not_ directly exposed to clients or the internet.</span></span> <span data-ttu-id="b10f2-350">Service Fabric은 특정 하드웨어 구성에서 특정 워크로드를 실행해야 하는 경우가 있다고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-350">Service Fabric expects that there are cases where particular workloads need to run on particular hardware configurations.</span></span> <span data-ttu-id="b10f2-351">예:</span><span class="sxs-lookup"><span data-stu-id="b10f2-351">For example:</span></span>

* <span data-ttu-id="b10f2-352">기존 n 계층 응용 프로그램은 서비스 패브릭 환경으로 "리프트 및 이동"되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-352">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="b10f2-353">성능, 규모 또는 보안상의 이유 등으로 특정 하드웨어에서 워크로드를 실행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-353">a workload wants to run on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="b10f2-354">워크로드는 정책 또는 리소스 소비를 이유로 다른 워크로드로부터 격리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-354">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="b10f2-355">이러한 유형의 구성을 지원하기 위해 Service Fabric에는 노드에 적용될 수 있는 첫 번째 클래스 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-355">To support these sorts of configurations, Service Fabric has a first class notion of tags that can be applied to nodes.</span></span> <span data-ttu-id="b10f2-356">이러한 태그를 **노드 속성**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-356">These tags are called **node properties**.</span></span> <span data-ttu-id="b10f2-357">**배치 제약 조건**은 하나 이상의 노드 속성에 대해 선택하는 개별 서비스에 연결되는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-357">**Placement constraints** are the statements attached to individual services that select for one or more node properties.</span></span> <span data-ttu-id="b10f2-358">배치 제약 조건은 서비스를 실행해야 하는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-358">Placement constraints define where services should run.</span></span> <span data-ttu-id="b10f2-359">제약 조건 집합은 확장 가능하며 모든 키/값 쌍을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-359">The set of constraints is extensible - any key/value pair can work.</span></span> 

<span data-ttu-id="b10f2-360"><center>
![다양한 클러스터 레이아웃 워크로드][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-360"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

### <a name="built-in-node-properties"></a><span data-ttu-id="b10f2-361">기본 제공 노드 속성</span><span class="sxs-lookup"><span data-stu-id="b10f2-361">Built in node properties</span></span>
<span data-ttu-id="b10f2-362">Service Fabric은 사용자가 정의할 필요 없이 자동으로 사용할 수 있는 몇 가지 기본 노드 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-362">Service Fabric defines some default node properties that can be used automatically without the user having to define them.</span></span> <span data-ttu-id="b10f2-363">각 노드에 정의되는 기본 속성은 **NodeType** 및 **NodeName**입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-363">The default properties defined at each node are the **NodeType** and the **NodeName**.</span></span> <span data-ttu-id="b10f2-364">예를 들어 배치 제약 조건을 `"(NodeType == NodeType03)"`으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-364">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="b10f2-365">일반적으로 NodeType이 가장 일반적으로 사용되는 속성임을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-365">Generally we have found NodeType to be one of the most commonly used properties.</span></span> <span data-ttu-id="b10f2-366">이는 컴퓨터 종류와 1:1로 대응하므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-366">It is useful since it corresponds 1:1 with a type of a machine.</span></span> <span data-ttu-id="b10f2-367">각 컴퓨터 종류는 기존의 n 계층 응용 프로그램에서 워크로드 유형에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-367">Each type of machine corresponds to a type of workload in a traditional n-tier application.</span></span>

<span data-ttu-id="b10f2-368"><center>
![배치 제약 조건 및 노드 속성][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-368"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

## <a name="placement-constraint-and-node-property-syntax"></a><span data-ttu-id="b10f2-369">배치 제약 조건 및 노드 속성 구문</span><span class="sxs-lookup"><span data-stu-id="b10f2-369">Placement Constraint and Node Property Syntax</span></span> 
<span data-ttu-id="b10f2-370">노드 속성에서 지정된 값은 문자열, 부울 또는 기호가 있는 long이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-370">The value specified in the node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="b10f2-371">서비스가 클러스터에서 실행할 수 있는 위치를 제한하기 때문에 서비스의 문은 배치 *제약 조건*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-371">The statement at the service is called a placement *constraint* since it constrains where the service can run in the cluster.</span></span> <span data-ttu-id="b10f2-372">이 제약 조건은 클러스터의 다른 노드 속성에 작동하는 부울 문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-372">The constraint can be any Boolean statement that operates on the different node properties in the cluster.</span></span> <span data-ttu-id="b10f2-373">이러한 부울 문의 유효한 선택기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-373">The valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="b10f2-374">특정 문을 만들기 위한 조건부 검사</span><span class="sxs-lookup"><span data-stu-id="b10f2-374">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="b10f2-375">문</span><span class="sxs-lookup"><span data-stu-id="b10f2-375">Statement</span></span> | <span data-ttu-id="b10f2-376">구문</span><span class="sxs-lookup"><span data-stu-id="b10f2-376">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="b10f2-377">"같음"</span><span class="sxs-lookup"><span data-stu-id="b10f2-377">"equal to"</span></span> | <span data-ttu-id="b10f2-378">"=="</span><span class="sxs-lookup"><span data-stu-id="b10f2-378">"=="</span></span> |
| <span data-ttu-id="b10f2-379">"다음과 같지 않음"</span><span class="sxs-lookup"><span data-stu-id="b10f2-379">"not equal to"</span></span> | <span data-ttu-id="b10f2-380">"!="</span><span class="sxs-lookup"><span data-stu-id="b10f2-380">"!="</span></span> |
| <span data-ttu-id="b10f2-381">"다음보다 큼"</span><span class="sxs-lookup"><span data-stu-id="b10f2-381">"greater than"</span></span> | <span data-ttu-id="b10f2-382">">"</span><span class="sxs-lookup"><span data-stu-id="b10f2-382">">"</span></span> |
| <span data-ttu-id="b10f2-383">"다음보다 크거나 같음"</span><span class="sxs-lookup"><span data-stu-id="b10f2-383">"greater than or equal to"</span></span> | <span data-ttu-id="b10f2-384">">="</span><span class="sxs-lookup"><span data-stu-id="b10f2-384">">="</span></span> |
| <span data-ttu-id="b10f2-385">"다음보다 작음"</span><span class="sxs-lookup"><span data-stu-id="b10f2-385">"less than"</span></span> | <span data-ttu-id="b10f2-386">"<"</span><span class="sxs-lookup"><span data-stu-id="b10f2-386">"<"</span></span> |
| <span data-ttu-id="b10f2-387">"다음보다 작거나 같음"</span><span class="sxs-lookup"><span data-stu-id="b10f2-387">"less than or equal to"</span></span> | <span data-ttu-id="b10f2-388">"<="</span><span class="sxs-lookup"><span data-stu-id="b10f2-388">"<="</span></span> |

2) <span data-ttu-id="b10f2-389">그룹화 및 논리 작업에 대한 부울 문</span><span class="sxs-lookup"><span data-stu-id="b10f2-389">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="b10f2-390">문</span><span class="sxs-lookup"><span data-stu-id="b10f2-390">Statement</span></span> | <span data-ttu-id="b10f2-391">구문</span><span class="sxs-lookup"><span data-stu-id="b10f2-391">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="b10f2-392">"및"</span><span class="sxs-lookup"><span data-stu-id="b10f2-392">"and"</span></span> | <span data-ttu-id="b10f2-393">"&&"</span><span class="sxs-lookup"><span data-stu-id="b10f2-393">"&&"</span></span> |
| <span data-ttu-id="b10f2-394">"또는"</span><span class="sxs-lookup"><span data-stu-id="b10f2-394">"or"</span></span> | <span data-ttu-id="b10f2-395">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="b10f2-395">"&#124;&#124;"</span></span> |
| <span data-ttu-id="b10f2-396">"아님"</span><span class="sxs-lookup"><span data-stu-id="b10f2-396">"not"</span></span> | <span data-ttu-id="b10f2-397">"!"</span><span class="sxs-lookup"><span data-stu-id="b10f2-397">"!"</span></span> |
| <span data-ttu-id="b10f2-398">"단일 문인 그룹"</span><span class="sxs-lookup"><span data-stu-id="b10f2-398">"group as single statement"</span></span> | <span data-ttu-id="b10f2-399">"()"</span><span class="sxs-lookup"><span data-stu-id="b10f2-399">"()"</span></span> |

<span data-ttu-id="b10f2-400">다음은 기본 제약 조건문의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-400">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="b10f2-401">전체 배치 제약 조건 문이 "True"로 평가되는 노드에만 서비스가 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-401">Only nodes where the overall placement constraint statement evaluates to “True” can have the service placed on it.</span></span> <span data-ttu-id="b10f2-402">정의된 속성이 없는 노드는 해당 속성을 포함하는 배치 제약 조건과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-402">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="b10f2-403">다음과 같은 노드 속성이 제시된 노드 형식에 대해 정의되었다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-403">Let’s say that the following node properties were defined for a given node type:</span></span>

<span data-ttu-id="b10f2-404">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b10f2-404">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="b10f2-405">독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-405">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

> [!NOTE]
> <span data-ttu-id="b10f2-406">Azure 리소스 관리자 템플릿에서 노드 형식은 대개 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-406">In your Azure Resource Manager template the node type is usually parameterized.</span></span> <span data-ttu-id="b10f2-407">"NodeType01" 대신 "[parameters('vmNodeType1Name')]"와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-407">It would look like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

<span data-ttu-id="b10f2-408">다음과 같이 서비스에 대한 서비스 배치 *제약 조건*을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-408">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="b10f2-409">C#</span><span class="sxs-lookup"><span data-stu-id="b10f2-409">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="b10f2-410">Powershell:</span><span class="sxs-lookup"><span data-stu-id="b10f2-410">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="b10f2-411">NodeType01의 모든 노드가 유효하면 "(NodeType == NodeType01)" 제약 조건을 사용하여 해당 노드 형식을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-411">If all nodes of NodeType01 are valid, you can also select that node type with the constraint "(NodeType == NodeType01)".</span></span>

<span data-ttu-id="b10f2-412">서비스 배치 제약 조건에 대한 멋진 기능 중 하나는 런타임 도중 동적으로 업데이트할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-412">One of the cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="b10f2-413">따라서 필요한 경우 클러스터에서 서비스를 이동할 수 있으며, 요구 사항 등을 추가 및 제거할 수 있습니다. Service Fabric은 이러한 유형의 변경이 수행된 경우에도 서비스를 유지하고 사용할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-413">So if you need to, you can move a service around in the cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that the service stays up and available even when these types of changes are made.</span></span>

<span data-ttu-id="b10f2-414">C#:</span><span class="sxs-lookup"><span data-stu-id="b10f2-414">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="b10f2-415">Powershell:</span><span class="sxs-lookup"><span data-stu-id="b10f2-415">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="b10f2-416">배치 제약 조건은 명명된 다른 모든 서비스 인스턴스에 대해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-416">Placement constraints are specified for every different named service instance.</span></span> <span data-ttu-id="b10f2-417">업데이트는 이전에 지정된 항목(덮어쓰기)에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-417">Updates always take the place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="b10f2-418">클러스터 정의는 노드의 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-418">The cluster definition defines the properties on a node.</span></span> <span data-ttu-id="b10f2-419">노드 속성을 변경하려면 클러스터 구성을 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-419">Changing a node's properties requires a cluster configuration upgrade.</span></span> <span data-ttu-id="b10f2-420">노드 속성을 업그레이드하려면 영향을 받는 각 노드를 다시 시작하여 새 속성을 보고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-420">Upgrading a node's properties requires each affected node to restart to report its new properties.</span></span> <span data-ttu-id="b10f2-421">이러한 롤링 업그레이드는 Service Fabric에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-421">These rolling upgrades are managed by Service Fabric.</span></span>

## <a name="describing-and-managing-cluster-resources"></a><span data-ttu-id="b10f2-422">클러스터 리소스 설명 및 관리</span><span class="sxs-lookup"><span data-stu-id="b10f2-422">Describing and Managing Cluster Resources</span></span>
<span data-ttu-id="b10f2-423">모든 조정자의 가장 중요한 작업 중 하나는 클러스터에서 리소스 소비를 관리할 수 있도록 돕는 일입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-423">One of the most important jobs of any orchestrator is to help manage resource consumption in the cluster.</span></span> <span data-ttu-id="b10f2-424">클러스터 리소스 관리는 여러 가지 다른 작업을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-424">Managing cluster resources can mean a couple of different things.</span></span> <span data-ttu-id="b10f2-425">첫째, 컴퓨터에 과부하가 걸리지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-425">First, there's ensuring that machines are not overloaded.</span></span> <span data-ttu-id="b10f2-426">즉 컴퓨터에서 처리할 수 있는 것보다 더 많은 서비스를 실행하지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-426">This means making sure that machines aren't running more services than they can handle.</span></span> <span data-ttu-id="b10f2-427">둘째, 서비스를 효율적으로 실행하는 데 중요한 분산 및 최적화가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-427">Second, there's balancing and optimization which is critical to running services efficiently.</span></span> <span data-ttu-id="b10f2-428">비용 효율적이거나 성능에 민감한 서비스 제품은 일부 노드가 핫 노드인 반면 다른 노드는 콜드 노드이도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-428">Cost effective or performance sensitive service offerings can't allow some nodes to be hot while others are cold.</span></span> <span data-ttu-id="b10f2-429">핫 노드는 리소스 경합 및 성능 저하를 일으키고, 콜드 노드는 리소스 낭비와 증가한 비용 증가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-429">Hot nodes lead to resource contention and poor performance, and cold nodes represent wasted resources and increased costs.</span></span> 

<span data-ttu-id="b10f2-430">Service Fabric은 리소스를 `Metrics`으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-430">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="b10f2-431">메트릭은 서비스 패브릭에 대해 설명하려는 논리적 또는 물리적 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-431">Metrics are any logical or physical resource that you want to describe to Service Fabric.</span></span> <span data-ttu-id="b10f2-432">메트릭의 예로는 "WorkQueueDepth" 또는 "MemoryInMb" 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-432">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="b10f2-433">Service Fabric에서 노드에 대해 관리할 수 있는 물리적 리소스에 대한 자세한 내용은 [리소스 관리](service-fabric-resource-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b10f2-433">For information about the physical resources that Service Fabric can govern on nodes, see [resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="b10f2-434">사용자 지정 메트릭 및 해당 용도를 구성하는 방법에 대한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b10f2-434">For information on configuring custom metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="b10f2-435">메트릭은 배치 제약 조건 및 노드 속성이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-435">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="b10f2-436">노드 속성은 노드 자체의 정적 설명자입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-436">Node properties are static descriptors of the nodes themselves.</span></span> <span data-ttu-id="b10f2-437">메트릭은 노드에 있고 노드에서 실행될 때 서비스에서 사용하는 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-437">Metrics describe resources that nodes have and that services consume when they are run on a node.</span></span> <span data-ttu-id="b10f2-438">노드 속성은 "HasSSD"일 수 있고 true 또는 false로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-438">A node property could be "HasSSD" and could be set to true or false.</span></span> <span data-ttu-id="b10f2-439">해당 SSD에서 사용할 수 있는 공간의 양과 서비스에서 사용되는 양은 "DriveSpaceInMb"와 같은 메트릭일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-439">The amount of space available on that SSD and how much is consumed by services would be a metric like “DriveSpaceInMb”.</span></span> 

<span data-ttu-id="b10f2-440">배치 제약 조건 및 노드 속성의 경우와 같이 Service Fabric Cluster Resource Manager가 메트릭 이름의 의미를 이해하지 못한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-440">It is important to note that just like for placement constraints and node properties, the Service Fabric Cluster Resource Manager doesn't understand what the names of the metrics mean.</span></span> <span data-ttu-id="b10f2-441">메트릭 이름은 단순한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-441">Metric names are just strings.</span></span> <span data-ttu-id="b10f2-442">만든 메트릭 이름이 모호할 경우 단위를 그 일부로 선언하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-442">It is a good practice to declare units as a part of the metric names that you create when it could be ambiguous.</span></span>

## <a name="capacity"></a><span data-ttu-id="b10f2-443">용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-443">Capacity</span></span>
<span data-ttu-id="b10f2-444">모든 리소스 *분산*을 해제한 경우에도 Service Fabric의 클러스터 리소스 관리자는 여전히 노드가 해당 용량을 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-444">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="b10f2-445">클러스터가 가득 차지 않았거나 워크로드가 어떤 노드보다 크지 않으면 용량 초과를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-445">Managing capacity overruns is possible unless the cluster is too full or the workload is larger than any node.</span></span> <span data-ttu-id="b10f2-446">용량은 Cluster Resource Manager가 노드에 있는 리소스의 양을 이해하기 위해 사용하는 또 다른 *제약 조건*입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-446">Capacity is another *constraint* that the Cluster Resource Manager uses to understand how much of a resource a node has.</span></span> <span data-ttu-id="b10f2-447">전체 클러스터에 대해 남은 용량을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-447">Remaining capacity is also tracked for the cluster as a whole.</span></span> <span data-ttu-id="b10f2-448">서비스 수준에서 용량과 소비량은 메트릭을 기준으로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-448">Both the capacity and the consumption at the service level are expressed in terms of metrics.</span></span> <span data-ttu-id="b10f2-449">예를 들어 메트릭이 "ClientConnections"이고 지정된 노드에 대한 "ClientConnections" 용량이 32768일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-449">So for example, the metric might be "ClientConnections" and a given Node may have a capacity for "ClientConnections" of 32768.</span></span> <span data-ttu-id="b10f2-450">다른 노드에는 다른 제한이 있을 수 있습니다. 해당 노드에서 실행 중인 어떤 서비스에서 현재 "ClientConnections" 메트릭 중 32256을 사용하고 있다고 말할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-450">Other nodes can have other limits Some service running on that node can say it is currently consuming 32256 of the metric "ClientConnections".</span></span>

<span data-ttu-id="b10f2-451">런타임 중에 클러스터 리소스 관리자는 클러스터 및 노드에서 남아 있는 용량을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-451">During runtime, the Cluster Resource Manager tracks remaining capacity in the cluster and on nodes.</span></span> <span data-ttu-id="b10f2-452">용량을 추적하기 위해 클러스터 리소스 관리자는 서비스에서 실행되는 노드의 용량에서 각 서비스의 사용량을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-452">In order to track capacity the Cluster Resource Manager subtracts each service's usage from node's capacity where the service runs.</span></span> <span data-ttu-id="b10f2-453">이 정보를 통해 Service Fabric Cluster Resource Manager는 노드가 용량을 초과하지 않도록 복제본을 배치하거나 이동시킬 위치를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-453">With this information, the Service Fabric Cluster Resource Manager can figure out where to place or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="b10f2-454"><center>
![클러스터 노드 및 용량][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="b10f2-454"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="b10f2-455">C#:</span><span class="sxs-lookup"><span data-stu-id="b10f2-455">C#:</span></span>

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="b10f2-456">Powershell:</span><span class="sxs-lookup"><span data-stu-id="b10f2-456">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

<span data-ttu-id="b10f2-457">클러스터 매니페스트에 정의된 용량을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-457">You can see capacities defined in the cluster manifest:</span></span>

<span data-ttu-id="b10f2-458">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b10f2-458">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="b10f2-459">독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-459">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

<span data-ttu-id="b10f2-460">일반적으로 서비스의 로드는 동적으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-460">Commonly a service’s load changes dynamically.</span></span> <span data-ttu-id="b10f2-461">복제본의 "ClientConnections"로드가 1024에서 2048로 변경되었지만, 실행 중인 노드에는 해당 메트릭에 대해 512 용량만 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-461">Say that a replica's load of "ClientConnections" changed from 1024 to 2048, but the node it was running on then only had 512 capacity remaining for that metric.</span></span> <span data-ttu-id="b10f2-462">이제 해당 노드에 있는 충분한 공간이 없기 때문에 해당 복제본 또는 인스턴스의 배치가 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-462">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="b10f2-463">클러스터 리소스 관리자가 시작되고 노드를 용량 이하로 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-463">The Cluster Resource Manager has to kick in and get the node back below capacity.</span></span> <span data-ttu-id="b10f2-464">하나 이상의 복제본 또는 인스턴스를 해당 노드에서 다른 노드로 이동하여 용량을 초과한 노드의 로드를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-464">It reduces load on the node that is over capacity by moving one or more of the replicas or instances from that node to other nodes.</span></span> <span data-ttu-id="b10f2-465">복제본을 이동하는 경우 Cluster Resource Manager에서는 이러한 움직임의 비용을 최소화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-465">When moving replicas, the Cluster Resource Manager tries to minimize the cost of those movements.</span></span> <span data-ttu-id="b10f2-466">이동 비용은 [이 문서](service-fabric-cluster-resource-manager-movement-cost.md)에서 설명하고, 클러스터 리소스 관리자의 재분산 전략 및 규칙에 대한 자세한 내용은 [여기](service-fabric-cluster-resource-manager-metrics.md)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-466">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md) and more about the Cluster Resource Manager's rebalancing strategies and rules is described [here](service-fabric-cluster-resource-manager-metrics.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="b10f2-467">클러스터 용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-467">Cluster capacity</span></span>
<span data-ttu-id="b10f2-468">그렇다면 Service Fabric 클러스터 리소스 관리자에서 전체 클러스터가 가득 차지 않도록 유지하는 방법은 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="b10f2-468">So how does the Service Fabric Cluster Resource Manager keep the overall cluster from being too full?</span></span> <span data-ttu-id="b10f2-469">물론 동적 로드로 수행할 수 있는 작업은 많지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-469">Well, with dynamic load there’s not a lot it can do.</span></span> <span data-ttu-id="b10f2-470">서비스에서는 Cluster Resource Manager에서 수행한 작업과 독립적으로 해당 부하가 급증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-470">Services can have their load spike independently of actions taken by the Cluster Resource Manager.</span></span> <span data-ttu-id="b10f2-471">즉, 오늘은 여유가 많은 클러스터가 내일은 수요가 많아져 전력이 부족해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-471">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="b10f2-472">즉 문제를 방지하기 위해 변환된 몇 가지 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-472">That said, there are some controls that are baked in to prevent problems.</span></span> <span data-ttu-id="b10f2-473">가장 먼저 할 수 있는 작업은 클러스터가 꽉 차도록 만드는 워크로드가 생성되지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-473">The first thing we can do is prevent the creation of new workloads that would cause the cluster to become full.</span></span>

<span data-ttu-id="b10f2-474">상태 비저장 서비스를 만들고 여기에는 이 서비스와 연결되는 일부 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-474">Say that you create a stateless service and it has some load associated with it.</span></span> <span data-ttu-id="b10f2-475">서비스가 "DiskSpaceInMb" 메트릭을 고려하지 않는다고 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-475">Let’s say that the service cares about the "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="b10f2-476">서비스의 모든 인스턴스에 대해 5단위의 "DiskSpaceInMb"를 사용하게 된다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-476">Let's also say that it is going to consume five units of "DiskSpaceInMb" for every instance of the service.</span></span> <span data-ttu-id="b10f2-477">3개의 서비스 인스턴스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-477">You want to create three instances of the service.</span></span> <span data-ttu-id="b10f2-478">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-478">Great!</span></span> <span data-ttu-id="b10f2-479">즉, 이러한 서비스 인스턴스를 만들기 위해서는 클러스터에서 15단위의 "DiskSpaceInMb"가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-479">So that means that we need 15 units of "DiskSpaceInMb" to be present in the cluster in order for us to even be able to create these service instances.</span></span> <span data-ttu-id="b10f2-480">클러스터 리소스 관리자에서 각 메트릭의 용량 및 사용량을 지속적으로 계산하여 클러스터에 남아 있는 용량을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-480">The Cluster Resource Manager continually calculates the capacity and consumption of each metric so it can determine the remaining capacity in the cluster.</span></span> <span data-ttu-id="b10f2-481">공간이 충분하지 않으면 클러스터 리소스 관리자에서 서비스 만들기 호출을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-481">If there isn't enough space, the Cluster Resource Manager rejects the create service call.</span></span>

<span data-ttu-id="b10f2-482">요구 사항은 사용할 수 있는 15단위이기 때문에 여러 가지 방법으로 이 공간을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-482">Since the requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="b10f2-483">예를 들어, 다른 15개의 노드에서 남은 1단위의 용량이나 다른 5개의 노드에서 남은 3단위의 용량일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-483">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="b10f2-484">클러스터 리소스 관리자에서 작업을 다시 정렬하여 3개 노드에서 5단위를 사용할 수 있으면 서비스를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-484">If the Cluster Resource Manager can rearrange things so there's five units available on three nodes, it places the service.</span></span> <span data-ttu-id="b10f2-485">클러스터가 거의 가득차거나 어떤 이유로 기존 서비스를 통합할 수 없는 경우가 아니면 일반적으로 클러스터를 다시 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-485">Rearranging the cluster is usually possible unless the cluster is almost full or the existing services can't be consolidated for some reason.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="b10f2-486">버퍼링된 용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-486">Buffered Capacity</span></span>
<span data-ttu-id="b10f2-487">버퍼링된 용량은 클러스터 리소스 관리자의 또 다른 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-487">Buffered capacity is another feature of the Cluster Resource Manager.</span></span> <span data-ttu-id="b10f2-488">전체 노드 용량의 일부를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-488">It allows reservation of some portion of the overall node capacity.</span></span> <span data-ttu-id="b10f2-489">이 용량 버퍼는 업그레이드 및 노드가 실패하는 동안에만 서비스를 배치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-489">This capacity buffer is only used to place services during upgrades and node failures.</span></span> <span data-ttu-id="b10f2-490">버퍼링된 용량은 모든 노드에 대해 메트릭별로 전역으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-490">Buffered Capacity is specified globally per metric for all nodes.</span></span> <span data-ttu-id="b10f2-491">예약된 용량에 대해 선택하는 값은 클러스터에 있는 장애 도메인 및 업그레이드 도메인 수의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-491">The value you pick for the reserved capacity is a function of the number of Fault and Upgrade Domains you have in the cluster.</span></span> <span data-ttu-id="b10f2-492">장애 도메인과 업그레이드 도메인이 증가하면 버퍼링된 용량에 대해 낮은 값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-492">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="b10f2-493">더 많은 도메인이 있는 경우 업그레이드 및 오류 중 사용할 수 없는 클러스터의 수가 감소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-493">If you have more domains, you can expect smaller amounts of your cluster to be unavailable during upgrades and failures.</span></span> <span data-ttu-id="b10f2-494">버퍼링된 용량 지정은 메트릭에 노드 용량을 지정한 경우에만 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-494">Specifying Buffered Capacity only makes sense if you have also specified the node capacity for a metric.</span></span>

<span data-ttu-id="b10f2-495">버퍼링된 용량을 지정하는 방법의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-495">Here's an example of how to specify buffered capacity:</span></span>

<span data-ttu-id="b10f2-496">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b10f2-496">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="b10f2-497">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-497">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

<span data-ttu-id="b10f2-498">클러스터가 메트릭에 대해 버퍼링된 용량을 소모한 경우 새 서비스를 만드는 데 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-498">The creation of new services fails when the cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="b10f2-499">버퍼를 유지하기 위해 새 서비스를 만들지 않도록 방지하면 업그레이드 및 실패로 인해 노드의 용량이 초과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-499">Preventing the creation of new services to preserve the buffer ensures that upgrades and failures don’t cause nodes to go over capacity.</span></span> <span data-ttu-id="b10f2-500">버퍼링된 용량은 선택적이지만 메트릭에 대한 용량을 정의하는 모든 클러스터에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-500">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="b10f2-501">클러스터 리소스 관리자는 이 로드 정보를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-501">The Cluster Resource Manager exposes this load information.</span></span> <span data-ttu-id="b10f2-502">각 메트릭에 대해 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-502">For each metric, this information includes:</span></span> 
  - <span data-ttu-id="b10f2-503">버퍼링된 용량 설정</span><span class="sxs-lookup"><span data-stu-id="b10f2-503">the buffered capacity settings</span></span>
  - <span data-ttu-id="b10f2-504">총 용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-504">the total capacity</span></span>
  - <span data-ttu-id="b10f2-505">현재 사용량</span><span class="sxs-lookup"><span data-stu-id="b10f2-505">the current consumption</span></span>
  - <span data-ttu-id="b10f2-506">각 메트릭이 분산된 것으로 간주되는지 여부</span><span class="sxs-lookup"><span data-stu-id="b10f2-506">whether each metric is considered balanced or not</span></span>
  - <span data-ttu-id="b10f2-507">표준 편차에 대한 통계</span><span class="sxs-lookup"><span data-stu-id="b10f2-507">statistics about the standard deviation</span></span>
  - <span data-ttu-id="b10f2-508">최대 및 최소 로드가 있는 노드</span><span class="sxs-lookup"><span data-stu-id="b10f2-508">the nodes which have the most and least load</span></span>  
  
<span data-ttu-id="b10f2-509">해당 출력의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b10f2-509">Below we see an example of that output:</span></span>

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a><span data-ttu-id="b10f2-510">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b10f2-510">Next steps</span></span>
* <span data-ttu-id="b10f2-511">Cluster Resource Manager 내의 아키텍처 및 정보 흐름에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-architecture.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b10f2-511">For information on the architecture and information flow within the Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="b10f2-512">조각 모음 메트릭 정의는 노드의 부하를 분배하는 대신 통합하는 한 가지 방법입니다. 조각 모음을 구성하는 방법에 대해 알아보려면 [이 문서](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="b10f2-512">Defining Defragmentation Metrics is one way to consolidate load on nodes instead of spreading it out. To learn how to configure defragmentation, refer to [this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="b10f2-513">처음부터 시작 및 [서비스 패브릭 클러스터 Resource Manager 소개](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b10f2-513">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="b10f2-514">클러스터 Resource Manager가 클러스터의 부하를 관리하고 분산하는 방법을 알아보려면 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="b10f2-514">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
