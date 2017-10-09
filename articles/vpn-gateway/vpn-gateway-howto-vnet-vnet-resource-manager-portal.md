---
title: "Azure 가상 네트워크 tooanother VNet 연결: 포털 | Microsoft Docs"
description: "리소스 관리자를 사용 하 여 Vnet 간의 VPN 게이트웨이 연결을 만들고 Azure 포털 hello 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a><span data-ttu-id="5fa63-103">Hello Azure 포털을 사용 하 여 VNet 대 VNet VPN 게이트웨이 연결 구성</span><span class="sxs-lookup"><span data-stu-id="5fa63-103">Configure a VNet-to-VNet VPN gateway connection using hello Azure portal</span></span>

<span data-ttu-id="5fa63-104">이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="5fa63-105">hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="5fa63-106">Hello 구독이 다른 구독에서 연결 Vnet toobe hello와 관련 된 필요 하지 않는 경우 동일한 Active Directory 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="5fa63-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="5fa63-107">이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용 하 고 hello Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-107">hello steps in this article apply toohello Resource Manager deployment model and use hello Azure portal.</span></span> <span data-ttu-id="5fa63-108">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fa63-109">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5fa63-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="5fa63-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa63-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="5fa63-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5fa63-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="5fa63-112">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="5fa63-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="5fa63-113">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5fa63-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="5fa63-114">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa63-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

<span data-ttu-id="5fa63-116">가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-116">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="5fa63-117">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-117">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="5fa63-118">Vnet hello에 있는 경우 동일한 지역 VNet 피어 링을 사용 하 여 연결 tooconsider 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-118">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="5fa63-119">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-119">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="5fa63-120">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fa63-120">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="5fa63-121">VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-121">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="5fa63-122">이렇게 하면 hello 다음 다이어그램에에서 나와 있는 것 처럼 가상 네트워크 간 연결 되 면 크로스-프레미스 연결을 결합 하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-122">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

<span data-ttu-id="5fa63-123">![연결 정보](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span><span class="sxs-lookup"><span data-stu-id="5fa63-123">![About connections](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span></span>

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="5fa63-124">가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="5fa63-124">Why connect virtual networks?</span></span>

<span data-ttu-id="5fa63-125">다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-125">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="5fa63-126">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="5fa63-126">**Cross region geo-redundancy and geo-presence**</span></span>
  
  * <span data-ttu-id="5fa63-127">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-127">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="5fa63-128">Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-128">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="5fa63-129">한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-129">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="5fa63-130">**분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="5fa63-130">**Regional multi-tier applications with isolation or administrative boundary**</span></span>
  
  * <span data-ttu-id="5fa63-131">내 동일한 hello 영역을 설정할 수 있습니다 다층 계층 응용 프로그램 기한 tooisolation 또는 관리 요구를 함께 연결 하는 여러 가상 네트워크가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-131">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="5fa63-132">VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-132">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> <span data-ttu-id="5fa63-133">Vnet 서로 다른 구독에 있는 경우 hello 포털에서 hello 연결을 만들 수 없다는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-133">Note that if your VNets are in different subscriptions, you can't create hello connection in hello portal.</span></span> <span data-ttu-id="5fa63-134">[PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 또는 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-134">You can use [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) or [CLI](vpn-gateway-howto-vnet-vnet-cli.md).</span></span>

### <span data-ttu-id="5fa63-135"><a name="values"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="5fa63-135"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="5fa63-136">연습으로 이러한 단계를 사용 하는 경우에 hello 예제 설정 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-136">When using these steps as an exercise, you can use hello example settings values.</span></span> <span data-ttu-id="5fa63-137">예제에서는 각 VNet에 대한 여러 주소 공간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-137">For example purposes, we use multiple address spaces for each VNet.</span></span> <span data-ttu-id="5fa63-138">그러나 VNet 간 구성에는 여러 개의 주소 공간이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-138">However, VNet-to-VNet configurations don't require multiple address spaces.</span></span>

<span data-ttu-id="5fa63-139">**TestVNet1에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="5fa63-139">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="5fa63-140">VNet 이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5fa63-140">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="5fa63-141">주소 공간: 10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5fa63-141">Address space: 10.11.0.0/16</span></span>
  * <span data-ttu-id="5fa63-142">서브넷 이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5fa63-142">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="5fa63-143">서브넷 주소 범위: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5fa63-143">Subnet address range: 10.11.0.0/24</span></span>
* <span data-ttu-id="5fa63-144">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="5fa63-144">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5fa63-145">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="5fa63-145">Location: East US</span></span>
* <span data-ttu-id="5fa63-146">주소 공간: 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5fa63-146">Address Space: 10.12.0.0/16</span></span>
  * <span data-ttu-id="5fa63-147">서브넷 이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="5fa63-147">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="5fa63-148">서브넷 주소 범위: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5fa63-148">Subnet address range: 10.12.0.0/24</span></span>
* <span data-ttu-id="5fa63-149">게이트웨이 서브넷 이름: GatewaySubnet (hello 포털에서 자동 채우기 됩니다)</span><span class="sxs-lookup"><span data-stu-id="5fa63-149">Gateway Subnet name: GatewaySubnet (this will auto-fill in hello portal)</span></span>
  * <span data-ttu-id="5fa63-150">게이트웨이 서브넷 주소 범위: 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5fa63-150">Gateway Subnet address range: 10.11.255.0/27</span></span>
* <span data-ttu-id="5fa63-151">DNS 서버의 IP 주소를 hello를 사용 하는 DNS 서버:</span><span class="sxs-lookup"><span data-stu-id="5fa63-151">DNS Server: Use hello IP address of your DNS Server</span></span>
* <span data-ttu-id="5fa63-152">Virtual Network 게이트웨이 이름: TestVNet1GW</span><span class="sxs-lookup"><span data-stu-id="5fa63-152">Virtual Network Gateway Name: TestVNet1GW</span></span>
* <span data-ttu-id="5fa63-153">게이트웨이 유형: VPN</span><span class="sxs-lookup"><span data-stu-id="5fa63-153">Gateway Type: VPN</span></span>
* <span data-ttu-id="5fa63-154">VPN 유형: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="5fa63-154">VPN type: Route-based</span></span>
* <span data-ttu-id="5fa63-155">SKU: hello toouse 게이트웨이 SKU를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-155">SKU: Select hello Gateway SKU you want toouse</span></span>
* <span data-ttu-id="5fa63-156">공용 IP 주소 이름: TestVNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="5fa63-156">Public IP address name: TestVNet1GWIP</span></span>
* <span data-ttu-id="5fa63-157">연결 값:</span><span class="sxs-lookup"><span data-stu-id="5fa63-157">Connection values:</span></span>
  * <span data-ttu-id="5fa63-158">이름: TestVNet1toTestVNet4</span><span class="sxs-lookup"><span data-stu-id="5fa63-158">Name: TestVNet1toTestVNet4</span></span>
  * <span data-ttu-id="5fa63-159">공유 키: hello 공유 키를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-159">Shared key: You can create hello shared key yourself.</span></span> <span data-ttu-id="5fa63-160">이 예제에서는 abc123을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-160">For this example, we'll use abc123.</span></span> <span data-ttu-id="5fa63-161">hello 중요 한 점은 hello Vnet 간의 hello 연결을 만들 때 hello 값 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-161">hello important thing is that when you create hello connection between hello VNets, hello value must match.</span></span>

<span data-ttu-id="5fa63-162">**TestVNet4에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="5fa63-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="5fa63-163">VNet 이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5fa63-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="5fa63-164">주소 공간: 10.41.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5fa63-164">Address space: 10.41.0.0/16</span></span>
  * <span data-ttu-id="5fa63-165">서브넷 이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5fa63-165">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="5fa63-166">서브넷 주소 범위: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5fa63-166">Subnet address range: 10.41.0.0/24</span></span>
* <span data-ttu-id="5fa63-167">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="5fa63-167">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5fa63-168">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="5fa63-168">Location: West US</span></span>
* <span data-ttu-id="5fa63-169">주소 공간: 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5fa63-169">Address Space: 10.42.0.0/16</span></span>
  * <span data-ttu-id="5fa63-170">서브넷 이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="5fa63-170">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="5fa63-171">서브넷 주소 범위: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5fa63-171">Subnet address range: 10.42.0.0/24</span></span>
* <span data-ttu-id="5fa63-172">GatewaySubnet 이름: GatewaySubnet (hello 포털에서 자동 채우기 됩니다)</span><span class="sxs-lookup"><span data-stu-id="5fa63-172">GatewaySubnet name: GatewaySubnet (this will auto-fill in hello portal)</span></span>
  * <span data-ttu-id="5fa63-173">게이트웨이 서브넷 주소 범위: 10.41.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5fa63-173">GatewaySubnet address range: 10.41.255.0/27</span></span>
* <span data-ttu-id="5fa63-174">DNS 서버의 IP 주소를 hello를 사용 하는 DNS 서버:</span><span class="sxs-lookup"><span data-stu-id="5fa63-174">DNS Server: Use hello IP address of your DNS Server</span></span>
* <span data-ttu-id="5fa63-175">Virtual Network 게이트웨이 이름: TestVNet4GW</span><span class="sxs-lookup"><span data-stu-id="5fa63-175">Virtual Network Gateway Name: TestVNet4GW</span></span>
* <span data-ttu-id="5fa63-176">게이트웨이 유형: VPN</span><span class="sxs-lookup"><span data-stu-id="5fa63-176">Gateway Type: VPN</span></span>
* <span data-ttu-id="5fa63-177">VPN 유형: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="5fa63-177">VPN type: Route-based</span></span>
* <span data-ttu-id="5fa63-178">SKU: hello toouse 게이트웨이 SKU를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-178">SKU: Select hello Gateway SKU you want toouse</span></span>
* <span data-ttu-id="5fa63-179">공용 IP 주소 이름: TestVNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="5fa63-179">Public IP address name: TestVNet4GWIP</span></span>
* <span data-ttu-id="5fa63-180">연결 값:</span><span class="sxs-lookup"><span data-stu-id="5fa63-180">Connection values:</span></span>
  * <span data-ttu-id="5fa63-181">이름: TestVNet4toTestVNet1</span><span class="sxs-lookup"><span data-stu-id="5fa63-181">Name: TestVNet4toTestVNet1</span></span>
  * <span data-ttu-id="5fa63-182">공유 키: hello 공유 키를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-182">Shared key: You can create hello shared key yourself.</span></span> <span data-ttu-id="5fa63-183">이 예제에서는 abc123을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-183">For this example, we'll use abc123.</span></span> <span data-ttu-id="5fa63-184">hello 중요 한 점은 hello Vnet 간의 hello 연결을 만들 때 hello 값 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-184">hello important thing is that when you create hello connection between hello VNets, hello value must match.</span></span>

## <span data-ttu-id="5fa63-185"><a name="CreatVNet"></a>1. TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="5fa63-185"><a name="CreatVNet"></a>1. Create and configure TestVNet1</span></span>
<span data-ttu-id="5fa63-186">VNet 이미 있는 경우 hello 설정이 VPN 게이트웨이 설계와 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-186">If you already have a VNet, verify that hello settings are compatible with your VPN gateway design.</span></span> <span data-ttu-id="5fa63-187">특히 주의 tooany 서브넷이 다른 네트워크와 겹칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-187">Pay particular attention tooany subnets that may overlap with other networks.</span></span> <span data-ttu-id="5fa63-188">겹치는 서브넷에 있으면 연결이 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-188">If you have overlapping subnets, your connection won't work properly.</span></span> <span data-ttu-id="5fa63-189">VNet을 hello 올바른 설정으로 구성 된 경우 hello의 hello 단계를 시작할 수 있습니다 [DNS 서버 지정](#dns) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5fa63-189">If your VNet is configured with hello correct settings, you can begin hello steps in hello [Specify a DNS server](#dns) section.</span></span>

### <a name="toocreate-a-virtual-network"></a><span data-ttu-id="5fa63-190">toocreate 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="5fa63-190">toocreate a virtual network</span></span>
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <span data-ttu-id="5fa63-191"><a name="subnets"></a>2. 다른 주소 공간 추가 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="5fa63-191"><a name="subnets"></a>2. Add additional address space and create subnets</span></span>
<span data-ttu-id="5fa63-192">VNet이 만들어지면 여기에 다른 주소 공간을 추가하고 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-192">You can add additional address space and create subnets once your VNet has been created.</span></span>

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <span data-ttu-id="5fa63-193"><a name="gatewaysubnet"></a>3. 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="5fa63-193"><a name="gatewaysubnet"></a>3. Create a gateway subnet</span></span>
<span data-ttu-id="5fa63-194">가상 네트워크 tooa 게이트웨이 연결 하기 전에 먼저 toocreate hello 게이트웨이 서브넷 tooconnect 원하는 가상 네트워크 toowhich hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-194">Before connecting your virtual network tooa gateway, you first need toocreate hello gateway subnet for hello virtual network toowhich you want tooconnect.</span></span> <span data-ttu-id="5fa63-195">가능 하면 것 최상의 toocreate 순서 tooprovide에 CIDR 블록/28/27 등의 사용 하는 게이트웨이 서브넷 충분 한 IP tooaccommodate 앞으로 추가 구성 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-195">If possible, it's best toocreate a gateway subnet using a CIDR block of /28 or /27 in order tooprovide enough IP addresses tooaccommodate additional future configuration requirements.</span></span>

<span data-ttu-id="5fa63-196">연습으로이 구성을 만드는 경우 참조 toothese [설정 예](#values) 게이트웨이 서브넷을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="5fa63-196">If you are creating this configuration as an exercise, refer toothese [Example settings](#values) when creating your gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a><span data-ttu-id="5fa63-197">게이트웨이 서브넷 toocreate</span><span class="sxs-lookup"><span data-stu-id="5fa63-197">toocreate a gateway subnet</span></span>
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <span data-ttu-id="5fa63-198"><a name="dns"></a>4. DNS 서버 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="5fa63-198"><a name="dns"></a>4. Specify a DNS server (optional)</span></span>
<span data-ttu-id="5fa63-199">DNS는 VNet 간 연결에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-199">DNS is not required for VNet-to-VNet connections.</span></span> <span data-ttu-id="5fa63-200">그러나 tooyour 배포 된 가상 네트워크 리소스에 대 한 toohave 이름 확인 하려는 경우에 DNS 서버를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-200">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="5fa63-201">이 설정을 사용 하면이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 hello DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-201">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="5fa63-202">DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-202">It does not create a DNS server.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="5fa63-203"><a name="VNetGateway"></a>5. 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="5fa63-203"><a name="VNetGateway"></a>5. Create a virtual network gateway</span></span>
<span data-ttu-id="5fa63-204">이 단계에서는 VNet에 대 한 hello 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-204">In this step, you create hello virtual network gateway for your VNet.</span></span> <span data-ttu-id="5fa63-205">게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-205">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span> <span data-ttu-id="5fa63-206">연습으로이 구성을 만드는 경우 toohello 참조할 수 있습니다 [설정 예](#values)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-206">If you are creating this configuration as an exercise, you can refer toohello [Example settings](#values).</span></span>

### <a name="toocreate-a-virtual-network-gateway"></a><span data-ttu-id="5fa63-207">가상 네트워크 게이트웨이 toocreate</span><span class="sxs-lookup"><span data-stu-id="5fa63-207">toocreate a virtual network gateway</span></span>
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <span data-ttu-id="5fa63-208"><a name="CreateTestVNet4"></a>6. TestVNet4 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="5fa63-208"><a name="CreateTestVNet4"></a>6. Create and configure TestVNet4</span></span>
<span data-ttu-id="5fa63-209">TestVNet1 구성한 경우 TestVNet4 TestVNet4의 hello 값을 대체 하는 hello 이전 단계를 반복 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-209">Once you've configured TestVNet1, create TestVNet4 by repeating hello previous steps, replacing hello values with those of TestVNet4.</span></span> <span data-ttu-id="5fa63-210">TestVNet1에 대 한 가상 네트워크 게이트웨이 hello TestVNet4 구성 하기 전에 만들기 끝날 때까지 toowait이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-210">You don't need toowait until hello virtual network gateway for TestVNet1 has finished creating before configuring TestVNet4.</span></span> <span data-ttu-id="5fa63-211">사용자가 직접 값을 사용 하는 hello 주소 공간을 tooconnect 원하는 Vnet hello를 사용 하 여 겹치지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-211">If you are using your own values, make sure that hello address spaces don't overlap with any of hello VNets that you want tooconnect to.</span></span>

## <span data-ttu-id="5fa63-212"><a name="TestVNet1Connection"></a>7. Hello TestVNet1 연결 구성</span><span class="sxs-lookup"><span data-stu-id="5fa63-212"><a name="TestVNet1Connection"></a>7. Configure hello TestVNet1 connection</span></span>
<span data-ttu-id="5fa63-213">Hello 가상 네트워크 게이트웨이 TestVNet1 및 TestVNet4 모두 완료 했을 때 게이트웨이 연결 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-213">When hello virtual network gateways for both TestVNet1 and TestVNet4 have completed, you can create your virtual network gateway connections.</span></span> <span data-ttu-id="5fa63-214">이 섹션에서는 VNet1 tooVNet4에서 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-214">In this section, you will create a connection from VNet1 tooVNet4.</span></span> <span data-ttu-id="5fa63-215">다음이 단계 동일 하 게 작동 hello에 Vnet에 대해서만 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-215">These steps work only for VNets in hello same subscription.</span></span> <span data-ttu-id="5fa63-216">Vnet 서로 다른 구독에 있는 경우 PowerShell toomake hello 연결을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-216">If your VNets are in different subscriptions, you must use PowerShell toomake hello connection.</span></span> <span data-ttu-id="5fa63-217">Hello 참조 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5fa63-217">See hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>

1. <span data-ttu-id="5fa63-218">**모든 리소스**, VNet에 대 한 toohello 가상 네트워크 게이트웨이 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-218">In **All resources**, navigate toohello virtual network gateway for your VNet.</span></span> <span data-ttu-id="5fa63-219">예를 들어 **TestVNet1GW**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-219">For example, **TestVNet1GW**.</span></span> <span data-ttu-id="5fa63-220">클릭 **TestVNet1GW** tooopen hello 가상 네트워크 게이트웨이 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-220">Click **TestVNet1GW** tooopen hello virtual network gateway blade.</span></span>
   
    <span data-ttu-id="5fa63-221">![연결 블레이드](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="5fa63-221">![Connections blade](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span></span>
2. <span data-ttu-id="5fa63-222">클릭 **+ 추가** tooopen hello **연결 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-222">Click **+Add** tooopen hello **Add connection** blade.</span></span>
3. <span data-ttu-id="5fa63-223">Hello에 **연결 추가** 블레이드에서 hello 이름 필드에 입력 한 연결에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-223">On hello **Add connection** blade, in hello name field, type a name for your connection.</span></span> <span data-ttu-id="5fa63-224">예를 들어, **TestVNet1toTestVNet4**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-224">For example, **TestVNet1toTestVNet4**.</span></span>
   
    <span data-ttu-id="5fa63-225">![연결 이름](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span><span class="sxs-lookup"><span data-stu-id="5fa63-225">![Connection name](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span></span>
4. <span data-ttu-id="5fa63-226">**연결 형식**은</span><span class="sxs-lookup"><span data-stu-id="5fa63-226">For **Connection type**.</span></span> <span data-ttu-id="5fa63-227">선택 **VNet 대 VNet** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-227">select **VNet-to-VNet** from hello dropdown.</span></span>
5. <span data-ttu-id="5fa63-228">hello **첫 번째 가상 네트워크 게이트웨이** 이 연결을 작성 하는 hello 지정 된 가상 네트워크 게이트웨이에서 자동으로 필드 값은 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-228">hello **First virtual network gateway** field value is automatically filled in because you are creating this connection from hello specified virtual network gateway.</span></span>
6. <span data-ttu-id="5fa63-229">hello **두 번째 가상 네트워크 게이트웨이** 필드는 hello VNet의 가상 네트워크 게이트웨이 hello 되도록 toocreate에 대 한 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-229">hello **Second virtual network gateway** field is hello virtual network gateway of hello VNet that you want toocreate a connection to.</span></span> <span data-ttu-id="5fa63-230">클릭 **다른 가상 네트워크 게이트웨이 선택** tooopen hello **가상 네트워크 게이트웨이 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-230">Click **Choose another virtual network gateway** tooopen hello **Choose virtual network gateway** blade.</span></span>
   
    <span data-ttu-id="5fa63-231">![연결 추가](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span><span class="sxs-lookup"><span data-stu-id="5fa63-231">![Add connection](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span></span>
7. <span data-ttu-id="5fa63-232">이 블레이드에 나열 된 보기 hello 가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="5fa63-232">View hello virtual network gateways that are listed on this blade.</span></span> <span data-ttu-id="5fa63-233">구독에 있는 가상 네트워크 게이트웨이만 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-233">Notice that only virtual network gateways that are in your subscription are listed.</span></span> <span data-ttu-id="5fa63-234">구독에 있지 않은 tooconnect tooa 가상 네트워크 게이트웨이 원하는 경우 hello를 사용 하십시오 [PowerShell 문서](vpn-gateway-vnet-vnet-rm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-234">If you want tooconnect tooa virtual network gateway that is not in your subscription, please use hello [PowerShell article](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> 
8. <span data-ttu-id="5fa63-235">Hello 가상 네트워크 게이트웨이를 tooconnect를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-235">Click hello virtual network gateway that you want tooconnect to.</span></span>
9. <span data-ttu-id="5fa63-236">Hello에 **공유 키** 필드 연결에 대 한 공유 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-236">In hello **Shared key** field, type a shared key for your connection.</span></span> <span data-ttu-id="5fa63-237">이 키를 생성하거나 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-237">You can generate or create this key yourself.</span></span> <span data-ttu-id="5fa63-238">사이트 간 연결에 사용 되는 hello 키가 수 정확히 hello 온-프레미스 장치 및 가상 네트워크 게이트웨이 연결에 대 한 동일한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-238">In a site-to-site connection, hello key you use would be exactly hello same for your on-premises device and your virtual network gateway connection.</span></span> <span data-ttu-id="5fa63-239">hello 개념은 비슷하지만 여기에서 점을 제외 하 고 tooanother 가상 네트워크 게이트웨이 연결 하려는 연결 tooa VPN 장치를 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-239">hello concept is similar here, except that rather than connecting tooa VPN device, you are connecting tooanother virtual network gateway.</span></span>
   
    <span data-ttu-id="5fa63-240">![공유 키](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="5fa63-240">![Shared key](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span></span>
10. <span data-ttu-id="5fa63-241">클릭 **확인** 에 hello hello 블레이드 toosave 맨 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-241">Click **OK** at hello bottom of hello blade toosave your changes.</span></span>

## <span data-ttu-id="5fa63-242"><a name="TestVNet4Connection"></a>8. Hello TestVNet4 연결 구성</span><span class="sxs-lookup"><span data-stu-id="5fa63-242"><a name="TestVNet4Connection"></a>8. Configure hello TestVNet4 connection</span></span>
<span data-ttu-id="5fa63-243">다음으로 TestVNet4 tooTestVNet1에서 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-243">Next, create a connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="5fa63-244">사용 하 여 hello 동일 toocreate hello 연결 TestVNet1 tooTestVNet4에서 사용 되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-244">Use hello same method that you used toocreate hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="5fa63-245">Hello를 사용 하면 동일한 키를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-245">Make sure that you use hello same shared key.</span></span>

## <span data-ttu-id="5fa63-246"><a name="VerifyConnection"></a>9. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="5fa63-246"><a name="VerifyConnection"></a>9. Verify your connection</span></span>
<span data-ttu-id="5fa63-247">Hello 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-247">Verify hello connection.</span></span> <span data-ttu-id="5fa63-248">각 가상 네트워크 게이트웨이에 대 한 않습니다 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-248">For each virtual network gateway, do hello following:</span></span>

1. <span data-ttu-id="5fa63-249">Hello 가상 네트워크 게이트웨이에 대 한 hello 블레이드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-249">Locate hello blade for hello virtual network gateway.</span></span> <span data-ttu-id="5fa63-250">예를 들어 **TestVNet4GW**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-250">For example, **TestVNet4GW**.</span></span> 
2. <span data-ttu-id="5fa63-251">Hello 가상 네트워크 게이트웨이 블레이드에서 클릭 **연결** tooview hello 연결 블레이드 hello 가상 네트워크 게이트웨이에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-251">On hello virtual network gateway blade, click **Connections** tooview hello connections blade for hello virtual network gateway.</span></span>

<span data-ttu-id="5fa63-252">Hello 연결을 표시 하 고 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-252">View hello connections and verify hello status.</span></span> <span data-ttu-id="5fa63-253">Hello 연결을 만들고 나타납니다 **Succeeded** 및 **연결 됨** hello 상태 값으로.</span><span class="sxs-lookup"><span data-stu-id="5fa63-253">Once hello connection is created, you will see **Succeeded** and **Connected** as hello Status values.</span></span>

<span data-ttu-id="5fa63-254">![성공](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span><span class="sxs-lookup"><span data-stu-id="5fa63-254">![Succeeded](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span></span>

<span data-ttu-id="5fa63-255">개별적으로 각 연결을 두 번 수 tooview hello 연결에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="5fa63-255">You can double-click each connection separately tooview more information about hello connection.</span></span>

<span data-ttu-id="5fa63-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span><span class="sxs-lookup"><span data-stu-id="5fa63-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span></span>

## <span data-ttu-id="5fa63-257"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="5fa63-257"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
<span data-ttu-id="5fa63-258">VNet 대 VNet 연결에 대 한 추가 정보에 대 한 hello FAQ 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-258">View hello FAQ details for additional information about VNet-to-VNet connections.</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5fa63-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fa63-259">Next steps</span></span>
<span data-ttu-id="5fa63-260">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-260">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5fa63-261">Hello 참조 [가상 컴퓨터 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa63-261">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
