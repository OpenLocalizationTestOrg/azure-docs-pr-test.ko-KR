---
title: "크로스-프레미스 Azure 연결에 대한 VPN Gateway 설정 | Microsoft Docs"
description: "Azure Virtual Network 게이트웨이의 VPN Gateway 설정에 대해 알아봅니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="eb1f6-103">VPN Gateway 구성 설정 정보</span><span class="sxs-lookup"><span data-stu-id="eb1f6-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="eb1f6-104">VPN Gateway는 공용 연결을 통해 가상 네트워크와 온-프레미스 위치 간에 암호화된 트래픽을 전송하는 가상 네트워크 게이트웨이의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="eb1f6-105">또한 VPN Gateway를 사용하여 Azure 백본에 있는 가상 네트워크 간에 트래픽을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="eb1f6-106">VPN Gateway 연결은 각각이 구성 가능한 설정을 포함하는 여러 리소스의 구성에 따라 좌우됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="eb1f6-107">이 문서의 섹션에서는 Resource Manager 배포 모델에서 생성된 가상 네트워크의 VPN Gateway와 관련된 리소스 및 설정에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="eb1f6-108">[VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 문서에서 각 연결 솔루션에 대한 설명 및 토폴로지 다이어그램을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="eb1f6-109"><a name="gwtype"></a>게이트웨이 유형</span><span class="sxs-lookup"><span data-stu-id="eb1f6-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="eb1f6-110">가상 네트워크마다 각 유형의 가상 네트워크 게이트웨이를 하나씩만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="eb1f6-111">가상 네트워크 게이트웨이를 만들 때 게이트웨이 유형이 구성에 정확한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="eb1f6-112">-GatewayType에 사용 가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="eb1f6-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="eb1f6-113">Vpn</span></span>
* <span data-ttu-id="eb1f6-114">Express 경로</span><span class="sxs-lookup"><span data-stu-id="eb1f6-114">ExpressRoute</span></span>

<span data-ttu-id="eb1f6-115">VPN Gateway에는 `-GatewayType` *Vpn*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="eb1f6-116">예:</span><span class="sxs-lookup"><span data-stu-id="eb1f6-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="eb1f6-117"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="eb1f6-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="eb1f6-118">게이트웨이 SKU 구성</span><span class="sxs-lookup"><span data-stu-id="eb1f6-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="eb1f6-119">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="eb1f6-119">Azure portal</span></span>

<span data-ttu-id="eb1f6-120">Azure Portal을 사용하여 Resource Manager 가상 네트워크 게이트웨이를 만드는 경우 드롭다운을 사용하여 게이트웨이 SKU를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="eb1f6-121">표시되는 옵션은 선택한 게이트웨이 형식 및 선택한 VPN 형식에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="eb1f6-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb1f6-122">PowerShell</span></span>

<span data-ttu-id="eb1f6-123">다음 PowerShell 예제에서는 `-GatewaySku`를 VpnGw1으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="eb1f6-124"><a name="resize"></a>게이트웨이 SKU 변경(크기 조정)</span><span class="sxs-lookup"><span data-stu-id="eb1f6-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="eb1f6-125">게이트웨이 SKU를 좀 더 강력한 SKU로 업그레이드하려면 `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="eb1f6-126">또한 이 cmdlet을 사용하여 게이트웨이 SKU 크기를 다운그레이드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="eb1f6-127">다음 PowerShell 예제에서는 VpnGw2로 크기가 조정되는 게이트웨이 SKU를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="eb1f6-128"><a name="connectiontype"></a>연결 유형</span><span class="sxs-lookup"><span data-stu-id="eb1f6-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="eb1f6-129">Resource Manager 배포 모델에서 각 구성이 작동하려면 특정 가상 네트워크 게이트웨이 연결 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="eb1f6-130">`-ConnectionType` 에 대해 사용 가능한 Resource Manager PowerShell 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="eb1f6-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="eb1f6-131">IPsec</span></span>
* <span data-ttu-id="eb1f6-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="eb1f6-132">Vnet2Vnet</span></span>
* <span data-ttu-id="eb1f6-133">Express 경로</span><span class="sxs-lookup"><span data-stu-id="eb1f6-133">ExpressRoute</span></span>
* <span data-ttu-id="eb1f6-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="eb1f6-134">VPNClient</span></span>

<span data-ttu-id="eb1f6-135">다음 PowerShell 예제에서는 *IPsec*연결 유형이 필요한 S2S 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="eb1f6-136"><a name="vpntype"></a>VPN 유형</span><span class="sxs-lookup"><span data-stu-id="eb1f6-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="eb1f6-137">VPN Gateway 구성에 대한 가상 네트워크 게이트웨이 만들 때 VPN 유형을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="eb1f6-138">선택하는 VPN 유형은 만들려는 연결 토폴로지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="eb1f6-139">예를 들어 P2S 연결에는 RouteBased VPN 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="eb1f6-140">또한 VPN 유형은 사용하는 하드웨어에 따라서도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="eb1f6-141">S2S 구성에는 VPN 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="eb1f6-142">일부 VPN 장치는 특정 VPN 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="eb1f6-143">선택하는 VPN 유형은 만들려는 솔루션에 대한 연결 요구 사항을 모두 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="eb1f6-144">예를 들어 동일한 가상 네트워크에 대해 S2S VPN Gateway 연결 및 P2S VPN Gateway 연결을 만들려는 경우 P2S에는 RouteBased VPN 유형이 필요하기 때문에 VPN 유형 *RouteBased* 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="eb1f6-145">VPN 장치가 RouteBased VPN 연결을 지원하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="eb1f6-146">가상 네트워크 게이트웨이를 만든 후에는 VPN 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="eb1f6-147">가상 네트워크 게이트웨이를 삭제하고 새로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="eb1f6-148">두 가지 VPN 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="eb1f6-149">다음 PowerShell 예제에서는 `-VpnType` 를 *RouteBased*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="eb1f6-150">게이트웨이를 만들 때 -VpnType이 구성에 정확한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="eb1f6-151"><a name="requirements"></a>게이트웨이 요구 사항</span><span class="sxs-lookup"><span data-stu-id="eb1f6-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="eb1f6-152"><a name="gwsub"></a>게이트웨이 서브넷</span><span class="sxs-lookup"><span data-stu-id="eb1f6-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="eb1f6-153">VPN Gateway를 만들기 전에 게이트웨이 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="eb1f6-154">게이트웨이 서브넷은 가상 네트워크 게이트웨이 VM 및 서비스에서 사용하는 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="eb1f6-155">가상 네트워크 게이트웨이 만들 때 게이트웨이 VM은 게이트웨이 서브넷에 배포되고 필수 VPN Gateway 설정으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="eb1f6-156">게이트웨이 서브넷에 다른 항목(예: 추가 VM)을 배포하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="eb1f6-157">게이트웨이 서브넷이 제대로 작동하려면 이름을 'GatewaySubnet'으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="eb1f6-158">게이트웨이 서브넷 이름을 'GatewaySubnet'으로 지정하면 Azure에서 해당 서브넷이 가상 네트워크 게이트웨이 VM 및 서비스를 배포할 서브넷임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="eb1f6-159">게이트웨이 서브넷을 만드는 경우 서브넷이 포함하는 IP 주소의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="eb1f6-160">게이트웨이 서브넷의 IP 주소는 게이트웨이 VM 및 게이트웨이 서비스에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="eb1f6-161">일부 구성에는 다른 구성보다 더 많은 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="eb1f6-162">만들려는 구성에 대한 지침을 검토하고 가지고 있는 만들려는 게이트웨이 서브넷이 해당 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="eb1f6-163">또한 이후 추가 구성이 추가될 가능성에 대비하여 게이트웨이 서브넷에 IP 주소가 충분히 포함되어 있는지 확인하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="eb1f6-164">게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 게이트웨이 서브넷을 /28 이상으로 만드는 것이 좋습니다(/28, /27, /26 등).</span><span class="sxs-lookup"><span data-stu-id="eb1f6-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="eb1f6-165">이런 방식으로 나중에 기능을 추가할 경우 게이트웨이를 중지하거나 서브넷을 삭제하고 다시 만들어서 추가 IP 주소를 허용하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="eb1f6-166">다음 Resource Manager PowerShell 예제에서는 이름이 GatewaySubnet인 게이트웨이 서브넷을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="eb1f6-167">CIDR 표기법이 /27을 지정하는 것을 확인할 수 있으며 이는 이번에 존재하는 대부분의 구성에 대한 충분한 IP 주소를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="eb1f6-168"><a name="lng"></a>로컬 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="eb1f6-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="eb1f6-169">VPN Gateway 구성을 만들 때 로컬 네트워크 게이트웨이는 종종 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="eb1f6-170">클래식 배포 모델에서 로컬 네트워크 게이트웨이는 로컬 사이트라고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="eb1f6-171">로컬 네트워크 게이트웨이에 이름인 온-프레미스 VPN 장치의 공용 IP 주소를 지정하고 온-프레미스 위치에 있는 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="eb1f6-172">Azure는 네트워크 트래픽에 대상 주소 접두사를 보고 로컬 네트워크 게이트웨이에 대해 지정한 구성을 참조하며 그에 따라 패킷을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="eb1f6-173">VPN Gateway 연결을 사용하는 VNet-VNet 구성에 대해서도 로컬 네트워크 게이트웨이를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="eb1f6-174">다음 PowerShell 예제에서는 새 로컬 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="eb1f6-175">로컬 네트워크 게이트웨이 설정을 수정해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="eb1f6-176">예를 들어 주소 범위를 추가 또는 수정할 경우 또는 VPN 장치의 IP 주소가 변경될 때가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="eb1f6-177">클래식 VNet의 경우 로컬 네트워크 페이지의 클래식 포털에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="eb1f6-178">Resource Manager의 경우 [PowerShell을 사용하여 로컬 네트워크 게이트웨이 설정 수정](vpn-gateway-modify-local-network-gateway.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="eb1f6-179"><a name="resources"></a>REST API 및 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="eb1f6-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="eb1f6-180">VPN Gateway를 구성하기 위해 REST API, PowerShell cmdlet 또는 Azure CLI를 사용할 경우 추가 기술 리소스 및 특정 구문 요구 사항에 대해서는 다음 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="eb1f6-181">**클래식**</span><span class="sxs-lookup"><span data-stu-id="eb1f6-181">**Classic**</span></span> | <span data-ttu-id="eb1f6-182">**리소스 관리자**</span><span class="sxs-lookup"><span data-stu-id="eb1f6-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="eb1f6-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb1f6-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="eb1f6-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb1f6-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="eb1f6-185">REST API</span><span class="sxs-lookup"><span data-stu-id="eb1f6-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="eb1f6-186">REST API</span><span class="sxs-lookup"><span data-stu-id="eb1f6-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="eb1f6-187">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="eb1f6-187">Not supported</span></span> | [<span data-ttu-id="eb1f6-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb1f6-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="eb1f6-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb1f6-189">Next steps</span></span>

<span data-ttu-id="eb1f6-190">사용 가능한 연결 구성에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb1f6-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>