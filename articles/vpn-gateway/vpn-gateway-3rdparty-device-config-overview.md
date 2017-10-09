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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>타사 VPN 장치 구성의 개요
이 문서에서는 tooAzure VPN 게이트웨이 연결 하기 위한 온-프레미스 VPN 장치 구성의 개요를 제공 합니다. hello 샘플 Azure 가상 네트워크 및 VPN 게이트웨이 프로그램에서 사용 되는 tooconnect toodifferent 온-프레미스 VPN 장치 hello로 동일한 매개 변수 수입니다.

## <a name="device-requirements"></a>장치 요구 사항
Azure VPN 게이트웨이는 표준 IPsec/IKE 프로토콜 도구 모음을 사용하여 S2S VPN 터널을 설정합니다. 너무 참조[에 대 한 VPN 장치](vpn-gateway-about-vpn-devices.md) hello에 대 한 자세한 IPsec/IKE 프로토콜 매개 변수 및 Azure VPN 게이트웨이에 대 한 기본 암호화 알고리즘입니다. 에 설명 된 대로 암호화 알고리즘 및 키 길이 특정 연결에 대 한 정확한 조합 hello를 선택적으로 지정할 수 [암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md)합니다.

## <a name ="singletunnel"></a>단일 VPN 터널
첫 번째 토폴로지 hello Azure VPN 게이트웨이와 온-프레미스 VPN 장치 간의 단일 S2S VPN 터널 구성 됩니다. 필요에 따라 hello VPN 터널에서 BGP를 구성할 수 있습니다.

![단일 터널](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

너무 참조[사이트 간 연결을 구성](vpn-gateway-howto-site-to-site-resource-manager-portal.md) 한 자세한 단계별 지침에 대 한 합니다. hello 다음 섹션에서는 hello 매개 변수를 나열 하 고 시작 하는 데는 샘플 PowerShell 스크립트 toohelp를 제공 합니다.

### <a name="network-and-vpn-gateway-information"></a>네트워크 및 VPN 게이트웨이 정보
이 섹션 위의 hello 예제에 대 한 hello 매개 변수를 나열 합니다.

| **매개 변수**                | **값**                    |
| ---                          | ---                          |
| VNet 주소 접두사        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN 게이트웨이 IP         | Azure VPN 게이트웨이 IP         |
| 온-프레미스 주소 접두사 | 10.51.0.0/16<br>10.52.0.0/16 |
| 온-프레미스 VPN 장치 IP    | 온-프레미스 VPN 장치 IP    |
| *VNet BGP ASN                | 65010                        |
| *Azure BGP 피어 IP           | 10.12.255.30                 |
| *온-프레미스 BGP ASN         | 65050                        |
| *온-프레미스 BGP 피어 IP     | 10.52.255.254                |

* (*) BGP에만 해당하는 선택적 매개 변수

### <a name="sample-powershell-script"></a>예제 PowerShell 스크립트
[PowerShell을 사용 하는 S2S VPN 연결 만들기](vpn-gateway-create-site-to-site-rm-powershell.md) 한 hello 자세한 지침. 이 섹션에서는 시작 하는 샘플 스크립트 tooget를 제공 합니다.

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

### <a name ="policybased"></a>[선택 사항] “UsePolicyBasedTrafficSelectors”로 사용자 지정 IPsec/IKE 정책 사용
VPN 장치 "any-에-any" 트래픽 선택기 (경로 기반/VTI-기반 구성)를 지원 하지 않는 경우 사용자 지정 IPsec/IKE 정책을 toocreate 필요 하 고에 설명 된 대로 "UsePolicyBasedTrafficSelectors" 옵션을 구성 합니다 [이 문서 ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Toocreate 순서 tooenable hello 연결에서 "UsePolicyBasedTrafficSelectors" 옵션에에서는 IPsec/IKE 정책이 필요합니다.

다음 샘플 스크립트 hello hello로 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, SA 수명 7200초 및 20480000KB(20GB)

Hello 정책을 적용 하 고 "UesPolicyBasedTrafficSelectors" hello 연결에서 사용 하도록 설정 합니다.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[선택 사항] S2S VPN 연결에 BGP 사용
필요에 따라 hello 연결에서 BGP를 사용할 수 있습니다. 참조 [VPN 게이트웨이용 BGP](vpn-gateway-bgp-resource-manager-ps.md)를 참조하세요. 다음과 같은 두 가지 차이점이 있습니다.

hello 온-프레미스 주소 접두사는 단일 호스트 주소, hello 온-프레미스 BGP 피어 IP 주소가 될 수 있습니다.

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

설정 해야 합니다 "-EnableBGP" hello 연결을 만들 때 $True 하는 너무:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>다음 단계
참조 [크로스-프레미스 및 VNet 대 VNet 연결에 대해 액티브-액티브 VPN 게이트웨이 구성](vpn-gateway-activeactive-rm-powershell.md) 단계 tooconfigure 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 합니다.

