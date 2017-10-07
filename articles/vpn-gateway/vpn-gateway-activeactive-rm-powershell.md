---
title: "VPN Gateway에 대한 활성-활성 S2S VPN 연결 구성: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 PowerShell을 사용하여 Azure VPN Gateway와의 활성-활성 연결을 구성하는 방법을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="90000-103">Azure VPN Gateway와의 활성-활성 S2S VPN 연결 구성</span><span class="sxs-lookup"><span data-stu-id="90000-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="90000-104">이 문서에서는 hello 단계 toocreate 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="90000-105">항상 사용 가능한 크로스-프레미스 연결 정보</span><span class="sxs-lookup"><span data-stu-id="90000-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="90000-106">고가용성 tooachieve 크로스-프레미스 및 VNet 대 VNet 연결을 위한 여러 VPN 게이트웨이 배포 및 네트워크와 Azure 간에 여러 병렬 연결을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="90000-107">연결 옵션 및 토폴로지의 개요에 대해서는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90000-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="90000-108">이 문서에서는 hello 설명은 액티브-액티브를 tooset 크로스-프레미스 VPN 연결 및 두 개의 가상 네트워크 간에 활성-활성 연결:</span><span class="sxs-lookup"><span data-stu-id="90000-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="90000-109">1부 - 활성-활성 모드로 Azure VPN Gateway 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="90000-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="90000-110">2부 - 활성-활성 프레미스 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="90000-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="90000-111">3부 - 활성-활성 VNet 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="90000-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="90000-112">4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트</span><span class="sxs-lookup"><span data-stu-id="90000-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="90000-113">이러한 함께 toobuild 요구 사항을 충족 하는 보다 복잡 한, 항상 사용 가능한 네트워크 토폴로지를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90000-114">Hello 액티브-액티브 모드를 사용 하는 Sku를 수행 하는 유일한 hello를 사용 하 여 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="90000-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="90000-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="90000-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="90000-116">HighPerformance(이전 레거시 SKU)</span><span class="sxs-lookup"><span data-stu-id="90000-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="90000-117"><a name ="aagateway"></a>1부 - 활성-활성 VPN Gateway 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="90000-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="90000-118">단계를 수행 하는 hello 액티브-액티브 모드에서 Azure VPN 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="90000-119">hello hello 액티브-액티브 및 활성-대기 게이트웨이 간의 주요 차이점:</span><span class="sxs-lookup"><span data-stu-id="90000-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="90000-120">두 개의 공용 IP 주소로 toocreate 두 게이트웨이 IP 구성을 사용 해야</span><span class="sxs-lookup"><span data-stu-id="90000-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="90000-121">Hello EnableActiveActiveFeature 플래그를 설정 필요</span><span class="sxs-lookup"><span data-stu-id="90000-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="90000-122">hello 게이트웨이 SKU VpnGw1, VpnGw2, VpnGw3, 또는 HighPerformance (레거시 SKU) 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="90000-123">hello 다른 속성은 hello hello 액티브-액티브 비 게이트웨이와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="90000-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="90000-124">Before you begin</span></span>
* <span data-ttu-id="90000-125">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="90000-126">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="90000-127">Tooinstall hello Azure 리소스 관리자 PowerShell cmdlet을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="90000-128">참조 [Azure PowerShell 개요](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="90000-129">1단계 - VNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="90000-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="90000-130">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="90000-130">1. Declare your variables</span></span>
<span data-ttu-id="90000-131">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="90000-132">hello 감시할 hello 값을 사용 하 여이 연습에 대 한 hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="90000-133">프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="90000-134">이러한 유형의 구성에 잘 알고 hello 단계 toobecome를 통해 실행 하는 경우 이러한 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="90000-135">Hello 변수를 수정 복사 하 고 PowerShell 콘솔에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="90000-136">2. Tooyour 구독을 연결 하 고 새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="90000-137">TooPowerShell 모드 toouse hello 리소스 관리자 cmdlet을 전환 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="90000-138">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90000-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="90000-139">PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="90000-140">다음 샘플 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="90000-141">3. TestVNet1 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-141">3. Create TestVNet1</span></span>
<span data-ttu-id="90000-142">아래 hello 샘플 TestVNet1 세 개의 서브넷, 하나의 호출된 GatewaySubnet, 하나의 호출된 프런트 엔드, 및 라는 하나의 호출된 백 엔드 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90000-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="90000-143">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="90000-144">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="90000-145">2 단계-액티브-액티브 모드 TestVNet1에 대 한 hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="90000-146">1. Hello 공용 IP 주소 및 게이트웨이 IP 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="90000-147">두 요청 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 VNet을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="90000-148">또한 hello 서브넷 및 필요한 IP 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="90000-149">2. 활성-활성 구성으로 hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="90000-150">TestVNet1에 대 한 hello 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90000-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="90000-151">Note GatewayIpConfig 항목이 두 및 hello EnableActiveActiveFeature 플래그가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="90000-152">한 게이트웨이 만드는 시간이 오래 걸릴 수 있습니다 (45 분 또는 자세한 toocomplete).</span><span class="sxs-lookup"><span data-stu-id="90000-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="90000-153">3. Hello 게이트웨이 공용 IP 주소 및 hello BGP 피어 IP 주소</span><span class="sxs-lookup"><span data-stu-id="90000-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="90000-154">Hello 게이트웨이 만든 후 Azure VPN 게이트웨이 hello에 tooobtain hello BGP 피어 IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="90000-155">온-프레미스 VPN 장치에 대 한 BGP 피어도 필요한 tooconfigure hello Azure VPN 게이트웨이 주소가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="90000-156">다음 cmdlet tooshow hello 두 개의 공용 IP 주소가 VPN 게이트웨이와 각 게이트웨이 인스턴스에 대 한 해당 BGP 피어 IP 주소에 할당 된 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="90000-157">hello 게이트웨이 인스턴스 및 해당 BGP 피어 링 주소는 hello에 대 한 hello 공용 IP 주소의 hello 순서 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="90000-158">이 예제에서는 hello 게이트웨이 40.112.190.5의 공용 IP 사용 하 여 VM 10.12.255.4을 사용 하 여 BGP 피어 링 주소로,과 138.91.156.129 hello 게이트웨이 10.12.255.5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="90000-159">Toohello 액티브-액티브 게이트웨이 연결 하는 VPN 장치 온-프레미스를 설정할 때이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="90000-160">hello 게이트웨이 아래의 모든 주소가 hello 다이어그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![활성-활성 게이트웨이](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="90000-162">Hello 게이트웨이 만든 후에이 게이트웨이 tooestablish 액티브-액티브 크로스-프레미스 또는 VNet 대 VNet 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="90000-163">hello 다음 섹션에서는 hello 단계 toocomplete hello 연습 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="90000-164"><a name ="aacrossprem"></a>2부 - 활성-활성 프레미스 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="90000-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="90000-165">로컬 네트워크 게이트웨이 toorepresent toocreate 해야 tooestablish 크로스-프레미스 연결을 온-프레미스 VPN 장치 및 hello 로컬 네트워크 게이트웨이와 tooconnect hello Azure VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="90000-166">이 예제에서는 hello Azure VPN 게이트웨이 액티브-액티브 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="90000-167">결과적으로,이 있어도 하나만 온-프레미스 VPN 장치 (로컬 네트워크 게이트웨이) 및 하나의 연결 리소스를 모두 Azure VPN 게이트웨이 인스턴스가 hello 온-프레미스 장치와 S2S VPN 터널을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="90000-168">계속하기 전에 이 연습의 [1부](#aagateway) 를 완료했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="90000-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="90000-169">1 단계-만들고 hello 로컬 네트워크 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="90000-170">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="90000-170">1. Declare your variables</span></span>
<span data-ttu-id="90000-171">이 연습에는 hello 다이어그램에 표시 된 toobuild hello 구성을 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="90000-172">수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="90000-173">몇 가지 작업 toonote hello 로컬 네트워크 게이트웨이 매개 변수 관련:</span><span class="sxs-lookup"><span data-stu-id="90000-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="90000-174">로컬 네트워크 게이트웨이 hello 동일 hello 또는 VPN 게이트웨이 hello와 그룹을 다른 위치 및 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="90000-175">이 예제에서는 찍고 다른 리소스 그룹에만 hello에 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="90000-176">위에 나와 있는 것 처럼 온-프레미스 VPN 장치를 하나만 경우 BGP 프로토콜 유무 hello 액티브-액티브 연결이 작동 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="90000-177">이 예제에서는 hello 크로스-프레미스 연결에 대 한 BGP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="90000-178">BGP가 사용 하는 경우 로컬 네트워크 게이트웨이 hello toodeclare 사용 해야 하는 hello 접두사는 hello 호스트 주소 VPN 장치에서 BGP 피어 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="90000-179">이 경우에는 "10.52.255.253/32"의 접두사 /32입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="90000-180">다시 확인하면 온-프레미스 네트워크와 Azure VNet 간에는 서로 다른 BGP ASN을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="90000-181">동일 hello는 이러한, 해야 toochange VNet ASN BGP 인접 항목과 다른 온-프레미스 VPN 장치 이미 사용 하 여 hello ASN toopeer 경우.</span><span class="sxs-lookup"><span data-stu-id="90000-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="90000-182">2. Site5에 대 한 hello 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="90000-183">계속 하기 전에 연결된 되어 tooSubscription 1이 선택 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="90000-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="90000-184">아직 만들지 않은 경우 hello 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90000-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="90000-185">2 단계-hello VNet 게이트웨이 및 로컬 네트워크 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="90000-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="90000-186">1. Hello 두 게이트웨이 가져오기</span><span class="sxs-lookup"><span data-stu-id="90000-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="90000-187">2. Hello TestVNet1 tooSite5 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="90000-188">이 단계에서는 hello 연결 만듭니다 TestVNet1 tooSite5_1에서 "EnableBGP" 너무 설정으로 $True입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="90000-189">3. 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수</span><span class="sxs-lookup"><span data-stu-id="90000-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="90000-190">이 연습에 대 한 온-프레미스 VPN 장치에 hello BGP 구성 섹션에 입력 해야 하는 hello 매개 변수를 나열 하는 hello 감시할:</span><span class="sxs-lookup"><span data-stu-id="90000-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="90000-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="90000-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="90000-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="90000-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="90000-193">Tooannounce 접두사: 10.51.0.0/16 및 10.52.0.0/16 (예)</span><span class="sxs-lookup"><span data-stu-id="90000-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="90000-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="90000-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="90000-195">Azure VNet BGP IP 1: 10.12.255.4 터널 too40.112.190.5에 대 한</span><span class="sxs-lookup"><span data-stu-id="90000-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="90000-196">Azure VNet BGP IP 2: 10.12.255.5 터널 too138.91.156.129에 대 한</span><span class="sxs-lookup"><span data-stu-id="90000-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="90000-197">고정 경로: 대상 10.12.255.4/32, 다음 홉 hello VPN 터널 인터페이스 too40.112.190.5 대상 10.12.255.5/32, 다음 홉 hello VPN 터널 인터페이스 too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="90000-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="90000-198">eBGP 멀티 홉: eBGP은 필요한 경우 장치에서 사용할 hello "멀티 홉" 옵션 확인</span><span class="sxs-lookup"><span data-stu-id="90000-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="90000-199">hello 연결 하도록 hello IPsec 연결을 설정 하는 몇 분 및 hello BGP 피어 링 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="90000-200">지금까지이 예에서는 아래의 그림과 hello에 하나의 온-프레미스 VPN 장치 구성에:</span><span class="sxs-lookup"><span data-stu-id="90000-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="90000-202">3 단계-연결할 두 개의 온-프레미스 VPN 장치 toohello 액티브-액티브 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="90000-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="90000-203">Hello에 두 개의 VPN 장치를 보유 하는 경우 동일 온-프레미스 네트워크로 연결 hello Azure VPN 게이트웨이 toohello 두 번째 VPN 장치 여 이중 중복성을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="90000-204">1. Site5에 대 한 hello 두 번째 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="90000-205">참고는 hello 게이트웨이 IP 주소, 주소 접두사 및 로컬 네트워크 게이트웨이 두 번째 hello에 대 한 BGP 피어 링 주소와 겹치면 안 hello에 대 한 이전 로컬 네트워크 게이트웨이 hello 동일한 온-프레미스 네트워크.</span><span class="sxs-lookup"><span data-stu-id="90000-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="90000-206">2. Hello VNet 게이트웨이 및 hello 두 번째 로컬 네트워크 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="90000-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="90000-207">TestVNet1 tooSite5_2 hello 연결 "EnableBGP" 너무 설정 만들기 $True</span><span class="sxs-lookup"><span data-stu-id="90000-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="90000-208">3. 두 번째 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수</span><span class="sxs-lookup"><span data-stu-id="90000-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="90000-209">마찬가지로, hello 매개 변수 목록 아래 입력할 예정 VPN 장치를 두 번째 hello:</span><span class="sxs-lookup"><span data-stu-id="90000-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="90000-210">Hello 연결 (터널), 설정 되 면 이중 중복 VPN 장치와 온-프레미스 네트워크 및 Azure에 연결 하는 터널 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="90000-212"><a name ="aav2v"></a>3부 - 활성-활성 VNet 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="90000-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="90000-213">이 섹션에서는 BGP를 사용하여 활성-활성 VNet 간 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90000-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="90000-214">아래 hello 지침 위에 나열 된 hello 이전 단계에서 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="90000-215">완료 해야 [1 부](#aagateway) toocreate TestVNet1를 구성 하 고 hello VPN 게이트웨이 BGP 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="90000-216">1 단계-TestVNet2 및 hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="90000-217">것이 중요 한 toomake hello 새 가상 네트워크를 TestVNet2의 hello IP 주소 공간 VNet 범위와 겹치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="90000-218">이 예제에서는 가상 네트워크 hello 속해 toohello 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="90000-219">다른 구독; 간에 VNet 대 VNet 연결을 설정할 수 있습니다. 너무를 참조 하십시오[VNet 대 VNet 연결 구성](vpn-gateway-vnet-vnet-rm-ps.md) toolearn 더 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="90000-220">Hello 추가 "-EnableBgp $True" 때 연결 tooenable BGP hello 만들기.</span><span class="sxs-lookup"><span data-stu-id="90000-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="90000-221">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="90000-221">1. Declare your variables</span></span>
<span data-ttu-id="90000-222">수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="90000-223">2. TestVNet2 hello 새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="90000-224">3. TestVNet2에 대 한 hello 액티브-액티브 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="90000-225">두 요청 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 VNet을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="90000-226">또한 hello 서브넷 및 필요한 IP 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="90000-227">번호 및 hello "EnableActiveActiveFeature" 플래그로 hello로 hello VPN 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90000-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="90000-228">참고 Azure VPN 게이트웨이 hello 기본 ASN를 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="90000-229">hello에 대 한 Asn hello Vnet 연결 된 다른 tooenable BGP 및 전송 라우팅과 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="90000-230">2 단계-hello TestVNet1 및 TestVNet2 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="90000-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="90000-231">이 예에서 두 게이트웨이 hello에는 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="90000-232">Hello에이 단계를 완료 하려면 같은 PowerShell 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="90000-233">1. 두 게이트웨이 가져오기</span><span class="sxs-lookup"><span data-stu-id="90000-233">1. Get both gateways</span></span>
<span data-ttu-id="90000-234">로그인 하 고 연결 tooSubscription 1에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="90000-235">2. 두 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="90000-235">2. Create both connections</span></span>
<span data-ttu-id="90000-236">이 단계에서는 만들어집니다 TestVNet1 tooTestVNet2에서 hello 연결과 hello 연결 TestVNet2 tooTestVNet1에서.</span><span class="sxs-lookup"><span data-stu-id="90000-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="90000-237">두 연결에 대 한 있는지 tooenable BGP를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="90000-238">다음이 단계를 완료 한 후 hello 연결 잠시 후에 설정 됩니다 및 이중 중복 hello VNet 대 VNet 연결 완료 되 면 hello BGP 피어 링 세션을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90000-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="90000-240"><a name ="aaupdate"></a>4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트</span><span class="sxs-lookup"><span data-stu-id="90000-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="90000-241">hello 마지막 섹션 기존 Azure VPN 게이트웨이 구성 하는 방법에 대해 설명 합니다 활성-대기 tooactive active 모드 또는 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="90000-242">이 섹션에는 표준 tooHighPerformance에서 이미 만들어진 VPN 게이트웨이의 hello 단계 tooresize 레거시 SKU (이전 SKU) 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="90000-243">이러한 단계는 이전 레거시 SKU tooone의 hello 업그레이드 하지 않는 새 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="90000-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="90000-244">활성-대기 게이트웨이 tooactive-활성 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="90000-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="90000-245">1. 게이트웨이 매개 변수</span><span class="sxs-lookup"><span data-stu-id="90000-245">1. Gateway parameters</span></span>
<span data-ttu-id="90000-246">다음 예제는 hello 액티브-액티브 게이트웨이 활성-대기 게이트웨이 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="90000-247">다른 공용 IP 주소 toocreate 필요 다음 두 번째 게이트웨이 IP 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="90000-248">다음 hello 매개 변수 사용.</span><span class="sxs-lookup"><span data-stu-id="90000-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="90000-249">2. Hello 공용 IP 주소를 만든 다음 hello 두 번째 게이트웨이 IP 구성에 추가</span><span class="sxs-lookup"><span data-stu-id="90000-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="90000-250">3. 활성-활성 모드 및 업데이트 hello 게이트웨이 사용</span><span class="sxs-lookup"><span data-stu-id="90000-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="90000-251">PowerShell tootrigger hello 실제 업데이트에서 hello 게이트웨이 개체를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="90000-252">hello hello 가상 네트워크 게이트웨이 SKU 변경 해야 (크기가 조정 된) tooHighPerformance 표준으로 이전에 만든 이후로 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="90000-253">이 업데이트에는 30 too45 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="90000-254">액티브-액티브 게이트웨이 tooactive 대기 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="90000-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="90000-255">1. 게이트웨이 매개 변수</span><span class="sxs-lookup"><span data-stu-id="90000-255">1. Gateway parameters</span></span>
<span data-ttu-id="90000-256">사용 하 여 hello 동일 위와 같이 매개 변수 이름을 가져옵니다. hello hello IP 구성 tooremove 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="90000-257">2. Hello 게이트웨이 IP 구성을 제거 하 고 hello 액티브-액티브 모드 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="90000-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="90000-258">마찬가지로, PowerShell tootrigger hello 실제 업데이트에서 hello 게이트웨이 개체를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90000-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="90000-259">이 업데이트를 too30 너무 45 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90000-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90000-260">Next steps</span></span>
<span data-ttu-id="90000-261">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90000-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="90000-262">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90000-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
