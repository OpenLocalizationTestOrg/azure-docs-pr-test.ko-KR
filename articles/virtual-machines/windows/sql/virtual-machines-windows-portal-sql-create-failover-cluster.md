---
title: SQL Server FCI - Azure Virtual Machines | Microsoft Docs
description: "이 문서에서는 Azure Virtual Machines에 SQL Server 장애 조치(Failover) 클러스터 인스턴스를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="dab7a-103">Azure Virtual Machines에 SQL Server 장애 조치(Failover) 클러스터 인스턴스 구성</span><span class="sxs-lookup"><span data-stu-id="dab7a-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="dab7a-104">이 문서에서는 리소스 관리자 모델에서 Azure 가상 컴퓨터에 SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="dab7a-105">이 솔루션에서는 Windows 클러스터에서 노드(Azure VM) 간 저장소(데이터 디스크)를 동기화하는 소프트웨어 기반 가상 SAN으로 [Windows Server 2016 Datacenter 버전 저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="dab7a-106">S2D는 Windows Server 2016의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="dab7a-107">다음 다이어그램에서는 Azure 가상 컴퓨터에 완전한 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="dab7a-109">위의 다이어그램은 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="dab7a-110">Windows 장애 조치(Failover) 클러스터에 있는 두 개의 Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="dab7a-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="dab7a-111">가상 컴퓨터가 장애 조치 클러스터에 있는 경우 *클러스터 노드* 또는 *노드*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="dab7a-112">각 가상 컴퓨터에는 두 개 이상의 데이터 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="dab7a-113">S2D는 데이터 디스크의 데이터를 동기화하고 저장소 풀로 동기화된 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="dab7a-114">저장소 풀은 장애 조치 클러스터에 CSV(클러스터 공유 볼륨)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="dab7a-115">SQL Server FCI 클러스터 역할은 데이터 드라이브에 CSV를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="dab7a-116">SQL Server FCI에 대한 IP 주소를 저장하는 Azure 부하 분산 장치.</span><span class="sxs-lookup"><span data-stu-id="dab7a-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="dab7a-117">Azure 가용성 집합은 모든 리소스를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dab7a-118">다이어그램의 모든 Azure 리소스는 동일한 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="dab7a-119">S2D에 대한 자세한 내용은 [Windows Server 2016 Datacenter 버전 저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="dab7a-120">S2D는 두 가지 유형의 아키텍처 수렴형 및 하이퍼 수렴형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="dab7a-121">이 문서의 아키텍처는 하이퍼 수렴형입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="dab7a-122">하이퍼 수렴형 인프라는 클러스터형 응용 프로그램을 호스트하는 동일한 서버에 저장소를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="dab7a-123">이 아키텍처에서 저장소는 각 SQL Server FCI 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="dab7a-124">예제 Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="dab7a-124">Example Azure template</span></span>

<span data-ttu-id="dab7a-125">템플릿에서 Azure에 전체 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="dab7a-126">템플릿의 예제는 GitHub [Azure 빠른 시작 템플릿](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="dab7a-127">이 예제는 특정 작업에 대해 설계되거나 테스트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="dab7a-128">템플릿을 실행하여 도메인에 연결된 S2D 저장소를 사용하여 SQL Server FCI를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="dab7a-129">템플릿을 평가하고 용도에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dab7a-130">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="dab7a-130">Before you begin</span></span>

<span data-ttu-id="dab7a-131">진행하기 전에 알아야 할 몇 가지 사항이 있으며 준비해야 할 몇 가지 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="dab7a-132">알아야 할 사항</span><span class="sxs-lookup"><span data-stu-id="dab7a-132">What to know</span></span>
<span data-ttu-id="dab7a-133">다음 기술의 작동을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="dab7a-134">Windows 클러스터 기술</span><span class="sxs-lookup"><span data-stu-id="dab7a-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="dab7a-135">[SQL Server 장애 조치(Failover) 클러스터 인스턴스](http://msdn.microsoft.com/library/ms189134.aspx)</span><span class="sxs-lookup"><span data-stu-id="dab7a-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="dab7a-136">또한 다음 기술에 대한 기본적인 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="dab7a-137">Windows Server 2016의 저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션</span><span class="sxs-lookup"><span data-stu-id="dab7a-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="dab7a-138">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="dab7a-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="dab7a-139">가지고 있어야 할 사항</span><span class="sxs-lookup"><span data-stu-id="dab7a-139">What to have</span></span>

<span data-ttu-id="dab7a-140">이 문서의 지침을 수행하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="dab7a-141">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="dab7a-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="dab7a-142">Azure 가상 컴퓨터의 Windows 도메인</span><span class="sxs-lookup"><span data-stu-id="dab7a-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="dab7a-143">Azure 가상 컴퓨터에 개체를 만들 수 있는 권한이 있는 계정</span><span class="sxs-lookup"><span data-stu-id="dab7a-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="dab7a-144">다음 구성 요소에 대한 충분한 IP 주소 공간이 있는 Azure 가상 네트워크 및 서브넷</span><span class="sxs-lookup"><span data-stu-id="dab7a-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="dab7a-145">두 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="dab7a-145">Both virtual machines.</span></span>
   - <span data-ttu-id="dab7a-146">장애 조치 클러스터 IP 주소</span><span class="sxs-lookup"><span data-stu-id="dab7a-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="dab7a-147">각 FCI에 대한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="dab7a-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="dab7a-148">도메인 컨트롤러를 가리키는 Azure 네트워크에 구성된 DNS</span><span class="sxs-lookup"><span data-stu-id="dab7a-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="dab7a-149">이러한 필수 구성 요소가 준비되면 장애 조치 클러스터 빌드를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="dab7a-150">첫 번째 단계는 가상 컴퓨터를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="dab7a-151">1단계: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="dab7a-152">사용자의 구독으로 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="dab7a-153">[Azure 가용성 집합을 만듭니다](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="dab7a-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="dab7a-154">가용성 집합은 장애 도메인 및 업데이트 도메인에 대해 가상 컴퓨터를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="dab7a-155">가용성 집합을 사용하면 응용 프로그램은 네트워크 스위치 또는 서버 랙의 전원 장치와 같은 단일 지점의 오류에 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="dab7a-156">가상 컴퓨터에 대한 리소스 그룹을 만들지 않은 경우 Azure 가용성 집합을 만들 때 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="dab7a-157">가용성 집합을 만드는 데 Azure Portal을 사용하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="dab7a-158">Azure Portal에서 **+**를 클릭하여 Azure Marketplace를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="dab7a-159">**가용성 집합**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="dab7a-160">**가용성 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="dab7a-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-161">Click **Create**.</span></span>
   - <span data-ttu-id="dab7a-162">**가용성 집합 만들기** 블레이드에서 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="dab7a-163">**이름**: 가용성 집합에 대한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="dab7a-164">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="dab7a-165">**리소스 그룹**: 기존 그룹을 사용하려는 경우 **기존 항목 사용**을 클릭하고 드롭다운 목록에서 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="dab7a-166">그렇지 않으면 **새로 만들기**를 선택하고 그룹에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="dab7a-167">**위치**: 가상 컴퓨터를 만들 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="dab7a-168">**장애 도메인**: 기본 (3)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="dab7a-169">**업데이트 도메인**: 기본 (5)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="dab7a-170">**만들기**를 클릭하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="dab7a-171">가용성 집합에 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="dab7a-172">Azure 가용성 집합에서 두 개의 SQL Server 가상 컴퓨터를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="dab7a-173">지침은 [Azure Portal에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="dab7a-174">두 가상 컴퓨터를 다음에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="dab7a-175">가용성 집합이 있는 동일한 Azure 리소스 그룹에.</span><span class="sxs-lookup"><span data-stu-id="dab7a-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="dab7a-176">도메인 컨트롤러와 동일한 네트워크에.</span><span class="sxs-lookup"><span data-stu-id="dab7a-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="dab7a-177">두 가상 컴퓨터에 대한 충분한 IP 주소 공간이 있는 서브넷 및 이 클러스터에서 사용할 수 있는 모든 FCI에.</span><span class="sxs-lookup"><span data-stu-id="dab7a-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="dab7a-178">Azure 가용성 집합에.</span><span class="sxs-lookup"><span data-stu-id="dab7a-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="dab7a-179">가상 컴퓨터를 만든 후에 가용성 집합을 설정 또는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="dab7a-180">Azure Marketplace에서 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="dab7a-181">Windows Server 및 SQL Server 또는 Windows Server만 포함하는 Marketplace 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="dab7a-182">자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../../virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="dab7a-183">Azure Gallery의 공식 SQL Server 이미지에는 설치된 SQL Server 인스턴스와 SQL Server 설치 소프트웨어 및 필요한 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="dab7a-184">SQL Server 라이선스에 대한 요금을 지불하려는 방법에 따라 올바른 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="dab7a-185">**사용 라이선스당 지불**: 이러한 이미지의 분당 비용은 SQL Server 라이선스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="dab7a-186">**Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="dab7a-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dab7a-187">**Windows Server Datacenter 2016의 SQL Server 2016 Standard**</span><span class="sxs-lookup"><span data-stu-id="dab7a-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dab7a-188">**Windows Server Datacenter 2016의 SQL Server 2016 Developer**</span><span class="sxs-lookup"><span data-stu-id="dab7a-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="dab7a-189">**BYOL(사용자 라이선스 필요)**</span><span class="sxs-lookup"><span data-stu-id="dab7a-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="dab7a-190">**{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="dab7a-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dab7a-191">**{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Standard**</span><span class="sxs-lookup"><span data-stu-id="dab7a-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="dab7a-192">가상 컴퓨터를 만든 후에 사전 설치된 독립 실행형 SQL Server 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="dab7a-193">장애 조치 클러스터 및 S2D를 구성한 후 사전 설치된 SQL Server 미디어를 사용하여 SQL Server FCI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="dab7a-194">또는 운영 체제와 함께 Azure Marketplace 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="dab7a-195">**Windows Server 2016 Datacenter** 이미지를 선택하고 장애 조치 클러스터와 S2D를 구성한 후 SQL Server FCI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="dab7a-196">이 이미지는 SQL Server 설치 이미지를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="dab7a-197">각 서버에 대한 SQL Server 설치를 실행할 수 있는 위치에 설치 미디어를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="dab7a-198">Azure에서 가상 컴퓨터를 만든 후에 RDP로 각 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="dab7a-199">RDP로 가상 컴퓨터에 처음 연결하면 컴퓨터는 이 PC를 네트워크에서 검색할 수 있도록 허용하는지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="dab7a-200">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-200">Click **Yes**.</span></span>

1. <span data-ttu-id="dab7a-201">SQL Server 기반 가상 컴퓨터 이미지 중 하나를 사용하고 있는 경우 SQL Server 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="dab7a-202">**프로그램 및 기능**에서 **Microsoft SQL Server 2016(64비트)**을 마우스 오른쪽 단추로 클릭하고 **제거/변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="dab7a-203">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-203">Click **Remove**.</span></span>
   - <span data-ttu-id="dab7a-204">기본 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-204">Select the default instance.</span></span>
   - <span data-ttu-id="dab7a-205">**데이터베이스 엔진 서비스**에서 모든 기능을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="dab7a-206">**공유 기능**을 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="dab7a-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="dab7a-207">다음 그림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-207">See the following picture:</span></span>

      ![기능 제거](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="dab7a-209">**다음**을 클릭한 후 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="dab7a-210"><a name="ports"></a>방화벽 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="dab7a-211">각 가상 컴퓨터에서 Windows 방화벽의 다음 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="dab7a-212">목적</span><span class="sxs-lookup"><span data-stu-id="dab7a-212">Purpose</span></span> | <span data-ttu-id="dab7a-213">TCP 포트</span><span class="sxs-lookup"><span data-stu-id="dab7a-213">TCP Port</span></span> | <span data-ttu-id="dab7a-214">참고</span><span class="sxs-lookup"><span data-stu-id="dab7a-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="dab7a-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dab7a-215">SQL Server</span></span> | <span data-ttu-id="dab7a-216">1433</span><span class="sxs-lookup"><span data-stu-id="dab7a-216">1433</span></span> | <span data-ttu-id="dab7a-217">SQL Server의 기본 인스턴스에 대한 표준 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="dab7a-218">갤러리에서 이미지를 사용한 경우 이 포트는 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="dab7a-219">상태 프로브</span><span class="sxs-lookup"><span data-stu-id="dab7a-219">Health probe</span></span> | <span data-ttu-id="dab7a-220">59999</span><span class="sxs-lookup"><span data-stu-id="dab7a-220">59999</span></span> | <span data-ttu-id="dab7a-221">모든 공개 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-221">Any open TCP port.</span></span> <span data-ttu-id="dab7a-222">이후 단계에서 이 포트를 사용하려면 부하 분산 장치 [상태 프로브](#probe) 및 클러스터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="dab7a-223">가상 컴퓨터에 저장소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="dab7a-224">자세한 내용은 [저장소 추가](../../../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="dab7a-225">두 가상 컴퓨터에 두 개 이상의 데이터 디스크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="dab7a-226">NTFS 포맷 디스크가 아닌 원시 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="dab7a-227">NTFS 포맷 디스크를 연결하는 경우 디스크 자격 확인 없이 S2D를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="dab7a-228">각 VM에 최소 두 개의 Premium Storage(SSD 디스크)를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="dab7a-229">적어도 P30(1TB) 디스크가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="dab7a-230">호스트 캐싱을 **읽기 전용**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="dab7a-231">프로덕션 환경에서 사용하는 저장소 용량은 작업에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="dab7a-232">이 문서에서 설명하는 값은 데모 및 테스트용입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="dab7a-233">[기존 도메인에 가상 컴퓨터를 추가합니다](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="dab7a-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="dab7a-234">가상 컴퓨터를 만들고 구성한 후에 장애 조치 클러스터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="dab7a-235">2단계: S2D로 Windows 장애 조치(Failover) 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="dab7a-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="dab7a-236">다음 단계는 S2D로 장애 조치 클러스터를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="dab7a-237">이 단계에서는 다음 하위 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="dab7a-238">Windows 장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="dab7a-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="dab7a-239">클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="dab7a-239">Validate the cluster</span></span>
1. <span data-ttu-id="dab7a-240">장애 조치 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-240">Create the failover cluster</span></span>
1. <span data-ttu-id="dab7a-241">클라우드 감시 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-241">Create the cloud witness</span></span>
1. <span data-ttu-id="dab7a-242">저장소 추가</span><span class="sxs-lookup"><span data-stu-id="dab7a-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="dab7a-243">Windows 장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="dab7a-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="dab7a-244">시작하려면 로컬 관리자의 구성원이며 Active Directory에 개체를 만들 수 있는 권한이 있는 도메인 계정을 사용하여 RDP로 첫 번째 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="dab7a-245">구성의 나머지 부분에서는 이 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="dab7a-246">[장애 조치(Failover) 클러스터링 기능을 각 가상 컴퓨터에 추가합니다](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="dab7a-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="dab7a-247">UI에서 장애 조치(Failover) 클러스터링 기능을 설치하려면 두 가상 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="dab7a-248">**서버 관리자**에서 **관리**를 클릭한 다음 **역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="dab7a-249">**역할 및 기능 추가 마법사**에서 **기능 선택**이 표시될 때까지 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="dab7a-250">**기능 선택**에서 **장애 조치(Failover) 클러스터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="dab7a-251">필요한 모든 기능 및 관리 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-251">Include all required features and the management tools.</span></span> <span data-ttu-id="dab7a-252">**기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="dab7a-253">**다음**을 클릭한 다음 **마침**을 클릭하여 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="dab7a-254">PowerShell로 장애 조치(Failover) 클러스터링 기능을 설치하려면 가상 컴퓨터 중 하나의 관리자 PowerShell 세션에서 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="dab7a-255">참고로 다음 단계는 [Windows Server 2016의 저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct)의 3단계 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="dab7a-256">클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="dab7a-256">Validate the cluster</span></span>

<span data-ttu-id="dab7a-257">이 가이드는 [클러스터 유효성 검사](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)의 지침을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="dab7a-258">UI에서 또는 PowerShell을 사용하여 클러스터의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="dab7a-259">UI를 사용하여 클러스터의 유효성을 검사하려면 가상 컴퓨터 중 하나에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="dab7a-260">**서버 관리자**에서 **도구**를 클릭한 다음 **장애 조치(Failover) 클러스터 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="dab7a-261">**장애 조치(Failover) 클러스터 관리자**에서 **작업**을 클릭한 다음 **구성 유효성 검사...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="dab7a-262">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-262">Click **Next**.</span></span>
1. <span data-ttu-id="dab7a-263">**서버 또는 클러스터 선택**에서 두 가상 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="dab7a-264">**테스트 옵션**에서 **선택한 테스트만 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="dab7a-265">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-265">Click **Next**.</span></span>
1. <span data-ttu-id="dab7a-266">**테스트 선택**에서 **저장소**를 제외한 모든 테스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="dab7a-267">다음 그림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-267">See the following picture:</span></span>

   ![유효성 검사 테스트](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="dab7a-269">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-269">Click **Next**.</span></span>
1. <span data-ttu-id="dab7a-270">**확인**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="dab7a-271">**구성 유효성 검사 마법사**가 유효성 검사 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="dab7a-272">PowerShell로 클러스터의 유효성을 검사하려면 가상 컴퓨터 중 하나의 관리자 PowerShell 세션에서 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="dab7a-273">클러스터의 유효성을 검사한 후에 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="dab7a-274">장애 조치 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-274">Create the failover cluster</span></span>

<span data-ttu-id="dab7a-275">이 가이드에서는 [장애 조치 클러스터 만들기](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="dab7a-276">장애 조치 클러스터를 만들려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="dab7a-277">클러스터 노드가 되는 가상 컴퓨터의 이름.</span><span class="sxs-lookup"><span data-stu-id="dab7a-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="dab7a-278">장애 조치 클러스터의 이름</span><span class="sxs-lookup"><span data-stu-id="dab7a-278">A name for the failover cluster</span></span>
- <span data-ttu-id="dab7a-279">장애 조치 클러스터의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="dab7a-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="dab7a-280">클러스터 노드와 동일한 Azure 가상 네트워크 및 서브넷에 사용되지 않는 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="dab7a-281">다음 PowerShell은 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="dab7a-282">스크립트를 노드의 이름(가상 컴퓨터 이름) 및 Azure VNET에서 사용 가능한 IP 주소 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="dab7a-283">클라우드 감시 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-283">Create a cloud witness</span></span>

<span data-ttu-id="dab7a-284">클라우드 감시는 Azure Storage Blob에 저장된 새로운 유형의 클러스터 쿼럼 감시입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="dab7a-285">감시 공유를 호스트하는 별도 VM의 필요성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="dab7a-286">[장애 조치 클러스터에 대한 클라우드 감시를 만듭니다](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="dab7a-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="dab7a-287">Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-287">Create a blob container.</span></span>

1. <span data-ttu-id="dab7a-288">액세스 키 및 컨테이너 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="dab7a-289">장애 조치 클러스터에 대한 클러스터 쿼럼 감시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="dab7a-290">UI에서 [사용자 인터페이스에서 쿼럼 감시 구성](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="dab7a-291">저장소 추가</span><span class="sxs-lookup"><span data-stu-id="dab7a-291">Add storage</span></span>

<span data-ttu-id="dab7a-292">S2D용 디스크는 비어 있고 파티션 또는 기타 데이터가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="dab7a-293">디스크를 정리하려면 [이 가이드의 단계](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="dab7a-294">[저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="dab7a-295">다음 PowerShell은 저장소 공간 다이렉트를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="dab7a-296">**장애 조치(Failover) 클러스터 관리자**에서 이제 저장소 풀을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="dab7a-297">[볼륨을 만듭니다](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="dab7a-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="dab7a-298">S2D의 기능 중 하나는 이를 활성화할 때 저장소 풀을 자동으로 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="dab7a-299">이제 볼륨을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-299">You are now ready to create a volume.</span></span> <span data-ttu-id="dab7a-300">PowerShell commandlet `New-Volume`은 서식 지정, 클러스터에 추가 및 CSV(클러스터 공유 볼륨) 만들기를 포함하는 볼륨 생성 프로세스를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="dab7a-301">다음 예제에서는 800GB(기가바이트) CSV를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="dab7a-302">이 명령이 완료되면 클러스터 리소스로 800GB 볼륨이 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="dab7a-303">볼륨은 `C:\ClusterStorage\Volume1\`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="dab7a-304">다음 다이어그램에서는 S2D로 클러스터 공유 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="dab7a-306">3단계: 장애 조치 클러스터의 장애 조치 테스트</span><span class="sxs-lookup"><span data-stu-id="dab7a-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="dab7a-307">장애 조치(Failover) 클러스터 관리자에서 저장소 리소스를 다른 클러스터 노드로 이동할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="dab7a-308">**장애 조치(Failover) 클러스터 관리자**를 사용하여 장애 조치 클러스터에 연결하고 한 노드에서 다른 노드로 저장소를 이동할 수 있는 경우 이제 FCI를 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="dab7a-309">4단계: SQL Server FCI 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="dab7a-310">장애 조치 클러스터 및 저장소를 포함한 모든 클러스터 구성 요소를 구성한 후 SQL Server FCI를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="dab7a-311">RDP를 사용하여 첫 번째 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="dab7a-312">**장애 조치(Failover) 클러스터 관리자**에서 모든 클러스터 코어 리소스가 첫 번째 가상 컴퓨터에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="dab7a-313">필요한 경우 모든 리소스를 이 가상 컴퓨터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="dab7a-314">설치 미디어를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-314">Locate the installation media.</span></span> <span data-ttu-id="dab7a-315">가상 컴퓨터가 Azure Marketplace 이미지 중 하나를 사용하는 경우 미디어는 `C:\SQLServer_<version number>_Full`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="dab7a-316">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-316">Click **Setup**.</span></span>

1. <span data-ttu-id="dab7a-317">**SQL Server 설치 센터**에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="dab7a-318">**새 SQL Server 장애 조치(failover) 클러스터 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="dab7a-319">마법사의 지침에 따라 SQL Server FCI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="dab7a-320">FCI 데이터 디렉터리는 클러스터형 저장소에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="dab7a-321">S2D를 사용하는 경우 공유 디스크가 아니고 각 서버의 볼륨에 대한 탑재 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="dab7a-322">S2D는 두 노드 간의 볼륨을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="dab7a-323">볼륨은 클러스터 공유 볼륨으로 클러스터에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="dab7a-324">데이터 디렉터리에 CSV 탑재 지점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-324">Use the CSV mount point for the data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="dab7a-326">마법사를 완료한 후 설정은 첫 번째 노드에 SQL Server FCI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="dab7a-327">설정이 첫 번째 노드에 FCI를 성공적으로 설치한 후 RDP를 사용하여 두 번째 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="dab7a-328">**SQL Server 설치 센터**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="dab7a-329">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-329">Click **Installation**.</span></span>

1. <span data-ttu-id="dab7a-330">**SQL Server 장애 조치(failover) 클러스터에 노드 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="dab7a-331">마법사의 지침에 따라 SQL Server를 설치하고 이 서버를 FCI에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dab7a-332">SQL Server와 함께 Azure Marketplace 갤러리 이미지를 사용한 경우 SQL Server 도구는 이미지에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="dab7a-333">이 이미지를 사용하지 않은 경우 SQL Server 도구를 개별적으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="dab7a-334">[SSMS(SQL Server Management Studio) 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="dab7a-335">5단계: Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="dab7a-336">Azure 가상 컴퓨터에서 클러스터는 한 번에 하나의 클러스터 노드에 있어야 하는 IP 주소를 저장하는 부하 분산 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="dab7a-337">이 솔루션에서 부하 분산 장치는 SQL Server FCI에 대한 IP 주소를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="dab7a-338">[Azure Load Balancer를 만들고 구성합니다](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="dab7a-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="dab7a-339">Azure Portal에서 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="dab7a-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="dab7a-340">부하 분산 장치를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="dab7a-340">To create the load balancer:</span></span>

1. <span data-ttu-id="dab7a-341">Azure Portal에서 가상 컴퓨터를 사용하여 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="dab7a-342">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-342">Click **+ Add**.</span></span> <span data-ttu-id="dab7a-343">**부하 분산 장치**에 대한 Marketplace를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="dab7a-344">**부하 분산 장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="dab7a-345">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-345">Click **Create**.</span></span>

1. <span data-ttu-id="dab7a-346">다음으로 부하 분산 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="dab7a-347">**이름**: 부하 분산 장치를 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="dab7a-348">**형식**: 부하 분산 장치는 공개 또는 개인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="dab7a-349">동일한 VNET 내에서 개인 부하 분산 장치에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="dab7a-350">대부분의 Azure 응용 프로그램은 개인 부하 분산 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="dab7a-351">응용 프로그램에 인터넷을 통해 직접 SQL Server에 대한 액세스가 필요한 경우 공개 부하 분산 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="dab7a-352">**가상 네트워크**: 가상 컴퓨터와 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="dab7a-353">**서브넷**: 가상 컴퓨터와 동일한 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="dab7a-354">**개인 IP 주소**: SQL Server FCI 클러스터 네트워크 리소스에 할당한 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="dab7a-355">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="dab7a-356">**리소스 그룹**: 가상 컴퓨터와 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="dab7a-357">**위치**: 가상 컴퓨터와 동일한 Azure 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="dab7a-358">다음 그림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dab7a-358">See the following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="dab7a-360">부하 분산 장치 백 엔드 풀 구성</span><span class="sxs-lookup"><span data-stu-id="dab7a-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="dab7a-361">가상 컴퓨터를 사용하여 Azure 리소스 그룹으로 돌아가고 새 부하 분산 장치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="dab7a-362">리소스 그룹의 보기를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="dab7a-363">부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-363">Click the load balancer.</span></span>

1. <span data-ttu-id="dab7a-364">부하 분산 장치 블레이드에서 **백 엔드 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="dab7a-365">**+ 추가**를 클릭하여 백 엔드 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="dab7a-366">백 엔드 풀의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="dab7a-367">**가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="dab7a-368">**가상 컴퓨터 선택** 블레이드에서 **가용성 집합 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="dab7a-369">SQL Server 가상 컴퓨터를 배치한 가용성 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="dab7a-370">**가상 컴퓨터 선택** 블레이드에서 **가상 컴퓨터 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="dab7a-371">Azure Portal은 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="dab7a-373">**가상 컴퓨터 선택** 블레이드에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="dab7a-374">**확인** 을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="dab7a-375">부하 분산 장치 상태 프로브 구성</span><span class="sxs-lookup"><span data-stu-id="dab7a-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="dab7a-376">부하 분산 장치 블레이드에서 **상태 프로브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="dab7a-377">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="dab7a-378">**상태 프로브 추가** 블레이드에서 <a name="probe"></a>상태 프로브 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="dab7a-379">**이름**: 상태 프로브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="dab7a-380">**프로토콜**: TCP입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="dab7a-381">**포트**: 사용 가능한 TCP 포트로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="dab7a-382">이 포트에는 공개 방화벽 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-382">This port requires an open firewall port.</span></span> <span data-ttu-id="dab7a-383">방화벽에서 상태 프로브에 대해 설정한 [동일한 포트](#ports)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="dab7a-384">**간격**: 5초입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="dab7a-385">**비정상 임계값**: 두 번 연속 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="dab7a-386">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="dab7a-387">부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="dab7a-387">Set load balancing rules</span></span>

1. <span data-ttu-id="dab7a-388">부하 분산 장치 블레이드에서 **부하 분산 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="dab7a-389">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="dab7a-390">부하 분산 규칙 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="dab7a-391">**이름**: 부하 분산 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="dab7a-392">**프런트 엔드 IP 주소**: SQL Server FCI 클러스터 네트워크 리소스에 대한 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="dab7a-393">**포트**: SQL Server FCI TCP 포트에 대해 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="dab7a-394">기본 인스턴스 포트는 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="dab7a-395">**백 엔드 포트**: 이 값은 **부동 IP(Direct Server Return)**를 활성화할 때 **포트** 값과 동일한 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="dab7a-396">**백 엔드 풀**: 이전에 구성한 백 엔드 풀 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="dab7a-397">**상태 프로브**: 이전에 구성한 상태 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="dab7a-398">**세션 지속성**: 없음.</span><span class="sxs-lookup"><span data-stu-id="dab7a-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="dab7a-399">**유휴 제한 시간(분)**: 4.</span><span class="sxs-lookup"><span data-stu-id="dab7a-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="dab7a-400">**부동 IP(Direct Server Return)**: 사용</span><span class="sxs-lookup"><span data-stu-id="dab7a-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="dab7a-401">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="dab7a-402">6단계: 프로브에 대한 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="dab7a-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="dab7a-403">PowerShell에서 클러스터 프로브 포트 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="dab7a-404">클러스터 프로브 포트 매개 변수를 설정하려면 사용자 환경에서 다음 스크립트의 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="dab7a-405">7단계: FCI 장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="dab7a-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="dab7a-406">FCI의 장애 조치(failover)를 테스트하여 클러스터 기능의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="dab7a-407">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-407">Do the following steps:</span></span>

1. <span data-ttu-id="dab7a-408">RDP를 사용하여 SQL Server FCI 클러스터 노드 중 하나에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="dab7a-409">**장애 조치(Failover) 클러스터 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="dab7a-410">**역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-410">Click **Roles**.</span></span> <span data-ttu-id="dab7a-411">SQL Server FCI 역할을 소유하는 노드를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="dab7a-412">SQL Server FCI 역할을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="dab7a-413">**이동**을 클릭하고 **가장 적합한 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="dab7a-414">**장애 조치(Failover) 클러스터 관리자**는 역할을 보여 주고 해당 리소스는 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="dab7a-415">그런 다음 리소스는 이동하고 다른 노드에서 온라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="dab7a-416">연결 테스트</span><span class="sxs-lookup"><span data-stu-id="dab7a-416">Test connectivity</span></span>

<span data-ttu-id="dab7a-417">연결을 테스트하려면 동일한 가상 네트워크의 다른 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="dab7a-418">**SQL Server Management Studio**를 열고 SQL Server FCI 이름에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="dab7a-419">필요한 경우 [SQL Server Management Studio를 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="dab7a-420">제한 사항</span><span class="sxs-lookup"><span data-stu-id="dab7a-420">Limitations</span></span>
<span data-ttu-id="dab7a-421">Azure 가상 컴퓨터에서 RPC 포트는 부하 분산 장치에서 지원되지 않으므로 Microsoft DTC(Distributed Transaction Coordinator)는 FCI에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dab7a-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="dab7a-422">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dab7a-422">See Also</span></span>

[<span data-ttu-id="dab7a-423">원격 데스크톱(Azure)을 사용하여 S2D 설치</span><span class="sxs-lookup"><span data-stu-id="dab7a-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="dab7a-424">[저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)</span><span class="sxs-lookup"><span data-stu-id="dab7a-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="dab7a-425">저장소 공간 다이렉트 개요</span><span class="sxs-lookup"><span data-stu-id="dab7a-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="dab7a-426">S2D에 대한 SQL Server 지원</span><span class="sxs-lookup"><span data-stu-id="dab7a-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
