---
title: "Azure VPN Gateway에서 BGP 구성: 리소스 관리자: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 PowerShell을 사용하여 Azure VPN Gateway와의 BGP 구성하는 방법을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>어떻게 tooconfigure BGP PowerShell을 사용 하 여 Azure VPN 게이트웨이
이 문서에서는 크로스-프레미스 사이트 및 사이트 간 (S2S) VPN 연결 및 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하는 VNet 대 VNet 연결에 hello 단계 tooenable BGP 안내 합니다.

## <a name="about-bgp"></a>BGP 정보
BGP는 hello 표준 라우팅 프로토콜 hello 인터넷 tooexchange 라우팅과 연결 가능성 정보 두 개 이상의 네트워크 사이에서 일반적으로 사용 합니다. BGP hello Azure VPN 게이트웨이 및 BGP 피어 또는 인접 한 항목을 호출 하 여 온-프레미스 VPN 장치, tooexchange "같은 경로"에서는 두 게이트웨이 hello 가용성을 하는 것에 대해 hello 게이트웨이 또는 라우터로 관련 된 통해 toogo 접두사입니다. BGP 경로 BGP 게이트웨이 한 BGP 피어 tooall에서 학습을 전파 하 여 여러 네트워크 간에 전송 라우팅과 활성화할 수도 다른 BGP 피어입니다.

참조 [Azure VPN 게이트웨이 사용한 BGP의 개요](vpn-gateway-bgp-overview.md) 에 대 한 자세한 설명은 이점에 BGP 및 toounderstand hello 기술 요구 사항 및 고려 사항이 BGP를 사용 하 여 합니다.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Azure VPN 게이트웨이에서 BGP 시작하기

이 문서는 hello 단계 toodo hello 다음 작업을 안내 합니다.

* [1부 - Azure VPN 게이트웨이에서 BGP 사용](#enablebgp)
* [2부 - BGP를 사용하여 프레미스 간 연결 설정](#crossprembgp)
* [3부 - BGP를 사용하여 VNet 간 연결 설정](#v2vbgp)

네트워크 연결에서 BGP를 사용 하기 위한 기본 구성 요소로 hello 지침의 각 부분을 형성 합니다. 세 부분을 모두 완료 하면 hello 다음 다이어그램에에서 표시 된 대로 hello 토폴로지 빌드:

![BGP 토폴로지](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

부분 함께 toobuild 요구 사항을 충족 하는 보다 복잡 한, 다중 홉 전송 네트워크를 결합할 수 있습니다.

## <a name ="enablebgp"></a>1 부-hello Azure VPN 게이트웨이에서 BGP를 구성 합니다.
hello 구성 단계를 설정 hello hello Azure VPN 게이트웨이의 BGP 매개 변수 hello 다음 다이어그램에에서 표시 된 대로:

![BGP 게이트웨이](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>시작하기 전에
* Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* Hello Azure 리소스 관리자 PowerShell cmdlet을 설치 합니다. Hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 

### <a name="step-1---create-and-configure-vnet1"></a>1단계 - VNet1 만들기 및 구성
#### <a name="1-declare-your-variables"></a>1. 변수 선언
이 연습에서는 먼저 변수를 선언합니다. hello 다음 예제에서는 변수를 선언 hello hello 값을 사용 하 여이 연습에 대 한 합니다. 프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다. 이러한 유형의 구성에 잘 알고 hello 단계 toobecome를 통해 실행 하는 경우 이러한 변수를 사용할 수 있습니다. Hello 변수를 수정 복사 하 고 PowerShell 콘솔에 붙여 넣습니다.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour 구독을 연결 하 고 새 리소스 그룹 만들기
toouse hello 리소스 관리자 cmdlet tooPowerShell 모드를 전환 해야 합니다. 자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 다음 샘플 toohelp 연결한 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 만들기
hello 다음 예제에서는 만듭니다 TestVNet1 세 개의 서브넷, 하나의 호출된 GatewaySubnet, 하나의 호출된 프런트 엔드, 및 라는 하나의 호출된 백 엔드 가상 네트워크입니다. 값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다. 다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>2 단계-TestVNet1에 대 한 BGP 매개 변수가 hello VPN 게이트웨이 만들기
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Hello IP 및 서브넷 구성 만들기
공용 IP 주소 toobe 할당 된 toohello 게이트웨이 만들려는 VNet에 대 한 요청 합니다. 또한 필요한 hello 서브넷과 IP 구성을 정의 합니다.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Hello로 hello VPN 게이트웨이 만들기 숫자로
TestVNet1에 대 한 hello 가상 네트워크 게이트웨이 만듭니다. BGP TestVNet1는 경로 기반 VPN 게이트웨이 및 hello 추가 매개 변수를-Asn, tooset hello ASN (AS 번호)가 필요합니다. Hello ASN 매개 변수를 설정 하지 않으면 ASN 65515 할당 됩니다. 한 게이트웨이 만드는 시간이 오래 걸릴 수 있습니다 (30 분 또는 자세한 toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Hello Azure BGP 피어 IP 주소 가져오기
Hello 게이트웨이 만든 후 Azure VPN 게이트웨이 hello에 tooobtain hello BGP 피어 IP 주소가 필요 합니다. 온-프레미스 VPN 장치에 대 한 BGP 피어도 필요한 tooconfigure hello Azure VPN 게이트웨이 주소가 없습니다.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

hello 마지막 명령은 hello Azure VPN 게이트웨이;에 해당 BGP 구성은 hello를 보여 줍니다. 예를 들어:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Hello 게이트웨이 만든 후 BGP를 사용이 tooestablish 크로스-프레미스 게이트웨이 연결 또는 VNet 대 VNet 연결을 사용할 수 있습니다. hello 다음 섹션에서는 안내 hello 단계 toocomplete hello 연습 합니다.

## <a name ="crossprembbgp"></a>2부 - BGP를 사용하여 프레미스 간 연결 설정

로컬 네트워크 게이트웨이 toorepresent toocreate 해야 tooestablish 크로스-프레미스 연결을 온-프레미스 VPN 장치 및 hello 로컬 네트워크 게이트웨이와 tooconnect hello VPN 게이트웨이 연결 합니다. 이러한 단계를 안내 하는 문서가 있을 때는이 문서 hello 추가 속성 필요한 toospecify hello BGP 구성 매개 변수를 포함 합니다.

![프레미스 간에 대한 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

계속하기 전에 이 연습의 [1부](#enablebgp)를 완료했는지 확인하세요.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>1 단계-만들고 hello 로컬 네트워크 게이트웨이 구성 합니다.

#### <a name="1-declare-your-variables"></a>1. 변수 선언

이 연습 계속 toobuild hello 구성을 hello 다이어그램에 표시 됩니다. 수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

몇 가지 작업 toonote hello 로컬 네트워크 게이트웨이 매개 변수 관련:

* 로컬 네트워크 게이트웨이 hello 동일 hello 또는 VPN 게이트웨이 hello와 그룹을 다른 위치 및 리소스 수 있습니다. 이 예제에서는 다른 위치의 다른 리소스 그룹에 표시됩니다.
* toodeclare hello 로컬 네트워크 게이트웨이에 대 한 필요한 hello 최소 접두사는 hello 호스트 주소를 VPN 장치에서 BGP 피어 IP 주소입니다. 이 경우에는 "10.52.255.254/32"의 접두사 /32입니다.
* 다시 확인하면 온-프레미스 네트워크와 Azure VNet 간에는 서로 다른 BGP ASN을 사용해야 합니다. 동일 hello는 이러한, 해야 toochange VNet ASN BGP 인접 항목과 다른 온-프레미스 VPN 장치 이미 사용 하 여 hello ASN toopeer 경우.

계속 하기 전에 연결된 되어 tooSubscription 1이 선택 되어 있는지 확인 합니다.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Site5에 대 한 hello 로컬 네트워크 게이트웨이 만들기

작성 되지 않은, hello 로컬 네트워크 게이트웨이 만들기 전에 경우 있는지 toocreate hello 리소스 그룹 수입니다. Hello 두 hello 로컬 네트워크 게이트웨이에 대 한 추가 매개 변수 확인: Asn과 BgpPeerAddress 합니다.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>2 단계-hello VNet 게이트웨이 및 로컬 네트워크 게이트웨이 연결

#### <a name="1-get-hello-two-gateways"></a>1. Hello 두 게이트웨이 가져오기

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Hello TestVNet1 tooSite5 연결 만들기

이 단계에서 TestVNet1 tooSite5 hello 연결을 만듭니다. 지정 해야 합니다 "-EnableBGP $True"이이 연결에 대 한 BGP tooenable 합니다. 앞에서 설명한 것 처럼 가능한 toohave BGP 및 비-BGP 연결 모두에 대 한 동일한 Azure VPN 게이트웨이에 hello 합니다. BGP를 사용 하 여 hello 연결 속성에서 하지 않으면 Azure가 사용 하지 않습니다 BGP이이 연결에 대 한 BGP 매개 변수는 두 게이트웨이에 이미 구성 된 경우에 합니다.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

hello 다음 예제에서는 hello 매개 변수를 나열이 연습에 대 한 온-프레미스 VPN 장치에서 hello BGP 구성 섹션에 입력 합니다.

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

IPsec 연결 hello 설정 되 면 몇 분 고 hello BGP 피어 링 세션 시작 된 후 hello 연결이 설정 됩니다.

## <a name ="v2vbgp"></a>3부 - BGP를 사용하여 VNet 간 연결 설정

이 섹션 hello 다음 다이어그램에에서 나와 있는 것 처럼 BGP와 VNet 대 VNet 연결을 추가 합니다.

![VNet-VNet에 대한 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

지침에 따라 hello hello 이전 단계에서 계속 합니다. 완료 해야 [1 부에서](#enablebgp) toocreate TestVNet1를 구성 하 고 hello VPN 게이트웨이 BGP 사용 합니다. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>1 단계-TestVNet2 및 hello VPN 게이트웨이 만들기

것이 중요 한 toomake hello 새 가상 네트워크를 TestVNet2의 hello IP 주소 공간 VNet 범위와 겹치지 않습니다.

이 예제에서는 가상 네트워크 hello 속해 toohello 동일한 구독 합니다. 다른 구독 간의 VNet 간 연결을 설정할 수 있습니다. 자세한 내용은 [VNet 간 연결 구성](vpn-gateway-vnet-vnet-rm-ps.md)을 참조하세요. Hello 추가 "-EnableBgp $True" 때 연결 tooenable BGP hello 만들기.

#### <a name="1-declare-your-variables"></a>1. 변수 선언

수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. TestVNet2에 대 한 BGP 매개 변수가 hello VPN 게이트웨이 만들기

공용 IP 주소 toobe 할당 된 toohello 게이트웨이 VNet에 대 한 만들고 필요한 hello 서브넷 및 IP 구성 정의 요청 합니다.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Hello로 hello VPN 게이트웨이 만들기 숫자로 합니다. Azure VPN 게이트웨이 hello 기본 ASN을 재정의 해야 합니다. hello에 대 한 Asn hello Vnet 연결 된 다른 tooenable BGP 및 전송 라우팅과 이어야 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

이 단계에서는 만들어야 TestVNet1 tooTestVNet2에서 hello 연결과 hello 연결 TestVNet2 tooTestVNet1에서.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> 두 연결에 대 한 있는지 tooenable BGP를 수 있습니다.
> 
> 

다음이 단계를 완료 한 후 몇 분 후 hello 연결이 설정 됩니다. hello BGP 피어 링 세션 제공 hello VNet 대 VNet 연결을 완료 됩니다.

이 작업의 세 부분이 모두 같기를 완료 한 경우 네트워크 토폴로지에 따라 hello 설정:

![VNet-VNet에 대한 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>다음 단계

연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.
