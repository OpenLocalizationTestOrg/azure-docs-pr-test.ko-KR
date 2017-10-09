---
title: "aaaCluster 리소스 관리자 클러스터 설명 | Microsoft Docs"
description: "서비스 패브릭 클러스터를 설명 하는 오류 도메인과 업그레이드 도메인, 노드 속성 hello 클러스터 리소스 관리자에 대 한 노드 용량을 지정 하 여 합니다."
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
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="0eb01-103">서비스 패브릭 클러스터 설명</span><span class="sxs-lookup"><span data-stu-id="0eb01-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="0eb01-104">hello 서비스 패브릭 클러스터 리소스 관리자는 클러스터를 설명 하기 위한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-104">hello Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="0eb01-105">런타임 중 hello 클러스터 리소스 관리자는이 정보 tooensure 서비스의 고가용성 hello hello 클러스터에서 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-105">During runtime, hello Cluster Resource Manager uses this information tooensure high availability of hello services running in hello cluster.</span></span> <span data-ttu-id="0eb01-106">이러한 중요 한 규칙을 적용 하는 동안 hello 클러스터 내에서 toooptimize hello 리소스 사용도 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-106">While enforcing these important rules, it also attempts toooptimize hello resource consumption within hello cluster.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="0eb01-107">주요 개념</span><span class="sxs-lookup"><span data-stu-id="0eb01-107">Key concepts</span></span>
<span data-ttu-id="0eb01-108">hello 클러스터 리소스 관리자는 클러스터를 설명 하는 몇 가지 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-108">hello Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="0eb01-109">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-109">Fault Domains</span></span>
* <span data-ttu-id="0eb01-110">업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-110">Upgrade Domains</span></span>
* <span data-ttu-id="0eb01-111">노드 속성</span><span class="sxs-lookup"><span data-stu-id="0eb01-111">Node Properties</span></span>
* <span data-ttu-id="0eb01-112">노드 용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="0eb01-113">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-113">Fault domains</span></span>
<span data-ttu-id="0eb01-114">장애 도메인은 통합된 오류는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="0eb01-115">단일 컴퓨터 이므로 오류 도메인 (에 전원 공급 장치 오류 toodrive 오류 toobad NIC 펌웨어에서 자체에 대 한 다양 한 이유로 실패할 수 있기)입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures toodrive failures toobad NIC firmware).</span></span> <span data-ttu-id="0eb01-116">동일한 이더넷 스위치에 있는 연결 된 toohello는 동일한 장애 도메인으로 hello 컴퓨터는 전원 또는 단일 위치에서 단일 소스를 공유 하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-116">Machines connected toohello same Ethernet switch are in hello same Fault Domain, as are machines sharing a single source of power or in a single location.</span></span> <span data-ttu-id="0eb01-117">하드웨어 오류 toooverlap에 대 한 자연 이므로, 오류 도메인은 기본적으로 계층 및 서비스 패브릭에서 Uri로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-117">Since it's natural for hardware faults toooverlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="0eb01-118">오류 도메인 올바르게 설정 되어 있는지 서비스 패브릭이 정보 toosafely 위치 서비스를 사용 하므로 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-118">It is important that Fault Domains are set up correctly since Service Fabric uses this information toosafely place services.</span></span> <span data-ttu-id="0eb01-119">서비스 패브릭 tooplace 서비스 (특정 구성 요소의 hello 오류로 인해 발생) 오류 도메인의 hello 손실로 아래로 서비스 toogo 인해 되도록 싶어하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-119">Service Fabric doesn't want tooplace services such that hello loss of a Fault Domain (caused by hello failure of some component) causes a service toogo down.</span></span> <span data-ttu-id="0eb01-120">Hello 서비스 패브릭 hello 환경 toocorrectly에서 제공 하는 hello 장애 도메인 정보를 사용 하 여 Azure 환경에서에서 사용자 대신 hello hello 클러스터 노드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-120">In hello Azure environment Service Fabric uses hello Fault Domain information provided by hello environment toocorrectly configure hello nodes in hello cluster on your behalf.</span></span> <span data-ttu-id="0eb01-121">해당 hello 클러스터 hello 시 정의 된 서비스 패브릭 독립 실행형, 오류 도메인에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="0eb01-121">For Service Fabric Standalone, Fault Domains are defined at hello time that hello cluster is set up</span></span> 

> [!WARNING]
> <span data-ttu-id="0eb01-122">해당 hello 장애 도메인 정보에 제공 된 패브릭 tooService는 정확 하 게 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-122">It is important that hello Fault Domain information provided tooService Fabric is accurate.</span></span> <span data-ttu-id="0eb01-123">예를 들어 Service Fabric 클러스터의 노드가 5개의 물리적 호스트에서 실행되는 10개의 가상 컴퓨터에서 실행된다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-123">For example, let's say that your Service Fabric cluster's nodes are running inside 10 virtual machines, running on five physical hosts.</span></span> <span data-ttu-id="0eb01-124">이 경우 10개의 가상 컴퓨터가 있지만 별도의 5개(최상위 수준) 장애 도메인만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-124">In this case, even though there are 10 virtual machines, there's only 5 different (top level) fault domains.</span></span> <span data-ttu-id="0eb01-125">동일한 실제 호스트 하면 hello 공유 hello Vm 경험의 실제 호스트가 실패 하면 오류를 조정 하므로 Vm tooshare hello 동일한 루트 장애 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-125">Sharing hello same physical host causes VMs tooshare hello same root fault domain, since hello VMs experience coordinated failure if their physical host fails.</span></span>  
>
> <span data-ttu-id="0eb01-126">서비스 패브릭에서는 이후 hello 노드 하지 toochange의 오류 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-126">Since Service Fabric expects hello Fault Domain of a node not toochange.</span></span> <span data-ttu-id="0eb01-127">와 같은 hello Vm의 고가용성을 보장의 다른 메커니즘 [HA Vm](https://technet.microsoft.com/en-us/library/cc967323.aspx), 하나의 호스트 tooanother에서 Vm의 투명 한 마이그레이션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-127">Other mechanisms of ensuring high availability of hello VMs, such as [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use transparent migration of VMs from one host tooanother.</span></span> <span data-ttu-id="0eb01-128">이러한 메커니즘 다시 구성 하지 않거나 hello VM 내부에서 코드를 실행 하는 hello를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-128">These mechanisms do not reconfigure or notify hello running code inside hello VM.</span></span> <span data-ttu-id="0eb01-129">따라서 Service Fabric 클러스터를 실행하기 위한 환경으로 **지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="0eb01-129">As such, they are **not supported** as environments for running Service Fabric clusters.</span></span> <span data-ttu-id="0eb01-130">서비스 패브릭 hello 높은 가용성 기술을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-130">Service Fabric should be hello only high-availability technology employed.</span></span> <span data-ttu-id="0eb01-131">라이브 VM 마이그레이션, SAN 또는 기타와 같은 메커니즘은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-131">Mechanisms like live VM migration, SANs, or others are not necessary.</span></span> <span data-ttu-id="0eb01-132">이러한 메커니즘은 Service Fabric과 함께 사용되는 경우 복잡성을 추가하고, 중앙 집중화된 오류 원인을 추가하며, Service Fabric과 충돌하는 안정성 및 가용성 전략을 사용하기 때문에 응용 프로그램 가용성 및 안정성을 _떨어뜨립니다_.</span><span class="sxs-lookup"><span data-stu-id="0eb01-132">If used in conjunction with Service Fabric, these mechanisms _reduce_ application availability and reliability because they introduce additional complexity, add centralized sources of failure, and utilize reliability and availability strategies that conflict with those in Service Fabric.</span></span> 
>
>

<span data-ttu-id="0eb01-133">Hello 그래픽 아래에서 발생 하는 여러 장애 도메인 hello 모든 tooFault 도메인 및 목록 영향을 주는 모든 hello 엔터티 색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-133">In hello graphic below we color all hello entities that contribute tooFault Domains and list all hello different Fault Domains that result.</span></span> <span data-ttu-id="0eb01-134">이 예제에는 데이터센터("DC"), 랙("R") 및 블레이드("B")가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-134">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="0eb01-135">생각할, 하나 이상의 가상 컴퓨터를 포함 하는 각 블레이드 경우 hello 장애 도메인 계층 구조에에서는 또 다른 계층 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-135">Conceivably, if each blade holds more than one virtual machine, there could be another layer in hello Fault Domain hierarchy.</span></span>

<span data-ttu-id="0eb01-136"><center>
![장애 도메인을 통해 구성된 노드][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-136"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="0eb01-137">런타임 중 hello 서비스 패브릭 클러스터 리소스 관리자는 hello 클러스터의 hello 오류 도메인을 고려 하 및 레이아웃을 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-137">During runtime, hello Service Fabric Cluster Resource Manager considers hello Fault Domains in hello cluster and plans layouts.</span></span> <span data-ttu-id="0eb01-138">상태 저장 복제본 hello 또는 지정된 된 서비스에 대 한 상태 비저장 인스턴스는 별도 오류 도메인에 맞게 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-138">hello stateful replicas or stateless instances for a given service are distributed so they are in separate Fault Domains.</span></span> <span data-ttu-id="0eb01-139">오류 도메인을 사용 하 여 hello 서비스 분산 hello 서비스의 가용성을 hello 장애 도메인 hello 계층의 모든 수준에서 실패 한 경우 손상 되지 않도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-139">Distributing hello service across fault domains ensures hello availability of hello service is not compromised when a Fault Domain fails at any level of hello hierarchy.</span></span>

<span data-ttu-id="0eb01-140">서비스 패브릭 클러스터 리소스 관리자는 hello 장애 도메인 계층에 계층 수를 신경 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-140">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in hello Fault Domain hierarchy.</span></span> <span data-ttu-id="0eb01-141">그러나 hello 계층의 한 일부 hello 손실에 실행 되는 서비스에 영향을 주지 tooensure 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-141">However, it tries tooensure that hello loss of any one portion of hello hierarchy doesn’t impact services running in it.</span></span> 

<span data-ttu-id="0eb01-142">있는 경우 것이 가장 좋습니다 깊이 hello 장애 도메인 계층 구조에서에서 각 수준의 노드 수가 같은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-142">It is best if there are hello same number of nodes at each level of depth in hello Fault Domain hierarchy.</span></span> <span data-ttu-id="0eb01-143">오류 도메인 "트리" hello를 클러스터의 균형 잡힌 없으면 어렵게 서비스의 hello 최상의 할당 아웃 클러스터 리소스 관리자 toofigure hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-143">If hello “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for hello Cluster Resource Manager toofigure out hello best allocation of services.</span></span> <span data-ttu-id="0eb01-144">불균형 오류 도메인 레이아웃 해당 hello 손실을 일부 도메인의 다른 도메인 보다 더 많은 서비스의 영향 hello 가용성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-144">Imbalanced Fault Domains layouts mean that hello loss of some domains impact hello availability of services more than other domains.</span></span> <span data-ttu-id="0eb01-145">두 가지 목표 hello 클러스터 리소스 관리자 삭제 되는지 결과적으로,: 서비스에 배치 하 여 해당 "고급" 도메인에 toouse hello 시스템은 원하는 및 도메인의 hello 손실 문제가 발생 하지 않는 있도록은 원하는 다른 도메인에서 tooplace 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-145">As a result, hello Cluster Resource Manager is torn between two goals: It wants toouse hello machines in that “heavy” domain by placing services on them, and it wants tooplace services in other domains so that hello loss of a domain doesn’t cause problems.</span></span> 

<span data-ttu-id="0eb01-146">분산되지 않은 도메인은 어떤 모양일까요?</span><span class="sxs-lookup"><span data-stu-id="0eb01-146">What do imbalanced domains look like?</span></span> <span data-ttu-id="0eb01-147">아래 hello 다이어그램에서는 두 개의 다른 클러스터 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-147">In hello diagram below, we show two different cluster layouts.</span></span> <span data-ttu-id="0eb01-148">Hello 첫 번째 예제에서는 hello 노드 hello 오류 도메인 간에 균등 하 게 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-148">In hello first example, hello nodes are distributed evenly across hello Fault Domains.</span></span> <span data-ttu-id="0eb01-149">Hello 두 번째 예제에서는 단일 장애 도메인에 많은 노드보다 hello 다른 오류 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-149">In hello second example, one Fault Domain has many more nodes than hello other Fault Domains.</span></span> 

<span data-ttu-id="0eb01-150"><center>
![두 개의 다른 클러스터 레이아웃][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-150"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="0eb01-151">Azure의 hello 선택 장애 도메인에 노드가 드립니다 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-151">In Azure, hello choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="0eb01-152">그러나 hello 프로 비전 하는 노드 수에 따라 있습니다 수 시작할 최 오류 도메인 다른 항목 보다 더 많은 노드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-152">However, depending on hello number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="0eb01-153">예를 들어 5 개의 오류 도메인 hello 클러스터에 있지만 특정된 노드 종류에 대 한 7 개의 노드를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-153">For example, say you have five Fault Domains in hello cluster but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="0eb01-154">이 경우 hello 처음 두 개의 오류 도메인 서로 다른 노드.</span><span class="sxs-lookup"><span data-stu-id="0eb01-154">In this case, hello first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="0eb01-155">몇 개의 인스턴스만와 자세한 NodeTypes toodeploy를 계속 하면 hello 문제가 악화 될</span><span class="sxs-lookup"><span data-stu-id="0eb01-155">If you continue toodeploy more NodeTypes with only a couple instances, hello problem gets worse.</span></span> <span data-ttu-id="0eb01-156">따라서 해당 hello 것이 좋습니다 각 노드 유형에의 노드 수의 배수가 hello 장애 도메인 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-156">For this reason it's recommended that hello number of nodes in each node type is a multiple of hello number of Fault Domains.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="0eb01-157">업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-157">Upgrade domains</span></span>
<span data-ttu-id="0eb01-158">업그레이드 도메인은 서비스 패브릭 클러스터 리소스 관리자 hello 도움이 되는 또 다른 기능은 hello 클러스터의 hello 레이아웃을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-158">Upgrade Domains are another feature that helps hello Service Fabric Cluster Resource Manager understand hello layout of hello cluster.</span></span> <span data-ttu-id="0eb01-159">Hello에서 업그레이드 된 집합을 정의 하는 업그레이드 도메인 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-159">Upgrade Domains define sets of nodes that are upgraded at hello same time.</span></span> <span data-ttu-id="0eb01-160">업그레이드 도메인 도움말 hello 클러스터 리소스 관리자를 이해 하 고 업그레이드와 같은 관리 작업을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-160">Upgrade Domains help hello Cluster Resource Manager understand and orchestrate management operations like upgrades.</span></span>

<span data-ttu-id="0eb01-161">업그레이드 도메인은 장애 도메인과 많이 닮았지만 몇 가지 주요 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-161">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="0eb01-162">먼저 장애 도메인은 조정된 하드웨어 오류 영역으로 정의되지만,</span><span class="sxs-lookup"><span data-stu-id="0eb01-162">First, areas of coordinated hardware failures define Fault Domains.</span></span> <span data-ttu-id="0eb01-163">업그레이드 도메인, 다른 손 hello, 정책에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-163">Upgrade Domains, on hello other hand, are defined by policy.</span></span> <span data-ttu-id="0eb01-164">얻게 toodecide hello 환경에 의해 결정 되 고 해당 하는 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-164">You get toodecide how many you want, rather than it being dictated by hello environment.</span></span> <span data-ttu-id="0eb01-165">노드를 갖추는 만큼 많은 업그레이드 도메인을 갖출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-165">You could have as many Upgrade Domains as you do nodes.</span></span> <span data-ttu-id="0eb01-166">장애 도메인과 업그레이드 도메인의 또 다른 차이점은 업그레이드 도메인이 계층적 구조가 아니라는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-166">Another difference between Fault Domains and Upgrade Domains is that Upgrade Domains are not hierarchical.</span></span> <span data-ttu-id="0eb01-167">대신, 간단한 태그와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-167">Instead, they are more like a simple tag.</span></span> 

<span data-ttu-id="0eb01-168">hello 다음 다이어그램에서는 세 개의 업그레이드 도메인은 세 개의 오류 도메인에 걸쳐 스트라이프된</span><span class="sxs-lookup"><span data-stu-id="0eb01-168">hello following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="0eb01-169">또한 상태 저장 서비스의 세 개의 서로 다른 복제본을 배치하는 한 가지 방법을 보여줍니다. 여기서 각각 다른 장애 도메인 및 업그레이드 도메인에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-169">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="0eb01-170">이 배치 서비스 업그레이드의 hello 중간에 있는 동안 장애 도메인 hello 손실 있으며 hello 코드 및 데이터의 복사본이 두 개에 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-170">This placement allows hello loss of a Fault Domain while in hello middle of a service upgrade and still have one copy of hello code and data.</span></span>  

<span data-ttu-id="0eb01-171"><center>
![장애 도메인 및 업그레이드 도메인으로 배치][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-171"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="0eb01-172">업그레이드 도메인의 장점 및 단점 toohaving 많은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-172">There are pros and cons toohaving large numbers of Upgrade Domains.</span></span> <span data-ttu-id="0eb01-173">더 많은 업그레이드 도메인 hello 업그레이드의 각 단계는 보다 세부적인 및 적은 수의 노드 또는 서비스에 영향을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-173">More Upgrade Domains means each step of hello upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="0eb01-174">따라서 더 적은 서비스가지고 toomove 한 번에 적은 변동을 hello 시스템에 도입 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-174">As a result, fewer services have toomove at a time, introducing less churn into hello system.</span></span> <span data-ttu-id="0eb01-175">이 hello 업그레이드 하는 동안 도입 된 모든 문제의 영향을 받음 hello 서비스의 작은 이후 tooimprove 안정성을 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-175">This tends tooimprove reliability, since less of hello service is impacted by any issue introduced during hello upgrade.</span></span> <span data-ttu-id="0eb01-176">더 많은 업그레이드 도메인 필요한 다른 노드 toohandle hello 영향의 hello에 사용할 수 있는 버퍼 덜 업그레이드 하는 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-176">More Upgrade Domains also means that you need less available buffer on other nodes toohandle hello impact of hello upgrade.</span></span> <span data-ttu-id="0eb01-177">예를 들어 5 개의 업그레이드 도메인이 있는 경우 각 hello 노드는 처리 중 약 20%의 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-177">For example, if you have five Upgrade Domains, hello nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="0eb01-178">업그레이드 도메인 업그레이드 아래로 tootake 해야 할 경우 해당 부하 toogo 어딘가에 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-178">If you need tootake down that Upgrade Domain for an upgrade, that load usually needs toogo somewhere.</span></span> <span data-ttu-id="0eb01-179">나머지 4 개의 업그레이드 도메인에 한 각 트래픽 당 총 hello의 약 5%를 위한 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-179">Since you have four remaining Upgrade Domains, each must have room for about 5% of hello total traffic.</span></span> <span data-ttu-id="0eb01-180">더 많은 업그레이드 도메인 hello 클러스터의 hello 노드에서 작은 버퍼 필요한 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-180">More Upgrade Domains means you need less buffer on hello nodes in hello cluster.</span></span> <span data-ttu-id="0eb01-181">예를 들어 10개의 업그레이드 도메인을 대신 갖추는 경우를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-181">For example, consider if you had 10 Upgrade Domains instead.</span></span> <span data-ttu-id="0eb01-182">이 경우 각 UD만 처리할 수도 트래픽 당 총 hello의 약 10%입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-182">In that case, each UD would only be handling about 10% of hello total traffic.</span></span> <span data-ttu-id="0eb01-183">Hello 클러스터 통해 업그레이드 단계는 경우 각 도메인에만 toohave 공간 트래픽 당 총 hello의 약 %에 1.1을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-183">When an upgrade steps through hello cluster, each domain would only need toohave room for about 1.1% of hello total traffic.</span></span> <span data-ttu-id="0eb01-184">더 많은 업그레이드 도메인 일반적으로 사용 하면 toorun 높은 사용률 덜 예약 된 용량을 해야 하기 때문에 프로그램 노드.</span><span class="sxs-lookup"><span data-stu-id="0eb01-184">More Upgrade Domains generally allow you toorun your nodes at higher utilization, since you need less reserved capacity.</span></span> <span data-ttu-id="0eb01-185">hello에 마찬가지입니다 오류 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-185">hello same is true for Fault Domains.</span></span>  

<span data-ttu-id="0eb01-186">여러 업그레이드 도메인의 hello 단점은 업그레이드는 긴 tootake 경향이 있음을입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-186">hello downside of having many Upgrade Domains is that upgrades tend tootake longer.</span></span> <span data-ttu-id="0eb01-187">서비스 패브릭 도메인 업그레이드 완료 되 고 tooupgrade hello를 시작 하기 전에 검사를 수행 하는 시간 짧은 기간 동안 다음을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-187">Service Fabric waits a short period of time after an Upgrade Domain is completed and performs checks before starting tooupgrade hello next one.</span></span> <span data-ttu-id="0eb01-188">이러한 지연은 hello 업그레이드 진행 하기 전에 hello 업그레이드에 의해 도입 된 검색 문제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-188">These delays enable detecting issues introduced by hello upgrade before hello upgrade proceeds.</span></span> <span data-ttu-id="0eb01-189">hello 적절 한 균형을 잘못 된 변경 내용에 영향을 미치는 hello 서비스의 과도 한 번에 없기 때문에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-189">hello tradeoff is acceptable because it prevents bad changes from affecting too much of hello service at a time.</span></span>

<span data-ttu-id="0eb01-190">업그레이드 도메인이 너무 적어도 많은 부작용이 있습니다. 개별 업그레이드 도메인이 각각 중단되고 업그레이드되는 동안 전체 용량 중 상당한 부분을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-190">Too few Upgrade Domains has many negative side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="0eb01-191">예를 들어, 세 개의 업그레이드 도메인만 있는 경우 전체 서비스 또는 클러스터 용량은 약 1/3로 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-191">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="0eb01-192">클러스터 toohandle hello 워크 로드의 hello rest에서 toohave 충분 한 용량이 있어야 하므로 적절 하지 아래로 한 번에 서비스의 상당 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-192">Having so much of your service down at once isn’t desirable since you have toohave enough capacity in hello rest of your cluster toohandle hello workload.</span></span> <span data-ttu-id="0eb01-193">해당 버퍼를 유지 관리하면 정상 작업 중에 이러한 노드가 다른 경우에 로드하는 것보다 더 적게 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-193">Maintaining that buffer means that during normal operation those nodes are less loaded than they would be otherwise.</span></span> <span data-ttu-id="0eb01-194">서비스 실행 hello 비용은 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-194">This increases hello cost of running your service.</span></span>

<span data-ttu-id="0eb01-195">수는 없습니다 한계 toohello 총 결함 또는 업그레이드 도메인의 겹치는 방식을 대 한 제약 조건을 만들거나는 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-195">There’s no real limit toohello total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="0eb01-196">즉 일반적인 몇 가지 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-196">That said, there are several common patterns:</span></span>

- <span data-ttu-id="0eb01-197">1:1 매핑된 장애 도메인 및 업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-197">Fault Domains and Upgrade Domains mapped 1:1</span></span>
- <span data-ttu-id="0eb01-198">노드(실제 또는 가상 OS 인스턴스) 당 하나의 업그레이드 도메인</span><span class="sxs-lookup"><span data-stu-id="0eb01-198">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
- <span data-ttu-id="0eb01-199">여기서 hello 장애 도메인과 업그레이드 도메인 형성 행렬 hello 대각선 다운 일반적으로 실행 중인 컴퓨터와 함께 "스트라이프" 또는 "행렬" 모델</span><span class="sxs-lookup"><span data-stu-id="0eb01-199">A “striped” or “matrix” model where hello Fault Domains and Upgrade Domains form a matrix with machines usually running down hello diagonals</span></span>

<span data-ttu-id="0eb01-200"><center>
![장애 도메인 및 업그레이드 도메인 레이아웃][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-200"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="0eb01-201">없는 가장 대답 어떤 레이아웃 toochoose를 몇 가지 장점 및 단점에 각각.</span><span class="sxs-lookup"><span data-stu-id="0eb01-201">There’s no best answer which layout toochoose, each has some pros and cons.</span></span> <span data-ttu-id="0eb01-202">예를 들어 hello 1FD:1UD 모델 된 최대 간단한 tooset입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-202">For example, hello 1FD:1UD model is simple tooset up.</span></span> <span data-ttu-id="0eb01-203">hello 1 업그레이드 도메인 노드 모델당은 가장에 사용 되는 어떤 사람들은 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-203">hello 1 Upgrade Domain per Node model is most like what people are used to.</span></span> <span data-ttu-id="0eb01-204">업그레이드하는 동안 각 노드는 독립적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-204">During upgrades each node is updated independently.</span></span> <span data-ttu-id="0eb01-205">이것은 유사 toohow 작은 집합 컴퓨터의 과거 hello에서 수동으로 업그레이드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-205">This is similar toohow small sets of machines were upgraded manually in hello past.</span></span> 

<span data-ttu-id="0eb01-206">hello 가장 일반적인 모델은 hello FD/UD 행렬, 여기서 hello Ud와 Fd 형성 테이블 및 노드 대각선 hello를 따라 시작 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-206">hello most common model is hello FD/UD matrix, where hello FDs and UDs form a table and nodes are placed starting along hello diagonal.</span></span> <span data-ttu-id="0eb01-207">Azure에서 서비스 패브릭 클러스터에는 기본적으로 사용 되는 hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-207">This is hello model used by default in Service Fabric clusters in Azure.</span></span> <span data-ttu-id="0eb01-208">노드가 여러 개인 클러스터에 대 한 모든 위의 hello 조밀한 매트릭스 패턴 같은 형태를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-208">For clusters with many nodes everything ends up looking like hello dense matrix pattern above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="0eb01-209">장애 도메인 및 업그레이드 도메인 제약 조건 및 결과 동작</span><span class="sxs-lookup"><span data-stu-id="0eb01-209">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="0eb01-210">hello 클러스터 리소스 관리자는 hello desire tookeep 서비스 장애 도메인과 업그레이드 도메인 제약 조건으로 간에 균형을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-210">hello Cluster Resource Manager treats hello desire tookeep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="0eb01-211">[이 문서](service-fabric-cluster-resource-manager-management-integration.md)에서 제약 조건에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-211">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="0eb01-212">장애 도메인과 업그레이드 도메인 제약 조건 상태 hello: "지정한 서비스 파티션에 대 한 없어야 차이가 *1 보다 큰* hello 수의 서비스 개체 (상태 비저장 서비스 인스턴스 또는 상태 저장 서비스 복제본)에 두 도메인. "</span><span class="sxs-lookup"><span data-stu-id="0eb01-212">hello Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in hello number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span> <span data-ttu-id="0eb01-213">이렇게 하면 이 제약 조건을 위반하는 특정 이동 또는 배열을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-213">This prevents certain moves or arrangements that violate this constraint.</span></span>

<span data-ttu-id="0eb01-214">한 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-214">Let's look at one example.</span></span> <span data-ttu-id="0eb01-215">6개의 노드를 포함하며 5개의 장애 도메인과 5개의 업그레이드 도메인으로 구성된 클러스터가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-215">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="0eb01-216">FD0</span><span class="sxs-lookup"><span data-stu-id="0eb01-216">FD0</span></span> | <span data-ttu-id="0eb01-217">FD1</span><span class="sxs-lookup"><span data-stu-id="0eb01-217">FD1</span></span> | <span data-ttu-id="0eb01-218">FD2</span><span class="sxs-lookup"><span data-stu-id="0eb01-218">FD2</span></span> | <span data-ttu-id="0eb01-219">FD3</span><span class="sxs-lookup"><span data-stu-id="0eb01-219">FD3</span></span> | <span data-ttu-id="0eb01-220">FD4</span><span class="sxs-lookup"><span data-stu-id="0eb01-220">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="0eb01-221">**UD0**</span><span class="sxs-lookup"><span data-stu-id="0eb01-221">**UD0**</span></span> |<span data-ttu-id="0eb01-222">N1</span><span class="sxs-lookup"><span data-stu-id="0eb01-222">N1</span></span> | | | | |
| <span data-ttu-id="0eb01-223">**UD1**</span><span class="sxs-lookup"><span data-stu-id="0eb01-223">**UD1**</span></span> |<span data-ttu-id="0eb01-224">N6</span><span class="sxs-lookup"><span data-stu-id="0eb01-224">N6</span></span> |<span data-ttu-id="0eb01-225">N2</span><span class="sxs-lookup"><span data-stu-id="0eb01-225">N2</span></span> | | | |
| <span data-ttu-id="0eb01-226">**UD2**</span><span class="sxs-lookup"><span data-stu-id="0eb01-226">**UD2**</span></span> | | |<span data-ttu-id="0eb01-227">N3</span><span class="sxs-lookup"><span data-stu-id="0eb01-227">N3</span></span> | | |
| <span data-ttu-id="0eb01-228">**UD3**</span><span class="sxs-lookup"><span data-stu-id="0eb01-228">**UD3**</span></span> | | | |<span data-ttu-id="0eb01-229">N4</span><span class="sxs-lookup"><span data-stu-id="0eb01-229">N4</span></span> | |
| <span data-ttu-id="0eb01-230">**UD4**</span><span class="sxs-lookup"><span data-stu-id="0eb01-230">**UD4**</span></span> | | | | |<span data-ttu-id="0eb01-231">N5</span><span class="sxs-lookup"><span data-stu-id="0eb01-231">N5</span></span> |

<span data-ttu-id="0eb01-232">이제 TargetReplicaSetSize(또는 상태 비저장 서비스를 위한 InstanceCount)가 5인 서비스를 만든다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-232">Now let's say that we create a service with a TargetReplicaSetSize (or, for a stateless service an InstanceCount) of five.</span></span> <span data-ttu-id="0eb01-233">hello 복제본 N1 N5에 도착 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-233">hello replicas land on N1-N5.</span></span> <span data-ttu-id="0eb01-234">실제로 많은 서비스를 만들더라도 N6은 절대 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-234">In fact, N6 is never used no matter how many services like this you create.</span></span> <span data-ttu-id="0eb01-235">그렇지만 그 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="0eb01-235">But why?</span></span> <span data-ttu-id="0eb01-236">Hello 사이의 차이 hello 현재 레이아웃 N6을 선택 하면 어떻게 되는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-236">Let's look at hello difference between hello current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="0eb01-237">다음은 hello 레이아웃 म 및 hello 장애 도메인과 업그레이드 도메인 당 복제본의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-237">Here's hello layout we got and hello total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="0eb01-238">FD0</span><span class="sxs-lookup"><span data-stu-id="0eb01-238">FD0</span></span> | <span data-ttu-id="0eb01-239">FD1</span><span class="sxs-lookup"><span data-stu-id="0eb01-239">FD1</span></span> | <span data-ttu-id="0eb01-240">FD2</span><span class="sxs-lookup"><span data-stu-id="0eb01-240">FD2</span></span> | <span data-ttu-id="0eb01-241">FD3</span><span class="sxs-lookup"><span data-stu-id="0eb01-241">FD3</span></span> | <span data-ttu-id="0eb01-242">FD4</span><span class="sxs-lookup"><span data-stu-id="0eb01-242">FD4</span></span> | <span data-ttu-id="0eb01-243">UDTotal</span><span class="sxs-lookup"><span data-stu-id="0eb01-243">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="0eb01-244">**UD0**</span><span class="sxs-lookup"><span data-stu-id="0eb01-244">**UD0**</span></span> |<span data-ttu-id="0eb01-245">R1</span><span class="sxs-lookup"><span data-stu-id="0eb01-245">R1</span></span> | | | | |<span data-ttu-id="0eb01-246">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-246">1</span></span> |
| <span data-ttu-id="0eb01-247">**UD1**</span><span class="sxs-lookup"><span data-stu-id="0eb01-247">**UD1**</span></span> | |<span data-ttu-id="0eb01-248">R2</span><span class="sxs-lookup"><span data-stu-id="0eb01-248">R2</span></span> | | | |<span data-ttu-id="0eb01-249">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-249">1</span></span> |
| <span data-ttu-id="0eb01-250">**UD2**</span><span class="sxs-lookup"><span data-stu-id="0eb01-250">**UD2**</span></span> | | |<span data-ttu-id="0eb01-251">R3</span><span class="sxs-lookup"><span data-stu-id="0eb01-251">R3</span></span> | | |<span data-ttu-id="0eb01-252">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-252">1</span></span> |
| <span data-ttu-id="0eb01-253">**UD3**</span><span class="sxs-lookup"><span data-stu-id="0eb01-253">**UD3**</span></span> | | | |<span data-ttu-id="0eb01-254">R4</span><span class="sxs-lookup"><span data-stu-id="0eb01-254">R4</span></span> | |<span data-ttu-id="0eb01-255">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-255">1</span></span> |
| <span data-ttu-id="0eb01-256">**UD4**</span><span class="sxs-lookup"><span data-stu-id="0eb01-256">**UD4**</span></span> | | | | |<span data-ttu-id="0eb01-257">R5</span><span class="sxs-lookup"><span data-stu-id="0eb01-257">R5</span></span> |<span data-ttu-id="0eb01-258">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-258">1</span></span> |
| <span data-ttu-id="0eb01-259">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="0eb01-259">**FDTotal**</span></span> |<span data-ttu-id="0eb01-260">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-260">1</span></span> |<span data-ttu-id="0eb01-261">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-261">1</span></span> |<span data-ttu-id="0eb01-262">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-262">1</span></span> |<span data-ttu-id="0eb01-263">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-263">1</span></span> |<span data-ttu-id="0eb01-264">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-264">1</span></span> |- |

<span data-ttu-id="0eb01-265">이 레이아웃은 장애 도메인 및 업그레이드 도메인당 노드의 측면에서 균형을 이룹니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-265">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="0eb01-266">Hello 장애 도메인과 업그레이드 도메인 당 스냅숏 수를 기준으로 균형이 조정도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-266">It is also balanced in terms of hello number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="0eb01-267">각 도메인에는 노드 수가 같은 hello 및 hello 동일한 복제본 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-267">Each domain has hello same number of nodes and hello same number of replicas.</span></span>

<span data-ttu-id="0eb01-268">이제 N2 대신 N6를 사용하는 경우 발생하는 결과를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-268">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="0eb01-269">어떻게 hello 복제본 배포 후?</span><span class="sxs-lookup"><span data-stu-id="0eb01-269">How would hello replicas be distributed then?</span></span>

|  | <span data-ttu-id="0eb01-270">FD0</span><span class="sxs-lookup"><span data-stu-id="0eb01-270">FD0</span></span> | <span data-ttu-id="0eb01-271">FD1</span><span class="sxs-lookup"><span data-stu-id="0eb01-271">FD1</span></span> | <span data-ttu-id="0eb01-272">FD2</span><span class="sxs-lookup"><span data-stu-id="0eb01-272">FD2</span></span> | <span data-ttu-id="0eb01-273">FD3</span><span class="sxs-lookup"><span data-stu-id="0eb01-273">FD3</span></span> | <span data-ttu-id="0eb01-274">FD4</span><span class="sxs-lookup"><span data-stu-id="0eb01-274">FD4</span></span> | <span data-ttu-id="0eb01-275">UDTotal</span><span class="sxs-lookup"><span data-stu-id="0eb01-275">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="0eb01-276">**UD0**</span><span class="sxs-lookup"><span data-stu-id="0eb01-276">**UD0**</span></span> |<span data-ttu-id="0eb01-277">R1</span><span class="sxs-lookup"><span data-stu-id="0eb01-277">R1</span></span> | | | | |<span data-ttu-id="0eb01-278">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-278">1</span></span> |
| <span data-ttu-id="0eb01-279">**UD1**</span><span class="sxs-lookup"><span data-stu-id="0eb01-279">**UD1**</span></span> |<span data-ttu-id="0eb01-280">R5</span><span class="sxs-lookup"><span data-stu-id="0eb01-280">R5</span></span> | | | | |<span data-ttu-id="0eb01-281">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-281">1</span></span> |
| <span data-ttu-id="0eb01-282">**UD2**</span><span class="sxs-lookup"><span data-stu-id="0eb01-282">**UD2**</span></span> | | |<span data-ttu-id="0eb01-283">R2</span><span class="sxs-lookup"><span data-stu-id="0eb01-283">R2</span></span> | | |<span data-ttu-id="0eb01-284">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-284">1</span></span> |
| <span data-ttu-id="0eb01-285">**UD3**</span><span class="sxs-lookup"><span data-stu-id="0eb01-285">**UD3**</span></span> | | | |<span data-ttu-id="0eb01-286">R3</span><span class="sxs-lookup"><span data-stu-id="0eb01-286">R3</span></span> | |<span data-ttu-id="0eb01-287">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-287">1</span></span> |
| <span data-ttu-id="0eb01-288">**UD4**</span><span class="sxs-lookup"><span data-stu-id="0eb01-288">**UD4**</span></span> | | | | |<span data-ttu-id="0eb01-289">R4</span><span class="sxs-lookup"><span data-stu-id="0eb01-289">R4</span></span> |<span data-ttu-id="0eb01-290">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-290">1</span></span> |
| <span data-ttu-id="0eb01-291">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="0eb01-291">**FDTotal**</span></span> |<span data-ttu-id="0eb01-292">2</span><span class="sxs-lookup"><span data-stu-id="0eb01-292">2</span></span> |<span data-ttu-id="0eb01-293">0</span><span class="sxs-lookup"><span data-stu-id="0eb01-293">0</span></span> |<span data-ttu-id="0eb01-294">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-294">1</span></span> |<span data-ttu-id="0eb01-295">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-295">1</span></span> |<span data-ttu-id="0eb01-296">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-296">1</span></span> |- |

<span data-ttu-id="0eb01-297">이 레이아웃 hello 장애 도메인 제약 조건에 대 한 정의 위반합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-297">This layout violates our definition for hello Fault Domain constraint.</span></span> <span data-ttu-id="0eb01-298">FD0 FD1에 0이 함으로써 hello 차이 FD0 FD1 총 두 번의 동안 두 개의 복제본에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-298">FD0 has two replicas, while FD1 has zero, making hello difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="0eb01-299">hello 클러스터 리소스 관리자는 이러한 작업을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-299">hello Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="0eb01-300">마찬가지로 N2 및 N6(N1 및 N2 대신)을 선택한 경우 다음에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-300">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="0eb01-301">FD0</span><span class="sxs-lookup"><span data-stu-id="0eb01-301">FD0</span></span> | <span data-ttu-id="0eb01-302">FD1</span><span class="sxs-lookup"><span data-stu-id="0eb01-302">FD1</span></span> | <span data-ttu-id="0eb01-303">FD2</span><span class="sxs-lookup"><span data-stu-id="0eb01-303">FD2</span></span> | <span data-ttu-id="0eb01-304">FD3</span><span class="sxs-lookup"><span data-stu-id="0eb01-304">FD3</span></span> | <span data-ttu-id="0eb01-305">FD4</span><span class="sxs-lookup"><span data-stu-id="0eb01-305">FD4</span></span> | <span data-ttu-id="0eb01-306">UDTotal</span><span class="sxs-lookup"><span data-stu-id="0eb01-306">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="0eb01-307">**UD0**</span><span class="sxs-lookup"><span data-stu-id="0eb01-307">**UD0**</span></span> | | | | | |<span data-ttu-id="0eb01-308">0</span><span class="sxs-lookup"><span data-stu-id="0eb01-308">0</span></span> |
| <span data-ttu-id="0eb01-309">**UD1**</span><span class="sxs-lookup"><span data-stu-id="0eb01-309">**UD1**</span></span> |<span data-ttu-id="0eb01-310">R5</span><span class="sxs-lookup"><span data-stu-id="0eb01-310">R5</span></span> |<span data-ttu-id="0eb01-311">R1</span><span class="sxs-lookup"><span data-stu-id="0eb01-311">R1</span></span> | | | |<span data-ttu-id="0eb01-312">2</span><span class="sxs-lookup"><span data-stu-id="0eb01-312">2</span></span> |
| <span data-ttu-id="0eb01-313">**UD2**</span><span class="sxs-lookup"><span data-stu-id="0eb01-313">**UD2**</span></span> | | |<span data-ttu-id="0eb01-314">R2</span><span class="sxs-lookup"><span data-stu-id="0eb01-314">R2</span></span> | | |<span data-ttu-id="0eb01-315">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-315">1</span></span> |
| <span data-ttu-id="0eb01-316">**UD3**</span><span class="sxs-lookup"><span data-stu-id="0eb01-316">**UD3**</span></span> | | | |<span data-ttu-id="0eb01-317">R3</span><span class="sxs-lookup"><span data-stu-id="0eb01-317">R3</span></span> | |<span data-ttu-id="0eb01-318">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-318">1</span></span> |
| <span data-ttu-id="0eb01-319">**UD4**</span><span class="sxs-lookup"><span data-stu-id="0eb01-319">**UD4**</span></span> | | | | |<span data-ttu-id="0eb01-320">R4</span><span class="sxs-lookup"><span data-stu-id="0eb01-320">R4</span></span> |<span data-ttu-id="0eb01-321">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-321">1</span></span> |
| <span data-ttu-id="0eb01-322">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="0eb01-322">**FDTotal**</span></span> |<span data-ttu-id="0eb01-323">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-323">1</span></span> |<span data-ttu-id="0eb01-324">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-324">1</span></span> |<span data-ttu-id="0eb01-325">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-325">1</span></span> |<span data-ttu-id="0eb01-326">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-326">1</span></span> |<span data-ttu-id="0eb01-327">1</span><span class="sxs-lookup"><span data-stu-id="0eb01-327">1</span></span> |- |

<span data-ttu-id="0eb01-328">이 레이아웃은 장애 도메인 측면에서 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-328">This layout is balanced in terms of Fault Domains.</span></span> <span data-ttu-id="0eb01-329">그러나 이제 것 위반 hello 업그레이드 도메인 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-329">However, now it's violating hello Upgrade Domain constraint.</span></span> <span data-ttu-id="0eb01-330">이는 UD0에는 복제본이 없고 UD1에는 두 개의 복제본이 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-330">This is because UD0 has zero replicas while UD1 has two.</span></span> <span data-ttu-id="0eb01-331">따라서이 레이아웃도 잘못 되었으며 hello 클러스터 리소스 관리자에서 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-331">Therefore, this layout is also invalid and won't be picked by hello Cluster Resource Manager.</span></span> 

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="0eb01-332">장애 도메인 및 업그레이드 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="0eb01-332">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="0eb01-333">장애 도메인 및 업그레이드 도메인 정의는 Azure 호스티드 Service Fabric 배포에서 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-333">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="0eb01-334">서비스 패브릭을 선택 하 고 Azure의 hello 환경 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-334">Service Fabric picks up and uses hello environment information from Azure.</span></span>

<span data-ttu-id="0eb01-335">자체 클러스터를 만드는 중입니다 (또는 원하는 toorun 개발의 특정 토폴로지)를 하는 경우에 사용자가 직접 hello 장애 도메인 및 업그레이드 도메인 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-335">If you’re creating your own cluster (or want toorun a particular topology in development), you can provide hello Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="0eb01-336">이 예제에서는 각각 세 개의 랙을 가진 세 가지 "데이터 센터"에 걸쳐 있는 9개의 노드 로컬 개발 클러스터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-336">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="0eb01-337">이 클러스터에는 세 개의 해당 데이터 센터에 스트라이프된 3개의 업그레이드 도메인도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-337">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="0eb01-338">Hello 구성의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-338">An example of hello configuration is below:</span></span> 

<span data-ttu-id="0eb01-339">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0eb01-339">ClusterManifest.xml</span></span>

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

<span data-ttu-id="0eb01-340">독립 실행형 배포의 경우 ClusterConfig.json을 통해</span><span class="sxs-lookup"><span data-stu-id="0eb01-340">via ClusterConfig.json for Standalone deployments</span></span>

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
> <span data-ttu-id="0eb01-341">Azure 리소스 관리자를 통해 클러스터를 정의할 때 Azure에서 장애 도메인과 업그레이드 도메인이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-341">When defining clusters via Azure Resource Manager, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="0eb01-342">따라서 Azure Resource Manager 템플릿에 노드 형식 및 가상 컴퓨터 크기 집합의 hello 정의 장애 도메인 또는 도메인 업그레이드 정보에는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-342">Therefore, hello definition of your Node Types and Virtual Machine Scale Sets in your Azure Resource Manager template does not include Fault Domain or Upgrade Domain information.</span></span>
>

## <a name="node-properties-and-placement-constraints"></a><span data-ttu-id="0eb01-343">노드 속성 및 배치 제약 조건</span><span class="sxs-lookup"><span data-stu-id="0eb01-343">Node properties and placement constraints</span></span>
<span data-ttu-id="0eb01-344">경우에 따라 (사실, 대부분의 hello) toowant tooensure hello 클러스터의 노드 중 특정 형식에 대해서만 특정 작업을 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-344">Sometimes (in fact, most of hello time) you’re going toowant tooensure that certain workloads run only on certain types of nodes in hello cluster.</span></span> <span data-ttu-id="0eb01-345">예를 들어, 일부 워크로드는GPU 또는 SSD가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-345">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="0eb01-346">하드웨어 tooparticular 워크 로드를 대상으로의 훌륭한 예는 거의 모든 n 계층 아키텍처 있는지입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-346">A great example of targeting hardware tooparticular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="0eb01-347">특정 컴퓨터의 역할 hello 프런트 엔드 또는 API hello 응용 프로그램의 역할을 하므로 고 노출된 toohello 클라이언트 또는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-347">Certain machines serve as hello front end or API serving side of hello application and are exposed toohello clients or hello internet.</span></span> <span data-ttu-id="0eb01-348">다른 하드웨어 리소스를 서로 다른 컴퓨터 hello 계산 또는 저장소 계층의 hello 작업을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-348">Different machines, often with different hardware resources, handle hello work of hello compute or storage layers.</span></span> <span data-ttu-id="0eb01-349">일반적으로 _하지_ tooclients 직접 노출 또는 인터넷을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-349">These are usually _not_ directly exposed tooclients or hello internet.</span></span> <span data-ttu-id="0eb01-350">서비스 패브릭 경우가 있음을 특정 작업 이곳 toorun 특정 하드웨어 구성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-350">Service Fabric expects that there are cases where particular workloads need toorun on particular hardware configurations.</span></span> <span data-ttu-id="0eb01-351">예:</span><span class="sxs-lookup"><span data-stu-id="0eb01-351">For example:</span></span>

* <span data-ttu-id="0eb01-352">기존 n 계층 응용 프로그램은 서비스 패브릭 환경으로 "리프트 및 이동"되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-352">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="0eb01-353">작업 성능, 배율 또는 보안상의 이유로 격리에 대 한 특정 하드웨어에 toorun가</span><span class="sxs-lookup"><span data-stu-id="0eb01-353">a workload wants toorun on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="0eb01-354">워크로드는 정책 또는 리소스 소비를 이유로 다른 워크로드로부터 격리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-354">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="0eb01-355">toosupport 이러한 종류의 구성, 서비스 패브릭 toonodes 적용된 될 수 있는 태그의 첫 번째 클래스 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-355">toosupport these sorts of configurations, Service Fabric has a first class notion of tags that can be applied toonodes.</span></span> <span data-ttu-id="0eb01-356">이러한 태그를 **노드 속성**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-356">These tags are called **node properties**.</span></span> <span data-ttu-id="0eb01-357">**배치 제약 조건** hello 문은 하나 이상의 노드 속성에 대 한 선택 tooindividual 서비스 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-357">**Placement constraints** are hello statements attached tooindividual services that select for one or more node properties.</span></span> <span data-ttu-id="0eb01-358">배치 제약 조건은 서비스를 실행해야 하는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-358">Placement constraints define where services should run.</span></span> <span data-ttu-id="0eb01-359">제약 조건 hello 집합은 확장 가능-모든 키/값 쌍 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-359">hello set of constraints is extensible - any key/value pair can work.</span></span> 

<span data-ttu-id="0eb01-360"><center>
![다양한 클러스터 레이아웃 워크로드][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-360"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

### <a name="built-in-node-properties"></a><span data-ttu-id="0eb01-361">기본 제공 노드 속성</span><span class="sxs-lookup"><span data-stu-id="0eb01-361">Built in node properties</span></span>
<span data-ttu-id="0eb01-362">서비스 패브릭 hello 사용자 toodefine가 필요 하지 않고 자동으로 사용할 수 있는 몇 가지 기본 노드 속성을 정의 합니다. 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-362">Service Fabric defines some default node properties that can be used automatically without hello user having toodefine them.</span></span> <span data-ttu-id="0eb01-363">각 노드에 정의 된 hello 기본 속성은 hello **NodeType** 및 hello **NodeName**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-363">hello default properties defined at each node are hello **NodeType** and hello **NodeName**.</span></span> <span data-ttu-id="0eb01-364">예를 들어 배치 제약 조건을 `"(NodeType == NodeType03)"`으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-364">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="0eb01-365">일반적으로 발견 했습니다 NodeType toobe hello 가장 일반적으로 사용 되는 속성 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-365">Generally we have found NodeType toobe one of hello most commonly used properties.</span></span> <span data-ttu-id="0eb01-366">이는 컴퓨터 종류와 1:1로 대응하므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-366">It is useful since it corresponds 1:1 with a type of a machine.</span></span> <span data-ttu-id="0eb01-367">각 유형의 컴퓨터가 tooa 유형의 기존 n 계층 응용 프로그램에서 작업 부하를 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-367">Each type of machine corresponds tooa type of workload in a traditional n-tier application.</span></span>

<span data-ttu-id="0eb01-368"><center>
![배치 제약 조건 및 노드 속성][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-368"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

## <a name="placement-constraint-and-node-property-syntax"></a><span data-ttu-id="0eb01-369">배치 제약 조건 및 노드 속성 구문</span><span class="sxs-lookup"><span data-stu-id="0eb01-369">Placement Constraint and Node Property Syntax</span></span> 
<span data-ttu-id="0eb01-370">hello 값 hello 노드 속성에 지정 된 string, bool, 이거나 긴 서명.</span><span class="sxs-lookup"><span data-stu-id="0eb01-370">hello value specified in hello node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="0eb01-371">hello 문을 hello 서비스에는 배치 라고 *제약 조건* hello 서비스 hello 클러스터에서 실행할 수 있는 제한 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-371">hello statement at hello service is called a placement *constraint* since it constrains where hello service can run in hello cluster.</span></span> <span data-ttu-id="0eb01-372">hello 제약 조건에는 hello 클러스터의 hello 다른 노드 속성에 작동 하는 모든 부울 문이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-372">hello constraint can be any Boolean statement that operates on hello different node properties in hello cluster.</span></span> <span data-ttu-id="0eb01-373">다음과 같은 부울 문에서 hello 유효한 선택기는:</span><span class="sxs-lookup"><span data-stu-id="0eb01-373">hello valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="0eb01-374">특정 문을 만들기 위한 조건부 검사</span><span class="sxs-lookup"><span data-stu-id="0eb01-374">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="0eb01-375">문</span><span class="sxs-lookup"><span data-stu-id="0eb01-375">Statement</span></span> | <span data-ttu-id="0eb01-376">구문</span><span class="sxs-lookup"><span data-stu-id="0eb01-376">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="0eb01-377">"같음"</span><span class="sxs-lookup"><span data-stu-id="0eb01-377">"equal to"</span></span> | <span data-ttu-id="0eb01-378">"=="</span><span class="sxs-lookup"><span data-stu-id="0eb01-378">"=="</span></span> |
| <span data-ttu-id="0eb01-379">"다음과 같지 않음"</span><span class="sxs-lookup"><span data-stu-id="0eb01-379">"not equal to"</span></span> | <span data-ttu-id="0eb01-380">"!="</span><span class="sxs-lookup"><span data-stu-id="0eb01-380">"!="</span></span> |
| <span data-ttu-id="0eb01-381">"다음보다 큼"</span><span class="sxs-lookup"><span data-stu-id="0eb01-381">"greater than"</span></span> | <span data-ttu-id="0eb01-382">">"</span><span class="sxs-lookup"><span data-stu-id="0eb01-382">">"</span></span> |
| <span data-ttu-id="0eb01-383">"다음보다 크거나 같음"</span><span class="sxs-lookup"><span data-stu-id="0eb01-383">"greater than or equal to"</span></span> | <span data-ttu-id="0eb01-384">">="</span><span class="sxs-lookup"><span data-stu-id="0eb01-384">">="</span></span> |
| <span data-ttu-id="0eb01-385">"다음보다 작음"</span><span class="sxs-lookup"><span data-stu-id="0eb01-385">"less than"</span></span> | <span data-ttu-id="0eb01-386">"<"</span><span class="sxs-lookup"><span data-stu-id="0eb01-386">"<"</span></span> |
| <span data-ttu-id="0eb01-387">"다음보다 작거나 같음"</span><span class="sxs-lookup"><span data-stu-id="0eb01-387">"less than or equal to"</span></span> | <span data-ttu-id="0eb01-388">"<="</span><span class="sxs-lookup"><span data-stu-id="0eb01-388">"<="</span></span> |

2) <span data-ttu-id="0eb01-389">그룹화 및 논리 작업에 대한 부울 문</span><span class="sxs-lookup"><span data-stu-id="0eb01-389">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="0eb01-390">문</span><span class="sxs-lookup"><span data-stu-id="0eb01-390">Statement</span></span> | <span data-ttu-id="0eb01-391">구문</span><span class="sxs-lookup"><span data-stu-id="0eb01-391">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="0eb01-392">"및"</span><span class="sxs-lookup"><span data-stu-id="0eb01-392">"and"</span></span> | <span data-ttu-id="0eb01-393">"&&"</span><span class="sxs-lookup"><span data-stu-id="0eb01-393">"&&"</span></span> |
| <span data-ttu-id="0eb01-394">"또는"</span><span class="sxs-lookup"><span data-stu-id="0eb01-394">"or"</span></span> | <span data-ttu-id="0eb01-395">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="0eb01-395">"&#124;&#124;"</span></span> |
| <span data-ttu-id="0eb01-396">"아님"</span><span class="sxs-lookup"><span data-stu-id="0eb01-396">"not"</span></span> | <span data-ttu-id="0eb01-397">"!"</span><span class="sxs-lookup"><span data-stu-id="0eb01-397">"!"</span></span> |
| <span data-ttu-id="0eb01-398">"단일 문인 그룹"</span><span class="sxs-lookup"><span data-stu-id="0eb01-398">"group as single statement"</span></span> | <span data-ttu-id="0eb01-399">"()"</span><span class="sxs-lookup"><span data-stu-id="0eb01-399">"()"</span></span> |

<span data-ttu-id="0eb01-400">다음은 기본 제약 조건문의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-400">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="0eb01-401">여기서 hello 전반적인 배치 제약 조건 평가 되 너무 "True" 노드만 hello 서비스 배치를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-401">Only nodes where hello overall placement constraint statement evaluates too“True” can have hello service placed on it.</span></span> <span data-ttu-id="0eb01-402">정의된 속성이 없는 노드는 해당 속성을 포함하는 배치 제약 조건과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-402">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="0eb01-403">속성이 지정 된 노드 형식에 대해 정의 하는 노드 다음에 해당 hello를 가정해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="0eb01-403">Let’s say that hello following node properties were defined for a given node type:</span></span>

<span data-ttu-id="0eb01-404">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0eb01-404">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="0eb01-405">독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-405">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

> [!NOTE]
> <span data-ttu-id="0eb01-406">Azure 리소스 관리자 템플릿 hello 노드에 형식이 일반적으로 매개 변수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-406">In your Azure Resource Manager template hello node type is usually parameterized.</span></span> <span data-ttu-id="0eb01-407">"NodeType01" 대신 "[parameters('vmNodeType1Name')]"와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-407">It would look like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>
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

<span data-ttu-id="0eb01-408">다음과 같이 서비스에 대한 서비스 배치 *제약 조건*을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-408">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="0eb01-409">C#</span><span class="sxs-lookup"><span data-stu-id="0eb01-409">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="0eb01-410">Powershell:</span><span class="sxs-lookup"><span data-stu-id="0eb01-410">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="0eb01-411">모든 노드의 NodeType01 올바르면 hello 제약 조건과 해당 노드 유형을 선택할 수도 있습니다 "(NodeType == NodeType01)"입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-411">If all nodes of NodeType01 are valid, you can also select that node type with hello constraint "(NodeType == NodeType01)".</span></span>

<span data-ttu-id="0eb01-412">서비스의 배치 제약 조건에 대 한 hello 유용한 기능 중 하나는 업데이트할 수 동적으로 런타임 중입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-412">One of hello cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="0eb01-413">따라서 해야 할 경우 hello 클러스터에서 서비스를 이동, 추가 및 제거할 수 있습니다 요구 사항, 등입니다. 서비스 패브릭 처리 된 hello 서비스 유지 및 사용 가능한도 경우 이러한 종류의 변경 내용이 적용 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-413">So if you need to, you can move a service around in hello cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that hello service stays up and available even when these types of changes are made.</span></span>

<span data-ttu-id="0eb01-414">C#:</span><span class="sxs-lookup"><span data-stu-id="0eb01-414">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="0eb01-415">Powershell:</span><span class="sxs-lookup"><span data-stu-id="0eb01-415">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="0eb01-416">배치 제약 조건은 명명된 다른 모든 서비스 인스턴스에 대해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-416">Placement constraints are specified for every different named service instance.</span></span> <span data-ttu-id="0eb01-417">업데이트 항상도 일어나지 hello의 (덮어쓰기) 이전에 지정 된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-417">Updates always take hello place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="0eb01-418">hello 클러스터 정의 노드에서 hello 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-418">hello cluster definition defines hello properties on a node.</span></span> <span data-ttu-id="0eb01-419">노드 속성을 변경하려면 클러스터 구성을 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-419">Changing a node's properties requires a cluster configuration upgrade.</span></span> <span data-ttu-id="0eb01-420">업그레이드 된 노드 속성의 새 속성 각 영향을 받는 노드에서 toorestart tooreport 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-420">Upgrading a node's properties requires each affected node toorestart tooreport its new properties.</span></span> <span data-ttu-id="0eb01-421">이러한 롤링 업그레이드는 Service Fabric에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-421">These rolling upgrades are managed by Service Fabric.</span></span>

## <a name="describing-and-managing-cluster-resources"></a><span data-ttu-id="0eb01-422">클러스터 리소스 설명 및 관리</span><span class="sxs-lookup"><span data-stu-id="0eb01-422">Describing and Managing Cluster Resources</span></span>
<span data-ttu-id="0eb01-423">Hello 클러스터의 리소스 소비를 관리 하는 가장 중요 한 모든 orchestrator의 작업은 toohelp hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-423">One of hello most important jobs of any orchestrator is toohelp manage resource consumption in hello cluster.</span></span> <span data-ttu-id="0eb01-424">클러스터 리소스 관리는 여러 가지 다른 작업을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-424">Managing cluster resources can mean a couple of different things.</span></span> <span data-ttu-id="0eb01-425">첫째, 컴퓨터에 과부하가 걸리지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-425">First, there's ensuring that machines are not overloaded.</span></span> <span data-ttu-id="0eb01-426">즉 컴퓨터에서 처리할 수 있는 것보다 더 많은 서비스를 실행하지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-426">This means making sure that machines aren't running more services than they can handle.</span></span> <span data-ttu-id="0eb01-427">둘째, 균형 조정 및 최적화 효율적으로 중요 한 toorunning 서비스 되는.</span><span class="sxs-lookup"><span data-stu-id="0eb01-427">Second, there's balancing and optimization which is critical toorunning services efficiently.</span></span> <span data-ttu-id="0eb01-428">유효 하지 않거나 중요 한 서비스 제공 비용된을 허용할 수 없습니다 일부 노드 toobe 핫 이지만 나머지는 콜드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-428">Cost effective or performance sensitive service offerings can't allow some nodes toobe hot while others are cold.</span></span> <span data-ttu-id="0eb01-429">핫 노드 tooresource 경합 및 성능 저하 및 콜드 노드 불필요 하 게 나타내는 리소스 및 비용이 증가 될 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-429">Hot nodes lead tooresource contention and poor performance, and cold nodes represent wasted resources and increased costs.</span></span> 

<span data-ttu-id="0eb01-430">Service Fabric은 리소스를 `Metrics`으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-430">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="0eb01-431">메트릭은 toodescribe tooService 패브릭 원하는 논리적 또는 물리적 리소스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-431">Metrics are any logical or physical resource that you want toodescribe tooService Fabric.</span></span> <span data-ttu-id="0eb01-432">메트릭의 예로는 "WorkQueueDepth" 또는 "MemoryInMb" 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-432">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="0eb01-433">노드에서 서비스 패브릭 수 제어 하는 hello 물리적 리소스에 대 한 정보를 참조 하십시오. [리소스 관리](service-fabric-resource-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-433">For information about hello physical resources that Service Fabric can govern on nodes, see [resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="0eb01-434">사용자 지정 메트릭 및 해당 용도를 구성하는 방법에 대한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb01-434">For information on configuring custom metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="0eb01-435">메트릭은 배치 제약 조건 및 노드 속성이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-435">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="0eb01-436">노드 속성은 hello 노드 자체의 정적 설명자입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-436">Node properties are static descriptors of hello nodes themselves.</span></span> <span data-ttu-id="0eb01-437">메트릭은 노드에 있고 노드에서 실행될 때 서비스에서 사용하는 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-437">Metrics describe resources that nodes have and that services consume when they are run on a node.</span></span> <span data-ttu-id="0eb01-438">노드 속성 "HasSSD" 수 있으며 tootrue 또는 false로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-438">A node property could be "HasSSD" and could be set tootrue or false.</span></span> <span data-ttu-id="0eb01-439">해당 SSD 및 서비스에서 사용할 양을 사용 가능한 공간의 크기를 hello "DriveSpaceInMb"와 같은 메트릭을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-439">hello amount of space available on that SSD and how much is consumed by services would be a metric like “DriveSpaceInMb”.</span></span> 

<span data-ttu-id="0eb01-440">중요 한 toonote 동일 하 게 배치 제약 조건 및 노드 속성에 대 한 서비스 패브릭 클러스터 리소스 관리자 hello hello 메트릭 평균의 어떤 hello 이름을 인식 하지 못하는 하는 경우</span><span class="sxs-lookup"><span data-stu-id="0eb01-440">It is important toonote that just like for placement constraints and node properties, hello Service Fabric Cluster Resource Manager doesn't understand what hello names of hello metrics mean.</span></span> <span data-ttu-id="0eb01-441">메트릭 이름은 단순한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-441">Metric names are just strings.</span></span> <span data-ttu-id="0eb01-442">그는 hello 메트릭 이름이 모호할 때 만드는의 일부로 좋습니다 toodeclare 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-442">It is a good practice toodeclare units as a part of hello metric names that you create when it could be ambiguous.</span></span>

## <a name="capacity"></a><span data-ttu-id="0eb01-443">용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-443">Capacity</span></span>
<span data-ttu-id="0eb01-444">모든 리소스 *분산*을 해제한 경우에도 Service Fabric의 클러스터 리소스 관리자는 여전히 노드가 해당 용량을 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-444">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="0eb01-445">관리 용량 오버런 hello 클러스터 꽉 hello 작업은 모든 노드에 보다 큰 경우가 아니면 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-445">Managing capacity overruns is possible unless hello cluster is too full or hello workload is larger than any node.</span></span> <span data-ttu-id="0eb01-446">용량은 또 다른 *제약 조건* toounderstand을 사용 하 여 해당 hello 클러스터 리소스 관리자에서 노드는 리소스의 양을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-446">Capacity is another *constraint* that hello Cluster Resource Manager uses toounderstand how much of a resource a node has.</span></span> <span data-ttu-id="0eb01-447">남은 용량을 전체적으로 hello 클러스터에 대 한 추적도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-447">Remaining capacity is also tracked for hello cluster as a whole.</span></span> <span data-ttu-id="0eb01-448">Hello 용량과 hello 서비스 수준에서 hello 사용 메트릭을 기준으로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-448">Both hello capacity and hello consumption at hello service level are expressed in terms of metrics.</span></span> <span data-ttu-id="0eb01-449">예를 들어 hello 메트릭을 "ClientConnections" 될 수 있습니다 및 지정된 된 노드의 32768의 "ClientConnections"에 대 한 용량 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-449">So for example, hello metric might be "ClientConnections" and a given Node may have a capacity for "ClientConnections" of 32768.</span></span> <span data-ttu-id="0eb01-450">다른 노드는 노드 수 있는에서 실행 중인 일부 서비스 예를 들어 현재 사용 중인 "ClientConnections" hello 메트릭의 32256 기타 제한을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-450">Other nodes can have other limits Some service running on that node can say it is currently consuming 32256 of hello metric "ClientConnections".</span></span>

<span data-ttu-id="0eb01-451">런타임 중 hello 클러스터 리소스 관리자는 노드 및 hello 클러스터에서 남아 있는 용량을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-451">During runtime, hello Cluster Resource Manager tracks remaining capacity in hello cluster and on nodes.</span></span> <span data-ttu-id="0eb01-452">순서 tootrack 용량 hello 클러스터 리소스 관리자는 hello 서비스를 실행 하는 노드의 용량에서 각 서비스의 사용을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-452">In order tootrack capacity hello Cluster Resource Manager subtracts each service's usage from node's capacity where hello service runs.</span></span> <span data-ttu-id="0eb01-453">이 정보를 통해 서비스 패브릭 클러스터 리소스 관리자 hello 알아낼 수 where tooplace 또는 노드 용량 지나치게 있도록 복제 데이터베이스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-453">With this information, hello Service Fabric Cluster Resource Manager can figure out where tooplace or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="0eb01-454"><center>
![클러스터 노드 및 용량][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="0eb01-454"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="0eb01-455">C#:</span><span class="sxs-lookup"><span data-stu-id="0eb01-455">C#:</span></span>

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

<span data-ttu-id="0eb01-456">Powershell:</span><span class="sxs-lookup"><span data-stu-id="0eb01-456">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

<span data-ttu-id="0eb01-457">Hello 클러스터 매니페스트에서 정의 된 용량을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-457">You can see capacities defined in hello cluster manifest:</span></span>

<span data-ttu-id="0eb01-458">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0eb01-458">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="0eb01-459">독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-459">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

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

<span data-ttu-id="0eb01-460">일반적으로 서비스의 로드는 동적으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-460">Commonly a service’s load changes dynamically.</span></span> <span data-ttu-id="0eb01-461">복제본의 부하 "ClientConnections"의 1024 too2048를 가져오지만 hello 노드에서 실행 되 고 그런 다음 해당 메트릭에 대 한 남은 512 용량 만으로는 변경 되었음을 말하십시오.</span><span class="sxs-lookup"><span data-stu-id="0eb01-461">Say that a replica's load of "ClientConnections" changed from 1024 too2048, but hello node it was running on then only had 512 capacity remaining for that metric.</span></span> <span data-ttu-id="0eb01-462">이제 해당 노드에 있는 충분한 공간이 없기 때문에 해당 복제본 또는 인스턴스의 배치가 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-462">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="0eb01-463">hello 클러스터 리소스 관리자 tookick을 갖고 있으며 용량 보다 다시 hello 노드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-463">hello Cluster Resource Manager has tookick in and get hello node back below capacity.</span></span> <span data-ttu-id="0eb01-464">해당 노드 tooother 노드에서 하나 이상의 hello 복제본 또는 인스턴스를 이동 하 여 용량을 통해 있는 hello 노드에 대 한 부하를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-464">It reduces load on hello node that is over capacity by moving one or more of hello replicas or instances from that node tooother nodes.</span></span> <span data-ttu-id="0eb01-465">복제 데이터베이스를 이동할 때 hello 클러스터 리소스 관리자는 해당 이동의 toominimize hello 비용을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-465">When moving replicas, hello Cluster Resource Manager tries toominimize hello cost of those movements.</span></span> <span data-ttu-id="0eb01-466">이동 비용에 대해서는 설명 [이 여기서](service-fabric-cluster-resource-manager-movement-cost.md) 및 더 hello에 대 한 클러스터 리소스 관리자의 작업 재 분산 전략, 규칙 설명 [여기](service-fabric-cluster-resource-manager-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-466">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md) and more about hello Cluster Resource Manager's rebalancing strategies and rules is described [here](service-fabric-cluster-resource-manager-metrics.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="0eb01-467">클러스터 용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-467">Cluster capacity</span></span>
<span data-ttu-id="0eb01-468">어떻게는 hello 서비스 패브릭 클러스터 리소스 관리자 유지 hello 전체에서 클러스터 꽉 찬 되 고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0eb01-468">So how does hello Service Fabric Cluster Resource Manager keep hello overall cluster from being too full?</span></span> <span data-ttu-id="0eb01-469">물론 동적 로드로 수행할 수 있는 작업은 많지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-469">Well, with dynamic load there’s not a lot it can do.</span></span> <span data-ttu-id="0eb01-470">서비스는 hello 클러스터 리소스 관리자가 수행한 작업을 독립적으로 자신의 부하 스파이크를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-470">Services can have their load spike independently of actions taken by hello Cluster Resource Manager.</span></span> <span data-ttu-id="0eb01-471">즉, 오늘은 여유가 많은 클러스터가 내일은 수요가 많아져 전력이 부족해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-471">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="0eb01-472">즉, tooprevent 문제에서 구운 컨트롤이 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-472">That said, there are some controls that are baked in tooprevent problems.</span></span> <span data-ttu-id="0eb01-473">hello 먼저 할 수 있는 점은 hello 클러스터 toobecome 전체를 발생 시키는 새 워크 로드의 hello 생성을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-473">hello first thing we can do is prevent hello creation of new workloads that would cause hello cluster toobecome full.</span></span>

<span data-ttu-id="0eb01-474">상태 비저장 서비스를 만들고 여기에는 이 서비스와 연결되는 일부 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-474">Say that you create a stateless service and it has some load associated with it.</span></span> <span data-ttu-id="0eb01-475">Hello 서비스 "DiskSpaceInMb" 메트릭을 hello에 대 한 데 관심이 있는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-475">Let’s say that hello service cares about hello "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="0eb01-476">또한 경우를 가정해 하락 tooconsume 5 단위에 "DiskSpaceInMb" 모든 인스턴스에 대해 hello 서비스 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-476">Let's also say that it is going tooconsume five units of "DiskSpaceInMb" for every instance of hello service.</span></span> <span data-ttu-id="0eb01-477">Hello 서비스의 세 인스턴스 toocreate 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-477">You want toocreate three instances of hello service.</span></span> <span data-ttu-id="0eb01-478">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-478">Great!</span></span> <span data-ttu-id="0eb01-479">15 단위 "DiskSpaceInMb" toobe의 필요한 의미 tooeven 하기 위해에서 hello 클러스터의 표시 되도록 이러한 서비스 인스턴스 수 toocreate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-479">So that means that we need 15 units of "DiskSpaceInMb" toobe present in hello cluster in order for us tooeven be able toocreate these service instances.</span></span> <span data-ttu-id="0eb01-480">클러스터 리소스 관리자 hello 지속적으로 계산 hello 용량 및 각 메트릭의 소비 hello 클러스터의 hello 남은 용량을 결정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-480">hello Cluster Resource Manager continually calculates hello capacity and consumption of each metric so it can determine hello remaining capacity in hello cluster.</span></span> <span data-ttu-id="0eb01-481">충분 한 공간이 없으면 hello 클러스터 리소스 관리자를 거절 hello 서비스 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-481">If there isn't enough space, hello Cluster Resource Manager rejects hello create service call.</span></span>

<span data-ttu-id="0eb01-482">이므로 hello 요구 사항에 있는 15 단위를 사용할 수, 여러 가지 방법으로이 공간 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-482">Since hello requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="0eb01-483">예를 들어, 다른 15개의 노드에서 남은 1단위의 용량이나 다른 5개의 노드에서 남은 3단위의 용량일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-483">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="0eb01-484">Hello 클러스터 리소스 관리자 세 개의 노드에서 5 단위는 작업을 다시 정렬할 수를 찾으면 hello 서비스를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-484">If hello Cluster Resource Manager can rearrange things so there's five units available on three nodes, it places hello service.</span></span> <span data-ttu-id="0eb01-485">다시 정렬 hello 클러스터 hello 클러스터 거의 꽉 찼습니다 hello 기존 서비스 어떤 이유로 통합 될 수 없는 경우가 아니면 일반적으로 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-485">Rearranging hello cluster is usually possible unless hello cluster is almost full or hello existing services can't be consolidated for some reason.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="0eb01-486">버퍼링된 용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-486">Buffered Capacity</span></span>
<span data-ttu-id="0eb01-487">버퍼링 된 용량에는 hello 클러스터 리소스 관리자의 또 다른 기능은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-487">Buffered capacity is another feature of hello Cluster Resource Manager.</span></span> <span data-ttu-id="0eb01-488">Hello 중 일부의 예약을 통해 전체 노드 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-488">It allows reservation of some portion of hello overall node capacity.</span></span> <span data-ttu-id="0eb01-489">이 용량 버퍼는 업그레이드 및 노드 실패 하는 동안 사용 되는 유일한 tooplace 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-489">This capacity buffer is only used tooplace services during upgrades and node failures.</span></span> <span data-ttu-id="0eb01-490">버퍼링된 용량은 모든 노드에 대해 메트릭별로 전역으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-490">Buffered Capacity is specified globally per metric for all nodes.</span></span> <span data-ttu-id="0eb01-491">hello 예약 용량에 대해 선택 하는 hello 값은 장애 도메인과 업그레이드 도메인 hello 클러스터에 있는 hello 수의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-491">hello value you pick for hello reserved capacity is a function of hello number of Fault and Upgrade Domains you have in hello cluster.</span></span> <span data-ttu-id="0eb01-492">장애 도메인과 업그레이드 도메인이 증가하면 버퍼링된 용량에 대해 낮은 값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-492">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="0eb01-493">더 많은 도메인이 업그레이드 및 실패 하는 동안 사용할 수 없는 적은 수의 클러스터 toobe 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-493">If you have more domains, you can expect smaller amounts of your cluster toobe unavailable during upgrades and failures.</span></span> <span data-ttu-id="0eb01-494">버퍼링 된 용량을 지정만 합리적 지정된 hello 노드 용량 메트릭에 대 한도 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-494">Specifying Buffered Capacity only makes sense if you have also specified hello node capacity for a metric.</span></span>

<span data-ttu-id="0eb01-495">Toospecify 용량을 버퍼링 하는 방법의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-495">Here's an example of how toospecify buffered capacity:</span></span>

<span data-ttu-id="0eb01-496">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0eb01-496">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="0eb01-497">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-497">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="0eb01-498">버퍼링 된 용량 메트릭에 대 한 hello 클러스터는 경우 새 서비스의 hello 만들기 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-498">hello creation of new services fails when hello cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="0eb01-499">새 서비스 toopreserve hello 버퍼의 hello 생성을 방지 조치용 업그레이드 및 오류 노드 toogo 발생 하지는 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-499">Preventing hello creation of new services toopreserve hello buffer ensures that upgrades and failures don’t cause nodes toogo over capacity.</span></span> <span data-ttu-id="0eb01-500">버퍼링된 용량은 선택적이지만 메트릭에 대한 용량을 정의하는 모든 클러스터에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-500">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="0eb01-501">hello 클러스터 리소스 관리자는이 부하 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-501">hello Cluster Resource Manager exposes this load information.</span></span> <span data-ttu-id="0eb01-502">각 메트릭에 대해 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-502">For each metric, this information includes:</span></span> 
  - <span data-ttu-id="0eb01-503">hello 버퍼링 용량 설정</span><span class="sxs-lookup"><span data-stu-id="0eb01-503">hello buffered capacity settings</span></span>
  - <span data-ttu-id="0eb01-504">hello 총 용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-504">hello total capacity</span></span>
  - <span data-ttu-id="0eb01-505">hello 현재 사용량</span><span class="sxs-lookup"><span data-stu-id="0eb01-505">hello current consumption</span></span>
  - <span data-ttu-id="0eb01-506">각 메트릭이 분산된 것으로 간주되는지 여부</span><span class="sxs-lookup"><span data-stu-id="0eb01-506">whether each metric is considered balanced or not</span></span>
  - <span data-ttu-id="0eb01-507">hello 표준 편차에 대 한 통계</span><span class="sxs-lookup"><span data-stu-id="0eb01-507">statistics about hello standard deviation</span></span>
  - <span data-ttu-id="0eb01-508">hello 노드 hello 대부분 및 최소 부하는</span><span class="sxs-lookup"><span data-stu-id="0eb01-508">hello nodes which have hello most and least load</span></span>  
  
<span data-ttu-id="0eb01-509">해당 출력의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb01-509">Below we see an example of that output:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0eb01-510">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0eb01-510">Next steps</span></span>
* <span data-ttu-id="0eb01-511">에 대 한 내용은 hello 클러스터 리소스 관리자 내에서 hello 아키텍처 및 정보 흐름을 체크 아웃 [이 문서](service-fabric-cluster-resource-manager-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0eb01-511">For information on hello architecture and information flow within hello Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="0eb01-512">조각 모음 메트릭을 정의 하는 것은 확산 하는 대신 노드에 대 한 가지 방법은 tooconsolidate 로드 합니다. toolearn 어떻게 tooconfigure 조각 모음, 너무 참조[이 문서](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="0eb01-512">Defining Defragmentation Metrics is one way tooconsolidate load on nodes instead of spreading it out. toolearn how tooconfigure defragmentation, refer too[this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="0eb01-513">Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0eb01-513">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="0eb01-514">toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="0eb01-514">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
