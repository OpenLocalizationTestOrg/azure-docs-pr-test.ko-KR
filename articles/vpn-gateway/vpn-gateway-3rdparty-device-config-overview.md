---
title: "aaaAbout 3rd 파티의 VPN 장치 구성 tooconnect tooAzure VPN 게이트웨이 | Microsoft Docs"
description: "이 문서에서는 tooAzure VPN 게이트웨이 연결 하기 위한 3rd 파티 VPN 장치 구성의 개요를 제공 합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="60c72-103">타사 VPN 장치 구성의 개요</span><span class="sxs-lookup"><span data-stu-id="60c72-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="60c72-104">이 문서에서는 tooAzure VPN 게이트웨이 연결 하기 위한 온-프레미스 VPN 장치 구성의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="60c72-105">hello 샘플 Azure 가상 네트워크 및 VPN 게이트웨이 프로그램에서 사용 되는 tooconnect toodifferent 온-프레미스 VPN 장치 hello로 동일한 매개 변수 수입니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="60c72-106">장치 요구 사항</span><span class="sxs-lookup"><span data-stu-id="60c72-106">Device requirements</span></span>
<span data-ttu-id="60c72-107">Azure VPN 게이트웨이는 표준 IPsec/IKE 프로토콜 도구 모음을 사용하여 S2S VPN 터널을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="60c72-108">너무 참조[에 대 한 VPN 장치](vpn-gateway-about-vpn-devices.md) hello에 대 한 자세한 IPsec/IKE 프로토콜 매개 변수 및 Azure VPN 게이트웨이에 대 한 기본 암호화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="60c72-109">에 설명 된 대로 암호화 알고리즘 및 키 길이 특정 연결에 대 한 정확한 조합 hello를 선택적으로 지정할 수 [암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="60c72-110"><a name ="singletunnel"></a>단일 VPN 터널</span><span class="sxs-lookup"><span data-stu-id="60c72-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="60c72-111">첫 번째 토폴로지 hello Azure VPN 게이트웨이와 온-프레미스 VPN 장치 간의 단일 S2S VPN 터널 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="60c72-112">필요에 따라 hello VPN 터널에서 BGP를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![단일 터널](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="60c72-114">너무 참조[사이트 간 연결을 구성](vpn-gateway-howto-site-to-site-resource-manager-portal.md) 한 자세한 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="60c72-115">hello 다음 섹션에서는 hello 매개 변수를 나열 하 고 시작 하는 데는 샘플 PowerShell 스크립트 toohelp를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="60c72-116">네트워크 및 VPN 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="60c72-116">Network and VPN gateway information</span></span>
<span data-ttu-id="60c72-117">이 섹션 위의 hello 예제에 대 한 hello 매개 변수를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="60c72-118">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="60c72-118">**Parameter**</span></span>                | <span data-ttu-id="60c72-119">**값**</span><span class="sxs-lookup"><span data-stu-id="60c72-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="60c72-120">VNet 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="60c72-120">VNet address prefixes</span></span>        | <span data-ttu-id="60c72-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60c72-121">10.11.0.0/16</span></span><br><span data-ttu-id="60c72-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60c72-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="60c72-123">Azure VPN 게이트웨이 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="60c72-124">Azure VPN 게이트웨이 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="60c72-125">온-프레미스 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="60c72-125">On-premises address prefixes</span></span> | <span data-ttu-id="60c72-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60c72-126">10.51.0.0/16</span></span><br><span data-ttu-id="60c72-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60c72-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="60c72-128">온-프레미스 VPN 장치 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="60c72-129">온-프레미스 VPN 장치 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="60c72-130">*VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="60c72-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="60c72-131">65010</span><span class="sxs-lookup"><span data-stu-id="60c72-131">65010</span></span>                        |
| <span data-ttu-id="60c72-132">*Azure BGP 피어 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="60c72-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="60c72-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="60c72-134">*온-프레미스 BGP ASN</span><span class="sxs-lookup"><span data-stu-id="60c72-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="60c72-135">65050</span><span class="sxs-lookup"><span data-stu-id="60c72-135">65050</span></span>                        |
| <span data-ttu-id="60c72-136">*온-프레미스 BGP 피어 IP</span><span class="sxs-lookup"><span data-stu-id="60c72-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="60c72-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="60c72-137">10.52.255.254</span></span>                |

* <span data-ttu-id="60c72-138">(*) BGP에만 해당하는 선택적 매개 변수</span><span class="sxs-lookup"><span data-stu-id="60c72-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="60c72-139">예제 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="60c72-139">Sample PowerShell script</span></span>
<span data-ttu-id="60c72-140">[PowerShell을 사용 하는 S2S VPN 연결 만들기](vpn-gateway-create-site-to-site-rm-powershell.md) 한 hello 자세한 지침.</span><span class="sxs-lookup"><span data-stu-id="60c72-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="60c72-141">이 섹션에서는 시작 하는 샘플 스크립트 tooget를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-141">This section provides a sample script tooget you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
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
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="60c72-142"><a name ="policybased"></a>[선택 사항] “UsePolicyBasedTrafficSelectors”로 사용자 지정 IPsec/IKE 정책 사용</span><span class="sxs-lookup"><span data-stu-id="60c72-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="60c72-143">VPN 장치 "any-에-any" 트래픽 선택기 (경로 기반/VTI-기반 구성)를 지원 하지 않는 경우 사용자 지정 IPsec/IKE 정책을 toocreate 필요 하 고에 설명 된 대로 "UsePolicyBasedTrafficSelectors" 옵션을 구성 합니다 [이 문서 ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="60c72-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60c72-144">Toocreate 순서 tooenable hello 연결에서 "UsePolicyBasedTrafficSelectors" 옵션에에서는 IPsec/IKE 정책이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="60c72-145">다음 샘플 스크립트 hello hello로 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="60c72-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="60c72-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="60c72-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="60c72-147">IPsec: AES256, SHA1, PFS24, SA 수명 7200초 및 20480000KB(20GB)</span><span class="sxs-lookup"><span data-stu-id="60c72-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="60c72-148">Hello 정책을 적용 하 고 "UesPolicyBasedTrafficSelectors" hello 연결에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="60c72-149"><a name ="bgp"></a>[선택 사항] S2S VPN 연결에 BGP 사용</span><span class="sxs-lookup"><span data-stu-id="60c72-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="60c72-150">필요에 따라 hello 연결에서 BGP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="60c72-151">참조 [VPN 게이트웨이용 BGP](vpn-gateway-bgp-resource-manager-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60c72-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="60c72-152">다음과 같은 두 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-152">There are two differences:</span></span>

<span data-ttu-id="60c72-153">hello 온-프레미스 주소 접두사는 단일 호스트 주소, hello 온-프레미스 BGP 피어 IP 주소가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="60c72-154">설정 해야 합니다 "-EnableBGP" hello 연결을 만들 때 $True 하는 너무:</span><span class="sxs-lookup"><span data-stu-id="60c72-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="60c72-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60c72-155">Next steps</span></span>
<span data-ttu-id="60c72-156">참조 [크로스-프레미스 및 VNet 대 VNet 연결에 대해 액티브-액티브 VPN 게이트웨이 구성](vpn-gateway-activeactive-rm-powershell.md) 단계 tooconfigure 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c72-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

