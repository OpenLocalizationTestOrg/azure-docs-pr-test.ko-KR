---
title: "경로 문제 해결 - PowerShell | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Azure Resource Manager 배포 모델에서 경로 문제를 해결하는 방법에 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 141e3c571d744470fd07e99538b6e38d4144e8d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="549da-103">Azure PowerShell을 사용하여 경로 문제 해결</span><span class="sxs-lookup"><span data-stu-id="549da-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="549da-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="549da-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="549da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="549da-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="549da-106">Azure VM(가상 컴퓨터)과의 네트워크 연결 문제가 발생하는 경우 경로가 VM 트래픽 흐름에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="549da-107">이 문서에서는 추가 문제 해결을 위해 경로에 대한 진단 기능 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="549da-108">경로 테이블은 서브넷과 연결되며 해당 서브넷의 모든 NIC(네트워크 인터페이스)에서 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="549da-109">다음 유형의 경로를 각 네트워크 인터페이스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="549da-110">**시스템 경로:** 기본적으로 Azure VNet(가상 네트워크)에서 생성된 모든 서브넷에는 로컬 VNet 트래픽, VPN Gateway를 통한 온-프레미스 트래픽 및 인터넷 트래픽을 허용하는 시스템 경로 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="549da-111">또한 피어링된 VNet에 대한 시스템 경로도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="549da-112">**BGP 경로:** Express 경로 또는 사이트 간 VPN 연결을 통해 네트워크 인터페이스로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="549da-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="549da-113">[VPN Gateway가 있는 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md) 및 [Express 경로 개요](../expressroute/expressroute-introduction.md) 문서를 읽어 BGP 라우팅에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="549da-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="549da-114">**UDR(사용자 정의 경로):** 네트워크 가상 어플라이언스를 사용하거나 사이트 간 VPN을 통해 온-프레미스 네트워크로 트래픽을 강제 터널링하는 경우 UDR(사용자 정의 경로)이 서브넷 경로 테이블에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="549da-115">UDR에 익숙하지 않은 경우 [사용자 정의 경로](virtual-networks-udr-overview.md#user-defined-routes) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="549da-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="549da-116">네트워크 인터페이스에 적용할 수 있는 다양한 경로를 사용하는 경우 유효한 집계 경로를 파악하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="549da-117">VM 네트워크 연결 문제를 해결하려면 Azure Resource Manager 배포 모델에서 네트워크 인터페이스에 대한 모든 유효 경로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="549da-118">유효 경로를 사용하여 VM 트래픽 흐름 문제 해결</span><span class="sxs-lookup"><span data-stu-id="549da-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="549da-119">이 문서에서는 다음과 같은 시나리오를 예제로 사용하여 네트워크 인터페이스에 대한 유효 경로 문제를 해결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="549da-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="549da-120">VNet(*VNet1*, 접두사: 10.9.0.0/16)에 연결된 VM(*VM1*)이 새로 피어링된 VNet(*VNet3*, 접두사 10.10.0.0/16)의 VM(VM3)에 연결하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="549da-121">VM에 연결된 VM1-NIC1 네트워크 인터페이스에 적용된 UDR 또는 BGP 경로가 없으면 시스템 경로만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="549da-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="549da-122">이 문서에서는 Azure 리소스 관리 배포 모델에서 유효 경로 기능을 사용하여 연결 실패의 원인을 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="549da-123">이 예제에서는 시스템 경로만 사용하지만 동일한 단계를 사용하여 임의 경로 유형에 대한 인바운드 및 아웃바운드 연결 실패를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="549da-124">VM에 연결된 NIC가 두 개 이상 있으면 각 NIC에 대한 유효 경로를 확인하여 VM에서 들어오고 나가는 네트워크 연결 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="549da-125">가상 컴퓨터에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="549da-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="549da-126">VM에 적용되는 집계 경로를 확인하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="549da-127">네트워크 인터페이스에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="549da-127">View effective routes for a network interface</span></span>
<span data-ttu-id="549da-128">네트워크 인터페이스에 적용되는 집계 경로를 확인하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="549da-129">Azure PowerShell 세션을 시작하고 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="549da-130">Azure PowerShell에 친숙하지 않은 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="549da-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="549da-131">다음 명령은 을 입력하여 리소스 그룹 *RG1*의 네트워크 인터페이스 *VM1-NIC1*에 적용되는 모든 경로를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="549da-132">네트워크 인터페이스의 이름을 모르는 경우 다음 명령을 입력하여 리소스 그룹에 있는 모든 네트워크 인터페이스의 이름을 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="549da-132">If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="549da-133">다음 출력은 NIC가 연결된 서브넷에 적용된 각 경로에 대한 출력과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="549da-134">출력에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="549da-135">**Name**: 명시적으로 지정하지 않은 경우 사용자 정의 경로에 대한 유효 경로의 이름은 비워 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="549da-136">**State**: 유효 경로의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="549da-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="549da-137">가능한 값은 “Active” 또는 “Invalid”입니다.</span><span class="sxs-lookup"><span data-stu-id="549da-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="549da-138">**AddressPrefixes**: CIDR 표기법에 따라 유효 경로의 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="549da-139">**nextHopType**: 지정된 경로에 대한 다음 홉을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="549da-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="549da-140">가능한 값은 *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* 또는 *Null*입니다.</span><span class="sxs-lookup"><span data-stu-id="549da-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="549da-141">UDR에서 *nextHopType* 값이 **Null** 이면 잘못된 경로를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="549da-142">예를 들어 **nextHopType** 이 *VirtualAppliance* 이고 네트워크 가상 어플라이언스 VM이 프로비전됨/실행 중 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="549da-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="549da-143">**nextHopType** 이 *VPNGateway* 이고 지정된 VNet에서 프로비전됨/실행 중 상태인 게이트웨이가 없으면 경로가 유효하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="549da-144">**NextHopIpAddress**: 유효 경로의 다음 홉에 대한 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="549da-145">다음 명령은 좀 더 보기 쉬운 표 형태로 경로를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="549da-146">다음 출력은 앞에서 설명한 시나리오에 대해 수신되는 출력의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="549da-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="549da-147">이전 단계의 출력에서 *WestUS-VNet1*(접두사 10.9.0.0/16)으로부터 *WestUS-VNet3* VNet(접두사 10.10.0.0/16)**으로의 경로는 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="549da-148">다음 그림과 같이 *WestUS-VNet3* VNet과의 VNet 피어링 링크는 *연결 끊김* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="549da-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="549da-149">피어링에 대한 양방향 링크가 끊어졌습니다. 이것은 *WestUS-VNet3* VNet에서 VM1이 VM3에 연결할 수 없는 이유를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="549da-150">*WestUS-VNet1* 및 *WestUS-VNet3* VNet에 대해 양방향 VNet 피어링 링크를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="549da-151">VNet 피어링 링크가 올바르게 설정된 후 반환되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="549da-152">문제를 확인한 경우 경로 및 경로 테이블을 추가, 제거 또는 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="549da-153">이 작업에 사용되는 명령 목록을 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="549da-154">고려 사항</span><span class="sxs-lookup"><span data-stu-id="549da-154">Considerations</span></span>
<span data-ttu-id="549da-155">반환된 경로 목록을 검토할 때 몇 가지 사항에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="549da-156">라우팅은 UDR, BGP 및 시스템 경로 중에서 LPM(가장 긴 접두사 일치)을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="549da-157">LPM 일치가 동일한 경로가 두 개 이상 있으면 다음 순서대로 해당 원점에 따라 경로가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="549da-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="549da-158">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="549da-158">User-defined route</span></span>
  * <span data-ttu-id="549da-159">BGP 경로</span><span class="sxs-lookup"><span data-stu-id="549da-159">BGP route</span></span>
  * <span data-ttu-id="549da-160">시스템(기본) 경로</span><span class="sxs-lookup"><span data-stu-id="549da-160">System (Default) route</span></span>
    
    <span data-ttu-id="549da-161">유효 경로를 사용하면 사용 가능한 모든 경로를 기준으로 LPM 일치에 해당하는 유효 경로만 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="549da-162">이 경우 지정된 NIC에 대해 경로가 실제로 평가되는 방식이 표시되므로 VM과의 연결에 영향을 미칠 수 있는 특정 경로 문제를 훨씬 더 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="549da-163">UDR이 있고 *VirtualAppliance*를 **nextHopType**으로 지정하여 NVA(네트워크 가상 어플라이언스)로 트래픽을 보내는 경우 트래픽을 수신하는 NVA에 대해 IP 전달이 사용되도록 설정되어 있는지 확인합니다. 그렇지 않으면 패킷이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="549da-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="549da-164">강제 터널링을 사용하도록 설정하면 모든 아웃바운드 인터넷 트래픽이 온-프레미스로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="549da-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="549da-165">온-프레미스가 이 트래픽을 처리하는 방법에 따라 인터넷에서 VM으로의 RDP/SSH가 이 설정에서 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="549da-166">다음과 같이 강제 터널링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="549da-167">nextHopType을 VPN Gateway로 지정하고 UDR(사용자 정의 경로) 설정하여 사이트 간 VPN을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="549da-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="549da-168">기본 경로가 BGP를 통해 보급되는 경우</span><span class="sxs-lookup"><span data-stu-id="549da-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="549da-169">VNet 피어링 트래픽이 제대로 작동하려면 피어링된 VNet의 접두사 범위에 대해 **nextHopType** *VNetPeering* 의 시스템 경로가 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="549da-170">이러한 경로가 존재하지 않고 VNet 피어링 링크에 문제가 없어 보이는 경우</span><span class="sxs-lookup"><span data-stu-id="549da-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="549da-171">몇 초 동안 기다린 후 새로 설정된 피어링 링크가 있으면 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="549da-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="549da-172">경우에 따라 서브넷에 있는 모든 네트워크 인터페이스로 경로를 전파하는 데 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="549da-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="549da-173">NSG(네트워크 보안 그룹) 규칙이 트래픽 흐름에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549da-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="549da-174">자세한 내용은 [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-powershell.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="549da-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

