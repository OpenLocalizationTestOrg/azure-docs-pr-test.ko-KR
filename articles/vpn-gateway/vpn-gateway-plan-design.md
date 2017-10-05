---
title: "프레미스 간 연결을 위한 계획 및 설계: Azure VPN Gateway | Microsoft Docs"
description: "크로스-프레미스, 하이브리드, VNet 간 연결에 대한 VPN Gateway 계획 및 설계에 대해 알아보세요."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="4fa30-103">VPN Gateway 계획 및 설계</span><span class="sxs-lookup"><span data-stu-id="4fa30-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="4fa30-104">크로스 프레미스 및 VNet-VNet 연결을 계획 및 설계할 경우 네트워킹 요구 사항에 따라 연결이 매우 단순하거나 복잡해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="4fa30-105">이 문서에서는 계획 및 설계 시 기본적으로 고려해야 할 사항을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="4fa30-106"><a name="planning"></a>계획</span><span class="sxs-lookup"><span data-stu-id="4fa30-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="4fa30-107"><a name="compare"></a>프레미스 간 연결 옵션</span><span class="sxs-lookup"><span data-stu-id="4fa30-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="4fa30-108">온-프레미스 사이트를 가상 네트워크에 안전하게 연결하려면 사이트 간, 지점 및 사이트 간, Express 경로의 세 가지 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="4fa30-109">사용 가능한 여러 크로스-프레미스 연결을 비교하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fa30-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="4fa30-110">선택하는 옵션은 다음과 같은 다양한 고려 사항에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="4fa30-111">솔루션에 어떤 종류의 처리량이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="4fa30-112">보안 VPN을 통한 공용 인터넷을 통해 통신하시겠어요? 아니면 개인 연결을 통해 통신하시겠어요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="4fa30-113">사용할 수 있는 공용 IP 주소가 있나요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="4fa30-114">VPN 장치를 사용할 계획인가요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="4fa30-115">그렇다면 해당 장치가 호환되나요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-115">If so, is it compatible?</span></span>
* <span data-ttu-id="4fa30-116">컴퓨터 몇 대만 연결하시겠어요? 아니면 사이트에 대한 영구 연결을 원하세요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="4fa30-117">만들려는 솔루션에 어떤 형식의 VPN Gateway가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="4fa30-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="4fa30-118">어떤 게이트웨이 SKU를 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4fa30-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="4fa30-119"><a name="planningtable"></a>계획 표</span><span class="sxs-lookup"><span data-stu-id="4fa30-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="4fa30-120">다음 테이블은 솔루션에 대한 최상의 연결 옵션을 결정하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="4fa30-121"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="4fa30-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="4fa30-122"><a name="wf"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="4fa30-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="4fa30-123">다음은 클라우드 연결의 공통 워크플로를 요약한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="4fa30-124">연결 토폴로지를 설계 및 계획하고 연결하려는 모든 네트워크의 주소 공간을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="4fa30-125">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="4fa30-126">가상 네트워크의 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="4fa30-127">필요에 따라 온-프레미스 네트워크 또는 기타 가상 네트워크에 대한 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="4fa30-128">필요에 따라 Azure VPN Gateway에 대한 지점 및 사이트 간 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="4fa30-129"><a name="design"></a>디자인</span><span class="sxs-lookup"><span data-stu-id="4fa30-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="4fa30-130"><a name="topologies"></a>연결 토폴로지</span><span class="sxs-lookup"><span data-stu-id="4fa30-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="4fa30-131">먼저 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 문서의 다이어그램을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="4fa30-132">이 문서는 기본 다이어그램, 각 토폴로지의 배포 모델, 구성을 배포하는 데 사용할 수 있는 배포 도구에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="4fa30-133"><a name="designbasics"></a>디자인 기본 사항</span><span class="sxs-lookup"><span data-stu-id="4fa30-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="4fa30-134">다음 섹션은 VPN Gateway 기본 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="4fa30-135"><a name="servicelimits"></a>네트워킹 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="4fa30-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="4fa30-136">표를 스크롤하여 [네트워킹 서비스 제한](../azure-subscription-service-limits.md#networking-limits)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="4fa30-137">목록의 제한은 디자인에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="4fa30-138"><a name="subnets"></a>서브넷 정보</span><span class="sxs-lookup"><span data-stu-id="4fa30-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="4fa30-139">연결을 만들 때 서브넷 범위를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="4fa30-140">서브넷 주소 범위가 겹치면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="4fa30-141">서브넷 중복이란 하나의 가상 네트워크 또는 온-프레미스 위치에 다른 위치에 포함된 것과 동일한 주소 공간이 포함된 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="4fa30-142">이 경우 로컬 온-프레미스 네트워크의 네트워크 엔지니어가 Azure IP 주소 지정 공간/서브넷에 사용할 범위를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="4fa30-143">로컬 온-프레미스 네트워크에서 사용되고 있지 않은 주소 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="4fa30-144">또한 VNet 간 연결을 사용할 때는 서브넷이 중복되지 않도록 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="4fa30-145">서브넷이 중복되고 보내는 VNet과 대상 VNet에 같은 IP 주소가 있을 경우 VNet 간 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="4fa30-146">대상 주소가 보내는 VNet의 일부이므로 Azure에서 다른 VNet으로 데이터를 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="4fa30-147">VPN Gateway에는 게이트웨이 서브넷이라는 특정 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="4fa30-148">모든 게이트웨이 서브넷이 제대로 작동하려면 이름을 GatewaySubnet으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="4fa30-149">게이트웨이 서브넷에 다른 이름을 지정하지 않도록 해야 하며 VM 등을 게이트웨이 서브넷에 배포하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="4fa30-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="4fa30-150">[게이트웨이 서브넷](vpn-gateway-about-vpn-gateway-settings.md#gwsub)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="4fa30-151"><a name="local"></a>로컬 네트워크 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="4fa30-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="4fa30-152">로컬 네트워크 게이트웨이는 일반적으로 온-프레미스 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="4fa30-153">클래식 배포 모델에서 로컬 네트워크 게이트웨이는 로컬 네트워크 사이트라고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="4fa30-154">로컬 네트워크 게이트웨이를 구성할 때 이름을 지정하고, 온-프레미스 VPN 장치의 공용 IP 주소를 지정하고, 온-프레미스 위치에 있는 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="4fa30-155">Azure는 네트워크 트래픽에 대상 주소 접두사를 보고 로컬 네트워크 게이트웨이에 대해 지정한 구성을 참조하며 그에 따라 패킷을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="4fa30-156">필요에 따라 주소 접두사를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="4fa30-157">자세한 내용은 [로컬 네트워크 게이트웨이](vpn-gateway-about-vpn-gateway-settings.md#lng)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="4fa30-158"><a name="gwtype"></a>게이트웨이 형식 정보</span><span class="sxs-lookup"><span data-stu-id="4fa30-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="4fa30-159">토폴로지에 정확한 게이트웨이 유형을 선택하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="4fa30-160">잘못된 형식을 선택할 경우 게이트웨이가 정상적으로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="4fa30-161">게이트웨이 유형은 게이트웨이 자체를 연결하는 방법을 지정하며 리소스 관리자 배포 모델에 대한 필수 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="4fa30-162">게이트웨이 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-162">The gateway types are:</span></span>

* <span data-ttu-id="4fa30-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="4fa30-163">Vpn</span></span>
* <span data-ttu-id="4fa30-164">Express 경로</span><span class="sxs-lookup"><span data-stu-id="4fa30-164">ExpressRoute</span></span>

#### <span data-ttu-id="4fa30-165"><a name="connectiontype"></a>연결 형식 정보</span><span class="sxs-lookup"><span data-stu-id="4fa30-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="4fa30-166">각 구성이 작동하려면 특정 연결 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="4fa30-167">연결 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-167">The connection types are:</span></span>

* <span data-ttu-id="4fa30-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="4fa30-168">IPsec</span></span>
* <span data-ttu-id="4fa30-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="4fa30-169">Vnet2Vnet</span></span>
* <span data-ttu-id="4fa30-170">Express 경로</span><span class="sxs-lookup"><span data-stu-id="4fa30-170">ExpressRoute</span></span>
* <span data-ttu-id="4fa30-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="4fa30-171">VPNClient</span></span>

#### <span data-ttu-id="4fa30-172"><a name="vpntype"></a>VPN 형식 정보</span><span class="sxs-lookup"><span data-stu-id="4fa30-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="4fa30-173">각 구성에는 특정 VPN 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="4fa30-174">동일한 VNet에 사이트 간 연결 및 지점 및 사이트 간 연결을 만드는 것과 같은 두 가지 구성을 결합하는 경우 두 연결 요구 사항을 충족하는 VPN 유형을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="4fa30-175">다음 테이블에는 각 연결 구성에 해당하는 VPN 형식이 정리되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="4fa30-176">게이트웨이의 VPN 유형이 만들려는 구성과 일치하는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fa30-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="4fa30-177"><a name="devices"></a>사이트 간 연결에 대한 VPN 장치</span><span class="sxs-lookup"><span data-stu-id="4fa30-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="4fa30-178">사이트 간 연결을 구성하려면 배포 모델과 상관없이 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="4fa30-179">Azure VPN Gateway와 호환되는 VPN 장치</span><span class="sxs-lookup"><span data-stu-id="4fa30-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="4fa30-180">NAT 뒤에 있지 않은 공용 IPv4 IP 주소</span><span class="sxs-lookup"><span data-stu-id="4fa30-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="4fa30-181">VPN 장치를 구성해본 경험이 필요하거나 누군가가 장치를 대신 구성해줄 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="4fa30-182"><a name="forcedtunnel"></a>강제 터널 라우팅 고려</span><span class="sxs-lookup"><span data-stu-id="4fa30-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="4fa30-183">대부분의 구성에서 강제 터널링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="4fa30-184">강제 터널링을 사용하면 검사 및 감사에 대한 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽을 온-프레미스 위치에 다시 리디렉션하거나 "force"할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="4fa30-185">대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="4fa30-186">강제 터널링 없이 Azure의 VM에서 인터넷 바인딩된 트래픽은 항상 트래픽을 검사 또는 감사하도록 허용하는 옵션 없이 Azure 네트워크 인프라에서 직접 인터넷으로 트래버스합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="4fa30-187">인증되지 않은 인터넷 액세스는 잠재적으로 정보 공개 또는 다른 유형의 보안 위반을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="4fa30-188">두 배포 모델에서 다양한 도구를 사용하여 강제 터널링 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa30-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="4fa30-189">자세한 내용은 [강제 터널링 구성](vpn-gateway-forced-tunneling-rm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="4fa30-190">**강제 터널링 다이어그램**</span><span class="sxs-lookup"><span data-stu-id="4fa30-190">**Forced tunneling diagram**</span></span>

![Azure VPN Gateway 강제 터널링 다이어그램](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="4fa30-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fa30-192">Next steps</span></span>

<span data-ttu-id="4fa30-193">설계에 도움이 되는 정보를 보려면 [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) 및 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="4fa30-194">특정 게이트웨이 설정에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fa30-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>