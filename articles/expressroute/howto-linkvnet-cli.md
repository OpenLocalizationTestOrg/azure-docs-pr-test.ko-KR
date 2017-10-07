---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: CLI: Azure | Microsoft Docs"
description: "이 문서는 가상 toolink (Vnet) tooExpressRoute 회로 hello 리소스 관리자 배포 모델 및 CLI를 사용 하 여 네트워크 하는 방법의 개요를 제공 합니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>CLI를 사용 하 여 가상 네트워크 tooan ExpressRoute 회로 연결

이 문서를 사용 하면 CLI를 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결할 수 있습니다. Azure CLI를 사용 하 여 toolink hello 리소스 관리자 배포 모델을 사용 하 여 hello 가상 네트워크를 만들 수 있어야 합니다. Hello에 있어야 하거나 수 동일한 구독 또는 다른 구독에 포함 합니다. 프로그램 VNet tooan ExpressRoute 회로 다른 방법 tooconnect toouse을 원하는 경우 아티클을 hello 다음 목록에서에서 선택할 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>필수 구성 요소

* Hello hello CLI (명령줄 인터페이스)의 최신 버전이 있어야합니다. 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 참조하세요.
* Tooreview hello 필요한 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 활성화된 Express 경로 회로가 있어야 합니다. 
  * 너무 hello 지침에 따라[ExpressRoute 회로 만들기](howto-circuit-cli.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다. 
  * 회로에 구성된 Azure 개인 피어링이 있는지 확인합니다. Hello 참조 [라우팅 구성](howto-routing-cli.md) 라우팅 지침에 대 한 문서입니다. 
  * Azure 개인 피어이링 구성되어 있는지 확인합니다. 종단 간 연결을 사용 하도록 설정할 수 있도록를 hello BGP 피어 링 네트워크와 Microsoft 사이 여야 합니다.
  * 가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다. 너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 구성](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)합니다. 수 있는지 toouse `--gateway-type ExpressRoute`합니다.

* Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다. 모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우. 

* Hello ExpressRoute premium 추가 기능을 사용 하도록 설정 하면 hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크 연결 또는 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다. Hello premium 추가 기능에 대 한 자세한 내용은 참조 hello [FAQ](expressroute-faqs.md)합니다.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Hello의 가상 네트워크 연결 동일한 구독 tooa 회로

Hello 예제를 사용 하 여 가상 네트워크 게이트웨이 tooan ExpressRoute 회로 연결할 수 있습니다. 해당 hello 가상 네트워크 게이트웨이 만들어지고 hello 명령을 실행 하기 전에 연결을 위한 준비 되어 있는지 확인 합니다.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>다른 구독 tooa 회로에 가상 네트워크에 연결

여러 구독에서 Express 경로 회로를 공유할 수 있습니다. 아래 hello 그림 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.

사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다. 가 자신의 구독을 사용할 수 각각 hello 부서 hello 조직 내에서 배포를 위한 서비스-있지만 공유할 수 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크입니다. 단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다. Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.

> [!NOTE]
> Hello 전용 회로 대 한 연결 및 대역폭 요금은 적용된 toohello ExpressRoute 회로 소유자 됩니다. Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>관리 - 회로 소유자 및 회로 사용자

' 회로 소유자 ' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다. hello 회로 소유자는 ' 회로 사용자 '가 교환할 수 있는 권한 부여를 만들 수 있습니다. 회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다. 회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.

hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한 부여에 있습니다. 권한 부여를 취소 하는 경우 모든 링크 연결 액세스가 해지 된 hello 구독에서 삭제 됩니다.

### <a name="circuit-owner-operations"></a>회로 소유자 작업

**toocreate 권한 부여**

hello 회로 소유자는 권한 부여 될 수 있는 인증 키를 만드는 만듭니다 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다. 권한 부여는 하나의 연결에만 유효합니다.

hello 방법을 예제와 다음 toocreate 권한 부여:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

hello 응답 hello 인증 키 및 상태에 포함 되어 있습니다.

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview 권한 부여**

hello 회로 소유자는 다음 예제는 hello를 실행 하 여 특정 회로에 발급 한 모든 권한 부여를 검토할 수 있습니다.:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd 권한 부여**

hello 회로 소유자는 다음 예제는 hello를 사용 하 여 권한 부여를 추가할 수 있습니다.:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete 권한 부여**

회로 소유자 hello 수 revoke/삭제 권한 부여 toohello 사용자 hello 다음 예제를 실행 하 여:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>회로 사용자 작업

hello 회로 사용자 hello 피어 ID 및 hello 회로 소유자에서에서 권한 부여 키가 필요합니다. hello 인증 키 GUID입니다.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem 연결 권한 부여**

hello 회로 사용자 다음 예제에서는 tooredeem hello 링크 권한 부여를 실행할 수 있습니다.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease 연결 권한 부여**

Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.

## <a name="next-steps"></a>다음 단계

ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
