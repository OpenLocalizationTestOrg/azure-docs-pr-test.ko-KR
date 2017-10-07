---
title: "aaaTroubleshoot 경로-포털 | Microsoft Docs"
description: "Hello Azure 리소스 관리자 배포 사용 하 여 모델의 tootroubleshoot 경로 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a><span data-ttu-id="400f7-103">Hello Azure 포털을 사용 하 여 경로 문제 해결</span><span class="sxs-lookup"><span data-stu-id="400f7-103">Troubleshoot routes using hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="400f7-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="400f7-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="400f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="400f7-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
>
>

<span data-ttu-id="400f7-106">발생 하는 경우 네트워크 연결 문제 tooor Azure 가상 컴퓨터 (VM)에서 경로 미치는 영향 VM 트래픽 흐름.</span><span class="sxs-lookup"><span data-stu-id="400f7-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="400f7-107">이 문서에서는 toohelp 추가로 문제를 해결 하는 경로 대 한 진단 기능에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="400f7-108">경로 테이블은 서브넷과 연결되며 해당 서브넷의 모든 NIC(네트워크 인터페이스)에서 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="400f7-109">유형의 경로 따라 hello 적용된 tooeach 네트워크 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="400f7-110">**시스템 경로:** 기본적으로 Azure VNet(가상 네트워크)에서 생성된 모든 서브넷에는 로컬 VNet 트래픽, VPN Gateway를 통한 온-프레미스 트래픽 및 인터넷 트래픽을 허용하는 시스템 경로 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="400f7-111">또한 피어링된 VNet에 대한 시스템 경로도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="400f7-112">**BGP 경로:** toonetwork 인터페이스 ExpressRoute 또는 사이트 간 VPN 연결을 통해 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="400f7-113">Hello를 참조 하 여 BGP 라우팅에 대 한 자세한 [VPN 게이트웨이 사용한 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md) 및 [ExpressRoute 개요](../expressroute/expressroute-introduction.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="400f7-114">**사용자 정의 경로 (UDR):** 은 강제 터널링 또는 네트워크 가상 어플라이언스를 사용 하는 경우 사이트 간 VPN 통해 트래픽 tooan 온-프레미스 네트워크를 사용자 정의 된 경로 (UDRs) 연결 된 서브넷 경로 테이블을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="400f7-115">UDRs 모르는 경우 읽기 hello [사용자 정의 경로](virtual-networks-udr-overview.md#user-defined-routes) 문서.</span><span class="sxs-lookup"><span data-stu-id="400f7-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="400f7-116">Hello로 적용된 tooa 네트워크 인터페이스 일 수 있는 다양 한 경로 가능 어려운 toodetermine 집계는 경로 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="400f7-117">toohelp VM 네트워크 연결 문제 해결, 네트워크 인터페이스에 대 한 모든 hello 유효 경로 hello Azure 리소스 관리자 배포 모델에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="400f7-118">유효 경로 tootroubleshoot VM 트래픽 흐름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="400f7-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="400f7-119">이 문서는 예제 tooillustrate tootroubleshoot hello 유효 네트워크 인터페이스에 대 한 라우팅하는 방법으로 시나리오를 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="400f7-120">VM (*VM1*) toohello VNet 연결 (*VNet1*, 접두사: 10.9.0.0/16) tooconnect tooa 새로 peered VNet에서 VM(VM3) 실패 (*VNet3*, 10.10.0.0/16 접두사).</span><span class="sxs-lookup"><span data-stu-id="400f7-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="400f7-121">있으며 범위 BGP 없음이나 UDRs 라우팅합니다 tooVM1-c 1의 적용 된 네트워크 인터페이스 연결 toohello VM만 시스템 경로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="400f7-122">이 문서에서는 toodetermine hello hello 연결 오류, 유효 경로 기능을 사용 하 여 Azure 리소스 관리 배포 모델에서 발생 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="400f7-123">동일한 단계를 hello hello 예제에서는 시스템 경로만 사용 하는 동안 모든 경로 형식에 대해 사용 되는 toodetermine 인바운드 및 아웃 바운드 연결 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="400f7-124">VM에 연결 된 NIC를 여러 개 있는 경우 각 VM에서 Nic toodiagnose 네트워크 연결 문제 tooand hello에 대 한 유효한 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="400f7-125">가상 컴퓨터에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="400f7-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="400f7-126">toosee hello 집계 되 경로 적용 된 tooa VM을 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="400f7-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

1. <span data-ttu-id="400f7-127">Azure 포털 https://portal.azure.com toohello를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-127">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="400f7-128">클릭 **더 많은 서비스**, 클릭 **가상 컴퓨터** 표시 되는 hello 목록에서입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-128">Click **More services**, then click **Virtual machines** in hello list that appears.</span></span>
3. <span data-ttu-id="400f7-129">VM tootroubleshoot 나타나는 hello 목록에서 선택한 옵션과 함께 VM 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-129">Select a VM tootroubleshoot from hello list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="400f7-130">**문제 진단 및 해결**을 클릭하고 일반적인 문제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-130">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="400f7-131">예를 들어 **toomy Windows VM을 연결할 수 없습니다.** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-131">For this example, **I can’t connect toomy Windows VM** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. <span data-ttu-id="400f7-132">단계는 hello 다음 그림에에서 나와 있는 것 처럼 hello 문제를 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-132">Steps appear under hello problem, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    <span data-ttu-id="400f7-133">클릭 *유효 경로* hello 권장된 단계 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-133">Click *effective routes* in hello list of recommended steps.</span></span>
6. <span data-ttu-id="400f7-134">hello **유효 경로** hello 다음 그림에에서 나와 있는 것 처럼 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-134">hello **Effective routes** blade appears, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    <span data-ttu-id="400f7-135">VM에 하나의 NIC만 있으면 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-135">If your VM has only one NIC, it is selected by default.</span></span> <span data-ttu-id="400f7-136">NIC 1 개 이상 있는 경우 tooview hello 유효 경로 원하는 hello NIC를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-136">If you have more than one NIC, select hello NIC for which you want tooview hello effective routes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="400f7-137">Hello VM에 연결 된 hello NIC가 실행 중 상태로, 유효 경로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-137">If hello VM associated with hello NIC is not in a running state, effective routes will not be shown.</span></span> <span data-ttu-id="400f7-138">만 hello 처음 200 유효 경로에 표시 됩니다 hello 포털.</span><span class="sxs-lookup"><span data-stu-id="400f7-138">Only hello first 200 effective routes are shown in hello portal.</span></span> <span data-ttu-id="400f7-139">Hello 전체 목록을 보려면 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-139">For hello full list, click **Download**.</span></span> <span data-ttu-id="400f7-140">Hello 다운로드 한.csv 파일 로부터 hello 결과에 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-140">You can further filter on hello results from hello downloaded .csv file.</span></span>
   >
   >

    <span data-ttu-id="400f7-141">Hello hello 출력에는 다음 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="400f7-141">Notice hello following in hello output:</span></span>

   * <span data-ttu-id="400f7-142">**소스**: 경로의 hello 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-142">**Source**: Indicates hello type of route.</span></span> <span data-ttu-id="400f7-143">시스템 경로는 *Default*로, UDR은 *User*로, 게이트웨이 경로(정적 또는 BGP)는 *VPNGateway*로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span></span>
   * <span data-ttu-id="400f7-144">**상태**: hello 유효 경로의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-144">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="400f7-145">가능한 값은 *Active* 또는 *Invalid*입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-145">Possible values are *Active* or *Invalid*.</span></span>
   * <span data-ttu-id="400f7-146">**AddressPrefixes**: CIDR 표기법으로 hello hello 유효한 경로의 주소 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-146">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span>
   * <span data-ttu-id="400f7-147">**nextHopType**: hello 경로 지정 하는 hello에 대 한 다음 홉을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-147">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="400f7-148">가능한 값은 *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* 또는 *Null*입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="400f7-149">UDR에서 *nextHopType* 값이 **Null** 이면 잘못된 경로를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="400f7-150">예를 들어 경우 **nextHopType** 은 *virtualappliance 인* 및 hello 네트워크 가상 어플라이언스 VM이 프로 비전/실행 중 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-150">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="400f7-151">경우 **nextHopType** 은 *VPNGateway* 및 실행 되 고 있는 게이트웨이가 없는 사용자를 프로 비전/hello 지정 된 VNet에에서, hello 경로 잘못 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
7. <span data-ttu-id="400f7-152">나열 된 경로 toohello 없습니다는 *WestUS VNET3* hello에서 VNet (접두사 10.10.0.0/16) *WestUS VNet1* (10.9.0.0/16 접두사) hello 이전 단계에서 hello 그림의 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-152">There is no route listed toohello *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from hello *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello picture in hello previous step.</span></span> <span data-ttu-id="400f7-153">다음 그림 hello, hello 피어 링 링크가 hello에 *Disconnected* 상태:</span><span class="sxs-lookup"><span data-stu-id="400f7-153">In hello following picture, hello peering link is in hello *Disconnected* state:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    <span data-ttu-id="400f7-154">hello 양방향 링크 VM1 tooVM3 hello에 연결 하지 못했습니다 이유를 설명 하 고 중단 되는 hello 피어 링에 대 한 *WestUS VNet3* VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-154">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span>
8. <span data-ttu-id="400f7-155">hello 다음 다음과 같은 순서로 hello 경로 hello 양방향 피어 링 링크를 설정한 후</span><span class="sxs-lookup"><span data-stu-id="400f7-155">hello following picture shows hello routes after establishing hello bi-directional peering link:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

<span data-ttu-id="400f7-156">강제 터널링 및 경로 평가 대 한 더 문제 해결 시나리오에 대 한 읽기 hello [고려 사항](virtual-network-routes-troubleshoot-portal.md#considerations) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="400f7-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read hello [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="400f7-157">네트워크 인터페이스에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="400f7-157">View effective routes for a network interface</span></span>
<span data-ttu-id="400f7-158">특정 네트워크 인터페이스(NIC)에 대해 네트워크 트래픽 흐름이 영향을 받을 경우 NIC에 대한 유효 경로의 전체 목록을 직접 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span></span> <span data-ttu-id="400f7-159">toosee hello 집계 되 경로 적용 된 tooa NIC를 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="400f7-159">toosee hello aggregate routes that are applied tooa NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="400f7-160">Azure 포털 https://portal.azure.com toohello를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-160">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="400f7-161">**더 많은 서비스**를 클릭한 다음 **네트워크 인터페이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-161">Click **More services**, then click **Network interfaces**</span></span>
3. <span data-ttu-id="400f7-162">NIC의 hello 이름에 대 한 hello 목록을 검색 하거나 나타나는 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-162">Search hello list for hello name of a NIC, or select it from hello list that appears.</span></span> <span data-ttu-id="400f7-163">이 예제에서는 **VM1-NIC1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-163">In this example, **VM1-NIC1** is selected.</span></span>
4. <span data-ttu-id="400f7-164">선택 **유효 경로** hello에 **네트워크 인터페이스** hello 다음 그림에에서 나와 있는 것 처럼 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="400f7-164">Select **Effective routes** in hello **Network interface** blade, as shown in hello following picture:</span></span>

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    <span data-ttu-id="400f7-165">hello **범위** 기본값 toohello 네트워크 인터페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-165">hello **Scope** defaults toohello network interface selected.</span></span>

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a><span data-ttu-id="400f7-166">경로 테이블에 대한 유효 경로 보기</span><span class="sxs-lookup"><span data-stu-id="400f7-166">View effective routes for a route table</span></span>
<span data-ttu-id="400f7-167">경로 테이블에 사용자 정의 경로 (UDRs)를 수정 하는 경우 특정 VM에 추가 되는 hello 경로의 tooreview hello 영향을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-167">When modifying user-defined routes (UDRs) in a route table, you may want tooreview hello impact of hello routes being added on a particular VM.</span></span> <span data-ttu-id="400f7-168">경로 테이블은 제한 없는 수의 서브넷에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-168">A route table can be associated with any number of subnets.</span></span> <span data-ttu-id="400f7-169">지정 된 경로 테이블에 적용 되는 Nic 모든 hello에 대 한 모든 hello 유효 경로 볼 수 경로 테이블 블레이드를 제공 하는 hello tooswitch 컨텍스트가 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-169">You can now view all hello effective routes for all hello NICs that a given route table is applied to, without having tooswitch context from hello given route table blade.</span></span>

<span data-ttu-id="400f7-170">이 예제에서는 UDR(*UDRoute*)이 경로 테이블(*UDRouteTable*)에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span></span> <span data-ttu-id="400f7-171">이 경로에서 모든 인터넷 트래픽에 보냅니다 *Subnet1* hello에 *WestUS VNet1* 네트워크 가상 어플라이언스 (NVA)를 통해 VNet에서 *e t 2* 의 동일한 VNet hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-171">This route sends all Internet traffic from *Subnet1* in hello *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of hello same VNet.</span></span> <span data-ttu-id="400f7-172">hello 경로 hello 다음 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-172">hello route is shown in hello following picture:</span></span>

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

<span data-ttu-id="400f7-173">경로 테이블의 경우 다음 단계 완료 hello toosee hello의 집계 경로:</span><span class="sxs-lookup"><span data-stu-id="400f7-173">toosee hello aggregate routes for a route table, complete hello following steps:</span></span>

1. <span data-ttu-id="400f7-174">Azure 포털 https://portal.azure.com toohello를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-174">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="400f7-175">**더 많은 서비스**를 클릭한 다음 **경로 테이블**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-175">Click **More services**, then click **Route tables**</span></span>
3. <span data-ttu-id="400f7-176">Hello 경로 테이블에 대 한 검색 hello 목록에 대 한 집계 경로 toosee을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-176">Search hello list for hello route table you want toosee aggregate routes for and select it.</span></span> <span data-ttu-id="400f7-177">이 예제에서는 **UDRouteTable** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-177">In this example, **UDRouteTable** is selected.</span></span> <span data-ttu-id="400f7-178">선택한 hello 경로 테이블에 대 한 블레이드 hello 다음 그림에에서 나와 있는 것 처럼 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-178">A blade for hello selected route table appears, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. <span data-ttu-id="400f7-179">선택 **유효 경로** hello에 **경로 테이블** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-179">Select **Effective Routes** in hello **Route table** blade.</span></span> <span data-ttu-id="400f7-180">hello **범위** 선택한 toohello 경로 테이블을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-180">hello **Scope** is set toohello route table you selected.</span></span>
5. <span data-ttu-id="400f7-181">경로 테이블에 적용 된 toomultiple 서브넷 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-181">A route table can be applied toomultiple subnets.</span></span> <span data-ttu-id="400f7-182">선택 hello **서브넷** tooreview hello 목록에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-182">Select hello **Subnet** you want tooreview from hello list.</span></span> <span data-ttu-id="400f7-183">이 예제에서는 **Subnet1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-183">In this example, **Subnet1** is selected.</span></span>
6. <span data-ttu-id="400f7-184">**네트워크 인터페이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-184">Select a **Network Interface**.</span></span> <span data-ttu-id="400f7-185">모든 Nic 연결 된 toohello 선택한 서브넷이 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-185">All NICs connected toohello selected subnet are listed.</span></span> <span data-ttu-id="400f7-186">이 예제에서는 **VM1-NIC1** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-186">In this example, **VM1-NIC1** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > <span data-ttu-id="400f7-187">Hello NIC를 실행 중인 VM과 연결 없으면 효과적인 경로가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-187">If hello NIC is not associated with a running VM, no effective routes are shown.</span></span>
   >
   >

## <a name="considerations"></a><span data-ttu-id="400f7-188">고려 사항</span><span class="sxs-lookup"><span data-stu-id="400f7-188">Considerations</span></span>
<span data-ttu-id="400f7-189">반환 되는 몇 가지 tookeep hello 경로 목록을 검토할 때 염두에서입니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-189">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="400f7-190">라우팅은 UDR, BGP 및 시스템 경로 중에서 LPM(가장 긴 접두사 일치)을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="400f7-191">Hello로 둘 이상의 경로가 있는 경우 동일 LPM 일치 한 경로 순서에 따라 hello에서 원본에 따라 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-191">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>

  * <span data-ttu-id="400f7-192">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="400f7-192">User-defined route</span></span>
  * <span data-ttu-id="400f7-193">BGP 경로</span><span class="sxs-lookup"><span data-stu-id="400f7-193">BGP route</span></span>
  * <span data-ttu-id="400f7-194">시스템(기본) 경로</span><span class="sxs-lookup"><span data-stu-id="400f7-194">System (Default) route</span></span>

    <span data-ttu-id="400f7-195">유효한 경로와 모든 hello 사용할 수 경로에 따라 LPM과 일치 하는 유효 경로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-195">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="400f7-196">Hello 경로 실제로 평가 되는 방식을 지정 nic를 표시 하 여이 통해 VM에서 연결에 미치는 영향는 훨씬 더 쉽게 tootroubleshoot 특정 경로.</span><span class="sxs-lookup"><span data-stu-id="400f7-196">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="400f7-197">UDRs 있고 트래픽을 tooa 네트워크 가상 어플라이언스 (NVA)으로 보내는 경우 *virtualappliance 인* 으로 **nextHopType**, hello NVA 수신 hello 트래픽을 IP 전달 설정 되어 있는지 확인 하거나 패킷이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-197">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span>
* <span data-ttu-id="400f7-198">강제 터널링을 사용 하는 경우 모든 아웃 바운드 인터넷 트래픽이 라우트된 tooon 온-프레미스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="400f7-199">인터넷 tooyour 어떻게 hello 온-프레미스에 따라이 설정을 사용 하 여 VM이 작동 하지 않을 수에서 RDP/SSH이이 트래픽을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-199">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span>
  <span data-ttu-id="400f7-200">다음과 같이 강제 터널링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-200">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="400f7-201">nextHopType을 VPN Gateway로 지정하고 UDR(사용자 정의 경로) 설정하여 사이트 간 VPN을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="400f7-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="400f7-202">기본 경로가 BGP를 통해 보급되는 경우</span><span class="sxs-lookup"><span data-stu-id="400f7-202">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="400f7-203">VNet 트래픽이 toowork를 올바르게 피어 링 인 시스템 경로 대 한 **nextHopType** *VNetPeering* hello 겹치기 VNet의 접두사 범위에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-203">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="400f7-204">이러한 경로 VNet 피어 링 hello에 존재 하지 않는 경우 링크 된 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-204">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="400f7-205">몇 초 동안 기다린 후 새로 설정된 피어링 링크가 있으면 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-205">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="400f7-206">긴 toopropagate 경로 tooall hello 네트워크 인터페이스 서브넷에 있는 경우에 따라 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="400f7-206">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="400f7-207">네트워크 보안 그룹 (NSG) 규칙에 미치는 영향 hello 트래픽 흐름.</span><span class="sxs-lookup"><span data-stu-id="400f7-207">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="400f7-208">자세한 내용은 참조 hello [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="400f7-208">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span></span>
