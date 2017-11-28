---
title: "여러 온-프레미스 정책 기반 VPN 장치에 Azure VPN Gateway 연결: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 PowerShell을 사용하여 여러 정책 기반 VPN 장치에 Azure 경로 기반 VPN Gateway를 구성하는 과정을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="f0963-103">PowerShell을 사용하여 여러 온-프레미스 정책 기반 VPN 장치에 Azure VPN Gateway 연결</span><span class="sxs-lookup"><span data-stu-id="f0963-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="f0963-104">이 문서에서는 S2S VPN 연결에서 사용자 지정 IPsec/IKE 정책을 활용하여 여러 온-프레미스 정책 기반 VPN 장치에 연결하도록 Azure 경로 기반 VPN Gateway를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="f0963-105">정책 기반 및 경로 기반 VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="f0963-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="f0963-106">정책 기반 *대* 경로 기반 VPN 장치는 연결에서 IPsec 트래픽 선택기가 설정되는 방식이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="f0963-107">**정책 기반** VPN 장치는 두 네트워크의 접두사 조합을 사용하여 트래픽이 IPsec 터널을 통해 암호화/암호 해독되는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="f0963-108">이는 일반적으로 패킷 필터링을 수행하는 방화벽 장치에 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="f0963-109">IPsec 터널 암호화 및 암호 해독이 패킷 필터링 및 처리 엔진에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="f0963-110">**경로 기반** VPN 장치는 임의(와일드 카드) 트래픽 선택기를 사용하며, 라우팅/전달 테이블이 서로 다른 IPsec 터널로 트래픽을 전달하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="f0963-111">이는 일반적으로 각 IPsec 터널이 네트워크 인터페이스 또는 VTI(가상 터널 인터페이스)로 모델링되는 라우터 플랫폼에 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="f0963-112">다음 다이어그램은 두 모델을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="f0963-113">정책 기반 VPN 예제</span><span class="sxs-lookup"><span data-stu-id="f0963-113">Policy-based VPN example</span></span>
![정책 기반](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="f0963-115">경로 기반 VPN 예제</span><span class="sxs-lookup"><span data-stu-id="f0963-115">Route-based VPN example</span></span>
![경로 기반](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="f0963-117">정책 기반 VPN에 대한 Azure 지원</span><span class="sxs-lookup"><span data-stu-id="f0963-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="f0963-118">현재 Azure에서는 VPN Gateway의 두 가지 모드(경로 기반 VPN Gateway 및 정책 기반 VPN Gateway)를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="f0963-119">이러한 게이트웨이는 서로 다른 플랫폼에 구축되므로 사양이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="f0963-120">**PolicyBased VPN Gateway**</span><span class="sxs-lookup"><span data-stu-id="f0963-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="f0963-121">**RouteBased VPN Gateway**</span><span class="sxs-lookup"><span data-stu-id="f0963-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="f0963-122">**Azure Gateway SKU**</span><span class="sxs-lookup"><span data-stu-id="f0963-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="f0963-123">Basic</span><span class="sxs-lookup"><span data-stu-id="f0963-123">Basic</span></span>                       | <span data-ttu-id="f0963-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="f0963-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="f0963-125">**IKE 버전**</span><span class="sxs-lookup"><span data-stu-id="f0963-125">**IKE version**</span></span>          | <span data-ttu-id="f0963-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="f0963-126">IKEv1</span></span>                       | <span data-ttu-id="f0963-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="f0963-127">IKEv2</span></span>                                    |
| <span data-ttu-id="f0963-128">**최대 S2S 연결**</span><span class="sxs-lookup"><span data-stu-id="f0963-128">**Max. S2S connections**</span></span> | <span data-ttu-id="f0963-129">**1**</span><span class="sxs-lookup"><span data-stu-id="f0963-129">**1**</span></span>                       | <span data-ttu-id="f0963-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="f0963-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="f0963-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="f0963-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="f0963-132">이제 사용자 지정 IPsec/IKE 정책을 사용하여 "**PolicyBasedTrafficSelectors**" 옵션과 함께 접두사 기반 트래픽 선택기를 사용하여 온-프레미스 정책 기반 VPN 장치에 연결하도록 Azure 경로 기반 VPN Gateway를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="f0963-133">이 기능을 사용하면 Azure Virtual Network 및 VPN Gateway에서 여러 온-프레미스 정책 기반 VPN/방화벽 장치에 연결할 수 있으므로 현재 Azure 정책 기반 VPN Gateway에서 단일 연결 제한이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="f0963-134">이 연결을 사용하려면 온-프레미스 정책 기반 VPN 장치가 Azure 경로 기반 VPN Gateway에 연결하도록 **IKEv2**를 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="f0963-135">VPN 장치 사양을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f0963-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="f0963-136">이 메커니즘을 사용하여 정책 기반 VPN 장치를 통해 연결되는 온-프레미스 네트워크는 Azure Virtual Network에 연결할 수 있습니다. **동일한 Azure VPN Gateway를 통해 다른 온-프레미스 네트워크 또는 가상 네트워크로 전송할 수는 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="f0963-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="f0963-137">구성 옵션은 사용자 지정 IPsec/IKE 연결 정책의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="f0963-138">정책 기반 트래픽 선택기 옵션을 사용하는 경우 전체 정책(IPsec/IKE 암호화 및 무결성 알고리즘, 키 수준 및 SA 수명)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="f0963-139">아래 다이어그램에서는 Azure VPN Gateway를 통한 전송 라우팅이 정책 기반 옵션에서 작동하지 않는 이유를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![정책 기반 전송](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="f0963-141">다이어그램에 나와 있는 것처럼 Azure VPN Gateway의 트래픽 선택기는 가상 네트워크에서 각각의 온-프레미스 네트워크 접두사로는 연결되지만 교차 연결 접두사로는 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="f0963-142">예를 들어 온-프레미스 사이트 2, 3 및 4는 각각 VNet1과 통신할 수 있지만 Azure VPN Gateway를 통해 서로 연결할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="f0963-143">다이어그램에서는 이 구성을 사용할 경우 Azure VPN Gateway에서 사용할 수 없는 상호 연결 트래픽 선택기를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="f0963-144">연결에서 정책 기반 트래픽 선택기 구성</span><span class="sxs-lookup"><span data-stu-id="f0963-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="f0963-145">이 문서의 지침은 [S2S 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)에 설명된 동일한 예제에 따라 S2S VPN 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="f0963-146">다음 다이어그램에 이러한 연결이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-146">This is shown in the following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="f0963-148">이 연결을 사용하도록 설정하는 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="f0963-149">크로스-프레미스 연결에 대한 가상 네트워크, VPN Gateway 및 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="f0963-150">IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="f0963-151">S2S 또는 VNet 간 연결을 만들 때 정책을 적용하고 연결에서 **정책 기반 트래픽 선택기를 사용하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="f0963-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="f0963-152">연결이 이미 생성된 경우 기존 연결에 정책을 적용하거나 업데이트할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f0963-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="f0963-153">연결에서 정책 기반 트래픽 선택기를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f0963-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="f0963-154">이 섹션에 대해 [IPsec/IKE 정책 구성 문서의 3부](vpn-gateway-ipsecikepolicy-rm-powershell.md)를 완료했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f0963-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="f0963-155">아래 예제에서는 동일한 매개 변수 및 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="f0963-156">1단계 - 가상 네트워크, VPN Gateway 및 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="f0963-157">1. 변수를 선언하고 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="f0963-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="f0963-158">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="f0963-159">생산을 위해 구성하는 경우 값을 사용자의 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-159">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="f0963-160">Resource Manager cmdlet을 사용하려면 PowerShell 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="f0963-161">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0963-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="f0963-162">PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="f0963-163">연결에 도움이 되도록 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="f0963-164">2. 가상 네트워크, VPN Gateway 및 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="f0963-165">아래 예제는 세 개의 서브넷과 VPN Gateway가 있는 가상 네트워크 TestVNet1을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="f0963-166">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 'GatewaySubnet'이라고 구체적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="f0963-167">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="f0963-168">2단계 - IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="f0963-169">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0963-170">연결에서 "UsePolicyBasedTrafficSelectors" 옵션을 사용하기 위해 IPsec/IKE 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="f0963-171">아래 예제에서는 다음 알고리즘 및 매개 변수를 사용하여 IPsec/IKE 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="f0963-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="f0963-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="f0963-173">IPsec: AES256, SHA256, PFS24, SA 수명 3600초 및 2,048KB</span><span class="sxs-lookup"><span data-stu-id="f0963-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="f0963-174">2. 정책 기반 트래픽 선택기 및 IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f0963-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="f0963-175">S2S VPN 연결을 만들고 이전 단계에서 만든 IPsec/IKE 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="f0963-176">연결에서 정책 기반 트래픽 선택기를 사용도록 설정하는 추가 매개 변수 "-UsePolicyBasedTrafficSelectors $True"가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="f0963-177">단계를 완료하면 S2S VPN 연결에서 정의된 IPsec/IKE 정책을 사용하며 연결에서 정책 기반 트래픽 선택기를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="f0963-178">동일한 단계를 반복하여 동일한 Azure VPN Gateway에서 추가 온-프레미스 정책 기반 VPN 장치에 연결을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="f0963-179">연결에 대한 정책 기반 트래픽 선택기 업데이트</span><span class="sxs-lookup"><span data-stu-id="f0963-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="f0963-180">마지막 섹션에서는 기존 S2S VPN 연결에 대한 정책 기반 트래픽 선택기 옵션을 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="f0963-181">1. 연결 가져오기</span><span class="sxs-lookup"><span data-stu-id="f0963-181">1. Get the connection</span></span>
<span data-ttu-id="f0963-182">연결 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="f0963-183">2. 정책 기반 트래픽 선택기 옵션 확인</span><span class="sxs-lookup"><span data-stu-id="f0963-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="f0963-184">다음 줄은 정책 기반 트래픽 선택기가 연결에 사용되는지 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="f0963-185">이 줄에서 "**True**"가 반환되면 연결에 정책 기반 트래픽 선택기가 구성되어 있는 것이고, 그렇지 않으면 "**False**"가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="f0963-186">3. 연결에서 정책 기반 트래픽 선택기 업데이트</span><span class="sxs-lookup"><span data-stu-id="f0963-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="f0963-187">연결 리소스를 가져온 후에는 옵션을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="f0963-188">UsePolicyBasedTrafficSelectors 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="f0963-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="f0963-189">아래 예제에서는 IPsec/IKE 정책을 변경되지 않은 상태로 두고 정책 기반 트래픽 선택기 옵션을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="f0963-190">UsePolicyBasedTrafficSelectors 사용</span><span class="sxs-lookup"><span data-stu-id="f0963-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="f0963-191">아래 예제에서는 IPsec/IKE 정책을 변경되지 않은 상태로 두고 정책 기반 트래픽 선택기 옵션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="f0963-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0963-192">Next steps</span></span>
<span data-ttu-id="f0963-193">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0963-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="f0963-194">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0963-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="f0963-195">사용자 지정 IPsec/IKE 정책에 대한 자세한 내용은 [S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0963-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
