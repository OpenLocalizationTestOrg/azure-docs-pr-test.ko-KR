---
title: "어떻게 tooconfigure Azure ExpressRoute 회로 대 한 라우팅: CLI | Microsoft Docs"
description: "이 문서를 사용 하 여 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전 할 수 있습니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>CLI를 사용하여 ExpressRoute 회로의 라우팅 만들기 및 수정

이 문서를 사용 하 여 만들고 CLI를 사용 하 여 hello 리소스 관리자 배포 모델의 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다. Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다. 다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.

> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [비디오 - 개인 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [비디오 - 공용 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [비디오 - Microsoft 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>필수 구성 요소

* 시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다. Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.
* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.
* 활성화된 Express 경로 회로가 있어야 합니다. 너무 hello 지침에 따라[ExpressRoute 회로 만들기](howto-circuit-cli.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. hello ExpressRoute 회로이 문서의에 toobe 수 toorun hello 명령을 가능 하 고 프로 비전 된 상태에 있어야 합니다.

이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.

ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다(Azure 개인, Azure 공용 및 Microsoft). 선택한 순서로 피어링을 구성할 수 있습니다. 그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.

## <a name="azure-private-peering"></a>Azure 개인 피어링

이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.

### <a name="toocreate-azure-private-peering"></a>Azure 개인 피어 링 toocreate

1. Hello Azure CLI의 최신 버전을 설치 합니다. Hello hello Azure 명령줄 인터페이스 (CLI)의 최신 버전을 사용 해야 합니다. * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.

  ```azurecli
  az login
  ```

  Toocreate ExpressRoute 회로 원하는 hello 구독 선택

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다. Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.
3. Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Azure 개인 피어 링 hello 회로 대 한 구성 합니다. Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다. 이 피어링에 개인 AS 숫자를 사용할 수 있습니다. 65515를 사용하지 않는지 확인합니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.

  다음 예에서는 tooconfigure 회로 대 한 피어 링 개인 Azure hello를 사용 합니다.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>세부 정보를 피어 링 개인 Azure tooview

다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

hello 비슷한 toohello 다음은 예제 출력:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 개인 피어 링 구성

다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다. 이 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>Azure 개인 피어 링 toodelete

다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.

> [!WARNING]
> 모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 예제를 실행 하기 전에 확인 해야 합니다. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Azure 공용 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.

### <a name="toocreate-azure-public-peering"></a>Azure 공용 피어 링 toocreate

1. Hello Azure CLI의 최신 버전을 설치 합니다. Hello hello Azure 명령줄 인터페이스 (CLI)의 최신 버전을 사용 해야 합니다. * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.

  ```azurecli
  az login
  ```

  ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다.  Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자가 Azure 개인 피어링을 사용하도록 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.
3. Hello ExpressRoute 회로 tooensure 프로 비전 되며 사용 하도록 설정도 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```azurecli
  az network express-route list
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Azure 공용 피어 링 hello 회로 대 한 구성 합니다. 다음 정보를 계속 진행 하기 전에 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.

  다음 예에서는 tooconfigure 회로 대 한 피어 링 공용 Azure hello를 실행 합니다.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.

### <a name="tooview-azure-public-peering-details"></a>세부 정보를 피어 링 공용 Azure tooview

다음 예제는 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

hello 비슷한 toohello 다음은 예제 출력:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 공용 피어 링 구성

다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다. 이 예제에서는 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>Azure 공용 피어 링 toodelete

다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Microsoft 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.

> [!IMPORTANT]
> 이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다. Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다. 자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 피어 링

1. Hello Azure CLI의 최신 버전을 설치 합니다. 사용 하 여 hello 최신 버전의 hello Azure 명령줄 인터페이스 (CLI). * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.

  ```azurecli
  az login
  ```

  ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다. Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.

3. Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```azurecli
  az network express-route list
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Microsoft hello 회로 대 한 피어 링을 구성 합니다. 계속 하기 전에 정보 다음 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
  * 접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다. 공용 IP 주소 접두사만 수락됩니다. Toosend 접두사를 사용 하도록 하려는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다. 이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.
  * **선택 사항-** 고객 ASN: 광고 접두사 수로 등록 된 toohello 피어 링 되지 않은 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.
  * 라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.

   다음 예에서는 tooconfigure Microsoft 피어 링 회로 대 한 hello를 실행 합니다.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft 피어 링 세부 정보

다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

hello 비슷한 toohello 다음은 예제 출력:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 피어 링 구성

Hello 구성의 어떠한 부분을 업데이트할 수 있습니다. hello 보급 hello 다음 예제에서에서 123.1.0.0/24 too124.1.0.0/24에서 hello 회로의 접두사를 업데이트 하는 중:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 피어 링

다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>다음 단계

다음 단계 [연결할 ExpressRoute 회로 VNet tooan](howto-linkvnet-cli.md)합니다.

* Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.
* 회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.
* 가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.