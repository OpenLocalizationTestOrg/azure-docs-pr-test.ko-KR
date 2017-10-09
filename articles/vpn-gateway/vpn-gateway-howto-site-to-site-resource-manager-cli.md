---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN: CLI | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 이 단계는 CLI를 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
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
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="53d4d-104">CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="53d4d-105">이 문서에서는 어떻게 toouse hello Azure CLI toocreate 온-프레미스 네트워크 toohello VNet에서에서 사이트 간 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="53d4d-106">이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="53d4d-107">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53d4d-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="53d4d-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="53d4d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53d4d-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="53d4d-110">CLI</span><span class="sxs-lookup"><span data-stu-id="53d4d-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="53d4d-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="53d4d-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="53d4d-113">사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="53d4d-114">이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="53d4d-115">VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="53d4d-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="53d4d-116">Before you begin</span></span>

<span data-ttu-id="53d4d-117">Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="53d4d-118">호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="53d4d-119">호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="53d4d-120">VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="53d4d-121">이 IP 주소는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="53d4d-122">온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="53d4d-123">이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="53d4d-124">온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="53d4d-125">Hello CLI 명령 (2.0 이상)의 최신 버전을 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="53d4d-126">Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="53d4d-127"><a name="example"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="53d4d-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="53d4d-128">값 toocreate 테스트 환경에 따라 hello를 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해:</span><span class="sxs-lookup"><span data-stu-id="53d4d-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

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

## <span data-ttu-id="53d4d-129"><a name="Login"></a>1. Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="53d4d-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="53d4d-130"><a name="rg"></a>2. 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="53d4d-131">hello 다음 예제에서는 'TestRG1' hello 'eastus' 위치에 명명 된 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="53d4d-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="53d4d-132">Hello 지역 되도록 toocreate VNet에에서 리소스 그룹이 이미 있는 경우 하나를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="53d4d-133"><a name="VNet"></a>3. 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="53d4d-134">가상 네트워크를 아직 없는 경우 새로 만들 hello를 사용 하 여 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="53d4d-135">가상 네트워크를 만들 때 지정한 hello 주소 공간 온-프레미스 네트워크에가지고 있는 hello 주소 공간 중 하나라도 겹치지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="53d4d-136">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 'TestVNet1' 및 'Subnet1' 서브넷에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="53d4d-137">4. <a name="gwsub"></a>Hello 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="53d4d-138">이 구성에는 게이트웨이 서브넷도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="53d4d-139">hello 가상 네트워크 게이트웨이 hello VPN 게이트웨이 서비스에서 사용 되는 hello IP 주소를 포함 하는 게이트웨이 서브넷을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="53d4d-140">게이트웨이 서브넷을 만들 때 이름을 'GatewaySubnet'으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="53d4d-141">다른 이름을 지정하는 경우 서브넷을 만들지만 Azure에서는 게이트웨이 서브넷으로 취급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="53d4d-142">지정 하는 hello 게이트웨이 서브넷의 hello 크기에 따라 달라 집니다 hello VPN 게이트웨이 구성 toocreate 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="53d4d-143">가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, / 27 또는/28 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="53d4d-144">더 큰 게이트웨이 서브넷을 사용 하 여 구성에 대 한 충분 한 IP 주소 tooaccommodate 가능한 이후 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="53d4d-145">사용 하 여 hello [az 네트워크 vnet 서브넷 만들기](/cli/azure/network/vnet/subnet#create) 명령 toocreate hello 게이트웨이 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="53d4d-146"><a name="localnet"></a>5. Hello 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="53d4d-147">일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="53d4d-148">Hello 사이트 기준인 Azure 수 tooit를 참조 하십시오. 그런 다음 hello IP 주소를 지정 된 이름을 지정 hello 온-프레미스 VPN 장치 toowhich의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="53d4d-149">또한 hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="53d4d-150">지정 하는 hello 주소 접두사는 온-프레미스 네트워크에 있는 hello 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="53d4d-151">온-프레미스 네트워크 변경 되 면 hello 접두사를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="53d4d-152">다음 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-152">Use hello following values:</span></span>

* <span data-ttu-id="53d4d-153">hello *-게이트웨이 ip 주소* 온-프레미스 VPN 장치의 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="53d4d-154">VPN 장치는 NAT 뒤에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="53d4d-155">hello *-로컬 주소-접두사* 는 온-프레미스 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="53d4d-156">사용 하 여 hello [az 네트워크 로컬 게이트웨이 만들기](/cli/azure/network/local-gateway#create) 명령 tooadd 여러 주소 접두사와 로컬 네트워크 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="53d4d-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="53d4d-157"><a name="PublicIP"></a>6. 공용 IP 주소 요청</span><span class="sxs-lookup"><span data-stu-id="53d4d-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="53d4d-158">VPN Gateway에는 공용 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="53d4d-159">먼저 hello IP 주소 리소스를 요청 하 고 가상 네트워크 게이트웨이 만들 때 tooit를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="53d4d-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="53d4d-160">hello IP 주소를 사용 hello VPN 게이트웨이 만들 때 toohello 리소스를 동적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="53d4d-161">현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="53d4d-162">고정 공용 IP 주소 할당을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="53d4d-163">그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="53d4d-164">hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="53d4d-165">VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="53d4d-166">사용 하 여 hello [az 네트워크 공용 ip 만들기](/cli/azure/network/public-ip#create) 명령 toorequest 동적 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="53d4d-167"><a name="CreateGateway"></a>7. Hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="53d4d-168">Hello 가상 네트워크 VPN 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="53d4d-169">VPN 게이트웨이 만들기 too45 분 또는 toocomplete 자세한 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="53d4d-170">다음 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-170">Use hello following values:</span></span>

* <span data-ttu-id="53d4d-171">hello *-게이트웨이 유형* 사이트-사이트에 대 한 구성은 *Vpn*합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="53d4d-172">hello 게이트웨이 형식은 항상 구현 하는 특정 toohello 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="53d4d-173">자세한 내용은 [게이트웨이 유형](vpn-gateway-about-vpn-gateway-settings.md#gwtype)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="53d4d-174">hello *-vpn 형식* 수 *RouteBased* (일부 설명서에서는 동적 게이트웨이 tooas 함) 또는 *PolicyBased* (tooas은 정적 게이트웨이가 중 일부를 참조 합니다. 설명서)입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="53d4d-175">hello 설정은 hello 장치에 연결 하는 특정 toorequirements입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="53d4d-176">VPN Gateway 유형에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#vpntype)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="53d4d-177">Hello toouse 게이트웨이 SKU를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="53d4d-178">특정 SKU에 대한 구성 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="53d4d-179">자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="53d4d-180">Hello를 사용 하 여 hello VPN 게이트웨이 만들기 [az 네트워크 vnet 게이트웨이 만들기](/cli/azure/network/vnet-gateway#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="53d4d-181">'대기 없음-' 매개 변수 hello를 사용 하 여이 명령을 실행 하면 피드백이 나 출력에 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="53d4d-182">이 매개 변수는 hello 백그라운드에 hello 게이트웨이 toocreate를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="53d4d-183">게이트웨이 toocreate 약 45 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="53d4d-184"><a name="VPNDevice"></a>8. VPN 장치 구성</span><span class="sxs-lookup"><span data-stu-id="53d4d-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="53d4d-185">사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="53d4d-186">이 단계에서는 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="53d4d-187">VPN 장치를 구성할 때 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="53d4d-188">공유 키 -</span><span class="sxs-lookup"><span data-stu-id="53d4d-188">A shared key.</span></span> <span data-ttu-id="53d4d-189">동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="53d4d-190">이 예제에서는 기본적인 공유 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="53d4d-191">더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="53d4d-192">가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="53d4d-193">Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="53d4d-194">가상 네트워크 게이트웨이 사용 하 여 hello의 toofind hello 공용 IP 주소 [az 네트워크 공개 ip 목록](/cli/azure/network/public-ip#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="53d4d-195">읽기 쉽도록 hello 출력은 테이블 형식으로 공용 Ip의 서식이 지정 된 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="53d4d-196"><a name="CreateConnection"></a>9. Hello VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="53d4d-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="53d4d-197">가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 간의 hello 사이트 간 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="53d4d-198">사용량 기준 과금 특별 한 주의 toohello 공유 키 값을 구성 하는 hello와 일치 해야 하는 VPN 장치에 대 한 키 값을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="53d4d-199">Hello를 사용 하 여 hello 연결 만들기 [az 네트워크 vpn 연결 만들기](/cli/azure/network/vpn-connection#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="53d4d-200">잠시 후, hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="53d4d-201"><a name="toverify"></a>10. Hello VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="53d4d-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="53d4d-202">다른 메서드 tooverify toouse 하려면 해당 연결을 참조 [VPN 게이트웨이 연결을 확인](vpn-gateway-verify-connection-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="53d4d-203"><a name="connectVM"></a>tooconnect tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="53d4d-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="53d4d-204"><a name="tasks"></a>일반 작업</span><span class="sxs-lookup"><span data-stu-id="53d4d-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="53d4d-205">이 섹션에는 사이트 간 구성을 작업할 때 도움이 되는 일반적인 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="53d4d-206">CLI 네트워킹 명령의 전체 목록을 hello에 대 한 참조 [Azure CLI-네트워킹](/cli/azure/network)합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="53d4d-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53d4d-207">Next steps</span></span>

* <span data-ttu-id="53d4d-208">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="53d4d-209">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="53d4d-210">BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53d4d-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="53d4d-211">강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="53d4d-212">항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="53d4d-213">네트워킹 Azure CLI 명령 목록은 [Azure CLI](https://docs.microsoft.com/cli/azure/network)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d4d-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>