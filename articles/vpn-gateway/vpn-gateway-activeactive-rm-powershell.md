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
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Azure VPN Gateway와의 활성-활성 S2S VPN 연결 구성

이 문서에서는 hello 단계 toocreate 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 안내 합니다.

## <a name="about-highly-available-cross-premises-connections"></a>항상 사용 가능한 크로스-프레미스 연결 정보
고가용성 tooachieve 크로스-프레미스 및 VNet 대 VNet 연결을 위한 여러 VPN 게이트웨이 배포 및 네트워크와 Azure 간에 여러 병렬 연결을 설정 해야 합니다. 연결 옵션 및 토폴로지의 개요에 대해서는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md) 을 참조하세요.

이 문서에서는 hello 설명은 액티브-액티브를 tooset 크로스-프레미스 VPN 연결 및 두 개의 가상 네트워크 간에 활성-활성 연결:

* [1부 - 활성-활성 모드로 Azure VPN Gateway 만들기 및 구성](#aagateway)
* [2부 - 활성-활성 프레미스 간 연결 설정](#aacrossprem)
* [3부 - 활성-활성 VNet 간 연결 설정](#aav2v)
* [4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트](#aaupdate)

이러한 함께 toobuild 요구 사항을 충족 하는 보다 복잡 한, 항상 사용 가능한 네트워크 토폴로지를 결합할 수 있습니다.

> [!IMPORTANT]
> Hello 액티브-액티브 모드를 사용 하는 Sku를 수행 하는 유일한 hello를 사용 하 여 note 하십시오. 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance(이전 레거시 SKU)
> 
> 

## <a name ="aagateway"></a>1부 - 활성-활성 VPN Gateway 만들기 및 구성
단계를 수행 하는 hello 액티브-액티브 모드에서 Azure VPN 게이트웨이 구성 합니다. hello hello 액티브-액티브 및 활성-대기 게이트웨이 간의 주요 차이점:

* 두 개의 공용 IP 주소로 toocreate 두 게이트웨이 IP 구성을 사용 해야
* Hello EnableActiveActiveFeature 플래그를 설정 필요
* hello 게이트웨이 SKU VpnGw1, VpnGw2, VpnGw3, 또는 HighPerformance (레거시 SKU) 이어야 합니다.

hello 다른 속성은 hello hello 액티브-액티브 비 게이트웨이와 동일 합니다. 

### <a name="before-you-begin"></a>시작하기 전에
* Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* Tooinstall hello Azure 리소스 관리자 PowerShell cmdlet을 필요 합니다. 참조 [Azure PowerShell 개요](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.

### <a name="step-1---create-and-configure-vnet1"></a>1단계 - VNet1 만들기 및 구성
#### <a name="1-declare-your-variables"></a>1. 변수 선언
이 연습에서는 먼저 변수를 선언합니다. hello 감시할 hello 값을 사용 하 여이 연습에 대 한 hello 변수를 선언 합니다. 프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다. 이러한 유형의 구성에 잘 알고 hello 단계 toobecome를 통해 실행 하는 경우 이러한 변수를 사용할 수 있습니다. Hello 변수를 수정 복사 하 고 PowerShell 콘솔에 붙여 넣습니다.

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour 구독을 연결 하 고 새 리소스 그룹 만들기
TooPowerShell 모드 toouse hello 리소스 관리자 cmdlet을 전환 하 고 있는지 확인 합니다. 자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 다음 샘플 toohelp 연결한 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 만들기
아래 hello 샘플 TestVNet1 세 개의 서브넷, 하나의 호출된 GatewaySubnet, 하나의 호출된 프런트 엔드, 및 라는 하나의 호출된 백 엔드 가상 네트워크를 만듭니다. 값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다. 다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>2 단계-액티브-액티브 모드 TestVNet1에 대 한 hello VPN 게이트웨이 만들기
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Hello 공용 IP 주소 및 게이트웨이 IP 구성 만들기
두 요청 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 VNet을 만들게 됩니다. 또한 hello 서브넷 및 필요한 IP 구성을 정의 합니다.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. 활성-활성 구성으로 hello VPN 게이트웨이 만들기
TestVNet1에 대 한 hello 가상 네트워크 게이트웨이 만듭니다. Note GatewayIpConfig 항목이 두 및 hello EnableActiveActiveFeature 플래그가 설정 됩니다. 한 게이트웨이 만드는 시간이 오래 걸릴 수 있습니다 (45 분 또는 자세한 toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Hello 게이트웨이 공용 IP 주소 및 hello BGP 피어 IP 주소
Hello 게이트웨이 만든 후 Azure VPN 게이트웨이 hello에 tooobtain hello BGP 피어 IP 주소가 필요 합니다. 온-프레미스 VPN 장치에 대 한 BGP 피어도 필요한 tooconfigure hello Azure VPN 게이트웨이 주소가 없습니다.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

다음 cmdlet tooshow hello 두 개의 공용 IP 주소가 VPN 게이트웨이와 각 게이트웨이 인스턴스에 대 한 해당 BGP 피어 IP 주소에 할당 된 hello를 사용 합니다.

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

hello 게이트웨이 인스턴스 및 해당 BGP 피어 링 주소는 hello에 대 한 hello 공용 IP 주소의 hello 순서 hello 동일 합니다. 이 예제에서는 hello 게이트웨이 40.112.190.5의 공용 IP 사용 하 여 VM 10.12.255.4을 사용 하 여 BGP 피어 링 주소로,과 138.91.156.129 hello 게이트웨이 10.12.255.5를 사용 합니다. Toohello 액티브-액티브 게이트웨이 연결 하는 VPN 장치 온-프레미스를 설정할 때이 정보가 필요 합니다. hello 게이트웨이 아래의 모든 주소가 hello 다이어그램에 표시 됩니다.

![활성-활성 게이트웨이](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Hello 게이트웨이 만든 후에이 게이트웨이 tooestablish 액티브-액티브 크로스-프레미스 또는 VNet 대 VNet 연결을 사용할 수 있습니다. hello 다음 섹션에서는 hello 단계 toocomplete hello 연습 과정을 안내 합니다.

## <a name ="aacrossprem"></a>2부 - 활성-활성 프레미스 간 연결 설정
로컬 네트워크 게이트웨이 toorepresent toocreate 해야 tooestablish 크로스-프레미스 연결을 온-프레미스 VPN 장치 및 hello 로컬 네트워크 게이트웨이와 tooconnect hello Azure VPN 게이트웨이 연결 합니다. 이 예제에서는 hello Azure VPN 게이트웨이 액티브-액티브 모드입니다. 결과적으로,이 있어도 하나만 온-프레미스 VPN 장치 (로컬 네트워크 게이트웨이) 및 하나의 연결 리소스를 모두 Azure VPN 게이트웨이 인스턴스가 hello 온-프레미스 장치와 S2S VPN 터널을 설정 합니다.

계속하기 전에 이 연습의 [1부](#aagateway) 를 완료했는지 확인하세요.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>1 단계-만들고 hello 로컬 네트워크 게이트웨이 구성 합니다.
#### <a name="1-declare-your-variables"></a>1. 변수 선언
이 연습에는 hello 다이어그램에 표시 된 toobuild hello 구성을 계속 됩니다. 수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

몇 가지 작업 toonote hello 로컬 네트워크 게이트웨이 매개 변수 관련:

* 로컬 네트워크 게이트웨이 hello 동일 hello 또는 VPN 게이트웨이 hello와 그룹을 다른 위치 및 리소스 수 있습니다. 이 예제에서는 찍고 다른 리소스 그룹에만 hello에 동일한 Azure 위치입니다.
* 위에 나와 있는 것 처럼 온-프레미스 VPN 장치를 하나만 경우 BGP 프로토콜 유무 hello 액티브-액티브 연결이 작동 수 있습니다. 이 예제에서는 hello 크로스-프레미스 연결에 대 한 BGP를 사용 합니다.
* BGP가 사용 하는 경우 로컬 네트워크 게이트웨이 hello toodeclare 사용 해야 하는 hello 접두사는 hello 호스트 주소 VPN 장치에서 BGP 피어 IP 주소입니다. 이 경우에는 "10.52.255.253/32"의 접두사 /32입니다.
* 다시 확인하면 온-프레미스 네트워크와 Azure VNet 간에는 서로 다른 BGP ASN을 사용해야 합니다. 동일 hello는 이러한, 해야 toochange VNet ASN BGP 인접 항목과 다른 온-프레미스 VPN 장치 이미 사용 하 여 hello ASN toopeer 경우.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Site5에 대 한 hello 로컬 네트워크 게이트웨이 만들기
계속 하기 전에 연결된 되어 tooSubscription 1이 선택 되어 있는지 확인 하십시오. 아직 만들지 않은 경우 hello 리소스 그룹을 만듭니다.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>2 단계-hello VNet 게이트웨이 및 로컬 네트워크 게이트웨이 연결
#### <a name="1-get-hello-two-gateways"></a>1. Hello 두 게이트웨이 가져오기

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Hello TestVNet1 tooSite5 연결 만들기
이 단계에서는 hello 연결 만듭니다 TestVNet1 tooSite5_1에서 "EnableBGP" 너무 설정으로 $True입니다.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수
이 연습에 대 한 온-프레미스 VPN 장치에 hello BGP 구성 섹션에 입력 해야 하는 hello 매개 변수를 나열 하는 hello 감시할:

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - Tooannounce 접두사: 10.51.0.0/16 및 10.52.0.0/16 (예)
    - Azure VNet ASN       : 65010
    - Azure VNet BGP IP 1: 10.12.255.4 터널 too40.112.190.5에 대 한
    - Azure VNet BGP IP 2: 10.12.255.5 터널 too138.91.156.129에 대 한
    - 고정 경로: 대상 10.12.255.4/32, 다음 홉 hello VPN 터널 인터페이스 too40.112.190.5 대상 10.12.255.5/32, 다음 홉 hello VPN 터널 인터페이스 too138.91.156.129
    - eBGP 멀티 홉: eBGP은 필요한 경우 장치에서 사용할 hello "멀티 홉" 옵션 확인

hello 연결 하도록 hello IPsec 연결을 설정 하는 몇 분 및 hello BGP 피어 링 세션을 시작 합니다. 지금까지이 예에서는 아래의 그림과 hello에 하나의 온-프레미스 VPN 장치 구성에:

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>3 단계-연결할 두 개의 온-프레미스 VPN 장치 toohello 액티브-액티브 VPN 게이트웨이
Hello에 두 개의 VPN 장치를 보유 하는 경우 동일 온-프레미스 네트워크로 연결 hello Azure VPN 게이트웨이 toohello 두 번째 VPN 장치 여 이중 중복성을 구현할 수 있습니다.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Site5에 대 한 hello 두 번째 로컬 네트워크 게이트웨이 만들기
참고는 hello 게이트웨이 IP 주소, 주소 접두사 및 로컬 네트워크 게이트웨이 두 번째 hello에 대 한 BGP 피어 링 주소와 겹치면 안 hello에 대 한 이전 로컬 네트워크 게이트웨이 hello 동일한 온-프레미스 네트워크.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Hello VNet 게이트웨이 및 hello 두 번째 로컬 네트워크 게이트웨이 연결
TestVNet1 tooSite5_2 hello 연결 "EnableBGP" 너무 설정 만들기 $True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. 두 번째 온-프레미스 VPN 장치에 대한 VPN 및 BGP 매개 변수
마찬가지로, hello 매개 변수 목록 아래 입력할 예정 VPN 장치를 두 번째 hello:

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

Hello 연결 (터널), 설정 되 면 이중 중복 VPN 장치와 온-프레미스 네트워크 및 Azure에 연결 하는 터널 갖습니다.

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>3부 - 활성-활성 VNet 간 연결 설정
이 섹션에서는 BGP를 사용하여 활성-활성 VNet 간 연결을 만듭니다. 

아래 hello 지침 위에 나열 된 hello 이전 단계에서 계속 합니다. 완료 해야 [1 부](#aagateway) toocreate TestVNet1를 구성 하 고 hello VPN 게이트웨이 BGP 사용 합니다. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>1 단계-TestVNet2 및 hello VPN 게이트웨이 만들기
것이 중요 한 toomake hello 새 가상 네트워크를 TestVNet2의 hello IP 주소 공간 VNet 범위와 겹치지 않습니다.

이 예제에서는 가상 네트워크 hello 속해 toohello 동일한 구독 합니다. 다른 구독; 간에 VNet 대 VNet 연결을 설정할 수 있습니다. 너무를 참조 하십시오[VNet 대 VNet 연결 구성](vpn-gateway-vnet-vnet-rm-ps.md) toolearn 더 자세히 설명 합니다. Hello 추가 "-EnableBgp $True" 때 연결 tooenable BGP hello 만들기.

#### <a name="1-declare-your-variables"></a>1. 변수 선언
수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. TestVNet2 hello 새 리소스 그룹 만들기

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. TestVNet2에 대 한 hello 액티브-액티브 VPN 게이트웨이 만들기
두 요청 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 VNet을 만들게 됩니다. 또한 hello 서브넷 및 필요한 IP 구성을 정의 합니다.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

번호 및 hello "EnableActiveActiveFeature" 플래그로 hello로 hello VPN 게이트웨이 만듭니다. 참고 Azure VPN 게이트웨이 hello 기본 ASN를 재정의 해야 합니다. hello에 대 한 Asn hello Vnet 연결 된 다른 tooenable BGP 및 전송 라우팅과 이어야 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>2 단계-hello TestVNet1 및 TestVNet2 게이트웨이 연결
이 예에서 두 게이트웨이 hello에는 동일한 구독 합니다. Hello에이 단계를 완료 하려면 같은 PowerShell 세션입니다.

#### <a name="1-get-both-gateways"></a>1. 두 게이트웨이 가져오기
로그인 하 고 연결 tooSubscription 1에 있는지 확인 합니다.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. 두 연결 만들기
이 단계에서는 만들어집니다 TestVNet1 tooTestVNet2에서 hello 연결과 hello 연결 TestVNet2 tooTestVNet1에서.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> 두 연결에 대 한 있는지 tooenable BGP를 수 있습니다.
> 
> 

다음이 단계를 완료 한 후 hello 연결 잠시 후에 설정 됩니다 및 이중 중복 hello VNet 대 VNet 연결 완료 되 면 hello BGP 피어 링 세션을 됩니다.

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>4부 - 활성-활성 및 활성-대기 간에 기존 게이트웨이 업데이트
hello 마지막 섹션 기존 Azure VPN 게이트웨이 구성 하는 방법에 대해 설명 합니다 활성-대기 tooactive active 모드 또는 그 반대의 경우도 마찬가지입니다.

> [!NOTE]
> 이 섹션에는 표준 tooHighPerformance에서 이미 만들어진 VPN 게이트웨이의 hello 단계 tooresize 레거시 SKU (이전 SKU) 포함 되어 있습니다. 이러한 단계는 이전 레거시 SKU tooone의 hello 업그레이드 하지 않는 새 Sku입니다.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>활성-대기 게이트웨이 tooactive-활성 게이트웨이 구성
#### <a name="1-gateway-parameters"></a>1. 게이트웨이 매개 변수
다음 예제는 hello 액티브-액티브 게이트웨이 활성-대기 게이트웨이 변환 합니다. 다른 공용 IP 주소 toocreate 필요 다음 두 번째 게이트웨이 IP 구성을 추가 합니다. 다음 hello 매개 변수 사용.

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

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Hello 공용 IP 주소를 만든 다음 hello 두 번째 게이트웨이 IP 구성에 추가

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. 활성-활성 모드 및 업데이트 hello 게이트웨이 사용
PowerShell tootrigger hello 실제 업데이트에서 hello 게이트웨이 개체를 설정 해야 합니다. hello hello 가상 네트워크 게이트웨이 SKU 변경 해야 (크기가 조정 된) tooHighPerformance 표준으로 이전에 만든 이후로 합니다.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

이 업데이트에는 30 too45 분 걸릴 수 있습니다.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>액티브-액티브 게이트웨이 tooactive 대기 게이트웨이 구성
#### <a name="1-gateway-parameters"></a>1. 게이트웨이 매개 변수
사용 하 여 hello 동일 위와 같이 매개 변수 이름을 가져옵니다. hello hello IP 구성 tooremove 합니다.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Hello 게이트웨이 IP 구성을 제거 하 고 hello 액티브-액티브 모드 사용 안 함
마찬가지로, PowerShell tootrigger hello 실제 업데이트에서 hello 게이트웨이 개체를 설정 해야 합니다.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

이 업데이트를 too30 너무 45 분 정도 걸릴 수 있습니다.

## <a name="next-steps"></a>다음 단계
연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.
