---
title: "Azure Resource Manager VNet에 클래식 가상 네트워크를 연결하는 방법: 포털 | Microsoft Docs"
description: "VPN 게이트웨이 및 포털을 사용하여 클래식 VNet 및 Resource Manager VNet 간에 VPN 연결을 만드는 방법을 알아봅니다"
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
ms.openlocfilehash: 1b7b67ec28986b7c20b3e990e3565265f74c28e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-the-portal"></a><span data-ttu-id="1d6c5-103">포털을 사용하여 다양한 배포 모델에서 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="1d6c5-103">Connect virtual networks from different deployment models using the portal</span></span>

<span data-ttu-id="1d6c5-104">이 문서에서는 Resource Manager VNet에 클래식 VNet을 연결하여 별도의 배포 모델에 있는 리소스가 서로 통신하도록 허용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="1d6c5-105">이 문서의 단계는 주로 Azure Portal을 사용하지만 이 목록에서 문서를 선택하여 PowerShell을 통해 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-105">The steps in this article primarily use the Azure portal, but you can also create this configuration using the PowerShell by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d6c5-106">포털</span><span class="sxs-lookup"><span data-stu-id="1d6c5-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="1d6c5-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6c5-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="1d6c5-108">클래식 VNet을 Resource Manager VNet에 연결하는 것은 VNet을 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="1d6c5-109">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="1d6c5-110">다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="1d6c5-111">또한 함께 구성된 게이트웨이가 동적이거나 경로 기반이면 온-프레미스 네트워크에 이미 연결된 VNet을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="1d6c5-112">VNet 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [VNet 간 FAQ](#faq) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="1d6c5-113">VNet이 동일한 지역에 있는 경우 VNet 피어링을 사용하여 연결하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="1d6c5-114">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="1d6c5-115">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="1d6c5-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1d6c5-116">Prerequisites</span></span>

* <span data-ttu-id="1d6c5-117">이 단계에서는 두 VNet이 이미 만들어졌다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-117">These steps assume that both VNets have already been created.</span></span> <span data-ttu-id="1d6c5-118">이 문서를 사용하여 연습을 하는 경우 VNet이 없으면 단계 내에 VNet 만들기를 도와주는 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-118">If you are using this article as an exercise and don't have VNets, there are links in the steps to help you create them.</span></span>
* <span data-ttu-id="1d6c5-119">VNet에 대한 주소 범위가 서로 겹치거나 게이트웨이가 연결되어 있는 다른 연결의 범위와 겹치지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-119">Verify that the address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="1d6c5-120">Resource Manager와 Service Management(클래식)에 대해 최신 PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-120">Install the latest PowerShell cmdlets for both Resource Manager and Service Management (classic).</span></span> <span data-ttu-id="1d6c5-121">이 문서에서는 Azure Portal 및 PowerShell을 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-121">In this article, we use both the Azure portal and PowerShell.</span></span> <span data-ttu-id="1d6c5-122">PowerShell은 클래식 VNet에서 Resource Manager VNet에 연결을 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-122">PowerShell is required to create the connection from the classic VNet to the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-123">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-123">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <span data-ttu-id="1d6c5-124"><a name="values"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="1d6c5-124"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="1d6c5-125">이러한 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 더 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-125">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="1d6c5-126">**클래식 VNet**</span><span class="sxs-lookup"><span data-stu-id="1d6c5-126">**Classic VNet**</span></span>

<span data-ttu-id="1d6c5-127">VNet 이름 = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-127">VNet name = ClassicVNet</span></span> <br>
<span data-ttu-id="1d6c5-128">Address space = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="1d6c5-128">Address space = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="1d6c5-129">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="1d6c5-129">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="1d6c5-130">Resource Group = ClassicRG</span><span class="sxs-lookup"><span data-stu-id="1d6c5-130">Resource Group = ClassicRG</span></span> <br>
<span data-ttu-id="1d6c5-131">Location = West US</span><span class="sxs-lookup"><span data-stu-id="1d6c5-131">Location = West US</span></span> <br>
<span data-ttu-id="1d6c5-132">GatewaySubnet = 10.0.0.32/28</span><span class="sxs-lookup"><span data-stu-id="1d6c5-132">GatewaySubnet = 10.0.0.32/28</span></span> <br>
<span data-ttu-id="1d6c5-133">Local site = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="1d6c5-133">Local site = RMVNetLocal</span></span> <br>

<span data-ttu-id="1d6c5-134">**Resource Manager VNet**</span><span class="sxs-lookup"><span data-stu-id="1d6c5-134">**Resource Manager VNet**</span></span>

<span data-ttu-id="1d6c5-135">VNet 이름 = RMVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-135">VNet name = RMVNet</span></span> <br>
<span data-ttu-id="1d6c5-136">Address space = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1d6c5-136">Address space = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="1d6c5-137">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="1d6c5-137">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="1d6c5-138">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="1d6c5-138">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="1d6c5-139">Resource Group = RG1</span><span class="sxs-lookup"><span data-stu-id="1d6c5-139">Resource Group = RG1</span></span> <br>
<span data-ttu-id="1d6c5-140">Location = East US</span><span class="sxs-lookup"><span data-stu-id="1d6c5-140">Location = East US</span></span> <br>
<span data-ttu-id="1d6c5-141">Virtual network gateway name = RMGateway</span><span class="sxs-lookup"><span data-stu-id="1d6c5-141">Virtual network gateway name = RMGateway</span></span> <br>
<span data-ttu-id="1d6c5-142">Gateway type = VPN</span><span class="sxs-lookup"><span data-stu-id="1d6c5-142">Gateway type = VPN</span></span> <br>
<span data-ttu-id="1d6c5-143">VPN type = Route-based</span><span class="sxs-lookup"><span data-stu-id="1d6c5-143">VPN type = Route-based</span></span> <br>
<span data-ttu-id="1d6c5-144">게이트웨이 공용 IP 주소 이름 = rmgwpip</span><span class="sxs-lookup"><span data-stu-id="1d6c5-144">Gateway Public IP address name = rmgwpip</span></span> <br>
<span data-ttu-id="1d6c5-145">Local network gateway = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="1d6c5-145">Local network gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="1d6c5-146">연결 이름 = RMtoClassic</span><span class="sxs-lookup"><span data-stu-id="1d6c5-146">Connection name = RMtoClassic</span></span>

### <a name="connection-overview"></a><span data-ttu-id="1d6c5-147">연결 개요</span><span class="sxs-lookup"><span data-stu-id="1d6c5-147">Connection overview</span></span>

<span data-ttu-id="1d6c5-148">이 구성에 대해 가상 네트워크 사이에 IPsec/IKE VPN 터널을 통해 VPN 게이트웨이 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-148">For this configuration, you create a VPN gateway connection over an IPsec/IKE VPN tunnel between the virtual networks.</span></span> <span data-ttu-id="1d6c5-149">VNet 범위가 서로 간에 또는 연결된 로컬 네트워크와 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-149">Make sure that none of your VNet ranges overlap with each other, or with any of the local networks that they connect to.</span></span>

<span data-ttu-id="1d6c5-150">다음 테이블은 예제 VNet 및 로컬 사이트가 어떻게 정의되는지 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-150">The following table shows an example of how the example VNets and local sites are defined:</span></span>

| <span data-ttu-id="1d6c5-151">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1d6c5-151">Virtual Network</span></span> | <span data-ttu-id="1d6c5-152">주소 공간</span><span class="sxs-lookup"><span data-stu-id="1d6c5-152">Address Space</span></span> | <span data-ttu-id="1d6c5-153">지역</span><span class="sxs-lookup"><span data-stu-id="1d6c5-153">Region</span></span> | <span data-ttu-id="1d6c5-154">로컬 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="1d6c5-154">Connects to local network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1d6c5-155">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-155">ClassicVNet</span></span> |<span data-ttu-id="1d6c5-156">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-156">(10.0.0.0/24)</span></span> |<span data-ttu-id="1d6c5-157">미국 서부</span><span class="sxs-lookup"><span data-stu-id="1d6c5-157">West US</span></span> | <span data-ttu-id="1d6c5-158">RMVNetLocal(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-158">RMVNetLocal (192.168.0.0/16)</span></span> |
| <span data-ttu-id="1d6c5-159">RMVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-159">RMVNet</span></span> | <span data-ttu-id="1d6c5-160">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-160">(192.168.0.0/16)</span></span> |<span data-ttu-id="1d6c5-161">미국 동부</span><span class="sxs-lookup"><span data-stu-id="1d6c5-161">East US</span></span> |<span data-ttu-id="1d6c5-162">ClassicVNetLocal(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-162">ClassicVNetLocal (10.0.0.0/24)</span></span> |

## <span data-ttu-id="1d6c5-163"><a name="classicvnet"></a>1. 클래식 VNet 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1d6c5-163"><a name="classicvnet"></a>1. Configure the classic VNet settings</span></span>

<span data-ttu-id="1d6c5-164">이 섹션에서는 클래식 VNet에 대한 로컬 네트워크(로컬 사이트) 및 가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-164">In this section, you create the local network (local site) and the virtual network gateway for your classic VNet.</span></span> <span data-ttu-id="1d6c5-165">클래식 VNet이 없는 상태에서 이 단계를 연습으로 실행하는 경우에는 [이 문서](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)와 위의 [예제](#values) 설정 값을 사용하여 VNet을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-165">If you don't have a classic VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) and the [Example](#values) settings values from above.</span></span>

<span data-ttu-id="1d6c5-166">포털을 사용하여 클래식 가상 네트워크를 만들 때 다음 단계를 사용하여 가상 네트워크 블레이드로 이동해야 합니다. 그렇지 않으면 가상 네트워크를 만드는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-166">When using the portal to create a classic virtual network, you must navigate to the virtual network blade by using the following steps, otherwise the option to create a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="1d6c5-167">'+'를 클릭하여 '새로 만들기' 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-167">Click the '+' to open the 'New' blade.</span></span>
2. <span data-ttu-id="1d6c5-168">‘Marketplace 검색’ 필드에 ‘가상 네트워크’를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-168">In the 'Search the marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="1d6c5-169">대신, 네트워킹 -> 가상 네트워크를 선택한 경우 클래식 VNet을 만드는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-169">If you instead, select Networking -> Virtual Network, you will not get the option to create a classic VNet.</span></span>
3. <span data-ttu-id="1d6c5-170">반환된 목록에서 ‘가상 네트워크’를 찾아서 클릭하여 가상 네트워크 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-170">Locate 'Virtual Network' from the returned list and click it to open the Virtual Network blade.</span></span> 
4. <span data-ttu-id="1d6c5-171">가상 네트워크 블레이드에서 '클래식'을 선택하여 클래식 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-171">On the virtual network blade, select 'Classic' to create a classic VNet.</span></span> 

<span data-ttu-id="1d6c5-172">VPN 게이트웨이가 있는 VNet이 이미 있는 경우 해다 게이트웨이가 동적인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-172">If you already have a VNet with a VPN gateway, verify that the gateway is Dynamic.</span></span> <span data-ttu-id="1d6c5-173">정적인 경우에는 먼저 VPN 게이트웨이를 삭제한 후 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-173">If it's Static, you must first delete the VPN gateway, then proceed.</span></span>

<span data-ttu-id="1d6c5-174">스크린샷은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-174">Screenshots are provided as examples.</span></span> <span data-ttu-id="1d6c5-175">값을 사용자의 값으로 대체하거나 [예제](#values) 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-175">Be sure to replace the values with your own, or use the [Example](#values) values.</span></span>

### <a name="part-1---configure-the-local-site"></a><span data-ttu-id="1d6c5-176">1부 - 로컬 사이트 구성</span><span class="sxs-lookup"><span data-stu-id="1d6c5-176">Part 1 - Configure the local site</span></span>

<span data-ttu-id="1d6c5-177">[클래식 포털](https://ms.portal.azure.com)을 열고 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-177">Open the [Azure portal](https://ms.portal.azure.com) and sign in with your Azure account.</span></span>

1. <span data-ttu-id="1d6c5-178">**모든 리소스**로 이동하여 목록에서 **ClassicVNet**을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-178">Navigate to **All resources** and locate the **ClassicVNet** in the list.</span></span>
2. <span data-ttu-id="1d6c5-179">**개요** 블레이드의 **VPN 연결** 섹션에서 **게이트웨이** 그래픽을 클릭하여 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-179">On the **Overview** blade, in the **VPN connections** section, click the **Gateway** graphic to create a gateway.</span></span>

    <span data-ttu-id="1d6c5-180">![VPN 게이트웨이 구성](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "VPN 게이트웨이 구성")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-180">![Configure a VPN gateway](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configure a VPN gateway")</span></span>
3. <span data-ttu-id="1d6c5-181">**새 VPN 연결** 블레이드에서 **연결 유형**으로 **사이트 간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-181">On the **New VPN Connection** blade, for **Connection type**, select **Site-to-site**.</span></span>
4. <span data-ttu-id="1d6c5-182">**로컬 사이트**로 **필요한 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-182">For **Local site**, click **Configure required settings**.</span></span> <span data-ttu-id="1d6c5-183">그러면 **로컬 사이트** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-183">This opens the **Local site** blade.</span></span>
5. <span data-ttu-id="1d6c5-184">**로컬 사이트** 블레이드에서 Resource Manager VNet을 언급하는 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-184">On the **Local site** blade, create a name to refer to the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-185">예: 'RMVNetLocal'.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-185">For example, 'RMVNetLocal'.</span></span>
6. <span data-ttu-id="1d6c5-186">Resource Manager VNet에 대한 VPN 게이트웨이에 공용 IP 주소가 이미 있는 경우 **VPN 게이트웨이 IP 주소** 필드의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-186">If the VPN gateway for the Resource Manager VNet already has a Public IP address, use the value for the **VPN gateway IP address** field.</span></span> <span data-ttu-id="1d6c5-187">이 단계를 연습으로 수행하는 경우 또는 아직 Resource Manager VNet에 대한 가상 네트워크 게이트웨이가 없는 경우 자리 표시자 IP 주소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-187">If you are doing these steps as an exercise, or don't yet have a virtual network gateway for your Resource Manager VNet, you can make up a placeholder IP address.</span></span> <span data-ttu-id="1d6c5-188">자리 표시자 IP 주소 형식이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-188">Make sure that the placeholder IP address uses a valid format.</span></span> <span data-ttu-id="1d6c5-189">나중에 자리 표시자 IP 주소를 Resource Manager 가상 네트워크 게이트웨이의 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-189">Later, you replace the placeholder IP address with the Public IP address of the Resource Manager virtual network gateway.</span></span>
7. <span data-ttu-id="1d6c5-190">**클라이언트 주소 공간**에 Resource Manager VNet에 대한 가상 네트워크 IP 주소 공간 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-190">For **Client Address Space**, use the values for the virtual network IP address spaces for the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-191">이 설정은 Resource Manager 가상 네트워크로 라우팅할 주소 공간을 지정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-191">This setting is used to specify the address spaces to route to the Resource Manager virtual network.</span></span>
8. <span data-ttu-id="1d6c5-192">**확인**을 클릭하여 값을 저장하고 **새 VPN 연결** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-192">Click **OK** to save the values and return to the **New VPN Connection** blade.</span></span>

### <a name="part-2---create-the-virtual-network-gateway"></a><span data-ttu-id="1d6c5-193">2부 - 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-193">Part 2 - Create the virtual network gateway</span></span>

1. <span data-ttu-id="1d6c5-194">**새 VPN 연결** 블레이드에서 **게이트웨이 즉시 만들기** 확인란을 선택하고 **선택적 게이트웨이 구성**을 클릭하여 **게이트웨이 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-194">On the **New VPN Connection** blade, select the **Create gateway immediately** checkbox and click **Optional gateway configuration** to open the **Gateway configuration** blade.</span></span> 

    <span data-ttu-id="1d6c5-195">![게이트웨이 구성 블레이드 열기](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "게이트웨이 구성 블레이드 열기")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-195">![Open gateway configuration blade](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Open gateway configuration blade")</span></span>
2. <span data-ttu-id="1d6c5-196">**서브넷 - 필요한 설정 구성**을 클릭하여 **서브넷 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-196">Click **Subnet - Configure required settings** to open the **Add subnet** blade.</span></span> <span data-ttu-id="1d6c5-197">**이름**이 필수 값인 **GatewaySubnet**으로 이미 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-197">The **Name** is already configured with the required value **GatewaySubnet**.</span></span>
3. <span data-ttu-id="1d6c5-198">**주소 범위**는 게이트웨이 서브넷에 대한 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-198">The **Address range** refers to the range for the gateway subnet.</span></span> <span data-ttu-id="1d6c5-199">게이트웨이 서브넷을 /29 주소 범위(주소 3개)로 만들 수 있지만 더 많은 IP 주소를 포함하는 게이트웨이 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-199">Although you can create a gateway subnet with a /29 address range (3 addresses), we recommend creating a gateway subnet that contains more IP addresses.</span></span> <span data-ttu-id="1d6c5-200">그러면 사용 가능한 IP 주소가 필요할 수 있는 향후 구성을 수용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-200">This will accommodate future configurations that may require more available IP addresses.</span></span> <span data-ttu-id="1d6c5-201">가능하면 /27 또는 /28을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-201">If possible, use /27 or /28.</span></span> <span data-ttu-id="1d6c5-202">이 단계를 연습으로 사용하는 경우 다음 [예제](#values) 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-202">If you are using these steps as an exercise, you can refer to the [Example](#values) values.</span></span> <span data-ttu-id="1d6c5-203">**확인**을 클릭하여 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-203">Click **OK** to create the gateway subnet.</span></span>
4. <span data-ttu-id="1d6c5-204">**게이트웨이 구성** 블레이드에서 **크기**는 게이트웨이 SKU를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-204">On the **Gateway configuration** blade, **Size** refers to the gateway SKU.</span></span> <span data-ttu-id="1d6c5-205">VPN 게이트웨이에 대한 게이트웨이 SKU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-205">Select the gateway SKU for your VPN gateway.</span></span>
5. <span data-ttu-id="1d6c5-206">**라우팅 유형**이 **동적**인지 확인하고 **확인**을 클릭하여 **새 VPN 연결** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-206">Verify the **Routing Type** is **Dynamic**, then click **OK** to return to the **New VPN Connection** blade.</span></span>
6. <span data-ttu-id="1d6c5-207">**새 VPN 연결** 블레이드에서 **확인**을 클릭하여 VPN 게이트웨이 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-207">On the **New VPN Connection** blade, click **OK** to begin creating your VPN gateway.</span></span> <span data-ttu-id="1d6c5-208">VPN 게이트웨이 만들기를 완료하는 데 최대 45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-208">Creating a VPN gateway can take up to 45 minutes to complete.</span></span>

### <span data-ttu-id="1d6c5-209"><a name="ip"></a>3부 - 가상 네트워크 게이트웨이 공용 IP 주소 복사</span><span class="sxs-lookup"><span data-stu-id="1d6c5-209"><a name="ip"></a>Part 3 - Copy the virtual network gateway Public IP address</span></span>

<span data-ttu-id="1d6c5-210">가상 네트워크 게이트웨이를 만든 후에 게이트웨이 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-210">After the virtual network gateway has been created, you can view the gateway IP address.</span></span> 

1. <span data-ttu-id="1d6c5-211">클래식 VNet으로 이동한 후 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-211">Navigate to your classic VNet, and click **Overview**.</span></span>
2. <span data-ttu-id="1d6c5-212">**VPN 연결**을 클릭하여 VPN 연결 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-212">Click **VPN connections** to open the VPN connections blade.</span></span> <span data-ttu-id="1d6c5-213">VPN 연결 블레이드에서 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-213">On the VPN connections blade, you can view the Public IP address.</span></span> <span data-ttu-id="1d6c5-214">이 주소는 가상 네트워크 게이트웨이에 할당된 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-214">This is the Public IP address assigned to your virtual network gateway.</span></span> 
3. <span data-ttu-id="1d6c5-215">공용 IP 주소를 적어두거나 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-215">Write down or copy the IP address.</span></span> <span data-ttu-id="1d6c5-216">나중 단계에서 Resource Manager 로컬 네트워크 게이트웨이 구성 설정 관련 작업을 수행할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-216">You use it in later steps when you work with your Resource Manager local network gateway configuration settings.</span></span> <span data-ttu-id="1d6c5-217">게이트웨이 연결의 상태를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-217">You can also view the status of your gateway connections.</span></span> <span data-ttu-id="1d6c5-218">만든 로컬 네트워크 사이트는 '연결 중'으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-218">Notice the local network site you created is listed as 'Connecting'.</span></span> <span data-ttu-id="1d6c5-219">연결을 만든 후에는 상태가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-219">The status will change after you have created your connections.</span></span>
4. <span data-ttu-id="1d6c5-220">게이트웨이 IP 주소를 복사한 후 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-220">Close the blade after copying the gateway IP address.</span></span>

## <span data-ttu-id="1d6c5-221"><a name="rmvnet"></a>2. Resource Manager VNet 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1d6c5-221"><a name="rmvnet"></a>2. Configure the Resource Manager VNet settings</span></span>

<span data-ttu-id="1d6c5-222">이 섹션에서는 Resource Manager VNet에 대한 가상 네트워크 게이트웨이 및 로컬 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-222">In this section, you create the virtual network gateway and the local network gateway for your Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-223">Resource Manager VNet이 없는 상태에서 이 단계를 연습으로 실행하는 경우에는 [이 문서](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)와 위의 [예제](#values) 설정 값을 사용하여 VNet을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-223">If you don't have a Resource Manager VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and the [Example](#values) settings values from above.</span></span>

<span data-ttu-id="1d6c5-224">스크린샷은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-224">Screenshots are provided as examples.</span></span> <span data-ttu-id="1d6c5-225">값을 사용자의 값으로 대체하거나 [예제](#values) 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-225">Be sure to replace the values with your own, or use the [Example](#values) values.</span></span>

### <a name="part-1---create-a-gateway-subnet"></a><span data-ttu-id="1d6c5-226">1부 - 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-226">Part 1 - Create a gateway subnet</span></span>

<span data-ttu-id="1d6c5-227">가상 네트워크 게이트웨이를 구성하려면 먼저 게이트웨이 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-227">Before creating a virtual network gateway, you first need to create the gateway subnet.</span></span> <span data-ttu-id="1d6c5-228">CIDR 개수가 /28 이상인 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-228">Create a gateway subnet with CIDR count of /28 or larger.</span></span> <span data-ttu-id="1d6c5-229">(/27, /26 등)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-229">(/27, /26, etc.)</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a><span data-ttu-id="1d6c5-230">2부 - 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-230">Part 2 - Create a virtual network gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <span data-ttu-id="1d6c5-231"><a name="createlng"></a>3부 - 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-231"><a name="createlng"></a>Part 3 - Create a local network gateway</span></span>

<span data-ttu-id="1d6c5-232">로컬 네트워크 게이트웨이는 클래식 VNet 및 가상 네트워크 게이트웨이에 연결된 주소 범위 및 공용 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-232">The local network gateway specifies the address range and the Public IP address associated with your classic VNet and its virtual network gateway.</span></span>

<span data-ttu-id="1d6c5-233">이 단계를 연습으로 수행하는 경우 다음 설정을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-233">If you are doing these steps as an exercise, refer to these settings:</span></span>

| <span data-ttu-id="1d6c5-234">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1d6c5-234">Virtual Network</span></span> | <span data-ttu-id="1d6c5-235">주소 공간</span><span class="sxs-lookup"><span data-stu-id="1d6c5-235">Address Space</span></span> | <span data-ttu-id="1d6c5-236">지역</span><span class="sxs-lookup"><span data-stu-id="1d6c5-236">Region</span></span> | <span data-ttu-id="1d6c5-237">로컬 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="1d6c5-237">Connects to local network site</span></span> |<span data-ttu-id="1d6c5-238">게이트웨이 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="1d6c5-238">Gateway Public IP address</span></span>|
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="1d6c5-239">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-239">ClassicVNet</span></span> |<span data-ttu-id="1d6c5-240">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-240">(10.0.0.0/24)</span></span> |<span data-ttu-id="1d6c5-241">미국 서부</span><span class="sxs-lookup"><span data-stu-id="1d6c5-241">West US</span></span> | <span data-ttu-id="1d6c5-242">RMVNetLocal(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-242">RMVNetLocal (192.168.0.0/16)</span></span> |<span data-ttu-id="1d6c5-243">ClassicVNet 게이트웨이에 할당된 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="1d6c5-243">The Public IP address that is assigned to the ClassicVNet gateway</span></span>|
| <span data-ttu-id="1d6c5-244">RMVNet</span><span class="sxs-lookup"><span data-stu-id="1d6c5-244">RMVNet</span></span> | <span data-ttu-id="1d6c5-245">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-245">(192.168.0.0/16)</span></span> |<span data-ttu-id="1d6c5-246">미국 동부</span><span class="sxs-lookup"><span data-stu-id="1d6c5-246">East US</span></span> |<span data-ttu-id="1d6c5-247">ClassicVNetLocal(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="1d6c5-247">ClassicVNetLocal (10.0.0.0/24)</span></span> |<span data-ttu-id="1d6c5-248">RMVNet 게이트웨이에 할당된 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="1d6c5-248">The Public IP address that is assigned to the RMVNet gateway.</span></span>|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <span data-ttu-id="1d6c5-249"><a name="modifylng"></a>3. 클래식 VNet 로컬 사이트 설정 수정</span><span class="sxs-lookup"><span data-stu-id="1d6c5-249"><a name="modifylng"></a>3. Modify the classic VNet local site settings</span></span>

<span data-ttu-id="1d6c5-250">이 섹션에서는 로컬 사이트 설정을 지정할 때 사용한 자리 표시자 IP 주소를 Resource Manager VPN 게이트웨이 IP 주소와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-250">In this section, you replace the placeholder IP address that you used when specifying the local site settings, with the Resource Manager VPN gateway IP address.</span></span> <span data-ttu-id="1d6c5-251">이 섹션에서는 클래식(SM) PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-251">This section uses the classic (SM) PowerShell cmdlets.</span></span>

1. <span data-ttu-id="1d6c5-252">Azure Portal에서 클래식 가상 네트워크로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-252">In the Azure portal, navigate to the classic virtual network.</span></span>
2. <span data-ttu-id="1d6c5-253">가상 네트워크에 대한 블레이드에서 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-253">On the blade for your virtual network, click **Overview**.</span></span>
3. <span data-ttu-id="1d6c5-254">**VPN 연결** 섹션에서 그래픽의 로컬 사이트 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-254">In the **VPN connections** section, click the name of your local site in the graphic.</span></span>

    <span data-ttu-id="1d6c5-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN 연결")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN Connections")</span></span>
4. <span data-ttu-id="1d6c5-256">**사이트 간 VPN 연결** 블레이드에서 사이트의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-256">On the **Site-to-site VPN connections** blade, click the name of the site.</span></span>

    <span data-ttu-id="1d6c5-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "로컬 사이트 이름")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Local site name")</span></span>
5. <span data-ttu-id="1d6c5-258">로컬 사이트에 대한 연결 블레이드에서 로컬 사이트의 이름을 클릭하여 **로컬 사이트** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-258">On the connection blade for your local site, click the name of the local site to open the **Local site** blade.</span></span>

    <span data-ttu-id="1d6c5-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "로컬 사이트 열기")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Open local site")</span></span>
6. <span data-ttu-id="1d6c5-260">**로컬 사이트** 블레이드에서 **VPN 게이트웨이 IP 주소**를 Resource Manager 게이트웨이의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-260">On the **Local site** blade, replace the **VPN gateway IP address** with the IP address of the Resource Manager gateway.</span></span>

    <span data-ttu-id="1d6c5-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "게이트웨이 IP 주소")</span><span class="sxs-lookup"><span data-stu-id="1d6c5-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Gateway IP address")</span></span>
7. <span data-ttu-id="1d6c5-262">**확인**을 클릭하여 IP 주소를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-262">Click **OK** to update the IP address.</span></span>

## <span data-ttu-id="1d6c5-263"><a name="RMtoclassic"></a>4. 클래식 연결에 대해 Resource Manager 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-263"><a name="RMtoclassic"></a>4. Create Resource Manager to classic connection</span></span>

<span data-ttu-id="1d6c5-264">이번 단계에서는 Azure Portal을 사용하여 Resource Manager VNet에서 클래식 VNet으로 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-264">In these steps, you configure the connection from the Resource Manager VNet to the classic VNet using the Azure portal.</span></span>

1. <span data-ttu-id="1d6c5-265">**모든 리소스**에서 로컬 네트워크 게이트웨이를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-265">In **All resources**, locate the local network gateway.</span></span> <span data-ttu-id="1d6c5-266">이 예제의 경우 로컬 네트워크 게이트웨이는 **ClassicVNetLocal**입니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-266">In our example, the local network gateway is **ClassicVNetLocal**.</span></span>
2. <span data-ttu-id="1d6c5-267">**구성**을 클릭하여 IP 주소 값이 클래식 VNet에 대한 VPN 게이트웨이인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-267">Click **Configuration** and verify that the IP address value is the VPN gateway for the classic VNet.</span></span> <span data-ttu-id="1d6c5-268">필요한 경우 업데이트하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-268">Update, if needed, then click **Save**.</span></span> <span data-ttu-id="1d6c5-269">블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-269">Close the blade.</span></span>
3. <span data-ttu-id="1d6c5-270">**모든 리소스**에서 로컬 네트워크 게이트웨이를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-270">In **All resources**, click the local network gateway.</span></span>
4. <span data-ttu-id="1d6c5-271">**연결**을 클릭하여 연결 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-271">Click **Connections** to open the Connections blade.</span></span>
5. <span data-ttu-id="1d6c5-272">**연결** 블레이드에서 **+**를 클릭하여 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-272">On the **Connections** blade, click **+** to add a connection.</span></span>
6. <span data-ttu-id="1d6c5-273">**연결 추가** 블레이드에서 연결의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-273">On the **Add connection** blade, name the connection.</span></span> <span data-ttu-id="1d6c5-274">예: 'RMtoClassic'.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-274">For example, 'RMtoClassic'.</span></span>
7. <span data-ttu-id="1d6c5-275">**사이트 간**이 블레이드에 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-275">**Site-to-Site** is already selected on this blade.</span></span>
8. <span data-ttu-id="1d6c5-276">이 사이트와 연결할 가상 네트워크 게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-276">Select the virtual network gateway that you want to associate with this site.</span></span>
9. <span data-ttu-id="1d6c5-277">**공유 키**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-277">Create a **shared key**.</span></span> <span data-ttu-id="1d6c5-278">이 키는 클래식 VNet에서 Resource Manager VNet에 만드는 연결에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-278">This key is also used in the connection that you create from the classic VNet to the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-279">키를 생성하거나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-279">You can generate the key or make one up.</span></span> <span data-ttu-id="1d6c5-280">이 예제에서는 'abc123'을 사용했지만 좀 더 복잡한 항목을 사용할 수 있고 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-280">In our example, we use 'abc123', but you can (and should) use something more complex.</span></span>
10. <span data-ttu-id="1d6c5-281">**확인**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-281">Click **OK** to create the connection.</span></span>

##<span data-ttu-id="1d6c5-282"><a name="classictoRM"></a>5. 클래식에서 Resource Manager 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-282"><a name="classictoRM"></a>5. Create classic to Resource Manager connection</span></span>

<span data-ttu-id="1d6c5-283">이번 단계에서는 클래식 VNet에서 Resource Manager VNet까지 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-283">In these steps, you configure the connection from the classic VNet to the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-284">이러한 단계에는 PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-284">These steps require PowerShell.</span></span> <span data-ttu-id="1d6c5-285">포털에서는 이 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-285">You can't create this connection in the portal.</span></span> <span data-ttu-id="1d6c5-286">클래식(SM) 및 Resource Manager(RM) PowerShell cmdlet을 모두 다운로드하고 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-286">Make sure you have downloaded and installed both the classic (SM) and Resource Manager (RM) PowerShell cmdlets.</span></span>

### <a name="1-connect-to-your-azure-account"></a><span data-ttu-id="1d6c5-287">1. Azure 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="1d6c5-287">1. Connect to your Azure account</span></span>

<span data-ttu-id="1d6c5-288">관리자 권한으로 PowerShell 콘솔을 열고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-288">Open the PowerShell console with elevated rights and log in to your Azure account.</span></span> <span data-ttu-id="1d6c5-289">다음 cmdlet가 Azure 계정에 대한 로그인 자격 증명을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-289">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="1d6c5-290">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-290">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

```powershell
Login-AzureRmAccount
```
   
<span data-ttu-id="1d6c5-291">둘 이상의 구독이 있는 경우 Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-291">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1d6c5-292">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-292">Specify the subscription that you want to use.</span></span> 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

<span data-ttu-id="1d6c5-293">Azure 계정을 추가하여 클래식 PowerShell cmdlet(SM)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-293">Add your Azure Account to use the classic PowerShell cmdlets (SM).</span></span> <span data-ttu-id="1d6c5-294">이렇게 하려면 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-294">To do so, you can use the following command:</span></span>

```powershell
Add-AzureAccount
```

### <a name="2-view-the-network-configuration-file-values"></a><span data-ttu-id="1d6c5-295">2. 네트워크 구성 파일 값 확인</span><span class="sxs-lookup"><span data-stu-id="1d6c5-295">2. View the network configuration file values</span></span>

<span data-ttu-id="1d6c5-296">Azure Portal에서 VNet을 만든 경우 Azure에서 사용되는 전체 이름은 Azure Portal에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-296">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the Azure portal.</span></span> <span data-ttu-id="1d6c5-297">예를 들어 Azure Portal에서 'ClassicVNet'이라는 이름으로 표시되는 VNet은 네트워크 구성 파일에 훨씬 더 긴 이름이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-297">For example, a VNet that appears to be named 'ClassicVNet' in the Azure portal may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="1d6c5-298">예를 들면 'Group ClassicRG ClassicVNet'과 같은 이름 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-298">The name might look something like: 'Group ClassicRG ClassicVNet'.</span></span> <span data-ttu-id="1d6c5-299">이 단계에서는 네트워크 구성 파일을 다운로드하고 값을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-299">In these steps, you download the network configuration file and view the values.</span></span>

<span data-ttu-id="1d6c5-300">컴퓨터에 디렉터리를 만들고 디렉터리에 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-300">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="1d6c5-301">이 예제에서는 네트워크 구성 파일을 C:\AzureNet으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-301">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="1d6c5-302">텍스트 편집기로 파일을 열고 클래식 VNet의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-302">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="1d6c5-303">PowerShell cmdlet을 실행할 때는 네트워크 구성 파일의 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-303">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

- <span data-ttu-id="1d6c5-304">VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-304">VNet names are listed as **VirtualNetworkSite name =**</span></span>
- <span data-ttu-id="1d6c5-305">사이트 이름은 **LocalNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-305">Site names are listed as **LocalNetworkSite name=**</span></span>

### <a name="3-create-the-connection"></a><span data-ttu-id="1d6c5-306">3. 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6c5-306">3. Create the connection</span></span>

<span data-ttu-id="1d6c5-307">공유 키를 설정하고 클래식 VNet에서 Resource Manager VNet으로 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-307">Set the shared key and create the connection from the classic VNet to the Resource Manager VNet.</span></span> <span data-ttu-id="1d6c5-308">포털을 사용하여 공유 키를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-308">You cannot set the shared key using the portal.</span></span> <span data-ttu-id="1d6c5-309">클래식 버전의 PowerShell cmdlet을 사용하여 로그인한 상태에서 이러한 단계를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-309">Make sure you run these steps while logged in using the classic version of the PowerShell cmdlets.</span></span> <span data-ttu-id="1d6c5-310">이 작업에는 **Add-AzureAccount**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-310">To do so, use **Add-AzureAccount**.</span></span> <span data-ttu-id="1d6c5-311">그러지 않으면 '-AzureVNetGatewayKey'를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-311">Otherwise, you will not be able to set the '-AzureVNetGatewayKey'.</span></span>

- <span data-ttu-id="1d6c5-312">이 예제에서 **-VNetName**은 클래식 VNet의 이름이며 네트워크 구성 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-312">In this example, **-VNetName** is the name of the classic VNet as found in your network configuration file.</span></span> 
- <span data-ttu-id="1d6c5-313">**-LocalNetworkSiteName**은 로컬 사이트에 대해 지정한 이름이며 네트워크 구성 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-313">The **-LocalNetworkSiteName** is the name you specified for the local site, as found in your network configuration file.</span></span>
- <span data-ttu-id="1d6c5-314">**-SharedKey**는 사용자가 생성하고 지정하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-314">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="1d6c5-315">이 예제에서는 *abc123*을 사용했으나 좀 더 복잡한 항목을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-315">For this example, we used *abc123*, but you can generate something more complex.</span></span> <span data-ttu-id="1d6c5-316">중요한 점은 여기에서 지정한 값이 클래식 연결에 대해 Resource Manager를 만들 때 지정한 값과 동일해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-316">The important thing is that the value you specify here must be the same value that you specified when creating your Resource Manager to classic connection.</span></span>

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<span data-ttu-id="1d6c5-317"><a name="verify"></a>6. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="1d6c5-317"><a name="verify"></a>6. Verify your connections</span></span>

<span data-ttu-id="1d6c5-318">Azure Portal 또는 PowerShell을 사용하여 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-318">You can verify your connections by using the Azure portal or PowerShell.</span></span> <span data-ttu-id="1d6c5-319">확인 시, 연결이 만들어지는 동안 1~2분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-319">When verifying, you may need to wait a minute or two as the connection is being created.</span></span> <span data-ttu-id="1d6c5-320">연결이 완료되면 연결 상태가 '연결 중'에서 '연결됨'으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6c5-320">When a connection is successful, the connectivity state changes from 'Connecting' to 'Connected'.</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="1d6c5-321">클래식 VNet에서 Resource Manager VNet으로의 연결을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="1d6c5-321">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="1d6c5-322">Resource Manager VNet에서 클래식 VNet으로의 연결을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="1d6c5-322">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="1d6c5-323"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="1d6c5-323"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
