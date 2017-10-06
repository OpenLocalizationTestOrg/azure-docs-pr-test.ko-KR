---
title: "가상 네트워크 tooanother VNet 연결: Azure CLI | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 Azure CLI를 사용하여 가상 네트워크를 함께 연결하는 과정을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Azure CLI를 사용하여 VNet 간 VPN 게이트웨이 연결 구성

이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다. hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다. Hello 구독이 다른 구독에서 연결 Vnet toobe hello와 관련 된 필요 하지 않는 경우 동일한 Active Directory 테 넌 트. 

이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용 하 고 Azure CLI를 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [다양한 배포 모델 간 연결 - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [다양한 배포 모델 간 연결 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. Vnet hello에 있는 경우 동일한 지역 VNet 피어 링을 사용 하 여 연결 tooconsider 할 수 있습니다. VNet 피어링은 VPN Gateway를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.

VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다. 이렇게 하면 hello 다음 다이어그램에에서 나와 있는 것 처럼 가상 네트워크 간 연결 되 면 크로스-프레미스 연결을 결합 하는 네트워크 토폴로지를 설정할 수 있습니다.

![연결 정보](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>가상 네트워크에 연결하는 이유

다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.

* **지역 간 지리적 중복 및 지리적 상태**

  * 인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.
  * Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다. 한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.
* **분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**

  * 내 동일한 hello 영역을 설정할 수 있습니다 다층 계층 응용 프로그램 기한 tooisolation 또는 관리 요구를 함께 연결 하는 여러 가상 네트워크가 됩니다.

VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

### <a name="which-set-of-steps-should-i-use"></a>어느 단계 집합을 사용해야 합니까?

이 문서에서는 서로 다른 두 집합의 단계를 볼 수 있습니다. 일련의 절차에 대 한 [Vnet에 상주 하는 동일한 구독 hello](#samesub), 용이고 다른 하나는 [서로 다른 구독에 있는 Vnet](#difsub)합니다.

## <a name="samesub"></a>Hello에 있는 Vnet 연결 동일한 구독

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>시작하기 전에

시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다. Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.

### <a name="Plan"></a>IP 주소 범위 계획

다음 단계는 hello, 두 가상 네트워크와 해당 게이트웨이 서브넷 및 구성을 만듭니다. Hello 간의 VPN 연결이 두 Vnet 다음 만듭니다. 네트워크 구성에 대 한 중요 한 tooplan hello IP 주소 범위는 따라서 VNet 범위 또는 로컬 네트워크 범위가 겹치지 않는지 확인해야 합니다. 이 예에서는 DNS 서버를 포함하지 않습니다. 가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.

다음 hello 예제에는 값에는 hello를 사용 합니다.

**TestVNet1에 대한 값:**

* VNet 이름: TestVNet1
* 리소스 그룹: TestRG1
* 위치: 미국 동부
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* 프런트 엔드: 10.11.0.0/24
* 백 엔드: 10.12.0.0/24
* 게이트웨이 서브넷 = 10.12.255.0/27
* 게이트웨이 이름: VNet1GW
* 공용 IP: VNet1GWIP
* VpnType: 경로 기반
* 연결(1 대 4): VNet1 대 VNet4
* 연결(1 대 5): VNet1 대 VNet5
* 연결 유형: VNet 간

**TestVNet4에 대한 값:**

* VNet 이름: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* 프런트 엔드: 10.41.0.0/24
* 백 엔드: 10.42.0.0/24
* 게이트웨이 서브넷: 10.42.255.0/27
* 리소스 그룹: TestRG4
* 위치: 미국 서부
* 게이트웨이 이름: VNet4GW
* 공용 IP: VNet4GWIP
* VpnType: 경로 기반
* 연결: VNet4 대 VNet1
* 연결 유형: VNet 간


### <a name="Connect"></a>1 단계-tooyour 구독 연결

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>2단계 - TestVNet1 만들기 및 구성

1. 리소스 그룹을 만듭니다.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. TestVNet1 용 TestVNet1 및 hello 서브넷을 만듭니다. 이 예제에서는 TestVNet1이라는 가상 네트워크와 FrontEnd라는 서브넷을 만듭니다.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Hello 백 엔드 서브넷에 대 한 추가 주소 공간을 만듭니다. 이 단계에서는 앞에서 만든 두 hello 주소 공간을 지정 하 고 hello tooadd 한다고 추가 주소 공간을 확인 합니다. 때문에 이것이 hello [az 네트워크 vnet 업데이트](https://docs.microsoft.com/cli/azure/network/vnet#update) hello 이전 설정을 덮어씁니다. 모든 확인 하십시오 있는지 toospecify hello 주소 접두사의이 명령을 사용 하는 경우.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Hello 백 엔드 서브넷을 만듭니다.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Hello 게이트웨이 서브넷을 만듭니다. Hello 게이트웨이 서브넷은 이라는 '를 확인 합니다. 이 이름은 필수입니다. 이 예제에서는 hello 게이트웨이 서브넷에 / 27을 사용 중입니다. 가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, 적어도/28 또는/27 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다. 이렇게 하면 충분 한 주소 tooaccommodate 가능한 추가 되는 구성에 만한 hello 이후 있습니다.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 만들려는 VNet에 대 한 요청 합니다. 해당 hello AllocationMethod 동적 점에 유의 하십시오. 원하는 toouse hello IP 주소를 지정할 수 없습니다. 그는 동적으로 할당 된 tooyour 게이트웨이입니다.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. TestVNet1에 대 한 hello 가상 네트워크 게이트웨이 만듭니다. VNet-VNet 구성에는 RouteBased VpnType이 필요합니다. '대기 없음-' 매개 변수 hello를 사용 하 여이 명령을 실행 하면 피드백이 나 출력에 표시 되지 않으면 합니다. hello '대기 없음-' 매개 변수는 hello 게이트웨이 toocreate hello 백그라운드에서 합니다. 해당 hello VPN 게이트웨이 즉시 만들기를 완료 것을 의미 하지 않습니다. 한 게이트웨이 만드는 45 분에 따라 이상 hello 게이트웨이 SKU 있습니다를 사용 하는 종종 걸릴 수 있습니다.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>3단계 - TestVNet4 만들기 및 구성

1. 리소스 그룹을 만듭니다.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. TestVNet4 만들기.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. TestVNet4의 추가 서브넷을 만듭니다.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Hello 게이트웨이 서브넷을 만듭니다.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. 공용 IP 주소를 요청합니다.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Hello TestVNet4 가상 네트워크 게이트웨이 만듭니다.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>4 단계-hello 연결 만들기

이제 VPN 게이트웨이가 있는 VNet이 두 개 있습니다. hello 다음 단계는 hello 가상 네트워크 게이트웨이 간에 VPN 게이트웨이 연결을 toocreate입니다. 위의 hello 예제를 사용 하는 경우 VNet 게이트웨이 다른 리소스 그룹에 포함 되어 있습니다. 게이트웨이 다른 리소스 그룹에서을 tooidentify 필요 하 고 연결할 때 각 게이트웨이에 대 한 hello 리소스 Id를 지정 합니다. Vnet hello에 있는 경우 동일한 리소스 그룹 hello를 사용할 수 있습니다 [명령의 두 번째 집합](#samerg) toospecify hello 리소스 Id는 필요 하지 않으므로 합니다.

### <a name="diffrg"></a>다른 리소스 그룹에 상주 하는 Vnet tooconnect

1. 다음 명령을 hello의 hello 출력에서 hello를 VNet1GW의 리소스 ID를 가져옵니다.

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  찾을 hello hello 출력에 "id:" 줄. hello 따옴표 안에 hello 값 hello 다음 섹션에서 필요한 toocreate hello 연결 됩니다. 쉽게 붙여 넣을 수 있습니다 하 여 연결을 만들 때 이러한 값 tooa 텍스트 편집기, 메모장과 같은 복사 합니다.

  예제 출력:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  복사 후 hello 값 **"id":** hello 따옴표 안에 있습니다.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Hello VNet4GW의 리소스 ID 및 복사 hello 값 tooa 텍스트 편집기를 가져옵니다.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Hello TestVNet1 tooTestVNet4 연결을 만듭니다. 이 단계에서 TestVNet1 tooTestVNet4 hello 연결을 만듭니다. Hello 예제에서 참조 하는 공유 키 있습니다. Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있습니다. 두 연결에 대 한 중요 한 점은 그 hello 공유 키 hello 일치 해야 합니다. 연결을 만드는 데 toocomplete 잠시 걸립니다.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Hello TestVNet4 tooTestVNet1 연결을 만듭니다. 이 단계에서 TestVNet4 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다. Hello 공유 키와 일치 하는지 확인 합니다. 몇 분 tooestablish hello 연결을 걸립니다.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. 연결을 확인합니다. [연결 확인](#verify)을 참조하세요.

### <a name="samerg"></a>tooconnect Vnet 동일 hello에 상주 하는 리소스 그룹

1. Hello TestVNet1 tooTestVNet4 연결을 만듭니다. 이 단계에서 TestVNet1 tooTestVNet4 hello 연결을 만듭니다. 공지 hello 리소스 그룹 hello 예제에서 동일한 hello 됩니다. Hello 예제에서 참조 하는 공유 키를 표시 됩니다. 하지만 Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있는데, 두 연결에 대 한 hello 공유 키와 일치 해야 합니다. 연결을 만드는 데 toocomplete 잠시 걸립니다.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Hello TestVNet4 tooTestVNet1 연결을 만듭니다. 이 단계에서 TestVNet4 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다. Hello 공유 키와 일치 하는지 확인 합니다. 몇 분 tooestablish hello 연결을 걸립니다.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. 연결을 확인합니다. [연결 확인](#verify)을 참조하세요.

## <a name="difsub"></a>다른 구독에 있는 VNet 연결

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

이 시나리오에서는 TestVNet1 및 TestVNet5를 연결합니다. hello Vnet에 서로 다른 구독 상주 합니다. hello 구독 hello와 관련 된 toobe 불필요 동일한 Active Directory 테 넌 트입니다. 이 구성에 대 한 hello 단계 순서 tooconnect TestVNet1 tooTestVNet5에에서 대 한 추가 VNet 대 VNet 연결을 추가합니다.

### <a name="TestVNet1diff"></a>5단계 - TestVNet1 만들기 및 구성

이러한 지침은 hello 이전 섹션의에서 hello 단계에서 계속 합니다. 완료 해야 [1 단계](#Connect) 및 [2 단계](#TestVNet1) toocreate TestVNet1를 구성 하 고 TestVNet1에 대 한 VPN 게이트웨이 hello 합니다. 이 구성에 대 한 하지 않으므로 필요한 toocreate TestVNet4 hello 이전 섹션에서 다음이 단계와 충돌을 만들지 않는 경우 하지 않지만. 1단계와 2단계를 완료하면 6단계(아래)를 계속 진행합니다.

### <a name="verifyranges"></a>6 단계-hello IP 주소 범위를 확인 합니다.

추가 연결을 만들 때 중요 한 tooverify hello 새 가상 네트워크의 IP 주소 공간을 hello 다른 VNet 범위 또는 로컬 네트워크 게이트웨이 범위와 겹치지 않는 됩니다. 이 연습에서는 다음 TestVNet5 hello에 대 한 값에는 hello를 사용할 수 있습니다.

**TestVNet5에 대한 값:**

* VNet 이름: TestVNet5
* 리소스 그룹: TestRG5
* 위치: 일본 동부
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* 프런트 엔드: 10.51.0.0/24
* 백 엔드: 10.52.0.0/24
* 게이트웨이 서브넷: 10.52.255.0.0/27
* 게이트웨이 이름: VNet5GW
* 공용 IP: VNet5GWIP
* VpnType: 경로 기반
* 연결: VNet5 대 VNet1
* 연결 유형: VNet 간

### <a name="TestVNet5"></a>7단계 - TestVNet5 만들기 및 구성

이 단계는 hello 새 구독을 구독 5의 hello 컨텍스트에서 수행 되어야 합니다. Hello 구독을 소유 하는 다른 조직의 관리자에 게가이 부분을 수행할 수 있습니다. 구독 사용 간의 tooswitch ' az 계정 목록-모든 ' toolist 구독 사용 가능한 tooyour 계정 hello 다음 사용 하 여 ' az 계정 세트-구독 <subscriptionID>' tooswitch toohello 구독 toouse 되도록 합니다.

1. 올바른지 확인 하는 연결 된 tooSubscription 5, 리소스 그룹을 만듭니다.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. TestVNet5 만들기.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. 서브넷을 추가합니다.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Hello 게이트웨이 서브넷을 추가 합니다.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. 공용 IP 주소를 요청합니다.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Hello TestVNet5 게이트웨이 만들기

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>8 단계-hello 연결 만들기

로 표시 하는 두 개의 CLI 세션에이 단계를 나눌 **[구독 1]**, 및 **[구독 5]** hello 게이트웨이 hello 서로 다른 구독에 있기 때문에 있습니다. 구독 사용 간의 tooswitch ' az 계정 목록-모든 ' toolist 구독 사용 가능한 tooyour 계정 hello 다음 사용 하 여 ' az 계정 세트-구독 <subscriptionID>' tooswitch toohello 구독 toouse 되도록 합니다.

1. **[1 구독]**  에 로그인 하 고 tooSubscription 1을 연결 합니다. 실행된 hello 다음 명령 hello hello 출력에서 게이트웨이의 tooget hello 이름 및 ID 수 있습니다.

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  에 대 한 hello 출력 복사 "id:". Hello ID 및 VNet 게이트웨이 (VNet1GW) toohello 관리자에 게 구독 5의 전자 메일 또는 다른 방법을 통해의 hello 이름을 전송 합니다.

  예제 출력:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[구독 5]**  에 로그인 하 고 5 tooSubscription 연결 합니다. 실행된 hello 다음 명령 hello hello 출력에서 게이트웨이의 tooget hello 이름 및 ID 수 있습니다.

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  에 대 한 hello 출력 복사 "id:". Hello ID 및 VNet 게이트웨이 (VNet5GW) toohello 관리자에 게 구독 1의 전자 메일 또는 다른 방법을 통해의 hello 이름을 전송 합니다.

3. **[1 구독]**  이 단계에서 TestVNet1 tooTestVNet5 hello 연결 만듭니다. 하지만 Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있는데, 두 연결에 대 한 hello 공유 키와 일치 해야 합니다. 연결 만들기 toocomplete 잠시를 걸릴 수 있습니다. TooSubscription 1을 연결 하 고 있는지 확인 합니다.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[구독 5]**  TestVNet5 tooTestVNet1에서 hello 연결을 만드는 점을 제외 하 고이 단계는 위에 나온 toohello 유사 합니다. 해당 hello 공유 키 일치 및 tooSubscription 5에 연결 해야 하 고 있는지 확인 합니다.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Hello 연결 되어 있는지 확인
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>VNet 간 FAQ
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>다음 단계

* 연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 참조 hello [가상 컴퓨터 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)합니다.
* BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.
