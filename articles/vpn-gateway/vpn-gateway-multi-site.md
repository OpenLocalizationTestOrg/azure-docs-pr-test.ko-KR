---
title: "VPN Gateway 및 PowerShell을 사용하여 가상 네트워크를 여러 사이트에 연결: 클래식 | Microsoft Docs"
description: "이 문서에서는 클래식 배포 모델에서 VPN 게이트웨이를 사용하여 여러 로컬 온-프레미스 사이트를 가상 네트워크에 연결하는 과정을 설명합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: bb3129f70f5eeed99d5889226aa6727f675b6217
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="f5607-103">기존 VPN Gateway 연결이 있는 VNet에 사이트 간 연결 추가(클래식)</span><span class="sxs-lookup"><span data-stu-id="f5607-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5607-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f5607-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="f5607-105">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f5607-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="f5607-106">이 문서에서는 PowerShell을 사용하여 기존 연결이 있는 VPN 게이트웨이에 S2S(사이트 간) 연결을 추가하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="f5607-107">이러한 유형의 연결을 "다중 사이트" 구성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="f5607-108">이 문서의 단계는 클래식 배포 모델(서비스 관리라고도 함)을 사용하여 만들어진 가상 네트워크에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="f5607-109">이러한 단계가 Express 경로/사이트 간 공존 연결 구성에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="f5607-110">배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="f5607-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="f5607-111">새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="f5607-112">문서를 사용할 수 있는 경우 표에서 직접 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-112">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="f5607-113">연결 정보</span><span class="sxs-lookup"><span data-stu-id="f5607-113">About connecting</span></span>

<span data-ttu-id="f5607-114">단일 가상 네트워크에 여러 온-프레미스 사이트를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-114">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="f5607-115">이 방식은 하이브리드 클라우드 솔루션을 구축하는 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="f5607-116">Azure Virtual Network 게이트웨이에 대한 다중 사이트 연결을 만드는 작업은 다른 사이트 간 연결을 만드는 작업과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="f5607-117">실제로, 게이트웨이가 동적(경로 기반)이라면 기존 Azure VPN 게이트웨이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="f5607-118">이미 정적 게이트웨이가 가상 네트워크에 연결된 경우에는 가상 네트워크를 다시 빌드하지 않고도 게이트웨이 유형을 동적으로 변경하여 다중 사이트를 수용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="f5607-119">라우팅 유형을 변경하기 전에 온-프레미스 VPN 게이트웨이가 경로 기반 VPN 구성을 지원하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="f5607-120">![다중 사이트 다이어그램](./media/vpn-gateway-multi-site/multisite.png "다중 사이트")</span><span class="sxs-lookup"><span data-stu-id="f5607-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="f5607-121">고려할 항목</span><span class="sxs-lookup"><span data-stu-id="f5607-121">Points to consider</span></span>

<span data-ttu-id="f5607-122">**이 가상 네트워크 변경을 위해 포털을 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="f5607-122">**You won't be able to use the portal to make changes to this virtual network.**</span></span> <span data-ttu-id="f5607-123">포털을 사용하는 대신 네트워크 구성 파일을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-123">You need to make changes to the network configuration file instead of using the portal.</span></span> <span data-ttu-id="f5607-124">포털에서 변경한 경우, 사용자의 다중 사이트 참조 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="f5607-125">따라서 다중 사이트 절차를 완료할 때까지는 네트워크 구성 파일을 사용하는 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="f5607-126">그러나 네트워크 구성을 여러 사용자가 사용하는 경우에는 이 제한에 대해 모든 사람이 알 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="f5607-127">포털을 아예 사용할 수 없다는 뜻은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-127">This doesn't mean that you can't use the portal at all.</span></span> <span data-ttu-id="f5607-128">이 특정 가상 네트워크에 대한 구성 변경을 제외한 모든 작업에 관리 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f5607-129">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f5607-129">Before you begin</span></span>

<span data-ttu-id="f5607-130">구성을 시작하기 전에 다음이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-130">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="f5607-131">각 온-프레미스 위치에서 호환되는 VPN 하드웨어.</span><span class="sxs-lookup"><span data-stu-id="f5607-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="f5607-132">사용하려는 장치가 호환 가능한 것인지 확인하려면 [가상 네트워크 연결을 위한 VPN 장치 정보](vpn-gateway-about-vpn-devices.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5607-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="f5607-133">각 VPN 장치에 대한 외부 연결 공용 IPv4 IP 주소.</span><span class="sxs-lookup"><span data-stu-id="f5607-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="f5607-134">IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-134">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="f5607-135">이는 필수 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-135">This is requirement.</span></span>
* <span data-ttu-id="f5607-136">최신 버전의 Azure PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f5607-137">SM(서비스 관리)와 Resource Manager 버전을 모두 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span></span> <span data-ttu-id="f5607-138">자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5607-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="f5607-139">VPN 하드웨어 구성에 능숙한 사용자.</span><span class="sxs-lookup"><span data-stu-id="f5607-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="f5607-140">사용자가 VPN 장치 구성 방법에 대해 매우 잘 알고 있거나 이와 관련된 지식이 있는 사람과 작업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="f5607-141">가상 네트워크에 사용할 IP 주소 범위(아직 만들지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="f5607-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="f5607-142">연결할 각 로컬 네트워크 사이트에 대한 IP 주소 범위.</span><span class="sxs-lookup"><span data-stu-id="f5607-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="f5607-143">연결하려는 각 로컬 네트워크 사이트의 IP 주소 범위가 겹치지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="f5607-144">그렇지 않은 경우 포털 또는 REST API는 업로드 중인 구성을 거절합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span></span><br><span data-ttu-id="f5607-145">예를 들어 두 로컬 네트워크 사이트에 IP 주소 범위 10.2.3.0/24가 모두 포함되어 있고 대상 주소가 10.2.3.3인 패키지가 있는 경우, 주소 범위가 겹치기 때문에 Azure는 어떤 사이트에 패키지를 전송할지 알지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="f5607-146">라우팅 문제를 방지하기 위해 Azure에서는 범위가 겹치는 구성 파일의 업로드를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="f5607-147">1. 사이트 간 VPN 만들기</span><span class="sxs-lookup"><span data-stu-id="f5607-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="f5607-148">동적 라우팅 게이트웨이를 사용한 사이트 간 VPN이 이미 있으면 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="f5607-149">[가상 네트워크 구성 설정 내보내기](#export)로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-149">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="f5607-150">아직 만들지 않은 경우는 아래 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-150">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="f5607-151">사이트 간 가상 네트워크가 이미 있지만 정적(정책 기반) 라우팅 게이트웨이가 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="f5607-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="f5607-152">게이트웨이 유형을 동적 라우팅으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-152">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="f5607-153">다중 사이트 VPN에는 동적(경로 기반이라고도 함) 라우팅 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="f5607-154">게이트웨이 유형을 변경하려면 먼저 기존 게이트웨이를 삭제한 다음 새로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span> <span data-ttu-id="f5607-155">자세한 내용은 [게이트웨이의 VPN 라우팅 유형을 변경하는 방법](vpn-gateway-configure-vpn-gateway-mp.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5607-155">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="f5607-156">새 게이트웨이를 구성하고 VPN 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="f5607-157">자세한 내용은 [Azure 클래식 포털에서 VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5607-157">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="f5607-158">먼저, 게이트웨이 유형을 동적 라우팅으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-158">First, change your gateway type to dynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="f5607-159">사이트 간 가상 네트워크 사이트가 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="f5607-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="f5607-160">[Azure 클래식 포털에서 사이트 간 VPN 연결을 사용하여 가상 네트워크 만들기](vpn-gateway-site-to-site-create.md)를 참조하여 사이트 간 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="f5607-161">[VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)을 참조하여 동적 라우팅 게이트웨이를 구성하십시오.</span><span class="sxs-lookup"><span data-stu-id="f5607-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="f5607-162">사용 중인 게이트웨이 유형에 맞는 **동적 라우팅** 을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-162">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="f5607-163"><a name="export"></a>2. 네트워크 구성 파일을 내보내기</span><span class="sxs-lookup"><span data-stu-id="f5607-163"><a name="export"></a>2. Export the network configuration file</span></span>
<span data-ttu-id="f5607-164">다음 명령을 실행하여 Azure 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-164">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="f5607-165">필요한 경우 다른 위치로 내보낼 파일의 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-165">You can change the location of the file to export to a different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="f5607-166">3. 네트워크 구성 파일 열기</span><span class="sxs-lookup"><span data-stu-id="f5607-166">3. Open the network configuration file</span></span>
<span data-ttu-id="f5607-167">마지막 단계에서 다운로드한 네트워크 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-167">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="f5607-168">원하는 xml 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-168">Use any xml editor that you like.</span></span> <span data-ttu-id="f5607-169">파일은 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-169">The file should look similar to the following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="f5607-170">4. 여러 사이트 참조 추가</span><span class="sxs-lookup"><span data-stu-id="f5607-170">4. Add multiple site references</span></span>
<span data-ttu-id="f5607-171">사이트 참조 정보를 추가 또는 제거하면 ConnectionsToLocalNetwork/LocalNetworkSiteRef의 구성이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-171">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="f5607-172">새 로컬 사이트 참조를 추가하면 Azure에서 새 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-172">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="f5607-173">아래 예제에서 네트워크 구성은 단일 사이트 연결용입니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-173">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="f5607-174">모두 변경했으면 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-174">Save the file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="f5607-175">추가 사이트 참조를 추가하려면(다중 사이트 구성 만들기) 아래 예제와 같이 추가 "LocalNetworkSiteRef" 줄을 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-175">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="f5607-176">5. 네트워크 구성 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="f5607-176">5. Import the network configuration file</span></span>
<span data-ttu-id="f5607-177">네트워크 구성 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-177">Import the network configuration file.</span></span> <span data-ttu-id="f5607-178">변경 내용과 함께 이 파일을 가져오면 새 터널이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-178">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="f5607-179">터널은 이전에 만든 동적 게이트웨이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-179">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="f5607-180">클래식 포털 또는 PowerShell을 사용하여 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-180">You can either use the classic portal, or PowerShell to import the file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="f5607-181">6. 키 다운로드</span><span class="sxs-lookup"><span data-stu-id="f5607-181">6. Download keys</span></span>
<span data-ttu-id="f5607-182">새 터널을 추가한 후 PowerShell cmdlet 'Get-AzureVNetGatewayKey'를 사용하여 각 터널의 IPsec/IKE 사전 공유 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-182">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="f5607-183">예:</span><span class="sxs-lookup"><span data-stu-id="f5607-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="f5607-184">원하는 경우 *가상 네트워크 게이트웨이 공유 키 가져오기* REST API를 사용하여 사전 공유 키를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-184">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="f5607-185">7. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="f5607-185">7. Verify your connections</span></span>
<span data-ttu-id="f5607-186">다중 사이트 터널 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-186">Check the multi-site tunnel status.</span></span> <span data-ttu-id="f5607-187">각 터널에 대한 키를 다운로드한 후 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-187">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="f5607-188">아래 예제에 나온 것처럼 'Get-AzureVnetConnection'을 사용하여 가상 네트워크 터널 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-188">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="f5607-189">VNet1이 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-189">VNet1 is the name of the VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="f5607-190">예제는 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5607-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="f5607-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5607-191">Next steps</span></span>

<span data-ttu-id="f5607-192">VPN 게이트웨이에 대한 자세한 내용은 [VPN 게이트웨이 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5607-192">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
