---
title: "클래식 가상 네트워크 tooAzure 리소스 관리자 Vnet 연결: 포털 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 클래식 Vnet 및 VPN 게이트웨이와 hello 포털을 사용 하 여 리소스 관리자 Vnet 간의 VPN 연결"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a><span data-ttu-id="f4e28-103">Hello 포털을 사용 하 여 다양 한 배포 모델에 있는 가상 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="f4e28-103">Connect virtual networks from different deployment models using hello portal</span></span>

<span data-ttu-id="f4e28-104">이 문서 tooconnect 클래식 Vnet tooResource 관리자 Vnet tooallow 서로 hello 별도 배포 모델 toocommunicate에 배치 된 리소스를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="f4e28-105">이 문서의 단계 hello 주로 hello Azure 포털을 사용 하지만 PowerShell hello를 사용 하 여 hello 문서가이 목록에서 선택 하 여이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-105">hello steps in this article primarily use hello Azure portal, but you can also create this configuration using hello PowerShell by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4e28-106">포털</span><span class="sxs-lookup"><span data-stu-id="f4e28-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="f4e28-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e28-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="f4e28-108">비슷한 tooconnecting VNet tooan 온-프레미스 사이트 위치는 클래식 VNet tooa 리소스 관리자 VNet를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="f4e28-109">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="f4e28-110">다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="f4e28-111">으로 구성 된 hello 게이트웨이 동적 또는 경로 기반으로 연결 tooon 온-프레미스 네트워크에 이미 있는 Vnet을 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="f4e28-112">VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="f4e28-113">Vnet hello에 있는 경우 동일한 지역 경우가 있습니다 tooinstead VNet 피어 링을 사용 하 여 연결을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="f4e28-114">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="f4e28-115">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4e28-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="f4e28-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4e28-116">Prerequisites</span></span>

* <span data-ttu-id="f4e28-117">이 단계에서는 두 VNet이 이미 만들어졌다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-117">These steps assume that both VNets have already been created.</span></span> <span data-ttu-id="f4e28-118">이 문서를 사용 하는 연습으로 Vnet이 없는 경우 링크 가지 hello 단계 toohelp에서 만드는지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-118">If you are using this article as an exercise and don't have VNets, there are links in hello steps toohelp you create them.</span></span>
* <span data-ttu-id="f4e28-119">Vnet이 서로 겹치지 않을 hello에 대 한 hello 주소 범위 또는 해당 hello 게이트웨이에 연결할 수 있습니다 다른 연결에 대 한 hello를 사용 하 여 겹치는 범위를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-119">Verify that hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="f4e28-120">리소스 관리자와 서비스 관리 (클래식)에 대 한 hello 최신 PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-120">Install hello latest PowerShell cmdlets for both Resource Manager and Service Management (classic).</span></span> <span data-ttu-id="f4e28-121">이 문서에서는 Azure 포털 hello 및 PowerShell을 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-121">In this article, we use both hello Azure portal and PowerShell.</span></span> <span data-ttu-id="f4e28-122">PowerShell은 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 필요한 toocreate hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-122">PowerShell is required toocreate hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-123">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-123">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <span data-ttu-id="f4e28-124"><a name="values"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="f4e28-124"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="f4e28-125">이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-125">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="f4e28-126">**클래식 VNet**</span><span class="sxs-lookup"><span data-stu-id="f4e28-126">**Classic VNet**</span></span>

<span data-ttu-id="f4e28-127">VNet 이름 = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-127">VNet name = ClassicVNet</span></span> <br>
<span data-ttu-id="f4e28-128">Address space = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f4e28-128">Address space = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="f4e28-129">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="f4e28-129">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="f4e28-130">Resource Group = ClassicRG</span><span class="sxs-lookup"><span data-stu-id="f4e28-130">Resource Group = ClassicRG</span></span> <br>
<span data-ttu-id="f4e28-131">Location = West US</span><span class="sxs-lookup"><span data-stu-id="f4e28-131">Location = West US</span></span> <br>
<span data-ttu-id="f4e28-132">GatewaySubnet = 10.0.0.32/28</span><span class="sxs-lookup"><span data-stu-id="f4e28-132">GatewaySubnet = 10.0.0.32/28</span></span> <br>
<span data-ttu-id="f4e28-133">Local site = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="f4e28-133">Local site = RMVNetLocal</span></span> <br>

<span data-ttu-id="f4e28-134">**Resource Manager VNet**</span><span class="sxs-lookup"><span data-stu-id="f4e28-134">**Resource Manager VNet**</span></span>

<span data-ttu-id="f4e28-135">VNet 이름 = RMVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-135">VNet name = RMVNet</span></span> <br>
<span data-ttu-id="f4e28-136">Address space = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f4e28-136">Address space = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="f4e28-137">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="f4e28-137">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="f4e28-138">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="f4e28-138">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="f4e28-139">Resource Group = RG1</span><span class="sxs-lookup"><span data-stu-id="f4e28-139">Resource Group = RG1</span></span> <br>
<span data-ttu-id="f4e28-140">Location = East US</span><span class="sxs-lookup"><span data-stu-id="f4e28-140">Location = East US</span></span> <br>
<span data-ttu-id="f4e28-141">Virtual network gateway name = RMGateway</span><span class="sxs-lookup"><span data-stu-id="f4e28-141">Virtual network gateway name = RMGateway</span></span> <br>
<span data-ttu-id="f4e28-142">Gateway type = VPN</span><span class="sxs-lookup"><span data-stu-id="f4e28-142">Gateway type = VPN</span></span> <br>
<span data-ttu-id="f4e28-143">VPN type = Route-based</span><span class="sxs-lookup"><span data-stu-id="f4e28-143">VPN type = Route-based</span></span> <br>
<span data-ttu-id="f4e28-144">게이트웨이 공용 IP 주소 이름 = rmgwpip</span><span class="sxs-lookup"><span data-stu-id="f4e28-144">Gateway Public IP address name = rmgwpip</span></span> <br>
<span data-ttu-id="f4e28-145">Local network gateway = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="f4e28-145">Local network gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="f4e28-146">연결 이름 = RMtoClassic</span><span class="sxs-lookup"><span data-stu-id="f4e28-146">Connection name = RMtoClassic</span></span>

### <a name="connection-overview"></a><span data-ttu-id="f4e28-147">연결 개요</span><span class="sxs-lookup"><span data-stu-id="f4e28-147">Connection overview</span></span>

<span data-ttu-id="f4e28-148">이 구성에 대 한 hello 가상 네트워크 간에 IPsec/IKE VPN 터널을 통해 VPN 게이트웨이 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-148">For this configuration, you create a VPN gateway connection over an IPsec/IKE VPN tunnel between hello virtual networks.</span></span> <span data-ttu-id="f4e28-149">또는 로컬 네트워크에 연결 하는 hello 사용 하 여 겹치는 VNet 범위 중 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-149">Make sure that none of your VNet ranges overlap with each other, or with any of hello local networks that they connect to.</span></span>

<span data-ttu-id="f4e28-150">hello 다음 표에서 hello 예제 Vnet 및 로컬 사이트 정의 하는 방법의 예:</span><span class="sxs-lookup"><span data-stu-id="f4e28-150">hello following table shows an example of how hello example VNets and local sites are defined:</span></span>

| <span data-ttu-id="f4e28-151">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="f4e28-151">Virtual Network</span></span> | <span data-ttu-id="f4e28-152">주소 공간</span><span class="sxs-lookup"><span data-stu-id="f4e28-152">Address Space</span></span> | <span data-ttu-id="f4e28-153">지역</span><span class="sxs-lookup"><span data-stu-id="f4e28-153">Region</span></span> | <span data-ttu-id="f4e28-154">Toolocal 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="f4e28-154">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4e28-155">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-155">ClassicVNet</span></span> |<span data-ttu-id="f4e28-156">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="f4e28-156">(10.0.0.0/24)</span></span> |<span data-ttu-id="f4e28-157">미국 서부</span><span class="sxs-lookup"><span data-stu-id="f4e28-157">West US</span></span> | <span data-ttu-id="f4e28-158">RMVNetLocal(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="f4e28-158">RMVNetLocal (192.168.0.0/16)</span></span> |
| <span data-ttu-id="f4e28-159">RMVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-159">RMVNet</span></span> | <span data-ttu-id="f4e28-160">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="f4e28-160">(192.168.0.0/16)</span></span> |<span data-ttu-id="f4e28-161">미국 동부</span><span class="sxs-lookup"><span data-stu-id="f4e28-161">East US</span></span> |<span data-ttu-id="f4e28-162">ClassicVNetLocal(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="f4e28-162">ClassicVNetLocal (10.0.0.0/24)</span></span> |

## <span data-ttu-id="f4e28-163"><a name="classicvnet"></a>1. Hello 클래식 VNet 설정 구성</span><span class="sxs-lookup"><span data-stu-id="f4e28-163"><a name="classicvnet"></a>1. Configure hello classic VNet settings</span></span>

<span data-ttu-id="f4e28-164">이 섹션에서는 만들 hello 로컬 네트워크 (사이트 로컬 사이트) 및 클래식 VNet에 대 한 가상 네트워크 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-164">In this section, you create hello local network (local site) and hello virtual network gateway for your classic VNet.</span></span> <span data-ttu-id="f4e28-165">클래식 VNet이 없는 연습으로 다음이 단계를 실행 하는 경우 사용 하 여 VNet을 만들 수 있습니다 [이 여기서](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) 및 hello [예제](#values) 위에서 설정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-165">If you don't have a classic VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) and hello [Example](#values) settings values from above.</span></span>

<span data-ttu-id="f4e28-166">Hello 포털 toocreate 클래식 가상 네트워크를 사용할 때는 hello hello 옵션 toocreate 클래식 가상 네트워크 나타나지 않으면 그렇지 않으면 다음 단계를 사용 하 여 toohello 가상 네트워크 블레이드를 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-166">When using hello portal toocreate a classic virtual network, you must navigate toohello virtual network blade by using hello following steps, otherwise hello option toocreate a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="f4e28-167">Hello 클릭 tooopen hello 'New' 블레이드 '+'.</span><span class="sxs-lookup"><span data-stu-id="f4e28-167">Click hello '+' tooopen hello 'New' blade.</span></span>
2. <span data-ttu-id="f4e28-168">' 가상 네트워크 ' hello 'hello 마켓플레이스' 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-168">In hello 'Search hello marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="f4e28-169">네트워킹을 대신 선택-> 가상 네트워크를 가져올 수 없습니다 hello 옵션 toocreate 클래식 VNet 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-169">If you instead, select Networking -> Virtual Network, you will not get hello option toocreate a classic VNet.</span></span>
3. <span data-ttu-id="f4e28-170">' 가상 네트워크 ' hello 반환 된 목록에서에서 찾은 tooopen hello 가상 네트워크 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-170">Locate 'Virtual Network' from hello returned list and click it tooopen hello Virtual Network blade.</span></span> 
4. <span data-ttu-id="f4e28-171">가상 네트워크 블레이드에서 hello '클래식' toocreate 클래식 VNet을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-171">On hello virtual network blade, select 'Classic' toocreate a classic VNet.</span></span> 

<span data-ttu-id="f4e28-172">VNet VPN 게이트웨이 통해 이미 있는 경우 해당 hello 게이트웨이 동적 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-172">If you already have a VNet with a VPN gateway, verify that hello gateway is Dynamic.</span></span> <span data-ttu-id="f4e28-173">정적 이면 먼저 hello VPN 게이트웨이 삭제 하십시오 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-173">If it's Static, you must first delete hello VPN gateway, then proceed.</span></span>

<span data-ttu-id="f4e28-174">스크린샷은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-174">Screenshots are provided as examples.</span></span> <span data-ttu-id="f4e28-175">있는지 tooreplace hello 사용 하 여 값을 직접 수행 하거나 사용할 hello [예제](#values) 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-175">Be sure tooreplace hello values with your own, or use hello [Example](#values) values.</span></span>

### <a name="part-1---configure-hello-local-site"></a><span data-ttu-id="f4e28-176">1 부-hello 로컬 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-176">Part 1 - Configure hello local site</span></span>

<span data-ttu-id="f4e28-177">열기 hello [Azure 포털](https://ms.portal.azure.com) Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-177">Open hello [Azure portal](https://ms.portal.azure.com) and sign in with your Azure account.</span></span>

1. <span data-ttu-id="f4e28-178">너무 이동**모든 리소스** hello 찾습니다 **ClassicVNet** hello 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-178">Navigate too**All resources** and locate hello **ClassicVNet** in hello list.</span></span>
2. <span data-ttu-id="f4e28-179">Hello에 **개요** 블레이드 hello **VPN 연결** 섹션에서 hello **게이트웨이** 그래픽 toocreate 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-179">On hello **Overview** blade, in hello **VPN connections** section, click hello **Gateway** graphic toocreate a gateway.</span></span>

    <span data-ttu-id="f4e28-180">![VPN 게이트웨이 구성](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "VPN 게이트웨이 구성")</span><span class="sxs-lookup"><span data-stu-id="f4e28-180">![Configure a VPN gateway](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configure a VPN gateway")</span></span>
3. <span data-ttu-id="f4e28-181">Hello에 **새 VPN 연결** 블레이드에서 대 한 **연결 유형**선택, **사이트 간**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-181">On hello **New VPN Connection** blade, for **Connection type**, select **Site-to-site**.</span></span>
4. <span data-ttu-id="f4e28-182">**로컬 사이트**로 **필요한 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-182">For **Local site**, click **Configure required settings**.</span></span> <span data-ttu-id="f4e28-183">Hello 열립니다 **로컬 사이트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-183">This opens hello **Local site** blade.</span></span>
5. <span data-ttu-id="f4e28-184">Hello에 **로컬 사이트** 블레이드에서 이름 toorefer toohello 리소스 관리자 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-184">On hello **Local site** blade, create a name toorefer toohello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-185">예: 'RMVNetLocal'.</span><span class="sxs-lookup"><span data-stu-id="f4e28-185">For example, 'RMVNetLocal'.</span></span>
6. <span data-ttu-id="f4e28-186">리소스 관리자 VNet hello에 대 한 hello VPN 게이트웨이 공용 IP 주소를 이미 있으면 hello 값을 사용 하 여 hello에 대 한 **VPN 게이트웨이 IP 주소** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-186">If hello VPN gateway for hello Resource Manager VNet already has a Public IP address, use hello value for hello **VPN gateway IP address** field.</span></span> <span data-ttu-id="f4e28-187">이 단계를 연습으로 수행하는 경우 또는 아직 Resource Manager VNet에 대한 가상 네트워크 게이트웨이가 없는 경우 자리 표시자 IP 주소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-187">If you are doing these steps as an exercise, or don't yet have a virtual network gateway for your Resource Manager VNet, you can make up a placeholder IP address.</span></span> <span data-ttu-id="f4e28-188">Hello 자리 표시자 IP 주소는 유효한 형식의 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-188">Make sure that hello placeholder IP address uses a valid format.</span></span> <span data-ttu-id="f4e28-189">이상에서는 hello hello 리소스 관리자 가상 네트워크 게이트웨이의 공용 IP 주소와 hello 자리 표시자 IP 주소를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-189">Later, you replace hello placeholder IP address with hello Public IP address of hello Resource Manager virtual network gateway.</span></span>
7. <span data-ttu-id="f4e28-190">에 대 한 **클라이언트 주소 공간**, 리소스 관리자 VNet hello에 대 한 hello 가상 네트워크 IP 주소 공간에 대 한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-190">For **Client Address Space**, use hello values for hello virtual network IP address spaces for hello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-191">이 설정은 사용 되는 toospecify hello 주소 공간 tooroute toohello 리소스 관리자 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-191">This setting is used toospecify hello address spaces tooroute toohello Resource Manager virtual network.</span></span>
8. <span data-ttu-id="f4e28-192">클릭 **확인** toosave 값 hello 돌아와 toohello **새 VPN 연결** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-192">Click **OK** toosave hello values and return toohello **New VPN Connection** blade.</span></span>

### <a name="part-2---create-hello-virtual-network-gateway"></a><span data-ttu-id="f4e28-193">2 부-hello 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-193">Part 2 - Create hello virtual network gateway</span></span>

1. <span data-ttu-id="f4e28-194">Hello에 **새 VPN 연결** 블레이드, 선택 hello **게이트웨이 즉시 만들기** 확인란을 클릭 하 고 **선택적 게이트웨이 구성** tooopen hello  **게이트웨이 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-194">On hello **New VPN Connection** blade, select hello **Create gateway immediately** checkbox and click **Optional gateway configuration** tooopen hello **Gateway configuration** blade.</span></span> 

    <span data-ttu-id="f4e28-195">![게이트웨이 구성 블레이드 열기](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "게이트웨이 구성 블레이드 열기")</span><span class="sxs-lookup"><span data-stu-id="f4e28-195">![Open gateway configuration blade](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Open gateway configuration blade")</span></span>
2. <span data-ttu-id="f4e28-196">클릭 **서브넷-필요한 설정 구성** tooopen hello **서브넷 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-196">Click **Subnet - Configure required settings** tooopen hello **Add subnet** blade.</span></span> <span data-ttu-id="f4e28-197">hello **이름** hello 필요한 값으로 이미 구성 되어 **GatewaySubnet**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-197">hello **Name** is already configured with hello required value **GatewaySubnet**.</span></span>
3. <span data-ttu-id="f4e28-198">hello **주소 범위** toohello 범위 hello 게이트웨이 서브넷에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-198">hello **Address range** refers toohello range for hello gateway subnet.</span></span> <span data-ttu-id="f4e28-199">게이트웨이 서브넷을 /29 주소 범위(주소 3개)로 만들 수 있지만 더 많은 IP 주소를 포함하는 게이트웨이 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-199">Although you can create a gateway subnet with a /29 address range (3 addresses), we recommend creating a gateway subnet that contains more IP addresses.</span></span> <span data-ttu-id="f4e28-200">그러면 사용 가능한 IP 주소가 필요할 수 있는 향후 구성을 수용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-200">This will accommodate future configurations that may require more available IP addresses.</span></span> <span data-ttu-id="f4e28-201">가능하면 /27 또는 /28을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-201">If possible, use /27 or /28.</span></span> <span data-ttu-id="f4e28-202">다음이 단계를 연습으로 사용 하는 경우에 toohello을 참조할 수 있습니다 [예제](#values) 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-202">If you are using these steps as an exercise, you can refer toohello [Example](#values) values.</span></span> <span data-ttu-id="f4e28-203">클릭 **확인** toocreate hello 게이트웨이 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-203">Click **OK** toocreate hello gateway subnet.</span></span>
4. <span data-ttu-id="f4e28-204">Hello에 **게이트웨이 구성** 블레이드에서 **크기** toohello 게이트웨이 SKU를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-204">On hello **Gateway configuration** blade, **Size** refers toohello gateway SKU.</span></span> <span data-ttu-id="f4e28-205">VPN 게이트웨이에 대 한 hello 게이트웨이 SKU를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-205">Select hello gateway SKU for your VPN gateway.</span></span>
5. <span data-ttu-id="f4e28-206">Hello 확인 **라우팅 유형** 은 **동적**, 클릭 **확인** tooreturn toohello **새 VPN 연결** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-206">Verify hello **Routing Type** is **Dynamic**, then click **OK** tooreturn toohello **New VPN Connection** blade.</span></span>
6. <span data-ttu-id="f4e28-207">Hello에 **새 VPN 연결** 블레이드에서 클릭 **확인** toobegin VPN 게이트웨이 만들기.</span><span class="sxs-lookup"><span data-stu-id="f4e28-207">On hello **New VPN Connection** blade, click **OK** toobegin creating your VPN gateway.</span></span> <span data-ttu-id="f4e28-208">VPN 게이트웨이 만들기 too45 분 toocomplete 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-208">Creating a VPN gateway can take up too45 minutes toocomplete.</span></span>

### <span data-ttu-id="f4e28-209"><a name="ip"></a>-3 부 복사 hello 가상 네트워크 게이트웨이 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="f4e28-209"><a name="ip"></a>Part 3 - Copy hello virtual network gateway Public IP address</span></span>

<span data-ttu-id="f4e28-210">Hello 가상 네트워크 게이트웨이 만든 후에 hello 게이트웨이 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-210">After hello virtual network gateway has been created, you can view hello gateway IP address.</span></span> 

1. <span data-ttu-id="f4e28-211">Tooyour 이동 클래식 VNet 및 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-211">Navigate tooyour classic VNet, and click **Overview**.</span></span>
2. <span data-ttu-id="f4e28-212">클릭 **VPN 연결** tooopen hello VPN 연결 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-212">Click **VPN connections** tooopen hello VPN connections blade.</span></span> <span data-ttu-id="f4e28-213">Hello VPN 연결 블레이드에서 hello 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-213">On hello VPN connections blade, you can view hello Public IP address.</span></span> <span data-ttu-id="f4e28-214">Tooyour 가상 네트워크 게이트웨이 할당 하는 hello 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-214">This is hello Public IP address assigned tooyour virtual network gateway.</span></span> 
3. <span data-ttu-id="f4e28-215">적어 두거나 hello IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-215">Write down or copy hello IP address.</span></span> <span data-ttu-id="f4e28-216">나중 단계에서 Resource Manager 로컬 네트워크 게이트웨이 구성 설정 관련 작업을 수행할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-216">You use it in later steps when you work with your Resource Manager local network gateway configuration settings.</span></span> <span data-ttu-id="f4e28-217">게이트웨이 연결의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-217">You can also view hello status of your gateway connections.</span></span> <span data-ttu-id="f4e28-218">사용자가 만든 공지 hello 로컬 네트워크 사이트 '연결'로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-218">Notice hello local network site you created is listed as 'Connecting'.</span></span> <span data-ttu-id="f4e28-219">연결을 만든 후 hello 상태가 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-219">hello status will change after you have created your connections.</span></span>
4. <span data-ttu-id="f4e28-220">Hello 게이트웨이 IP 주소를 복사한 후 hello 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-220">Close hello blade after copying hello gateway IP address.</span></span>

## <span data-ttu-id="f4e28-221"><a name="rmvnet"></a>2. Hello 리소스 관리자 VNet 설정 구성</span><span class="sxs-lookup"><span data-stu-id="f4e28-221"><a name="rmvnet"></a>2. Configure hello Resource Manager VNet settings</span></span>

<span data-ttu-id="f4e28-222">이 섹션에서는 가상 네트워크 게이트웨이 hello와 만들어야 hello 로컬 네트워크 게이트웨이 리소스 관리자 VNet에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-222">In this section, you create hello virtual network gateway and hello local network gateway for your Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-223">리소스 관리자 VNet이 없는 연습으로 다음이 단계를 실행 하는 경우 사용 하 여 VNet을 만들 수 있습니다 [이 여기서](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 및 hello [예제](#values) 위에서 설정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-223">If you don't have a Resource Manager VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and hello [Example](#values) settings values from above.</span></span>

<span data-ttu-id="f4e28-224">스크린샷은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-224">Screenshots are provided as examples.</span></span> <span data-ttu-id="f4e28-225">있는지 tooreplace hello 사용 하 여 값을 직접 수행 하거나 사용할 hello [예제](#values) 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-225">Be sure tooreplace hello values with your own, or use hello [Example](#values) values.</span></span>

### <a name="part-1---create-a-gateway-subnet"></a><span data-ttu-id="f4e28-226">1부 - 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-226">Part 1 - Create a gateway subnet</span></span>

<span data-ttu-id="f4e28-227">가상 네트워크 게이트웨이 만들기 전에 먼저 toocreate hello 게이트웨이 서브넷을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-227">Before creating a virtual network gateway, you first need toocreate hello gateway subnet.</span></span> <span data-ttu-id="f4e28-228">CIDR 개수가 /28 이상인 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-228">Create a gateway subnet with CIDR count of /28 or larger.</span></span> <span data-ttu-id="f4e28-229">(/27, /26 등)</span><span class="sxs-lookup"><span data-stu-id="f4e28-229">(/27, /26, etc.)</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a><span data-ttu-id="f4e28-230">2부 - 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-230">Part 2 - Create a virtual network gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <span data-ttu-id="f4e28-231"><a name="createlng"></a>3부 - 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-231"><a name="createlng"></a>Part 3 - Create a local network gateway</span></span>

<span data-ttu-id="f4e28-232">로컬 네트워크 게이트웨이 hello hello 주소 범위 및 클래식 VNet 및 해당 가상 네트워크 게이트웨이에 연결 된 hello 공용 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-232">hello local network gateway specifies hello address range and hello Public IP address associated with your classic VNet and its virtual network gateway.</span></span>

<span data-ttu-id="f4e28-233">다음이 단계를 연습으로 수행 하는 경우에 toothese 설정을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-233">If you are doing these steps as an exercise, refer toothese settings:</span></span>

| <span data-ttu-id="f4e28-234">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="f4e28-234">Virtual Network</span></span> | <span data-ttu-id="f4e28-235">주소 공간</span><span class="sxs-lookup"><span data-stu-id="f4e28-235">Address Space</span></span> | <span data-ttu-id="f4e28-236">지역</span><span class="sxs-lookup"><span data-stu-id="f4e28-236">Region</span></span> | <span data-ttu-id="f4e28-237">Toolocal 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="f4e28-237">Connects toolocal network site</span></span> |<span data-ttu-id="f4e28-238">게이트웨이 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="f4e28-238">Gateway Public IP address</span></span>|
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4e28-239">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-239">ClassicVNet</span></span> |<span data-ttu-id="f4e28-240">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="f4e28-240">(10.0.0.0/24)</span></span> |<span data-ttu-id="f4e28-241">미국 서부</span><span class="sxs-lookup"><span data-stu-id="f4e28-241">West US</span></span> | <span data-ttu-id="f4e28-242">RMVNetLocal(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="f4e28-242">RMVNetLocal (192.168.0.0/16)</span></span> |<span data-ttu-id="f4e28-243">hello toohello ClassicVNet 게이트웨이에 할당 된 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="f4e28-243">hello Public IP address that is assigned toohello ClassicVNet gateway</span></span>|
| <span data-ttu-id="f4e28-244">RMVNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-244">RMVNet</span></span> | <span data-ttu-id="f4e28-245">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="f4e28-245">(192.168.0.0/16)</span></span> |<span data-ttu-id="f4e28-246">미국 동부</span><span class="sxs-lookup"><span data-stu-id="f4e28-246">East US</span></span> |<span data-ttu-id="f4e28-247">ClassicVNetLocal(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="f4e28-247">ClassicVNetLocal (10.0.0.0/24)</span></span> |<span data-ttu-id="f4e28-248">hello toohello RMVNet 게이트웨이에 할당 된 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-248">hello Public IP address that is assigned toohello RMVNet gateway.</span></span>|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <span data-ttu-id="f4e28-249"><a name="modifylng"></a>3. Hello 클래식 VNet 로컬 사이트 설정 수정</span><span class="sxs-lookup"><span data-stu-id="f4e28-249"><a name="modifylng"></a>3. Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="f4e28-250">이 섹션에서는 hello 리소스 관리자 VPN 게이트웨이 IP 주소를 사용 하 여 hello 로컬 사이트 설정을 지정 하는 때 사용한 hello 자리 표시자 IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-250">In this section, you replace hello placeholder IP address that you used when specifying hello local site settings, with hello Resource Manager VPN gateway IP address.</span></span> <span data-ttu-id="f4e28-251">이 섹션에서는 hello 클래식 (SM) PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-251">This section uses hello classic (SM) PowerShell cmdlets.</span></span>

1. <span data-ttu-id="f4e28-252">Azure 포털 hello toohello 클래식 가상 네트워크를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-252">In hello Azure portal, navigate toohello classic virtual network.</span></span>
2. <span data-ttu-id="f4e28-253">가상 네트워크에 대 한 hello 블레이드에서 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-253">On hello blade for your virtual network, click **Overview**.</span></span>
3. <span data-ttu-id="f4e28-254">Hello에 **VPN 연결** 섹션에서 hello 그래픽에 로컬 사이트의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-254">In hello **VPN connections** section, click hello name of your local site in hello graphic.</span></span>

    <span data-ttu-id="f4e28-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN 연결")</span><span class="sxs-lookup"><span data-stu-id="f4e28-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN Connections")</span></span>
4. <span data-ttu-id="f4e28-256">Hello에 **사이트 간 VPN 연결** 블레이드에서 hello hello 사이트 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-256">On hello **Site-to-site VPN connections** blade, click hello name of hello site.</span></span>

    <span data-ttu-id="f4e28-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "로컬 사이트 이름")</span><span class="sxs-lookup"><span data-stu-id="f4e28-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Local site name")</span></span>
5. <span data-ttu-id="f4e28-258">로컬 사이트에 대 한 연결 블레이드에서 hello hello 로컬 사이트 tooopen hello의 hello 이름을 클릭 **로컬 사이트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-258">On hello connection blade for your local site, click hello name of hello local site tooopen hello **Local site** blade.</span></span>

    <span data-ttu-id="f4e28-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "로컬 사이트 열기")</span><span class="sxs-lookup"><span data-stu-id="f4e28-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Open local site")</span></span>
6. <span data-ttu-id="f4e28-260">Hello에 **로컬 사이트** 블레이드, replace hello **VPN 게이트웨이 IP 주소** hello 리소스 관리자 게이트웨이의 hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-260">On hello **Local site** blade, replace hello **VPN gateway IP address** with hello IP address of hello Resource Manager gateway.</span></span>

    <span data-ttu-id="f4e28-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "게이트웨이 IP 주소")</span><span class="sxs-lookup"><span data-stu-id="f4e28-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Gateway IP address")</span></span>
7. <span data-ttu-id="f4e28-262">클릭 **확인** tooupdate hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-262">Click **OK** tooupdate hello IP address.</span></span>

## <span data-ttu-id="f4e28-263"><a name="RMtoclassic"></a>4. 리소스 관리자 tooclassic 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-263"><a name="RMtoclassic"></a>4. Create Resource Manager tooclassic connection</span></span>

<span data-ttu-id="f4e28-264">리소스 관리자 VNet hello에서 hello 연결을 구성 하면이 단계에서는 Azure 포털 hello toohello 클래식 VNet 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-264">In these steps, you configure hello connection from hello Resource Manager VNet toohello classic VNet using hello Azure portal.</span></span>

1. <span data-ttu-id="f4e28-265">**모든 리소스**, hello 로컬 네트워크 게이트웨이 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-265">In **All resources**, locate hello local network gateway.</span></span> <span data-ttu-id="f4e28-266">이 예에서 hello 로컬 네트워크 게이트웨이 **ClassicVNetLocal**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-266">In our example, hello local network gateway is **ClassicVNetLocal**.</span></span>
2. <span data-ttu-id="f4e28-267">클릭 **구성** hello에 대 한 hello VPN 게이트웨이 IP 주소 값을 hello 인지 확인 클래식 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-267">Click **Configuration** and verify that hello IP address value is hello VPN gateway for hello classic VNet.</span></span> <span data-ttu-id="f4e28-268">필요한 경우 업데이트하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-268">Update, if needed, then click **Save**.</span></span> <span data-ttu-id="f4e28-269">닫기 hello 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-269">Close hello blade.</span></span>
3. <span data-ttu-id="f4e28-270">**모든 리소스**, hello 로컬 네트워크 게이트웨이 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-270">In **All resources**, click hello local network gateway.</span></span>
4. <span data-ttu-id="f4e28-271">클릭 **연결** tooopen hello 연결 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-271">Click **Connections** tooopen hello Connections blade.</span></span>
5. <span data-ttu-id="f4e28-272">Hello에 **연결** 블레이드에서 클릭  **+**  tooadd 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-272">On hello **Connections** blade, click **+** tooadd a connection.</span></span>
6. <span data-ttu-id="f4e28-273">Hello에 **연결 추가** 블레이드, 이름 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-273">On hello **Add connection** blade, name hello connection.</span></span> <span data-ttu-id="f4e28-274">예: 'RMtoClassic'.</span><span class="sxs-lookup"><span data-stu-id="f4e28-274">For example, 'RMtoClassic'.</span></span>
7. <span data-ttu-id="f4e28-275">**사이트 간**이 블레이드에 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-275">**Site-to-Site** is already selected on this blade.</span></span>
8. <span data-ttu-id="f4e28-276">이 사이트와 tooassociate 원하는 hello 가상 네트워크 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-276">Select hello virtual network gateway that you want tooassociate with this site.</span></span>
9. <span data-ttu-id="f4e28-277">**공유 키**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-277">Create a **shared key**.</span></span> <span data-ttu-id="f4e28-278">이 키는 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 만든 hello 연결에도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-278">This key is also used in hello connection that you create from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-279">Hello 키를 생성 하거나 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-279">You can generate hello key or make one up.</span></span> <span data-ttu-id="f4e28-280">이 예제에서는 'abc123'을 사용했지만 좀 더 복잡한 항목을 사용할 수 있고 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-280">In our example, we use 'abc123', but you can (and should) use something more complex.</span></span>
10. <span data-ttu-id="f4e28-281">클릭 **확인** toocreate hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-281">Click **OK** toocreate hello connection.</span></span>

##<span data-ttu-id="f4e28-282"><a name="classictoRM"></a>5. 클래식 tooResource에 대 한 연결 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-282"><a name="classictoRM"></a>5. Create classic tooResource Manager connection</span></span>

<span data-ttu-id="f4e28-283">이 단계에서는 hello 연결 hello 클래식 VNet toohello 리소스 관리자 VNet을에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-283">In these steps, you configure hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-284">이러한 단계에는 PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-284">These steps require PowerShell.</span></span> <span data-ttu-id="f4e28-285">Hello 포털에서이 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-285">You can't create this connection in hello portal.</span></span> <span data-ttu-id="f4e28-286">다운로드 하 고 hello 클래식 (SM)와 관리자 RM (리소스) PowerShell cmdlet은 모두 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-286">Make sure you have downloaded and installed both hello classic (SM) and Resource Manager (RM) PowerShell cmdlets.</span></span>

### <a name="1-connect-tooyour-azure-account"></a><span data-ttu-id="f4e28-287">1. Tooyour Azure 계정 연결</span><span class="sxs-lookup"><span data-stu-id="f4e28-287">1. Connect tooyour Azure account</span></span>

<span data-ttu-id="f4e28-288">관리자 권한을 가진 hello PowerShell 콘솔을 열고 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-288">Open hello PowerShell console with elevated rights and log in tooyour Azure account.</span></span> <span data-ttu-id="f4e28-289">hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-289">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="f4e28-290">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정은 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-290">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

```powershell
Login-AzureRmAccount
```
   
<span data-ttu-id="f4e28-291">둘 이상의 구독이 있는 경우 Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-291">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f4e28-292">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-292">Specify hello subscription that you want toouse.</span></span> 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

<span data-ttu-id="f4e28-293">프로그램 Azure 계정 toouse hello 클래식 PowerShell cmdlet (SM)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-293">Add your Azure Account toouse hello classic PowerShell cmdlets (SM).</span></span> <span data-ttu-id="f4e28-294">toodo 따라서 hello 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-294">toodo so, you can use hello following command:</span></span>

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a><span data-ttu-id="f4e28-295">2. 보기 hello 네트워크 구성 파일 값</span><span class="sxs-lookup"><span data-stu-id="f4e28-295">2. View hello network configuration file values</span></span>

<span data-ttu-id="f4e28-296">Hello Azure 포털에서에서 VNet을 만들 때 Azure를 사용 하는 hello 전체 이름을 hello Azure 포털에에서 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-296">When you create a VNet in hello Azure portal, hello full name that Azure uses is not visible in hello Azure portal.</span></span> <span data-ttu-id="f4e28-297">예를 들어 hello Azure 포털에에서 'ClassicVNet' 라는 toobe 나타나는 VNet 있을 수는 훨씬 더 긴 이름을 hello 네트워크 구성 파일에서.</span><span class="sxs-lookup"><span data-stu-id="f4e28-297">For example, a VNet that appears toobe named 'ClassicVNet' in hello Azure portal may have a much longer name in hello network configuration file.</span></span> <span data-ttu-id="f4e28-298">hello 이름이 같을 수 있습니다: ' 그룹 ClassicRG ClassicVNet'.</span><span class="sxs-lookup"><span data-stu-id="f4e28-298">hello name might look something like: 'Group ClassicRG ClassicVNet'.</span></span> <span data-ttu-id="f4e28-299">이 단계에서는 hello 네트워크 구성 파일, 보기 hello 값 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-299">In these steps, you download hello network configuration file and view hello values.</span></span>

<span data-ttu-id="f4e28-300">컴퓨터에 디렉터리를 만들고 hello 네트워크 구성 파일 toohello 디렉터리를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-300">Create a directory on your computer and then export hello network configuration file toohello directory.</span></span> <span data-ttu-id="f4e28-301">이 예제에서는 hello 네트워크 구성 파일에는 내보낸된 tooC:\AzureNet은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-301">In this example, hello network configuration file is exported tooC:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="f4e28-302">클래식 VNet에 대 한 텍스트 편집기 및 보기 hello 이름으로 hello 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-302">Open hello file with a text editor and view hello name for your classic VNet.</span></span> <span data-ttu-id="f4e28-303">PowerShell cmdlet을 실행 하는 경우 hello 이름을 hello 네트워크 구성 파일에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-303">Use hello names in hello network configuration file when running your PowerShell cmdlets.</span></span>

- <span data-ttu-id="f4e28-304">VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-304">VNet names are listed as **VirtualNetworkSite name =**</span></span>
- <span data-ttu-id="f4e28-305">사이트 이름은 **LocalNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-305">Site names are listed as **LocalNetworkSite name=**</span></span>

### <a name="3-create-hello-connection"></a><span data-ttu-id="f4e28-306">3. Hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f4e28-306">3. Create hello connection</span></span>

<span data-ttu-id="f4e28-307">Hello 공유 키를 설정 하 고 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-307">Set hello shared key and create hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="f4e28-308">Hello 포털을 사용 하 여 hello 공유 키를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-308">You cannot set hello shared key using hello portal.</span></span> <span data-ttu-id="f4e28-309">Hello 클래식 버전의 hello PowerShell cmdlet 사용 하 여 로그인 하는 동안 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-309">Make sure you run these steps while logged in using hello classic version of hello PowerShell cmdlets.</span></span> <span data-ttu-id="f4e28-310">toodo를 사용 하 여 **Add-azureaccount**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-310">toodo so, use **Add-AzureAccount**.</span></span> <span data-ttu-id="f4e28-311">이렇게 하지 않으면 됩니다 수 tooset hello '-AzureVNetGatewayKey'.</span><span class="sxs-lookup"><span data-stu-id="f4e28-311">Otherwise, you will not be able tooset hello '-AzureVNetGatewayKey'.</span></span>

- <span data-ttu-id="f4e28-312">이 예제에서는 **-VNetName** hello 이름인 hello의 클래식 VNet으로 네트워크 구성 파일에서 발견 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-312">In this example, **-VNetName** is hello name of hello classic VNet as found in your network configuration file.</span></span> 
- <span data-ttu-id="f4e28-313">hello **-LocalNetworkSiteName** 네트워크 구성 파일에서 발견 하 hello 이름으로 hello 로컬 사이트에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-313">hello **-LocalNetworkSiteName** is hello name you specified for hello local site, as found in your network configuration file.</span></span>
- <span data-ttu-id="f4e28-314">hello **-에서 SharedKey** 생성 하 고 지정 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-314">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="f4e28-315">이 예제에서는 *abc123*을 사용했으나 좀 더 복잡한 항목을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-315">For this example, we used *abc123*, but you can generate something more complex.</span></span> <span data-ttu-id="f4e28-316">중요 한 점은 여기에서 지정한 hello 값 hello hello 같은 리소스 관리자 tooclassic 연결을 만들 때 지정한 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-316">hello important thing is that hello value you specify here must be hello same value that you specified when creating your Resource Manager tooclassic connection.</span></span>

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<span data-ttu-id="f4e28-317"><a name="verify"></a>6. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="f4e28-317"><a name="verify"></a>6. Verify your connections</span></span>

<span data-ttu-id="f4e28-318">사용 하 여 연결 hello Azure 포털 또는 PowerShell을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e28-318">You can verify your connections by using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="f4e28-319">을 확인할 때 할 수 있습니다 toowait 2 분 정도로 hello 연결을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="f4e28-319">When verifying, you may need toowait a minute or two as hello connection is being created.</span></span> <span data-ttu-id="f4e28-320">연결이 성공적 '연결' too'Connected에서 hello 연결 상태가 변경 '.</span><span class="sxs-lookup"><span data-stu-id="f4e28-320">When a connection is successful, hello connectivity state changes from 'Connecting' too'Connected'.</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="f4e28-321">프로그램 클래식 VNet tooyour 리소스 관리자 VNet에서에서 tooverify hello 연결</span><span class="sxs-lookup"><span data-stu-id="f4e28-321">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="f4e28-322">리소스 관리자 VNet tooyour에서 tooverify hello 연결 클래식 VNet</span><span class="sxs-lookup"><span data-stu-id="f4e28-322">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="f4e28-323"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="f4e28-323"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
