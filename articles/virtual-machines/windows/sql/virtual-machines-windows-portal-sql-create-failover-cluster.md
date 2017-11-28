---
title: "aaaSQL 서버 FCI-Azure 가상 컴퓨터 | Microsoft Docs"
description: "이 문서에서는 설명 toocreate SQL Server 장애 조치 클러스터 인스턴스를 Azure 가상 컴퓨터는 방법입니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="12f14-103">Azure Virtual Machines에 SQL Server 장애 조치(Failover) 클러스터 인스턴스 구성</span><span class="sxs-lookup"><span data-stu-id="12f14-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="12f14-104">이 문서에 설명 방법을 toocreate SQL Server 장애 조치 클러스터 인스턴스 (FCI) 리소스 관리자 모델에서 Azure 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="12f14-105">이 솔루션에서는 [저장소 공간 다이렉트 Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) hello 노드 (Azure Vm) 간에 hello 저장소 (데이터 디스크)를 동기화 하는 소프트웨어 기반 가상 SAN으로는 Windows 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="12f14-106">S2D는 Windows Server 2016의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="12f14-107">hello 다음 그림에 hello 완벽 한 솔루션 Azure 가상 컴퓨터에:</span><span class="sxs-lookup"><span data-stu-id="12f14-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="12f14-109">이전 다이어그램에 표시 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="12f14-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="12f14-110">Windows 장애 조치(Failover) 클러스터에 있는 두 개의 Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="12f14-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="12f14-111">가상 컴퓨터가 장애 조치 클러스터에 있는 경우 *클러스터 노드* 또는 *노드*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="12f14-112">각 가상 컴퓨터에는 두 개 이상의 데이터 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="12f14-113">S2D는 hello 데이터 디스크에 hello 데이터를 동기화 하 고 저장소 풀으로 동기화 하는 hello 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="12f14-114">hello 저장소 풀에는 클러스터 공유 볼륨 (CSV) toohello 장애 조치 클러스터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="12f14-115">SQL Server FCI 클러스터 역할 hello hello 데이터 드라이브에 대 한 hello CSV를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="12f14-116">Azure 부하 분산 장치 toohold hello IP 주소를 SQL Server FCI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="12f14-117">Azure 가용성 집합 모든 hello 리소스를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="12f14-118">모든 Azure 리소스는 hello 다이어그램에서 hello에 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="12f14-119">S2D에 대한 자세한 내용은 [Windows Server 2016 Datacenter 버전 저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12f14-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="12f14-120">S2D는 두 가지 유형의 아키텍처 수렴형 및 하이퍼 수렴형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="12f14-121">이 문서에 hello 아키텍처 하이퍼 수렴 형는입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="12f14-122">하이퍼 수렴 형 인프라 위치 hello 저장소를 동일한 서버로 해당 호스트 클러스터 hello 응용 프로그램을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="12f14-123">이 아키텍처에서 hello 저장소는 각 SQL Server FCI 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="12f14-124">예제 Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="12f14-124">Example Azure template</span></span>

<span data-ttu-id="12f14-125">서식 파일에서 Azure의 hello 전체 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="12f14-126">서식 파일의 예는 hello GitHub에서에서 사용할 수 있는 [Azure 빠른 시작 템플릿](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="12f14-127">이 예제는 특정 작업에 대해 설계되거나 테스트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="12f14-128">S2D 저장소 연결 된 tooyour 도메인과 hello 템플릿 toocreate SQL Server FCI를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="12f14-129">Hello 서식 파일을 평가 하 고 용도 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="12f14-130">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="12f14-130">Before you begin</span></span>

<span data-ttu-id="12f14-131">몇 가지 방법으로 계속 진행 하기 전에 tooknow와 몇 가지 기능 필요한 위치에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="12f14-132">어떤 tooknow</span><span class="sxs-lookup"><span data-stu-id="12f14-132">What tooknow</span></span>
<span data-ttu-id="12f14-133">다음 기술 hello 작동 이해가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="12f14-134">Windows 클러스터 기술</span><span class="sxs-lookup"><span data-stu-id="12f14-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="12f14-135">[SQL Server 장애 조치(Failover) 클러스터 인스턴스](http://msdn.microsoft.com/library/ms189134.aspx)</span><span class="sxs-lookup"><span data-stu-id="12f14-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="12f14-136">또한 다음 기술을 hello에 대 한 기본적인 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="12f14-137">Windows Server 2016의 저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션</span><span class="sxs-lookup"><span data-stu-id="12f14-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="12f14-138">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="12f14-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="12f14-139">어떤 toohave</span><span class="sxs-lookup"><span data-stu-id="12f14-139">What toohave</span></span>

<span data-ttu-id="12f14-140">이 문서의 지침 hello를 수행 하기 전에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="12f14-141">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="12f14-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="12f14-142">Azure 가상 컴퓨터의 Windows 도메인</span><span class="sxs-lookup"><span data-stu-id="12f14-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="12f14-143">Hello Azure 가상 컴퓨터의에서 toocreate 개체 사용 권한 있는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="12f14-144">Azure 가상 네트워크와 서브넷에 다음과 같은 구성 요소가 hello에 대 한 충분 한 IP 주소 공간:</span><span class="sxs-lookup"><span data-stu-id="12f14-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="12f14-145">두 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="12f14-145">Both virtual machines.</span></span>
   - <span data-ttu-id="12f14-146">hello 장애 조치 클러스터 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="12f14-147">각 FCI에 대한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="12f14-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="12f14-148">DNS에 hello toohello 도메인 컨트롤러를 가리키는 Azure 네트워크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="12f14-149">이러한 필수 구성 요소가 준비되면 장애 조치 클러스터 빌드를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="12f14-150">hello 첫 번째 단계는 toocreate hello 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="12f14-151">1단계: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="12f14-152">Toohello 로그인 [Azure 포털](http://portal.azure.com) 를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="12f14-153">[Azure 가용성 집합을 만듭니다](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="12f14-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="12f14-154">hello 가용성 오류 도메인 그룹 가상 컴퓨터를 설정 하 고 도메인을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="12f14-155">hello 가용성 집합을 사용 하면 응용 프로그램이 단일 hello 네트워크 스위치, 서버 랙의 전원 공급 장치 hello 등 실패 지점의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="12f14-156">가상 컴퓨터에 대 한 hello 리소스 그룹을 만들지 않은 수행 Azure 가용성 집합을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="12f14-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="12f14-157">Hello Azure 포털 toocreate hello 가용성 집합을 사용 하는 경우 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="12f14-158">Hello Azure 포털에서에서 클릭 ** + ** tooopen hello Azure 마켓플레이스입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="12f14-159">**가용성 집합**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="12f14-160">**가용성 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="12f14-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-161">Click **Create**.</span></span>
   - <span data-ttu-id="12f14-162">Hello에 **가용성 집합 만들기** 블레이드를 다음 값에는 집합 hello:</span><span class="sxs-lookup"><span data-stu-id="12f14-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="12f14-163">**이름**: hello 가용성 집합에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="12f14-164">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="12f14-165">**리소스 그룹**: 기존 그룹 toouse 클릭 **기존 항목 사용** 및 hello 드롭 다운 목록에서 선택 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="12f14-166">그렇지 않은 경우 선택 **새로 만들기** hello 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="12f14-167">**위치**: hello 위치 toocreate 설치할 가상 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="12f14-168">**오류 도메인**: hello 기본 (3)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="12f14-169">**업데이트 도메인**: hello 기본 (5)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="12f14-170">클릭 **만들기** toocreate hello 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="12f14-171">Hello 가용성 집합의 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="12f14-172">Hello Azure 가용성 집합에 두 개의 SQL Server 가상 컴퓨터를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="12f14-173">자세한 내용은 [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="12f14-174">두 가상 컴퓨터를 다음에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="12f14-175">Hello 가능 여부를 설정 하는 같은 Azure 리소스 그룹에서는입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="12f14-176">Hello에 도메인 컨트롤러로 네트워크 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="12f14-177">두 가상 컴퓨터에 대한 충분한 IP 주소 공간이 있는 서브넷 및 이 클러스터에서 사용할 수 있는 모든 FCI에.</span><span class="sxs-lookup"><span data-stu-id="12f14-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="12f14-178">Hello Azure 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="12f14-179">가상 컴퓨터를 만든 후에 가용성 집합을 설정 또는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="12f14-180">Hello Azure Marketplace에서에서 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="12f14-181">마켓플레이스를 사용할 수 있습니다 Windows Server 및 SQL Server 또는 Windows Server 정당한 hello를 사용 하 여 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="12f14-182">자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../../virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12f14-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="12f14-183">hello 공식 SQL Server 이미지 hello Azure 갤러리에서에서 설치 된 SQL Server 인스턴스 및 hello SQL Server를 설치 하는 소프트웨어 및 hello 필요한 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="12f14-184">원하는 toohow toopay hello SQL Server 라이선스에 따라 hello 오른쪽 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="12f14-185">**사용 라이선스 비용을 지불**: 이러한 이미지의 분당 비용 hello hello SQL Server 라이선스에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="12f14-186">**Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="12f14-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="12f14-187">**Windows Server Datacenter 2016의 SQL Server 2016 Standard**</span><span class="sxs-lookup"><span data-stu-id="12f14-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="12f14-188">**Windows Server Datacenter 2016의 SQL Server 2016 Developer**</span><span class="sxs-lookup"><span data-stu-id="12f14-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="12f14-189">**BYOL(사용자 라이선스 필요)**</span><span class="sxs-lookup"><span data-stu-id="12f14-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="12f14-190">**{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="12f14-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="12f14-191">**{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Standard**</span><span class="sxs-lookup"><span data-stu-id="12f14-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="12f14-192">Hello 가상 컴퓨터를 만든 후 hello 사전 설치 된 독립 실행형 SQL Server 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="12f14-193">Hello 장애 조치 클러스터와 S2D을 구성한 후에 hello 사전 설치 된 SQL Server 미디어 toocreate hello SQL Server FCI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="12f14-194">또는 바로 hello 운영 체제와 함께 Azure 마켓플레이스 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="12f14-195">선택 된 **Windows Server 2016 Datacenter** 이미지 및 S2D 및 hello 장애 조치 클러스터 구성 후 hello SQL Server FCI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="12f14-196">이 이미지는 SQL Server 설치 이미지를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="12f14-197">각 서버에 대 한 hello SQL Server 설치를 실행할 수 있는 위치에 hello 설치 미디어를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="12f14-198">Azure 가상 컴퓨터를 만든 후 RDP와 tooeach 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="12f14-199">RDP와 tooa 가상 컴퓨터를 처음 연결 하면 hello 컴퓨터 묻는 tooallow이 PC toobe hello 네트워크에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="12f14-200">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-200">Click **Yes**.</span></span>

1. <span data-ttu-id="12f14-201">Hello SQL Server 기반 가상 컴퓨터 이미지 중 하나를 사용 하는 경우 hello SQL Server 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="12f14-202">**프로그램 및 기능**에서 **Microsoft SQL Server 2016(64비트)**을 마우스 오른쪽 단추로 클릭하고 **제거/변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="12f14-203">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-203">Click **Remove**.</span></span>
   - <span data-ttu-id="12f14-204">Hello 기본 인스턴스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-204">Select hello default instance.</span></span>
   - <span data-ttu-id="12f14-205">**데이터베이스 엔진 서비스**에서 모든 기능을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="12f14-206">**공유 기능**을 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="12f14-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="12f14-207">Hello 다음 그림을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="12f14-207">See hello following picture:</span></span>

      ![기능 제거](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="12f14-209">**다음**을 클릭한 후 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="12f14-210"><a name="ports"></a>Hello 방화벽 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="12f14-211">각 가상 컴퓨터에서 포트에 나오는 hello Windows 방화벽에 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="12f14-212">목적</span><span class="sxs-lookup"><span data-stu-id="12f14-212">Purpose</span></span> | <span data-ttu-id="12f14-213">TCP 포트</span><span class="sxs-lookup"><span data-stu-id="12f14-213">TCP Port</span></span> | <span data-ttu-id="12f14-214">참고</span><span class="sxs-lookup"><span data-stu-id="12f14-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="12f14-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="12f14-215">SQL Server</span></span> | <span data-ttu-id="12f14-216">1433</span><span class="sxs-lookup"><span data-stu-id="12f14-216">1433</span></span> | <span data-ttu-id="12f14-217">SQL Server의 기본 인스턴스에 대한 표준 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="12f14-218">Hello 갤러리에서 이미지를 사용 하는 경우에이 포트는 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="12f14-219">상태 프로브</span><span class="sxs-lookup"><span data-stu-id="12f14-219">Health probe</span></span> | <span data-ttu-id="12f14-220">59999</span><span class="sxs-lookup"><span data-stu-id="12f14-220">59999</span></span> | <span data-ttu-id="12f14-221">모든 공개 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-221">Any open TCP port.</span></span> <span data-ttu-id="12f14-222">이후 단계에서 hello 부하 분산 장치 구성 [상태 프로브](#probe) 클러스터 toouse이이 포트 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="12f14-223">저장소 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="12f14-224">자세한 내용은 [저장소 추가](../../../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12f14-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="12f14-225">두 가상 컴퓨터에 두 개 이상의 데이터 디스크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="12f14-226">NTFS 포맷 디스크가 아닌 원시 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="12f14-227">NTFS 포맷 디스크를 연결하는 경우 디스크 자격 확인 없이 S2D를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="12f14-228">최소 두 개의 프리미엄 저장소 (SSD 디스크) tooeach VM 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="12f14-229">적어도 P30(1TB) 디스크가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="12f14-230">집합 호스트 너무 캐싱**읽기 전용**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="12f14-231">프로덕션 환경에서 사용 하는 hello 스토리지 용량 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="12f14-232">이 문서에서 설명 하는 hello 값 데모 및 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="12f14-233">[Hello 가상 컴퓨터 tooyour 기존 도메인을 추가](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="12f14-234">Hello 가상 컴퓨터를 만들고 구성한 후에 hello 장애 조치 클러스터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="12f14-235">2 단계: S2D와 hello Windows 장애 조치 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="12f14-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="12f14-236">hello 다음 단계와 S2D tooconfigure hello 장애 조치 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="12f14-237">이 단계에서 수행한 하위 단계 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="12f14-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="12f14-238">Windows 장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="12f14-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="12f14-239">Hello 클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12f14-239">Validate hello cluster</span></span>
1. <span data-ttu-id="12f14-240">Hello 장애 조치 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="12f14-241">Hello 클라우드 미러링 모니터 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="12f14-242">저장소 추가</span><span class="sxs-lookup"><span data-stu-id="12f14-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="12f14-243">Windows 장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="12f14-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="12f14-244">toobegin, Active Directory의 권한 toocreate 개체 되었으며 로컬 관리자의 멤버인 도메인 계정을 사용 하 여 RDP를 사용 하 여 toohello 첫 번째 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="12f14-245">Hello 구성의 hello 나머지를 위해이 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="12f14-246">[장애 조치 클러스터링 기능 tooeach 가상 컴퓨터 추가](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="12f14-247">hello UI에서에서 장애 조치 클러스터링 기능은 tooinstall 두 가상 컴퓨터에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="12f14-248">**서버 관리자**에서 **관리**를 클릭한 다음 **역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="12f14-249">**추가 역할 및 기능 마법사**, 클릭 **다음** 너무에 도달할 때까지**기능 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="12f14-250">**기능 선택**에서 **장애 조치(Failover) 클러스터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="12f14-251">모든 필요한 기능 및 hello 관리 도구를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="12f14-252">**기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="12f14-253">클릭 **다음** 클릭 하 고 **마침** tooinstall hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="12f14-254">tooinstall hello 장애 조치 클러스터링 기능은 powershell을 hello 나오는 hello 가상 컴퓨터 중 하나에 따라 관리자 권한 PowerShell 세션에서 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="12f14-255">Hello 다음 단계를 참조로의 3 단계 hello 지침을 따르십시오 [Windows Server 2016에서 저장소 공간 다이렉트를 사용 하 여 하이퍼 수렴 형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="12f14-256">Hello 클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12f14-256">Validate hello cluster</span></span>

<span data-ttu-id="12f14-257">이 설명서에서는 아래 tooinstructions [클러스터 유효성 검사](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="12f14-258">Hello UI에서에서 또는 PowerShell을 사용 하는 hello 클러스터의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="12f14-259">UI hello로 toovalidate hello 클러스터 hello 가상 컴퓨터 중 하나에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="12f14-260">**서버 관리자**에서 **도구**를 클릭한 다음 **장애 조치(Failover) 클러스터 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="12f14-261">**장애 조치(Failover) 클러스터 관리자**에서 **작업**을 클릭한 다음 **구성 유효성 검사...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="12f14-262">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-262">Click **Next**.</span></span>
1. <span data-ttu-id="12f14-263">**서버 선택 또는 클러스터**, 두 가상 컴퓨터의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="12f14-264">**테스트 옵션**에서 **선택한 테스트만 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="12f14-265">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-265">Click **Next**.</span></span>
1. <span data-ttu-id="12f14-266">**테스트 선택**에서 **저장소**를 제외한 모든 테스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="12f14-267">Hello 다음 그림을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="12f14-267">See hello following picture:</span></span>

   ![유효성 검사 테스트](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="12f14-269">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-269">Click **Next**.</span></span>
1. <span data-ttu-id="12f14-270">**확인**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="12f14-271">hello **유효성 검사 구성 마법사** 실행 hello 유효성 검사 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="12f14-272">powershell을 실행 hello 가상 컴퓨터 중 하나에 관리자 권한 PowerShell 세션에서 스크립트를 다음과 같은 hello toovalidate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="12f14-273">Hello 클러스터, 유효성 검사 후 hello 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="12f14-274">Hello 장애 조치 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-274">Create hello failover cluster</span></span>

<span data-ttu-id="12f14-275">이 가이드는 너무 참조[hello 장애 조치 클러스터 만들기](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="12f14-276">toocreate hello 장애 조치 클러스터를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="12f14-277">hello 클러스터 노드 역할을 하는 hello 가상 컴퓨터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="12f14-278">Hello 장애 조치 클러스터에 대 한 이름</span><span class="sxs-lookup"><span data-stu-id="12f14-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="12f14-279">Hello 장애 조치 클러스터에 대 한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="12f14-280">Hello에 사용 되지 않는 IP 주소를 사용할 수 있습니다 동일한 Azure 가상 네트워크와 서브넷을 클러스터 노드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="12f14-281">다음 PowerShell hello 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="12f14-282">Hello hello 노드 (가상 컴퓨터 이름 hello) 이름 사용 하 여 hello 스크립트와 hello Azure VNET에서에서 사용 가능한 IP 주소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="12f14-283">클라우드 감시 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-283">Create a cloud witness</span></span>

<span data-ttu-id="12f14-284">클라우드 감시는 Azure Storage Blob에 저장된 새로운 유형의 클러스터 쿼럼 감시입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="12f14-285">미러링 모니터 서버 공유를 호스트 하는 별도 VM의 hello 필요성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="12f14-286">[Hello 장애 조치 클러스터에 대 한 클라우드 감시 만들기](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="12f14-287">Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-287">Create a blob container.</span></span>

1. <span data-ttu-id="12f14-288">Hello 액세스 키 및 hello 컨테이너 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="12f14-289">Hello 장애 조치 클러스터의 클러스터 쿼럼 감시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="12f14-290">[Hello 사용자 인터페이스에 구성 hello 쿼럼 감시를] 참조 하십시오. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="12f14-291">저장소 추가</span><span class="sxs-lookup"><span data-stu-id="12f14-291">Add storage</span></span>

<span data-ttu-id="12f14-292">hello 디스크 S2D에 대 한 빈 및 파티션 또는 기타 데이터 없이 toobe를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="12f14-293">tooclean 디스크에 따라 [이 가이드의 단계를 hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="12f14-294">[저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="12f14-295">다음 PowerShell hello 직접 액세스를 저장소 공간을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="12f14-296">**장애 조치 클러스터 관리자**, 이제 hello 저장소 풀을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="12f14-297">[볼륨을 만듭니다](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="12f14-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="12f14-298">S2D hello 기능 중 하나는 사용 하도록 설정 하면 저장소 풀을 자동으로 만들 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="12f14-299">준비 toocreate 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="12f14-300">PowerShell commandlet hello `New-Volume` 서식 toohello 클러스터를 추가 하 고, 클러스터 공유 볼륨 (CSV) 만들기를 포함 하 여 hello 볼륨 만들기 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="12f14-301">hello 다음 예제는 800 기가바이트 (GB) CSV 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="12f14-302">이 명령이 완료되면 클러스터 리소스로 800GB 볼륨이 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="12f14-303">hello 볼륨이에 `C:\ClusterStorage\Volume1\`합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="12f14-304">다이어그램을 다음 hello S2D 클러스터 공유 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="12f14-306">3단계: 장애 조치 클러스터의 장애 조치 테스트</span><span class="sxs-lookup"><span data-stu-id="12f14-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="12f14-307">장애 조치 클러스터 관리자에서 이동할 수 있는지 hello 저장소 리소스 toohello 다른 클러스터 노드로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="12f14-308">Toohello 장애 조치 클러스터와 연결할 수 있는 경우 **장애 조치 클러스터 관리자** 에서 하나의 노드만 toohello 다른 hello 저장소를 이동 하 고, 준비 tooconfigure hello FCI는 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="12f14-309">4단계: SQL Server FCI 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="12f14-310">Hello 장애 조치 클러스터와 저장소를 포함 하 여 모든 클러스터 구성 요소를 구성 하 고 나면 hello SQL Server FCI를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="12f14-311">RDP와 toohello 첫 번째 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="12f14-312">**장애 조치 클러스터 관리자**, 모든 클러스터 코어 리소스 hello 첫 번째 가상 컴퓨터에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="12f14-313">필요한 경우에 모든 리소스 toothis 가상 컴퓨터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="12f14-314">Hello 설치 미디어를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-314">Locate hello installation media.</span></span> <span data-ttu-id="12f14-315">Hello 미디어에는 가상 컴퓨터가 hello hello Azure 마켓플레이스 이미지 중 하나를 사용 하는 경우 `C:\SQLServer_<version number>_Full`합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="12f14-316">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-316">Click **Setup**.</span></span>

1. <span data-ttu-id="12f14-317">Hello에 **SQL Server 설치 센터**, 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="12f14-318">**새 SQL Server 장애 조치(failover) 클러스터 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="12f14-319">Hello 마법사 tooinstall hello SQL Server FCI의에서 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="12f14-320">hello FCI 데이터 디렉터리 toobe 클러스터 된 저장소에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="12f14-321">S2D, 이므로 없이 각 서버에 있는 탑재 지점 tooa 볼륨 하지만 공유 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="12f14-322">S2D 두 노드 간에 hello 볼륨을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="12f14-323">hello 볼륨이 클러스터 공유 볼륨으로 toohello 클러스터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="12f14-324">Hello 데이터 디렉터리에 대 한 hello CSV 탑재 지점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="12f14-326">Hello 마법사를 마친 후 설치 프로그램 hello 첫 번째 노드에 SQL Server FCI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="12f14-327">성공적으로 설치 hello FCI hello 첫 번째 노드에 설치 된 후 RDP와 toohello 두 번째 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="12f14-328">열기 hello **SQL Server 설치 센터**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="12f14-329">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-329">Click **Installation**.</span></span>

1. <span data-ttu-id="12f14-330">클릭 **추가 노드 tooa SQL Server 장애 조치 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="12f14-331">Hello 마법사 tooinstall SQL server의 hello 지침을 따르고이 서버 toohello FCI를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="12f14-332">SQL Server와 함께 Azure 마켓플레이스 갤러리 이미지를 사용 하는 경우 SQL Server 도구 hello 이미지와 함께 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="12f14-333">이 이미지를 사용 하지 않은 경우 별도로 hello SQL Server 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="12f14-334">[SSMS(SQL Server Management Studio) 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12f14-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="12f14-335">5단계: Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="12f14-336">Azure 가상 컴퓨터에서 클러스터는 부하 분산 장치 toohold에 한 번에 하나의 클러스터 노드에서 toobe 필요한 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="12f14-337">이 솔루션에서는 hello 부하 분산 장치는 SQL Server FCI hello에 대 한 hello IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="12f14-338">[Azure Load Balancer를 만들고 구성합니다](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="12f14-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="12f14-339">Hello Azure 포털에서에서 hello 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="12f14-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="12f14-340">toocreate hello 부하 분산 장치:</span><span class="sxs-lookup"><span data-stu-id="12f14-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="12f14-341">Azure 포털 hello hello 가상 컴퓨터와 toohello 리소스 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="12f14-342">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-342">Click **+ Add**.</span></span> <span data-ttu-id="12f14-343">마켓플레이스 검색 hello에 대 한 **부하 분산 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="12f14-344">**부하 분산 장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="12f14-345">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-345">Click **Create**.</span></span>

1. <span data-ttu-id="12f14-346">포함 된 hello 부하 분산 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="12f14-347">**이름**: hello 부하 분산 장치를 식별 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="12f14-348">**형식**: hello 부하 분산 장치는 모두 public 또는 private 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="12f14-349">개인 부하 분산 장치 내에서 액세스할 수 동일한 VNET hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="12f14-350">대부분의 Azure 응용 프로그램은 개인 부하 분산 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="12f14-351">응용 프로그램에 대 한 액세스 tooSQL 서버 hello 인터넷을 통해 직접 필요한 경우 공용 부하 분산 장치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="12f14-352">**가상 네트워크**: hello hello 가상 컴퓨터 네트워크에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="12f14-353">**서브넷**: hello 가상 컴퓨터와 동일한 서브넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="12f14-354">**개인 IP 주소가**: hello toohello SQL Server FCI 클러스터 네트워크 리소스를 할당 하는 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="12f14-355">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="12f14-356">**리소스 그룹**: 사용 하 여 hello 동일한 가상 컴퓨터와 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="12f14-357">**위치**: 사용 하 여 hello 동일한 가상 컴퓨터와 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="12f14-358">Hello 다음 그림을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="12f14-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="12f14-360">Hello 부하 분산 장치 백 엔드 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="12f14-361">Hello 가상 컴퓨터와 toohello Azure 리소스 그룹을 반환 하 고 hello 새 부하 분산 장치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="12f14-362">Toorefresh hello 뷰를 사용할 수 있습니다 있습니다 hello 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="12f14-363">Hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="12f14-364">Hello 부하 분산 장치 블레이드에서 클릭 **백 엔드 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="12f14-365">클릭 **+ 추가** tooadd 백 엔드 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="12f14-366">Hello 백 엔드 풀에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="12f14-367">**가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="12f14-368">Hello에 **가상 컴퓨터를 선택할** 블레이드에서 클릭 **가용성 집합 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="12f14-369">Hello SQL Server 가상 컴퓨터를 배치 하는 hello 가용성 집합을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="12f14-370">Hello에 **가상 컴퓨터를 선택할** 블레이드에서 클릭 **hello 가상 컴퓨터를 선택할**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="12f14-371">Azure 포털을 가리키도록 다음 그림 hello 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="12f14-373">클릭 **선택** hello에 **가상 컴퓨터를 선택할** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="12f14-374">**확인** 을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="12f14-375">부하 분산 장치 상태 프로브 구성</span><span class="sxs-lookup"><span data-stu-id="12f14-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="12f14-376">Hello 부하 분산 장치 블레이드에서 클릭 **상태 프로브**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="12f14-377">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="12f14-378">Hello에 **추가 상태 프로브** 블레이드에서 <a name="probe"> </a>hello 상태 프로브 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="12f14-379">**이름**: hello 상태 검색에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="12f14-380">**프로토콜**: TCP입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="12f14-381">**포트**: tooan 사용 가능한 TCP 포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="12f14-382">이 포트에는 공개 방화벽 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-382">This port requires an open firewall port.</span></span> <span data-ttu-id="12f14-383">사용 하 여 hello [동일한 포트](#ports) hello 방화벽에서 hello 상태 검색에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="12f14-384">**간격**: 5초입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="12f14-385">**비정상 임계값**: 두 번 연속 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="12f14-386">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="12f14-387">부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="12f14-387">Set load balancing rules</span></span>

1. <span data-ttu-id="12f14-388">Hello 부하 분산 장치 블레이드에서 클릭 **부하 분산 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="12f14-389">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="12f14-390">Hello 부하 분산 규칙 매개 변수 설정:</span><span class="sxs-lookup"><span data-stu-id="12f14-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="12f14-391">**이름**: hello 부하 분산 규칙에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="12f14-392">**프런트 엔드 IP 주소**: hello SQL Server FCI의 클러스터 네트워크 리소스에 대 한 hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="12f14-393">**포트**: hello SQL Server FCI TCP 포트에 대해 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="12f14-394">hello 기본 인스턴스가 포트는 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="12f14-395">**백 엔드 포트가**:이 값이 동일한 포트 hello를 사용 하 여 hello로 **포트** 사용 하도록 설정 하면 값 **부동 IP (직접 서버 반환)**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="12f14-396">**백 엔드 풀**: 이전에 구성 된 사용 하 여 hello 백 엔드 풀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="12f14-397">**상태 프로브**: 이전에 구성 된 사용 하 여 hello 상태 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="12f14-398">**세션 지속성**: 없음.</span><span class="sxs-lookup"><span data-stu-id="12f14-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="12f14-399">**유휴 제한 시간(분)**: 4.</span><span class="sxs-lookup"><span data-stu-id="12f14-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="12f14-400">**부동 IP(Direct Server Return)**: 사용</span><span class="sxs-lookup"><span data-stu-id="12f14-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="12f14-401">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="12f14-402">6단계: 프로브에 대한 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="12f14-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="12f14-403">PowerShell에서 hello 클러스터 프로브 포트 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="12f14-404">tooset hello 클러스터 프로브 포트 매개 변수, 사용자 환경에서 스크립트를 다음 hello에서 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="12f14-405">7단계: FCI 장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="12f14-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="12f14-406">장애 조치의 hello FCI toovalidate 클러스터 기능을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="12f14-407">다음 단계 hello 마십시오.</span><span class="sxs-lookup"><span data-stu-id="12f14-407">Do hello following steps:</span></span>

1. <span data-ttu-id="12f14-408">RDP tooone hello SQL Server FCI의 클러스터 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="12f14-409">**장애 조치(Failover) 클러스터 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="12f14-410">**역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-410">Click **Roles**.</span></span> <span data-ttu-id="12f14-411">Hello SQL Server FCI 역할을 소유 하는 노드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="12f14-412">Hello SQL Server FCI 역할을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="12f14-413">**이동**을 클릭하고 **가장 적합한 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="12f14-414">**장애 조치 클러스터 관리자** 표시 hello 역할 및 리소스를 오프 라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="12f14-415">hello 리소스 이동 하 고 온라인 상태로 전환에 다른 노드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="12f14-416">연결 테스트</span><span class="sxs-lookup"><span data-stu-id="12f14-416">Test connectivity</span></span>

<span data-ttu-id="12f14-417">tootest 연결, 로그 hello에 tooanother 가상 컴퓨터에 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="12f14-418">열기 **SQL Server Management Studio** toohello SQL Server FCI 이름을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="12f14-419">필요한 경우 [SQL Server Management Studio를 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="12f14-420">제한 사항</span><span class="sxs-lookup"><span data-stu-id="12f14-420">Limitations</span></span>
<span data-ttu-id="12f14-421">Azure 가상 컴퓨터에 Microsoft Distributed Transaction Coordinator (DTC)는 hello RPC 포트 hello 부하 분산 장치에서 지원 되지 않으므로 Fci에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12f14-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="12f14-422">참고 항목</span><span class="sxs-lookup"><span data-stu-id="12f14-422">See Also</span></span>

[<span data-ttu-id="12f14-423">원격 데스크톱(Azure)을 사용하여 S2D 설치</span><span class="sxs-lookup"><span data-stu-id="12f14-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="12f14-424">[저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)</span><span class="sxs-lookup"><span data-stu-id="12f14-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="12f14-425">저장소 공간 다이렉트 개요</span><span class="sxs-lookup"><span data-stu-id="12f14-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="12f14-426">S2D에 대한 SQL Server 지원</span><span class="sxs-lookup"><span data-stu-id="12f14-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
