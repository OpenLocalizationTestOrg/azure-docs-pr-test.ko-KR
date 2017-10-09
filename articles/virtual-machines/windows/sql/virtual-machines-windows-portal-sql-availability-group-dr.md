---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-재해 복구 aaaSQL | Microsoft Docs"
description: "이 문서는 다른 지역에 복제 데이터베이스와 Azure 가상 컴퓨터에 SQL Server 가용성 tooconfigure 그룹화 하는 방법을 설명 합니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="02dea-103">다른 하위 지역의 Azure Virtual Machines에서 Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="02dea-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="02dea-104">이 문서에서는 tooconfigure SQL Server Always On 가용성 복제본 원격 Azure 위치에 Azure 가상 컴퓨터에 그룹화 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="02dea-105">이 구성 toosupport 재해 복구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="02dea-106">이 문서에는 리소스 관리자 모드에서 가상 컴퓨터 tooAzure 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="02dea-107">hello 다음 이미지는 가용성 그룹의 일반적인 배포 Azure 가상 컴퓨터에</span><span class="sxs-lookup"><span data-stu-id="02dea-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="02dea-109">이 배포에서 모든 가상 컴퓨터는 하나의 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="02dea-110">hello 가용성 그룹 복제본이 동기 커밋 SQL-1과 2 SQL에서 자동 장애 조치를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="02dea-111">toobuild이이 아키텍처 참조 [가용성 그룹 템플릿 또는 자습서](virtual-machines-windows-portal-sql-availability-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="02dea-112">이 아키텍처 취약 toodowntime 이면 hello Azure 지역에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="02dea-113">tooovercome이이 취약점 다른 Azure 지역에서 복제본을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="02dea-114">hello 다음 다이어그램 모양을 보여 줍니다 hello 새로운 아키텍처:</span><span class="sxs-lookup"><span data-stu-id="02dea-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![가용성 그룹 DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="02dea-116">hello 이전 다이어그램에서는 SQL 3 라는 새 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="02dea-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="02dea-117">SQL-3는 다른 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="02dea-118">SQL 3 toohello Windows Server 장애 조치 클러스터에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="02dea-119">SQL-3는 가용성 그룹 복제본을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="02dea-120">마지막으로, 해당 hello SQL 3에 대 한 Azure 지역에 새 Azure 부하 분산 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="02dea-121">Azure 가용성 집합은 동일한 지역 hello 가상 컴퓨터가 하나 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="02dea-122">경우에 하나의 가상 컴퓨터에 hello 지역에 있으면 hello 가용성 집합에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="02dea-123">생성 시 가용성 집합에 하나의 가상 컴퓨터만 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="02dea-124">Hello 가상 컴퓨터 가용성 집합에 이미 있으면 추가 나중에 복제본 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="02dea-125">이 아키텍처에서 비동기 커밋 가용성 모드와 수동 장애 조치 모드 hello 원격 영역의 hello 복제본 일반적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="02dea-126">가용성 그룹 복제본이 다른 Azure 지역의 Azure Virtual Machines에 있는 경우에 각 지역에 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="02dea-127">가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="02dea-127">A virtual network gateway</span></span>
* <span data-ttu-id="02dea-128">가상 네트워크 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="02dea-128">A virtual network gateway connection</span></span>

<span data-ttu-id="02dea-129">hello 다음 다이어그램에서는 데이터 센터 간에 hello 네트워크 통신 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="02dea-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="02dea-131">이 아키텍처에서는 Azure 지역 간에 복제되는 데이터에 대해 아웃바운드 데이터 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="02dea-132">[대역폭 가격 책정](http://azure.microsoft.com/pricing/details/bandwidth/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dea-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="02dea-133">원격 복제본 만들기</span><span class="sxs-lookup"><span data-stu-id="02dea-133">Create remote replica</span></span>

<span data-ttu-id="02dea-134">다음 단계는 원격 데이터 센터로의 복제 toocreate hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="02dea-135">[Hello 새 영역에서 가상 네트워크 만들기](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="02dea-136">[Hello Azure 포털을 사용 하 여 VNet 대 VNet 연결 구성](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="02dea-137">경우에 따라 toouse PowerShell toocreate hello VNet 대 VNet 연결을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="02dea-138">예를 들어 서로 다른 Azure 계정을 사용 하는 경우 hello 연결 hello 포털에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="02dea-139">이 경우 참조 [Azure 포털 hello 사용 하 여 구성 VNet 대 VNet 연결](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="02dea-140">[Hello 새 영역에서 도메인 컨트롤러 만들기](../../../active-directory/active-directory-new-forest-virtual-machine.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="02dea-141">이 도메인 컨트롤러는 hello 기본 사이트의 hello 도메인 컨트롤러를 사용할 수 없는 경우 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="02dea-142">[Hello 새 영역에는 SQL Server 가상 컴퓨터를 만들](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="02dea-143">[Hello 새 영역에 hello 네트워크에는 Azure 부하 분산 장치를 만듭니다](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="02dea-144">이 부하 분산 장치는 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-144">This load balancer must:</span></span>

   - <span data-ttu-id="02dea-145">에 새 가상 컴퓨터를 hello 처럼 동일한 네트워크 및 서브넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="02dea-146">Hello 가용성 그룹 수신기에 대 한 고정 IP 주소를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="02dea-147">Hello 가상 컴퓨터 부하 분산 장치 hello으로 같은 지역 hello만 이루어진 백 엔드 풀을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="02dea-148">TCP 포트 프로브 toohello 특정 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="02dea-149">부하 분산 규칙 특정 toohello hello에서 만든 SQL Server가 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="02dea-150">[장애 조치 클러스터링 기능 toohello 추가 새 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="02dea-151">[Hello 새 SQL Server toohello 도메인 가입](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="02dea-152">[도메인 계정 hello 새 SQL Server 서비스 계정 toouse 설정](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="02dea-153">[Hello 새 SQL Server toohello Windows Server 장애 조치 클러스터를 추가](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="02dea-154">Hello 클러스터 IP 주소 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="02dea-155">장애 조치 클러스터 관리자에서 hello IP 주소 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="02dea-156">Hello 가용성 그룹 역할을 마우스 오른쪽 단추로 클릭 하 여, **리소스 추가**, **더 리소스**를 클릭 하 고 **IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![IP 주소 만들기](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="02dea-158">이 IP 주소를 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="02dea-159">Hello 네트워크를 사용 하 여 hello 원격 데이터 센터에서.</span><span class="sxs-lookup"><span data-stu-id="02dea-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="02dea-160">Hello 새 Azure 부하 분산 장치에서 hello IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="02dea-161">새 SQL Server SQL Server 구성 관리자에서 hello [Always On 가용성 그룹을 사용 하도록 설정](http://msdn.microsoft.com/library/ff878259.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="02dea-162">[열기 방화벽 포트를 새 SQL Server hello](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="02dea-163">tooopen 필요한 hello 포트 번호는 사용자 환경에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="02dea-164">열린 포트 미러링 끝점 및 Azure hello에 대 한 부하 분산 장치 상태 프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="02dea-165">[Hello에 복제본 toohello 가용성 그룹을 추가 새 SQL Server](http://msdn.microsoft.com/library/hh213239.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="02dea-166">원격 Azure 지역에 있는 복제본의 경우 수동 장애 조치를 사용한 비동기 복제에 대해 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="02dea-167">Hello 수신기 클라이언트 액세스 지점 (네트워크 이름) 클러스터에 대 한 종속성으로 hello IP 주소 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="02dea-168">hello 다음 스크린샷은 올바르게 구성 된 IP 주소 클러스터 리소스:</span><span class="sxs-lookup"><span data-stu-id="02dea-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="02dea-170">hello 클러스터 리소스 그룹에는 IP 주소가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="02dea-171">IP 주소는 hello 수신기 클라이언트 액세스 지점에 대 한 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="02dea-172">사용 하 여 hello **또는** hello 클러스터 종속성 구성의 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="02dea-173">[PowerShell에서 hello 클러스터 매개 변수를 설정](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="02dea-174">새 영역 hello hello 부하 분산 장치에 구성 된 프로브 포트 hello 클러스터 네트워크 이름, IP 주소와 hello PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="02dea-175">여러 서브넷에 대한 연결 설정</span><span class="sxs-lookup"><span data-stu-id="02dea-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="02dea-176">hello 원격 데이터 센터에 hello 복제본 hello 가용성 그룹의 일부 이지만 다른 서브넷에.</span><span class="sxs-lookup"><span data-stu-id="02dea-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="02dea-177">이 복제본이 주 복제본 hello, 응용 프로그램 연결 제한 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="02dea-178">이 동작은 온-프레미스 가용성 그룹 다중 서브넷 배포에서와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="02dea-179">클라이언트 응용 프로그램에서 tooallow 연결은 hello 클라이언트 연결을 업데이트 하거나 hello 클러스터 네트워크 이름 리소스에 대 한 캐싱을 이름 확인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="02dea-180">가급적 hello 클라이언트 연결 문자열 tooset 업데이트 `MultiSubnetFailover=Yes`합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="02dea-181">[MultiSubnetFailover로 연결](http://msdn.microsoft.com/library/gg471494#Anchor_0)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dea-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="02dea-182">연결 문자열 hello를 수정할 수 없는 경우 이름 확인 캐싱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="02dea-183">[다중 서브넷 가용성 그룹의 연결 시간 제한](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dea-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="02dea-184">장애 조치 tooremote 영역</span><span class="sxs-lookup"><span data-stu-id="02dea-184">Fail over tooremote region</span></span>

<span data-ttu-id="02dea-185">tootest 수신기 연결 toohello 원격 영역 hello 복제본 toohello 원격 지역의 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="02dea-186">Hello 복제본이 비동기 인 동안 장애 조치가 취약 toopotential 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="02dea-187">데이터 손실 없이 통해 toofail hello 가용성 모드 toosynchronous 변경 하 고 장애 조치 모드 tooautomatic hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="02dea-188">단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-188">Use hello following steps:</span></span>

1. <span data-ttu-id="02dea-189">**개체 탐색기**, toohello hello 주 복제본을 호스팅하는 SQL Server 인스턴스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="02dea-190">**Always On 가용성 그룹**, **가용성 그룹** 아래에서 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="02dea-191">Hello에 **일반** 페이지의 **가용성 복제본**, 집합 hello hello DR 사이트 toouse의 보조 복제본 **동기 커밋** 가용성 모드와 **자동** 장애 조치 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="02dea-192">보조 복제본을 고가용성에 대 한 기본 복제 데이터베이스와 같은 사이트에 있을 경우이 복제본에 너무 설정**비동기 커밋** 및 **수동**합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="02dea-193">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-193">Click OK.</span></span>
1. <span data-ttu-id="02dea-194">**개체 탐색기**hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **대시보드 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="02dea-195">Hello 대시보드에서 해당 hello 확인 hello DR 사이트에서 복제본이 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="02dea-196">**개체 탐색기**hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **장애 조치 중...** . SQL Server Management Studio를 통해 SQL Server 마법사 toofail을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="02dea-197">클릭 **다음**, 및 hello DR 사이트에서 SQL Server 인스턴스 선택 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="02dea-198">다시 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-198">Click **Next** again.</span></span>
1. <span data-ttu-id="02dea-199">Hello DR 사이트에서 toohello SQL Server 인스턴스에 연결 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="02dea-200">Hello에 **요약** 페이지 hello 설정을 확인 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="02dea-201">연결 테스트를 마친 후 hello 주 복제본 백 tooyour 주 데이터 센터 및 설정을 hello 가용성 모드 백 tootheir 정상 작동을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dea-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="02dea-202">hello 아래 표에 나와 hello이이 문서에서 설명 하는 hello 아키텍처에 대 한 기본 작업 설정.</span><span class="sxs-lookup"><span data-stu-id="02dea-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="02dea-203">위치</span><span class="sxs-lookup"><span data-stu-id="02dea-203">Location</span></span> | <span data-ttu-id="02dea-204">서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="02dea-204">Server Instance</span></span> | <span data-ttu-id="02dea-205">역할</span><span class="sxs-lookup"><span data-stu-id="02dea-205">Role</span></span> | <span data-ttu-id="02dea-206">가용성 모드</span><span class="sxs-lookup"><span data-stu-id="02dea-206">Availability Mode</span></span> | <span data-ttu-id="02dea-207">장애 조치(Failover) 모드</span><span class="sxs-lookup"><span data-stu-id="02dea-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="02dea-208">주 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="02dea-208">Primary data center</span></span> | <span data-ttu-id="02dea-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="02dea-209">SQL-1</span></span> | <span data-ttu-id="02dea-210">보조</span><span class="sxs-lookup"><span data-stu-id="02dea-210">Primary</span></span> | <span data-ttu-id="02dea-211">동기</span><span class="sxs-lookup"><span data-stu-id="02dea-211">Synchronous</span></span> | <span data-ttu-id="02dea-212">자동</span><span class="sxs-lookup"><span data-stu-id="02dea-212">Automatic</span></span>
| <span data-ttu-id="02dea-213">주 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="02dea-213">Primary data center</span></span> | <span data-ttu-id="02dea-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="02dea-214">SQL-2</span></span> | <span data-ttu-id="02dea-215">주</span><span class="sxs-lookup"><span data-stu-id="02dea-215">Secondary</span></span> | <span data-ttu-id="02dea-216">동기</span><span class="sxs-lookup"><span data-stu-id="02dea-216">Synchronous</span></span> | <span data-ttu-id="02dea-217">자동</span><span class="sxs-lookup"><span data-stu-id="02dea-217">Automatic</span></span>
| <span data-ttu-id="02dea-218">보조 또는 원격 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="02dea-218">Secondary or remote data center</span></span> | <span data-ttu-id="02dea-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="02dea-219">SQL-3</span></span> | <span data-ttu-id="02dea-220">주</span><span class="sxs-lookup"><span data-stu-id="02dea-220">Secondary</span></span> | <span data-ttu-id="02dea-221">비동기</span><span class="sxs-lookup"><span data-stu-id="02dea-221">Asynchronous</span></span> | <span data-ttu-id="02dea-222">설명서</span><span class="sxs-lookup"><span data-stu-id="02dea-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="02dea-223">계획된 및 강제 수동 장애 조치에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="02dea-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="02dea-224">자세한 내용은 hello 다음 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="02dea-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="02dea-225">가용성 그룹의 계획된 수동 장애 조치 수행(SQL Server)</span><span class="sxs-lookup"><span data-stu-id="02dea-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="02dea-226">가용성 그룹의 강제 수동 장애 조치 수행(SQL Server)</span><span class="sxs-lookup"><span data-stu-id="02dea-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="02dea-227">추가 링크</span><span class="sxs-lookup"><span data-stu-id="02dea-227">Additional Links</span></span>

* [<span data-ttu-id="02dea-228">Always On 가용성 그룹</span><span class="sxs-lookup"><span data-stu-id="02dea-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="02dea-229">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="02dea-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="02dea-230">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="02dea-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="02dea-231">Azure 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="02dea-231">Azure Availability Sets</span></span>](../manage-availability.md)
