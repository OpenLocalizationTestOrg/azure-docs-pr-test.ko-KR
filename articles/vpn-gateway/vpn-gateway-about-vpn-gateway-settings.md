---
title: "크로스-프레미스 Azure 연결에 대 한 게이트웨이 설정을 aaaVPN | Microsoft Docs"
description: "Azure Virtual Network 게이트웨이의 VPN Gateway 설정에 대해 알아봅니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>VPN Gateway 구성 설정 정보

VPN Gateway는 공용 연결을 통해 가상 네트워크와 온-프레미스 위치 간에 암호화된 트래픽을 전송하는 가상 네트워크 게이트웨이의 유형입니다. 또한 Azure backbone hello에 걸쳐 가상 네트워크 간의 VPN 게이트웨이 toosend 트래픽을 사용할 수 있습니다.

VPN 게이트웨이 연결을 각각 포함 하는 구성 가능한 설정 여러 리소스의 hello 구성에 의존 합니다. 이 문서의 섹션 hello hello 리소스 및 리소스 관리자 배포 모델에서 만든 가상 네트워크에 대 한 VPN 게이트웨이 tooa와 관련 된 설정을 설명 합니다. Hello에 각 연결 솔루션에 대 한 설명 및 토폴로지 다이어그램을 찾을 수 있습니다 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 문서.

## <a name="gwtype"></a>게이트웨이 유형

가상 네트워크마다 각 유형의 가상 네트워크 게이트웨이를 하나씩만 포함할 수 있습니다. 가상 네트워크 게이트웨이 만들 때 hello 게이트웨이 유형 구성에 대 한 정확한 지 확인 해야 합니다.

hello-GatewayType에 대 한 사용 가능한 값은 같습니다.

* Vpn
* Express 경로

VPN 게이트웨이 필요 hello `-GatewayType` *Vpn*합니다.

예제:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>게이트웨이 SKU

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Hello 게이트웨이 SKU 구성

#### <a name="azure-portal"></a>Azure portal

Hello Azure 포털 toocreate 리소스 관리자 가상 네트워크 게이트웨이 사용 하는 경우에 hello 드롭다운을 사용 하 여 hello 게이트웨이 SKU를 선택할 수 있습니다. toohello 게이트웨이 유형 및 선택 하는 VPN 유형에 해당 하는 hello 옵션이 제공 됩니다.

#### <a name="powershell"></a>PowerShell

hello 다음 PowerShell 예에서는 지정 hello `-GatewaySku` VpnGw1으로 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>게이트웨이 SKU 변경(크기 조정)

Tooupgrade 게이트웨이 SKU tooa를 원하는 경우 더 강력한 SKU hello를 사용할 수 있습니다 `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet. 또한이 cmdlet을 사용 하 여 hello 게이트웨이 SKU 크기를 다운 그레이드할 수 있습니다.

다음 PowerShell 예에서는 hello tooVpnGw2 크기가 조정 되는 게이트웨이 SKU를 보여 줍니다.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>연결 유형

Hello 리소스 관리자 배포 모델에서 각 구성은 특정 가상 네트워크 게이트웨이 연결 형식이 필요합니다. hello 사용 가능한 리소스 관리자 PowerShell에 대 한 값 `-ConnectionType` 됩니다.

* IPsec
* Vnet2Vnet
* Express 경로
* VPNClient

다음 PowerShell 예에서는 hello, hello 연결 형식이 필요로 하는 S2S 연결 만듭니다 *IPsec*합니다.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>VPN 유형

VPN 게이트웨이 구성에 대 한 hello 가상 네트워크 게이트웨이 만들 때 VPN 유형을 지정 해야 합니다. 선택 하는 VPN 유형 hello에 있어서 hello 연결 토폴로지 toocreate 되도록 합니다. 예를 들어 P2S 연결에는 RouteBased VPN 유형이 필요합니다. VPN 유형을 사용 하는 hello 하드웨어에도 달라질 수 있습니다. S2S 구성에는 VPN 장치가 필요합니다. 일부 VPN 장치는 특정 VPN 유형을 지원합니다.

선택한 VPN 유형은 hello toocreate 원하는 hello 솔루션에 대 한 모든 hello 연결 요구 사항을 충족 해야 합니다. 예를 들어 toocreate S2S VPN 게이트웨이 연결 및 P2S VPN 게이트웨이 연결에 대 한 hello 동일한 가상 네트워크를 VPN 형식을 사용 *RouteBased* P2S VPN RouteBased 유형 필요 하기 때문에 있습니다. VPN 장치 RouteBased VPN 연결을 지원 하는지 tooverify는도 필요 합니다. 

가상 네트워크 게이트웨이 만든 후 hello VPN 유형을 변경할 수 없습니다. 가상 네트워크 게이트웨이 hello 및 새로 만들 toodelete를 해야 합니다. 두 가지 VPN 유형이 있습니다.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

hello 다음 PowerShell 예에서는 지정 hello `-VpnType` 으로 *RouteBased*합니다. 게이트웨이 만들 때 있어야 해당 hello-VpnType가 구성에 적합 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>게이트웨이 요구 사항

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>게이트웨이 서브넷

VPN Gateway를 만들기 전에 게이트웨이 서브넷을 만들어야 합니다. hello 게이트웨이 서브넷에 hello IP 주소가 해당 hello 가상 네트워크 게이트웨이 Vm 및 서비스에서 사용 합니다. 가상 네트워크 게이트웨이 만들 때 게이트웨이 Vm은 배포 된 toohello 게이트웨이 서브넷 및 필요한 hello VPN 게이트웨이 설정으로 구성 합니다. (예: 추가 Vm) 다른 무엇 toohello 게이트웨이 서브넷을 배포 하지 해야 합니다. hello 게이트웨이 서브넷 이름을 지정 해야 'GatewaySubnet' toowork 제대로 합니다. 이 hello 서브넷 toodeploy hello 가상 네트워크 게이트웨이 Vm 및 서비스를 Azure 알고 'GatewaySubnet' 있습니다 hello 게이트웨이 서브넷에 이름을 지정 합니다.

Hello 게이트웨이 서브넷을 만들 때 포함 하는 hello 수가 IP 주소 서브넷 hello를 지정할 수 있습니다. hello 게이트웨이 서브넷의 IP 주소가 hello은 할당 된 toohello 게이트웨이 Vm 및 게이트웨이 서비스입니다. 일부 구성에는 다른 구성보다 더 많은 IP 주소가 필요합니다. Hello hello 구성 toocreate 원하고 toocreate 원하는 hello 게이트웨이 서브넷에는 이러한 요구 사항을 충족 하는지 확인 지침을 살펴봅니다. 또한 toomake 게이트웨이 서브넷에 충분 한 IP 주소 tooaccommodate 가능한 향후 추가 구성이 포함 되어 있는지를 지정할 수 있습니다. 게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 게이트웨이 서브넷을 /28 이상으로 만드는 것이 좋습니다(/28, /27, /26 등). Hello 미래에 기능을 추가 하는 경우 이렇게 않습니다 tootear 게이트웨이 한 다음 삭제 있고 더 많은 IP 주소에 대 한 게이트웨이 서브넷 tooallow hello를 다시 만듭니다.

hello 다음 리소스 관리자 PowerShell 예제 이라는 게이트웨이 서브넷. Hello CIDR 표기법 지정 에/27 현재 존재 하는 대부분의 구성에 대 한 충분 한 IP 주소를 볼 수 있습니다.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>로컬 네트워크 게이트웨이

VPN 게이트웨이 구성을 만들 때 hello 로컬 네트워크 게이트웨이 종종 온-프레미스 위치를 나타냅니다. Hello 클래식 배포 모델에 hello 로컬 네트워크 게이트웨이 로컬 사이트 참조 tooas 되었습니다. 

하면 hello 로컬 네트워크 게이트웨이 이름 지정, hello hello 온-프레미스 VPN 장치의 공용 IP 주소 하 고 hello 온-프레미스 위치에 있는 hello 주소 접두사를 지정 합니다. Azure는 네트워크 트래픽에 대 한 hello 대상 주소 접두사, 로컬 네트워크 게이트웨이 위해 지정한 hello 구성 참조 찾은 그에 따라 패킷을 라우팅할 합니다. VPN Gateway 연결을 사용하는 VNet-VNet 구성에 대해서도 로컬 네트워크 게이트웨이를 지정합니다.

다음 PowerShell 예에서는 hello 새 로컬 네트워크 게이트웨이 만듭니다.

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Toomodify hello 로컬 네트워크 게이트웨이 설정이 필요한 경우가 있습니다. Hello VPN 장치의 hello IP 주소가 변경 된 경우 추가 또는 수정 hello 주소 범위 또는 예를 들어 있습니다. 클래식 VNet에 대 한 hello 로컬 네트워크 페이지 hello 클래식 포털에서 이러한 설정을 변경할 수 있습니다. Resource Manager의 경우 [PowerShell을 사용하여 로컬 네트워크 게이트웨이 설정 수정](vpn-gateway-modify-local-network-gateway.md)을 참조하세요.

## <a name="resources"></a>REST API 및 PowerShell cmdlet

추가 기술 리소스 및 VPN 게이트웨이 구성에 대 한 REST Api, PowerShell cmdlet 또는 Azure CLI를 사용 하는 경우 특정 구문 요구 사항에 대 한 hello 다음 페이지를 참조:

| **클래식** | **리소스 관리자** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| 지원되지 않음 | [Azure CLI](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>다음 단계

사용 가능한 연결 구성에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md) 를 참조하세요.