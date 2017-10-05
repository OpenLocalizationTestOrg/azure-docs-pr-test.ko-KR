---
title: "경로 문제 해결 - 포털 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Resource Manager 배포 모델에서 경로 문제를 해결하는 방법에 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: dad415936280b4af916b8c46df46f6c51ac0bca4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-the-azure-portal"></a><span data-ttu-id="7a24e-103">Azure Portal을 사용하여 경로 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7a24e-103">Troubleshoot routes using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a24e-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7a24e-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="7a24e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a24e-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
>
>

<span data-ttu-id="7a24e-106">Azure VM(가상 컴퓨터)과의 네트워크 연결 문제가 발생하는 경우 경로가 VM 트래픽 흐름에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="7a24e-107">이 문서에서는 추가 문제 해결을 위해 경로에 대한 진단 기능 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="7a24e-108">경로 테이블은 서브넷과 연결되며 해당 서브넷의 모든 NIC(네트워크 인터페이스)에서 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="7a24e-109">다음 유형의 경로를 각 네트워크 인터페이스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="7a24e-110">**시스템 경로:** 기본적으로 Azure VNet(가상 네트워크)에서 생성된 모든 서브넷에는 로컬 VNet 트래픽, VPN Gateway를 통한 온-프레미스 트래픽 및 인터넷 트래픽을 허용하는 시스템 경로 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="7a24e-111">또한 피어링된 VNet에 대한 시스템 경로도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="7a24e-112">**BGP 경로:** Express 경로 또는 사이트 간 VPN 연결을 통해 네트워크 인터페이스로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="7a24e-113">[VPN Gateway가 있는 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md) 및 [Express 경로 개요](../expressroute/expressroute-introduction.md) 문서를 읽어 BGP 라우팅에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="7a24e-114">**UDR(사용자 정의 경로):** 네트워크 가상 어플라이언스를 사용하거나 사이트 간 VPN을 통해 온-프레미스 네트워크로 트래픽을 강제 터널링하는 경우 UDR(사용자 정의 경로)이 서브넷 경로 테이블에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="7a24e-115">UDR에 익숙하지 않은 경우 [사용자 정의 경로](virtual-networks-udr-overview.md#user-defined-routes) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7a24e-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="7a24e-116">네트워크 인터페이스에 적용할 수 있는 다양한 경로를 사용하는 경우 유효한 집계 경로를 파악하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="7a24e-117">VM 네트워크 연결 문제를 해결하려면 Azure Resource Manager 배포 모델에서 네트워크 인터페이스에 대한 모든 유효 경로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="7a24e-118">유효 경로를 사용하여 VM 트래픽 흐름 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7a24e-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="7a24e-119">이 문서에서는 다음과 같은 시나리오를 예제로 사용하여 네트워크 인터페이스에 대한 유효 경로 문제를 해결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="7a24e-120">VNet(*VNet1*, 접두사: 10.9.0.0/16)에 연결된 VM(*VM1*)이 새로 피어링된 VNet(*VNet3*, 접두사 10.10.0.0/16)의 VM(VM3)에 연결하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="7a24e-121">VM에 연결된 VM1-NIC1 네트워크 인터페이스에 적용된 UDR 또는 BGP 경로가 없으면 시스템 경로만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="7a24e-122">이 문서에서는 Azure 리소스 관리 배포 모델에서 유효 경로 기능을 사용하여 연결 실패의 원인을 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="7a24e-123">이 예제에서는 시스템 경로만 사용하지만 동일한 단계를 사용하여 임의 경로 유형에 대한 인바운드 및 아웃바운드 연결 실패를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="7a24e-124">VM에 연결된 NIC가 두 개 이상 있으면 각 NIC에 대한 유효 경로를 확인하여 VM에서 들어오고 나가는 네트워크 연결 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="7a24e-125">가상 컴퓨터에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="7a24e-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="7a24e-126">VM에 적용되는 집계 경로를 확인하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

1. <span data-ttu-id="7a24e-127">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-127">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="7a24e-128">**더 많은 서비스**를 클릭한 다음 표시되는 목록에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-128">Click **More services**, then click **Virtual machines** in the list that appears.</span></span>
3. <span data-ttu-id="7a24e-129">표시되는 목록에서 문제를 해결할 VM을 선택합니다. 그러면 옵션을 포함하는 VM 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-129">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="7a24e-130">**문제 진단 및 해결**을 클릭하고 일반적인 문제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-130">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="7a24e-131">이 예제에서는 **Windows VM에 연결할 수 없습니다.** 가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-131">For this example, **I can’t connect to my Windows VM** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. <span data-ttu-id="7a24e-132">다음 그림과 같이 문제 아래에 단계가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-132">Steps appear under the problem, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    <span data-ttu-id="7a24e-133">권장 단계 목록에서 *유효 경로* 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-133">Click *effective routes* in the list of recommended steps.</span></span>
6. <span data-ttu-id="7a24e-134">다음 그림과 같이 **유효 경로** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-134">The **Effective routes** blade appears, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    <span data-ttu-id="7a24e-135">VM에 하나의 NIC만 있으면 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-135">If your VM has only one NIC, it is selected by default.</span></span> <span data-ttu-id="7a24e-136">둘 이상의 NIC가 있으면 유효 경로를 보려는 NIC를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-136">If you have more than one NIC, select the NIC for which you want to view the effective routes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a24e-137">NIC와 연결된 VM이 실행 중 상태가 아니면 유효 경로가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-137">If the VM associated with the NIC is not in a running state, effective routes will not be shown.</span></span> <span data-ttu-id="7a24e-138">포털에는 처음 200개의 유효 경로만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-138">Only the first 200 effective routes are shown in the portal.</span></span> <span data-ttu-id="7a24e-139">전체 목록을 보려면 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-139">For the full list, click **Download**.</span></span> <span data-ttu-id="7a24e-140">다운로드한 .csv 파일에서 결과를 추가적으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-140">You can further filter on the results from the downloaded .csv file.</span></span>
   >
   >

    <span data-ttu-id="7a24e-141">출력에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-141">Notice the following in the output:</span></span>

   * <span data-ttu-id="7a24e-142">**Source**: 경로의 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-142">**Source**: Indicates the type of route.</span></span> <span data-ttu-id="7a24e-143">시스템 경로는 *Default*로, UDR은 *User*로, 게이트웨이 경로(정적 또는 BGP)는 *VPNGateway*로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span></span>
   * <span data-ttu-id="7a24e-144">**State**: 유효 경로의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-144">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="7a24e-145">가능한 값은 *Active* 또는 *Invalid*입니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-145">Possible values are *Active* or *Invalid*.</span></span>
   * <span data-ttu-id="7a24e-146">**AddressPrefixes**: CIDR 표기법에 따라 유효 경로의 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-146">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span>
   * <span data-ttu-id="7a24e-147">**nextHopType**: 지정된 경로에 대한 다음 홉을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-147">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="7a24e-148">가능한 값은 *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* 또는 *Null*입니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="7a24e-149">UDR에서 *nextHopType* 값이 **Null** 이면 잘못된 경로를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="7a24e-150">예를 들어 **nextHopType** 이 *VirtualAppliance* 이고 네트워크 가상 어플라이언스 VM이 프로비전됨/실행 중 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-150">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="7a24e-151">**nextHopType** 이 *VPNGateway* 이고 지정된 VNet에서 프로비전됨/실행 중 상태인 게이트웨이가 없으면 경로가 유효하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
7. <span data-ttu-id="7a24e-152">이전 단계에 제공되는 그림에서 *WestUS-VNet1*(접두사 10.9.0.0/16)으로부터 *WestUS-VNET3* VNet(접두사 10.10.0.0/16)으로의 경로는 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-152">There is no route listed to the *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from the *WestUS-VNet1* (Prefix 10.9.0.0/16) in the picture in the previous step.</span></span> <span data-ttu-id="7a24e-153">다음 그림에서 피어링 링크는 *연결 끊김* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-153">In the following picture, the peering link is in the *Disconnected* state:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    <span data-ttu-id="7a24e-154">피어링에 대한 양방향 링크가 끊어졌습니다. 이것은 *WestUS-VNet3* VNet에서 VM1이 VM3에 연결할 수 없는 이유를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-154">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span>
8. <span data-ttu-id="7a24e-155">다음 그림은 양방향 피어링 링크를 설정한 후의 경로를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-155">The following picture shows the routes after establishing the bi-directional peering link:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

<span data-ttu-id="7a24e-156">강제 터널링 및 경로 평가에 대한 추가 문제 해결 시나리오에 대해서는 이 문서의 [고려 사항](virtual-network-routes-troubleshoot-portal.md#considerations) 섹션을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7a24e-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read the [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="7a24e-157">네트워크 인터페이스에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="7a24e-157">View effective routes for a network interface</span></span>
<span data-ttu-id="7a24e-158">특정 네트워크 인터페이스(NIC)에 대해 네트워크 트래픽 흐름이 영향을 받을 경우 NIC에 대한 유효 경로의 전체 목록을 직접 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span></span> <span data-ttu-id="7a24e-159">NIC에 적용되는 집계 경로를 확인하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-159">To see the aggregate routes that are applied to a NIC, complete the following steps:</span></span>

1. <span data-ttu-id="7a24e-160">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-160">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="7a24e-161">**더 많은 서비스**를 클릭한 다음 **네트워크 인터페이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-161">Click **More services**, then click **Network interfaces**</span></span>
3. <span data-ttu-id="7a24e-162">목록에서 NIC의 이름을 검색하거나 나타나는 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-162">Search the list for the name of a NIC, or select it from the list that appears.</span></span> <span data-ttu-id="7a24e-163">이 예제에서는 **VM1-NIC1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-163">In this example, **VM1-NIC1** is selected.</span></span>
4. <span data-ttu-id="7a24e-164">다음 그림과 같이 **네트워크 인터페이스** 블레이드에서 **유효 경로**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-164">Select **Effective routes** in the **Network interface** blade, as shown in the following picture:</span></span>

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    <span data-ttu-id="7a24e-165">**범위** 의 기본값은 선택한 네트워크 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-165">The **Scope** defaults to the network interface selected.</span></span>

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a><span data-ttu-id="7a24e-166">경로 테이블에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="7a24e-166">View effective routes for a route table</span></span>
<span data-ttu-id="7a24e-167">경로 테이블에서 UDR(사용자 정의 경로)을 수정하는 경우 특정 VM에 경로가 추가될 때의 미치는 영향을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-167">When modifying user-defined routes (UDRs) in a route table, you may want to review the impact of the routes being added on a particular VM.</span></span> <span data-ttu-id="7a24e-168">경로 테이블은 제한 없는 수의 서브넷에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-168">A route table can be associated with any number of subnets.</span></span> <span data-ttu-id="7a24e-169">지정된 경로 테이블 블레이드에서 컨텍스트를 전환하지 않고도, 지정된 경로 테이블이 적용되는 모든 NIC에 대한 모든 유효 경로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-169">You can now view all the effective routes for all the NICs that a given route table is applied to, without having to switch context from the given route table blade.</span></span>

<span data-ttu-id="7a24e-170">이 예제에서는 UDR(*UDRoute*)이 경로 테이블(*UDRouteTable*)에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span></span> <span data-ttu-id="7a24e-171">이 경로는 동일한 VNet의 *Subnet2*에 있는 NVA(네트워크 가상 어플라이언스)를 통해 *WestUS-VNet1* VNet의 *Subnet1*에서 모든 인터넷 트래픽을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-171">This route sends all Internet traffic from *Subnet1* in the *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of the same VNet.</span></span> <span data-ttu-id="7a24e-172">이 경로는 다음 그림에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-172">The route is shown in the following picture:</span></span>

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

<span data-ttu-id="7a24e-173">경로 테이블에 대한 집계 경로를 확인하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-173">To see the aggregate routes for a route table, complete the following steps:</span></span>

1. <span data-ttu-id="7a24e-174">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-174">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="7a24e-175">**더 많은 서비스**를 클릭한 다음 **경로 테이블**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-175">Click **More services**, then click **Route tables**</span></span>
3. <span data-ttu-id="7a24e-176">목록에서 보려는 경로 테이블을 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-176">Search the list for the route table you want to see aggregate routes for and select it.</span></span> <span data-ttu-id="7a24e-177">이 예제에서는 **UDRouteTable** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-177">In this example, **UDRouteTable** is selected.</span></span> <span data-ttu-id="7a24e-178">다음 그림과 같이 선택한 경로 테이블에 대한 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-178">A blade for the selected route table appears, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. <span data-ttu-id="7a24e-179">**경로 테이블** 블레이드에서 **유효 경로**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-179">Select **Effective Routes** in the **Route table** blade.</span></span> <span data-ttu-id="7a24e-180">**범위** 가 선택한 경로 테이블로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-180">The **Scope** is set to the route table you selected.</span></span>
5. <span data-ttu-id="7a24e-181">하나의 경로 테이블을 여러 서브넷에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-181">A route table can be applied to multiple subnets.</span></span> <span data-ttu-id="7a24e-182">목록에서 검토하려는 **서브넷** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-182">Select the **Subnet** you want to review from the list.</span></span> <span data-ttu-id="7a24e-183">이 예제에서는 **Subnet1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-183">In this example, **Subnet1** is selected.</span></span>
6. <span data-ttu-id="7a24e-184">**네트워크 인터페이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-184">Select a **Network Interface**.</span></span> <span data-ttu-id="7a24e-185">선택한 서브넷에 연결된 모든 NIC가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-185">All NICs connected to the selected subnet are listed.</span></span> <span data-ttu-id="7a24e-186">이 예제에서는 **VM1-NIC1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-186">In this example, **VM1-NIC1** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > <span data-ttu-id="7a24e-187">NIC가 실행 중인 VM에 연결되지 않으면 유효 경로가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-187">If the NIC is not associated with a running VM, no effective routes are shown.</span></span>
   >
   >

## <a name="considerations"></a><span data-ttu-id="7a24e-188">고려 사항</span><span class="sxs-lookup"><span data-stu-id="7a24e-188">Considerations</span></span>
<span data-ttu-id="7a24e-189">반환된 경로 목록을 검토할 때 몇 가지 사항에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-189">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="7a24e-190">라우팅은 UDR, BGP 및 시스템 경로 중에서 LPM(가장 긴 접두사 일치)을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="7a24e-191">LPM 일치가 동일한 경로가 두 개 이상 있으면 다음 순서대로 해당 원점에 따라 경로가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-191">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>

  * <span data-ttu-id="7a24e-192">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="7a24e-192">User-defined route</span></span>
  * <span data-ttu-id="7a24e-193">BGP 경로</span><span class="sxs-lookup"><span data-stu-id="7a24e-193">BGP route</span></span>
  * <span data-ttu-id="7a24e-194">시스템(기본) 경로</span><span class="sxs-lookup"><span data-stu-id="7a24e-194">System (Default) route</span></span>

    <span data-ttu-id="7a24e-195">유효 경로를 사용하면 사용 가능한 모든 경로를 기준으로 LPM 일치에 해당하는 유효 경로만 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-195">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="7a24e-196">이 경우 지정된 NIC에 대해 경로가 실제로 평가되는 방식이 표시되므로 VM과의 연결에 영향을 미칠 수 있는 특정 경로 문제를 훨씬 더 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-196">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="7a24e-197">UDR이 있고 *VirtualAppliance*를 **nextHopType**으로 지정하여 NVA(네트워크 가상 어플라이언스)로 트래픽을 보내는 경우 트래픽을 수신하는 NVA에 대해 IP 전달이 사용되도록 설정되어 있는지 확인합니다. 그렇지 않으면 패킷이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-197">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span>
* <span data-ttu-id="7a24e-198">강제 터널링을 사용하도록 설정하면 모든 아웃바운드 인터넷 트래픽이 온-프레미스로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="7a24e-199">온-프레미스가 이 트래픽을 처리하는 방법에 따라 인터넷에서 VM으로의 RDP/SSH가 이 설정에서 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-199">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span>
  <span data-ttu-id="7a24e-200">다음과 같이 강제 터널링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-200">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="7a24e-201">nextHopType을 VPN Gateway로 지정하고 UDR(사용자 정의 경로) 설정하여 사이트 간 VPN을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7a24e-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="7a24e-202">기본 경로가 BGP를 통해 보급되는 경우</span><span class="sxs-lookup"><span data-stu-id="7a24e-202">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="7a24e-203">VNet 피어링 트래픽이 제대로 작동하려면 피어링된 VNet의 접두사 범위에 대해 **nextHopType** *VNetPeering* 의 시스템 경로가 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-203">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="7a24e-204">이러한 경로가 존재하지 않고 VNet 피어링 링크에 문제가 없어 보이는 경우</span><span class="sxs-lookup"><span data-stu-id="7a24e-204">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="7a24e-205">몇 초 동안 기다린 후 새로 설정된 피어링 링크가 있으면 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-205">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="7a24e-206">경우에 따라 서브넷에 있는 모든 네트워크 인터페이스로 경로를 전파하는 데 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-206">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="7a24e-207">NSG(네트워크 보안 그룹) 규칙이 트래픽 흐름에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a24e-207">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="7a24e-208">자세한 내용은 [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a24e-208">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span></span>
