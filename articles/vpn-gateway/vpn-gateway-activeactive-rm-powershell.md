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
ms.openlocfilehash: a9f71b566ffdb163f95634835f64589a700d712f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="6b902-103">Azure VPN Gateway와의 활성-활성 S2S VPN 연결 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="6b902-104">이 문서에서는 Resource Manager 배포 모델 및 PowerShell을 사용하여 활성-활성 프레미스 간 및 VNet 간 연결을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="6b902-105">항상 사용 가능한 크로스-프레미스 연결 정보</span><span class="sxs-lookup"><span data-stu-id="6b902-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="6b902-106">크로스-프레미스 및 VNet 간 연결에 대해 고가용성을 달성하려면 여러 VPN Gateway를 배포하고 네트워크와 Azure 간에 여러 병렬 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="6b902-107">연결 옵션 및 토폴로지의 개요에 대해서는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="6b902-108">이 문서에서는 활성-활성 크로스-프레미스 VPN 연결 및 두 개의 가상 네트워크 간의 활성-활성 연결을 설정하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="6b902-109">1부 - 활성-활성 모드로 Azure VPN Gateway 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="6b902-110">2부 - 활성-활성 프레미스 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="6b902-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="6b902-111">3부 - 활성-활성 VNet 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="6b902-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="6b902-112">4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b902-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="6b902-113">이러한 요소를 결합하여 필요에 따라 더 복잡하고 가용성이 높은 네트워크 토폴로지를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-113">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b902-114">활성-활성 모드에서 다음 SKU만 사용하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-114">Please note that the active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="6b902-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="6b902-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="6b902-116">HighPerformance(이전 레거시 SKU)</span><span class="sxs-lookup"><span data-stu-id="6b902-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="6b902-117"><a name ="aagateway"></a>1부 - 활성-활성 VPN Gateway 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="6b902-118">다음 단계에서는 활성-활성 모드로 Azure VPN Gateway를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-118">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="6b902-119">활성-활성 및 활성-대기 게이트웨이 간의 주요 차이점:</span><span class="sxs-lookup"><span data-stu-id="6b902-119">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="6b902-120">두 개의 공용 IP 주소를 갖는 두 게이트웨이 IP 구성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-120">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="6b902-121">EnableActiveActiveFeature 플래그를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-121">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="6b902-122">게이트웨이 SKU는 VpnGw1, VpnGw2, VpnGw3 또는 HighPerformance(레거시 SKU)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-122">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="6b902-123">다른 속성은 비 활성-활성 게이트웨이와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-123">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="6b902-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6b902-124">Before you begin</span></span>
* <span data-ttu-id="6b902-125">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="6b902-126">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6b902-127">Azure 리소스 관리자 PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-127">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6b902-128">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 개요](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="6b902-129">1단계 - VNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="6b902-130">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="6b902-130">1. Declare your variables</span></span>
<span data-ttu-id="6b902-131">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="6b902-132">아래 예제에서는 이 연습에 대한 값을 사용하여 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-132">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="6b902-133">생산을 위해 구성하는 경우 값을 사용자의 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-133">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="6b902-134">이 구성 유형에 익숙해지기 위해 단계를 차례로 실행하는 경우 이 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-134">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="6b902-135">변수를 수정한 다음 복사하여 PowerShell 콘솔에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-135">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="6b902-136">2. 구독에 연결하고 새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-136">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="6b902-137">리소스 관리자 cmdlet을 사용하려면 PowerShell 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-137">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="6b902-138">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="6b902-139">PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-139">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="6b902-140">연결에 도움이 되도록 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-140">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="6b902-141">3. TestVNet1 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-141">3. Create TestVNet1</span></span>
<span data-ttu-id="6b902-142">아래 샘플은 TestVNet1이라는 가상 네트워크 및 GatewaySubnet, FrontEnd 및 Backend라는 서브넷 세 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-142">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="6b902-143">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="6b902-144">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="6b902-145">2단계 - 활성-활성 모드로 TestVNet1용 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-145">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="6b902-146">1. 공용 IP 주소 및 게이트웨이 IP 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-146">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="6b902-147">VNet용으로 만들 게이트웨이에 할당할 공용 IP 주소를 2개 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-147">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="6b902-148">필요한 서브넷 및 IP 구성도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-148">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="6b902-149">2. 활성-활성 구성으로 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-149">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="6b902-150">TestVNet1용 가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-150">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="6b902-151">GatewayIpConfig 항목이 두 개 있고 EnableActiveActiveFeature 플래그가 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-151">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="6b902-152">게이트웨이 만들기는 꽤 시간이 걸릴 수 있습니다(완료되려면 45분 이상).</span><span class="sxs-lookup"><span data-stu-id="6b902-152">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="6b902-153">3. 게이트웨이 공용 IP 주소 및 BGP 피어 IP 주소 획득</span><span class="sxs-lookup"><span data-stu-id="6b902-153">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="6b902-154">게이트웨이를 만든 후 Azure VPN 게이트웨이에서 BGP 피어 IP 주소를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-154">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="6b902-155">온-프레미스 VPN 장치에 대해 Azure VPN 게이트웨이를 BGP 피어로 구성하려면 이 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-155">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="6b902-156">다음 cmdlet을 사용하여 VPN Gateway에 할당된 두 개의 공용 IP 주소와 각 게이트웨이 인스턴스에 해당하는 BGP 피어 IP 주소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-156">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="6b902-157">게이트웨이 인스턴스에 대한 공용 IP 주소와 해당 BGP 피어링 주소의 순서는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-157">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="6b902-158">이 예제에서는 공용 IP가 40.112.190.5인 게이트웨이 VM은 BGP 피어링 주소로 10.12.255.4를 사용하고 138.91.156.129를 갖는 게이트웨이는 10.12.255.5를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-158">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="6b902-159">활성-활성 게이트웨이에 연결되는 온-프레미스 VPN 장치를 설정할 때 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-159">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="6b902-160">게이트웨이 및 모든 주소는 다음 다이어그램에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-160">The gateway is shown in the diagram below with all addresses:</span></span>

![활성-활성 게이트웨이](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="6b902-162">게이트웨이가 만들어지면 이 게이트웨이를 사용하여 활성-활성 프레미스 간 연결 또는 VNet 간 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-162">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="6b902-163">다음 섹션에서는 연습을 완료하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-163">The following sections will walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="6b902-164"><a name ="aacrossprem"></a>2부 - 활성-활성 프레미스 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="6b902-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="6b902-165">프레미스 간 연결을 설정하려면 온-프레미스 VPN 장치를 나타내는 로컬 네트워크 게이트웨이를 만들고 Azure VPN 게이트웨이와 로컬 네트워크 게이트웨이를 연결하는 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-165">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="6b902-166">이 예제에서 Azure VPN Gateway는 활성-활성 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-166">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="6b902-167">따라서 온-프레미스 VPN 장치(로컬 네트워크 게이트웨이)와 연결 리소스가 하나씩만 있더라도 Azure VPN Gateway 인스턴스는 온-프레미스 장치와의 S2S VPN 터널을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="6b902-168">계속하기 전에 이 연습의 [1부](#aagateway) 를 완료했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="6b902-169">1단계 - 로컬 네트워크 게이트웨이 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-169">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="6b902-170">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="6b902-170">1. Declare your variables</span></span>
<span data-ttu-id="6b902-171">이 연습에서는 다이어그램에 표시된 구성을 계속 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-171">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="6b902-172">값을 구성에 사용할 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-172">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="6b902-173">로컬 네트워크 게이트웨이 매개 변수와 관련하여 몇 가지 주의할 점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-173">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="6b902-174">로컬 네트워크 게이트웨이는 VPN 게이트웨이와 같거나 다른 위치 및 리소스 그룹에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-174">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="6b902-175">이 예제에서는 리소스 그룹은 다르지만 Azure 위치는 같은 게이트웨이를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-175">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="6b902-176">위와 같이 온-프레미스 VPN 장치가 하나뿐이면 BGP 프로토콜 사용 여부에 관계없이 활성-활성 연결이 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-176">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="6b902-177">이 예제에서는 프레미스 간 연결에 대해 BGP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-177">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="6b902-178">BGP가 사용되도록 설정되면 로컬 네트워크 게이트웨이에 대해 선언해야 하는 접두사는 VPN 장치의 BGP 피어 IP 주소의 호스트 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-178">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="6b902-179">이 경우에는 "10.52.255.253/32"의 접두사 /32입니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="6b902-180">다시 확인하면 온-프레미스 네트워크와 Azure VNet 간에는 서로 다른 BGP ASN을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="6b902-181">동일한 경우 온-프레미스 VPN 장치가 이미 다른 BGP 인접과의 피어에 ASN을 사용하고 있으면 VNet ASN을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-181">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="6b902-182">2. Site5용 로컬 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-182">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="6b902-183">계속하기 전에 여전히 구독 1에 연결되어 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="6b902-183">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="6b902-184">아직 만들지 않은 경우 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-184">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="6b902-185">2단계 - VNet 게이트웨이 및 로컬 네트워크 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="6b902-185">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="6b902-186">1. 두 게이트웨이 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b902-186">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="6b902-187">2. TestVNet1 및 Site5 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-187">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="6b902-188">이 단계에서는 "EnableBGP"를 $True로 설정하여 TestVNet1에서 Site5_1까지의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-188">In this step, you will create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="6b902-189">3. 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6b902-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="6b902-190">아래 예제에서 이 연습을 위해 온-프레미스 VPN 장치의 BGP 구성 섹션에 입력할 매개 변수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-190">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="6b902-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="6b902-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="6b902-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="6b902-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="6b902-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6b902-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="6b902-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="6b902-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="6b902-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="6b902-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span></span>
    - <span data-ttu-id="6b902-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="6b902-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span></span>
    - <span data-ttu-id="6b902-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="6b902-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span></span>
    - <span data-ttu-id="6b902-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span><span class="sxs-lookup"><span data-stu-id="6b902-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="6b902-199">몇 분 후 연결이 설정되어야 하며, IPsec 연결이 설정되면 BGP 피어링 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-199">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="6b902-200">지금까지 이 예제에서는 하나의 온-프레미스 VPN 장치만 구성했으며 그 결과는 아래 다이어그램과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-200">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="6b902-202">3단계 - 두 개의 온-프레미스 VPN 장치를 활성-활성 VPN Gateway에 연결</span><span class="sxs-lookup"><span data-stu-id="6b902-202">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="6b902-203">두 개의 VPN 장치가 동일한 온-프레미스 네트워크에 있는 경우 Azure VPN Gateway를 두 번째 VPN 장치에 연결하여 이중 중복성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-203">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="6b902-204">1. Site5용 두 번째 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-204">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="6b902-205">두 번째 로컬 네트워크 게이트웨이에 대한 게이트웨이 IP 주소, 주소 접두사 및 BGP 피어링 주소는 동일한 온-프레미스 네트워크에 대한 이전 로컬 네트워크 게이트웨이와 중복되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-205">Note that the gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="6b902-206">2. VNet 게이트웨이 및 두 번째 로컬 네트워크 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="6b902-206">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="6b902-207">"EnableBGP"를 $True로 설정하여 TestVNet1에서 Site5_2까지의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-207">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="6b902-208">3. 두 번째 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6b902-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="6b902-209">마찬가지로 아래에는 두 번째 VPN 장치에 입력하는 매개 변수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-209">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="6b902-210">연결(터널)이 설정되면 이중 중복 VPN 장치와 터널을 통해 온-프레미스 네트워크와 Azure가 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-210">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="6b902-212"><a name ="aav2v"></a>3부 - 활성-활성 VNet 간 연결 설정</span><span class="sxs-lookup"><span data-stu-id="6b902-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="6b902-213">이 섹션에서는 BGP를 사용하여 활성-활성 VNet 간 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="6b902-214">아래 지침은 위에 나열된 이전 단계에서 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-214">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="6b902-215">BGP를 사용하여 TestVNet1 및 VPN Gateway를 만들고 구성하려면 [1부](#aagateway) 를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-215">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="6b902-216">1단계 - TestVNet2 및 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-216">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="6b902-217">새 가상 네트워크 TestVNet2의 IP 주소 공간이 VNet 범위와 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-217">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="6b902-218">이 예제에서 가상 네트워크는 동일한 구독에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-218">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="6b902-219">다른 구독 간에 VNet 간 연결을 설정할 수 있습니다. 자세한 내용은 [VNet 간 연결 구성](vpn-gateway-vnet-vnet-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-219">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="6b902-220">BGP를 사용하는 연결을 만들 때 "-EnableBgp $True"를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-220">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="6b902-221">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="6b902-221">1. Declare your variables</span></span>
<span data-ttu-id="6b902-222">값을 구성에 사용할 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-222">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="6b902-223">2. 새 리소스 그룹에서 TestVNet2 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-223">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="6b902-224">3. TestVNet2에 대한 활성-활성 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-224">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="6b902-225">VNet용으로 만들 게이트웨이에 할당할 공용 IP 주소를 2개 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-225">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="6b902-226">필요한 서브넷 및 IP 구성도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-226">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="6b902-227">AS 번호 및 "EnableActiveActiveFeature" 플래그를 사용하여 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-227">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="6b902-228">Azure VPN 게이트웨이에서 기본 ASN을 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-228">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="6b902-229">BGP 및 전송 라우팅을 사용할 수 있도록 하려면 연결된 VNet용 ASN은 서로 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-229">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="6b902-230">2단계 - TestVNet1 및 TestVNet2 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="6b902-230">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="6b902-231">이 예제에서 두 게이트웨이는 동일한 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-231">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="6b902-232">동일한 PowerShell 세션에서 이 단계를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-232">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="6b902-233">1. 두 게이트웨이 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b902-233">1. Get both gateways</span></span>
<span data-ttu-id="6b902-234">로그인하고 구독 1에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-234">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="6b902-235">2. 두 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="6b902-235">2. Create both connections</span></span>
<span data-ttu-id="6b902-236">이 단계에서는 TestVNet1에서 TestVNet2까지 및 TestVNet2에서 TestVNet1까지의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-236">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="6b902-237">두 연결 모두에 대해 BGP를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-237">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="6b902-238">이러한 단계를 완료하면 몇 분 내에 연결이 설정됩니다. 또한 이중 중복성을 사용하여 VNet 간 연결이 완료되면 BGP 피어링 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-238">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="6b902-240"><a name ="aaupdate"></a>4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b902-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="6b902-241">마지막 섹션에서는 기존 Azure VPN Gateway를 활성-대기 모드에서 활성-활성 모드로 또는 그 반대로 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-241">The last section will describe how you can configure an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="6b902-242">이 섹션에는 이미 만든 VPN Gateway의 레거시 SKU(이전 SKU) 크기를 Standard에서 HighPerformance로 조정하기 위한 단계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-242">This section includes the steps to resize a legacy SKU (old SKU) of an already created VPN gateway from Standard to HighPerformance.</span></span> <span data-ttu-id="6b902-243">이러한 단계에서 이전 레거시 SKU는 새 SKU 중 하나로 업그레이드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-243">These steps do not upgrade an old legacy SKU to one of the new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-to-active-active-gateway"></a><span data-ttu-id="6b902-244">활성-대기 게이트웨이를 활성-활성 게이트웨이로 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-244">Configure an active-standby gateway to active-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="6b902-245">1. 게이트웨이 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6b902-245">1. Gateway parameters</span></span>
<span data-ttu-id="6b902-246">다음 예제에서는 활성-대기 게이트웨이를 활성-활성 게이트웨이로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-246">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="6b902-247">다른 공용 IP 주소를 만든 다음 두 번째 게이트웨이 IP 구성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-247">You need to create another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="6b902-248">사용되는 매개 변수를 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-248">Below shows the parameters used:</span></span>

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

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="6b902-249">2. 공용 IP 주소를 만든 다음 두 번째 게이트웨이 IP 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-249">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="6b902-250">3. 활성-활성 모드를 사용하도록 설정하고 게이트웨이 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b902-250">3. Enable active-active mode and update the gateway</span></span>
<span data-ttu-id="6b902-251">실제 업데이트를 트리거하도록 PowerShell에서 gateway 개체를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-251">You must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="6b902-252">또한 가상 네트워크 게이트웨이의 SKU가 이전에 Standard로 생성되었으므로 이를 HighPerformance로 변경(크기 조정)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-252">The SKU of the virtual network gateway must also be changed (resized) to HighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="6b902-253">이 업데이트에는 30-45분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-253">This update can take 30 to 45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-to-active-standby-gateway"></a><span data-ttu-id="6b902-254">활성-활성 게이트웨이를 활성-대기 게이트웨이로 구성</span><span class="sxs-lookup"><span data-stu-id="6b902-254">Configure an active-active gateway to active-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="6b902-255">1. 게이트웨이 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6b902-255">1. Gateway parameters</span></span>
<span data-ttu-id="6b902-256">위와 동일한 매개 변수를 사용하고 제거하려는 IP 구성의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-256">Use the same parameters as above, get the name of the IP configuration you want to remove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="6b902-257">2. 게이트웨이 IP 구성을 제거하고 활성-활성 모드를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="6b902-257">2. Remove the gateway IP configuration and disable the active-active mode</span></span>
<span data-ttu-id="6b902-258">마찬가지로 실제 업데이트를 트리거하도록 PowerShell에서 gateway 개체를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-258">Similarly, you must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="6b902-259">이 업데이트에는 30-45분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-259">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b902-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b902-260">Next steps</span></span>
<span data-ttu-id="6b902-261">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b902-261">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="6b902-262">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b902-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>