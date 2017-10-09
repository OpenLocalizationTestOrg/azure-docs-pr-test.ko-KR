---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: PowerShell: Azure | Microsoft Docs"
description: "이 문서는 가상 toolink (Vnet) tooExpressRoute 회로 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 네트워크 하는 방법의 개요를 제공 합니다."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>가상 네트워크 tooan ExpressRoute 회로 연결
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-linkvnet-classic.md)
>

이 문서를 사용 하면 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결할 수 있습니다. Hello에 수 가상 네트워크가 동일한 구독 또는 다른 구독에 포함 합니다. 또한 이렇게 하면 어떻게 tooupdate 가상 네트워크를 연결 합니다. 

## <a name="before-you-begin"></a>시작하기 전에
* Hello hello Azure PowerShell 모듈의 최신 버전을 설치 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* 검토 hello [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 활성화된 Express 경로 회로가 있어야 합니다. 
  * 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다. 
  * 회로에 구성된 Azure 개인 피어링이 있는지 확인합니다. Hello 참조 [라우팅 구성](expressroute-howto-routing-arm.md) 라우팅 지침에 대 한 문서입니다. 
  * 구성 된 Azure 개인 피어 링 및 종단 간 연결을 사용 하도록 설정할 수 있도록 중일 hello 네트워크와 Microsoft 간에 BGP 피어 링을 확인 합니다.
  * 가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다. 너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 만들](expressroute-howto-add-gateway-resource-manager.md)합니다. ExpressRoute에 대 한 가상 네트워크 게이트웨이 hello GatewayType 'ExpressRoute' 하지 VPN을 사용합니다.

* Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다. 모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우. 

* Hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크를 연결 하거나 hello ExpressRoute premium 추가 기능을 사용 하는 경우 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다. Hello 확인 [FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Hello의 가상 네트워크 연결 동일한 구독 tooa 회로
Hello 다음 cmdlet을 사용 하 여 가상 네트워크 게이트웨이 tooan ExpressRoute 회로 연결할 수 있습니다. 해당 hello 가상 네트워크 게이트웨이 만들어지고 hello cmdlet을 실행 하기 전에 연결을 위한 준비 되어 있는지 확인 합니다.

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>다른 구독 tooa 회로에 가상 네트워크에 연결
여러 구독에서 Express 경로 회로를 공유할 수 있습니다. 다음 그림 hello 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.

사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다. 가 자신의 구독을 사용할 수 각각 hello 부서 hello 조직 내에서 배포를 위한 서비스-있지만 공유할 수 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크입니다. 단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다. Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.

> [!NOTE]
> Hello ExpressRoute 회로 대 한 연결 및 대역폭 요금은 구독 소유자 toohello 적용된 됩니다. Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>관리 - 회로 소유자 및 회로 사용자

'회로 소유자' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다. hello 회로 소유자는 '회로 사용자'가 교환할 수 있는 권한 부여를 만들 수 있습니다. 회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다. 회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.

hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한을 가집니다. 액세스가 해지 된 hello 구독에서 삭제 되 고 모든 링크 연결에는 권한 부여 결과 취소 합니다.

### <a name="circuit-owner-operations"></a>회로 소유자 작업

**toocreate 권한 부여**

hello 회로 소유자는 권한 부여를 만듭니다. 이 인해 hello 생성 될 수 있는 권한 부여 키의 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다. 권한 부여는 하나의 연결에만 유효합니다.

hello cmdlet 조각과 방법을 따르는 toocreate 권한 부여:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


hello 응답 toothis hello 인증 키 및 상태에 포함 됩니다.

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview 권한 부여**

hello 회로 소유자는 hello 다음 cmdlet을 실행 하 여 특정 회로에 발급 한 모든 권한 부여를 검토할 수 있습니다.:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd 권한 부여**

hello 회로 소유자는 hello 다음 cmdlet을 사용 하 여 권한 부여를 추가할 수 있습니다.

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete 권한 부여**

hello 회로 소유자 수 revoke/삭제 권한 부여 toohello 사용자 hello 다음 cmdlet을 실행 하 여:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>회로 사용자 작업

hello 회로 사용자는 hello 피어 ID 및 권한 부여 hello 회로 소유자 로부터 키가 필요합니다. hello 인증 키 GUID입니다.

다음 명령을 hello에서 피어 ID는 확인할 수 있습니다.

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem 연결 권한 부여**

hello 회로 사용자 cmdlet tooredeem 다음 hello 링크 권한 부여를 실행할 수 있습니다.

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease 연결 권한 부여**

Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.

## <a name="modify-a-virtual-network-connection"></a>가상 네트워크 연결 수정
가상 네트워크 연결의 특정 속성을 업데이트할 수 있습니다. 

**tooupdate hello 연결 가중치**

가상 네트워크에 연결 된 toomultiple ExpressRoute 회로 될 수 있습니다. 접두사는 hello에서 하나 이상의 ExpressRoute 회로 나타날 수 있습니다. 변경할 수 있습니다이 접두사에 대 한 연결 toosend 트래픽을 보내는 toochoose, *RoutingWeight* 연결 합니다. 가장 높은 hello로 hello 연결에서 트래픽을 보낼 *RoutingWeight*합니다.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

다양 한 hello *RoutingWeight* 0 too32000 됩니다. hello 기본값은 0입니다.

## <a name="next-steps"></a>다음 단계
ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
