---
title: "S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 PowerShell을 사용하여 Azure VPN Gateway와의 S2S 또는 VNet 간 연결에 대한 IPsec/IKE 정책을 구성하는 방법을 안내합니다."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성

이 문서는 hello 단계 tooconfigure hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 사이트 간 VPN 또는 VNet 대 VNet 연결을 위한 IPsec/IKE 정책을 안내 합니다.

## <a name="about"></a>Azure VPN Gateway에 대한 IPsec 및 IKE 정책 매개 변수 정보
IPsec 및 IKE 프로토콜 표준은 다양하게 결합된 다양한 암호화 알고리즘을 지원합니다. 너무 참조[Azure VPN 게이트웨이 및 암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md) toosee이 도울 수 있는 방법 크로스-프레미스 및 VNet 대 VNet 연결을 확인 하면 규정 준수 또는 보안 요구 사항을 충족 합니다.

이 문서 toocreate 지침을 제공 하 고 IPsec/IKE 정책을 구성 하 고 tooa 기존 또는 새 연결을 적용:

* [1-워크플로 toocreate 부 및 IPsec/IKE 정책 설정](#workflow)
* [2부 - 지원되는 암호화 알고리즘 및 키 수준](#params)
* [3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기](#crossprem)
* [4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기](#vnet2vnet)
* [5부 - 연결에 대한 IPsec/IKE 정책 관리(만들기, 추가, 제거)](#managepolicy)

> [!IMPORTANT]
> 1. IPsec/IKE 정책 hello 게이트웨이 Sku를 다음에 작동 한다는 note:
>    * ***VpnGw1, VpnGw2, VpnGw3***(경로 기반)
>    * ***Standard*** 및 ***HighPerformance***(경로 기반)
> 2. 지정된 연결에 대해 ***하나의*** 정책 조합만 지정할 수 있습니다.
> 3. IKE(주 모드)와 IPsec(빠른 모드) 둘 다에 대한 모든 알고리즘 및 매개 변수를 지정해야 합니다. 부분 정책 지정은 허용되지 않습니다.
> 4. VPN 장치 공급 업체 사양을 tooensure hello 정책은 온-프레미스 VPN 장치 지원에 문의 하십시오. Hello 정책 호환 되지 않습니다 S2S 또는 VNet 대 VNet 연결을 설정할 수 없습니다.

## <a name ="workflow"></a>1-워크플로 toocreate 부 및 IPsec/IKE 정책 설정
이 섹션에서는 연결 S2S VPN 또는 VNet 대 VNet 연결 hello 워크플로 toocreate 및 update IPsec/IKE 정책 설명:
1. 가상 네트워크 및 VPN Gateway 만들기
2. 프레미스 간 연결에 대한 로컬 네트워크 게이트웨이 또는 VNet 간 연결에 대한 다른 가상 네트워크 및 게이트웨이 만들기
3. 선택한 알고리즘 및 매개 변수를 사용하여 IPsec/IKE 정책 만들기
4. Hello IPsec/IKE 정책을 사용 하 여 연결 (IPsec 또는 VNet2VNet) 만들기
5. 기존 연결에 대한 IPsec/IKE 정책 추가/업데이트/제거

이 문서의 지침 hello를 사용 하 여를 설정 하 고 hello 다이어그램에 나타난 대로 IPsec/IKE 정책을 구성할 수 있습니다.

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>2부 - 지원되는 암호화 알고리즘 및 키 수준

hello 다음 표에 지원 되는 hello 암호화 알고리즘 및 hello 고객에 의해 구성 가능한 키 길이:

| **IPsec/IKEv2**  | **옵션**    |
| ---  | --- 
| IKEv2 암호화 | AES256, AES192, AES128, DES3, DES  
| IKEv2 무결성  | SHA384, SHA256, SHA1, MD5  |
| DH 그룹         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, 없음 |
| IPsec 암호화 | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, 없음    |
| IPsec 무결성  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| PFS 그룹        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, 없음 
| QM SA 수명   | (**선택 사항**: 지정되지 않으면 기본값이 사용됨)<br>초(정수, **최소 300**/기본값 27,000초)<br>KB(정수, **최소 1,024**/기본값 102,400,000KB)   |
| 트래픽 선택기 | UsePolicyBasedTrafficSelectors** ($True/$False - **선택 사항**, 지정되지 않으면 기본값 $False)    |
|  |  |

> [!IMPORTANT]
> 1. **선택 해야 GCMAES IPsec 암호화 알고리즘의 경우와 사용 하는 경우 IPsec 무결성;에 대 한 동일한 GCMAES 알고리즘 및 키 길이 hello 예를 들어 GCMAES128 둘 다에 대해 사용 하 여**
> 2. Hello Azure VPN 게이트웨이 28, 800 초 IKEv2 주 모드 SA 수명 동안 고정 됩니다.
> 3. 설정 "UsePolicyBasedTrafficSelectors" $True 연결에는 구성 너무 hello Azure VPN 게이트웨이 tooconnect toopolicy 기반 VPN 방화벽 온-프레미스 합니다. VPN 장치에는 온-프레미스 네트워크 (로컬 네트워크 게이트웨이) 접두사 hello Azure 가상 네트워크 접두사를의 모든 조합으로 정의 된 hello 일치 하는 트래픽을 선택기 tooensure 필요한 PolicyBasedTrafficSelectors을 설정한 경우 대신 any-에-any입니다. 예를 들어 온-프레미스 네트워크 접두사는 10.1.0.0/16 및 10.2.0.0/16, 하는 경우 가상 네트워크 접두사는 192.168.0.0/16 및 172.16.0.0/16 트래픽 선택기 뒤 toospecify hello가 필요 합니다.
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.

다음 표에 hello hello hello 사용자 지정 정책에서 지 원하는 해당 Diffie-hellman 그룹:

| **Diffie-Hellman 그룹**  | **DHGroup**              | **PFSGroup** | **키 길이** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | 768비트 MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024비트 MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048비트 MODP  |
| 19                        | ECP256                   | ECP256       | 256비트 ECP    |
| 20                        | ECP384                   | ECP284       | 384비트 ECP    |
| 24                        | DHGroup24                | PFS24        | 2048비트 MODP  |

너무 참조[RFC3526](https://tools.ietf.org/html/rfc3526) 및 [RFC5114](https://tools.ietf.org/html/rfc5114) 내용을 확인 합니다.

## <a name ="crossprem"></a>3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기

이 섹션에서는 hello IPsec/IKE 정책과 S2S VPN 연결을 만드는 과정을 안내 합니다. hello 다음 단계를 만듭니다 hello 연결 hello 다이어그램에 나타난 대로:

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

S2S VPN 연결을 만드는 자세한 단계별 지침은 [S2S VPN 연결 만들기](vpn-gateway-create-site-to-site-rm-powershell.md)를 참조하세요.

### <a name="before"></a>시작하기 전에

* Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* Hello Azure 리소스 관리자 PowerShell cmdlet을 설치 합니다. 참조 [Azure PowerShell 개요](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.

### <a name="createvnet1"></a>1 단계-hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기

#### <a name="1-declare-your-variables"></a>1. 변수 선언

이 연습에서는 먼저 변수를 선언합니다. 프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다.

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour 구독을 연결 하 고 새 리소스 그룹 만들기

TooPowerShell 모드 toouse hello 리소스 관리자 cmdlet을 전환 하 고 있는지 확인 합니다. 자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 다음 샘플 toohelp 연결한 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기

다음 예제는 hello 세 개의 서브넷 및 hello VPN 게이트웨이 사용 하 여 TestVNet1, hello 가상 네트워크를 만듭니다. 값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다. 다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.

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

### <a name="s2sconnection"></a>2단계 - IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기

#### <a name="1-create-an-ipsecike-policy"></a>1. IPsec/IKE 정책 만들기

다음 샘플 스크립트는 hello hello로 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, SA 수명 7,200초 및 2,048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

사용 해야 GCMAES ipsec을 사용 하면 동일한 GCMAES 알고리즘 및 키 길이 IPsec 암호화와 무결성에 대 한 예를 들어 hello:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, SA 수명 7200초 및 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. IPsec/IKE 정책 hello로 hello S2S VPN 연결 만들기

S2S VPN 연결을 만들고 앞에서 만든 hello IPsec/IKE 정책을 적용 합니다.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

선택적으로 추가할 수 있습니다 "-UsePolicyBasedTrafficSelectors $True" toohello 연결 만듭니다 cmdlet tooenable Azure VPN 게이트웨이 tooconnect toopolicy 기반 VPN 장치와 온-프레미스로 위에서 설명한 것 처럼 합니다.

> [!IMPORTANT]
> 연결에 IPsec/IKE 정책을 지정 되 면 hello Azure VPN 게이트웨이 보내거나 지정 된 암호화 알고리즘 및 키 길이 특정 연결에 IPsec/IKE 제안 hello 수락 합니다. Hello 연결에 대 한 온-프레미스 VPN 장치를 사용 하거나 그렇지 않으면 hello S2S VPN 터널을 설정 하지 것입니다 hello 정확한 정책 조합을 받아들이는 있는지 확인 합니다.


## <a name ="vnet2vnet"></a>4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기

hello IPsec/IKE 정책을 사용 하 여 VNet 대 VNet 연결을 만드는 단계는 S2S VPN 연결의 유사한 toothat 합니다. hello 다음 예제 스크립트 만들기 hello 연결 hello 다이어그램에 나타난 대로:

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

VNet 간 연결을 만드는 자세한 단계는 [VNet 간 연결 만들기](vpn-gateway-vnet-vnet-rm-ps.md)를 참조하세요. 완료 해야 [3 부](#crossprem) toocreate TestVNet1를 구성 하 고 VPN 게이트웨이 hello 합니다.

### <a name="createvnet2"></a>1 단계-hello 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기

#### <a name="1-declare-your-variables"></a>1. 변수 선언

수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Hello 새 리소스 그룹에 hello 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>2 단계-IPsec/IKE 정책 hello로 VNet toVNet 연결 만들기

비슷한 toohello S2S VPN 연결을 IPsec/IKE 정책을 만든 다음 toopolicy toohello 새 연결을 적용 합니다.

#### <a name="1-create-an-ipsecike-policy"></a>1. IPsec/IKE 정책 만들기

다음 샘플 스크립트는 hello hello로 다른 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, SA 수명 7,200초 및 4,096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. IPsec/IKE 정책 hello VNet 대 VNet 연결을 만듭니다.

VNet 대 VNet 연결을 만들고 사용자가 만든 hello IPsec/IKE 정책을 적용 합니다. 이 예에서 두 게이트웨이 hello에는 동일한 구독 합니다. 가능한 toocreate 이며와 모두 연결을 구성 하도록 hello hello에 동일한 IPsec/IKE 정책을 같은 PowerShell 세션입니다.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> 연결에 IPsec/IKE 정책을 지정 되 면 hello Azure VPN 게이트웨이 보내거나 지정 된 암호화 알고리즘 및 키 길이 특정 연결에 IPsec/IKE 제안 hello 수락 합니다. 확인 한 다음 있는지 hello IPsec 정책을 모두 연결 된 hello 동일 하지만, 그렇지 않으면 VNet 대 VNet 연결을 설정 하지 것입니다.

다음이 단계를 완료 한 후 몇 분 안에 hello 연결이 설정 되 고 hello hello 시작 부분에 표시 된 대로 네트워크 토폴로지를 수행 해야 합니다.

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>5부 - 연결에 대한 IPsec/IKE 정책 업데이트

표시 하는 hello 마지막 섹션 toomanage 기존 S2S 또는 VNet 대 VNet 연결에 대 한 IPsec/IKE 정책입니다. 아래 hello 연습 hello 다음 연결에 대 한 작업을 안내 합니다.

1. 연결의 IPsec/IKE 정책 hello를 표시 합니다.
2. 추가 하거나 hello IPsec/IKE 정책 tooa 연결 업데이트
3. 연결에서 hello IPsec/IKE 정책 제거

hello 동일한 단계 적용 tooboth S2S 및 VNet 대 VNet 연결 됩니다.

> [!IMPORTANT]
> IPsec/IKE 정책은 *표준* 및 *고성능* 경로 기반 VPN 게이트웨이에서만 지원됩니다. Hello 기본 게이트웨이 SKU 또는 hello 정책 기반 VPN 게이트웨이 작동 하지 않습니다.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. 연결의 IPsec/IKE 정책 hello를 표시 합니다.

다음 예제는 hello tooget 연결에 구성 된 IPsec/IKE 정책 hello 하는 방법을 보여 줍니다. hello 스크립트는 또한 위의 hello 연습에서 진행합니다.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

마지막 명령은 hello 되어 hello 연결에 구성 된 hello 현재 IPsec/IKE 정책을 나열 합니다. 샘플 출력 다음 hello hello 연결입니다.

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

IPsec/IKE 정책 구성 안 됨 이면 hello 명령 (PS > $connection6.policy)는 빈 반환 가져옵니다. IPsec/IKE hello 연결에 구성 되어 있지 않습니다 이지만 사용자 지정 하는 IPsec/IKE 정책이 없는 있다는 것을 의미 하지 않습니다. hello 실제 연결은 온-프레미스 VPN 장치 및 hello Azure VPN 게이트웨이 간의 협상 hello 기본 정책이 사용 합니다.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. 연결에 대한 IPsec/IKE 정책 추가 또는 업데이트

hello 단계 tooadd 새 정책 또는 업데이트 한 연결에서 기존 정책을 사용 하면 동일한 hello: 새 정책을 만든 다음 hello 새 정책 toohello 연결을 적용 합니다.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable 때 tooan 연결 온-프레미스 정책 기반 VPN 장치를 "UsePolicyBasedTrafficSelectors" hello 추가 "-UsePolicyBaseTrafficSelectors" 매개 변수 toohello cmdlet 너무 설정 또는 $False toodisable hello 옵션:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Hello 연결을 가져올 수 있습니다 hello 정책이 업데이트 되는 경우 다시 toocheck 합니다.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

다음 예제는 hello와 같이 hello 마지막 줄의 hello 출력을 나타나야 합니다.

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. 연결에서 IPsec/IKE 정책 제거

Hello Azure VPN 게이트웨이 백 toohello 되돌립니다 연결에서 사용자 지정 정책 hello를 제거 하면 [기본 IPsec/IKE 제안 목록을](vpn-gateway-about-vpn-devices.md) 및 다시 온-프레미스 VPN 장치와 재협상 합니다.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

사용할 수 있습니다 hello 정책 hello 연결에서 제거 된 경우 동일한 스크립트 toocheck hello 합니다.

## <a name="next-steps"></a>다음 단계

정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.

연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.
