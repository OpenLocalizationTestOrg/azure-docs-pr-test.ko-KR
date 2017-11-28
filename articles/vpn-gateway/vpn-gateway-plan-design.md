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
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="e54f7-103">VPN Gateway 계획 및 설계</span><span class="sxs-lookup"><span data-stu-id="e54f7-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="e54f7-104">크로스 프레미스 및 VNet-VNet 연결을 계획 및 설계할 경우 네트워킹 요구 사항에 따라 연결이 매우 단순하거나 복잡해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="e54f7-105">이 문서에서는 계획 및 설계 시 기본적으로 고려해야 할 사항을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="e54f7-106"><a name="planning"></a>계획</span><span class="sxs-lookup"><span data-stu-id="e54f7-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="e54f7-107"><a name="compare"></a>프레미스 간 연결 옵션</span><span class="sxs-lookup"><span data-stu-id="e54f7-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="e54f7-108">Tooconnect를 원하는 경우 온-프레미스 사이트 안전 하 게 tooa 가상 네트워크, 세 가지 방법으로 toodo 개일 있으므로: 사이트 간 및 지점-사이트 및 express 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="e54f7-109">사용할 수 있는 hello 다른 크로스-프레미스 연결을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="e54f7-110">hello 옵션 선택와 같은 다양 한 고려 사항에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="e54f7-111">솔루션에 어떤 종류의 처리량이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="e54f7-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="e54f7-112">시겠습니까 toocommunicate hello를 통해 공용 인터넷 또는 개인 연결을 보안 VPN을 통해?</span><span class="sxs-lookup"><span data-stu-id="e54f7-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="e54f7-113">공용 IP 주소 사용 가능한 toouse 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e54f7-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="e54f7-114">VPN 장치 toouse 계획 입니까?</span><span class="sxs-lookup"><span data-stu-id="e54f7-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="e54f7-115">그렇다면 해당 장치가 호환되나요?</span><span class="sxs-lookup"><span data-stu-id="e54f7-115">If so, is it compatible?</span></span>
* <span data-ttu-id="e54f7-116">컴퓨터 몇 대만 연결하시겠어요? 아니면 사이트에 대한 영구 연결을 원하세요?</span><span class="sxs-lookup"><span data-stu-id="e54f7-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="e54f7-117">어떤 유형의 VPN 게이트웨이 필요는 원하는 toocreate hello 솔루션에 대 한?</span><span class="sxs-lookup"><span data-stu-id="e54f7-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="e54f7-118">어떤 게이트웨이 SKU를 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e54f7-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="e54f7-119"><a name="planningtable"></a>계획 표</span><span class="sxs-lookup"><span data-stu-id="e54f7-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="e54f7-120">다음 표는 hello hello 솔루션에 대 한 최상의 연결 옵션을 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="e54f7-121"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="e54f7-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="e54f7-122"><a name="wf"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="e54f7-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="e54f7-123">hello 다음 목록 윤곽선 hello 클라우드 연결에 대 한 일반적인 워크플로:</span><span class="sxs-lookup"><span data-stu-id="e54f7-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="e54f7-124">디자인와 모든 네트워크에 대 한 연결 토폴로지 및 목록 hello 주소 공간 계획 tooconnect 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="e54f7-125">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="e54f7-126">Hello 가상 네트워크용 VPN 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="e54f7-127">만들고 필요에 따라 tooon 온-프레미스 네트워크 연결 또는 다른 가상 네트워크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="e54f7-128">필요에 따라 Azure VPN Gateway에 대한 지점 및 사이트 간 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="e54f7-129"><a name="design"></a>디자인</span><span class="sxs-lookup"><span data-stu-id="e54f7-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="e54f7-130"><a name="topologies"></a>연결 토폴로지</span><span class="sxs-lookup"><span data-stu-id="e54f7-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="e54f7-131">Hello 다이어그램 hello에 확인 하 여 시작 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="e54f7-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="e54f7-132">hello 문서 기본 다이어그램, 각 토폴로지와 hello 사용 가능한 배포 도구 구성 toodeploy를 사용할 수 있습니다에 대 한 hello 배포 모델을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="e54f7-133"><a name="designbasics"></a>디자인 기본 사항</span><span class="sxs-lookup"><span data-stu-id="e54f7-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="e54f7-134">다음 섹션 hello hello VPN 게이트웨이 기본 사항에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="e54f7-135"><a name="servicelimits"></a>네트워킹 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="e54f7-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="e54f7-136">Hello 테이블 tooview 통해 스크롤 [네트워킹 서비스 제한](../azure-subscription-service-limits.md#networking-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="e54f7-137">나열 된 hello 제한 디자인에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="e54f7-138"><a name="subnets"></a>서브넷 정보</span><span class="sxs-lookup"><span data-stu-id="e54f7-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="e54f7-139">연결을 만들 때 서브넷 범위를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="e54f7-140">서브넷 주소 범위가 겹치면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="e54f7-141">다른 위치를 hello 같은 주소 공간을 포함 하는 hello 한 가상 네트워크 또는 온-프레미스 위치가 포함 되어 있으면에 겹치는 서브넷.</span><span class="sxs-lookup"><span data-stu-id="e54f7-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="e54f7-142">즉, Azure IP에 대 한 사용자 로컬 온-프레미스 네트워크 toocarve toouse 있습니다에 대 한 기간에 네트워크 엔지니어를 필요한 공간/서브넷 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="e54f7-143">Hello 로컬 온-프레미스 네트워크에서 사용 되지 않는 주소 공간이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="e54f7-144">또한 VNet 간 연결을 사용할 때는 서브넷이 중복되지 않도록 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="e54f7-145">서브넷 겹치는 IP 주소에 있는 경우 hello 보내기 및 대상 Vnet VNet 대 VNet 연결 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="e54f7-146">Azure는 hello 대상 주소 hello VNet 전송의 일부 이므로 hello 데이터 toohello 다른 VNet 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="e54f7-147">VPN Gateway에는 게이트웨이 서브넷이라는 특정 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="e54f7-148">모든 게이트웨이 서브넷 이름을 지정 해야 GatewaySubnet toowork 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="e54f7-149">확인 되지 tooname 다른 게이트웨이 서브넷 이름을 지정 하 고 Vm 또는 다른 무엇 toohello 게이트웨이 서브넷에 배포 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="e54f7-150">[게이트웨이 서브넷](vpn-gateway-about-vpn-gateway-settings.md#gwsub)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54f7-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="e54f7-151"><a name="local"></a>로컬 네트워크 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="e54f7-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="e54f7-152">일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="e54f7-153">Hello 클래식 배포 모델 hello 로컬 네트워크 게이트웨이 로컬 네트워크 사이트 참조 tooas 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="e54f7-154">로컬 네트워크 게이트웨이 구성할 때 이름을 지정, hello hello 온-프레미스 VPN 장치의 공용 IP 주소를 지정 했으며 hello 온-프레미스 위치에 있는 hello 주소 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="e54f7-155">Azure는 네트워크 트래픽에 대 한 hello 대상 주소 접두사에 조회 하 고, 사용자가 지정한 hello 구성 hello 로컬 네트워크 게이트웨이에 대 한 참조, 그에 따라 패킷을 라우팅할 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="e54f7-156">필요에 따라 hello 주소 접두사를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="e54f7-157">자세한 내용은 [로컬 네트워크 게이트웨이](vpn-gateway-about-vpn-gateway-settings.md#lng)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54f7-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="e54f7-158"><a name="gwtype"></a>게이트웨이 형식 정보</span><span class="sxs-lookup"><span data-stu-id="e54f7-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="e54f7-159">토폴로지에 대 한 hello 올바른 게이트웨이 유형을 선택 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="e54f7-160">Hello 잘못 된 유형을 선택 하면 게이트웨이가 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="e54f7-161">hello 게이트웨이 유형을 hello 게이트웨이 자체 연결 하 고 hello 리소스 관리자 배포 모델에 대 한 필수 구성 설정 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="e54f7-162">hello 게이트웨이 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-162">hello gateway types are:</span></span>

* <span data-ttu-id="e54f7-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="e54f7-163">Vpn</span></span>
* <span data-ttu-id="e54f7-164">Express 경로</span><span class="sxs-lookup"><span data-stu-id="e54f7-164">ExpressRoute</span></span>

#### <span data-ttu-id="e54f7-165"><a name="connectiontype"></a>연결 형식 정보</span><span class="sxs-lookup"><span data-stu-id="e54f7-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="e54f7-166">각 구성이 작동하려면 특정 연결 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="e54f7-167">hello 연결 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-167">hello connection types are:</span></span>

* <span data-ttu-id="e54f7-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="e54f7-168">IPsec</span></span>
* <span data-ttu-id="e54f7-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="e54f7-169">Vnet2Vnet</span></span>
* <span data-ttu-id="e54f7-170">Express 경로</span><span class="sxs-lookup"><span data-stu-id="e54f7-170">ExpressRoute</span></span>
* <span data-ttu-id="e54f7-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="e54f7-171">VPNClient</span></span>

#### <span data-ttu-id="e54f7-172"><a name="vpntype"></a>VPN 형식 정보</span><span class="sxs-lookup"><span data-stu-id="e54f7-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="e54f7-173">각 구성에는 특정 VPN 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="e54f7-174">사이트 간 연결과 지점 및 사이트 연결 toohello 만들기와 같은 두 가지 구성을 결합 하는 경우 동일한 VNet 연결 요구 사항을 모두 충족 하는 VPN 형식을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="e54f7-175">hello 다음 표에서 보여 hello VPN 유형을 대로 tooeach 연결 구성에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="e54f7-176">있는지 hello toocreate 원하는 게이트웨이 일치 hello 구성에 대 한 VPN 유형을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e54f7-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="e54f7-177"><a name="devices"></a>사이트 간 연결에 대한 VPN 장치</span><span class="sxs-lookup"><span data-stu-id="e54f7-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="e54f7-178">사이트-사이트 tooconfigure 연결 배포 모델에 관계 없이 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="e54f7-179">Azure VPN Gateway와 호환되는 VPN 장치</span><span class="sxs-lookup"><span data-stu-id="e54f7-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="e54f7-180">NAT 뒤에 있지 않은 공용 IPv4 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e54f7-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="e54f7-181">VPN 장치를 구성 하는 toohave 경험 필요 또는 누군가가 수 있는 hello 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="e54f7-182"><a name="forcedtunnel"></a>강제 터널 라우팅 고려</span><span class="sxs-lookup"><span data-stu-id="e54f7-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="e54f7-183">대부분의 구성에서 강제 터널링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="e54f7-184">강제 터널링 리디렉션 또는 "강제" 검사 및 감사용 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치로 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="e54f7-185">대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="e54f7-186">강제 터널링 기능이 없으면 Azure 내 Vm의에서 인터넷 바인딩된 트래픽이 항상 트래버스할 hello 옵션 tooallow 없이 toohello 인터넷 아웃 직접 Azure 네트워크 인프라에서 있습니다 tooinspect 또는 감사 hello 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="e54f7-187">인터넷에 대 한 무단된 액세스 tooinformation 노출 또는 기타 유형의 보안 위반을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="e54f7-188">두 배포 모델에서 다양한 도구를 사용하여 강제 터널링 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="e54f7-189">자세한 내용은 [강제 터널링 구성](vpn-gateway-forced-tunneling-rm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54f7-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="e54f7-190">**강제 터널링 다이어그램**</span><span class="sxs-lookup"><span data-stu-id="e54f7-190">**Forced tunneling diagram**</span></span>

![Azure VPN Gateway 강제 터널링 다이어그램](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="e54f7-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e54f7-192">Next steps</span></span>

<span data-ttu-id="e54f7-193">Hello 참조 [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md) 및 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 에 대 한 자세한 내용은 toohelp 있습니다으로 설정 된 아티클에 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54f7-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="e54f7-194">특정 게이트웨이 설정에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54f7-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>