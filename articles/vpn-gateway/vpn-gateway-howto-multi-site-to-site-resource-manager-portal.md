---
title: "VNet에 여러 VPN Gateway 사이트 간 연결 추가: Azure Portal: Resource Manager| Microsoft Docs"
description: "기존 연결이 있는 VPN Gateway에 다중 사이트 S2S 연결 추가"
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
ms.openlocfilehash: 7ec57789ee76f4ec54e4f7b68ea75c19522f3d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="cecef-103">기존 VPN 게이트웨이 연결이 있는 VNet에 사이트 간 연결 추가</span><span class="sxs-lookup"><span data-stu-id="cecef-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cecef-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="cecef-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="cecef-105">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="cecef-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="cecef-106">이 문서에서는 Azure Portal을 사용하여 기존 연결이 있는 VPN 게이트웨이에 S2S(사이트 간) 연결을 추가하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="cecef-107">이러한 유형의 연결을 "다중 사이트" 구성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="cecef-108">S2S 연결, 사이트 간 연결 또는 VNet 간 연결이 이미 있는 VNet에 S2S 연결을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="cecef-109">연결을 추가하는 데 몇 가지 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="cecef-110">구성을 시작하기 전에 확인하려면 이 문서의 [시작 하기 전에](#before) 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="cecef-111">이 문서는 RouteBased VPN 게이트웨이가 있는 Resource Manager 배포 모델을 사용하여 만든 VNet에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="cecef-112">이러한 단계가 Express 경로/사이트 간 공존 연결 구성에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="cecef-113">공존 연결에 대한 자세한 내용은 [xpress 경로/S2S 공존 연결](../expressroute/expressroute-howto-coexist-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cecef-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="cecef-114">배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="cecef-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="cecef-115">새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="cecef-116">문서를 사용할 수 있는 경우 표에서 직접 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="cecef-117"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cecef-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="cecef-118">다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-118">Verify the following items:</span></span>

* <span data-ttu-id="cecef-119">ExpressRoute/S2S 공존 연결을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="cecef-120">기존 연결로 Resource Manager 배포 모델을 사용하여 만든 가상 네트워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="cecef-121">VNet용 가상 네트워크 게이트웨이는 RouteBased입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="cecef-122">PolicyBased VPN 게이트웨이가 있다면 가상 네트워크 게이트웨이를 삭제하고 새 VPN 게이트웨이를 RouteBased로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="cecef-123">어떠한 주소 범위도 이 Vnet이 연결하고 있는 Vnet에 대해 겹치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="cecef-124">호환되는 VPN 장치 및 그것을 구성할 수 있는 사람이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="cecef-125">[VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cecef-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="cecef-126">VPN 장치를 구성하는 방법과 온-프레미스 네트워크 구성에 있는 IP 주소 범위에 익숙하지 않은 경우 세부 정보를 제공할 수 있는 다른 사람의 도움을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="cecef-127">VPN 장치에 대한 외부 연결 공용 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="cecef-128">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="cecef-129"><a name="part1"></a>1부 - 연결 구성</span><span class="sxs-lookup"><span data-stu-id="cecef-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="cecef-130">브라우저에서 [Azure Portal](http://portal.azure.com) 로 이동하고 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="cecef-131">**모든 리소스**를 클릭하고 리소스 목록에서 **가상 네트워크 게이트웨이**를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="cecef-132">**가상 네트워크 게이트웨이** 블레이드에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-132">On the **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="cecef-133">![연결 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="cecef-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="cecef-134">**연결** 블레이드에서 **+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-134">On the **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="cecef-135">![연결 추가 단추](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="cecef-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="cecef-136">**연결 추가** 블레이드에서 다음 필드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-136">On the **Add connection** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="cecef-137">**이름:** 연결을 만들고자 하는 사이트에 부여하고자 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="cecef-138">**연결 형식:** **사이트 간(IPSec)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="cecef-139">![연결 추가 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span><span class="sxs-lookup"><span data-stu-id="cecef-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="cecef-140"><a name="part2"></a>2부 - 로컬 네트워크 게이트웨이 추가</span><span class="sxs-lookup"><span data-stu-id="cecef-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="cecef-141">**로컬 네트워크 게이트웨이**를 클릭하고 ***로컬 네트워크 게이트웨이를 선택 합니다***.</span><span class="sxs-lookup"><span data-stu-id="cecef-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="cecef-142">그러면 **로컬 네트워크 게이트웨이 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-142">This will open the **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="cecef-143">![로컬 네트워크 게이트웨이 선택](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="cecef-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="cecef-144">**로컬 네트워크 게이트웨이 만들기** 블레이드를 열려면 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-144">Click **Create new** to open the **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="cecef-145">![로컬 네트워크 게이트웨이 만들기 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="cecef-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="cecef-146">**로컬 네트워크 게이트웨이 만들기** 블레이드에서 다음 필드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-146">On the **Create local network gateway** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="cecef-147">**이름:** 로컬 네트워크 게이트웨이 리소스에 부여하고자 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="cecef-148">**IP 주소:** 연결하려는 사이트에 있는 VPN 장치의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="cecef-149">**주소 공간:** 새 로컬 네트워크 사이트로 라우팅하려는 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="cecef-150">변경 내용을 저장하려면 **로컬 네트워크 게이트웨이 만들기** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span></span>

## <span data-ttu-id="cecef-151"><a name="part3"></a>3부 - 공유 키 추가 및 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="cecef-151"><a name="part3"></a>Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="cecef-152">**연결 추가** 블레이드에서 연결을 만드는 데 사용하려는 공유 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="cecef-153">사용자가 VPN 장치에서 공유 키를 가져오거나, 여기서 공유 키를 만든 후 VPN 장치에서 동일한 공유 키를 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="cecef-154">중요한 것은 키가 정확히 동일하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="cecef-155">![공유 키](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="cecef-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="cecef-156">블레이드의 맨 아래에서 **확인**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-156">At the bottom of the blade, click **OK** to create the connection.</span></span>

## <span data-ttu-id="cecef-157"><a name="part4"></a>4부 - VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="cecef-157"><a name="part4"></a>Part 4 - Verify the VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cecef-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cecef-158">Next steps</span></span>

<span data-ttu-id="cecef-159">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cecef-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="cecef-160">자세한 내용은 가상 컴퓨터 [학습 경로](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cecef-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
