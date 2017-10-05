---
title: "온-프레미스 네트워크를 Azure Virtual Network에 연결: 사이트 간 VPN: Portal | Microsoft Docs"
description: "공용 인터넷을 통해 온-프레미스 네트워크에서 Azure Virtual Network에 IPsec을 만드는 단계입니다. 이 단계는 포털을 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="54dc0-104">Azure Portal에서 사이트 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="54dc0-105">이 문서에서는 Azure Portal을 사용하여 온-프레미스 네트워크에서 VNet으로 사이트 간 VPN Gateway 연결을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="54dc0-106">이 문서의 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="54dc0-107">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54dc0-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="54dc0-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="54dc0-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54dc0-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="54dc0-110">CLI</span><span class="sxs-lookup"><span data-stu-id="54dc0-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="54dc0-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="54dc0-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="54dc0-112">사이트 간 VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통해 온-프레미스 네트워크를 Azure Virtual Network에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="54dc0-113">이 연결 유형은 할당된 외부 연결 공용 IP 주소를 갖고 있는 온-프레미스에 있는 VPN 장치를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="54dc0-114">VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="54dc0-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="54dc0-116">Before you begin</span></span>

<span data-ttu-id="54dc0-117">구성을 시작하기 전에 다음 기준을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="54dc0-118">호환되는 VPN 장치 및 이 장치를 구성할 수 있는 사람이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="54dc0-119">호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="54dc0-120">VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="54dc0-121">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="54dc0-122">온-프레미스 네트워크에 있는 IP 주소 범위에 익숙하지 않은 경우 세부 정보를 제공할 수 있는 다른 사람의 도움을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="54dc0-123">이 구성을 만들 때 Azure가 온-프레미스 위치에 라우팅할 IP 주소 범위 접두사를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="54dc0-124">온-프레미스 네트워크의 어떤 서브넷도 사용자가 연결하려는 가상 네트워크 서브넷과 중첩될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="54dc0-125"><a name="values"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="54dc0-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="54dc0-126">이 문서의 예제에서는 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-126">The examples in this article use the following values.</span></span> <span data-ttu-id="54dc0-127">이러한 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 보다 정확하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="54dc0-128">**VNet 이름:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="54dc0-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="54dc0-129">**주소 공간:**</span><span class="sxs-lookup"><span data-stu-id="54dc0-129">**Address Space:**</span></span> 
  * <span data-ttu-id="54dc0-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="54dc0-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="54dc0-131">10.12.0.0/16(이 연습의 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="54dc0-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="54dc0-132">**서브넷:**</span><span class="sxs-lookup"><span data-stu-id="54dc0-132">**Subnets:**</span></span>
  * <span data-ttu-id="54dc0-133">프런트 엔드: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="54dc0-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="54dc0-134">백 엔드: 10.12.0.0/24(이 연습의 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="54dc0-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="54dc0-135">**게이트웨이 서브넷:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="54dc0-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="54dc0-136">**리소스 그룹:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="54dc0-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="54dc0-137">**위치:** 미국 동부</span><span class="sxs-lookup"><span data-stu-id="54dc0-137">**Location:** East US</span></span>
* <span data-ttu-id="54dc0-138">**DNS 서버:** 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="54dc0-139">DNS 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="54dc0-140">**Virtual Network 게이트웨이 이름:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="54dc0-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="54dc0-141">**공용 IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="54dc0-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="54dc0-142">**VPN 유형:** 경로 기반</span><span class="sxs-lookup"><span data-stu-id="54dc0-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="54dc0-143">**연결 형식:** 사이트 간(IPsec)</span><span class="sxs-lookup"><span data-stu-id="54dc0-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="54dc0-144">**게이트웨이 유형:** VPN</span><span class="sxs-lookup"><span data-stu-id="54dc0-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="54dc0-145">**로컬 네트워크 게이트웨이 이름:** Site2</span><span class="sxs-lookup"><span data-stu-id="54dc0-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="54dc0-146">**연결 이름:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="54dc0-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="54dc0-147"><a name="CreatVNet"></a>1. 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="54dc0-148"><a name="dns"></a>2. DNS 서버 지정</span><span class="sxs-lookup"><span data-stu-id="54dc0-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="54dc0-149">DNS는 사이트 간 연결을 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="54dc0-150">하지만 가상 네트워크에 배포된 리소스에 대한 이름을 확인하려는 경우 DNS 서버를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="54dc0-151">이 설정을 통해 이 가상 네트워크에 대한 이름을 확인하는 데 사용하려는 DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="54dc0-152">DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-152">It does not create a DNS server.</span></span> <span data-ttu-id="54dc0-153">이름 확인에 대한 자세한 내용은 [VM에서 이름 확인 및 역할 인스턴스](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="54dc0-154"><a name="gatewaysubnet"></a>3. 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="54dc0-155"><a name="VNetGateway"></a>4. VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="54dc0-156"><a name="LocalNetworkGateway"></a>5. 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="54dc0-157">로컬 네트워크 게이트웨이는 일반적으로 온-프레미스 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="54dc0-158">Azure가 참조할 수 있는 사이트 이름을 지정한 다음 연결을 만들 온-프레미스 VPN 장치의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="54dc0-159">또한 VPN Gateway를 통해 VPN 장치로 라우팅될 IP 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="54dc0-160">사용자가 지정하는 주소 접두사는 온-프레미스 네트워크에 있는 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="54dc0-161">온-프레미스 네트워크가 변경되거나 VPN 장치에서 공용 IP 주소를 변경해야 하는 경우 나중에 값을 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="54dc0-162"><a name="VPNDevice"></a>6. VPN 장치 구성</span><span class="sxs-lookup"><span data-stu-id="54dc0-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="54dc0-163">온-프레미스 네트워크에 대한 사이트 간 연결에는 VPN 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="54dc0-164">이 단계에서는 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="54dc0-165">VPN 장치를 구성할 때 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="54dc0-166">공유 키 -</span><span class="sxs-lookup"><span data-stu-id="54dc0-166">A shared key.</span></span> <span data-ttu-id="54dc0-167">사이트 간 VPN 연결을 만들 때 지정하는 것과 동일한 공유 키입니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="54dc0-168">이 예제에서는 기본적인 공유 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="54dc0-169">실제로 사용할 키는 좀 더 복잡하게 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="54dc0-170">가상 네트워크 게이트웨이의 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="54dc0-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="54dc0-171">Azure Portal, PowerShell 또는 CLI를 사용하여 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="54dc0-172">Azure Portal을 사용하여 VPN Gateway의 공용 IP 주소를 찾으려면 **가상 네트워크 게이트웨이**로 이동한 다음 게이트웨이의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="54dc0-173"><a name="CreateConnection"></a>7. VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="54dc0-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="54dc0-174">가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 사이의 사이트 간 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="54dc0-175"><a name="VerifyConnection"></a>8. VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="54dc0-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="54dc0-176"><a name="connectVM"></a>가상 컴퓨터에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="54dc0-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="54dc0-177"><a name="reset"></a>VPN 게이트웨이를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="54dc0-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="54dc0-178">Azure VPN Gateway 재설정은 하나 이상의 사이트 간 VPN 터널에서 크로스-프레미스 VPN 연결이 손실되는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="54dc0-179">이 상황에서 온-프레미스 VPN 장치는 모두 올바르게 작동하지만 Azure VPN 게이트웨이와 IPsec 터널을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54dc0-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="54dc0-180">자세한 단계는 [VPN 게이트웨이 다시 설정](vpn-gateway-resetgw-classic.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="54dc0-181"><a name="resize"></a>게이트웨이 SKU를 변경하는 방법(게이트웨이 크기 조정)</span><span class="sxs-lookup"><span data-stu-id="54dc0-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="54dc0-182">게이트웨이 SKU를 변경하는 단계는 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54dc0-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54dc0-183">Next steps</span></span>

* <span data-ttu-id="54dc0-184">BGP에 대한 내용은 [BGP 개요](vpn-gateway-bgp-overview.md) 및 [BGP를 구성하는 방법](vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="54dc0-185">강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="54dc0-186">항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54dc0-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
