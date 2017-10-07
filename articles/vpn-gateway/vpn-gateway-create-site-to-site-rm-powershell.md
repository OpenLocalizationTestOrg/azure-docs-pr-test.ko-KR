---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN: PowerShell | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 이 단계는 PowerShell을 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>PowerShell을 사용하여 사이트 간 VPN 연결로 VNet 만들기

이 문서 toouse 온-프레미스에서 PowerShell toocreate 사이트-사이트 VPN 게이트웨이 연결 toohello VNet 네트워크 하는 방법을 보여 줍니다. 이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [클래식 포털(클래식)](vpn-gateway-site-to-site-create.md)
> 
>


사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다. 이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다. VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>시작하기 전에

Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.

* 호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다. 호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.
* VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다. 이 IP 주소는 NAT 뒤에 배치할 수 없습니다.
* 온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다. 이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다. 온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다.
* Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다. PowerShell cmdlet은 자주 업데이트 되 고는 일반적으로 tooupdate 프로그램 PowerShell cmdlet tooget hello 최신 기능 기능 합니다. PowerShell cmdlet을 업데이트 하지 않으면 지정 된 hello 값 실패할 수 있습니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 다운로드 하 고 PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.

### <a name="example"></a>예제 값

이 문서의 hello 예제는 다음 값에는 hello를 사용 합니다. 이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Tooyour 구독 연결

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. 가상 네트워크 및 게이트웨이 서브넷 만들기

가상 네트워크가 아직 없는 경우 만듭니다. 가상 네트워크를 만들 때 지정한 hello 주소 공간 온-프레미스 네트워크에가지고 있는 hello 주소 공간 중 하나라도 겹치지 않는지 확인 합니다.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate 가상 네트워크 및 게이트웨이 서브넷

이 예제에서는 가상 네트워크 및 게이트웨이 서브넷을 만듭니다. Tooadd 게이트웨이 서브넷을 참조 해야 하는 가상 네트워크를 이미 있는 경우 [tooadd 게이트웨이 서브넷 tooa 가상 네트워크를 이미 만든](#gatewaysubnet)합니다.

리소스 그룹 만들기:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

가상 네트워크를 만듭니다.

1. Hello 변수를 설정 합니다.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Hello VNet을 만듭니다.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>이미 만든 tooadd 게이트웨이 서브넷 tooa 가상 네트워크

1. Hello 변수를 설정 합니다.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Hello 게이트웨이 서브넷을 만듭니다.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Hello 구성을 설정 합니다.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Hello 로컬 네트워크 게이트웨이 만들기

일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다. Hello 사이트 기준인 Azure 수 tooit를 참조 하십시오. 그런 다음 hello IP 주소를 지정 된 이름을 지정 hello 온-프레미스 VPN 장치 toowhich의 연결을 만듭니다. 또한 hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 접두사를 지정 합니다. 지정 하는 hello 주소 접두사는 온-프레미스 네트워크에 있는 hello 접두사입니다. 온-프레미스 네트워크 변경 되 면 hello 접두사를 쉽게 업데이트할 수 있습니다.

다음 값에는 hello를 사용 합니다.

* hello *GatewayIPAddress* 온-프레미스 VPN 장치의 hello IP 주소입니다. VPN 장치는 NAT 뒤에 배치할 수 없습니다.
* hello *AddressPrefix* 은 온-프레미스 주소 공간입니다.

tooadd 단일 주소 접두사와 로컬 네트워크 게이트웨이:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

여러 개의 주소 접두사와 로컬 네트워크 게이트웨이 tooadd:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

로컬 네트워크 게이트웨이에 대 한 IP 주소 접두사 toomodify:<br>
경우에 따라 로컬 네트워크 게이트웨이 접두사를 변경합니다. hello 단계를 수행한 toomodify 사용자의 IP 주소 접두사는 VPN 게이트웨이 연결을 만들었는지 여부에 따라 달라 집니다. Hello 참조 [로컬 네트워크 게이트웨이에 대 한 수정 IP 주소 접두사](#modify) 이 문서의 섹션.

## <a name="PublicIP"></a>4. 공용 IP 주소 요청

VPN Gateway에는 공용 IP 주소가 있어야 합니다. 먼저 hello IP 주소 리소스를 요청 하 고 가상 네트워크 게이트웨이 만들 때 tooit를 참조 하십시오. hello IP 주소를 사용 hello VPN 게이트웨이 만들 때 toohello 리소스를 동적으로 할당 됩니다. 현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다. 고정 공용 IP 주소 할당을 요청할 수 없습니다. 그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에이 아닙니다. hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다. VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.

Tooyour 가상 네트워크 VPN 게이트웨이 할당할 수 있는 공용 IP 주소를 요청 합니다.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Hello 게이트웨이 IP 주소 지정 구성을 만들기

hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다. 다음 예제에서는 toocreate hello 게이트웨이 구성을 사용 합니다.

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Hello VPN 게이트웨이 만들기

Hello 가상 네트워크 VPN 게이트웨이 만듭니다. VPN 게이트웨이 만들기 too45 분 또는 toocomplete 자세한 정도 걸릴 수 있습니다.

다음 값에는 hello를 사용 합니다.

* hello *-GatewayType* 사이트-사이트에 대 한 구성은 *Vpn*합니다. hello 게이트웨이 형식은 항상 구현 하는 특정 toohello 구성입니다. 예를 들어 다른 게이트웨이 구성인 GatewayType ExpressRoute가 필요할 수 있습니다.
* hello *-VpnType* 수 *RouteBased* (일부 설명서에서는 동적 게이트웨이 tooas 함) 또는 *PolicyBased* (tooas 일부 설명서에서는 정적 게이트웨이 참조 합니다. ). VPN Gateway 형식에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.
* Hello toouse 게이트웨이 SKU를 선택 합니다. 특정 SKU에 대한 구성 제한이 있습니다. 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요. Hello에 대 한 hello VPN 게이트웨이 만들 때 오류가 발생 하는 경우-GatewaySku, hello 최신 버전의 hello PowerShell cmdlet 설치 했는지 확인 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. VPN 장치 구성

사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다. 이 단계에서는 VPN 장치를 구성합니다. VPN 장치를 구성할 때 hello 다음이 필요 합니다.

- 공유 키 - 동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다. 이 예제에서는 기본적인 공유 키를 사용합니다. 더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.
- 가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다. Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다. toofind hello PowerShell을 사용 하 여 hello 다음 예제를 사용 하 여 가상 네트워크 게이트웨이의 공용 IP 주소:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Hello VPN 연결 만들기

다음으로 가상 네트워크 게이트웨이 및 VPN 장치 사이의 사이트 간 VPN 연결을 hello를 만듭니다. 자신의 있는지 tooreplace hello 값 수입니다. hello 공유 키에는 VPN 장치 구성에 사용한 hello 값과 일치 해야 합니다. 해당 hello 확인 '-ConnectionType'에서 사이트에 대 한 *IPsec*합니다.

1. Hello 변수를 설정 합니다.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Hello 연결을 만듭니다.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

잠시 후, hello 연결이 설정 됩니다.

## <a name="toverify"></a>9. Hello VPN 연결 확인

VPN 연결 되는 몇 가지 방법으로 tooverify 합니다.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa 가상 컴퓨터

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>로컬 네트워크 게이트웨이에 대한 IP 주소 접두사 수정

Hello IP 주소 접두사 라우팅된 tooyour 온-프레미스 위치를 변경 하는 경우에 hello 로컬 네트워크 게이트웨이 수정할 수 있습니다. 두 가지 지침이 제공됩니다. 선택한 hello 지침 게이트웨이 연결을 이미 작성 여부에 따라 달라 집니다.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>로컬 네트워크 게이트웨이에 대 한 hello 게이트웨이 IP 주소를 수정 합니다.

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>다음 단계

*  연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.
* BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.
