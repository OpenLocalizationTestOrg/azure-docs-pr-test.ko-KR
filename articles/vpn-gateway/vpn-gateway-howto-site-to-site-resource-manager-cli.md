---
title: "온-프레미스 네트워크를 Azure 가상 네트워크에 연결: 사이트 간 VPN: CLI | Microsoft Docs"
description: "공용 인터넷을 통해 온-프레미스 네트워크에서 Azure Virtual Network에 IPsec을 만드는 단계입니다. 이 단계는 CLI를 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="35cbe-104">CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="35cbe-105">이 문서에서는 Azure CLI를 사용하여 온-프레미스 네트워크에서 VNet으로 사이트 간 VPN Gateway 연결을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="35cbe-106">이 문서의 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="35cbe-107">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35cbe-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="35cbe-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="35cbe-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35cbe-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="35cbe-110">CLI</span><span class="sxs-lookup"><span data-stu-id="35cbe-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="35cbe-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="35cbe-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="35cbe-113">사이트 간 VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통해 온-프레미스 네트워크를 Azure Virtual Network에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="35cbe-114">이 연결 유형은 할당된 외부 연결 공용 IP 주소를 갖고 있는 온-프레미스에 있는 VPN 장치를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="35cbe-115">VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="35cbe-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="35cbe-116">Before you begin</span></span>

<span data-ttu-id="35cbe-117">구성을 시작하기 전에 다음 기준을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="35cbe-118">호환되는 VPN 장치 및 이 장치를 구성할 수 있는 사람이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="35cbe-119">호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="35cbe-120">VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="35cbe-121">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="35cbe-122">온-프레미스 네트워크에 있는 IP 주소 범위에 익숙하지 않은 경우 세부 정보를 제공할 수 있는 다른 사람의 도움을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="35cbe-123">이 구성을 만들 때 Azure가 온-프레미스 위치에 라우팅할 IP 주소 범위 접두사를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="35cbe-124">온-프레미스 네트워크의 어떤 서브넷도 사용자가 연결하려는 가상 네트워크 서브넷과 중첩될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="35cbe-125">최신 버전의 CLI 명령(2.0 이상)이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="35cbe-126">CLI 명령 설치에 대한 자세한 내용은 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="35cbe-127"><a name="example"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="35cbe-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="35cbe-128">다음 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 보다 정확하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="35cbe-129"><a name="Login"></a>1. 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="35cbe-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="35cbe-130"><a name="rg"></a>2. 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="35cbe-131">다음 예제에서는 'eastus' 위치에 'TestRG1'이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="35cbe-132">VNet을 만들려는 지역에 이미 리소스 그룹이 있는 경우 그 리소스 그룹을 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="35cbe-133"><a name="VNet"></a>3. 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="35cbe-134">아직 가상 네트워크가 없으면 [az network vnet create](/cli/azure/network/vnet#create) 명령을 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="35cbe-135">가상 네트워크를 만들 때 지정하는 주소 공간이 온-프레미스 네트워크에 있는 주소 공간과 겹치지 않는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="35cbe-136">다음 예제에서는 'TestVNet1'이라는 가상 네트워크와 'Subnet1'이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="35cbe-137">4. <a name="gwsub"></a>게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="35cbe-138">이 구성에는 게이트웨이 서브넷도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="35cbe-139">가상 네트워크 게이트웨이는 VPN Gateway 서비스에서 사용하는 IP 주소가 포함된 게이트웨이 서브넷을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="35cbe-140">게이트웨이 서브넷을 만들 때 이름을 'GatewaySubnet'으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="35cbe-141">다른 이름을 지정하는 경우 서브넷을 만들지만 Azure에서는 게이트웨이 서브넷으로 취급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="35cbe-142">지정하는 게이트웨이 서브넷의 크기는 만들려는 VPN Gateway 구성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="35cbe-143">게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 /27 또는 /28을 선택하여 더 많은 주소를 포함하는 큰 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="35cbe-144">더 큰 게이트웨이 서브넷을 사용하면 향후 구성을 수용할 수 있을 만큼 충분한 IP 주소를 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="35cbe-145">[az network vnet subnet create](/cli/azure/network/vnet/subnet#create) 명령을 사용하여 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="35cbe-146"><a name="localnet"></a>5. 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="35cbe-147">로컬 네트워크 게이트웨이는 일반적으로 온-프레미스 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="35cbe-148">Azure가 참조할 수 있는 사이트 이름을 지정한 다음 연결을 만들 온-프레미스 VPN 장치의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="35cbe-149">또한 VPN Gateway를 통해 VPN 장치로 라우팅될 IP 주소 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="35cbe-150">사용자가 지정하는 주소 접두사는 온-프레미스 네트워크에 있는 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="35cbe-151">온-프레미스 네트워크가 변경되면 이러한 접두사를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="35cbe-152">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-152">Use the following values:</span></span>

* <span data-ttu-id="35cbe-153">*--gateway-ip-address*는 온-프레미스 VPN 장치의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="35cbe-154">VPN 장치는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="35cbe-155">*--local-address-prefixes*는 온-프레미스 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="35cbe-156">[az network local-gateway create](/cli/azure/network/local-gateway#create) 명령을 사용하여 주소 접두사가 여러 개인 로컬 네트워크 게이트웨이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="35cbe-157"><a name="PublicIP"></a>6. 공용 IP 주소 요청</span><span class="sxs-lookup"><span data-stu-id="35cbe-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="35cbe-158">VPN Gateway에는 공용 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="35cbe-159">먼저 IP 주소 리소스를 요청하고, 가상 네트워크 게이트웨이를 만들 때 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="35cbe-160">VPN Gateway가 생성될 때 IP 주소는 리소스에 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="35cbe-161">현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="35cbe-162">고정 공용 IP 주소 할당을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="35cbe-163">하지만 IP 주소가 VPN Gateway에 할당된 후 변경되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="35cbe-164">게이트웨이가 삭제되고 다시 만들어지는 경우에만 공용 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="35cbe-165">VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="35cbe-166">[az network public-ip create](/cli/azure/network/public-ip#create) 명령을 사용하여 동적 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="35cbe-167"><a name="CreateGateway"></a>7. VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="35cbe-168">가상 네트워크 VPN Gateway 만들기.</span><span class="sxs-lookup"><span data-stu-id="35cbe-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="35cbe-169">VPN Gateway 만들기를 완료하는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="35cbe-170">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-170">Use the following values:</span></span>

* <span data-ttu-id="35cbe-171">사이트 간 구성에 대한 *--gateway-type*은 *Vpn*입니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="35cbe-172">게이트웨이 유형은 항상 구현하는 구성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="35cbe-173">자세한 내용은 [게이트웨이 유형](vpn-gateway-about-vpn-gateway-settings.md#gwtype)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="35cbe-174">*--vpn-type*은 *경로 기반*(일부 설명서에서는 동적 게이트웨이라고도 함)이거나 *정책 기반*(일부 설명서에서는 고정 게이트웨이라고도 함)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="35cbe-175">설정은 연결하는 장치의 요구 사항에 따라 좌우됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="35cbe-176">VPN Gateway 유형에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#vpntype)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="35cbe-177">사용할 게이트웨이 SKU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="35cbe-178">특정 SKU에 대한 구성 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="35cbe-179">자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="35cbe-180">[az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) 명령을 사용하여 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="35cbe-181">'--no-wait' 매개 변수를 사용하여 이 명령을 실행하면 피드백 또는 출력이 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="35cbe-182">이 매개 변수는 백그라운드에서 게이트웨이를 만드는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="35cbe-183">게이트웨이를 만들 때까지 약 45분 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="35cbe-184"><a name="VPNDevice"></a>8. VPN 장치 구성</span><span class="sxs-lookup"><span data-stu-id="35cbe-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="35cbe-185">온-프레미스 네트워크에 대한 사이트 간 연결에는 VPN 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="35cbe-186">이 단계에서는 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="35cbe-187">VPN 장치를 구성할 때 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="35cbe-188">공유 키 -</span><span class="sxs-lookup"><span data-stu-id="35cbe-188">A shared key.</span></span> <span data-ttu-id="35cbe-189">사이트 간 VPN 연결을 만들 때 지정하는 것과 동일한 공유 키입니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="35cbe-190">이 예제에서는 기본적인 공유 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="35cbe-191">실제로 사용할 키는 좀 더 복잡하게 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="35cbe-192">가상 네트워크 게이트웨이의 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="35cbe-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="35cbe-193">Azure Portal, PowerShell 또는 CLI를 사용하여 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="35cbe-194">가상 네트워크 게이트웨이의 공용 IP 주소를 찾으려면 [az network public-ip list](/cli/azure/network/public-ip#list) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="35cbe-195">읽기 쉽도록 공용 IP 목록을 테이블 형식으로 표시하도록 출력 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="35cbe-196"><a name="CreateConnection"></a>9. VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="35cbe-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="35cbe-197">가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 사이의 사이트 간 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="35cbe-198">VPN 장치에 구성된 공유 키 값과 일치하도록 공유 키 값에 특히 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="35cbe-199">[az network vpn-connection create](/cli/azure/network/vpn-connection#create) 명령을 사용하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="35cbe-200">잠시 후, 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="35cbe-201"><a name="toverify"></a>10. VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="35cbe-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="35cbe-202">다른 방법을 사용하여 연결을 확인하려면 [VPN Gateway 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="35cbe-203"><a name="connectVM"></a>가상 컴퓨터에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="35cbe-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="35cbe-204"><a name="tasks"></a>일반 작업</span><span class="sxs-lookup"><span data-stu-id="35cbe-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="35cbe-205">이 섹션에는 사이트 간 구성을 작업할 때 도움이 되는 일반적인 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="35cbe-206">CLI 네트워킹 명령의 전체 목록은 [Azure CLI - 네트워킹](/cli/azure/network)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="35cbe-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35cbe-207">Next steps</span></span>

* <span data-ttu-id="35cbe-208">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cbe-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="35cbe-209">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="35cbe-210">BGP에 대한 내용은 [BGP 개요](vpn-gateway-bgp-overview.md) 및 [BGP를 구성하는 방법](vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="35cbe-211">강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="35cbe-212">항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="35cbe-213">네트워킹 Azure CLI 명령 목록은 [Azure CLI](https://docs.microsoft.com/cli/azure/network)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35cbe-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>