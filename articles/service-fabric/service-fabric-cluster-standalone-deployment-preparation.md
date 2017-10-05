---
title: "Azure Service Fabric 독립 실행형 클러스터 배포 준비 | Microsoft Docs"
description: "프로덕션 워크로드를 처리하기 위한 클러스터를 배포하기 전에 고려해야 하는 환경 준비 및 클러스터 구성 만들기와 관련된 설명서입니다."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: f332193f9a53260173a1010b8bf9f08726bea427
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a><span data-ttu-id="3f276-103">Service Fabric 독립 실행형 클러스터 배포 계획 및 준비</span><span class="sxs-lookup"><span data-stu-id="3f276-103">Plan and prepare your Service Fabric standalone cluster deployment</span></span>
<span data-ttu-id="3f276-104">클러스터를 만들기 전에 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-104">Perform the following steps before you create your cluster.</span></span>

### <a name="step-1-plan-your-cluster-infrastructure"></a><span data-ttu-id="3f276-105">1단계: 클러스터 인프라 계획</span><span class="sxs-lookup"><span data-stu-id="3f276-105">Step 1: Plan your cluster infrastructure</span></span>
<span data-ttu-id="3f276-106">클러스터가 견뎌낼 수 있는 실패의 종류를 결정할 수 있도록 소유한 컴퓨터에서 서비스 패브릭 클러스터를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-106">You are about to create a Service Fabric cluster on machines you own, so you can decide what kinds of failures you want the cluster to survive.</span></span> <span data-ttu-id="3f276-107">예를 들어 이러한 컴퓨터를 제공하는 전원 줄 또는 인터넷 연결을 구분해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3f276-107">For example, do you need separate power lines or Internet connections supplied to these machines?</span></span> <span data-ttu-id="3f276-108">또한 이러한 컴퓨터의 물리적 보안을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-108">In addition, consider the physical security of these machines.</span></span> <span data-ttu-id="3f276-109">컴퓨터는 어디에 있으며 누가 액세스해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3f276-109">Where are the machines located and who needs access to them?</span></span> <span data-ttu-id="3f276-110">이러한 결정을 내리면 다양한 오류 도메인에 컴퓨터를 논리적으로 매핑할 수 있습니다(4단계 참조).</span><span class="sxs-lookup"><span data-stu-id="3f276-110">After you make these decisions, you can logically map the machines to the various fault domains (see Step 4).</span></span> <span data-ttu-id="3f276-111">프로덕션 클러스터에 대한 인프라 계획은 테스트 클러스터보다 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-111">The infrastructure planning for production clusters is more involved than for test clusters.</span></span>

### <a name="step-2-prepare-the-machines-to-meet-the-prerequisites"></a><span data-ttu-id="3f276-112">2단계: 컴퓨터를 준비하여 필수 구성 요소 충족</span><span class="sxs-lookup"><span data-stu-id="3f276-112">Step 2: Prepare the machines to meet the prerequisites</span></span>
<span data-ttu-id="3f276-113">클러스터에 추가하려는 각 컴퓨터에 대한 필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="3f276-113">Prerequisites for each machine that you want to add to the cluster:</span></span>

* <span data-ttu-id="3f276-114">최소 16GB의 RAM을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-114">A minimum of 16 GB of RAM is recommended.</span></span>
* <span data-ttu-id="3f276-115">최소 40GB의 사용 가능한 디스크 공간이 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-115">A minimum of 40 of GB available disk space is recommended.</span></span>
* <span data-ttu-id="3f276-116">4코어 이상의 CPU가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-116">A 4 core or greater CPU is recommended.</span></span>
* <span data-ttu-id="3f276-117">모든 컴퓨터가 보안 네트워크에 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-117">Connectivity to a secure network or networks for all machines.</span></span>
* <span data-ttu-id="3f276-118">Windows Server 2012 R2 또는 Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3f276-118">Windows Server 2012 R2 or Windows Server 2016.</span></span> 
* <span data-ttu-id="3f276-119">[.NET Framework 4.5.1 이상](https://www.microsoft.com/download/details.aspx?id=40773), 전체 설치.</span><span class="sxs-lookup"><span data-stu-id="3f276-119">[.NET Framework 4.5.1 or higher](https://www.microsoft.com/download/details.aspx?id=40773), full install.</span></span>
* <span data-ttu-id="3f276-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="3f276-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).</span></span>
* <span data-ttu-id="3f276-121">[RemoteRegistry 서비스](https://technet.microsoft.com/library/cc754820) 는 모든 컴퓨터에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-121">The [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) should be running on all the machines.</span></span>

<span data-ttu-id="3f276-122">클러스터를 배포하고 구성하는 클러스터 관리자는 각 컴퓨터에서 [관리자 권한](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) 이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-122">The cluster administrator deploying and configuring the cluster must have [administrator privileges](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) on each of the machines.</span></span> <span data-ttu-id="3f276-123">도메인 컨트롤러에 Service Fabric을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-123">You cannot install Service Fabric on a domain controller.</span></span>

### <a name="step-3-determine-the-initial-cluster-size"></a><span data-ttu-id="3f276-124">3단계: 초기 클러스터 크기 결정</span><span class="sxs-lookup"><span data-stu-id="3f276-124">Step 3: Determine the initial cluster size</span></span>
<span data-ttu-id="3f276-125">독립 실행형 Service Fabric 클러스터에 있는 각 노드는 배포된 Service Fabric 런타임을 가지며 클러스터의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-125">Each node in a standalone Service Fabric cluster has the Service Fabric runtime deployed and is a member of the cluster.</span></span> <span data-ttu-id="3f276-126">일반적인 프로덕션 배포에서는 OS 인스턴스당(실제 또는 가상) 하나의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-126">In a typical production deployment, there is one node per OS instance (physical or virtual).</span></span> <span data-ttu-id="3f276-127">클러스터 크기는 비즈니스 요구에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-127">The cluster size is determined by your business needs.</span></span> <span data-ttu-id="3f276-128">그러나 적어도 세 개 노드의 클러스터 크기가 필요합니다(컴퓨터 또는 가상 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="3f276-128">However, you must have a minimum cluster size of three nodes (machines or virtual machines).</span></span>
<span data-ttu-id="3f276-129">개발 용도로 지정된 컴퓨터에 하나 이상의 노드를 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-129">For development purposes, you can have more than one node on a given machine.</span></span> <span data-ttu-id="3f276-130">프로덕션 환경에서 서비스 패브릭은 실제 또는 가상 컴퓨터당 하나의 노드만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-130">In a production environment, Service Fabric supports only one node per physical or virtual machine.</span></span>

### <a name="step-4-determine-the-number-of-fault-domains-and-upgrade-domains"></a><span data-ttu-id="3f276-131">4단계: 장애 도메인 및 업그레이드 도메인 수 확인</span><span class="sxs-lookup"><span data-stu-id="3f276-131">Step 4: Determine the number of fault domains and upgrade domains</span></span>
<span data-ttu-id="3f276-132">*FD(장애 도메인)*는 실패의 물리적 단위이며 데이터 센터의 물리적 인프라에 직접 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-132">A *fault domain* (FD) is a physical unit of failure and is directly related to the physical infrastructure in the data centers.</span></span> <span data-ttu-id="3f276-133">장애 도메인은 실패한 단일 지점이 공유하는 하드웨어 구성 요소(컴퓨터, 스위치, 네트워크 등)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-133">A fault domain consists of hardware components (computers, switches, networks, and more) that share a single point of failure.</span></span> <span data-ttu-id="3f276-134">쉽게 말해 장애 도메인과 랙 간에 1:1 매핑이 없지만 각 랙은 장애 도메인으로 간주될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-134">Although there is no 1:1 mapping between fault domains and racks, loosely speaking, each rack can be considered a fault domain.</span></span> <span data-ttu-id="3f276-135">클러스터에서 노드를 고려하는 경우 노드가 세 개 이상의 장애 도메인에 배포되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-135">When considering the nodes in your cluster, we strongly recommend that the nodes be distributed among at least three fault domains.</span></span>

<span data-ttu-id="3f276-136">FD를 ClusterConfig.json에 지정하는 경우 각 FD의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-136">When you specify FDs in ClusterConfig.json, you can choose the name for each FD.</span></span> <span data-ttu-id="3f276-137">서비스 패브릭은 내부에서 인프라 토폴로지를 반영할 수 있도록 계층적 FD를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-137">Service Fabric supports hierarchical FDs, so you can reflect your infrastructure topology in them.</span></span>  <span data-ttu-id="3f276-138">예를 들어 다음 FD가 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-138">For example, the following FDs are valid:</span></span>

* <span data-ttu-id="3f276-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span><span class="sxs-lookup"><span data-stu-id="3f276-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span></span>
* <span data-ttu-id="3f276-140">"faultDomain": "fd:/FD1"</span><span class="sxs-lookup"><span data-stu-id="3f276-140">"faultDomain": "fd:/FD1"</span></span>
* <span data-ttu-id="3f276-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span><span class="sxs-lookup"><span data-stu-id="3f276-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span></span>

<span data-ttu-id="3f276-142">*UD(업그레이드 도메인)*는 노드의 논리적 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-142">An *upgrade domain* (UD) is a logical unit of nodes.</span></span> <span data-ttu-id="3f276-143">Service Fabric이 업그레이드(응용 프로그램 업그레이드 또는 클러스터 업그레이드)를 조정하는 동안 다른 UD의 노드를 요청을 처리하는 데 계속 사용할 수 있도록 업그레이드를 수행하기 위해 UD의 모든 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-143">During Service Fabric orchestrated upgrades (either an application upgrade or a cluster upgrade), all nodes in a UD are taken down to perform the upgrade while nodes in other UDs remain available to serve requests.</span></span> <span data-ttu-id="3f276-144">컴퓨터에 수행하는 펌웨어 업그레이드는 UD를 인식하지 못하므로 한 번에 하나의 컴퓨터를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-144">The firmware upgrades you perform on your machines do not honor UDs, so you must do them one machine at a time.</span></span>

<span data-ttu-id="3f276-145">이러한 개념에 대해 생각하는 가장 간단한 방법은 FD를 계획되지 않은 오류의 단위로, UD를 계획된 유지 관리의 단위로 인식하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-145">The simplest way to think about these concepts is to consider FDs as the unit of unplanned failure and UDs as the unit of planned maintenance.</span></span>

<span data-ttu-id="3f276-146">UD를 ClusterConfig.json에 지정하는 경우 각 UD의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-146">When you specify UDs in ClusterConfig.json, you can choose the name for each UD.</span></span> <span data-ttu-id="3f276-147">예를 들어 다음 이름이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-147">For example, the following names are valid:</span></span>

* <span data-ttu-id="3f276-148">"upgradeDomain": "UD0"</span><span class="sxs-lookup"><span data-stu-id="3f276-148">"upgradeDomain": "UD0"</span></span>
* <span data-ttu-id="3f276-149">"upgradeDomain": "UD1A"</span><span class="sxs-lookup"><span data-stu-id="3f276-149">"upgradeDomain": "UD1A"</span></span>
* <span data-ttu-id="3f276-150">"upgradeDomain": "DomainRed"</span><span class="sxs-lookup"><span data-stu-id="3f276-150">"upgradeDomain": "DomainRed"</span></span>
* <span data-ttu-id="3f276-151">"upgradeDomain": "Blue"</span><span class="sxs-lookup"><span data-stu-id="3f276-151">"upgradeDomain": "Blue"</span></span>

<span data-ttu-id="3f276-152">업그레이드 도메인 및 장애 도메인에 대한 자세한 내용은 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f276-152">For more detailed information on upgrade domains and fault domains, see [Describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>

### <a name="step-5-download-the-service-fabric-standalone-package-for-windows-server"></a><span data-ttu-id="3f276-153">5단계: Windows Server용 서비스 패브릭 독립 실행형 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="3f276-153">Step 5: Download the Service Fabric standalone package for Windows Server</span></span>
<span data-ttu-id="3f276-154">[다운로드 링크 - Service Fabric 독립 실행형 패키지 -Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690), 클러스터의 일부가 아닌 배포 컴퓨터 또는 클러스터의 일부인 컴퓨터 중 하나에 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-154">[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip the package, either to a deployment machine that is not part of the cluster, or to one of the machines that will be a part of your cluster.</span></span>

### <a name="step-6-modify-cluster-configuration"></a><span data-ttu-id="3f276-155">6단계: 클러스터 구성 수정</span><span class="sxs-lookup"><span data-stu-id="3f276-155">Step 6: Modify cluster configuration</span></span>
<span data-ttu-id="3f276-156">독립 실행형 클러스터를 만들려면 클러스터의 사양을 설명하는 독립 실행형 클러스터 구성 ClusterConfig.json 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-156">To create a standalone cluster you have to create a standalone cluster configuration ClusterConfig.json file, which describes the specification of the cluster.</span></span> <span data-ttu-id="3f276-157">아래 링크에서 찾을 수 있는 템플릿의 구성 파일을 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-157">You can base the configuration file on the templates found at the below link.</span></span> <br><span data-ttu-id="3f276-158">
[독립 실행형 클러스터 구성](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="3f276-158">
[Standalone Cluster Configurations](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<span data-ttu-id="3f276-159">이 파일의 섹션에 대한 자세한 내용은 [독립 실행형 Windows 클러스터에 대한 구성 설정](service-fabric-cluster-manifest.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f276-159">For details on the sections in this file, see [Configuration settings for standalone Windows cluster](service-fabric-cluster-manifest.md).</span></span>

<span data-ttu-id="3f276-160">다운로드한 패키지에서 ClusterConfig.json 파일 중 하나를 열고 다음 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-160">Open one of the ClusterConfig.json files from the package you downloaded and modify the following settings:</span></span>
| <span data-ttu-id="3f276-161">**구성 설정**</span><span class="sxs-lookup"><span data-stu-id="3f276-161">**Configuration Setting**</span></span> | <span data-ttu-id="3f276-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="3f276-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3f276-163">**NodeTypes**</span><span class="sxs-lookup"><span data-stu-id="3f276-163">**NodeTypes**</span></span> |<span data-ttu-id="3f276-164">노드 유형을 사용하면 클러스터 노드를 다양한 그룹으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-164">Node types allow you to separate your cluster nodes into various groups.</span></span> <span data-ttu-id="3f276-165">클러스터에는 하나 이상이 NodeType이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-165">A cluster must have at least one NodeType.</span></span> <span data-ttu-id="3f276-166">그룹의 모든 노드는 다음과 같은 일반적인 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-166">All nodes in a group have the following common characteristics:</span></span> <br> <span data-ttu-id="3f276-167">**이름** - 노드 유형 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-167">**Name** - This is the node type name.</span></span> <br><span data-ttu-id="3f276-168">**끝점 포트** - 이 노드 유형과 연결된 다양한 이름의 끝점(포트)입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-168">**Endpoint Ports** - These are various named end points (ports) that are associated with this node type.</span></span> <span data-ttu-id="3f276-169">이 매니페스트의 다른 요소와 충돌하지 않으며 컴퓨터/VM에서 실행 중인 다른 응용 프로그램에서 사용하지 않는 한 원하는 모든 포트 번호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-169">You can use any port number that you wish, as long as they do not conflict with anything else in this manifest and are not already in use by any other application running on the machine/VM.</span></span> <br> <span data-ttu-id="3f276-170">**배치 속성** - 이는 시스템 서비스 또는 서비스에 대한 배치 제약 조건으로 사용할 다음 노드 유형에 대한 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-170">**Placement Properties** - These describe properties for this node type that you use as placement constraints for the system services or your services.</span></span> <span data-ttu-id="3f276-171">이런 속성은 주어진 노드에 대한 여분의 메타데이터를 제공하는 사용자 정의 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-171">These properties are user-defined key/value pairs that provide extra meta data for a given node.</span></span> <span data-ttu-id="3f276-172">노드 속성의 예로는 노드에 하드 드라이브 또는 그래픽 카드가 있는지 여부, 하드 드라이브, 코어에 포함된 스핀들 수, 기타 물리 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-172">Examples of node properties would be whether the node has a hard drive or graphics card, the number of spindles in its hard drive, cores, and other physical properties.</span></span> <br> <span data-ttu-id="3f276-173">**용량** - 노드 용량은 특정 노드가 사용할 수 있는 특정 리소스의 이름과 양을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-173">**Capacities** - Node capacities define the name and amount of a particular resource that a particular node has available for consumption.</span></span> <span data-ttu-id="3f276-174">예를 들어 노드에는 "MemoryInMb"라는 메트릭에 대한 용량 및 기본적으로 사용할 수 있는 2048MB가 있음을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-174">For example, a node may define that it has capacity for a metric called “MemoryInMb” and that it has 2048 MB available by default.</span></span> <span data-ttu-id="3f276-175">이러한 용량은 특정한 양의 리소스를 필요로 하는 서비스가 해당 리소스가 필요한 양만큼 사용 가능한 노드에 배치되도록 런타임 시 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-175">These capacities are used at runtime to ensure that services that require particular amounts of resources are placed on the nodes that have those resources available in the required amounts.</span></span><br><span data-ttu-id="3f276-176">**IsPrimary** - 둘 이상의 NodeType이 정의되어 있으면 하나만 기본으로 설정되어 있는지 확인합니다(값 *true* 지정). 이러한 기본 유형에서 시스템 서비스가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-176">**IsPrimary** - If you have more than one NodeType defined ensure that only one is set to primary with the value *true*, which is where the system services run.</span></span> <span data-ttu-id="3f276-177">다른 모든 노드 유형은 *false* 값으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-177">All other node types should be set to the value *false*</span></span> |
| <span data-ttu-id="3f276-178">**노드**</span><span class="sxs-lookup"><span data-stu-id="3f276-178">**Nodes**</span></span> |<span data-ttu-id="3f276-179">클러스터의 일부인 노드 각각에 대한 세부 정보입니다(노드 유형, 노드 이름, IP 주소, 노드의 장애 도메인 및 업그레이드 도메인).</span><span class="sxs-lookup"><span data-stu-id="3f276-179">These are the details for each of the nodes that are part of the cluster (node type, node name, IP address, fault domain, and upgrade domain of the node).</span></span> <span data-ttu-id="3f276-180">클러스터를 만들려는 컴퓨터는 여기서 해당 IP 주소로 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-180">The machines you want the cluster to be created on need to be listed here with their IP addresses.</span></span> <br> <span data-ttu-id="3f276-181">모든 노드에 동일한 IP 주소를 사용하는 경우 다음 one-box 클러스터가 만들어지며 테스트를 목적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-181">If you use the same IP address for all the nodes, then a one-box cluster is created, which you can use for testing purposes.</span></span> <span data-ttu-id="3f276-182">one-box 클러스터는 프로덕션 워크로드를 배포하는 데 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3f276-182">Do not use One-box clusters for deploying production workloads.</span></span> |

<span data-ttu-id="3f276-183">클러스터 구성에서 모든 설정을 환경에 구성한 후 클러스터 환경에 대해 테스트할 수 있습니다(7단계).</span><span class="sxs-lookup"><span data-stu-id="3f276-183">After the cluster configuration has had all settings configured to the environment, it can be tested against the cluster environment (step 7).</span></span>

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a><span data-ttu-id="3f276-184">7단계.</span><span class="sxs-lookup"><span data-stu-id="3f276-184">Step 7.</span></span> <span data-ttu-id="3f276-185">환경 설정</span><span class="sxs-lookup"><span data-stu-id="3f276-185">Environment setup</span></span>

<span data-ttu-id="3f276-186">클러스터 관리자가 Service Fabric 독립 실행형 클러스터를 구성할 때 환경은 다음 기준으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-186">When a cluster administrator configures a Service Fabric standalone cluster, the environment is needs to be set up with the following criteria:</span></span> <br>
1. <span data-ttu-id="3f276-187">클러스터를 만드는 사용자에는 클러스터 구성 파일에서 노드로 나열된 모든 컴퓨터에 대한 관리자 수준 보안 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-187">The user creating the cluster should have administrator-level security privileges to all machines that are listed as nodes in the cluster configuration file.</span></span>
2. <span data-ttu-id="3f276-188">클러스터가 생성되는 컴퓨터 뿐 아니라 각 클러스터 노드 컴퓨터는 다음이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-188">Machine from which the cluster is created, as well as each cluster node machine must:</span></span>
* <span data-ttu-id="3f276-189">Service Fabric SDK 제거</span><span class="sxs-lookup"><span data-stu-id="3f276-189">Have Service Fabric SDK uninstalled</span></span>
* <span data-ttu-id="3f276-190">Service Fabric 런타임 제거</span><span class="sxs-lookup"><span data-stu-id="3f276-190">Have Service Fabric runtime uninstalled</span></span> 
* <span data-ttu-id="3f276-191">Windows 방화벽 서비스(mpssvc) 활성화</span><span class="sxs-lookup"><span data-stu-id="3f276-191">Have the Windows Firewall service (mpssvc) enabled</span></span>
* <span data-ttu-id="3f276-192">원격 레지스트리 서비스(remoteregistry) 활성화</span><span class="sxs-lookup"><span data-stu-id="3f276-192">Have the Remote Registry Service (remoteregistry) enabled</span></span>
* <span data-ttu-id="3f276-193">파일 공유(SMB) 활성화</span><span class="sxs-lookup"><span data-stu-id="3f276-193">Have file sharing (SMB) enabled</span></span>
* <span data-ttu-id="3f276-194">클러스터 구성 포트에 따라 필요한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="3f276-194">Have necessary ports opened, based on cluster configuration ports</span></span>
* <span data-ttu-id="3f276-195">Windows SMB 및 원격 레지스트리 서비스: 135, 137, 138, 139 및 445에 대한 필요한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="3f276-195">Have necessary ports opened for Windows SMB and Remote Registry service: 135, 137, 138, 139, and 445</span></span>
* <span data-ttu-id="3f276-196">네트워크 간 연결</span><span class="sxs-lookup"><span data-stu-id="3f276-196">Have network connectivity to one another</span></span>
3. <span data-ttu-id="3f276-197">모든 클러스터 노드 컴퓨터는 도메인 컨트롤러여서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-197">None of the cluster node machines should be a Domain Controller.</span></span>
4. <span data-ttu-id="3f276-198">배포되는 클러스터가 보안 클러스터인 경우 필수 보안 구성 요소가 배치되고 구성에 대해 올바르게 구성되어 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-198">If the cluster to be deployed is a secure cluster, validate the necessary security prerequisites are in place, and are configured correctly against the configuration.</span></span>
5. <span data-ttu-id="3f276-199">클러스터 컴퓨터를 인터넷에서 액세스할 수 없는 경우 클러스터 구성에서 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-199">If the cluster machines are not internet-accessible, set the following in the cluster configuration:</span></span>
* <span data-ttu-id="3f276-200">원격 분석 사용 안 함: *속성*에서 *“enableTelemetry”: false* 설정</span><span class="sxs-lookup"><span data-stu-id="3f276-200">Disable telemetry:   Under *properties* set   *"enableTelemetry": false*</span></span>
* <span data-ttu-id="3f276-201">자동 패브릭 버전 다운로드 및 현재 클러스터 버전이 곧 지원 종료된다는 알림 사용 안 함: *속성*에서 *“fabricClusterAutoupgradeEnabled”: false* 설정</span><span class="sxs-lookup"><span data-stu-id="3f276-201">Disable automatic Fabric version downloading & notifications that the current cluster version is nearing end of support:   Under *properties* set   *"fabricClusterAutoupgradeEnabled": false*</span></span>
* <span data-ttu-id="3f276-202">또는 네트워크 인터넷 액세스가 허용 목록 도메인으로 제한될 경우 자동 업그레이드를 위해 도메인 go.microsoft.com   download.microsoft.com이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-202">Alternatively if network internet access is limited to white-listed domains, the domains below are required for automatic upgrade:   go.microsoft.com   download.microsoft.com</span></span>

6. <span data-ttu-id="3f276-203">적절한 Service Fabric 바이러스 백신 예외 설정:</span><span class="sxs-lookup"><span data-stu-id="3f276-203">Set appropriate Service Fabric antivirus exclusions:</span></span>

| <span data-ttu-id="3f276-204">**바이러스 백신 제외된 디렉터리**</span><span class="sxs-lookup"><span data-stu-id="3f276-204">**Antivirus Excluded directories**</span></span> |
| --- |
| <span data-ttu-id="3f276-205">Program Files\Microsoft Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3f276-205">Program Files\Microsoft Service Fabric</span></span> |
| <span data-ttu-id="3f276-206">FabricDataRoot(클러스터 구성에서)</span><span class="sxs-lookup"><span data-stu-id="3f276-206">FabricDataRoot (from cluster configuration)</span></span> |
| <span data-ttu-id="3f276-207">FabricLogRoot(클러스터 구성에서)</span><span class="sxs-lookup"><span data-stu-id="3f276-207">FabricLogRoot (from cluster configuration)</span></span> |

| <span data-ttu-id="3f276-208">**바이러스 백신 제외된 프로세스**</span><span class="sxs-lookup"><span data-stu-id="3f276-208">**Antivirus Excluded processes**</span></span> |
| --- |
| <span data-ttu-id="3f276-209">Fabric.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-209">Fabric.exe</span></span> |
| <span data-ttu-id="3f276-210">FabricHost.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-210">FabricHost.exe</span></span> |
| <span data-ttu-id="3f276-211">FabricInstallerService.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-211">FabricInstallerService.exe</span></span> |
| <span data-ttu-id="3f276-212">FabricSetup.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-212">FabricSetup.exe</span></span> |
| <span data-ttu-id="3f276-213">FabricDeployer.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-213">FabricDeployer.exe</span></span> |
| <span data-ttu-id="3f276-214">ImageBuilder.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-214">ImageBuilder.exe</span></span> |
| <span data-ttu-id="3f276-215">FabricGateway.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-215">FabricGateway.exe</span></span> |
| <span data-ttu-id="3f276-216">FabricDCA.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-216">FabricDCA.exe</span></span> |
| <span data-ttu-id="3f276-217">FabricFAS.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-217">FabricFAS.exe</span></span> |
| <span data-ttu-id="3f276-218">FabricUOS.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-218">FabricUOS.exe</span></span> |
| <span data-ttu-id="3f276-219">FabricRM.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-219">FabricRM.exe</span></span> |
| <span data-ttu-id="3f276-220">FileStoreService.exe</span><span class="sxs-lookup"><span data-stu-id="3f276-220">FileStoreService.exe</span></span> |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a><span data-ttu-id="3f276-221">8단계:</span><span class="sxs-lookup"><span data-stu-id="3f276-221">Step 8.</span></span> <span data-ttu-id="3f276-222">TestConfiguration 스크립트를 사용하여 환경 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3f276-222">Validate environment using TestConfiguration script</span></span>
<span data-ttu-id="3f276-223">TestConfiguration.ps1 스크립트는 독립 실행형 패키지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-223">The TestConfiguration.ps1 script can be found in the standalone package.</span></span> <span data-ttu-id="3f276-224">위의 조건 중 일부의 유효성을 검사하는 모범 사례 분석기로 사용되며 지정된 환경에 클러스터를 배포할 수 있는지 여부를 확인하는 온전성 검사로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-224">It is used as a Best Practices Analyzer to validate some of the criteria above and should be used as a sanity check to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="3f276-225">오류가 있는 경우 문제 해결은 [환경 설치](service-fabric-cluster-standalone-deployment-preparation.md) 아래의 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f276-225">If there is any failure, refer to the list under [Environment Setup](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting.</span></span> 

<span data-ttu-id="3f276-226">이 스크립트는 클러스터 구성 파일에서 노드로 나열된 모든 컴퓨터에 대한 관리자 액세스 권한이 있는 모든 컴퓨터에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-226">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="3f276-227">이 스크립트가 실행되는 컴퓨터가 클러스터의 일부일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-227">The machine that this script is run on does not have to be part of the cluster.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

<span data-ttu-id="3f276-228">현재 이 구성 테스트 모듈은 보안 구성을 확인하지 않으므로 독립적으로 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f276-228">Currently this configuration testing module does not validate the security configuration so this has to be done independently.</span></span>  

> [!NOTE]
> <span data-ttu-id="3f276-229">이 모듈을 더욱 강력하게 만들도록 계속해서 개선하고 있으므로 현재 TestConfiguration에서 감지하지 못한다고 생각하는 결함 또는 누락된 사례가 있는 경우 [지원 채널](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)을 통해 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="3f276-229">We are continually making improvements to make this module more robust, so if there is a faulty or missing case which you believe isn't currently caught by TestConfiguration, please let us know through our [support channels](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>   
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3f276-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f276-230">Next steps</span></span>
* [<span data-ttu-id="3f276-231">Windows Server에서 실행되는 독립 실행형 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="3f276-231">Create a standalone cluster running on Windows Server</span></span>](service-fabric-cluster-creation-for-windows-server.md)
