---
title: "여러 VPN 사이트 간 게이트웨이 연결 tooa VNet 추가: Azure 포털: 리소스 관리자 | Microsoft Docs"
description: "다중 사이트 S2S 연결 tooa VPN 게이트웨이 추가 하는 기존 연결"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="c071d-103">기존 VPN 게이트웨이 연결에는 사이트 간 연결 tooa VNet 추가</span><span class="sxs-lookup"><span data-stu-id="c071d-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c071d-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c071d-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c071d-105">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="c071d-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="c071d-106">이 문서 hello Azure 포털 tooadd 사이트 및 사이트 간 (S2S) 연결 tooa VPN 게이트웨이 기존 연결이 있는 사용 하 여 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="c071d-107">이 연결의 형식은 종종 참조 tooas "멀티 사이트" 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="c071d-108">S2S 연결 tooa S2S 연결, 지점 및 사이트 연결 또는 VNet 대 VNet 연결을 이미 있는 VNet을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="c071d-109">연결을 추가하는 데 몇 가지 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="c071d-110">Hello 확인 [시작 하기 전에](#before) 섹션에서 구성을 시작 하기 전에이 문서 tooverify 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="c071d-111">이 문서 RouteBased VPN 게이트웨이가 있는 hello 리소스 관리자 배포 모델을 사용 하 여 만든 tooVNets 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="c071d-112">이러한 단계는 tooExpressRoute /-사이트 공존할 연결 구성 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="c071d-113">공존 연결에 대한 자세한 내용은 [xpress 경로/S2S 공존 연결](../expressroute/expressroute-howto-coexist-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c071d-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="c071d-114">배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="c071d-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="c071d-115">새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="c071d-116">문서를 사용할 수 있는이 테이블에서 tooit을 연결 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="c071d-117"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c071d-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="c071d-118">Hello 다음 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-118">Verify hello following items:</span></span>

* <span data-ttu-id="c071d-119">ExpressRoute/S2S 공존 연결을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="c071d-120">기존에 연결 되어 있는 hello 리소스 관리자 배포 모델을 사용 하 여 만든 가상 네트워크를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="c071d-121">VNet에 대 한 가상 네트워크 게이트웨이 hello RouteBased입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="c071d-122">PolicyBased VPN 게이트웨이 사용 하도록 설정한 경우에 hello 가상 네트워크 게이트웨이 삭제 하 고 RouteBased로 새 VPN 게이트웨이 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="c071d-123">Hello 주소 범위가 겹치지 Vnet이이 VNet에 연결 하는 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="c071d-124">호환 VPN 장치 및 사용자 수 tooconfigure가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c071d-125">[VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c071d-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="c071d-126">VPN 장치 구성에 익숙하지 않은 익숙하지 않은 hello IP 주소 범위를 온-프레미스 네트워크 구성에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="c071d-127">VPN 장치에 대한 외부 연결 공용 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="c071d-128">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="c071d-129"><a name="part1"></a>1부 - 연결 구성</span><span class="sxs-lookup"><span data-stu-id="c071d-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="c071d-130">브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c071d-131">클릭 **모든 리소스** 찾습니다 프로그램 **가상 네트워크 게이트웨이** hello 리소스 목록에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="c071d-132">Hello에 **가상 네트워크 게이트웨이** 블레이드에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="c071d-133">![연결 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="c071d-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="c071d-134">Hello에 **연결** 블레이드에서 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="c071d-135">![추가 연결 단추](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "추가 연결 단추")</span><span class="sxs-lookup"><span data-stu-id="c071d-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="c071d-136">Hello에 **연결 추가** 블레이드에서 hello 필드에 다음 내용을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="c071d-137">**이름:** toogive toohello 사이트 hello 연결을 만들면 원하는 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="c071d-138">**연결 형식:** **사이트 간(IPSec)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="c071d-139">![추가 연결 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "추가 연결 블레이드")</span><span class="sxs-lookup"><span data-stu-id="c071d-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="c071d-140"><a name="part2"></a>2부 - 로컬 네트워크 게이트웨이 추가</span><span class="sxs-lookup"><span data-stu-id="c071d-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="c071d-141">**로컬 네트워크 게이트웨이**를 클릭하고 ***로컬 네트워크 게이트웨이를 선택 합니다***.</span><span class="sxs-lookup"><span data-stu-id="c071d-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="c071d-142">Hello 열립니다 **로컬 네트워크 게이트웨이 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="c071d-143">![로컬 네트워크 게이트웨이 선택](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "로컬 네트워크 게이트웨이 선택")</span><span class="sxs-lookup"><span data-stu-id="c071d-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="c071d-144">클릭 **새로 만들기** tooopen hello **로컬 네트워크 게이트웨이 만들기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="c071d-145">![로컬 네트워크 게이트웨이 블레이드 만들기](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "로컬 네트워크 게이트웨이 만들기")</span><span class="sxs-lookup"><span data-stu-id="c071d-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="c071d-146">Hello에 **로컬 네트워크 게이트웨이 만들기** 블레이드에서 hello 필드에 다음 내용을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="c071d-147">**이름:** toogive toohello 로컬 네트워크 게이트웨이 리소스 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="c071d-148">**IP 주소:** hello tooconnect를 원하는 hello 사이트에 대 한 hello VPN 장치의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="c071d-149">**주소 공간:** toobe 원하는 hello 주소 공간 toohello 새 로컬 네트워크 사이트를 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="c071d-150">클릭 **확인** hello에 **로컬 네트워크 게이트웨이 만들기** 블레이드 toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="c071d-151"><a name="part3"></a>3 부-hello 공유 키를 추가 하 고 hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c071d-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="c071d-152">Hello에 **연결 추가** 블레이드에서 원하는 toouse toocreate 연결 hello 공유 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="c071d-153">중 하나 가져와서 hello 공유 키 VPN 장치에서 또는 여기 하나를 수행 하 여 VPN 장치 toouse hello를 구성 합니다 동일한 키를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="c071d-154">hello hello 키 정확 하 게 되는 중요 한 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="c071d-155">![공유 키](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="c071d-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="c071d-156">Hello 블레이드의 hello 아래쪽 클릭 **확인** toocreate hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="c071d-157"><a name="part4"></a>4 부-hello VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="c071d-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c071d-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c071d-158">Next steps</span></span>

<span data-ttu-id="c071d-159">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c071d-160">Hello 가상 컴퓨터를 참조 하십시오. [학습 경로](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c071d-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
