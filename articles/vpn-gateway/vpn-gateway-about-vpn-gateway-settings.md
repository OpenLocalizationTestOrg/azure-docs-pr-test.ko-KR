---
title: "크로스-프레미스 Azure 연결에 대 한 게이트웨이 설정을 aaaVPN | Microsoft Docs"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="3976e-103">VPN Gateway 구성 설정 정보</span><span class="sxs-lookup"><span data-stu-id="3976e-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="3976e-104">VPN Gateway는 공용 연결을 통해 가상 네트워크와 온-프레미스 위치 간에 암호화된 트래픽을 전송하는 가상 네트워크 게이트웨이의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="3976e-105">또한 Azure backbone hello에 걸쳐 가상 네트워크 간의 VPN 게이트웨이 toosend 트래픽을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="3976e-106">VPN 게이트웨이 연결을 각각 포함 하는 구성 가능한 설정 여러 리소스의 hello 구성에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="3976e-107">이 문서의 섹션 hello hello 리소스 및 리소스 관리자 배포 모델에서 만든 가상 네트워크에 대 한 VPN 게이트웨이 tooa와 관련 된 설정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="3976e-108">Hello에 각 연결 솔루션에 대 한 설명 및 토폴로지 다이어그램을 찾을 수 있습니다 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="3976e-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="3976e-109"><a name="gwtype"></a>게이트웨이 유형</span><span class="sxs-lookup"><span data-stu-id="3976e-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="3976e-110">가상 네트워크마다 각 유형의 가상 네트워크 게이트웨이를 하나씩만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="3976e-111">가상 네트워크 게이트웨이 만들 때 hello 게이트웨이 유형 구성에 대 한 정확한 지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="3976e-112">hello-GatewayType에 대 한 사용 가능한 값은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="3976e-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="3976e-113">Vpn</span></span>
* <span data-ttu-id="3976e-114">Express 경로</span><span class="sxs-lookup"><span data-stu-id="3976e-114">ExpressRoute</span></span>

<span data-ttu-id="3976e-115">VPN 게이트웨이 필요 hello `-GatewayType` *Vpn*합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="3976e-116">예제:</span><span class="sxs-lookup"><span data-stu-id="3976e-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="3976e-117"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="3976e-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="3976e-118">Hello 게이트웨이 SKU 구성</span><span class="sxs-lookup"><span data-stu-id="3976e-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="3976e-119">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3976e-119">Azure portal</span></span>

<span data-ttu-id="3976e-120">Hello Azure 포털 toocreate 리소스 관리자 가상 네트워크 게이트웨이 사용 하는 경우에 hello 드롭다운을 사용 하 여 hello 게이트웨이 SKU를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="3976e-121">toohello 게이트웨이 유형 및 선택 하는 VPN 유형에 해당 하는 hello 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="3976e-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3976e-122">PowerShell</span></span>

<span data-ttu-id="3976e-123">hello 다음 PowerShell 예에서는 지정 hello `-GatewaySku` VpnGw1으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="3976e-124"><a name="resize"></a>게이트웨이 SKU 변경(크기 조정)</span><span class="sxs-lookup"><span data-stu-id="3976e-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="3976e-125">Tooupgrade 게이트웨이 SKU tooa를 원하는 경우 더 강력한 SKU hello를 사용할 수 있습니다 `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3976e-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="3976e-126">또한이 cmdlet을 사용 하 여 hello 게이트웨이 SKU 크기를 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="3976e-127">다음 PowerShell 예에서는 hello tooVpnGw2 크기가 조정 되는 게이트웨이 SKU를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="3976e-128"><a name="connectiontype"></a>연결 유형</span><span class="sxs-lookup"><span data-stu-id="3976e-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="3976e-129">Hello 리소스 관리자 배포 모델에서 각 구성은 특정 가상 네트워크 게이트웨이 연결 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="3976e-130">hello 사용 가능한 리소스 관리자 PowerShell에 대 한 값 `-ConnectionType` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="3976e-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="3976e-131">IPsec</span></span>
* <span data-ttu-id="3976e-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="3976e-132">Vnet2Vnet</span></span>
* <span data-ttu-id="3976e-133">Express 경로</span><span class="sxs-lookup"><span data-stu-id="3976e-133">ExpressRoute</span></span>
* <span data-ttu-id="3976e-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="3976e-134">VPNClient</span></span>

<span data-ttu-id="3976e-135">다음 PowerShell 예에서는 hello, hello 연결 형식이 필요로 하는 S2S 연결 만듭니다 *IPsec*합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="3976e-136"><a name="vpntype"></a>VPN 유형</span><span class="sxs-lookup"><span data-stu-id="3976e-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="3976e-137">VPN 게이트웨이 구성에 대 한 hello 가상 네트워크 게이트웨이 만들 때 VPN 유형을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="3976e-138">선택 하는 VPN 유형 hello에 있어서 hello 연결 토폴로지 toocreate 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="3976e-139">예를 들어 P2S 연결에는 RouteBased VPN 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="3976e-140">VPN 유형을 사용 하는 hello 하드웨어에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="3976e-141">S2S 구성에는 VPN 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="3976e-142">일부 VPN 장치는 특정 VPN 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="3976e-143">선택한 VPN 유형은 hello toocreate 원하는 hello 솔루션에 대 한 모든 hello 연결 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="3976e-144">예를 들어 toocreate S2S VPN 게이트웨이 연결 및 P2S VPN 게이트웨이 연결에 대 한 hello 동일한 가상 네트워크를 VPN 형식을 사용 *RouteBased* P2S VPN RouteBased 유형 필요 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="3976e-145">VPN 장치 RouteBased VPN 연결을 지원 하는지 tooverify는도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="3976e-146">가상 네트워크 게이트웨이 만든 후 hello VPN 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="3976e-147">가상 네트워크 게이트웨이 hello 및 새로 만들 toodelete를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="3976e-148">두 가지 VPN 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="3976e-149">hello 다음 PowerShell 예에서는 지정 hello `-VpnType` 으로 *RouteBased*합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="3976e-150">게이트웨이 만들 때 있어야 해당 hello-VpnType가 구성에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="3976e-151"><a name="requirements"></a>게이트웨이 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3976e-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="3976e-152"><a name="gwsub"></a>게이트웨이 서브넷</span><span class="sxs-lookup"><span data-stu-id="3976e-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="3976e-153">VPN Gateway를 만들기 전에 게이트웨이 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="3976e-154">hello 게이트웨이 서브넷에 hello IP 주소가 해당 hello 가상 네트워크 게이트웨이 Vm 및 서비스에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="3976e-155">가상 네트워크 게이트웨이 만들 때 게이트웨이 Vm은 배포 된 toohello 게이트웨이 서브넷 및 필요한 hello VPN 게이트웨이 설정으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="3976e-156">(예: 추가 Vm) 다른 무엇 toohello 게이트웨이 서브넷을 배포 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="3976e-157">hello 게이트웨이 서브넷 이름을 지정 해야 'GatewaySubnet' toowork 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="3976e-158">이 hello 서브넷 toodeploy hello 가상 네트워크 게이트웨이 Vm 및 서비스를 Azure 알고 'GatewaySubnet' 있습니다 hello 게이트웨이 서브넷에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="3976e-159">Hello 게이트웨이 서브넷을 만들 때 포함 하는 hello 수가 IP 주소 서브넷 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="3976e-160">hello 게이트웨이 서브넷의 IP 주소가 hello은 할당 된 toohello 게이트웨이 Vm 및 게이트웨이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="3976e-161">일부 구성에는 다른 구성보다 더 많은 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="3976e-162">Hello hello 구성 toocreate 원하고 toocreate 원하는 hello 게이트웨이 서브넷에는 이러한 요구 사항을 충족 하는지 확인 지침을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="3976e-163">또한 toomake 게이트웨이 서브넷에 충분 한 IP 주소 tooaccommodate 가능한 향후 추가 구성이 포함 되어 있는지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="3976e-164">게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 게이트웨이 서브넷을 /28 이상으로 만드는 것이 좋습니다(/28, /27, /26 등).</span><span class="sxs-lookup"><span data-stu-id="3976e-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="3976e-165">Hello 미래에 기능을 추가 하는 경우 이렇게 않습니다 tootear 게이트웨이 한 다음 삭제 있고 더 많은 IP 주소에 대 한 게이트웨이 서브넷 tooallow hello를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="3976e-166">hello 다음 리소스 관리자 PowerShell 예제 이라는 게이트웨이 서브넷.</span><span class="sxs-lookup"><span data-stu-id="3976e-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="3976e-167">Hello CIDR 표기법 지정 에/27 현재 존재 하는 대부분의 구성에 대 한 충분 한 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="3976e-168"><a name="lng"></a>로컬 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="3976e-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="3976e-169">VPN 게이트웨이 구성을 만들 때 hello 로컬 네트워크 게이트웨이 종종 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="3976e-170">Hello 클래식 배포 모델에 hello 로컬 네트워크 게이트웨이 로컬 사이트 참조 tooas 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="3976e-171">하면 hello 로컬 네트워크 게이트웨이 이름 지정, hello hello 온-프레미스 VPN 장치의 공용 IP 주소 하 고 hello 온-프레미스 위치에 있는 hello 주소 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="3976e-172">Azure는 네트워크 트래픽에 대 한 hello 대상 주소 접두사, 로컬 네트워크 게이트웨이 위해 지정한 hello 구성 참조 찾은 그에 따라 패킷을 라우팅할 합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="3976e-173">VPN Gateway 연결을 사용하는 VNet-VNet 구성에 대해서도 로컬 네트워크 게이트웨이를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="3976e-174">다음 PowerShell 예에서는 hello 새 로컬 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="3976e-175">Toomodify hello 로컬 네트워크 게이트웨이 설정이 필요한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="3976e-176">Hello VPN 장치의 hello IP 주소가 변경 된 경우 추가 또는 수정 hello 주소 범위 또는 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="3976e-177">클래식 VNet에 대 한 hello 로컬 네트워크 페이지 hello 클래식 포털에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3976e-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="3976e-178">Resource Manager의 경우 [PowerShell을 사용하여 로컬 네트워크 게이트웨이 설정 수정](vpn-gateway-modify-local-network-gateway.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3976e-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="3976e-179"><a name="resources"></a>REST API 및 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="3976e-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="3976e-180">추가 기술 리소스 및 VPN 게이트웨이 구성에 대 한 REST Api, PowerShell cmdlet 또는 Azure CLI를 사용 하는 경우 특정 구문 요구 사항에 대 한 hello 다음 페이지를 참조:</span><span class="sxs-lookup"><span data-stu-id="3976e-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="3976e-181">**클래식**</span><span class="sxs-lookup"><span data-stu-id="3976e-181">**Classic**</span></span> | <span data-ttu-id="3976e-182">**리소스 관리자**</span><span class="sxs-lookup"><span data-stu-id="3976e-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="3976e-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3976e-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="3976e-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3976e-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="3976e-185">REST API</span><span class="sxs-lookup"><span data-stu-id="3976e-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="3976e-186">REST API</span><span class="sxs-lookup"><span data-stu-id="3976e-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="3976e-187">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="3976e-187">Not supported</span></span> | [<span data-ttu-id="3976e-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3976e-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="3976e-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3976e-189">Next steps</span></span>

<span data-ttu-id="3976e-190">사용 가능한 연결 구성에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3976e-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>