---
title: "Azure VPN 게이트웨이 toomultiple 온-프레미스 정책 기반 VPN 장치 연결: Azure 리소스 관리자: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure 경로 기반 VPN 게이트웨이 toomultiple 정책 기반 VPN 장치 Azure 리소스 관리자 및 PowerShell을 사용 하 여 구성 하는 과정을 안내 합니다."
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
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="25434-103">Azure VPN 게이트웨이 toomultiple 온-프레미스 정책 기반 VPN 장치 PowerShell을 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="25434-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="25434-104">이 문서는 Azure 경로 기반 VPN 게이트웨이 tooconnect toomultiple 온-프레미스 정책 기반 VPN 장치 S2S VPN 연결에 IPsec/IKE 정책을 사용자 지정을 활용 하 여 구성 하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="25434-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="25434-105">정책 기반 및 경로 기반 VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="25434-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="25434-106">정책- *비교* 경로 기반 VPN 장치 hello IPsec 트래픽 선택기 연결에 설정 된 방식에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="25434-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="25434-107">**정책 기반** VPN 장치에서 어떻게 트래픽이 암호화/암호 해독 되 IPsec 터널을 통해 두 네트워크 toodefine 접두사의 hello 조합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="25434-108">이는 일반적으로 패킷 필터링을 수행하는 방화벽 장치에 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="25434-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="25434-109">IPsec 터널 암호화 및 암호 해독 toohello 패킷 필터링과 처리 엔진 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25434-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="25434-110">**경로 기반** any-에-any (와일드 카드) 트래픽 선택기를 사용 하는 VPN 장치 및 테이블 트래픽을 직접 toodifferent IPsec 터널을 let 라우팅/전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="25434-111">이는 일반적으로 각 IPsec 터널이 네트워크 인터페이스 또는 VTI(가상 터널 인터페이스)로 모델링되는 라우터 플랫폼에 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="25434-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="25434-112">hello 다음 다이어그램 강조 hello 두 모델:</span><span class="sxs-lookup"><span data-stu-id="25434-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="25434-113">정책 기반 VPN 예제</span><span class="sxs-lookup"><span data-stu-id="25434-113">Policy-based VPN example</span></span>
![정책 기반](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="25434-115">경로 기반 VPN 예제</span><span class="sxs-lookup"><span data-stu-id="25434-115">Route-based VPN example</span></span>
![경로 기반](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="25434-117">정책 기반 VPN에 대한 Azure 지원</span><span class="sxs-lookup"><span data-stu-id="25434-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="25434-118">현재 Azure에서는 VPN Gateway의 두 가지 모드(경로 기반 VPN Gateway 및 정책 기반 VPN Gateway)를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="25434-119">이러한 게이트웨이는 서로 다른 플랫폼에 구축되므로 사양이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="25434-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="25434-120">**PolicyBased VPN Gateway**</span><span class="sxs-lookup"><span data-stu-id="25434-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="25434-121">**RouteBased VPN Gateway**</span><span class="sxs-lookup"><span data-stu-id="25434-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="25434-122">**Azure Gateway SKU**</span><span class="sxs-lookup"><span data-stu-id="25434-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="25434-123">Basic</span><span class="sxs-lookup"><span data-stu-id="25434-123">Basic</span></span>                       | <span data-ttu-id="25434-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="25434-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="25434-125">**IKE 버전**</span><span class="sxs-lookup"><span data-stu-id="25434-125">**IKE version**</span></span>          | <span data-ttu-id="25434-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="25434-126">IKEv1</span></span>                       | <span data-ttu-id="25434-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="25434-127">IKEv2</span></span>                                    |
| <span data-ttu-id="25434-128">**최대 S2S 연결**</span><span class="sxs-lookup"><span data-stu-id="25434-128">**Max. S2S connections**</span></span> | <span data-ttu-id="25434-129">**1**</span><span class="sxs-lookup"><span data-stu-id="25434-129">**1**</span></span>                       | <span data-ttu-id="25434-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="25434-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="25434-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="25434-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="25434-132">사용자 지정 IPsec/IKE 정책 hello Azure 경로 기반 VPN 게이트웨이 toouse 접두사 기반 트래픽 선택기 옵션으로 구성할 수 있습니다 "**PolicyBasedTrafficSelectors**", tooconnect tooon 온-프레미스 정책 기반 VPN 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="25434-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="25434-133">이 기능을 통해 Azure 가상 네트워크에서 tooconnect 있습니다 및 VPN 게이트웨이 toomultiple 온-프레미스 hello 현재 Azure 정책 기반 VPN 게이트웨이에서 hello 단일 연결 제한을 제거 하는 정책 기반 VPN/방화벽 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="25434-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="25434-134">tooenable 온-프레미스 정책 기반 VPN 장치를 지원 해야이 연결 **IKEv2** tooconnect toohello Azure VPN 게이트웨이 경로 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="25434-135">VPN 장치 사양을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="25434-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="25434-136">정책 기반 VPN 장치를 통해 연결 하 여이 메커니즘 hello 온-프레미스 네트워크에는 Azure 가상 네트워크; toohello만 연결할 수 있습니다. **tooother 온-프레미스 네트워크를 전환 없습니다 또는 가상 네트워크를 통해 동일한 Azure VPN 게이트웨이 환영**합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="25434-137">hello 구성 옵션에는 사용자 지정 IPsec/IKE 연결 정책 hello의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="25434-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="25434-138">Hello 정책 기반 트래픽 선택기 옵션을 설정한 경우 hello 완성 된 정책 (IPsec/IKE 암호화 및 무결성 알고리즘, 키 길이 및 SA 수명)을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="25434-139">다음 다이어그램 hello hello 정책 기반 옵션으로 Azure VPN 게이트웨이 통해 전송 라우팅과 작동 하지 않는 이유를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25434-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![정책 기반 전송](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="25434-141">Hello 다이어그램에 표시 된 것과 같이 hello Azure VPN 게이트웨이 hello 온-프레미스 네트워크 접두사 하지만 하지 hello 상호 연결 접두사의 가상 네트워크 tooeach hello에서에서 트래픽 선택기는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="25434-142">예를 들어, 온-프레미스 사이트 2, 3, 사이트 및 사이트 4 통신할 수 있습니다 각 tooVNet1 각각 있지만 hello Azure VPN 게이트웨이 tooeach 다른를 통해 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="25434-143">hello 다이어그램 hello를 보여 줍니다.이 구성에서 Azure VPN 게이트웨이 hello에 사용할 수 없는 트래픽 선택기 교차 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="25434-144">연결에서 정책 기반 트래픽 선택기 구성</span><span class="sxs-lookup"><span data-stu-id="25434-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="25434-145">hello 지침에 따라가 문서에 hello 동일 예제에 설명 된 대로 [S2S 또는 VNet 대 VNet 연결에 대 한 IPsec/IKE 구성 정책을](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish S2S VPN 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="25434-146">이 hello 다음 다이어그램에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25434-146">This is shown in hello following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="25434-148">워크플로 tooenable이이 연결을 hello:</span><span class="sxs-lookup"><span data-stu-id="25434-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="25434-149">Hello 가상 네트워크, VPN 게이트웨이 및 크로스-프레미스 연결에 대 한 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="25434-150">IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="25434-151">S2S 또는 VNet 대 VNet 연결을 만들 때 hello 정책을 적용 하 고 **hello 정책 기반 트래픽 선택기를 사용 하도록 설정** hello 연결에서</span><span class="sxs-lookup"><span data-stu-id="25434-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="25434-152">Hello 연결을 이미 만든 경우에 적용 하거나 hello 정책 tooan 기존 연결을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="25434-153">연결에서 정책 기반 트래픽 선택기를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="25434-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="25434-154">완료 했는지 확인 [hello IPsec/IKE 구성 정책 문서의 3 부](vpn-gateway-ipsecikepolicy-rm-powershell.md) 이 섹션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="25434-155">다음 예제에서는 hello 동일한 매개 변수 및 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="25434-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="25434-156">1 단계-hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="25434-157">1. 변수를 선언 및 tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="25434-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="25434-158">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="25434-159">프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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
<span data-ttu-id="25434-160">toouse hello 리소스 관리자 cmdlet tooPowerShell 모드를 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="25434-161">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25434-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="25434-162">PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="25434-163">다음 샘플 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="25434-164">2. Hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="25434-165">다음 예제는 hello TestVNet1 세 개의 서브넷 및 hello VPN 게이트웨이 사용 하 여 hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25434-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="25434-166">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 'GatewaySubnet'이라고 구체적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="25434-167">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="25434-168">2단계 - IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="25434-169">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25434-170">Toocreate 순서 tooenable hello 연결에서 "UsePolicyBasedTrafficSelectors" 옵션에에서는 IPsec/IKE 정책이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="25434-171">hello 다음 예제는 IPsec/IKE가 있는 정책을 만들고 이러한 알고리즘 및 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="25434-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="25434-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="25434-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="25434-173">IPsec: AES256, SHA256, PFS24, SA 수명 3600초 및 2,048KB</span><span class="sxs-lookup"><span data-stu-id="25434-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="25434-174">2. 정책 기반 트래픽 선택기 및 IPsec/IKE 정책 hello S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="25434-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="25434-175">S2S VPN 연결을 만들고 hello 이전 단계에서 만든 hello IPsec/IKE 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="25434-176">Hello 추가 매개 변수를 알고 있어야 "-UsePolicyBasedTrafficSelectors $True" hello 연결에서 정책 기반 트래픽 선택기 할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="25434-177">Hello 단계를 완료 한 후 hello S2S VPN 연결 hello IPsec/IKE 정책이 정의 사용 되 고 hello 연결에서 정책 기반 트래픽 선택기를 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25434-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="25434-178">더 많은 연결 tooadditional 온-프레미스 정책 기반 VPN 장치에서 tooadd 단계 동일 hello를 반복할 수 동일한 Azure VPN 게이트웨이에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="25434-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="25434-179">연결에 대한 정책 기반 트래픽 선택기 업데이트</span><span class="sxs-lookup"><span data-stu-id="25434-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="25434-180">hello 마지막 섹션에서는 기존 S2S VPN 연결에 대 한 tooupdate hello 정책 기반 트래픽 선택기 옵션 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25434-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="25434-181">1. Hello 연결 가져오기</span><span class="sxs-lookup"><span data-stu-id="25434-181">1. Get hello connection</span></span>
<span data-ttu-id="25434-182">Hello 연결 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="25434-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="25434-183">2. Hello 정책 기반 트래픽 선택기 옵션 확인</span><span class="sxs-lookup"><span data-stu-id="25434-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="25434-184">hello에 다음 줄은 hello 정책 기반 트래픽 선택기 hello 연결에 대 한 사용 되는지 여부를</span><span class="sxs-lookup"><span data-stu-id="25434-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="25434-185">Hello 줄을 반환 하는 경우 "**True**", 그렇지 않으면 반환; 정책 기반 트래픽 선택기는 hello 연결에 구성 된 다음 "**False**."</span><span class="sxs-lookup"><span data-stu-id="25434-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="25434-186">3. Hello 정책 기반 트래픽 선택기에 대 한 연결 업데이트</span><span class="sxs-lookup"><span data-stu-id="25434-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="25434-187">Hello 연결 리소스를 가져오고 나면 사용 하도록 설정 하거나 hello 옵션을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="25434-188">UsePolicyBasedTrafficSelectors 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="25434-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="25434-189">hello 다음 예제에서는 비활성화 hello 정책 기반 트래픽 선택기 옵션 하지만 leaves hello 변경 하지 않고 IPsec/IKE 정책:</span><span class="sxs-lookup"><span data-stu-id="25434-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="25434-190">UsePolicyBasedTrafficSelectors 사용</span><span class="sxs-lookup"><span data-stu-id="25434-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="25434-191">hello 다음 예에서는 hello 정책 기반 트래픽 선택기 옵션 하지만 leaves hello 변경 하지 않고 IPsec/IKE 정책:</span><span class="sxs-lookup"><span data-stu-id="25434-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="25434-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25434-192">Next steps</span></span>
<span data-ttu-id="25434-193">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25434-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="25434-194">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25434-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="25434-195">사용자 지정 IPsec/IKE 정책에 대한 자세한 내용은 [S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25434-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
