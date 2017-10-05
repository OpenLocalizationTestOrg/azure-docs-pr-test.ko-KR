---
title: "온-프레미스 네트워크를 Azure Virtual Network에 연결: 사이트 간 VPN: PowerShell | Microsoft Docs"
description: "공용 인터넷을 통해 온-프레미스 네트워크에서 Azure Virtual Network에 IPsec을 만드는 단계입니다. 이 단계는 PowerShell을 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 27f4a8fb9a83b98e99df635bf4c80f6048ce348c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="3cbb2-104">PowerShell을 사용하여 사이트 간 VPN 연결로 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="3cbb2-105">이 문서에서는 PowerShell을 사용하여 온-프레미스 네트워크에서 VNet으로 사이트 간 VPN Gateway 연결을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-105">This article shows you how to use PowerShell to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="3cbb2-106">이 문서의 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="3cbb2-107">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cbb2-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3cbb2-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="3cbb2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cbb2-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="3cbb2-110">CLI</span><span class="sxs-lookup"><span data-stu-id="3cbb2-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="3cbb2-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="3cbb2-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="3cbb2-112">클래식 포털(클래식)</span><span class="sxs-lookup"><span data-stu-id="3cbb2-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="3cbb2-113">사이트 간 VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통해 온-프레미스 네트워크를 Azure Virtual Network에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="3cbb2-114">이 연결 유형은 할당된 외부 연결 공용 IP 주소를 갖고 있는 온-프레미스에 있는 VPN 장치를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="3cbb2-115">VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="3cbb2-117"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3cbb2-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="3cbb2-118">구성을 시작하기 전에 다음 기준을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-118">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="3cbb2-119">호환되는 VPN 장치 및 이 장치를 구성할 수 있는 사람이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-119">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="3cbb2-120">호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="3cbb2-121">VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="3cbb2-122">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="3cbb2-123">온-프레미스 네트워크에 있는 IP 주소 범위에 익숙하지 않은 경우 세부 정보를 제공할 수 있는 다른 사람의 도움을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-123">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="3cbb2-124">이 구성을 만들 때 Azure가 온-프레미스 위치에 라우팅할 IP 주소 범위 접두사를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-124">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="3cbb2-125">온-프레미스 네트워크의 어떤 서브넷도 사용자가 연결하려는 가상 네트워크 서브넷과 중첩될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-125">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="3cbb2-126">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-126">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3cbb2-127">PowerShell cmdlet은 자주 업데이트되며, 일반적으로 PowerShell cmdlet을 업데이트하여 최신 기능을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-127">PowerShell cmdlets are updated frequently and you will typically need to update your PowerShell cmdlets to get the latest feature functionality.</span></span> <span data-ttu-id="3cbb2-128">PowerShell cmdlet을 업데이트하지 않으면 지정된 값이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-128">If you don't update your PowerShell cmdlets, the values specified may fail.</span></span> <span data-ttu-id="3cbb2-129">PowerShell cmdlet 다운로드 및 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-129">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="3cbb2-130"><a name="example"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="3cbb2-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="3cbb2-131">이 문서의 예제에서는 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-131">The examples in this article use the following values.</span></span> <span data-ttu-id="3cbb2-132">이러한 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 보다 정확하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-132">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="3cbb2-133"><a name="Login"></a>1. 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="3cbb2-133"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="3cbb2-134"><a name="VNet"></a>2. 가상 네트워크 및 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="3cbb2-135">가상 네트워크가 아직 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="3cbb2-136">가상 네트워크를 만들 때 지정하는 주소 공간이 온-프레미스 네트워크에 있는 주소 공간과 겹치지 않는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-136">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="3cbb2-137"><a name="vnet"></a>가상 네트워크 및 게이트웨이 서브넷을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3cbb2-137"><a name="vnet"></a>To create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="3cbb2-138">이 예제에서는 가상 네트워크 및 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="3cbb2-139">게이트웨이 서브넷을 추가해야 하는 가상 네트워크가 이미 있는 경우 [이미 만든 가상 네트워크에 게이트웨이 서브넷을 추가하려면](#gatewaysubnet)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-139">If you already have a virtual network that you need to add a gateway subnet to, see [To add a gateway subnet to a virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="3cbb2-140">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="3cbb2-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="3cbb2-141">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-141">Create your virtual network.</span></span>

1. <span data-ttu-id="3cbb2-142">변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-142">Set the variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="3cbb2-143">VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-143">Create the VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="3cbb2-144"><a name="gatewaysubnet"></a>이미 만든 가상 네트워크에 게이트웨이 서브넷을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="3cbb2-144"><a name="gatewaysubnet"></a>To add a gateway subnet to a virtual network you have already created</span></span>

1. <span data-ttu-id="3cbb2-145">변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-145">Set the variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="3cbb2-146">게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-146">Create the gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="3cbb2-147">구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-147">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="3cbb2-148">3. <a name="localnet"></a>로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-148">3. <a name="localnet"></a>Create the local network gateway</span></span>

<span data-ttu-id="3cbb2-149">로컬 네트워크 게이트웨이는 일반적으로 온-프레미스 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-149">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="3cbb2-150">Azure가 참조할 수 있는 사이트 이름을 지정한 다음 연결을 만들 온-프레미스 VPN 장치의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-150">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="3cbb2-151">또한 VPN Gateway를 통해 VPN 장치로 라우팅될 IP 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-151">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="3cbb2-152">사용자가 지정하는 주소 접두사는 온-프레미스 네트워크에 있는 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-152">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="3cbb2-153">온-프레미스 네트워크가 변경되면 이러한 접두사를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-153">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="3cbb2-154">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-154">Use the following values:</span></span>

* <span data-ttu-id="3cbb2-155">*GatewayIPAddress*는 온-프레미스 VPN 장치의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-155">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="3cbb2-156">VPN 장치는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="3cbb2-157">*AddressPrefix*는 온-프레미스 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-157">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="3cbb2-158">로컬 네트워크 게이트웨이에 단일 주소 접두사를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="3cbb2-158">To add a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="3cbb2-159">로컬 네트워크 게이트웨이에 중복 주소 접두사를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="3cbb2-159">To add a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="3cbb2-160">로컬 네트워크 게이트웨이에 대한 IP 주소 접두사를 수정하려면:</span><span class="sxs-lookup"><span data-stu-id="3cbb2-160">To modify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="3cbb2-161">경우에 따라 로컬 네트워크 게이트웨이 접두사를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="3cbb2-162">IP 주소 접두사를 수정하기 위해 수행하는 단계는 VPN Gateway 연결을 만들었는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-162">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="3cbb2-163">이 문서의 [로컬 네트워크 게이트웨이에 대한 IP 주소 접두사 수정](#modify) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-163">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="3cbb2-164"><a name="PublicIP"></a>4. 공용 IP 주소 요청</span><span class="sxs-lookup"><span data-stu-id="3cbb2-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="3cbb2-165">VPN Gateway에는 공용 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="3cbb2-166">먼저 IP 주소 리소스를 요청하고, 가상 네트워크 게이트웨이를 만들 때 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-166">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="3cbb2-167">VPN Gateway가 생성될 때 IP 주소는 리소스에 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-167">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="3cbb2-168">현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="3cbb2-169">고정 공용 IP 주소 할당을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="3cbb2-170">하지만 IP 주소가 VPN Gateway에 할당된 후 변경되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-170">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="3cbb2-171">게이트웨이가 삭제되고 다시 만들어지는 경우에만 공용 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-171">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="3cbb2-172">VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="3cbb2-173">가상 네트워크 VPN Gateway에 할당할 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-173">Request a Public IP address that will be assigned to your virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="3cbb2-174"><a name="GatewayIPConfig"></a>5. 게이트웨이 IP 주소 지정 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-174"><a name="GatewayIPConfig"></a>5. Create the gateway IP addressing configuration</span></span>

<span data-ttu-id="3cbb2-175">게이트웨이 구성은 사용할 공용 IP 주소 및 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-175">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="3cbb2-176">다음 예제를 사용하여 게이트웨이 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-176">Use the following example to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="3cbb2-177"><a name="CreateGateway"></a>6. VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-177"><a name="CreateGateway"></a>6. Create the VPN gateway</span></span>

<span data-ttu-id="3cbb2-178">가상 네트워크 VPN Gateway 만들기.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-178">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="3cbb2-179">VPN Gateway 만들기를 완료하는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-179">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="3cbb2-180">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-180">Use the following values:</span></span>

* <span data-ttu-id="3cbb2-181">사이트 간 구성에 대한 *-GatewayType*은 *Vpn*입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-181">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="3cbb2-182">게이트웨이 유형은 항상 구현하는 구성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-182">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="3cbb2-183">예를 들어 다른 게이트웨이 구성인 GatewayType ExpressRoute가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="3cbb2-184">*-VpnType*은 *경로 기반*(일부 설명서에서는 동적 게이트웨이라고도 함)이거나 *정책 기반*(일부 설명서에서는 고정 게이트웨이라고도 함)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-184">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="3cbb2-185">VPN Gateway 형식에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="3cbb2-186">사용할 게이트웨이 SKU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-186">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="3cbb2-187">특정 SKU에 대한 구성 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="3cbb2-188">자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="3cbb2-189">-GatewaySku와 관련하여 VPN 게이트웨이를 만들 때 오류가 발생하면 최신 버전의 PowerShell cmdlet을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-189">If you get an error when creating the VPN gateway regarding the -GatewaySku, verify that you have installed the latest version of the PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="3cbb2-190"><a name="ConfigureVPNDevice"></a>7. VPN 장치 구성</span><span class="sxs-lookup"><span data-stu-id="3cbb2-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="3cbb2-191">온-프레미스 네트워크에 대한 사이트 간 연결에는 VPN 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-191">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="3cbb2-192">이 단계에서는 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="3cbb2-193">VPN 장치를 구성할 때 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-193">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="3cbb2-194">공유 키 -</span><span class="sxs-lookup"><span data-stu-id="3cbb2-194">A shared key.</span></span> <span data-ttu-id="3cbb2-195">사이트 간 VPN 연결을 만들 때 지정하는 것과 동일한 공유 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-195">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="3cbb2-196">이 예제에서는 기본적인 공유 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="3cbb2-197">실제로 사용할 키는 좀 더 복잡하게 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-197">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="3cbb2-198">가상 네트워크 게이트웨이의 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="3cbb2-198">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="3cbb2-199">Azure Portal, PowerShell 또는 CLI를 사용하여 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-199">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="3cbb2-200">PowerShell을 사용하여 가상 네트워크 게이트웨이의 공용 IP 주소를 찾으려면 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-200">To find the Public IP address of your virtual network gateway using PowerShell, use the following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="3cbb2-201"><a name="CreateConnection"></a>8. VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="3cbb2-201"><a name="CreateConnection"></a>8. Create the VPN connection</span></span>

<span data-ttu-id="3cbb2-202">다음으로 가상 네트워크 게이트웨이와 VPN 장치 사이에 사이트 간 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-202">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="3cbb2-203">사용자 고유의 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-203">Be sure to replace the values with your own.</span></span> <span data-ttu-id="3cbb2-204">공유 키는 VPN 장치 구성에 사용한 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-204">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="3cbb2-205">사이트 간 '-ConnectionType'은 *IPsec*입니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-205">Notice that the '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="3cbb2-206">변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-206">Set the variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="3cbb2-207">연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-207">Create the connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="3cbb2-208">잠시 후, 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-208">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="3cbb2-209"><a name="toverify"></a>9. VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="3cbb2-209"><a name="toverify"></a>9. Verify the VPN connection</span></span>

<span data-ttu-id="3cbb2-210">VPN 연결을 확인하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-210">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="3cbb2-211"><a name="connectVM"></a>가상 컴퓨터에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="3cbb2-211"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="3cbb2-212"><a name="modify"></a>로컬 네트워크 게이트웨이에 대한 IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="3cbb2-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="3cbb2-213">온-프레미스 위치에 라우팅하려는 IP 주소 접두사를 변경하는 경우 로컬 네트워크 게이트웨이를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-213">If the IP address prefixes that you want routed to your on-premises location change, you can modify the local network gateway.</span></span> <span data-ttu-id="3cbb2-214">두 가지 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="3cbb2-215">게이트웨이 연결을 이미 만들었는지 여부에 따라 선택하는 지침이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-215">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="3cbb2-216"><a name="modifygwipaddress"></a>로컬 네트워크 게이트웨이에 대한 IP 주소 수정</span><span class="sxs-lookup"><span data-stu-id="3cbb2-216"><a name="modifygwipaddress"></a>Modify the gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3cbb2-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cbb2-217">Next steps</span></span>

*  <span data-ttu-id="3cbb2-218">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-218">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="3cbb2-219">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="3cbb2-220">BGP에 대한 내용은 [BGP 개요](vpn-gateway-bgp-overview.md) 및 [BGP를 구성하는 방법](vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cbb2-220">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
