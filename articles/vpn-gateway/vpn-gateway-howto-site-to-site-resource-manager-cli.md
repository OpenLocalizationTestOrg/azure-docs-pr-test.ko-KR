---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN: CLI | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 이 단계는 CLI를 사용하여 크로스-프레미스 사이트 간 VPN Gateway 연결을 만드는 데 도움이 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기

이 문서에서는 어떻게 toouse hello Azure CLI toocreate 온-프레미스 네트워크 toohello VNet에서에서 사이트 간 VPN 게이트웨이 연결 합니다. 이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.<br>

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다. 이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다. VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.

* 호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다. 호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.
* VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다. 이 IP 주소는 NAT 뒤에 배치할 수 없습니다.
* 온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다. 이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다. 온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다.
* Hello CLI 명령 (2.0 이상)의 최신 버전을 설치 했는지 확인 합니다. Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)합니다.

### <a name="example"></a>예제 값

값 toocreate 테스트 환경에 따라 hello를 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Tooyour 구독 연결

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. 리소스 그룹 만들기

hello 다음 예제에서는 'TestRG1' hello 'eastus' 위치에 명명 된 리소스 그룹 Hello 지역 되도록 toocreate VNet에에서 리소스 그룹이 이미 있는 경우 하나를 대신 사용할 수 있습니다.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. 가상 네트워크 만들기

가상 네트워크를 아직 없는 경우 새로 만들 hello를 사용 하 여 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create) 명령입니다. 가상 네트워크를 만들 때 지정한 hello 주소 공간 온-프레미스 네트워크에가지고 있는 hello 주소 공간 중 하나라도 겹치지 않는지 확인 합니다.

hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 'TestVNet1' 및 'Subnet1' 서브넷에 있습니다.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Hello 게이트웨이 서브넷 만들기

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

이 구성에는 게이트웨이 서브넷도 필요합니다. hello 가상 네트워크 게이트웨이 hello VPN 게이트웨이 서비스에서 사용 되는 hello IP 주소를 포함 하는 게이트웨이 서브넷을 사용 합니다. 게이트웨이 서브넷을 만들 때 이름을 'GatewaySubnet'으로 지정해야 합니다. 다른 이름을 지정하는 경우 서브넷을 만들지만 Azure에서는 게이트웨이 서브넷으로 취급하지 않습니다.

지정 하는 hello 게이트웨이 서브넷의 hello 크기에 따라 달라 집니다 hello VPN 게이트웨이 구성 toocreate 되도록 합니다. 가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, / 27 또는/28 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다. 더 큰 게이트웨이 서브넷을 사용 하 여 구성에 대 한 충분 한 IP 주소 tooaccommodate 가능한 이후 수 있습니다.

사용 하 여 hello [az 네트워크 vnet 서브넷 만들기](/cli/azure/network/vnet/subnet#create) 명령 toocreate hello 게이트웨이 서브넷입니다.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Hello 로컬 네트워크 게이트웨이 만들기

일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다. Hello 사이트 기준인 Azure 수 tooit를 참조 하십시오. 그런 다음 hello IP 주소를 지정 된 이름을 지정 hello 온-프레미스 VPN 장치 toowhich의 연결을 만듭니다. 또한 hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 접두사를 지정 합니다. 지정 하는 hello 주소 접두사는 온-프레미스 네트워크에 있는 hello 접두사입니다. 온-프레미스 네트워크 변경 되 면 hello 접두사를 쉽게 업데이트할 수 있습니다.

다음 값에는 hello를 사용 합니다.

* hello *-게이트웨이 ip 주소* 온-프레미스 VPN 장치의 hello IP 주소입니다. VPN 장치는 NAT 뒤에 배치할 수 없습니다.
* hello *-로컬 주소-접두사* 는 온-프레미스 주소 공간입니다.

사용 하 여 hello [az 네트워크 로컬 게이트웨이 만들기](/cli/azure/network/local-gateway#create) 명령 tooadd 여러 주소 접두사와 로컬 네트워크 게이트웨이:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. 공용 IP 주소 요청

VPN Gateway에는 공용 IP 주소가 있어야 합니다. 먼저 hello IP 주소 리소스를 요청 하 고 가상 네트워크 게이트웨이 만들 때 tooit를 참조 하십시오. hello IP 주소를 사용 hello VPN 게이트웨이 만들 때 toohello 리소스를 동적으로 할당 됩니다. 현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다. 고정 공용 IP 주소 할당을 요청할 수 없습니다. 그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에이 아닙니다. hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다. VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.

사용 하 여 hello [az 네트워크 공용 ip 만들기](/cli/azure/network/public-ip#create) 명령 toorequest 동적 공용 IP 주소입니다.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Hello VPN 게이트웨이 만들기

Hello 가상 네트워크 VPN 게이트웨이 만듭니다. VPN 게이트웨이 만들기 too45 분 또는 toocomplete 자세한 정도 걸릴 수 있습니다.

다음 값에는 hello를 사용 합니다.

* hello *-게이트웨이 유형* 사이트-사이트에 대 한 구성은 *Vpn*합니다. hello 게이트웨이 형식은 항상 구현 하는 특정 toohello 구성입니다. 자세한 내용은 [게이트웨이 유형](vpn-gateway-about-vpn-gateway-settings.md#gwtype)을 참조하세요.
* hello *-vpn 형식* 수 *RouteBased* (일부 설명서에서는 동적 게이트웨이 tooas 함) 또는 *PolicyBased* (tooas은 정적 게이트웨이가 중 일부를 참조 합니다. 설명서)입니다. hello 설정은 hello 장치에 연결 하는 특정 toorequirements입니다. VPN Gateway 유형에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#vpntype)를 참조하세요.
* Hello toouse 게이트웨이 SKU를 선택 합니다. 특정 SKU에 대한 구성 제한이 있습니다. 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.

Hello를 사용 하 여 hello VPN 게이트웨이 만들기 [az 네트워크 vnet 게이트웨이 만들기](/cli/azure/network/vnet-gateway#create) 명령입니다. '대기 없음-' 매개 변수 hello를 사용 하 여이 명령을 실행 하면 피드백이 나 출력에 표시 되지 않으면 합니다. 이 매개 변수는 hello 백그라운드에 hello 게이트웨이 toocreate를 허용합니다. 게이트웨이 toocreate 약 45 분이 필요합니다.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. VPN 장치 구성

사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다. 이 단계에서는 VPN 장치를 구성합니다. VPN 장치를 구성할 때 hello 다음이 필요 합니다.

- 공유 키 - 동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다. 이 예제에서는 기본적인 공유 키를 사용합니다. 더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.
- 가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다. Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다. 가상 네트워크 게이트웨이 사용 하 여 hello의 toofind hello 공용 IP 주소 [az 네트워크 공개 ip 목록](/cli/azure/network/public-ip#list) 명령입니다. 읽기 쉽도록 hello 출력은 테이블 형식으로 공용 Ip의 서식이 지정 된 toodisplay hello 목록입니다.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Hello VPN 연결 만들기

가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 간의 hello 사이트 간 VPN 연결을 만듭니다. 사용량 기준 과금 특별 한 주의 toohello 공유 키 값을 구성 하는 hello와 일치 해야 하는 VPN 장치에 대 한 키 값을 공유 합니다.

Hello를 사용 하 여 hello 연결 만들기 [az 네트워크 vpn 연결 만들기](/cli/azure/network/vpn-connection#create) 명령입니다.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

잠시 후, hello 연결이 설정 됩니다.

## <a name="toverify"></a>10. Hello VPN 연결 확인

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

다른 메서드 tooverify toouse 하려면 해당 연결을 참조 [VPN 게이트웨이 연결을 확인](vpn-gateway-verify-connection-resource-manager.md)합니다.

## <a name="connectVM"></a>tooconnect tooa 가상 컴퓨터

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>일반 작업

이 섹션에는 사이트 간 구성을 작업할 때 도움이 되는 일반적인 명령이 포함되어 있습니다. CLI 네트워킹 명령의 전체 목록을 hello에 대 한 참조 [Azure CLI-네트워킹](/cli/azure/network)합니다.

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>다음 단계

* 연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.
* BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.
* 강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.
* 항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.
* 네트워킹 Azure CLI 명령 목록은 [Azure CLI](https://docs.microsoft.com/cli/azure/network)를 참조하세요.