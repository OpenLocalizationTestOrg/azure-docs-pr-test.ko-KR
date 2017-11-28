---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN: 포털 | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 다음이 단계를 사용 하면 hello 포털을 사용 하는 크로스-프레미스 사이트 간 VPN 게이트웨이 연결을 만들 수 있습니다."
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
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="43f17-104">Hello Azure 포털에서에서 사이트 간 연결을 만들려면</span><span class="sxs-lookup"><span data-stu-id="43f17-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="43f17-105">이 문서에서는 어떻게 toouse hello Azure 포털 toocreate 온-프레미스 네트워크 toohello VNet에서에서 사이트 간 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="43f17-106">이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="43f17-107">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43f17-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="43f17-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="43f17-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43f17-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="43f17-110">CLI</span><span class="sxs-lookup"><span data-stu-id="43f17-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="43f17-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="43f17-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="43f17-112">사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="43f17-113">이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="43f17-114">VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="43f17-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="43f17-116">Before you begin</span></span>

<span data-ttu-id="43f17-117">Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="43f17-118">호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="43f17-119">호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="43f17-120">VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="43f17-121">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="43f17-122">온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="43f17-123">이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="43f17-124">온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="43f17-125"><a name="values"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="43f17-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="43f17-126">이 문서의 hello 예제는 다음 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="43f17-127">이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="43f17-128">**VNet 이름:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="43f17-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="43f17-129">**주소 공간:**</span><span class="sxs-lookup"><span data-stu-id="43f17-129">**Address Space:**</span></span> 
  * <span data-ttu-id="43f17-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="43f17-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="43f17-131">10.12.0.0/16(이 연습의 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="43f17-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="43f17-132">**서브넷:**</span><span class="sxs-lookup"><span data-stu-id="43f17-132">**Subnets:**</span></span>
  * <span data-ttu-id="43f17-133">프런트 엔드: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="43f17-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="43f17-134">백 엔드: 10.12.0.0/24(이 연습의 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="43f17-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="43f17-135">**게이트웨이 서브넷:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="43f17-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="43f17-136">**리소스 그룹:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="43f17-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="43f17-137">**위치:** 미국 동부</span><span class="sxs-lookup"><span data-stu-id="43f17-137">**Location:** East US</span></span>
* <span data-ttu-id="43f17-138">**DNS 서버:** 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="43f17-139">hello DNS 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="43f17-140">**Virtual Network 게이트웨이 이름:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="43f17-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="43f17-141">**공용 IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="43f17-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="43f17-142">**VPN 유형:** 경로 기반</span><span class="sxs-lookup"><span data-stu-id="43f17-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="43f17-143">**연결 형식:** 사이트 간(IPsec)</span><span class="sxs-lookup"><span data-stu-id="43f17-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="43f17-144">**게이트웨이 유형:** VPN</span><span class="sxs-lookup"><span data-stu-id="43f17-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="43f17-145">**로컬 네트워크 게이트웨이 이름:** Site2</span><span class="sxs-lookup"><span data-stu-id="43f17-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="43f17-146">**연결 이름:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="43f17-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="43f17-147"><a name="CreatVNet"></a>1. 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="43f17-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="43f17-148"><a name="dns"></a>2. DNS 서버 지정</span><span class="sxs-lookup"><span data-stu-id="43f17-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="43f17-149">DNS 필요한 toocreate 사이트-사이트 연결이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="43f17-150">그러나 tooyour 배포 된 가상 네트워크 리소스에 대 한 toohave 이름 확인 하려는 경우에 DNS 서버를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="43f17-151">이 설정을 사용 하면이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 hello DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="43f17-152">DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-152">It does not create a DNS server.</span></span> <span data-ttu-id="43f17-153">이름 확인에 대한 자세한 내용은 [VM에서 이름 확인 및 역할 인스턴스](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="43f17-154"><a name="gatewaysubnet"></a>3. Hello 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="43f17-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="43f17-155"><a name="VNetGateway"></a>4. Hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="43f17-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="43f17-156"><a name="LocalNetworkGateway"></a>5. Hello 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="43f17-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="43f17-157">일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="43f17-158">Hello 사이트 기준인 Azure 수 tooit를 참조 하십시오. 그런 다음 hello IP 주소를 지정 된 이름을 지정 hello 온-프레미스 VPN 장치 toowhich의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="43f17-159">또한 hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="43f17-160">지정 하는 hello 주소 접두사는 온-프레미스 네트워크에 있는 hello 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="43f17-161">온-프레미스 네트워크 변경 되거나 hello VPN 장치에 대 한 toochange hello 공용 IP 주소 필요, 나중에 hello 값을 업데이트할 쉽게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="43f17-162"><a name="VPNDevice"></a>6. VPN 장치 구성</span><span class="sxs-lookup"><span data-stu-id="43f17-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="43f17-163">사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="43f17-164">이 단계에서는 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="43f17-165">VPN 장치를 구성할 때 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="43f17-166">공유 키 -</span><span class="sxs-lookup"><span data-stu-id="43f17-166">A shared key.</span></span> <span data-ttu-id="43f17-167">동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="43f17-168">이 예제에서는 기본적인 공유 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="43f17-169">더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="43f17-170">가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="43f17-171">Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="43f17-172">toofind hello hello Azure 포털을 사용 하 여 VPN 게이트웨이의 공용 IP 주소를 너무 탐색**가상 네트워크 게이트웨이**, 게이트웨이의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="43f17-173"><a name="CreateConnection"></a>7. Hello VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="43f17-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="43f17-174">가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 간의 hello 사이트 간 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="43f17-175"><a name="VerifyConnection"></a>8. Hello VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="43f17-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="43f17-176"><a name="connectVM"></a>tooconnect tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="43f17-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="43f17-177"><a name="reset"></a>어떻게 tooreset VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="43f17-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="43f17-178">Azure VPN Gateway 재설정은 하나 이상의 사이트 간 VPN 터널에서 크로스-프레미스 VPN 연결이 손실되는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="43f17-179">이 경우 온-프레미스 VPN 장치는 모든 정상적으로 작동 하지만 수 없습니다. tooestablish IPsec 터널 hello Azure VPN 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="43f17-180">자세한 단계는 [VPN 게이트웨이 다시 설정](vpn-gateway-resetgw-classic.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="43f17-181"><a name="resize"></a>어떻게 toochange 게이트웨이 SKU (게이트웨이 크기 조정)</span><span class="sxs-lookup"><span data-stu-id="43f17-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="43f17-182">Hello 게이트웨이 SKU toochange를 단계에 대 한 참조 [게이트웨이 Sku](vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43f17-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43f17-183">Next steps</span></span>

* <span data-ttu-id="43f17-184">BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43f17-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="43f17-185">강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="43f17-186">항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f17-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
