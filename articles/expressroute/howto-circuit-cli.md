---
title: "Azure ExpressRoute 회로 만들기 및 수정: CLI | Microsoft Docs"
description: "이 문서에서는 어떻게 toocreate, 프로 비전, 확인, 업데이트, 삭제 및 CLI를 사용 하 여 ExpressRoute 회로 프로 비전 해제를 설명 합니다."
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>CLI를 사용하여 ExpressRoute 회로 만들기 및 수정


이 문서에서는 toocreate Azure ExpressRoute 회로 사용 하 여 명령줄 인터페이스 (CLI) hello 하는 방법을 설명 합니다. 또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 회로 프로 비전 해제 알 수 있습니다. ExpressRoute 회로와 다른 방법 toowork toouse 원한다 면 hello 문서 hello 다음 목록에서에서 선택할 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>시작하기 전에

* 시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다. Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)합니다.
* 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.

## <a name="create-and-provision-an-expressroute-circuit"></a>Express 경로 회로 만들기 및 프로비전

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Tooyour Azure 계정에에서 로그인 하 고 구독을 선택 합니다.

toobegin 구성, tooyour Azure 계정에에서 로그인 합니다. 예제 toohelp 연결한 다음 hello를 사용 합니다.

```azurecli
az login
```

Hello 계정에 대 한 hello 구독을 확인 합니다.

```azurecli
az account list
```

ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. 지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.

ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다. CLI 명령 ' az 네트워크 express 경로 목록-서비스-공급자 ' hello 이후 단계에서 사용 하는이 정보를 반환 합니다.

```azurecli
az network express-route list-service-providers
```

hello 응답은 다음 예제와 비슷한 toohello입니다.

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

연결 공급자가 나열 하는 경우에 hello 응답 toosee를 확인 합니다. 다음 정보는 회로 만들 때 필요 합니다 hello 기록해 두십시오.

* 이름
* PeeringLocations
* BandwidthsOffered

이제 준비 toocreate ExpressRoute 회로 것입니다.

### <a name="3-create-an-expressroute-circuit"></a>3. Express 경로 회로 만들기

> [!IMPORTANT]
> ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다. Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행 합니다.
> 
> 

아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다. Hello 다음 명령을 실행 하 여 리소스 그룹을 만들 수 있습니다.

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다. 다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다. 

Hello 올바른 SKU 계층과 SKU 제품군을 지정 하 고 있는지 확인 합니다.

* SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다. Hello premium 추가 기능에 대해 '표준' tooget hello 표준 SKU 또는 '프리미엄'를 지정할 수 있습니다.
* SKU 제품군 hello 청구 유형을 결정합니다. 데이터 요금제의 경우 'Metereddata'를 선택하고 무제한 데이터 요금제의 경우 'Unlimiteddata'를 선택할 수 있습니다. 'Metereddata 'too'Unlimiteddata' 있지만 유형을 변경할 수 없습니다 hello too'Metereddata 'Unlimiteddata' 에서' hello 청구 유형을 변경할 수 있습니다.


ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다. 다음 예제는 hello은 새 서비스 키에 대 한 요청입니다.

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

hello 응답 hello 서비스 키를 포함합니다.

### <a name="4-list-all-expressroute-circuits"></a>4. 모든 Express 경로 회로 나열

사용자가 만든 모든 hello ExpressRoute 회로 목록을 tooget는 hello 'az 네트워크 express 경로 목록' 명령을 실행 합니다. 이 명령을 사용하여 이 정보를 언제든지 검색할 수 있습니다. toolist 모든 회로 hello 매개 변수 없이 호출을 확인 합니다.

```azurecli
az network express-route list
```

서비스 키 hello에 나열 된 *ServiceKey* hello 응답의 필드입니다.

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Hello를 사용 하 여 hello 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다 '-h' 매개 변수입니다.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기

'ServiceProviderProvisioningState' hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대 한 정보를 제공 합니다. hello 상태는 Microsoft의 hello에 hello 상태를 제공합니다. 자세한 내용은 참조 hello [워크플로 문서](expressroute-workflows.md#expressroute-circuit-provisioning-states)합니다.

새 ExpressRoute 회로 만들 때 hello 회로 hello 다음 상태는 있습니다.

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 뒤에 상태를 변경 합니다.

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

하면 toobe 수 toouse ExpressRoute 회로 hello 상태 뒤에 있어야 합니다.

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인

Hello 상태 및 hello 회로 키의 hello 상태를 확인 하면 공급자가 회로 설정 하는 때를 알 수 있습니다. Hello 회로 구성한 후에 'ServiceProviderProvisioningState' hello 다음 예제와 같이 '프로 비전 됨'으로 나타납니다.

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. 라우팅 구성 만들기

단계별 지침은 hello [ExpressRoute 회로 라우팅 구성을](howto-routing-cli.md) toocreate 문서 및 회로 피어 링을 수정 합니다.

> [!IMPORTANT]
> 이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. 가상 네트워크 tooan ExpressRoute 회로 연결

다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다. 사용 하 여 hello [tooExpressRoute 회로 네트워크 가상 연결](howto-linkvnet-cli.md) 문서.

## <a name="modify"></a>Express 경로 회로 수정

연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다. Hello 가동 중지 시간 없이 변경 내용을 다음을 수행할 수 있습니다.

* ExpressRoute 회로에 대해 ExpressRoute Premium 추가 기능을 사용하거나 사용하지 않을 수 있습니다.
* 제공 된 hello 포트에서 용량은 hello 대역폭의 ExpressRoute 회로 늘릴 수 있습니다. 그러나 회로의 대역폭 hello를 다운 그레이드도 지원 되지 않습니다. 
* 데이터 요금 tooUnlimited 데이터에서에서 hello 계량 계획을 변경할 수 있습니다. 그러나 hello 계량 데이터가 지원 되지 않습니다 무제한 데이터 요금 tooMetered에서 계획을 변경 합니다.
* *Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.

제한 및 제한 사항에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium 추가 기능

다음 명령을 hello를 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

hello 회로 hello ExpressRoute premium 추가 기능 사용 하도록 설정 되었습니다. Hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 시작 합니다.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium 추가 기능

> [!IMPORTANT]
> 이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.
> 
> 

Hello ExpressRoute premium 추가 기능을 해제 하기 전에 다음 조건을 hello 이해:

* Toostandard premium에서에서 다운 그레이드 먼저 10 개 미만의 가상 네트워크 연결 된 toohello 회로 있는지 확인 해야 합니다. 10개를 초과하면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.
* 다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다. 가상 네트워크의 연결을 해제하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.
* 사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다. 경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션을 삭제 합니다. 보급된 된 접두사의 hello 수가 4, 000 아래 될 때까지 hello 세션 했다가 다시 설정할 수 없습니다.

다음 예제는 hello를 사용 하 여 hello 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 회로 대역폭

공급자에 대 한 지원 hello 대역폭 옵션에 대 한 확인 hello [express 경로 FAQ](expressroute-faqs.md)합니다. 기존 회로 hello 크기 보다 큰 모든 크기를 선택할 수 있습니다.

> [!IMPORTANT]
> 기존 포트 hello에 용량이 부족 하면 toorecreate hello ExpressRoute 회로 할 수 있습니다. 해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.
>
> Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다. 대역폭을 다운 그레이드 하면 toodeprovision hello ExpressRoute 회로 차지 하며 다음 새 ExpressRoute 회로 다시 프로 비전 합니다.
>

필요한 hello 크기를 결정 한 후 다음 명령 tooresize hello 회로 사용 합니다.

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

회로 hello Microsoft 쪽에서 크기가 조정 됩니다. 다음으로 문의 해야 해당 측 toomatch 사용자 연결 공급자 tooupdate 구성을이 변경 합니다. 이 알림은 변경한 후 업데이트 하는 hello 대역폭 옵션에 대 한 청구 있습니다을 시작 합니다.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>요금제 toounlimited에서 toomove hello SKU

다음 예제는 hello를 사용 하 여 hello ExpressRoute 회로의 SKU를 변경할 수 있습니다.

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol 액세스 toohello 클래식 및 리소스 관리자 환경

지침에 hello 검토 [hello 클래식 toohello 리소스 관리자 배포 모델의 이동 ExpressRoute 회로](expressroute-howto-move-arm.md)합니다.

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Express 경로 회로 프로비전 해제 및 삭제

toodeprovision 및 delete ExpressRoute 회로 다음 조건을 hello 이해 있는지 확인 합니다.

* ExpressRoute 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다. 이 작업이 실패 하면 가상 네트워크가 있는 경우 toosee toohello 회로 연결을 확인 합니다.
* Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨**, 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다. Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.
* Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 hello 회로 삭제할 수 있습니다. Hello 서비스 공급자 프로 비전 상태가 너무 회로 프로 비전이 해제 될 때 설정 됩니다**프로 비전 되지**합니다. 그러면 hello 회로 대 한 청구 되지 않습니다.

Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>다음 단계

회로 만든 후 다음 작업 hello 수행 하면 있는지 확인 합니다.

* [Express 경로 회로의 라우팅 만들기 및 수정](howto-routing-cli.md)
* [가상 네트워크 tooyour ExpressRoute 회로 연결](howto-linkvnet-cli.md)
