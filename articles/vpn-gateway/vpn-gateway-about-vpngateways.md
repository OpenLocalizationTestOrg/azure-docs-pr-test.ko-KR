---
title: "VPN Gateway 개요: Azure 가상 네트워크에 대한 크로스-프레미스 VPN 연결 만들기 | Microsoft Docs"
description: "이 VPN Gateway 개요에서는 VPN 연결을 사용하여 인터넷을 통해 Azure 가상 네트워크에 연결하는 방법에 대해 설명합니다. 기본 연결 구성의 다이어그램이 포함됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: ecfe6dab6e4deaa75d073badcb88d536396fe678
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="about-vpn-gateway"></a><span data-ttu-id="cdc38-104">VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="cdc38-104">About VPN Gateway</span></span>

<span data-ttu-id="cdc38-105">VPN Gateway는 공용 연결을 통해 온-프레미스 위치에 암호화된 트래픽을 보내는 가상 네트워크 게이트웨이의 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-105">A VPN gateway is a type of virtual network gateway that sends encrypted traffic across a public connection to an on-premises location.</span></span> <span data-ttu-id="cdc38-106">또한 VPN Gateway를 사용하여 Microsoft 네트워크를 통해 Azure 가상 네트워크 간에 암호화된 트래픽을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-106">You can also use VPN gateways to send encrypted traffic between Azure virtual networks over the Microsoft network.</span></span> <span data-ttu-id="cdc38-107">Azure 가상 네트워크와 온-프레미스 사이트 간에 암호화된 네트워크 트래픽을 보내려면 가상 네트워크에 대한 가상 VPN Gateway를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-107">To send encrypted network traffic between your Azure virtual network and your on-premises site, you must create a VPN gateway for your virtual network.</span></span>

<span data-ttu-id="cdc38-108">각 가상 네트워크에는 하나의 VPN Gateway만이 있을 수 있지만 동일한 VPN Gateway에 여러 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-108">Each virtual network can have only one VPN gateway, however, you can create multiple connections to the same VPN gateway.</span></span> <span data-ttu-id="cdc38-109">한 가지 예로 다중 사이트 연결 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-109">An example of this is a Multi-Site connection configuration.</span></span> <span data-ttu-id="cdc38-110">동일한 VPN Gateway에 대한 여러 연결을 만들면 지점 및 사이트 간 VPN을 비롯한 모든 VPN 터널이 해당 게이트웨이의 사용 가능한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-110">When you create multiple connections to the same VPN gateway, all VPN tunnels, including Point-to-Site VPNs, share the bandwidth that is available for the gateway.</span></span>

### <span data-ttu-id="cdc38-111"><a name="whatis"></a>가상 네트워크 게이트웨이란?</span><span class="sxs-lookup"><span data-stu-id="cdc38-111"><a name="whatis"></a>What is a virtual network gateway?</span></span>

<span data-ttu-id="cdc38-112">가상 네트워크 게이트웨이는 GatewaySubnet이라는 특정 서브넷에 배포되는 두 개 이상의 가상 컴퓨터로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-112">A virtual network gateway is composed of two or more virtual machines that are deployed to a specific subnet called the GatewaySubnet.</span></span> <span data-ttu-id="cdc38-113">GatewaySubnet에 있는 VM은 가상 네트워크 게이트웨이를 만들 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-113">The VMs that are located in the GatewaySubnet are created when you create the virtual network gateway.</span></span> <span data-ttu-id="cdc38-114">VM을 구성한 가상 네트워크 게이트웨이는 라우팅 테이블 및 게이트웨이에 특정한 게이트웨이 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-114">Virtual network gateway VMs are configured to contain routing tables and gateway services specific to the gateway.</span></span> <span data-ttu-id="cdc38-115">가상 네트워크 게이트웨이의 일부인 VM을 직접 구성할 수 없고 GatewaySubnet에 추가 리소스를 배포하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-115">You can't directly configure the VMs that are part of the virtual network gateway and you should never deploy additional resources to the GatewaySubnet.</span></span>

<span data-ttu-id="cdc38-116">'Vpn' 게이트웨이 형식을 사용하여 가상 네트워크 게이트웨이를 만들 때 트래픽을 암호화하는 특정 종류의 가상 네트워크 게이트웨이인 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-116">When you create a virtual network gateway using the gateway type 'Vpn', it creates a specific type of virtual network gateway that encrypts traffic; a VPN gateway.</span></span> <span data-ttu-id="cdc38-117">VPN Gateway를 만드는 데 최대 45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-117">A VPN gateway can take up to 45 minutes to create.</span></span> <span data-ttu-id="cdc38-118">이는 VPN Gateway에 대한 VM을 GatewaySubnet에 배포하고 사용자가 지정한 설정으로 구성하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-118">This is because the VMs for the VPN gateway are being deployed to the GatewaySubnet and configured with the settings that you specified.</span></span> <span data-ttu-id="cdc38-119">선택한 Gateway SKU가 얼마나 강력한 VM인지 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-119">The Gateway SKU that you select determines how powerful the VMs are.</span></span>

## <span data-ttu-id="cdc38-120"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="cdc38-120"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <span data-ttu-id="cdc38-121"><a name="configuring"></a>VPN Gateway 구성</span><span class="sxs-lookup"><span data-stu-id="cdc38-121"><a name="configuring"></a>Configuring a VPN Gateway</span></span>

<span data-ttu-id="cdc38-122">VPN Gateway 연결은 특정 설정으로 구성된 여러 리소스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-122">A VPN gateway connection relies on multiple resources that are configured with specific settings.</span></span> <span data-ttu-id="cdc38-123">대부분의 리소스를 특정 순서로 구성해야 하지만 어떤 경우에는 개별적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-123">Most of the resources can be configured separately, although they must be configured in a certain order in some cases.</span></span>

### <span data-ttu-id="cdc38-124"><a name="settings"></a>설정</span><span class="sxs-lookup"><span data-stu-id="cdc38-124"><a name="settings"></a>Settings</span></span>

<span data-ttu-id="cdc38-125">각 리소스에 선택하는 설정은 성공적인 연결을 만드는 데 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-125">The settings that you chose for each resource are critical to creating a successful connection.</span></span> <span data-ttu-id="cdc38-126">VPN Gateway의 개별 리소스 및 설정에 대한 정보는 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-126">For information about individual resources and settings for VPN Gateway, see [About VPN Gateway settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span> <span data-ttu-id="cdc38-127">이 문서에는 게이트웨이 유형, VPN 유형, 연결 유형, 게이트웨이 서브넷, 로컬 네트워크 게이트웨이 및 고려해야 할 다른 다양한 리소스 설정을 이해하는 데 유용한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-127">The article contains information to help you understand gateway types, VPN types, connection types, gateway subnets, local network gateways, and various other resource settings that you may want to consider.</span></span>

### <span data-ttu-id="cdc38-128"><a name="tools"></a>배포 도구</span><span class="sxs-lookup"><span data-stu-id="cdc38-128"><a name="tools"></a>Deployment tools</span></span>

<span data-ttu-id="cdc38-129">Azure Portal과 같은 하나의 구성 도구를 사용하여 리소스를 시작하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-129">You can start out creating and configuring resources using one configuration tool, such as the Azure portal.</span></span> <span data-ttu-id="cdc38-130">나중에 PowerShell과 같은 다른 도구로 전환하도록 결정하여 추가 리소스를 구성하거나 해당하는 경우 기존 리소스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-130">You can later decide to switch to another tool, such as PowerShell, to configure additional resources, or modify existing resources when applicable.</span></span> <span data-ttu-id="cdc38-131">현재, Azure Portal에서 모든 리소스 및 리소스 설정을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-131">Currently, you can't configure every resource and resource setting in the Azure portal.</span></span> <span data-ttu-id="cdc38-132">각 연결 토폴로지에 대한 문서의 지침은 특정 구성 도구가 필요한지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-132">The instructions in the articles for each connection topology specify when a specific configuration tool is needed.</span></span> 

### <span data-ttu-id="cdc38-133"><a name="models"></a>배포 모델</span><span class="sxs-lookup"><span data-stu-id="cdc38-133"><a name="models"></a>Deployment model</span></span>

<span data-ttu-id="cdc38-134">VPN Gateway를 구성할 때 수행할 단계는 가상 네트워크를 만드는 데 사용되는 배포 모델에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-134">When you configure a VPN gateway, the steps you take depend on the deployment model that you used to create your virtual network.</span></span> <span data-ttu-id="cdc38-135">예를 들어 클래식 배포 모델을 사용하여 VNet을 만든 경우 클래식 배포 모델에 대한 가이드 및 지침을 사용하여 VPN 게이트웨이 설정을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-135">For example, if you created your VNet using the classic deployment model, you use the guidelines and instructions for the classic deployment model to create and configure your VPN gateway settings.</span></span> <span data-ttu-id="cdc38-136">배포 모델에 대한 자세한 내용은 [Resource Manager 배포 및 클래식 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-136">For more information about deployment models, see [Understanding Resource Manager and classic deployment models](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <span data-ttu-id="cdc38-137"><a name="diagrams"></a>연결 토폴로지 다이어그램</span><span class="sxs-lookup"><span data-stu-id="cdc38-137"><a name="diagrams"></a>Connection topology diagrams</span></span>

<span data-ttu-id="cdc38-138">VPN Gateway 연결에 사용할 수 있는 다양한 구성이 있다는 사실을 꼭 기억하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-138">It's important to know that there are different configurations available for VPN gateway connections.</span></span> <span data-ttu-id="cdc38-139">그 중에서 필요에 맞는 최상의 구성을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-139">You need to determine which configuration best fits your needs.</span></span> <span data-ttu-id="cdc38-140">아래 섹션에서는 다음과 같은 VPN Gateway 연결에 대한 정보 및 토폴로지 다이어그램을 볼 수 있습니다. 다음 섹션에는 다음에 나열된 테이블이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-140">In the sections below, you can view information and topology diagrams about the following VPN gateway connections: The following sections contain tables which list:</span></span>

* <span data-ttu-id="cdc38-141">사용 가능한 배포 모델</span><span class="sxs-lookup"><span data-stu-id="cdc38-141">Available deployment model</span></span>
* <span data-ttu-id="cdc38-142">사용 가능한 구성 도구</span><span class="sxs-lookup"><span data-stu-id="cdc38-142">Available configuration tools</span></span>
* <span data-ttu-id="cdc38-143">사용할 수 있는 경우 문서로 직접 이동하는 링크</span><span class="sxs-lookup"><span data-stu-id="cdc38-143">Links that take you directly to an article, if available</span></span>

<span data-ttu-id="cdc38-144">다이어그램 및 설명을 사용하여 요구 사항에 맞게 연결 토폴로지를 선택하도록 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-144">Use the diagrams and descriptions to help select the connection topology to match your requirements.</span></span> <span data-ttu-id="cdc38-145">다이어그램은 기본 초기 토폴로지를 보여 주지만 다이어그램을 지침으로 사용하여 더 복잡한 구성을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-145">The diagrams show the main baseline topologies, but it's possible to build more complex configurations using the diagrams as a guideline.</span></span>

## <span data-ttu-id="cdc38-146"><a name="s2smulti"></a>사이트 간 및 다중 사이트(IPsec/IKE VPN 터널)</span><span class="sxs-lookup"><span data-stu-id="cdc38-146"><a name="s2smulti"></a>Site-to-Site and Multi-Site (IPsec/IKE VPN tunnel)</span></span>

### <span data-ttu-id="cdc38-147"><a name="S2S"></a>사이트 간</span><span class="sxs-lookup"><span data-stu-id="cdc38-147"><a name="S2S"></a>Site-to-Site</span></span>

<span data-ttu-id="cdc38-148">S2S(사이트 간) VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-148">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="cdc38-149">S2S 연결은 공용 IP 주소가 할당되어 있고 NAT 다음에 위치하지 않는 온-프레미스에 있는 VPN 장치를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-149">A S2S connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT.</span></span> <span data-ttu-id="cdc38-150">S2S 연결은 프레미스 간 및 하이브리드 구성에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-150">S2S connections can be used for cross-premises and hybrid configurations.</span></span>   

![Azure VPN Gateway 사이트 간 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <span data-ttu-id="cdc38-152"><a name="Multi"></a>다중 사이트</span><span class="sxs-lookup"><span data-stu-id="cdc38-152"><a name="Multi"></a>Multi-Site</span></span>

<span data-ttu-id="cdc38-153">사이트 간 연결에서 변형된 연결 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-153">This type of connection is a variation of the Site-to-Site connection.</span></span> <span data-ttu-id="cdc38-154">가상 네트워크 게이트웨이에서 일반적으로 여러 온-프레미스 사이트에 연결하는 둘 이상의 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-154">You create more than one VPN connection from your virtual network gateway, typically connecting to multiple on-premises sites.</span></span> <span data-ttu-id="cdc38-155">여러 연결을 사용하는 경우 경로 기반 VPN 유형(클래식 VNet을 사용하는 경우 동적 게이트웨이)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-155">When working with multiple connections, you must use a RouteBased VPN type (known as a dynamic gateway when working with classic VNets).</span></span> <span data-ttu-id="cdc38-156">각 가상 네트워크가 하나의 VPN Gateway만 사용할 수 있으므로 게이트웨이를 통한 모든 연결은 사용 가능한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-156">Because each virtual network can only have one VPN gateway, all connections through the gateway share the available bandwidth.</span></span> <span data-ttu-id="cdc38-157">이는 "다중 사이트" 연결이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-157">This is often called a "multi-site" connection.</span></span>

![Azure VPN Gateway 다중 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a><span data-ttu-id="cdc38-159">사이트 간 및 다중 사이트의 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="cdc38-159">Deployment models and methods for Site-to-Site and Multi-Site</span></span>

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <span data-ttu-id="cdc38-160"><a name="P2S"></a>지점 및 사이트 간(SSTP를 통한 VPN)</span><span class="sxs-lookup"><span data-stu-id="cdc38-160"><a name="P2S"></a>Point-to-Site (VPN over SSTP)</span></span>

<span data-ttu-id="cdc38-161">지점 및 사이트 간(P2S) VPN Gateway를 통해 개별 클라이언트 컴퓨터에서 가상 네트워크에 안전한 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-161">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="cdc38-162">지점 및 사이트 간 VPN 연결은 집 또는 회의에서 원격 통신하는 경우와 같이 원격 위치에서 VNet에 연결하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-162">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="cdc38-163">VNet에 연결해야 하는 몇 가지 클라이언트만 있는 경우에 사이트 간 VPN 대신 P2S VPN을 사용하는 것도 유용한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-163">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span> 

<span data-ttu-id="cdc38-164">S2S 연결과 달리 P2S 연결은 온-프레미스 공용 IP 주소 또는 VPN 장치가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-164">Unlike S2S connections, P2S connections do not require an on-premises public-facing IP address or a VPN device.</span></span> <span data-ttu-id="cdc38-165">P2S 연결과 S2S 연결에 대한 구성 요구 사항이 모두 충족될 경우 동일한 VPN Gateway를 통해 두 연결을 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-165">P2S connections can be used with S2S connections through the same VPN gateway, as long as all the configuration requirements for both connections are compatible.</span></span>

<span data-ttu-id="cdc38-166">P2S는 SSL 기반 VPN 프로토콜인 SSTP(Secure Socket Tunneling Protocol)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-166">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="cdc38-167">클라이언트 컴퓨터에서 시작하여 P2S VPN 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-167">A P2S VPN connection is established by starting it from the client computer.</span></span>

![Azure VPN Gateway 지점 및 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a><span data-ttu-id="cdc38-169">지점 및 사이트에 대한 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="cdc38-169">Deployment models and methods for Point-to-Site</span></span>

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <span data-ttu-id="cdc38-170"><a name="V2V"></a>VNet 간 연결(IPsec/IKE VPN 터널)</span><span class="sxs-lookup"><span data-stu-id="cdc38-170"><a name="V2V"></a>VNet-to-VNet connections (IPsec/IKE VPN tunnel)</span></span>

<span data-ttu-id="cdc38-171">가상 네트워크를 다른 가상 네트워크에 연결(VNet-VNet)하는 것은 VNet을 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-171">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="cdc38-172">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-172">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="cdc38-173">VNet 간 통신을 다중 사이트 연결 구성과 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-173">You can even combine VNet-to-VNet communication with multi-site connection configurations.</span></span> <span data-ttu-id="cdc38-174">이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-174">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

<span data-ttu-id="cdc38-175">연결할 VNet의 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-175">The VNets you connect can be:</span></span>

* <span data-ttu-id="cdc38-176">동일하거나 다른 지역에 위치</span><span class="sxs-lookup"><span data-stu-id="cdc38-176">in the same or different regions</span></span>
* <span data-ttu-id="cdc38-177">동일하거나 다른 구독에 위치</span><span class="sxs-lookup"><span data-stu-id="cdc38-177">in the same or different subscriptions</span></span> 
* <span data-ttu-id="cdc38-178">동일하거나 다른 배포 모델</span><span class="sxs-lookup"><span data-stu-id="cdc38-178">in the same or different deployment models</span></span>

![Azure VPN Gateway VNet 간 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a><span data-ttu-id="cdc38-180">배포 모델 간의 연결</span><span class="sxs-lookup"><span data-stu-id="cdc38-180">Connections between deployment models</span></span>

<span data-ttu-id="cdc38-181">Azure에는 현재 클래식 및 Resource Manager 등 두 개의 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-181">Azure currently has two deployment models: classic and Resource Manager.</span></span> <span data-ttu-id="cdc38-182">일정 기간 동안 Azure를 사용한 경우 Azure VM 및 인스턴스 역할이 클래식 VNet에서 실행되고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-182">If you have been using Azure for some time, you probably have Azure VMs and instance roles running in a classic VNet.</span></span> <span data-ttu-id="cdc38-183">이후의 VM 및 역할 인스턴스는 Resource Manager에서 만들 VNet에서 실행되고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-183">Your newer VMs and role instances may be running in a VNet created in Resource Manager.</span></span> <span data-ttu-id="cdc38-184">VNet 간의 연결을 만들어 어떤 VNet의 리소스가 다른 리소스와 서로 직접 통신하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-184">You can create a connection between the VNets to allow the resources in one VNet to communicate directly with resources in another.</span></span>

### <a name="vnet-peering"></a><span data-ttu-id="cdc38-185">VNet 피어링</span><span class="sxs-lookup"><span data-stu-id="cdc38-185">VNet peering</span></span>

<span data-ttu-id="cdc38-186">가상 네트워크가 특정 요구 사항을 충족하면 VNet 피어링을 사용하여 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-186">You may be able to use VNet peering to create your connection, as long as your virtual network meets certain requirements.</span></span> <span data-ttu-id="cdc38-187">VNet 피어링은 가상 네트워크 게이트웨이를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-187">VNet peering does not use a virtual network gateway.</span></span> <span data-ttu-id="cdc38-188">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-188">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a><span data-ttu-id="cdc38-189">VNet 간 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="cdc38-189">Deployment models and methods for VNet-to-VNet</span></span>

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <span data-ttu-id="cdc38-190"><a name="ExpressRoute"></a>ExpressRoute(전용 개인 연결)</span><span class="sxs-lookup"><span data-stu-id="cdc38-190"><a name="ExpressRoute"></a>ExpressRoute (dedicated private connection)</span></span>

<span data-ttu-id="cdc38-191">Microsoft Azure ExpressRoute를 사용하면 연결 공급자에서 쉽게 처리된 전용 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-191">Microsoft Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="cdc38-192">ExpressRoute를 사용하면 Microsoft Azure, Office 365, CRM Online과 같은 Microsoft 클라우드 서비스에 대한 연결을 설정하거나,</span><span class="sxs-lookup"><span data-stu-id="cdc38-192">With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="cdc38-193">공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-193">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span>

<span data-ttu-id="cdc38-194">ExpressRoute 연결은 공용 인터넷을 통해 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-194">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="cdc38-195">이 기능을 사용하면 ExpressRoute 연결은 인터넷을 통한 일반 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧고 보안성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-195">This allows ExpressRoute connections to offer more reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet.</span></span>

<span data-ttu-id="cdc38-196">ExpressRoute 연결은 필수 구성의 일부분으로 가상 네트워크 게이트웨이를 사용하지만 VPN Gateway는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-196">An ExpressRoute connection does not use a VPN gateway, although it does use a virtual network gateway as part of its required configuration.</span></span> <span data-ttu-id="cdc38-197">ExpressRoute 연결에서 가상 네트워크 게이트웨이는 'Vpn'이 아닌 'ExpressRoute' 게이트웨이 유형으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-197">In an ExpressRoute connection, the virtual network gateway is configured with the gateway type 'ExpressRoute', rather than 'Vpn'.</span></span> <span data-ttu-id="cdc38-198">ExpressRoute에 대한 자세한 내용은 [ExpressRoute 기술 개요](../expressroute/expressroute-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-198">For more information about ExpressRoute, see the [ExpressRoute technical overview](../expressroute/expressroute-introduction.md).</span></span>

## <span data-ttu-id="cdc38-199"><a name="coexisting"></a>사이트 간 및 ExpressRoute 공존 연결</span><span class="sxs-lookup"><span data-stu-id="cdc38-199"><a name="coexisting"></a>Site-to-Site and ExpressRoute coexisting connections</span></span>

<span data-ttu-id="cdc38-200">ExpressRoute는 공용 인터넷을 사용하지 않고 WAN에서 Azure를 비롯한 Microsoft 서비스에 대한 직접 전용 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-200">ExpressRoute is a direct, dedicated connection from your WAN (not over the public Internet) to Microsoft Services, including Azure.</span></span> <span data-ttu-id="cdc38-201">사이트 간 VPN 트래픽은 공용 인터넷을 통해 암호화되어 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-201">Site-to-Site VPN traffic travels encrypted over the public Internet.</span></span> <span data-ttu-id="cdc38-202">동일한 가상 네트워크에 대한 사이트 간 VPN 및 Express 경로 연결을 구성할 수 있으면 여러 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-202">Being able to configure Site-to-Site VPN and ExpressRoute connections for the same virtual network has several advantages.</span></span>

<span data-ttu-id="cdc38-203">사이트 간 VPN을 ExpressRoute에 대한 보안 장애 조치(failover) 경로로 구성하거나 사이트 간 VPN을 사용하여 사용자 네트워크의 일부가 아니지만 ExpressRoute를 통해 연결된 사이트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-203">You can configure a Site-to-Site VPN as a secure failover path for ExpressRoute, or use Site-to-Site VPNs to connect to sites that are not part of your network, but that are connected through ExpressRoute.</span></span> <span data-ttu-id="cdc38-204">이 구성에는 동일한 가상 네트워크에 대한 두 개의 가상 네트워크 게이트웨이가 필요합니다. 하나는 'Vpn' 게이트웨이 유형을 사용하고 다른 하나는 'ExpressRoute' 게이트웨이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-204">Notice that this configuration requires two virtual network gateways for the same virtual network, one using the gateway type 'Vpn', and the other using the gateway type 'ExpressRoute'.</span></span>

![ExpressRoute 및 VPN Gateway 공존 연결 예제](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a><span data-ttu-id="cdc38-206">S2S 및 ExpressRoute에 대한 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="cdc38-206">Deployment models and methods for S2S and ExpressRoute</span></span>

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a><span data-ttu-id="cdc38-207">가격</span><span class="sxs-lookup"><span data-stu-id="cdc38-207">Pricing</span></span>

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

<span data-ttu-id="cdc38-208">VPN Gateway용 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-208">For more information about gateway SKUs for VPN Gateway, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <span data-ttu-id="cdc38-209"><a name="faq"></a>FAQ</span><span class="sxs-lookup"><span data-stu-id="cdc38-209"><a name="faq"></a>FAQ</span></span>

<span data-ttu-id="cdc38-210">VPN Gateway에 대한 자주 묻는 질문은 [VPN Gateway FAQ](vpn-gateway-vpn-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-210">For frequently asked questions about VPN gateway, see the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdc38-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdc38-211">Next steps</span></span>

- <span data-ttu-id="cdc38-212">VPN Gateway 구성을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-212">Plan your VPN gateway configuration.</span></span> <span data-ttu-id="cdc38-213">[VPN Gateway 계획 및 설계](vpn-gateway-plan-design.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-213">See [VPN Gateway Planning and Design](vpn-gateway-plan-design.md).</span></span>
- <span data-ttu-id="cdc38-214">자세한 내용은 [VPN Gateway FAQ](vpn-gateway-vpn-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-214">View the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) for additional information.</span></span>
- <span data-ttu-id="cdc38-215">[구독 및 서비스 한도](../azure-subscription-service-limits.md#networking-limits)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc38-215">View the [Subscription and service limits](../azure-subscription-service-limits.md#networking-limits).</span></span>
- <span data-ttu-id="cdc38-216">Azure의 다른 주요 [네트워킹 기능](../networking/networking-overview.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cdc38-216">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>